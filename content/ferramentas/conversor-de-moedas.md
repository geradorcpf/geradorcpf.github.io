---
title: "Conversor de Moedas"
seoTitle: "Conversor de Moedas: online e grátis"
description: "Conversor de Moedas: converta valores entre moedas com a cotação do dia. Grátis e online, sem cadastro."
summary: "Converta valores entre moedas com a cotação do dia."
date: 2026-10-25
draft: false
category: "financas"
tags: ["moedas", "câmbio", "finanças", "conversão"]
keywords: ["conversor de moedas", "conversor de moedas online", "moedas", "câmbio", "finanças"]
---
<!--sudah dikerjakan-->

Basta digitar o valor, escolher a moeda de origem e a moeda de destino abaixo. O resultado aparece na hora, com a cotação do dia.

<div id="calc-moedas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💱 Conversor de Moedas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o valor, escolha as moedas e veja o resultado na hora.</p>
<label for="mo-valor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Valor</label>
<input id="mo-valor" type="text" inputmode="decimal" placeholder="Ex.: 100" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="mo-de" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">De (moeda de origem)</label>
<select id="mo-de" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;"></select>
<label for="mo-para" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Para (moeda de destino)</label>
<select id="mo-para" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;"></select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="mo-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter</button>
<button type="button" id="mo-inverter" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">⇅ Inverter</button>
<button type="button" id="mo-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="mo-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="mo-resultado">preencha o valor e escolha as moedas.</span></div>
<p id="mo-status" style="margin:10px 0 0;font-size:0.8rem;color:#64748b;line-height:1.4;"></p>
</div>
<script>
(function () {
  var moedas = [
    ['ZAR', 'África do Sul (Rande)'], ['ARS', 'Argentina (Peso)'], ['AUD', 'Austrália (Dólar)'],
    ['BOB', 'Bolívia (Boliviano)'], ['BRL', 'Brasil (Real)'], ['BTN', 'Butão (Rúpia)'],
    ['CAD', 'Canadá (Dólar)'], ['CLP', 'Chile (Peso)'], ['CNY', 'China (Iuan)'],
    ['SGD', 'Cingapura (Dólar)'], ['COP', 'Colômbia (Peso)'], ['KRW', 'Coréia do Sul (Won)'],
    ['DKK', 'Dinamarca (Coroa)'], ['USD', 'Estados Unidos (Dólar)'], ['EUR', 'Europa (Euro)'],
    ['IDR', 'Indonésia (Rúpia)'], ['ILS', 'Israel (Shekel)'], ['JPY', 'Japão (Iene)'],
    ['MYR', 'Malásia (Ringgit)'], ['MXN', 'México (Peso)'], ['NGN', 'Nigéria (Naira)'],
    ['NOK', 'Noruega (Coroa)'], ['NZD', 'Nova Zelândia (Dólar)'], ['GBP', 'Reino Unido (Libra)'],
    ['RUB', 'Rússia (Rublo)'], ['SEK', 'Suécia (Coroa)'], ['CHF', 'Suíça (Franco)'],
    ['TWD', 'Taiwan (Dólar)']
  ];
  var aproximadas = {
    ZAR: 18, ARS: 1450, AUD: 1.53, BOB: 6.91, BRL: 5.4, BTN: 88, CAD: 1.4, CLP: 950,
    CNY: 7.1, SGD: 1.3, COP: 3900, KRW: 1400, DKK: 6.45, USD: 1, EUR: 0.86, IDR: 16600,
    ILS: 3.3, JPY: 150, MYR: 4.2, MXN: 18.4, NGN: 1450, NOK: 10, NZD: 1.75, GBP: 0.75,
    RUB: 82, SEK: 9.4, CHF: 0.8, TWD: 30.5
  };
  var taxas = aproximadas;
  var usandoAproximadas = true;
  var atualizadoEm = '';
  var valor = document.getElementById('mo-valor');
  var de = document.getElementById('mo-de');
  var para = document.getElementById('mo-para');
  var resultado = document.getElementById('mo-resultado');
  var caixa = document.getElementById('mo-resposta');
  var status = document.getElementById('mo-status');
  var textoInicial = 'preencha o valor e escolha as moedas.';
  function preencher(sel, padrao) {
    moedas.forEach(function (m) {
      var o = document.createElement('option');
      o.value = m[0];
      o.textContent = m[1];
      sel.appendChild(o);
    });
    sel.value = padrao;
  }
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n, max) {
    return n.toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: max });
  }
  function esvaziar(no) {
    while (no.firstChild) { no.removeChild(no.firstChild); }
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function atualizarStatus() {
    if (usandoAproximadas) {
      status.textContent = 'Não foi possível obter a cotação atual. Os valores exibidos usam taxas aproximadas.';
    } else {
      status.textContent = 'Cotação atualizada em ' + atualizadoEm + '. Valores de referência, podem diferir das taxas praticadas por bancos e casas de câmbio.';
    }
  }
  function converter() {
    var v = numero(valor.value);
    if (isNaN(v)) { erro('informe um valor numérico válido.'); return; }
    if (!(v >= 0)) { erro('o valor não pode ser negativo.'); return; }
    var fator = taxas[para.value] / taxas[de.value];
    var total = v * fator;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    esvaziar(resultado);
    resultado.appendChild(document.createTextNode(fmt(v, 2) + ' ' + de.value + ' = '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = fmt(total, 4) + ' ' + para.value;
    resultado.appendChild(forte);
    resultado.appendChild(document.createElement('br'));
    var pequeno = document.createElement('small');
    pequeno.style.color = '#475569';
    pequeno.textContent = '1 ' + de.value + ' = ' + fmt(fator, 6) + ' ' + para.value;
    resultado.appendChild(pequeno);
  }
  function reiniciar() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
  }
  function automatico() {
    if (valor.value.trim() === '') { reiniciar(); } else { converter(); }
  }
  function inverter() {
    var tmp = de.value;
    de.value = para.value;
    para.value = tmp;
    automatico();
  }
  function limpar() {
    valor.value = '';
    de.value = 'USD';
    para.value = 'BRL';
    reiniciar();
    valor.focus();
  }
  preencher(de, 'USD');
  preencher(para, 'BRL');
  atualizarStatus();
  document.getElementById('mo-converter').addEventListener('click', converter);
  document.getElementById('mo-inverter').addEventListener('click', inverter);
  document.getElementById('mo-limpar').addEventListener('click', limpar);
  valor.addEventListener('input', automatico);
  de.addEventListener('change', automatico);
  para.addEventListener('change', automatico);
  valor.addEventListener('keydown', function (e) { if (e.key === 'Enter') { converter(); } });
  [valor, de, para].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  fetch('https://open.er-api.com/v6/latest/USD')
    .then(function (r) {
      if (!r.ok) { throw new Error('http'); }
      return r.json();
    })
    .then(function (d) {
      if (!d || d.result !== 'success' || !d.rates) { throw new Error('dados'); }
      var novas = {};
      Object.keys(aproximadas).forEach(function (cod) {
        novas[cod] = d.rates[cod] ? d.rates[cod] : aproximadas[cod];
      });
      taxas = novas;
      usandoAproximadas = false;
      atualizadoEm = new Date(d.time_last_update_unix * 1000).toLocaleString('pt-BR');
    })
    .catch(function () {
      usandoAproximadas = true;
    })
    .then(function () {
      atualizarStatus();
      if (valor.value.trim() !== '') { converter(); }
    });
})();
</script>

## Como usar o conversor

1. Digite o **Valor** que você quer converter no primeiro campo.
2. Escolha a moeda de origem em **De (moeda de origem)**, ou seja, a moeda em que o valor está.
3. Escolha a moeda de destino em **Para (moeda de destino)**, ou seja, a moeda para a qual você quer converter.
4. O resultado aparece automaticamente. Se preferir, clique em **Converter** (ou pressione Enter).
5. Use o botão **Inverter** para trocar a moeda de origem com a de destino e fazer a conversão contrária.
6. Use o botão **Limpar** para apagar o valor, voltar às moedas padrão (Dólar e Real) e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `100,50` ou `100.50`). A cotação é carregada quando a página abre. Se não for possível obter a cotação do dia, o conversor avisa e usa taxas aproximadas.

## Entendendo os termos

- **Moeda:** unidade monetária usada por um país ou região para pagamentos e preços, como o Real (Brasil), o Dólar (Estados Unidos) e o Euro (Europa).
- **Valor:** quantia que você deseja converter, expressa na moeda de origem.
- **Moeda de origem:** moeda em que o valor informado está. É a moeda que você "tem".
- **Moeda de destino:** moeda para a qual o valor será convertido. É a moeda que você "quer".
- **Cotação (taxa de câmbio):** preço de uma moeda em relação a outra. Por exemplo, se 1 USD = 5,40 BRL, a cotação do dólar é de 5,40 reais.
- **Câmbio:** troca de uma moeda por outra, feita de acordo com a cotação do momento.
- **Código da moeda (ISO 4217):** sigla de três letras que identifica cada moeda, como BRL (Real), USD (Dólar americano), EUR (Euro) e GBP (Libra esterlina).
- **Conversão:** cálculo que transforma um valor de uma moeda em outro, multiplicando o valor pela cotação entre as duas moedas.
- **Inverter:** troca de lugar a moeda de origem e a de destino, mostrando quanto vale o caminho contrário.
- **Cotação do dia:** taxa de câmbio de referência atualizada recentemente. Ela varia ao longo do tempo e pode diferir da taxa cobrada por bancos, corretoras e casas de câmbio, que costumam incluir tarifas e margens.