---
title: "Calculadora da Área do Trapézio"
seoTitle: "Calculadora da Área do Trapézio"
description: "Calculadora da Área do Trapézio: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do trapézio com a fórmula."
date: 2026-10-22
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do trapézio", "calculadora da área do trapézio online", "área", "geometria", "calculadora"]
---
<!--SUDAH DIKERJAKAN-->

Basta digitar as bases e a altura do trapézio abaixo e depois clicar em **Calcular Área**.

<div id="calc-trapezio" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📐 Calculadora da Área do Trapézio</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe as bases e a altura e veja o resultado na hora.</p>
<label for="trap-base-maior" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Base Maior</label>
<input id="trap-base-maior" type="text" inputmode="decimal" placeholder="Ex.: 10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="trap-base-menor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Base Menor</label>
<input id="trap-base-menor" type="text" inputmode="decimal" placeholder="Ex.: 6" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="trap-altura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura do trapézio</label>
<input id="trap-altura" type="text" inputmode="decimal" placeholder="Ex.: 4" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="trap-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Área</button>
<button type="button" id="trap-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="trap-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="trap-resultado">preencha os campos e clique em "Calcular Área".</span></div>
</div>
<script>
(function () {
  var baseMaior = document.getElementById('trap-base-maior');
  var baseMenor = document.getElementById('trap-base-menor');
  var altura = document.getElementById('trap-altura');
  var resultado = document.getElementById('trap-resultado');
  var caixa = document.getElementById('trap-resposta');
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
    var B = numero(baseMaior.value);
    var b = numero(baseMenor.value);
    var h = numero(altura.value);
    if (isNaN(B) || isNaN(b) || isNaN(h)) { erro('informe números válidos nos três campos.'); return; }
    if (B <= 0 || b <= 0 || h <= 0) { erro('as bases e a altura devem ser maiores que zero.'); return; }
    var area = ((B + b) * h) / 2;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'A área do trapézio é <strong style="font-size:1.2rem;">' + fmt(area) + '</strong> (unidade²)<br><small style="color:#475569;">A = (' + fmt(B) + ' + ' + fmt(b) + ') × ' + fmt(h) + ' ÷ 2 = ' + fmt(area) + '</small>';
  }
  function limpar() {
    baseMaior.value = '';
    baseMenor.value = '';
    altura.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular Área".';
    baseMaior.focus();
  }
  document.getElementById('trap-calcular').addEventListener('click', calcular);
  document.getElementById('trap-limpar').addEventListener('click', limpar);
  [baseMaior, baseMenor, altura].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o comprimento da **Base Maior** do trapézio no primeiro campo.
2. Digite o comprimento da **Base Menor** no segundo campo.
3. Digite a **Altura do trapézio** no terceiro campo.
4. Clique em **Calcular Área** (ou pressione Enter) para ver o resultado.
5. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`). As duas bases e a altura devem estar na mesma unidade de medida (cm, m, km etc.). O resultado sai na mesma unidade elevada ao quadrado (cm², m², km² etc.).

## Entendendo os termos

- **Trapézio:** quadrilátero que tem um par de lados paralelos, chamados de bases.
- **Base Maior:** o lado paralelo mais longo do trapézio, representado pela letra **B**.
- **Base Menor:** o lado paralelo mais curto do trapézio, representado pela letra **b**.
- **Altura:** distância perpendicular entre as duas bases, representada pela letra **h**. Não é o comprimento dos lados inclinados.
- **Área:** medida da superfície ocupada pelo trapézio, ou seja, o espaço dentro dos seus lados.
- **Unidade de medida:** padrão usado para medir as bases e a altura, como centímetro (cm) ou metro (m).
- **Unidade quadrada:** unidade em que a área é expressa, como cm² ou m². Ela indica quantos quadrados de 1 unidade de lado cabem dentro da figura.

## Fórmula da área do trapézio

A área do trapézio é a soma das bases multiplicada pela altura, dividida por 2:

**A = (B + b) × h ÷ 2**

Em que **B** é a base maior, **b** é a base menor e **h** é a altura.

## Exemplo resolvido

Um terreno em forma de trapézio tem base maior de 10 m, base menor de 6 m e altura de 4 m. Qual é a sua área?

1. Identifique as medidas: B = 10 m, b = 6 m e h = 4 m.
2. Aplique a fórmula: A = (10 + 6) × 4 ÷ 2.
3. Some as bases: A = 16 × 4 ÷ 2.
4. Multiplique e divida: A = 64 ÷ 2 = 32.

**Resposta:** a área do terreno é de **32 m²**.