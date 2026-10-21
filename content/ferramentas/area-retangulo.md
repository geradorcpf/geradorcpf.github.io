---
title: "Calculadora da Área do Retângulo"
seoTitle: "Calculadora da Área do Retângulo"
description: "Calculadora da Área do Retângulo: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do retângulo com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do retângulo", "calculadora da área do retângulo online", "área", "geometria", "calculadora"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta digitar as laterais do retângulo abaixo e depois clicar em **Calcular Área**.

<div id="calc-retangulo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📐 Calculadora da Área do Retângulo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dois lados e veja o resultado na hora.</p>
<label for="ret-lado-maior" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Lado Maior</label>
<input id="ret-lado-maior" type="text" inputmode="decimal" placeholder="Ex.: 8" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ret-lado-menor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Lado Menor</label>
<input id="ret-lado-menor" type="text" inputmode="decimal" placeholder="Ex.: 5" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ret-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Área</button>
<button type="button" id="ret-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ret-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ret-resultado">preencha os campos e clique em "Calcular Área".</span></div>
</div>
<script>
(function () {
  var maior = document.getElementById('ret-lado-maior');
  var menor = document.getElementById('ret-lado-menor');
  var resultado = document.getElementById('ret-resultado');
  var caixa = document.getElementById('ret-resposta');
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
    var a = numero(maior.value);
    var b = numero(menor.value);
    if (isNaN(a) || isNaN(b)) { erro('informe números válidos nos dois lados.'); return; }
    if (a <= 0 || b <= 0) { erro('os lados devem ser maiores que zero.'); return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'A área do retângulo é <strong style="font-size:1.2rem;">' + fmt(a * b) + '</strong> (unidade²)<br><small style="color:#475569;">A = ' + fmt(a) + ' × ' + fmt(b) + ' = ' + fmt(a * b) + '</small>';
  }
  function limpar() {
    maior.value = '';
    menor.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular Área".';
    maior.focus();
  }
  document.getElementById('ret-calcular').addEventListener('click', calcular);
  document.getElementById('ret-limpar').addEventListener('click', limpar);
  [maior, menor].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o comprimento do **Lado Maior** do retângulo no primeiro campo.
2. Digite o comprimento do **Lado Menor** no segundo campo.
3. Clique em **Calcular Área** (ou pressione Enter) para ver o resultado.
4. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`). Os dois lados devem estar na mesma unidade de medida (cm, m, km etc.). O resultado sai na mesma unidade elevada ao quadrado (cm², m², km² etc.).

## Entendendo os termos

- **Retângulo:** quadrilátero com quatro ângulos retos (90°) e lados opostos com o mesmo comprimento.
- **Lado Maior:** o lado mais longo do retângulo, também chamado de comprimento ou base.
- **Lado Menor:** o lado mais curto do retângulo, também chamado de largura ou altura.
- **Área:** medida da superfície ocupada pelo retângulo, ou seja, o espaço dentro dos seus lados.
- **Unidade de medida:** padrão usado para medir os lados, como centímetro (cm) ou metro (m).
- **Unidade quadrada:** unidade em que a área é expressa, como cm² ou m². Ela indica quantos quadrados de 1 unidade de lado cabem dentro da figura.

## Fórmula da área do retângulo

A área do retângulo é o produto entre os seus dois lados:

**A = lado maior × lado menor**

Também é comum escrever **A = b × h**, em que **b** é a base e **h** é a altura.

## Exemplo resolvido

Um terreno retangular tem 8 m de lado maior e 5 m de lado menor. Qual é a sua área?

1. Identifique os lados: lado maior = 8 m e lado menor = 5 m.
2. Aplique a fórmula: A = 8 × 5.
3. Calcule: A = 40.

**Resposta:** a área do terreno é de **40 m²**.