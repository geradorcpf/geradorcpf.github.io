---
title: "Gerador de CNH"
seoTitle: "Gerador de CNH"
description: "Gerador de CNH: gere números de CNH válidos para testes. Grátis e online, sem cadastro."
summary: "Gere números de CNH válidos para testes."
date: 2026-10-29
draft: false
category: "documentos"
tags: ["cnh", "veículos", "gerador", "dados de teste", "cpf", "documentos"]
keywords: ["gerador de cnh", "gerador de cnh online", "cnh", "veículos", "gerador"]
---

Basta clicar em **Gerar CNH** abaixo e um novo número de registro válido será criado na hora.

<div id="gerador-cnh" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🪪 Gerador de CNH</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números de CNH válidos para testes.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cnh-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar CNH</button>
<button type="button" id="cnh-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="cnh-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Número de registro da CNH:</strong> <span id="cnh-resultado">clique em "Gerar CNH".</span></div>
</div>
<script>
(function () {
  var resultado = document.getElementById('cnh-resultado');
  var caixa = document.getElementById('cnh-resposta');
  var botaoCopiar = document.getElementById('cnh-copiar');
  var atual = '';
  function digito() { return Math.floor(Math.random() * 10); }
  function gerarNumero() {
    var n;
    do {
      n = Array.from({ length: 9 }, digito);
    } while (n.every(function (d) { return d === n[0]; }));
    var desconto = 0;
    var soma1 = n.reduce(function (s, d, i) { return s + d * (9 - i); }, 0);
    var dv1 = soma1 % 11;
    if (dv1 >= 10) { dv1 = 0; desconto = 2; }
    var soma2 = n.reduce(function (s, d, i) { return s + d * (i + 1); }, 0);
    var dv2 = (soma2 % 11) - desconto;
    if (Math.sign(dv2) === -1) { dv2 += 11; }
    if (dv2 >= 10) { dv2 = 0; }
    return n.join('') + String(dv1) + String(dv2);
  }
  function gerar() {
    atual = gerarNumero();
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = atual;
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '1px';
  }
  function copiarFallback(texto) {
    var ta = document.createElement('textarea');
    ta.value = texto;
    ta.style.position = 'fixed';
    ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(ta);
  }
  function avisoCopiado() {
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiar() {
    if (atual === '') { gerar(); }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).then(avisoCopiado, function () {
        copiarFallback(atual);
        avisoCopiado();
      });
    } else {
      copiarFallback(atual);
      avisoCopiado();
    }
  }
  document.getElementById('cnh-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Clique no botão **Gerar CNH**.
2. O número de registro aparece na caixa de resposta, com 11 dígitos.
3. Clique em **Copiar** para levar o número à área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Clique em **Gerar CNH** novamente sempre que precisar de um novo número.

Os números são gerados de forma aleatória, respeitando a regra de cálculo dos dígitos verificadores. Eles servem apenas para testes de software e não correspondem a nenhuma pessoa real.

## Entendendo os termos

- **CNH:** Carteira Nacional de Habilitação, documento oficial que autoriza uma pessoa a dirigir veículos no Brasil.
- **Número de registro:** sequência de 11 dígitos que identifica a CNH de cada condutor.
- **Dígitos verificadores:** os dois últimos dígitos do número, calculados a partir dos 9 primeiros para confirmar que o número é válido.
- **Número válido:** número que passa no cálculo dos dígitos verificadores, mesmo sem pertencer a uma pessoa real.
- **Dados de teste:** informações fictícias usadas para testar sistemas, formulários e validações sem expor dados reais.
- **Validador de CNH:** ferramenta ou rotina de código que confere se o número informado respeita a regra de cálculo.
- **DETRAN:** órgão estadual de trânsito responsável por emitir e controlar as CNHs.

## Como o número é gerado

O gerador sorteia 9 dígitos aleatórios e calcula os 2 dígitos verificadores com base em somas ponderadas e no resto da divisão por 11:

1. O primeiro dígito verificador usa pesos de 9 a 1 sobre os 9 primeiros dígitos.
2. O segundo dígito verificador usa pesos de 1 a 9 sobre os mesmos dígitos, com ajuste quando o primeiro cálculo passa de 9.
3. Números com todos os dígitos iguais são descartados.

## Aviso importante

Este gerador tem como objetivo ajudar estudantes, programadores, analistas e testadores a obter números de CNH válidos para testar softwares em desenvolvimento. O uso indevido dos dados gerados é de total responsabilidade do usuário.