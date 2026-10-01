---
title: "Como validar um CPF: passo a passo"
description: "Aprenda a checar se um CPF é válido: limpar a pontuação, conferir o tamanho, recalcular os dígitos e entender o que a validação não prova."
date: 2026-09-29
---
Validar um CPF é recalcular os dois dígitos verificadores e comparar com os que foram informados. Se baterem, o número é matematicamente válido. Para conferir agora, use o [validador de CPF online](/validador-de-cpf/).

## Passo a passo

1. **Remova a pontuação.** Deixe só os dígitos: 123.456.789-09 vira 12345678909.
2. **Confira o tamanho.** Precisam ser exatamente 11 dígitos, sem letras.
3. **Rejeite sequências repetidas.** 111.111.111-11 e similares passam na conta, mas os sistemas costumam tratá-los como inválidos.
4. **Recalcule o 10º dígito** a partir dos nove primeiros e compare.
5. **Recalcule o 11º dígito** a partir dos dez primeiros e compare.

O cálculo está explicado em [como calcular os dígitos verificadores](/artigos/como-calcular-digitos-verificadores-cpf/).

## O que a validação não prova

Um CPF válido não significa que ele existe na base da Receita Federal, que pertence a uma pessoa específica ou que está regular. A conta só detecta erros de digitação. Para saber a situação de um CPF é preciso [consultar a Receita Federal](/artigos/como-consultar-a-situacao-do-cpf/), com número e data de nascimento.

## Erros comuns ao validar

- **Guardar o CPF como número.** Um CPF pode começar com zero (como 012.345.678-90). Trate sempre como texto.
- **Aceitar só o formato com pontos.** Aceite as duas formas e normalize antes de validar.
- **Achar que válido é real.** Um número gerado ao acaso pode ser válido e mesmo assim não ter dono.

Para implementar, veja o [código em JavaScript, Python e PHP](/artigos/codigo-para-gerar-e-validar-cpf/).
