---
title: "Gerador de Inscrição Estadual do Espírito Santo (ES)"
seoTitle: "Gerador de Inscrição Estadual do Espírito Santo (ES)"
description: "Gerador de Inscrição Estadual do Espírito Santo (ES): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "espírito santo", "documentos"]
keywords: ["gerador de inscrição estadual do espírito santo (es)", "gerador de inscrição estadual do espírito santo (es) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

<style>
.ie-tool{max-width:560px;margin:0 auto 24px;padding:20px;border:1px solid #e2e8f0;border-radius:12px;background:#ffffff;box-shadow:0 1px 3px rgba(0,0,0,0.08);font-family:inherit;color:#1f2937;box-sizing:border-box}
.ie-tool *{box-sizing:border-box}
.ie-tool .ie-row{margin-bottom:16px}
.ie-tool .ie-label{display:block;margin-bottom:6px;font-size:14px;font-weight:600;color:#374151}
.ie-tool .ie-options{display:flex;gap:16px;flex-wrap:wrap}
.ie-tool .ie-options label{display:inline-flex;align-items:center;gap:6px;font-size:15px;cursor:pointer}
.ie-tool .ie-input{width:100%;padding:10px 12px;font-size:16px;border:1px solid #cbd5e1;border-radius:8px;background:#f8fafc;color:#111827}
.ie-tool .ie-input:focus{outline:2px solid #3b82f6;border-color:#3b82f6}
.ie-tool .ie-actions{display:flex;gap:10px;flex-wrap:wrap}
.ie-tool .ie-btn{padding:10px 18px;font-size:15px;font-weight:600;border:0;border-radius:8px;cursor:pointer;background:#2563eb;color:#ffffff}
.ie-tool .ie-btn:hover{background:#1d4ed8}
.ie-tool .ie-btn.ie-secondary{background:#e2e8f0;color:#1f2937}
.ie-tool .ie-btn.ie-secondary:hover{background:#cbd5e1}
.ie-tool .ie-result{margin-top:16px;padding:14px;border-radius:8px;background:#f1f5f9;text-align:center}
.ie-tool .ie-result-label{font-size:13px;color:#64748b;margin-bottom:4px}
.ie-tool .ie-result-value{font-size:24px;font-weight:700;letter-spacing:1px;color:#0f172a;word-break:break-all}
.ie-tool .ie-msg{margin-top:8px;font-size:13px;color:#16a34a;min-height:18px;text-align:center}
</style>
<div class="ie-tool" id="ie-tool">
<div class="ie-row">
<span class="ie-label">Gerar com pontuação?</span>
<div class="ie-options">
<label><input type="radio" name="ie-punct" value="yes" checked> Sim</label>
<label><input type="radio" name="ie-punct" value="no"> Não</label>
</div>
</div>
<div class="ie-row">
<label class="ie-label" for="ie-state">Estado</label>
<input class="ie-input" id="ie-state" type="text" value="ES - Espírito Santo" readonly>
</div>
<div class="ie-actions">
<button type="button" class="ie-btn" id="ie-generate">Gerar Inscrição Estadual</button>
<button type="button" class="ie-btn ie-secondary" id="ie-copy">Copiar</button>
</div>
<div class="ie-result">
<div class="ie-result-label">Resposta:</div>
<div class="ie-result-value" id="ie-result">-</div>
</div>
<div class="ie-msg" id="ie-msg"></div>
<script>
(function () {
var WEIGHTS = [9, 8, 7, 6, 5, 4, 3, 2];
var current = "";
var resultEl = document.getElementById("ie-result");
var msgEl = document.getElementById("ie-msg");
function randomBase() {
var digits = [];
for (var i = 0; i !== 8; i += 1) {
digits.push(Math.floor(Math.random() * 10));
}
return digits;
}
function checkDigit(digits) {
var sum = digits.reduce(function (acc, d, idx) {
return acc + d * WEIGHTS[idx];
}, 0);
var rest = sum % 11;
return rest > 1 ? 11 - rest : 0;
}
function format(raw) {
return raw.slice(0, 3) + "." + raw.slice(3, 6) + "." + raw.slice(6, 8) + "-" + raw.slice(8);
}
function usePunctuation() {
var checked = document.querySelector('input[name="ie-punct"]:checked');
return checked ? checked.value === "yes" : true;
}
function render() {
if (!current) {
return;
}
resultEl.textContent = usePunctuation() ? format(current) : current;
}
function generate() {
var base = randomBase();
current = base.join("") + String(checkDigit(base));
msgEl.textContent = "";
render();
}
function fallbackCopy(text) {
var area = document.createElement("textarea");
area.value = text;
area.style.position = "fixed";
area.style.opacity = "0";
document.body.appendChild(area);
area.select();
var ok = false;
try {
ok = document.execCommand("copy");
} catch (e) {
ok = false;
}
document.body.removeChild(area);
return ok;
}
function copy() {
if (!current) {
msgEl.textContent = "Gere um número primeiro.";
return;
}
var text = resultEl.textContent;
var done = function () {
msgEl.textContent = "Copiado!";
};
if (navigator.clipboard && navigator.clipboard.writeText) {
navigator.clipboard.writeText(text).then(done, function () {
if (fallbackCopy(text)) {
done();
}
});
} else if (fallbackCopy(text)) {
done();
}
}
document.getElementById("ie-generate").addEventListener("click", generate);
document.getElementById("ie-copy").addEventListener("click", copy);
var radios = document.querySelectorAll('input[name="ie-punct"]');
Array.prototype.forEach.call(radios, function (r) {
r.addEventListener("change", render);
});
})();
</script>
</div>

> **Importante:** este gerador online de Inscrições Estaduais ajuda estudantes, programadores, analistas e testadores a gerar números válidos, normalmente necessários para testar softwares em desenvolvimento. Os números são gerados de forma aleatória, respeitando a regra de criação do Espírito Santo. O uso indevido dos dados gerados é de total responsabilidade do usuário.

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para o formato com máscara (`999.999.99-9`) ou **Não** para apenas os 9 dígitos.
2. Clique em **Gerar Inscrição Estadual**. Um novo número válido para o Espírito Santo aparece em **Resposta**.
3. Alterne entre **Sim** e **Não** a qualquer momento para ver o mesmo número com ou sem pontuação.
4. Clique em **Copiar** para enviar o número à área de transferência e cole no formulário ou sistema que você está testando.
5. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

## Como o número é gerado

A Inscrição Estadual do Espírito Santo tem 9 dígitos: 8 dígitos-base aleatórios e 1 dígito verificador no final.

1. Cada um dos 8 dígitos-base é multiplicado pelos pesos 9, 8, 7, 6, 5, 4, 3 e 2, da esquerda para a direita.
2. Os resultados são somados.
3. Divide-se a soma por 11 e pega-se o resto.
4. Se o resto for menor que 2, o dígito verificador é 0. Caso contrário, o dígito verificador é 11 menos o resto.

## Glossário

- **Inscrição Estadual (IE):** número de registro de uma empresa contribuinte do ICMS na Secretaria da Fazenda do seu estado.
- **ES:** sigla do Espírito Santo, estado cuja regra de formação é usada neste gerador.
- **Pontuação (máscara):** pontos e hífen que separam os dígitos para facilitar a leitura. No ES, o formato é `999.999.99-9`.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos anteriores para detectar erros de digitação ou números inventados.
- **Dígitos-base:** os 8 primeiros dígitos, gerados aleatoriamente.
- **Pesos:** multiplicadores (9 a 2) aplicados a cada dígito-base no cálculo do dígito verificador.
- **Módulo 11:** método que usa o resto da divisão por 11 para obter o dígito verificador.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, de competência estadual, que exige a Inscrição Estadual.
- **Dados de teste:** números válidos na forma, mas fictícios, usados para testar sistemas sem expor dados reais.