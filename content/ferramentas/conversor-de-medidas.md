---
title: "Conversor de Medidas"
seoTitle: "Conversor de Medidas: online e grátis"
description: "Conversor de Medidas: converta comprimento, peso, volume e outras unidades. Grátis e online, sem cadastro."
summary: "Converta comprimento, peso, volume e outras unidades."
date: 2026-10-25
draft: false
category: "matematica"
tags: ["medidas", "unidades", "conversão", "matemática"]
keywords: ["conversor de medidas", "conversor de medidas online", "medidas", "unidades", "conversão"]
---

<!--sudah dikerjakan-->

Basta escolher o tipo de medida abaixo e digitar um valor em qualquer campo. Os outros campos são convertidos na hora.

<div id="calc-medidas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📏 Conversor de Medidas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o tipo de medida e digite o valor em qualquer unidade.</p>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Medida</span>
<div id="med-categorias" style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px;"></div>
<div id="med-campos"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:4px;">
<button type="button" id="med-limpar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Limpar</button>
</div>
<div id="med-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="med-resultado">digite um valor em qualquer campo para converter.</span></div>
</div>
<script>
(function () {
  var categorias = [
    { id: 'comprimento', nome: 'Comprimento', unidades: [
      { n: 'Quilômetro (km)', f: 1000 },
      { n: 'Metro (m)', f: 1 },
      { n: 'Centímetro (cm)', f: 0.01 },
      { n: 'Milha (mi)', f: 1609.344 },
      { n: 'Pé (ft)', f: 0.3048 },
      { n: 'Polegada (in)', f: 0.0254 }
    ] },
    { id: 'massa', nome: 'Massa', unidades: [
      { n: 'Tonelada (t)', f: 1000 },
      { n: 'Quilograma (kg)', f: 1 },
      { n: 'Grama (g)', f: 0.001 },
      { n: 'Miligrama (mg)', f: 0.000001 },
      { n: 'Libra (lb)', f: 0.45359237 },
      { n: 'Onça (oz)', f: 0.028349523125 }
    ] },
    { id: 'temperatura', nome: 'Temperatura', unidades: [
      { n: 'Celsius (°C)', para: function (v) { return v; }, de: function (b) { return b; } },
      { n: 'Fahrenheit (°F)', para: function (v) { return (v - 32) * 5 / 9; }, de: function (b) { return b * 9 / 5 + 32; } },
      { n: 'Kelvin (K)', para: function (v) { return v - 273.15; }, de: function (b) { return b + 273.15; } }
    ] },
    { id: 'tempo', nome: 'Tempo', unidades: [
      { n: 'Semana (sem)', f: 604800 },
      { n: 'Dia (d)', f: 86400 },
      { n: 'Hora (h)', f: 3600 },
      { n: 'Minuto (min)', f: 60 },
      { n: 'Segundo (s)', f: 1 },
      { n: 'Milissegundo (ms)', f: 0.001 }
    ] },
    { id: 'velocidade', nome: 'Velocidade', unidades: [
      { n: 'Quilômetro por hora (km/h)', f: 1 / 3.6 },
      { n: 'Metro por segundo (m/s)', f: 1 },
      { n: 'Milha por hora (mph)', f: 0.44704 },
      { n: 'Nó (kn)', f: 1852 / 3600 },
      { n: 'Pé por segundo (ft/s)', f: 0.3048 }
    ] }
  ];
  var estLabel = 'display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;';
  var estInput = 'width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;';
  var estAtivo = 'padding:10px 14px;font-size:0.95rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid #4f46e5;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);';
  var estInativo = 'padding:10px 14px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
  var boxCategorias = document.getElementById('med-categorias');
  var boxCampos = document.getElementById('med-campos');
  var resultado = document.getElementById('med-resultado');
  var caixa = document.getElementById('med-resposta');
  var atual = categorias[0];
  var inputs = [];
  var botoes = [];
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') !== -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 4, useGrouping: false }); }
  function paraBase(u, v) { return u.f !== undefined ? v * u.f : u.para(v); }
  function deBase(u, b) { return u.f !== undefined ? b / u.f : u.de(b); }
  function neutro() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'digite um valor em qualquer campo para converter.';
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function ok(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = msg;
  }
  function converter(idx) {
    var texto = inputs[idx].value;
    var v = numero(texto);
    inputs.forEach(function (campo, j) { if (j !== idx) { campo.value = ''; } });
    if (String(texto).trim() === '') { neutro(); return; }
    if (isNaN(v)) { erro('informe um número válido.'); return; }
    var base = paraBase(atual.unidades[idx], v);
    inputs.forEach(function (campo, j) {
      if (j !== idx) { campo.value = fmt(deBase(atual.unidades[j], base)); }
    });
    ok('conversão atualizada. Valores arredondados para até 4 casas decimais.');
  }
  function montarCampos() {
    while (boxCampos.firstChild) { boxCampos.removeChild(boxCampos.firstChild); }
    inputs = [];
    atual.unidades.forEach(function (u, i) {
      var id = 'med-u-' + i;
      var label = document.createElement('label');
      label.setAttribute('for', id);
      label.setAttribute('style', estLabel);
      label.textContent = u.n;
      var campo = document.createElement('input');
      campo.id = id;
      campo.type = 'text';
      campo.setAttribute('inputmode', 'decimal');
      campo.setAttribute('autocomplete', 'off');
      campo.setAttribute('style', estInput);
      campo.addEventListener('input', function () { converter(i); });
      campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
      campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
      boxCampos.appendChild(label);
      boxCampos.appendChild(campo);
      inputs.push(campo);
    });
    neutro();
  }
  function marcarBotoes() {
    botoes.forEach(function (b, i) {
      b.setAttribute('style', categorias[i] === atual ? estAtivo : estInativo);
    });
  }
  function escolher(cat) {
    atual = cat;
    marcarBotoes();
    montarCampos();
  }
  categorias.forEach(function (cat) {
    var b = document.createElement('button');
    b.type = 'button';
    b.textContent = cat.nome;
    b.addEventListener('click', function () { escolher(cat); });
    boxCategorias.appendChild(b);
    botoes.push(b);
  });
  document.getElementById('med-limpar').addEventListener('click', function () {
    inputs.forEach(function (campo) { campo.value = ''; });
    neutro();
    if (inputs.length) { inputs[0].focus(); }
  });
  escolher(atual);
})();
</script>

## Como usar o conversor

1. Clique no tipo de **Medida** que você quer converter: Comprimento, Massa, Temperatura, Tempo ou Velocidade.
2. Digite o valor em qualquer um dos campos, na unidade que você já tem.
3. Veja os demais campos serem preenchidos automaticamente com o valor convertido.
4. Para converter outro valor, basta digitar em outro campo ou usar o botão **Limpar**.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`). Na temperatura, também é possível digitar valores negativos. Os resultados são arredondados para até 4 casas decimais.

## Entendendo os termos

- **Medida:** tipo de grandeza que será convertida, como comprimento, massa, temperatura, tempo ou velocidade.
- **Unidade de medida:** padrão usado para expressar uma grandeza, como o metro para comprimento ou o quilograma para massa.
- **Conversão:** troca de uma unidade por outra da mesma medida, sem mudar a quantidade real.
- **Comprimento:** distância entre dois pontos. Unidades: quilômetro (km), metro (m), centímetro (cm), milha (mi), pé (ft) e polegada (in).
- **Massa:** quantidade de matéria de um corpo, popularmente chamada de peso. Unidades: tonelada (t), quilograma (kg), grama (g), miligrama (mg), libra (lb) e onça (oz).
- **Temperatura:** grau de calor ou frio de um corpo ou ambiente. Unidades: Celsius (°C), Fahrenheit (°F) e Kelvin (K).
- **Tempo:** duração entre dois momentos. Unidades: semana, dia (d), hora (h), minuto (min), segundo (s) e milissegundo (ms).
- **Velocidade:** distância percorrida em um intervalo de tempo. Unidades: quilômetro por hora (km/h), metro por segundo (m/s), milha por hora (mph), nó (kn) e pé por segundo (ft/s).
- **Milha:** unidade de comprimento usada nos Estados Unidos e no Reino Unido, equivalente a 1.609,344 metros.
- **Pé e polegada:** unidades de comprimento do sistema imperial. Um pé tem 30,48 cm e uma polegada tem 2,54 cm.
- **Libra e onça:** unidades de massa do sistema imperial. Uma libra equivale a cerca de 453,59 g e uma onça a cerca de 28,35 g.
- **Kelvin:** escala de temperatura usada na ciência, em que 0 K é o zero absoluto (cerca de −273,15 °C).
- **Nó:** unidade de velocidade usada na navegação e na aviação, equivalente a uma milha náutica por hora (1,852 km/h).

## Fórmulas de conversão de temperatura

Diferente das outras medidas, a temperatura não usa só multiplicação:

- **Celsius para Fahrenheit:** °F = °C × 9 ÷ 5 + 32
- **Fahrenheit para Celsius:** °C = (°F − 32) × 5 ÷ 9
- **Celsius para Kelvin:** K = °C + 273,15