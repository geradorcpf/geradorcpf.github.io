---
title: "Calendário 2026"
seoTitle: "Calendário 2026: online e grátis"
description: "Calendário 2026: calendário de 2026 com feriados e datas importantes. Grátis e online, sem cadastro."
summary: "Calendário de 2026 com feriados e datas importantes."
date: 2026-10-24
draft: false
category: "datas"
tags: ["calendário", "feriados", "datas"]
keywords: ["calendário 2026", "calendário 2026 online", "calendário", "feriados", "datas"]
---

<!--INI SUDAH DIKERJAKAN-->

Basta digitar o ano abaixo e depois clicar em **Mostrar Calendário**. A página abre sempre no ano atual e se atualiza sozinha todos os dias.

<div id="calc-calendario" style="max-width:960px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📅 Calendário<span id="cal-sufixo"></span></h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o ano e veja os 12 meses com feriados e datas importantes.</p>
<label for="cal-ano" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ano</label>
<input id="cal-ano" type="text" inputmode="numeric" maxlength="4" placeholder="Ex.: 2026" autocomplete="off" style="width:100%;max-width:240px;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cal-anterior" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">« Anterior</button>
<button type="button" id="cal-mostrar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Mostrar Calendário</button>
<button type="button" id="cal-proximo" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Próximo »</button>
<button type="button" id="cal-hoje" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Hoje</button>
<button type="button" id="cal-imprimir" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Imprimir</button>
</div>
<div id="cal-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cal-resultado">digite um ano e clique em "Mostrar Calendário".</span></div>
<div style="display:flex;gap:16px;flex-wrap:wrap;margin-top:16px;font-size:0.85rem;color:#475569;">
<span><span style="display:inline-block;width:12px;height:12px;border-radius:3px;background:#4f46e5;margin-right:6px;vertical-align:middle;"></span>Hoje</span>
<span><span style="display:inline-block;width:12px;height:12px;border-radius:3px;background:#fee2e2;border:1px solid #b91c1c;margin-right:6px;vertical-align:middle;"></span>Feriado nacional</span>
<span><span style="display:inline-block;width:12px;height:12px;border-radius:3px;background:#fef3c7;border:1px solid #92400e;margin-right:6px;vertical-align:middle;"></span>Ponto facultativo</span>
<span><span style="display:inline-block;width:12px;height:12px;border-radius:3px;background:#e0e7ff;border:1px solid #3730a3;margin-right:6px;vertical-align:middle;"></span>Data comemorativa</span>
</div>
<div id="cal-meses" style="margin-top:16px;display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;"></div>
<div id="cal-feriados" style="margin-top:20px;"></div>
</div>
<script>
(function () {
  var MESES = ['janeiro', 'fevereiro', 'março', 'abril', 'maio', 'junho', 'julho', 'agosto', 'setembro', 'outubro', 'novembro', 'dezembro'];
  var DIAS = ['domingo', 'segunda-feira', 'terça-feira', 'quarta-feira', 'quinta-feira', 'sexta-feira', 'sábado'];
  var CABECALHO = ['Do', 'Se', 'Te', 'Qu', 'Qu', 'Se', 'Sa'];
  var CORES = { n: { bg: '#fee2e2', cor: '#b91c1c' }, f: { bg: '#fef3c7', cor: '#92400e' }, c: { bg: '#e0e7ff', cor: '#3730a3' } };
  var PESO = { n: 3, f: 2, c: 1 };
  var TIPOS = { n: 'Feriado nacional', f: 'Ponto facultativo', c: 'Data comemorativa' };
  var ANO_MIN = 1583;
  var ANO_MAX = 9999;
  var campo = document.getElementById('cal-ano');
  var resultado = document.getElementById('cal-resultado');
  var caixa = document.getElementById('cal-resposta');
  var gradeMeses = document.getElementById('cal-meses');
  var listaFeriados = document.getElementById('cal-feriados');
  var sufixo = document.getElementById('cal-sufixo');
  var anoAtual = 0;
  var anoMostrado = 0;
  var ultimaChave = '';
  function cap(t) { return t.charAt(0).toUpperCase() + t.slice(1); }
  function pad(n) { return n > 9 ? String(n) : '0' + n; }
  function limparNo(no) { while (no.firstChild) { no.removeChild(no.firstChild); } }
  function el(tag, css, texto) {
    var e = document.createElement(tag);
    if (css) { e.style.cssText = css; }
    if (texto !== undefined) { e.textContent = texto; }
    return e;
  }
  function texto(t) { return document.createTextNode(t); }
  function plural(n, um, varios) { return n + ' ' + (n === 1 ? um : varios); }
  function bissexto(y) { return y % 4 === 0 ? (y % 100 !== 0 ? true : y % 400 === 0) : false; }
  function dataPorExtenso(d) {
    return cap(DIAS[d.getDay()]) + ', ' + d.getDate() + ' de ' + MESES[d.getMonth()] + ' de ' + d.getFullYear();
  }
  function pascoa(y) {
    var a = y % 19;
    var b = Math.floor(y / 100);
    var c = y % 100;
    var d = Math.floor(b / 4);
    var e = b % 4;
    var f = Math.floor((b + 8) / 25);
    var g = Math.floor((b - f + 1) / 3);
    var h = (19 * a + b - d - g + 15) % 30;
    var i = Math.floor(c / 4);
    var k = c % 4;
    var l = (32 + 2 * e + 2 * i - h - k) % 7;
    var m = Math.floor((a + 11 * h + 22 * l) / 451);
    var mes = Math.floor((h + l - 7 * m + 114) / 31);
    var dia = ((h + l - 7 * m + 114) % 31) + 1;
    return new Date(y, mes - 1, dia);
  }
  function segundoDomingo(y, mesIdx) {
    var primeiro = new Date(y, mesIdx, 1).getDay();
    var primeiroDomingo = 1 + (7 - primeiro) % 7;
    return new Date(y, mesIdx, primeiroDomingo + 7);
  }
  function feriadosDoAno(y) {
    var lista = [];
    function add(d, nome, tipo) { lista.push({ d: d, nome: nome, tipo: tipo }); }
    var p = pascoa(y);
    function rel(off) { return new Date(y, p.getMonth(), p.getDate() + off); }
    add(new Date(y, 0, 1), 'Confraternização Universal', 'n');
    add(new Date(y, 2, 8), 'Dia Internacional da Mulher', 'c');
    add(rel(-48), 'Carnaval', 'f');
    add(rel(-47), 'Carnaval', 'f');
    add(rel(-46), 'Quarta-feira de Cinzas', 'f');
    add(rel(-2), 'Sexta-feira Santa', 'n');
    add(p, 'Páscoa', 'c');
    add(new Date(y, 3, 21), 'Tiradentes', 'n');
    add(new Date(y, 4, 1), 'Dia do Trabalho', 'n');
    add(segundoDomingo(y, 4), 'Dia das Mães', 'c');
    add(rel(60), 'Corpus Christi', 'f');
    add(new Date(y, 5, 12), 'Dia dos Namorados', 'c');
    add(segundoDomingo(y, 7), 'Dia dos Pais', 'c');
    add(new Date(y, 8, 7), 'Independência do Brasil', 'n');
    add(new Date(y, 9, 12), 'Nossa Senhora Aparecida', 'n');
    add(new Date(y, 9, 12), 'Dia das Crianças', 'c');
    add(new Date(y, 10, 2), 'Finados', 'n');
    add(new Date(y, 10, 15), 'Proclamação da República', 'n');
    add(new Date(y, 10, 20), 'Dia da Consciência Negra', y >= 2024 ? 'n' : 'c');
    add(new Date(y, 11, 25), 'Natal', 'n');
    lista.sort(function (a, b) { return a.d - b.d; });
    return lista;
  }
  function criarDia(y, m, dia, inicio, mapa, hoje) {
    var itens = mapa[m + '-' + dia];
    var css = 'text-align:center;font-size:0.85rem;padding:6px 0;border-radius:6px;';
    var titulo = '';
    var ehHoje = false;
    if (y === hoje.getFullYear()) {
      if (m === hoje.getMonth()) { ehHoje = dia === hoje.getDate(); }
    }
    if ((inicio + dia - 1) % 7 === 0) { css += 'color:#b91c1c;'; }
    if (itens) {
      var topo = itens[0].tipo;
      var nomes = [];
      for (var j = 0; itens.length > j; j++) {
        if (PESO[itens[j].tipo] > PESO[topo]) { topo = itens[j].tipo; }
        nomes.push(itens[j].nome);
      }
      css += 'background:' + CORES[topo].bg + ';color:' + CORES[topo].cor + ';font-weight:700;';
      titulo = nomes.join(' / ');
    }
    if (ehHoje) {
      css += 'background:#4f46e5;color:#ffffff;font-weight:700;box-shadow:0 2px 8px rgba(79,70,229,0.35);';
      titulo = titulo ? 'Hoje - ' + titulo : 'Hoje';
    }
    var cel = el('div', css, String(dia));
    if (titulo) { cel.title = titulo; }
    return cel;
  }
  function criarMes(y, m, mapa, hoje) {
    var card = el('div', 'background:#ffffff;border:1px solid #c7d2fe;border-radius:12px;padding:12px;');
    card.appendChild(el('div', 'font-weight:700;color:#3730a3;margin-bottom:8px;text-align:center;', cap(MESES[m])));
    var grade = el('div', 'display:grid;grid-template-columns:repeat(7,1fr);gap:2px;');
    for (var i = 0; 7 > i; i++) {
      grade.appendChild(el('div', 'text-align:center;font-size:0.75rem;font-weight:700;color:#64748b;padding:4px 0;', CABECALHO[i]));
    }
    var inicio = new Date(y, m, 1).getDay();
    var total = new Date(y, m + 1, 0).getDate();
    for (var v = 0; inicio > v; v++) { grade.appendChild(el('div', 'padding:6px 0;', '')); }
    for (var dia = 1; total >= dia; dia++) { grade.appendChild(criarDia(y, m, dia, inicio, mapa, hoje)); }
    card.appendChild(grade);
    return card;
  }
  function criarLista(y, lista) {
    var caixaLista = el('div', 'padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;');
    caixaLista.appendChild(el('h3', 'margin:0 0 10px;font-size:1.05rem;color:#3730a3;', 'Feriados e datas importantes de ' + y));
    var ul = el('ul', 'margin:0;padding:0;list-style:none;');
    for (var i = 0; lista.length > i; i++) {
      var it = lista[i];
      var li = el('li', 'display:flex;gap:10px;align-items:center;flex-wrap:wrap;padding:7px 0;border-bottom:1px solid #eef2ff;font-size:0.95rem;');
      li.appendChild(el('span', 'min-width:56px;text-align:center;padding:3px 8px;border-radius:6px;font-weight:700;font-size:0.85rem;background:' + CORES[it.tipo].bg + ';color:' + CORES[it.tipo].cor + ';', pad(it.d.getDate()) + '/' + pad(it.d.getMonth() + 1)));
      li.appendChild(el('strong', 'color:#1e293b;', it.nome));
      li.appendChild(el('span', 'font-size:0.85rem;color:#64748b;', DIAS[it.d.getDay()] + ' · ' + TIPOS[it.tipo]));
      ul.appendChild(li);
    }
    caixaLista.appendChild(ul);
    return caixaLista;
  }
  function sucesso() {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    limparNo(resultado);
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    limparNo(resultado);
    resultado.textContent = msg;
  }
  function mostrar(y) {
    anoMostrado = y;
    campo.value = String(y);
    var hoje = new Date();
    var lista = feriadosDoAno(y);
    var mapa = {};
    var nacionais = 0;
    var facultativos = 0;
    for (var i = 0; lista.length > i; i++) {
      var k = lista[i].d.getMonth() + '-' + lista[i].d.getDate();
      if (!mapa[k]) { mapa[k] = []; }
      mapa[k].push(lista[i]);
      if (lista[i].tipo === 'n') { nacionais++; }
      if (lista[i].tipo === 'f') { facultativos++; }
    }
    limparNo(gradeMeses);
    for (var m = 0; 12 > m; m++) { gradeMeses.appendChild(criarMes(y, m, mapa, hoje)); }
    limparNo(listaFeriados);
    listaFeriados.appendChild(criarLista(y, lista));
    var p = pascoa(y);
    sucesso();
    resultado.appendChild(texto('O ano '));
    resultado.appendChild(el('strong', 'font-size:1.2rem;', String(y)));
    resultado.appendChild(texto(' tem '));
    resultado.appendChild(el('strong', 'font-size:1.2rem;', bissexto(y) ? '366' : '365'));
    resultado.appendChild(texto(' dias (' + (bissexto(y) ? 'ano bissexto' : 'não é bissexto') + '), com ' + plural(nacionais, 'feriado nacional', 'feriados nacionais') + ' e ' + plural(facultativos, 'ponto facultativo', 'pontos facultativos') + '.'));
    resultado.appendChild(el('br'));
    resultado.appendChild(el('small', 'color:#475569;', 'A Páscoa de ' + y + ' cai em ' + p.getDate() + ' de ' + MESES[p.getMonth()] + '.'));
  }
  function lerAno() {
    var t = String(campo.value).trim();
    if (/^[0-9]{4}$/.test(t)) {
      var n = Number(t);
      if (n >= ANO_MIN) { return n; }
    }
    return NaN;
  }
  function mostrarDigitado() {
    var y = lerAno();
    if (isNaN(y)) { erro('informe um ano válido com 4 dígitos, entre ' + ANO_MIN + ' e ' + ANO_MAX + '.'); return; }
    mostrar(y);
  }
  function mudar(delta) {
    var alvo = anoMostrado + delta;
    if (ANO_MIN > alvo || alvo > ANO_MAX) { erro('o calendário está disponível de ' + ANO_MIN + ' a ' + ANO_MAX + '.'); return; }
    mostrar(alvo);
  }
  function atualizarDia() {
    var agora = new Date();
    var chave = agora.getFullYear() + '-' + agora.getMonth() + '-' + agora.getDate();
    if (chave === ultimaChave) { return; }
    ultimaChave = chave;
    sufixo.textContent = ' | ' + dataPorExtenso(agora);
    var acompanha = anoMostrado === anoAtual;
    anoAtual = agora.getFullYear();
    mostrar(acompanha ? anoAtual : anoMostrado);
  }
  function agendar() {
    var agora = new Date();
    var proximo = new Date(agora.getFullYear(), agora.getMonth(), agora.getDate() + 1, 0, 0, 2);
    setTimeout(function () { atualizarDia(); agendar(); }, proximo - agora);
  }
  document.getElementById('cal-mostrar').addEventListener('click', mostrarDigitado);
  document.getElementById('cal-anterior').addEventListener('click', function () { mudar(-1); });
  document.getElementById('cal-proximo').addEventListener('click', function () { mudar(1); });
  document.getElementById('cal-hoje').addEventListener('click', function () { mostrar(new Date().getFullYear()); });
  document.getElementById('cal-imprimir').addEventListener('click', function () { window.print(); });
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { mostrarDigitado(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  document.addEventListener('visibilitychange', atualizarDia);
  atualizarDia();
  agendar();
})();
</script>

## Como usar o calendário

1. Digite o **Ano** com 4 dígitos no campo (por exemplo, `2026`). Ao abrir a página, o campo já vem preenchido com o ano atual.
2. Clique em **Mostrar Calendário** (ou pressione Enter) para ver os 12 meses do ano escolhido.
3. Use **« Anterior** e **Próximo »** para passar de um ano para outro sem digitar.
4. Clique em **Hoje** para voltar ao ano atual. O dia de hoje aparece destacado em azul-escuro.
5. Passe o mouse (ou toque) sobre um dia colorido para ver o nome do feriado ou da data comemorativa.
6. Clique em **Imprimir** para abrir a janela de impressão do navegador.

O calendário funciona de 1583 a 9999 e se atualiza sozinho: a data de hoje aparece ao lado do título e o destaque muda à meia-noite, sem precisar recarregar a página. Os feriados móveis (Carnaval, Sexta-feira Santa, Páscoa e Corpus Christi) são calculados para cada ano. Feriados estaduais e municipais não estão incluídos, pois variam conforme o local.

## Entendendo os termos

- **Calendário:** sistema que organiza o tempo em dias, semanas, meses e anos. Este usa o calendário gregoriano, adotado no Brasil.
- **Ano:** período de 12 meses, com 365 dias (ou 366 em ano bissexto).
- **Ano bissexto:** ano com 366 dias, em que fevereiro tem 29 dias. Ocorre a cada 4 anos, exceto nos anos divisíveis por 100 que não sejam divisíveis por 400.
- **Dia da semana:** posição do dia dentro da semana, de domingo (Do) a sábado (Sa).
- **Hoje:** dia atual, de acordo com a data do seu dispositivo, destacado no calendário.
- **Feriado nacional:** data prevista em lei federal que vale em todo o país, como o Natal e a Independência do Brasil.
- **Ponto facultativo:** dia em que o expediente das repartições públicas federais fica a critério do governo. Empresas privadas seguem suas próprias regras ou convenções coletivas. Exemplos: Carnaval e Corpus Christi.
- **Data comemorativa:** data lembrada pela sociedade que não é feriado, como o Dia das Mães e o Dia dos Namorados.
- **Feriado móvel:** feriado cuja data muda a cada ano porque depende da Páscoa, como o Carnaval e o Corpus Christi.
- **Páscoa:** festa cristã celebrada no primeiro domingo após a primeira lua cheia que ocorre depois do equinócio de março. É a base para calcular os feriados móveis.
- **Carnaval:** festa popular que cai na segunda e na terça-feira 47 e 48 dias antes da Páscoa; a Quarta-feira de Cinzas encerra a folia.
- **Corpus Christi:** celebração católica realizada 60 dias depois da Páscoa, sempre numa quinta-feira.