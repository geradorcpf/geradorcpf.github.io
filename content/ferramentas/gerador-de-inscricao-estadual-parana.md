---
title: "Gerador de Inscrição Estadual do Paraná (PR)"
seoTitle: "Gerador de Inscrição Estadual do Paraná (PR)"
description: "Gerador de Inscrição Estadual do Paraná (PR): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "paraná", "documentos"]
keywords: ["gerador de inscrição estadual do paraná (pr)", "gerador de inscrição estadual do paraná (pr) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se quer a Inscrição Estadual com ou sem pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-pr" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🧾 Gerador de Inscrição Estadual do Paraná (PR)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testar seu software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="display:inline-flex;align-items:center;gap:8px;padding:10px 16px;font-size:1rem;font-weight:600;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;"><input type="radio" name="ie-pontuacao" id="ie-pont-sim" value="sim" checked style="accent-color:#4f46e5;margin:0;">Sim</label>
<label for="ie-pont-nao" style="display:inline-flex;align-items:center;gap:8px;padding:10px 16px;font-size:1rem;font-weight:600;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;"><input type="radio" name="ie-pontuacao" id="ie-pont-nao" value="nao" style="accent-color:#4f46e5;margin:0;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
var botaoGerar = document.getElementById('ie-gerar');
var botaoCopiar = document.getElementById('ie-copiar');
var radioSim = document.getElementById('ie-pont-sim');
var resultado = document.getElementById('ie-resultado');
var caixa = document.getElementById('ie-resposta');
var atual = '';
function digito(nums, pesos) {
var soma = 0;
for (var i = 0; i !== nums.length; i++) { soma += nums[i] * pesos[i]; }
var d = 11 - (soma % 11);
if (d === 10 || d === 11) { d = 0; }
return d;
}
function gerar() {
var base = [];
for (var i = 0; i !== 8; i++) { base.push(Math.floor(Math.random() * 10)); }
var d1 = digito(base, [3, 2, 7, 6, 5, 4, 3, 2]);
var d2 = digito(base.concat([d1]), [4, 3, 2, 7, 6, 5, 4, 3, 2]);
var ie = base.join('') + String(d1) + String(d2);
if (radioSim.checked) {
ie = ie.slice(0, 3) + '.' + ie.slice(3, 8) + '-' + ie.slice(8);
}
return ie;
}
function mostrar() {
atual = gerar();
caixa.style.borderColor = '#86efac';
caixa.style.background = '#f0fdf4';
resultado.style.color = '#166534';
resultado.textContent = atual;
resultado.style.fontWeight = '700';
resultado.style.fontSize = '1.2rem';
resultado.style.letterSpacing = '0.04em';
botaoCopiar.textContent = 'Copiar';
}
function copiar() {
if (atual === '') { mostrar(); }
function ok() {
botaoCopiar.textContent = 'Copiado!';
setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
}
function alternativo() {
var t = document.createElement('textarea');
t.value = atual;
t.style.position = 'fixed';
t.style.opacity = '0';
document.body.appendChild(t);
t.select();
try { document.execCommand('copy'); ok(); } catch (e) { botaoCopiar.textContent = 'Erro'; }
document.body.removeChild(t);
}
if (navigator.clipboard && navigator.clipboard.writeText) {
navigator.clipboard.writeText(atual).then(ok, alternativo);
} else {
alternativo();
}
}
botaoGerar.addEventListener('click', mostrar);
botaoCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com pontos e hífen (por exemplo, `123.45678-50`) ou **Não** para receber apenas os dígitos (`1234567850`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Paraná.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema.
4. Clique em **Gerar Inscrição Estadual** novamente quantas vezes quiser para obter outros números.

**Importante:** os números são gerados de forma aleatória, seguindo apenas a regra matemática de formação da Inscrição Estadual do Paraná. Eles servem para testes de software e não correspondem a empresas reais. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do seu estado, usado para identificá-la como contribuinte do ICMS.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados sobre a venda de mercadorias e alguns serviços.
- **Paraná (PR):** estado brasileiro para o qual o número é gerado. Cada estado tem o seu próprio formato e a sua própria regra de cálculo.
- **Com pontuação:** número escrito com separadores, no formato `XXX.XXXXX-XX`.
- **Sem pontuação:** número escrito apenas com os 10 dígitos, sem pontos nem hífen.
- **Dígitos base:** os 8 primeiros dígitos do número, sorteados aleatoriamente.
- **Dígito verificador:** os 2 últimos dígitos, calculados a partir dos anteriores para confirmar que o número segue a regra.
- **Módulo 11:** cálculo em que cada dígito é multiplicado por um peso, os resultados são somados e dividido por 11. O resto da divisão define o dígito verificador.
- **Número válido:** número que passa na verificação matemática dos dígitos. Ele não prova que a empresa existe nem que está registrada.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar o funcionamento de formulários, sistemas e cadastros.

## Como a Inscrição Estadual do Paraná é formada

A Inscrição Estadual do Paraná tem **10 dígitos**: 8 dígitos base e 2 dígitos verificadores.

**Formato:** `XXX.XXXXX-XX`

1. **Primeiro dígito verificador:** multiplique os 8 dígitos base pelos pesos 3, 2, 7, 6, 5, 4, 3 e 2, some os resultados e calcule o resto da divisão da soma por 11. O dígito é 11 menos o resto. Se o resultado for 10 ou 11, o dígito é 0.
2. **Segundo dígito verificador:** multiplique os 9 dígitos (os 8 base mais o primeiro verificador) pelos pesos 4, 3, 2, 7, 6, 5, 4, 3 e 2 e repita o mesmo cálculo.

## Exemplo resolvido

Considere os dígitos base **12345678**.

1. Primeiro dígito: 1×3 + 2×2 + 3×7 + 4×6 + 5×5 + 6×4 + 7×3 + 8×2 = 138.
2. O resto de 138 ÷ 11 é 6, então o primeiro dígito é 11 − 6 = **5**.
3. Segundo dígito: 1×4 + 2×3 + 3×2 + 4×7 + 5×6 + 6×5 + 7×4 + 8×3 + 5×2 = 166.
4. O resto de 166 ÷ 11 é 1, então o cálculo dá 11 − 1 = 10, e o dígito é **0**.

**Resposta:** a Inscrição Estadual é **1234567850**, ou **123.45678-50** com pontuação.