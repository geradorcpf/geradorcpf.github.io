---
title: "Semana do Ano"
seoTitle: "Semana do Ano"
description: "Semana do Ano: descubra em que semana do ano estamos. Grátis e online, sem cadastro."
summary: "Descubra em que semana do ano estamos."
date: 2026-11-09
draft: false
category: "datas"
tags: ["calendário", "semana", "datas"]
keywords: ["semana do ano", "semana do ano online", "calendário", "semana", "datas"]
---

Ao abrir a página, a ferramenta já mostra a semana de hoje. Para consultar outro dia, escolha a data abaixo e clique em **Calcular Semana**.

<div id="calc-semana" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📅 Semana do Ano</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha uma data e veja em que semana do ano ela está.</p>
<label for="sem-data" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data</label>
<input id="sem-data" type="date" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sem-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Semana</button>
<button type="button" id="sem-hoje" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Hoje</button>
</div>
<div id="sem-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sem-resultado">escolha uma data e clique em "Calcular Semana".</span>
<div id="sem-trilha" style="display:none;margin-top:12px;height:10px;background:#e0e7ff;border-radius:999px;overflow:hidden;"><div id="sem-barra" style="height:100%;width:0;background:linear-gradient(135deg,#4f46e5,#6366f1);border-radius:999px;"></div></div>
</div>
</div>
<script>
(function () {
  var campo = document.getElementById('sem-data');
  var resultado = document.getElementById('sem-resultado');
  var caixa = document.getElementById('sem-resposta');
  var trilha = document.getElementById('sem-trilha');
  var barra = document.getElementById('sem-barra');
  var DIA = 86400000;
  function dois(n) { return String(n).padStart(2, '0'); }
  function hoje() {
    var h = new Date();
    return h.getFullYear() + '-' + dois(h.getMonth() + 1) + '-' + dois(h.getDate());
  }
  function montar(a, m, d) {
    a = Number(a); m = Number(m); d = Number(d);
    if (isNaN(a) || isNaN(m) || isNaN(d)) { return null; }
    var dt = new Date(Date.UTC(a, m - 1, d));
    if (dt.getUTCFullYear() !== a || dt.getUTCMonth() !== m - 1 || dt.getUTCDate() !== d) { return null; }
    return dt;
  }
  function lerData(v) {
    var t = String(v).trim();
    var p;
    if (t.indexOf('/') !== -1) { p = t.split('/'); return montar(p[2], p[1], p[0]); }
    p = t.split('-');
    return montar(p[0], p[1], p[2]);
  }
  function semanaIso(dt) {
    var dn = (dt.getUTCDay() + 6) % 7;
    var quinta = new Date(dt.getTime() + (3 - dn) * DIA);
    var ano = quinta.getUTCFullYear();
    var n = Math.floor((quinta.getTime() - Date.UTC(ano, 0, 1)) / DIA / 7) + 1;
    return { ano: ano, semana: n, inicio: new Date(dt.getTime() - dn * DIA) };
  }
  function totalSemanas(ano) { return semanaIso(new Date(Date.UTC(ano, 11, 28))).semana; }
  function texto(dt) {
    return dt.toLocaleDateString('pt-BR', { weekday: 'long', day: '2-digit', month: 'long', year: 'numeric', timeZone: 'UTC' });
  }
  function plural(n) { return n + (n === 1 ? ' semana' : ' semanas'); }
  function esvaziar() {
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
  }
  function add(tag, txt, estilo) {
    var el = document.createElement(tag);
    if (txt) { el.textContent = txt; }
    if (estilo) { el.style.cssText = estilo; }
    resultado.appendChild(el);
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    trilha.style.display = 'none';
    esvaziar();
    resultado.textContent = msg;
  }
  function calcular() {
    var dt = lerData(campo.value);
    if (!dt) { erro('informe uma data válida.'); return; }
    var s = semanaIso(dt);
    var total = totalSemanas(s.ano);
    var fim = new Date(s.inicio.getTime() + 6 * DIA);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    esvaziar();
    add('span', 'Semana ');
    add('strong', String(s.semana), 'font-size:1.2rem;');
    add('span', ' de ' + s.ano + ' (o ano tem ' + total + ' semanas)');
    add('br');
    add('small', 'De ' + texto(s.inicio) + ' a ' + texto(fim), 'color:#475569;');
    add('br');
    add('small', 'Já passaram: ' + plural(s.semana - 1) + ' · Esta semana: ' + s.semana + ' · Faltam: ' + plural(total - s.semana), 'color:#475569;');
    barra.style.width = Math.round(s.semana / total * 100) + '%';
    trilha.style.display = 'block';
  }
  function irParaHoje() {
    campo.value = hoje();
    calcular();
  }
  document.getElementById('sem-calcular').addEventListener('click', calcular);
  document.getElementById('sem-hoje').addEventListener('click', irParaHoje);
  campo.addEventListener('change', calcular);
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  irParaHoje();
})();
</script>

## Como usar a ferramenta

1. Ao abrir a página, a ferramenta já mostra a **semana de hoje**, com as datas de início e fim.
2. Para consultar outro dia, escolha a data no campo **Data** (ou digite no formato `dd/mm/aaaa`).
3. Clique em **Calcular Semana** (ou pressione Enter) para ver o resultado.
4. Veja o número da semana, o período (de segunda a domingo), quantas semanas já passaram e quantas faltam.
5. Use o botão **Hoje** para voltar rapidamente à data atual.

## Entendendo os termos

- **Semana do ano:** número que indica a posição de uma semana dentro do ano, contando a partir da semana 1.
- **Semana ISO 8601:** padrão internacional usado nesta ferramenta. A semana começa na segunda-feira e termina no domingo, e a semana 1 é a que contém a primeira quinta-feira do ano.
- **Período da semana:** intervalo de sete dias, da segunda-feira ao domingo, em que a data escolhida está.
- **Já passaram:** quantidade de semanas completas que ficaram para trás desde o início do ano.
- **Esta semana:** número da semana em que a data consultada está.
- **Faltam:** quantidade de semanas restantes até o fim do ano, sem contar a semana atual.
- **Total de semanas:** um ano pode ter 52 ou 53 semanas, conforme o dia da semana em que ele começa.

## Como a semana do ano é calculada

Pelo padrão ISO 8601, a semana pertence ao ano em que cai a sua **quinta-feira**. Por isso, os primeiros dias de janeiro podem fazer parte da última semana do ano anterior, e os últimos dias de dezembro podem pertencer à semana 1 do ano seguinte.

## Exemplo resolvido

Em qual semana do ano está o dia 9 de novembro de 2026?

1. Identifique o dia da semana: 9 de novembro de 2026 é uma segunda-feira, o primeiro dia da semana.
2. Encontre a quinta-feira dessa semana: 12 de novembro de 2026.
3. Conte quantas semanas completas se passaram desde 1º de janeiro até essa quinta-feira e some 1.

**Resposta:** é a **semana 46**, que vai de segunda-feira, 9 de novembro de 2026, a domingo, 15 de novembro de 2026. Como 2026 tem 53 semanas, já passaram 45 e faltam 7.