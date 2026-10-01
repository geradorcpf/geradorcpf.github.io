---
title: "Gerador de CPF"
seoTitle: "Gerador de CPF Válido: gere CPF aleatório online grátis"
description: "Gerador de CPF online: gere um CPF válido e aleatório, com ou sem pontuação e por estado. Grátis, para testes de software."
faq:
  - q: "O CPF gerado é real?"
    a: "Não. Ele é matematicamente válido, mas fictício. Como a combinação é aleatória, pode coincidir com o CPF de uma pessoa real, por isso não deve ser usado em cadastros de verdade."
  - q: "Posso usar o CPF gerado para me cadastrar em sites ou serviços?"
    a: "Não. O gerador serve para testar sistemas, formulários e validações. Usar números gerados para fraude ou identidade falsa é indevido."
  - q: "Como o dígito verificador do CPF é calculado?"
    a: "Cada um dos dois últimos dígitos vem de uma soma ponderada dos dígitos anteriores, com o resto da divisão por 11 (módulo 11). O segundo dígito usa o primeiro no cálculo."
  - q: "O que o nono dígito do CPF indica?"
    a: "A região fiscal em que o CPF foi inscrito. Por isso o gerador permite escolher o estado de origem."
  - q: "Por que 111.111.111-11 é tratado como inválido?"
    a: "Sequências de dígitos repetidos passam na conta do módulo 11, mas costumam ser rejeitadas pelos sistemas na prática. Este gerador evita esse tipo de número."
  - q: "Como gerar vários CPFs de uma vez?"
    a: "Escolha a quantidade (de 1 a 100) antes de clicar em Gerar CPF. Os números saem em lista, sem repetição, e você pode copiar tudo de uma vez."
  - q: "Posso baixar os CPFs gerados em CSV?"
    a: "Sim. Ao gerar mais de um CPF aparece o botão Baixar CSV. O arquivo é montado no seu navegador, sem enviar nada a servidor algum."
  - q: "Como gerar CPF sem pontuação?"
    a: "Marque Não em Gerar com pontuação. O número sai só com os 11 dígitos, no formato usado em campos de banco de dados e APIs."
  - q: "Como gerar um CPF de um estado específico?"
    a: "Escolha o estado em Estado de origem. O gerador usa o nono dígito da região fiscal correspondente, por exemplo 8 para São Paulo."
---

## Gerador de CPF: gere um CPF válido em segundos

Este gerador de CPF cria números com os 11 dígitos no formato correto e com os dois dígitos verificadores calculados pelo mesmo método usado pela Receita Federal. Você pode gerar com ou sem pontuação e escolher o estado de origem. Quem busca por gerador cpf ou gerador de CPF online costuma precisar disso para testar formulários, cadastros e validações.

## O que é um CPF válido?

O número de inscrição no CPF tem onze dígitos: oito são atribuídos de forma aleatória na inscrição, o nono indica a região fiscal e os dois últimos são dígitos verificadores. Um CPF válido é aquele em que esses dois últimos dígitos batem com o cálculo feito sobre os anteriores.

Muita gente pesquisa por “cpf valido” ou “cpf aleatorio valido” sem acento, mas a ideia é a mesma: um número que passa na validação. Ser válido não significa estar registrado em nome de alguém. Para conferir um número, use o [validador de CPF](/validador-de-cpf/).

## Como funciona o gerador de CPF

1. Sorteia oito dígitos.
2. Define o nono dígito: o da região fiscal do estado escolhido, ou aleatório se você deixar “Indiferente”.
3. Calcula o primeiro e o segundo dígito verificador pelo módulo 11.
4. Aplica a pontuação, se você pediu: o número 12345678909 vira 123.456.789-09.

## CPF aleatório válido: para que serve (e para que não serve)

Serve para testes de software, demonstrações, preenchimento de formulários em ambiente de desenvolvimento e aulas de programação. Não serve para cadastros reais, comprovação de identidade ou qualquer tipo de fraude.

## Gerar CPF por estado, sem pontuação e em massa

Além do CPF avulso, o gerador aceita três ajustes que costumam ser pedidos em testes:

- **Por estado:** o nono dígito segue a região fiscal do estado escolhido. A tabela completa está mais abaixo e no artigo sobre a [região fiscal do CPF](/artigos/regiao-fiscal-do-cpf/).
- **Sem pontuação:** só os 11 dígitos, pronto para colar em um campo de banco de dados ou em uma requisição de API.
- **Em massa:** gere até 100 CPFs sem repetição, copie a lista inteira ou baixe em CSV para importar em planilhas e ferramentas de teste.

## Boas práticas ao usar CPF gerado em testes

Use sempre números gerados em ambientes de teste e mantenha-os separados da produção. O artigo [como gerar CPF para testes de software](/artigos/gerar-cpf-para-testes-de-software/) lista os casos de teste mais úteis, e quem precisa implementar a conta pode ver o [código para gerar e validar CPF](/artigos/codigo-para-gerar-e-validar-cpf/). Para checar um número que você já tem, use o [validador de CPF](/validador-de-cpf/).

## CPF válido não é CPF existente

A conta do módulo 11 só detecta erro de digitação. Um número pode passar na validação e não estar inscrito em nenhum cadastro, ou coincidir com o de uma pessoa real. Quem precisa conferir a situação de um CPF de verdade deve seguir o passo a passo em [como consultar a situação do CPF](/artigos/como-consultar-a-situacao-do-cpf/), direto no site da Receita Federal.

## CPF generator: how it works

This CPF generator produces random Brazilian taxpayer numbers that pass the standard check-digit validation (modulo 11). The numbers are fictional and meant only for software testing and development.

## Estrutura do CPF e região fiscal

O nono dígito indica a região fiscal responsável pela inscrição:

| Nono dígito | Estados |
|---|---|
| 1 | DF, GO, MT, MS, TO |
| 2 | AC, AP, AM, PA, RO, RR |
| 3 | CE, MA, PI |
| 4 | AL, PB, PE, RN |
| 5 | BA, SE |
| 6 | MG |
| 7 | ES, RJ |
| 8 | SP |
| 9 | PR, SC |
| 0 | RS |

## Infográfico: CPF, muito além de 11 números

{{< infographic >}}
