---
title: "Contador de Dias entre Datas"
seoTitle: "Contador de Dias entre Datas"
description: "Contador de Dias entre Datas: conte quantos dias existem entre duas datas. Grátis e online, sem cadastro."
summary: "Conte quantos dias existem entre duas datas."
date: 2026-10-27
draft: false
category: "datas"
tags: ["datas", "calendário", "calculadora", "contagem de dias"]
keywords: ["contador de dias entre datas", "contador de dias entre datas online", "datas", "calendário", "calculadora"]
---

<!--sudah dikerjakan-->

Basta escolher a data de início e a data de fim abaixo e depois clicar em **Calcular Dias**.

<div id="calc-dias" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📅 Contador de Dias entre Datas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as duas datas e veja o resultado na hora.</p>
<label for="dias-inicio" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data de início</label>
<input id="dias-inicio" type="date" min="0001-01-01" max="9999-12-31" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="dias-fim" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data de fim</label>
<input id="dias-fim" type="date" min="0001-01-01" max="9999-12-31" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="dias-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Dias</button>
<button type="button" id="dias-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="dias-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="dias-resultado">selecione as duas datas e clique em "Calcular Dias".</span></div>
</div>
<script>
(function () {
  var inicio = document.getElementById('dias-inicio');
  var fim = document.getElementById('dias-fim');
  var resultado = document.getElementById('dias-resultado');
  var caixa = document.getElementById('dias-resposta');
  var MSG_PADRAO = 'selecione as duas datas e clique em "Calcular Dias".';
  var MS_DIA = 86400000;
  function lerData(v) {
    var p = String(v).split('-');
    if (p.length !== 3) { return NaN; }
    var y = Number(p[0]);
    var m = Number(p[1]);
    var d = Number(p[2]);
    var t = Date.UTC(y, m - 1, d);
    if (isNaN(t)) { return NaN; }
    var c = new Date(t);
    if (c.getUTCFullYear() !== y || c.getUTCMonth() !== m - 1 || c.getUTCDate() !== d) { return NaN; }
    return t;
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function plural(n, singular, pluralTxt) { return n === 1 ? singular : pluralTxt; }
  function limparResultado() {
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    limparResultado();
    resultado.appendChild(document.createTextNode(msg));
  }
  function sucesso(diff, iniTxt, fimTxt) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    limparResultado();
    var semanas = Math.floor(diff / 7);
    var resto = diff % 7;
    resultado.appendChild(document.createTextNode('Existem '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.appendChild(document.createTextNode(fmt(diff) + ' ' + plural(diff, 'dia', 'dias')));
    resultado.appendChild(forte);
    resultado.appendChild(document.createTextNode(' entre as duas datas.'));
    resultado.appendChild(document.createElement('br'));
    var pequeno = document.createElement('small');
    pequeno.style.color = '#475569';
    pequeno.appendChild(document.createTextNode('De ' + iniTxt + ' até ' + fimTxt + ' (equivale a ' + fmt(semanas) + ' ' + plural(semanas, 'semana', 'semanas') + ' e ' + resto + ' ' + plural(resto, 'dia', 'dias') + ').'));
    resultado.appendChild(pequeno);
  }
  function dataBR(v) {
    var p = v.split('-');
    return p[2] + '/' + p[1] + '/' + p[0];
  }
  function calcular() {
    var a = lerData(inicio.value);
    var b = lerData(fim.value);
    if (isNaN(a) || isNaN(b)) { erro('data inválida. Informe as duas datas.'); return; }
    var diff = Math.round((b - a) / MS_DIA);
    if (diff === 0) { erro('a data de início não pode ser igual à data de fim.'); return; }
    if (Math.sign(diff) === -1) { erro('a data de início não pode ser posterior à data de fim.'); return; }
    sucesso(diff, dataBR(inicio.value), dataBR(fim.value));
  }
  function limpar() {
    inicio.value = '';
    fim.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    limparResultado();
    resultado.appendChild(document.createTextNode(MSG_PADRAO));
    inicio.focus();
  }
  document.getElementById('dias-calcular').addEventListener('click', calcular);
  document.getElementById('dias-limpar').addEventListener('click', limpar);
  [inicio, fim].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Escolha a **Data de início** no primeiro campo. Você pode digitar a data ou selecioná-la clicando no calendário.
2. Escolha a **Data de fim** no segundo campo, da mesma forma.
3. Clique em **Calcular Dias** (ou pressione Enter) para ver quantos dias existem entre as duas datas.
4. Use o botão **Limpar** para apagar as datas e fazer uma nova contagem.

A data de início deve ser anterior à data de fim. Se as datas forem iguais, se a data de início for posterior à data de fim ou se alguma data estiver vazia ou inválida, a calculadora mostra uma mensagem de erro.

## Entendendo os termos

- **Data de início:** primeiro dia do período que você quer contar.
- **Data de fim:** último dia do período, ou seja, a data até a qual a contagem é feita.
- **Dias entre datas:** quantidade de dias que separa a data de início da data de fim. O dia de início não entra na contagem, mas o dia de fim entra.
- **Semana:** período de 7 dias seguidos. O resultado também mostra a diferença em semanas e dias restantes.
- **Calendário:** seletor visual que permite escolher o dia, o mês e o ano com um clique, sem precisar digitar.
- **Data inválida:** data que não existe no calendário (como 31/02) ou campo deixado em branco.