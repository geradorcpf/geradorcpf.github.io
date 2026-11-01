---
title: "Gerador de Inscrição Estadual de Santa Catarina (SC)"
seoTitle: "Gerador de Inscrição Estadual de Santa Catarina (SC)"
description: "Gerador de Inscrição Estadual de Santa Catarina (SC): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "santa catarina", "documentos"]
keywords: ["gerador de inscrição estadual de santa catarina (sc)", "gerador de inscrição estadual de santa catarina (sc) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Gere números de Inscrição Estadual (IE) válidos para Santa Catarina (SC), prontos para usar em testes de software, formulários e bancos de dados de homologação.

<style>
.iesc-box{max-width:520px;margin:1.5rem 0;padding:1.25rem;border:1px solid #d0d7de;border-radius:12px;background:#f8fafc;font-family:inherit;color:#1f2937}
.iesc-title{margin:0 0 1rem;font-size:1.1rem;font-weight:700}
.iesc-label{display:block;margin:0 0 .4rem;font-size:.9rem;font-weight:600}
.iesc-options{display:flex;gap:1rem;margin-bottom:1rem}
.iesc-option{display:flex;align-items:center;gap:.4rem;cursor:pointer;font-size:.95rem}
.iesc-input{width:100%;box-sizing:border-box;padding:.65rem .75rem;border:1px solid #cbd5e1;border-radius:8px;background:#ffffff;font-size:1.1rem;font-weight:600;letter-spacing:.5px;color:#111827}
.iesc-buttons{display:flex;gap:.6rem;margin-top:1rem;flex-wrap:wrap}
.iesc-btn{flex:1;min-width:120px;padding:.65rem 1rem;border:0;border-radius:8px;background:#2563eb;color:#ffffff;font-size:.95rem;font-weight:600;cursor:pointer}
.iesc-btn:hover{background:#1d4ed8}
.iesc-btn-alt{background:#e2e8f0;color:#1f2937}
.iesc-btn-alt:hover{background:#cbd5e1}
.iesc-status{min-height:1.2rem;margin-top:.6rem;font-size:.85rem;color:#16a34a}
</style>
<div class="iesc-box" id="iesc-box">
<p class="iesc-title">Gerador de Inscrição Estadual - SC</p>
<span class="iesc-label">Gerar com pontuação?</span>
<div class="iesc-options">
<label class="iesc-option"><input type="radio" name="iesc-mask" value="sim" checked> Sim</label>
<label class="iesc-option"><input type="radio" name="iesc-mask" value="nao"> Não</label>
</div>
<label class="iesc-label" for="iesc-result">Resultado:</label>
<input class="iesc-input" id="iesc-result" type="text" readonly>
<div class="iesc-buttons">
<button class="iesc-btn" id="iesc-generate" type="button">Gerar Inscrição Estadual</button>
<button class="iesc-btn iesc-btn-alt" id="iesc-copy" type="button">Copiar</button>
</div>
<div class="iesc-status" id="iesc-status"></div>
</div>
<script>
(function () {
  var resultEl = document.getElementById("iesc-result");
  var statusEl = document.getElementById("iesc-status");
  var generateBtn = document.getElementById("iesc-generate");
  var copyBtn = document.getElementById("iesc-copy");
  var maskRadios = document.getElementsByName("iesc-mask");
  var timer = null;
  function showStatus(text) {
    statusEl.textContent = text;
    clearTimeout(timer);
    timer = setTimeout(function () { statusEl.textContent = ""; }, 2000);
  }
  function useMask() {
    for (var i = 0; i !== maskRadios.length; i++) {
      if (maskRadios[i].checked) { return maskRadios[i].value === "sim"; }
    }
    return true;
  }
  function generateIE() {
    var digits = [];
    var sum = 0;
    for (var i = 0; i !== 8; i++) {
      var d = Math.floor(Math.random() * 10);
      digits.push(d);
      sum += d * (9 - i);
    }
    var rest = sum % 11;
    var dv = rest > 1 ? 11 - rest : 0;
    digits.push(dv);
    return digits.join("");
  }
  function formatIE(value) {
    return value.substr(0, 3) + "." + value.substr(3, 3) + "." + value.substr(6, 3);
  }
  function render() {
    var ie = generateIE();
    resultEl.value = useMask() ? formatIE(ie) : ie;
  }
  function fallbackCopy(text) {
    var temp = document.createElement("textarea");
    temp.value = text;
    temp.style.position = "fixed";
    temp.style.opacity = "0";
    document.body.appendChild(temp);
    temp.select();
    var ok = false;
    try { ok = document.execCommand("copy"); } catch (e) { ok = false; }
    document.body.removeChild(temp);
    showStatus(ok ? "Copiado!" : "Não foi possível copiar.");
  }
  function copyResult() {
    var text = resultEl.value;
    if (!text) { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(text).then(
        function () { showStatus("Copiado!"); },
        function () { fallbackCopy(text); }
      );
    } else {
      fallbackCopy(text);
    }
  }
  generateBtn.addEventListener("click", render);
  copyBtn.addEventListener("click", copyResult);
  for (var j = 0; j !== maskRadios.length; j++) {
    maskRadios[j].addEventListener("change", render);
  }
  render();
})();
</script>

> **Importante:** este gerador serve para ajudar estudantes, programadores, analistas e testadores a obter Inscrições Estaduais com formato e dígito verificador válidos para testes. Os números são aleatórios e não pertencem, necessariamente, a empresas reais. O uso indevido dos dados gerados é de responsabilidade do usuário.

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para obter o número com pontos (`000.000.000`) ou **Não** para obter apenas os 9 dígitos.
2. Clique em **Gerar Inscrição Estadual**. Um novo número válido aparece no campo **Resultado**.
3. Clique em **Copiar** para enviar o número para a área de transferência.
4. Cole o número no formulário, na API ou no banco de dados que você está testando.

Ao alternar entre **Sim** e **Não**, um novo número é gerado automaticamente no formato escolhido.

## Como a Inscrição Estadual de SC é formada

A Inscrição Estadual de Santa Catarina possui **9 dígitos**: os 8 primeiros formam o número-base e o último é o dígito verificador. O cálculo é feito assim:

1. Multiplique cada um dos 8 primeiros dígitos pelos pesos **9, 8, 7, 6, 5, 4, 3 e 2**, da esquerda para a direita.
2. Some todos os resultados.
3. Divida a soma por 11 e pegue o **resto**.
4. Se o resto for **0 ou 1**, o dígito verificador é **0**. Caso contrário, o dígito é **11 menos o resto**.

## Glossário

- **Inscrição Estadual (IE):** número de cadastro de uma empresa contribuinte de ICMS na Secretaria da Fazenda do seu estado.
- **SC:** sigla de Santa Catarina, o estado para o qual este gerador cria números.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados e a razão de existir da Inscrição Estadual.
- **SEFAZ:** Secretaria da Fazenda, órgão estadual responsável por emitir e controlar as inscrições.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos anteriores para detectar erros de digitação.
- **Módulo 11:** método de cálculo do dígito verificador que usa o resto da divisão por 11.
- **Peso:** valor pelo qual cada dígito é multiplicado durante o cálculo do dígito verificador.
- **Pontuação (máscara):** os pontos que separam os grupos do número, como em `000.000.000`.
- **Dados de teste:** informações fictícias, mas com formato válido, usadas para testar sistemas sem expor dados reais.
- **Número válido:** número que respeita o formato e o cálculo do dígito verificador; isso não significa que exista de fato na SEFAZ.