---
title: "Como calcular os dígitos verificadores do CPF (módulo 11)"
description: "Passo a passo para calcular o 10º e o 11º dígito do CPF pelo módulo 11, com exemplo numérico completo e a regra do resto menor que 2."
date: 2026-09-29
---
Os dois últimos dígitos do CPF são calculados a partir dos nove primeiros por uma soma ponderada e pelo resto da divisão por 11, método conhecido como módulo 11. O segundo dígito usa o primeiro no cálculo.

## Regra resumida

1. Multiplique cada dígito por um peso e some os resultados.
2. Divida a soma por 11 e pegue o resto.
3. Se o resto for menor que 2, o dígito é 0. Caso contrário, o dígito é 11 menos o resto.

## Primeiro dígito

Use os 9 primeiros dígitos com pesos de 10 a 2. Para 123.456.789:

| Dígito | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| Peso | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 |
| Produto | 10 | 18 | 24 | 28 | 30 | 30 | 28 | 24 | 18 |

A soma é 210. O resto de 210 dividido por 11 é 1, que é menor que 2, então o primeiro dígito é **0**.

## Segundo dígito

Agora use 10 dígitos (os nove primeiros mais o dígito calculado) com pesos de 11 a 2. Para 1234567890:

11 + 20 + 27 + 32 + 35 + 36 + 35 + 32 + 27 + 0 = 255

O resto de 255 dividido por 11 é 2, e 11 − 2 = **9**. O CPF completo é 123.456.789-09.

## Por que existem dois dígitos

Como 11 é primo, o método detecta erros de digitação e troca de posição entre dígitos. Porém, o cálculo pode resultar em 10, e a Receita Federal determinou que esse valor seja representado por 0. Isso enfraquece um pouco a verificação, e o segundo dígito ajuda a compensar.

## Detalhes úteis

- Existem formulações equivalentes do mesmo cálculo, com pesos em ordem inversa. Todas chegam aos mesmos dígitos.
- O CNPJ usa a mesma ideia, sobre mais dígitos.
- 012.345.678-90 é matematicamente válido, o que mostra que o cálculo aceita números com zero à esquerda.

Veja o código pronto em [JavaScript, Python e PHP](/artigos/codigo-para-gerar-e-validar-cpf/).

## Leia também

- [Como validar um CPF](/artigos/como-validar-cpf/)
- [Estrutura do CPF](/artigos/estrutura-do-cpf/)
