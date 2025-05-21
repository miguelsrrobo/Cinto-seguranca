# Cinto-seguranca

## 🔹 Objetivo do Projeto

Simular um **sistema digital** que detecta:

* Se o banco está ocupado (com sensor de peso ou presença)
* Se o cinto de segurança está afivelado

E com base nesses sinais, aciona um **aviso luminoso (LED)** ou **buzzer**, indicando se o cinto está ou não corretamente colocado.

---

## 🔹 Entradas e Saída

Conforme os arquivos do repositório, o sistema possui:

### Entradas:

* `ocupado`: sinal que representa se o assento está ocupado (`1` = ocupado, `0` = vazio)
* `cinto`: sinal que representa se o cinto está afivelado (`1` = sim, `0` = não)

### Saída:

* `aviso`: LED ou alarme que acende (`1`) quando há alguém sentado **sem o cinto afivelado**

---

## 🔹 Lógica do sistema

Expressão booleana baseada na regra:

```
aviso = ocupado & ~cinto
```

Ou seja:

* Se **ocupado = 1** e **cinto = 0** ⇒ **aviso = 1**
* Em todos os outros casos, **aviso = 0**

---

## 🔹 Código Verilog (baseado no repositório)

### `cinto_seguranca.v`

```verilog
module cinto_seguranca (
    input wire ocupado,
    input wire cinto,
    output wire aviso
);

assign aviso = ocupado & ~cinto;

endmodule
```

Simples e direto: usa apenas um **AND** e um **NOT**.

---

## 🔹 Testbench (Simulação)

O testbench (`sim/cinto_tb.v`) simula os quatro casos possíveis das entradas:

| Ocupado | Cinto | Aviso |                 |
| ------- | ----- | ----- | --------------- |
| 0       | 0     | 0     |                 |
| 0       | 1     | 0     |                 |
| 1       | 1     | 0     |                 |
| 1       | 0     | 1     | ✅ Alerta ligado |

Trecho do testbench:

```verilog
initial begin
    ocupado = 0; cinto = 0; #10;
    ocupado = 0; cinto = 1; #10;
    ocupado = 1; cinto = 1; #10;
    ocupado = 1; cinto = 0; #10;
end
```

---

## 🔹 Aplicações reais

Esse tipo de sistema é comum em:

* Carros modernos
* Tratores e empilhadeiras (normas de segurança industrial)
* Ônibus escolares
