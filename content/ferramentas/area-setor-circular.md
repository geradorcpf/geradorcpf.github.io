---
title: "Calculadora da Área do Setor Circular"
seoTitle: "Calculadora da Área do Setor Circular"
description: "Calculadora da Área do Setor Circular: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do setor circular com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do setor circular", "calculadora da área do setor circular online", "área", "geometria", "calculadora"]
---
<!--INI SUDAH DIKERJAKAN -->

Basta digitar o raio e o ângulo do setor circular abaixo e depois clicar em **Calcular Área**.

<div id="calc-setor-circular" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📐 Calculadora da Área do Setor Circular</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o raio e o ângulo e veja o resultado na hora.</p>
<label for="set-raio" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Raio</label>
<input id="set-raio" type="text" inputmode="decimal" placeholder="Ex.: 6" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="set-angulo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ângulo (em graus)</label>
<input id="set-angulo" type="text" inputmode="decimal" placeholder="Ex.: 60" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="set-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Área</button>
<button type="button" id="set-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="set-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="set-resultado">preencha os campos e clique em "Calcular Área".</span></div>
</div>
<script>
(function () {
  var raio = document.getElementById('set-raio');
  var angulo = document.getElementById('set-angulo');
  var resultado = document.getElementById('set-resultado');
  var caixa = document.getElementById('set-resposta');
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
    var r = numero(raio.value);
    var a = numero(angulo.value);
    if (isNaN(r) || isNaN(a)) { erro('informe números válidos no raio e no ângulo.'); return; }
    if (r <= 0 || a <= 0) { erro('o raio e o ângulo devem ser maiores que zero.'); return; }
    if (a > 360) { erro('o ângulo deve ser de no máximo 360°.'); return; }
    var area = (a / 360) * Math.PI * r * r;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'A área do setor circular é <strong style="font-size:1.2rem;">' + fmt(area) + '</strong> (unidade²)<br><small style="color:#475569;">A = (' + fmt(a) + ' ÷ 360) × π × ' + fmt(r) + '² = ' + fmt(area) + '</small>';
  }
  function limpar() {
    raio.value = '';
    angulo.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular Área".';
    raio.focus();
  }
  document.getElementById('set-calcular').addEventListener('click', calcular);
  document.getElementById('set-limpar').addEventListener('click', limpar);
  [raio, angulo].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o comprimento do **Raio** do setor circular no primeiro campo.
2. Digite a medida do **Ângulo** do setor, em graus, no segundo campo.
3. Clique em **Calcular Área** (ou pressione Enter) para ver o resultado.
4. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`). O ângulo deve estar em graus e ser maior que 0° e no máximo 360°. O resultado sai na mesma unidade do raio elevada ao quadrado (cm², m², km² etc.).

## Entendendo os termos

- **Círculo:** região do plano formada por todos os pontos que estão a uma mesma distância (o raio) de um ponto central.
- **Setor circular:** "fatia" do círculo delimitada por dois raios e pelo arco entre eles, como uma fatia de pizza.
- **Raio:** distância do centro do círculo até qualquer ponto da sua borda. É também o comprimento dos dois lados retos do setor.
- **Ângulo:** abertura entre os dois raios que formam o setor, medida em graus (°). Um círculo completo tem 360°.
- **Arco:** parte curva da borda do círculo que fecha o setor.
- **π (pi):** constante matemática de valor aproximado 3,14159, que relaciona a circunferência de um círculo ao seu diâmetro.
- **Área:** medida da superfície ocupada pelo setor, ou seja, o espaço dentro dos seus limites.
- **Unidade quadrada:** unidade em que a área é expressa, como cm² ou m². Ela indica quantos quadrados de 1 unidade de lado cabem dentro da figura.

## Fórmula da área do setor circular

A área do setor circular é a fração do círculo que o ângulo representa, multiplicada pela área do círculo inteiro:

**A = (ângulo ÷ 360) × π × raio²**

Também é comum escrever **A = (α ÷ 360) × π × r²**, em que **α** é o ângulo em graus e **r** é o raio.

## Exemplo resolvido

Uma fatia de torta tem formato de setor circular, com 6 cm de raio e ângulo de 60°. Qual é a sua área?

1. Identifique os valores: raio = 6 cm e ângulo = 60°.
2. Aplique a fórmula: A = (60 ÷ 360) × π × 6².
3. Calcule: A = (1 ÷ 6) × π × 36 = 6π ≈ 18,85.

**Resposta:** a área da fatia é de aproximadamente **18,85 cm²**.