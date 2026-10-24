---
title: "Calendário Lunar 2026"
seoTitle: "Calendário Lunar 2026"
description: "Calendário Lunar 2026: veja as fases da lua mês a mês em 2026. Grátis e online, sem cadastro."
summary: "Veja as fases da lua mês a mês em 2026."
date: 2026-10-24
draft: false
category: "datas"
tags: ["calendário", "lua", "astronomia"]
keywords: ["calendário lunar 2026", "calendário lunar 2026 online", "calendário", "lua", "astronomia"]
---
<!--sudah dikerjakan-->

Basta escolher o mês abaixo e clicar em **Ver Calendário** para ver as fases da lua de 2026.

<div id="calc-lunar" style="max-width:560px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌙 Calendário Lunar 2026</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o mês e veja as fases da lua e a iluminação de cada dia.</p>
<label for="lua-mes" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Mês</label>
<select id="lua-mes" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="0">Janeiro</option>
<option value="1">Fevereiro</option>
<option value="2">Março</option>
<option value="3">Abril</option>
<option value="4">Maio</option>
<option value="5">Junho</option>
<option value="6">Julho</option>
<option value="7">Agosto</option>
<option value="8">Setembro</option>
<option value="9">Outubro</option>
<option value="10">Novembro</option>
<option value="11">Dezembro</option>
<option value="12">Ano inteiro</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="lua-ver" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Ver Calendário</button>
<button type="button" id="lua-hoje" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Hoje</button>
</div>
<div id="lua-calendario" style="margin-top:20px;"></div>
<div id="lua-resposta" aria-live="polite" style="margin-top:4px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="lua-resultado">clique em um dia do calendário para ver os detalhes.</span></div>
</div>
<script>
(function () {
  var NOMES = ['janeiro', 'fevereiro', 'março', 'abril', 'maio', 'junho', 'julho', 'agosto', 'setembro', 'outubro', 'novembro', 'dezembro'];
  var DIAS = ['domingo', 'segunda-feira', 'terça-feira', 'quarta-feira', 'quinta-feira', 'sexta-feira', 'sábado'];
  var CURTOS = ['Dom', 'Seg', 'Ter', 'Qua', 'Qui', 'Sex', 'Sáb'];
  var FASES = { C: 'Lua Cheia', M: 'Quarto Minguante', N: 'Lua Nova', Q: 'Quarto Crescente' };
  var DADOS = [
    'C3@07:04,M10@12:49,N18@16:53,Q26@01:48',
    'C1@19:10,M9@09:44,N17@09:03,Q24@09:28',
    'C3@08:39,M11@06:41,N18@22:26,Q25@16:19',
    'C1@23:13,M10@01:55,N17@08:54,Q23@23:33',
    'C1@14:24,M9@18:13,N16@17:03,Q23@08:12,C31@05:46',
    'M8@07:03,N14@23:56,Q21@18:55,C29@20:58',
    'M7@16:30,N14@06:45,Q21@08:05,C29@11:37',
    'M5@23:22,N12@14:37,Q19@23:46,C28@01:19',
    'M4@04:52,N11@00:27,Q18@17:44,C26@13:50',
    'M3@10:26,N10@12:50,Q18@13:13,C26@01:13',
    'M1@17:30,N9@04:02,Q17@08:48,C24@11:55',
    'M1@03:10,N8@21:52,Q17@02:43,C23@22:29,M30@16:00'
  ];
  var BASE = 'display:flex;flex-direction:column;align-items:center;gap:3px;padding:6px 0;border:1px solid #e0e7ff;border-radius:8px;background:#ffffff;color:#1e293b;cursor:pointer;font-family:inherit;min-width:0;';
  var EVT = 'border:2px solid #6366f1;background:#eef2ff;';
  var HOJE = 'box-shadow:0 0 0 2px #4f46e5;';
  var SEL = 'background:#c7d2fe;border-color:#4f46e5;';
  var NS = 'http://www.w3.org/2000/svg';
  var EV = [];
  DADOS.forEach(function (linha, m) {
    linha.split(',').forEach(function (s) {
      var a = s.indexOf('@');
      EV.push({ m: m, d: parseInt(s.substring(1, a), 10), t: s.charAt(0), h: s.substring(a + 1) });
    });
  });
  var seletor = document.getElementById('lua-mes');
  var area = document.getElementById('lua-calendario');
  var caixa = document.getElementById('lua-resposta');
  var resultado = document.getElementById('lua-resultado');
  var hoje = new Date();
  var hojeM = hoje.getFullYear() === 2026 ? hoje.getMonth() : -1;
  var hojeD = hoje.getDate();
  var selecionado = null;
  var padrao = null;
  function dd(n) { return ('0' + n).slice(-2); }
  function rad(g) { return g * Math.PI / 180; }
  function el(tag, css, texto, pai) {
    var e = document.createElement(tag);
    if (css) { e.style.cssText = css; }
    if (texto) { e.textContent = texto; }
    if (pai) { pai.appendChild(e); }
    return e;
  }
  function eventoDo(m, d) {
    return EV.filter(function (e) { return e.m === m && e.d === d; })[0];
  }
  function crescente(m, d) {
    var ult = null;
    EV.forEach(function (e) { if (e.m < m || (e.m === m && e.d < d)) { ult = e; } });
    return ult === null ? true : (ult.t === 'N' || ult.t === 'Q');
  }
  function iluminacao(m, d) {
    var T = (Date.UTC(2026, m, d, 3, 0, 0) / 86400000 + 2440587.5 - 2451545) / 36525;
    var D = 297.8501921 + 445267.1114034 * T - 0.0018819 * T * T;
    var M = 357.5291092 + 35999.0502909 * T - 0.0001536 * T * T;
    var P = 134.9633964 + 477198.8675055 * T + 0.0087414 * T * T;
    var i = 180 - D - 6.289 * Math.sin(rad(P)) + 2.1 * Math.sin(rad(M)) - 1.274 * Math.sin(rad(2 * D - P)) - 0.658 * Math.sin(rad(2 * D)) - 0.214 * Math.sin(rad(2 * P)) - 0.11 * Math.sin(rad(D));
    return (1 + Math.cos(rad(i))) / 2;
  }
  function lua(k, cresc, tam) {
    var s = document.createElementNS(NS, 'svg');
    s.setAttribute('viewBox', '0 0 28 28');
    s.setAttribute('width', tam);
    s.setAttribute('height', tam);
    s.setAttribute('aria-hidden', 'true');
    var base = document.createElementNS(NS, 'circle');
    base.setAttribute('cx', '14');
    base.setAttribute('cy', '14');
    base.setAttribute('r', '12');
    base.setAttribute('fill', '#312e81');
    base.setAttribute('stroke', '#a5b4fc');
    base.setAttribute('stroke-width', '1');
    s.appendChild(base);
    var luz;
    if (k >= 0.995) {
      luz = document.createElementNS(NS, 'circle');
      luz.setAttribute('cx', '14');
      luz.setAttribute('cy', '14');
      luz.setAttribute('r', '12');
    } else if (k > 0.005) {
      var fora = cresc ? 0 : 1;
      var dentro = k > 0.5 ? fora : 1 - fora;
      var rx = 12 * Math.abs(2 * k - 1);
      luz = document.createElementNS(NS, 'path');
      luz.setAttribute('d', 'M14 2 A12 12 0 0 ' + fora + ' 14 26 A' + rx.toFixed(2) + ' 12 0 0 ' + dentro + ' 14 2 Z');
    }
    if (luz) {
      luz.setAttribute('fill', '#fef3c7');
      s.appendChild(luz);
    }
    return s;
  }
  function nomeFase(k, cr, ev) {
    if (ev) { return FASES[ev.t]; }
    if (k <= 0.03) { return 'Lua Nova'; }
    if (k >= 0.97) { return 'Lua Cheia'; }
    if (cr) { return k < 0.5 ? 'Lua Crescente' : 'Gibosa Crescente'; }
    return k < 0.5 ? 'Lua Minguante' : 'Gibosa Minguante';
  }
  function zerar() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'clique em um dia do calendário para ver os detalhes.';
  }
  function escolher(b, m, d, k, cr, ev) {
    if (selecionado) { selecionado.style.cssText = selecionado.base; }
    selecionado = b;
    b.style.cssText = b.base + SEL;
    var dt = new Date(2026, m, d);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode(DIAS[dt.getDay()] + ', ' + d + ' de ' + NOMES[m] + ' de 2026: '));
    el('strong', 'font-size:1.2rem;', nomeFase(k, cr, ev), resultado);
    el('br', '', '', resultado);
    var detalhe = 'Iluminação de ' + Math.round(k * 100) + '% (' + (cr ? 'aumentando' : 'diminuindo') + ' a cada dia).';
    if (ev) { detalhe += ' ' + FASES[ev.t] + ' às ' + ev.h + ' (horário de Brasília).'; }
    el('small', 'color:#475569;', detalhe, resultado);
  }
  function celula(m, d) {
    var k = iluminacao(m, d);
    var cr = crescente(m, d);
    var ev = eventoDo(m, d);
    var css = BASE;
    if (ev) { css += EVT; }
    if (m === hojeM && d === hojeD) { css += HOJE; }
    var b = el('button', css, '', null);
    b.type = 'button';
    b.base = css;
    b.title = dd(d) + '/' + dd(m + 1) + ': ' + Math.round(k * 100) + '% iluminada';
    el('span', 'font-size:0.85rem;font-weight:700;color:#3730a3;line-height:1;', String(d), b);
    b.appendChild(lua(k, cr, 26));
    el('span', 'font-size:0.68rem;color:#64748b;line-height:1;', Math.round(k * 100) + '%', b);
    b.addEventListener('click', function () { escolher(b, m, d, k, cr, ev); });
    if (m === hojeM && d === hojeD) { padrao = function () { escolher(b, m, d, k, cr, ev); }; }
    return b;
  }
  function mes(m, pai) {
    var bloco = el('div', 'margin-bottom:20px;', '', pai);
    el('div', 'font-weight:700;font-size:1.05rem;color:#3730a3;margin-bottom:8px;', NOMES[m].charAt(0).toUpperCase() + NOMES[m].slice(1) + ' de 2026', bloco);
    var grade = el('div', 'display:grid;grid-template-columns:repeat(7,minmax(0,1fr));gap:4px;', '', bloco);
    CURTOS.forEach(function (c) {
      el('div', 'text-align:center;font-size:0.75rem;font-weight:600;color:#64748b;padding-bottom:2px;', c, grade);
    });
    var inicio = new Date(2026, m, 1).getDay();
    var total = new Date(2026, m + 1, 0).getDate();
    for (var v = 0; v !== inicio; v++) { el('div', '', '', grade); }
    for (var d = 1; d !== total + 1; d++) { grade.appendChild(celula(m, d)); }
    var lista = el('div', 'margin-top:10px;font-size:0.85rem;color:#475569;line-height:1.8;', '', bloco);
    EV.filter(function (e) { return e.m === m; }).forEach(function (e) {
      var linha = el('div', 'display:flex;align-items:center;gap:8px;', '', lista);
      linha.appendChild(lua(e.t === 'N' ? 0 : (e.t === 'C' ? 1 : 0.5), e.t === 'Q', 18));
      el('span', '', FASES[e.t] + ': ' + dd(e.d) + '/' + dd(m + 1) + ' às ' + e.h, linha);
    });
  }
  function mostrar() {
    var v = parseInt(seletor.value, 10);
    area.textContent = '';
    selecionado = null;
    padrao = null;
    zerar();
    if (v === 12) {
      for (var m = 0; m !== 12; m++) { mes(m, area); }
    } else {
      mes(v, area);
    }
    if (padrao) { padrao(); }
  }
  function irParaHoje() {
    seletor.value = String(hojeM === -1 ? 0 : hojeM);
    mostrar();
  }
  document.getElementById('lua-ver').addEventListener('click', mostrar);
  document.getElementById('lua-hoje').addEventListener('click', irParaHoje);
  seletor.addEventListener('change', mostrar);
  seletor.addEventListener('focus', function () { seletor.style.borderColor = '#6366f1'; });
  seletor.addEventListener('blur', function () { seletor.style.borderColor = '#c7d2fe'; });
  irParaHoje();
})();
</script>

## Como usar o calendário lunar

1. Escolha o mês no campo **Mês**. Para ver os doze meses de uma vez, selecione **Ano inteiro**.
2. Clique em **Ver Calendário**. O calendário também atualiza sozinho quando você troca o mês.
3. Em cada dia, veja o desenho da lua e, logo abaixo, a porcentagem de iluminação.
4. Os dias com borda destacada marcam uma mudança de fase. A lista abaixo de cada mês mostra o dia e o horário exato.
5. Clique em qualquer dia para ver a fase, a iluminação e o horário na caixa **Resposta**.
6. Use o botão **Hoje** para voltar ao mês atual. O dia de hoje aparece com contorno azul.

Os horários seguem o fuso de Brasília (UTC-3). A porcentagem de cada dia considera a lua à meia-noite desse dia.

## Entendendo os termos

- **Fase da lua:** aspecto da parte iluminada da lua vista da Terra, que muda ao longo do mês conforme a posição da lua em relação ao Sol.
- **Lua Nova:** a lua fica entre a Terra e o Sol e a face voltada para nós não recebe luz. Ela praticamente não aparece no céu.
- **Quarto Crescente:** metade do disco lunar iluminada, com a iluminação aumentando a cada dia. Ocorre cerca de uma semana depois da Lua Nova.
- **Lua Cheia:** a face voltada para a Terra está totalmente iluminada. É a fase em que a lua aparece inteira e brilhante durante a noite.
- **Quarto Minguante:** metade do disco lunar iluminada, com a iluminação diminuindo a cada dia. Ocorre cerca de uma semana depois da Lua Cheia.
- **Lua Crescente:** fase entre a Lua Nova e o Quarto Crescente, em que aparece só uma faixa fina e iluminada.
- **Gibosa:** fase em que a lua tem mais da metade do disco iluminada, antes (crescente) ou depois (minguante) da Lua Cheia.
- **Lua Minguante:** fase entre o Quarto Minguante e a Lua Nova, com a faixa iluminada ficando cada vez mais fina.
- **Iluminação:** percentual do disco lunar que aparece iluminado. Vai de 0% na Lua Nova a 100% na Lua Cheia.
- **Crescente e minguante:** crescente é quando a iluminação aumenta de um dia para o outro; minguante é quando ela diminui.
- **Ciclo lunar:** intervalo de cerca de 29,5 dias entre duas Luas Novas (ou duas Luas Cheias). Por isso alguns meses têm duas Luas Cheias.
- **Horário de Brasília:** fuso UTC-3, usado em todos os horários desta página.
- **Hemisfério Sul:** os desenhos seguem o que se vê no Brasil, onde a lua crescente tem o lado iluminado à esquerda e a minguante, à direita.