---
title: "Calculadora da Área do Triângulo"
seoTitle: "Calculadora da Área do Triângulo"
description: "Calculadora da Área do Triângulo: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do triângulo com a fórmula."
date: 2026-10-22
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do triângulo", "calculadora da área do triângulo online", "área", "geometria", "calculadora"]
---
<!--SUDAH DIKERJAKAN-->

Basta digitar a base e a altura do triângulo abaixo e depois clicar em **Calcular Área**.

<div id="calc-triangulo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📐 Calculadora da Área do Triângulo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe a base e a altura e veja o resultado na hora.</p>
<label for="tri-base" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Base</label>
<input id="tri-base" type="text" inputmode="decimal" placeholder="Ex.: 10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="tri-altura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura</label>
<input id="tri-altura" type="text" inputmode="decimal" placeholder="Ex.: 6" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="tri-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Área</button>
<button type="button" id="tri-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="tri-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="tri-resultado">preencha os campos e clique em "Calcular Área".</span></div>
</div>
<script>
(function () {
  var base = document.getElementById('tri-base');
  var altura = document.getElementById('tri-altura');
  var resultado = document.getElementById('tri-resultado');
  var caixa = document.getElementById('tri-resposta');
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 6 }); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var b = numero(base.value);
    var h = numero(altura.value);
    if (isNaN(b) || isNaN(h)) { erro('informe números válidos na base e na altura.'); return; }
    if (b <= 0 || h <= 0) { erro('a base e a altura devem ser maiores que zero.'); return; }
    var area = (b * h) / 2;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'A área do triângulo é <strong style="font-size:1.2rem;">' + fmt(area) + '</strong> (unidade²)<br><small style="color:#475569;">A = (' + fmt(b) + ' × ' + fmt(h) + ') ÷ 2 = ' + fmt(area) + '</small>';
  }
  function limpar() {
    base.value = '';
    altura.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular Área".';
    base.focus();
  }
  document.getElementById('tri-calcular').addEventListener('click', calcular);
  document.getElementById('tri-limpar').addEventListener('click', limpar);
  [base, altura].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o comprimento da **Base** do triângulo no primeiro campo.
2. Digite a medida da **Altura** no segundo campo.
3. Clique em **Calcular Área** (ou pressione Enter) para ver o resultado.
4. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`). A base e a altura devem estar na mesma unidade de medida (cm, m, km etc.). O resultado sai na mesma unidade elevada ao quadrado (cm², m², km² etc.).

## Entendendo os termos

- **Triângulo:** polígono de três lados e três ângulos, cuja soma dos ângulos internos é sempre 180°.
- **Base:** qualquer um dos lados do triângulo que se escolhe como referência para o cálculo, normalmente o lado que fica apoiado embaixo.
- **Altura:** distância perpendicular (em ângulo reto) entre a base e o vértice oposto a ela. Nem sempre coincide com um dos lados do triângulo.
- **Área:** medida da superfície ocupada pelo triângulo, ou seja, o espaço dentro dos seus lados.
- **Unidade de medida:** padrão usado para medir a base e a altura, como centímetro (cm) ou metro (m).
- **Unidade quadrada:** unidade em que a área é expressa, como cm² ou m². Ela indica quantos quadrados de 1 unidade de lado cabem dentro da figura.

## Fórmula da área do triângulo

A área do triângulo é a metade do produto entre a base e a altura:

**A = (base × altura) ÷ 2**

Também é comum escrever **A = (b × h) / 2**, em que **b** é a base e **h** é a altura. A divisão por 2 existe porque todo triângulo ocupa metade da área de um retângulo com a mesma base e a mesma altura.

## Exemplo resolvido

Uma vela triangular tem 10 m de base e 6 m de altura. Qual é a sua área?

1. Identifique as medidas: base = 10 m e altura = 6 m.
2. Aplique a fórmula: A = (10 × 6) ÷ 2.
3. Calcule: A = 60 ÷ 2 = 30.

**Resposta:** a área da vela é de **30 m²**.