---
title: "Gerador de Inscrição Estadual de Pernambuco (PE)"
seoTitle: "Gerador de Inscrição Estadual de Pernambuco (PE)"
description: "Gerador de Inscrição Estadual de Pernambuco (PE): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "pernambuco", "documentos"]
keywords: ["gerador de inscrição estadual de pernambuco (pe)", "gerador de inscrição estadual de pernambuco (pe) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Use o gerador abaixo para criar números de Inscrição Estadual de Pernambuco (PE) válidos, ideais para testar formulários, cadastros e validações em softwares em desenvolvimento.

<style>
.ie-card{max-width:640px;margin:1.5rem 0;padding:1.5rem;background:#ffffff;color:#1e293b;border:1px solid #e2e8f0;border-radius:12px;box-shadow:0 2px 8px rgba(15,23,42,.06);font-family:inherit;box-sizing:border-box}
.ie-card *{box-sizing:border-box}
.ie-group{margin-bottom:1.1rem}
.ie-label{display:block;margin-bottom:.45rem;font-size:.95rem;font-weight:600;color:#334155}
.ie-radios{display:flex;flex-wrap:wrap;gap:1.25rem}
.ie-radios label{display:inline-flex;align-items:center;gap:.4rem;font-size:.95rem;cursor:pointer}
.ie-input{width:100%;padding:.7rem .85rem;font-size:1.15rem;font-family:inherit;color:#1e293b;background:#f8fafc;border:1px solid #cbd5e1;border-radius:8px}
.ie-input:focus{outline:2px solid #3b82f6;outline-offset:1px;border-color:#3b82f6}
.ie-fixed{background:#f1f5f9;color:#475569}
.ie-actions{display:flex;flex-wrap:wrap;gap:.6rem;margin-top:.25rem}
.ie-btn{padding:.7rem 1.3rem;font-size:.95rem;font-weight:600;font-family:inherit;border:0;border-radius:8px;cursor:pointer;transition:background .15s ease}
.ie-btn-primary{background:#2563eb;color:#ffffff}
.ie-btn-primary:hover{background:#1d4ed8}
.ie-btn-secondary{background:#e2e8f0;color:#1e293b}
.ie-btn-secondary:hover{background:#cbd5e1}
.ie-status{min-height:1.3rem;margin:.75rem 0 0;font-size:.875rem;color:#16a34a}
.ie-note{margin:1rem 0 0;padding:.75rem 1rem;font-size:.85rem;line-height:1.5;color:#475569;background:#f8fafc;border-left:4px solid #94a3b8;border-radius:4px}
</style>
<div class="ie-card" id="ie-tool">
<div class="ie-group">
<span class="ie-label">Gerar com pontuação?</span>
<div class="ie-radios">
<label><input type="radio" name="ie-punct" id="ie-punct-yes" value="yes" checked> Sim</label>
<label><input type="radio" name="ie-punct" id="ie-punct-no" value="no"> Não</label>
</div>
</div>
<div class="ie-group">
<label class="ie-label" for="ie-state">Estado</label>
<input type="text" id="ie-state" class="ie-input ie-fixed" value="PE - Pernambuco" readonly>
</div>
<div class="ie-group">
<label class="ie-label" for="ie-result">Resposta</label>
<input type="text" id="ie-result" class="ie-input" readonly placeholder="Clique em Gerar Inscrição Estadual">
</div>
<div class="ie-actions">
<button type="button" id="ie-generate" class="ie-btn ie-btn-primary">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copy" class="ie-btn ie-btn-secondary">Copiar</button>
</div>
<p class="ie-status" id="ie-status" aria-live="polite"></p>
<p class="ie-note"><strong>Importante:</strong> este gerador ajuda estudantes, programadores, analistas e testadores a obter Inscrições Estaduais válidas para testar softwares em desenvolvimento. Os números são aleatórios e seguem a regra de cálculo do dígito verificador, mas não pertencem a empresas reais. O uso indevido dos dados gerados é de responsabilidade do usuário.</p>
</div>
<script>
(function () {
var resultEl = document.getElementById('ie-result');
var statusEl = document.getElementById('ie-status');
var yesEl = document.getElementById('ie-punct-yes');
var timer = null;
function randomDigit() {
return Math.floor(Math.random() * 10);
}
function calcDv(digits) {
var weight = digits.length + 1;
var sum = 0;
var i;
for (i = 0; digits.length > i; i++) {
sum += digits[i] * (weight - i);
}
var rest = sum % 11;
if (2 > rest) {
return 0;
}
return 11 - rest;
}
function generate() {
var digits = [];
var i;
for (i = 0; 7 > i; i++) {
digits.push(randomDigit());
}
var base = digits.join('');
var dv1 = calcDv(digits);
digits.push(dv1);
var dv2 = calcDv(digits);
if (yesEl.checked) {
return base + '-' + dv1 + dv2;
}
return base + dv1 + dv2;
}
function showStatus(text) {
statusEl.textContent = text;
if (timer) {
clearTimeout(timer);
}
timer = setTimeout(function () {
statusEl.textContent = '';
}, 2000);
}
function fallbackCopy() {
resultEl.focus();
resultEl.select();
var ok = false;
try {
ok = document.execCommand('copy');
} catch (err) {
ok = false;
}
showStatus(ok ? 'Copiado!' : 'Não foi possível copiar.');
}
function copyResult() {
if (!resultEl.value) {
showStatus('Gere uma inscrição primeiro.');
return;
}
if (navigator.clipboard) {
navigator.clipboard.writeText(resultEl.value).then(function () {
showStatus('Copiado!');
}, fallbackCopy);
} else {
fallbackCopy();
}
}
function run() {
resultEl.value = generate();
}
document.getElementById('ie-generate').addEventListener('click', run);
document.getElementById('ie-copy').addEventListener('click', copyResult);
yesEl.addEventListener('change', run);
document.getElementById('ie-punct-no').addEventListener('change', run);
run();
})();
</script>

## Como usar o gerador

1. Escolha se deseja gerar a Inscrição Estadual **com pontuação** (formato `0000000-00`) ou **sem pontuação** (apenas números, `000000000`).
2. Confira o estado: este gerador é fixo para **Pernambuco (PE)**.
3. Clique em **Gerar Inscrição Estadual**. Um novo número válido aparece no campo **Resposta**.
4. Clique em **Copiar** para levar o número à área de transferência e cole no sistema ou formulário que você está testando.
5. Repita quantas vezes precisar. Cada clique gera um número diferente.

## Como a inscrição é composta

A Inscrição Estadual de Pernambuco, no padrão atual, tem **9 dígitos**: os 7 primeiros são o número-base, gerado de forma aleatória, e os 2 últimos são os dígitos verificadores, calculados a partir deles.

- **1º dígito verificador:** multiplique os 7 dígitos do número-base pelos pesos 8, 7, 6, 5, 4, 3 e 2, some os resultados e calcule o resto da divisão por 11. Se o resto for 0 ou 1, o dígito é 0. Nos demais casos, o dígito é 11 menos o resto.
- **2º dígito verificador:** repita o cálculo com os 8 dígitos já obtidos (base + 1º dígito) e os pesos 9, 8, 7, 6, 5, 4, 3 e 2, aplicando a mesma regra do resto.

## Glossário

- **Inscrição Estadual (IE):** número de cadastro de uma empresa contribuinte do ICMS na Secretaria da Fazenda do seu estado. Cada estado tem seu próprio formato e regra de cálculo.
- **Pernambuco (PE):** estado brasileiro para o qual este gerador cria os números, seguindo as regras definidas pela Secretaria da Fazenda estadual.
- **SEFAZ-PE:** Secretaria da Fazenda de Pernambuco, órgão responsável por cadastrar contribuintes e emitir a Inscrição Estadual no estado.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, tributo estadual que torna obrigatória a Inscrição Estadual para as empresas contribuintes.
- **Contribuinte:** pessoa jurídica ou empresário individual que realiza operações sujeitas ao ICMS.
- **Número-base:** os 7 primeiros dígitos da inscrição, que identificam o contribuinte e, neste gerador, são sorteados aleatoriamente.
- **Dígito verificador (DV):** dígitos finais calculados a partir dos anteriores, usados para detectar erros de digitação e validar o número.
- **Módulo 11:** método de cálculo em que a soma ponderada dos dígitos é dividida por 11 e o resto define o dígito verificador.
- **Pesos:** multiplicadores aplicados a cada dígito, em ordem decrescente, durante o cálculo do dígito verificador.
- **Pontuação (máscara):** formatação visual do número, com hífen separando o número-base dos dígitos verificadores (por exemplo, `0000000-00`).
- **Dados de teste:** informações fictícias, mas com formato válido, usadas para testar sistemas sem expor dados reais de empresas.
- **Validação:** verificação feita por um sistema para confirmar se o número respeita o formato e o cálculo dos dígitos verificadores.