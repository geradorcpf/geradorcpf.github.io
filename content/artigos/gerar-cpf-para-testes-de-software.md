---
title: "Como gerar CPF para testes de software (QA)"
description: "Boas práticas para usar CPFs gerados em testes: por que evitar CPFs reais, casos de teste importantes e erros comuns ao tratar o CPF."
date: 2026-09-29
---
Em testes de software, use CPFs gerados, e não CPFs de pessoas reais. Um CPF gerado é matematicamente válido, passa nas validações do sistema e não expõe dados de ninguém.

## Por que não usar CPFs reais

CPF é dado pessoal. Usar o CPF de uma pessoa real (o seu, o de um colega ou um copiado da internet) em ambientes de teste cria risco de privacidade e pode acabar misturando dados reais com dados de teste. Prefira números gerados e mantenha o ambiente de teste separado da produção.

Um ponto de atenção: como a geração é aleatória, um CPF gerado pode coincidir com o de uma pessoa real. Por isso, ele serve para testes, nunca para cadastros de verdade.

## Casos de teste que valem a pena

- CPF válido, com pontuação e sem pontuação.
- CPF com dígito verificador errado (troque o último dígito).
- Sequências repetidas, como 111.111.111-11.
- Menos ou mais de 11 dígitos, letras e campo vazio.
- CPF que começa com zero, como 012.345.678-90: confirme que o zero não some.
- CPFs de regiões fiscais diferentes, se o sistema trata o nono dígito. O [gerador de CPF](/) permite escolher o estado.

## Erros comuns

- **Guardar o CPF como número inteiro.** Isso remove os zeros à esquerda. Use texto.
- **Validar só o formato** (a máscara) e esquecer os dígitos verificadores.
- **Reprovar CPF sem pontuação.** Normalize a entrada antes de validar.

## Automatizar

Você pode gerar CPFs direto no código dos testes. Veja funções prontas em [JavaScript, Python e PHP](/artigos/codigo-para-gerar-e-validar-cpf/), e entenda a regra em [como validar um CPF](/artigos/como-validar-cpf/).
