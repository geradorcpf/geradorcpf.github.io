---
title: "Simulador de Financiamento"
seoTitle: "Simulador de Financiamento"
description: "Simulador de Financiamento: simule parcelas e juros de um financiamento. Grátis e online, sem cadastro."
summary: "Simule parcelas e juros de um financiamento."
date: 2026-11-09
draft: false
category: "financas"
tags: ["financiamento", "juros", "finanças", "simulador"]
keywords: ["simulador de financiamento", "simulador de financiamento online", "financiamento", "juros", "finanças"]
---

Basta preencher os campos abaixo e clicar em **Calcular PRICE** ou **Calcular SAC** para simular o seu financiamento.

<div id="calc-financiamento" style="max-width:720px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💰 Simulador de Financiamento</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dados e escolha a tabela PRICE ou SAC.</p>
<label for="fin-valor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Valor (R$)</label>
<input id="fin-valor" type="text" inputmode="decimal" placeholder="Ex.: 50000" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="fin-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Entrada (R$)</label>
<input id="fin-entrada" type="text" inputmode="decimal" placeholder="Ex.: 10000 (deixe vazio se não houver)" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="fin-prestacoes" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número de Prestações</label>
<input id="fin-prestacoes" type="text" inputmode="numeric" placeholder="Ex.: 48" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="fin-juros" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Taxa de juros (% ao mês)</label>
<input id="fin-juros" type="text" inputmode="decimal" placeholder="Ex.: 1,5" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="fin-price" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular PRICE</button>
<button type="button" id="fin-sac" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular SAC</button>
<button type="button" id="fin-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="fin-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="fin-resultado">preencha os campos e clique em "Calcular PRICE" ou "Calcular SAC".</span></div>
<div id="fin-tabela" style="display:none;margin-top:16px;max-height:420px;overflow:auto;background:#ffffff;border:1px solid #c7d2fe;border-radius:12px;"></div>
</div>
<script>
(function () {
  var elValor = document.getElementById('fin-valor');
  var elEntrada = document.getElementById('fin-entrada');
  var elPrestacoes = document.getElementById('fin-prestacoes');
  var elJuros = document.getElementById('fin-juros');
  var resultado = document.getElementById('fin-resultado');
  var caixa = document.getElementById('fin-resposta');
  var tabelaBox = document.getElementById('fin-tabela');
  var textoInicial = 'preencha os campos e clique em "Calcular PRICE" ou "Calcular SAC".';
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function moeda(n) { return n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }); }
  function esvaziar(el) { while (el.firstChild) { el.removeChild(el.firstChild); } }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
    esvaziar(tabelaBox);
    tabelaBox.style.display = 'none';
  }
  function linha(rotulo, valor) {
    var d = document.createElement('div');
    var s = document.createElement('strong');
    s.textContent = rotulo + ' ';
    d.appendChild(s);
    d.appendChild(document.createTextNode(valor));
    resultado.appendChild(d);
  }
  function celula(tr, tag, texto, alinhar) {
    var c = document.createElement(tag);
    c.textContent = texto;
    c.style.cssText = 'padding:8px 10px;font-size:0.85rem;text-align:' + alinhar + ';border-bottom:1px solid #e2e8f0;white-space:nowrap;' + (tag === 'th' ? 'background:#eef2ff;color:#3730a3;position:sticky;top:0;' : 'color:#1e293b;');
    tr.appendChild(c);
  }
  function calcular(sistema) {
    var valor = numero(elValor.value);
    var entrada = String(elEntrada.value).trim() === '' ? 0 : numero(elEntrada.value);
    var n = numero(elPrestacoes.value);
    var taxa = numero(elJuros.value);
    if (isNaN(valor) || isNaN(entrada) || isNaN(n) || isNaN(taxa)) { erro('informe números válidos em todos os campos.'); return; }
    if (!(valor > 0)) { erro('o valor deve ser maior que zero.'); return; }
    if (!(entrada >= 0)) { erro('a entrada não pode ser negativa.'); return; }
    if (entrada >= valor) { erro('a entrada deve ser menor que o valor.'); return; }
    if (!(n >= 1) || n !== Math.floor(n) || n > 480) { erro('o número de prestações deve ser um inteiro entre 1 e 480.'); return; }
    if (!(taxa >= 0)) { erro('a taxa de juros não pode ser negativa.'); return; }
    var pv = valor - entrada;
    var i = taxa / 100;
    var pmt = i === 0 ? pv / n : (pv * i) / (1 - Math.pow(1 + i, -n));
    var saldo = pv;
    var totalJuros = 0;
    var totalPago = 0;
    var primeira = 0;
    var ultima = 0;
    var tabela = document.createElement('table');
    tabela.style.cssText = 'width:100%;border-collapse:collapse;';
    var cab = document.createElement('tr');
    celula(cab, 'th', 'Nº', 'center');
    celula(cab, 'th', 'Prestação', 'right');
    celula(cab, 'th', 'Juros', 'right');
    celula(cab, 'th', 'Amortização', 'right');
    celula(cab, 'th', 'Saldo Devedor', 'right');
    tabela.appendChild(cab);
    for (var k = 1; n >= k; k++) {
      var juros = saldo * i;
      var amort = sistema === 'PRICE' ? pmt - juros : pv / n;
      var parcela = juros + amort;
      saldo = k === n ? 0 : Math.max(0, saldo - amort);
      totalJuros += juros;
      totalPago += parcela;
      if (k === 1) { primeira = parcela; }
      ultima = parcela;
      var tr = document.createElement('tr');
      celula(tr, 'td', String(k), 'center');
      celula(tr, 'td', moeda(parcela), 'right');
      celula(tr, 'td', moeda(juros), 'right');
      celula(tr, 'td', moeda(amort), 'right');
      celula(tr, 'td', moeda(saldo), 'right');
      tabela.appendChild(tr);
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    esvaziar(resultado);
    linha('Sistema:', sistema === 'PRICE' ? 'Tabela PRICE (parcelas fixas)' : 'Tabela SAC (amortização constante)');
    linha('Valor financiado:', moeda(pv));
    linha('Valor da prestação:', sistema === 'PRICE' ? moeda(pmt) : moeda(primeira) + ' (1ª) até ' + moeda(ultima) + ' (última)');
    linha('Total de juros:', moeda(totalJuros));
    linha('Total devido:', moeda(totalPago));
    esvaziar(tabelaBox);
    tabelaBox.appendChild(tabela);
    tabelaBox.style.display = 'block';
  }
  function limpar() {
    elValor.value = '';
    elEntrada.value = '';
    elPrestacoes.value = '';
    elJuros.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
    esvaziar(tabelaBox);
    tabelaBox.style.display = 'none';
    elValor.focus();
  }
  document.getElementById('fin-price').addEventListener('click', function () { calcular('PRICE'); });
  document.getElementById('fin-sac').addEventListener('click', function () { calcular('SAC'); });
  document.getElementById('fin-limpar').addEventListener('click', limpar);
  [elValor, elEntrada, elPrestacoes, elJuros].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular('PRICE'); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o simulador

1. Digite o **Valor** do bem que você quer financiar (veículo, imóvel ou outro).
2. Informe a **Entrada**, se houver. Se não houver entrada, deixe o campo vazio.
3. Digite o **Número de Prestações** (de 1 a 480 meses).
4. Informe a **Taxa de juros** em % ao mês (por exemplo, `1,5`).
5. Clique em **Calcular PRICE** ou **Calcular SAC** para ver a prestação, o total de juros, o total devido e a tabela mês a mês. Pressionar Enter calcula pela tabela PRICE.
6. Use o botão **Limpar** para apagar os valores e fazer uma nova simulação.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `1,5` ou `1.5`). A taxa deve ser mensal; se você só tem a taxa anual, converta-a antes de simular.

## Entendendo os termos

- **Financiamento:** compra de um bem pagando o valor aos poucos, em prestações, com a cobrança de juros.
- **Valor:** preço total do bem que será financiado.
- **Entrada:** parte do valor paga à vista no início. Ela reduz o valor financiado.
- **Valor financiado:** valor do bem menos a entrada, ou seja, o que realmente será parcelado.
- **Número de Prestações:** quantidade de parcelas mensais em que o financiamento será pago.
- **Taxa de juros:** percentual cobrado por mês sobre o saldo devedor.
- **Prestação (parcela):** valor pago a cada mês, formado por juros e amortização.
- **Juros:** custo do dinheiro emprestado, calculado sobre o saldo devedor de cada mês.
- **Amortização:** parte da prestação que realmente reduz a dívida.
- **Saldo Devedor:** quanto ainda falta pagar do valor financiado, sem contar os juros futuros.
- **Total de juros:** soma de todos os juros pagos ao longo do financiamento.
- **Total devido:** soma de todas as prestações, ou seja, o valor financiado mais o total de juros.
- **Tabela PRICE:** também chamada de Sistema Francês de Amortização, é muito usada em veículos e bens de menor valor. As prestações são fixas e a amortização cresce ao longo do tempo.
- **Tabela SAC:** Sistema de Amortização Constante, muito usado em financiamento de imóveis. A amortização é constante e as prestações diminuem ao longo do tempo.