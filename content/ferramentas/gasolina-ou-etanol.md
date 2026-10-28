---
title: "Gasolina ou Etanol: qual compensa"
seoTitle: "Gasolina ou Etanol: qual compensa"
description: "Gasolina ou Etanol: qual compensa: descubra se compensa abastecer com gasolina ou etanol. Grátis e online, sem cadastro."
summary: "Descubra se compensa abastecer com gasolina ou etanol."
date: 2026-10-28
draft: false
category: "financas"
tags: ["combustível", "veículos", "economia", "calculadora"]
keywords: ["gasolina ou etanol: qual compensa", "gasolina ou etanol: qual compensa online", "combustível", "veículos", "economia"]
---

Basta digitar o preço da gasolina e o preço do etanol abaixo e depois clicar em **Calcular**.

<div id="calc-gasolina-etanol" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⛽ Gasolina ou Etanol: qual compensa</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dois preços por litro e veja qual combustível compensa mais.</p>
<label for="ge-gasolina" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Preço da gasolina (R$/litro)</label>
<input id="ge-gasolina" type="text" inputmode="decimal" placeholder="Ex.: 6,29" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ge-etanol" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Preço do etanol (R$/litro)</label>
<input id="ge-etanol" type="text" inputmode="decimal" placeholder="Ex.: 4,19" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ge-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular</button>
<button type="button" id="ge-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ge-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ge-resultado">preencha os campos e clique em "Calcular".</span></div>
</div>
<script>
(function () {
  var gasolina = document.getElementById('ge-gasolina');
  var etanol = document.getElementById('ge-etanol');
  var resultado = document.getElementById('ge-resultado');
  var caixa = document.getElementById('ge-resposta');
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n, casas) { return n.toLocaleString('pt-BR', { minimumFractionDigits: casas, maximumFractionDigits: casas }); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var g = numero(gasolina.value);
    var e = numero(etanol.value);
    if (isNaN(g) || isNaN(e)) { erro('informe números válidos nos dois preços.'); return; }
    if (g <= 0 || e <= 0) { erro('os preços devem ser maiores que zero.'); return; }
    var relacao = (e / g) * 100;
    var esq = Math.round(e * 100 * 1000000) / 1000000;
    var dir = Math.round(g * 70 * 1000000) / 1000000;
    var texto;
    if (esq === dir) {
      texto = 'tanto faz: o etanol custa exatamente <strong style="font-size:1.2rem;">70%</strong> do preço da gasolina.';
    } else if (esq > dir) {
      texto = 'compensa abastecer com <strong style="font-size:1.2rem;">gasolina</strong>.';
    } else {
      texto = 'compensa abastecer com <strong style="font-size:1.2rem;">etanol</strong>.';
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = texto + '<br><small style="color:#475569;">Relação etanol/gasolina = ' + fmt(e, 2) + ' ÷ ' + fmt(g, 2) + ' = ' + fmt(relacao, 2) + '% (limite de referência: 70%)</small>';
  }
  function limpar() {
    gasolina.value = '';
    etanol.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular".';
    gasolina.focus();
  }
  document.getElementById('ge-calcular').addEventListener('click', calcular);
  document.getElementById('ge-limpar').addEventListener('click', limpar);
  [gasolina, etanol].forEach(function (el) {
    el.addEventListener('keydown', function (ev) { if (ev.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o **Preço da gasolina** por litro no primeiro campo.
2. Digite o **Preço do etanol** por litro no segundo campo.
3. Clique em **Calcular** (ou pressione Enter) para ver qual combustível compensa mais.
4. Use o botão **Limpar** para apagar os valores e fazer uma nova comparação.

Você pode usar números decimais, com vírgula ou ponto (por exemplo, `6,29` ou `6.29`). Os dois preços devem ser do mesmo posto ou da mesma região e estar na mesma unidade (reais por litro) para que a comparação seja justa.

## Entendendo os termos

- **Veículo flex:** carro ou moto que funciona tanto com gasolina quanto com etanol, em qualquer proporção.
- **Gasolina:** combustível derivado do petróleo, com maior poder energético por litro.
- **Etanol (álcool):** combustível de origem renovável, geralmente feito de cana-de-açúcar, que rende menos quilômetros por litro que a gasolina.
- **Preço por litro:** valor cobrado por cada litro de combustível na bomba, em reais (R$/litro).
- **Relação etanol/gasolina:** percentual obtido dividindo o preço do etanol pelo preço da gasolina e multiplicando por 100.
- **Regra dos 70%:** referência prática segundo a qual o etanol compensa quando custa até 70% do preço da gasolina.
- **Consumo médio:** quantidade de quilômetros que o veículo percorre com um litro de combustível.

## Como funciona o cálculo

O etanol rende, em média, cerca de 70% da distância que a gasolina rende com o mesmo volume. Por isso, a comparação usa a relação entre os dois preços:

**Relação = preço do etanol ÷ preço da gasolina × 100**

- Se a relação for **menor que 70%**, compensa abastecer com **etanol**.
- Se a relação for **maior que 70%**, compensa abastecer com **gasolina**.
- Se for exatamente **70%**, tanto faz.

Essa relação é uma referência e pode variar conforme a eficiência do veículo com cada combustível, o consumo médio e a qualidade do combustível disponível.

## Exemplo resolvido

Em um posto, a gasolina custa R$ 6,29 por litro e o etanol custa R$ 4,19 por litro. Qual compensa?

1. Identifique os preços: gasolina = 6,29 e etanol = 4,19.
2. Calcule a relação: 4,19 ÷ 6,29 × 100 ≈ 66,61%.
3. Compare com o limite: 66,61% é menor que 70%.

**Resposta:** compensa abastecer com **etanol**.