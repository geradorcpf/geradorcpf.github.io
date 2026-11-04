---
title: "Hora Certa"
seoTitle: "Hora Certa"
description: "Hora Certa: veja a hora certa agora, com data e fuso horário. Grátis e online, sem cadastro."
summary: "Veja a hora certa agora, com data e fuso horário."
date: 2026-11-04
draft: false
category: "datas"
tags: ["hora", "relógio", "datas"]
keywords: ["hora certa", "hora certa online", "hora", "relógio", "datas"]
---

Veja abaixo a hora certa agora no seu dispositivo e nas principais cidades do Brasil e do mundo. Você também pode adicionar outras cidades à lista.

<div id="hora-certa" style="max-width:520px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🕐 Hora Certa</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Hora, data e fuso horário atualizados a cada segundo.</p>
<div aria-live="off" style="margin-bottom:20px;padding:16px;background:#f0fdf4;border:2px solid #86efac;border-radius:12px;color:#166534;font-size:1rem;line-height:1.6;text-align:center;">
<strong style="color:#3730a3;">Hora no seu dispositivo</strong><br>
<span id="hc-local-hora" style="display:block;font-size:2.4rem;font-weight:700;letter-spacing:1px;">--:--:--</span>
<span id="hc-local-data" style="display:block;color:#475569;font-size:0.95rem;"></span>
<small id="hc-local-zona" style="color:#475569;"></small>
</div>
<strong style="display:block;margin-bottom:10px;color:#3730a3;">Cidades</strong>
<div id="hc-lista" style="display:flex;flex-direction:column;gap:10px;margin-bottom:20px;"></div>
<label for="hc-cidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Adicionar cidade</label>
<select id="hc-cidade" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="hc-adicionar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Adicionar</button>
<button type="button" id="hc-restaurar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Restaurar lista</button>
</div>
</div>
<script>
(function () {
  var catalogo = [
    ['Brasília', 'America/Sao_Paulo'],
    ['Manaus', 'America/Manaus'],
    ['Fernando de Noronha', 'America/Noronha'],
    ['São Paulo', 'America/Sao_Paulo'],
    ['Recife', 'America/Recife'],
    ['Fortaleza', 'America/Fortaleza'],
    ['Salvador', 'America/Bahia'],
    ['Cuiabá', 'America/Cuiaba'],
    ['Rio de Janeiro', 'America/Sao_Paulo'],
    ['Belém', 'America/Belem'],
    ['Porto Alegre', 'America/Sao_Paulo'],
    ['Rio Branco', 'America/Rio_Branco'],
    ['Lisboa', 'Europe/Lisbon'],
    ['Londres', 'Europe/London'],
    ['Paris', 'Europe/Paris'],
    ['Madri', 'Europe/Madrid'],
    ['Roma', 'Europe/Rome'],
    ['Berlim', 'Europe/Berlin'],
    ['Nova York', 'America/New_York'],
    ['Chicago', 'America/Chicago'],
    ['Los Angeles', 'America/Los_Angeles'],
    ['Cidade do México', 'America/Mexico_City'],
    ['Buenos Aires', 'America/Argentina/Buenos_Aires'],
    ['Dubai', 'Asia/Dubai'],
    ['Jacarta', 'Asia/Jakarta'],
    ['Tóquio', 'Asia/Tokyo'],
    ['Pequim', 'Asia/Shanghai'],
    ['Sydney', 'Australia/Sydney'],
    ['UTC (Tempo Universal)', 'UTC']
  ];
  var padrao = [0, 1, 2, 3, 4, 5, 6, 7, 8];
  var chave = 'hora-certa-cidades';
  var selecionadas = padrao.slice();
  var linhas = [];
  var agora = new Date();
  var cacheFmt = {};
  var lista = document.getElementById('hc-lista');
  var seletor = document.getElementById('hc-cidade');
  var estCard = 'display:flex;justify-content:space-between;align-items:center;gap:12px;padding:12px 14px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;';
  var estBotaoRemover = 'padding:2px 10px;font-size:1.1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
  function el(tag, estilo, texto) {
    var e = document.createElement(tag);
    if (estilo) { e.setAttribute('style', estilo); }
    if (texto) { e.textContent = texto; }
    return e;
  }
  function formatador(id, zona, opcoes, idioma) {
    var k = id + '|' + zona;
    if (!cacheFmt[k]) {
      opcoes.timeZone = zona;
      cacheFmt[k] = new Intl.DateTimeFormat(idioma, opcoes);
    }
    return cacheFmt[k];
  }
  function fmtHora(zona) {
    return formatador('h', zona, { hour: '2-digit', minute: '2-digit', second: '2-digit', hourCycle: 'h23' }, 'pt-BR').format(agora);
  }
  function fmtData(zona) {
    var t = formatador('d', zona, { weekday: 'long', day: 'numeric', month: 'long', year: 'numeric' }, 'pt-BR').format(agora);
    return t.charAt(0).toUpperCase() + t.slice(1);
  }
  function fmtOffset(zona) {
    var k = 'o|' + zona;
    if (!cacheFmt[k]) {
      try {
        cacheFmt[k] = new Intl.DateTimeFormat('en-US', { timeZone: zona, timeZoneName: 'longOffset' });
      } catch (e) {
        cacheFmt[k] = new Intl.DateTimeFormat('en-US', { timeZone: zona, timeZoneName: 'short' });
      }
    }
    var nome = '';
    cacheFmt[k].formatToParts(agora).forEach(function (p) {
      if (p.type === 'timeZoneName') { nome = p.value; }
    });
    nome = nome.replace('GMT', 'UTC');
    return nome === 'UTC' ? 'UTC+00:00' : nome;
  }
  var zonaLocal = 'UTC';
  try {
    zonaLocal = Intl.DateTimeFormat().resolvedOptions().timeZone || 'UTC';
  } catch (e) {
    zonaLocal = 'UTC';
  }
  function salvar() {
    try { localStorage.setItem(chave, JSON.stringify(selecionadas)); } catch (e) {}
  }
  function carregar() {
    try {
      var bruto = localStorage.getItem(chave);
      if (bruto) {
        var lido = JSON.parse(bruto);
        if (Array.isArray(lido)) {
          selecionadas = lido.filter(function (i) { return typeof i === 'number' && catalogo[i] !== undefined; });
        }
      }
    } catch (e) {
      selecionadas = padrao.slice();
    }
  }
  function preencherSeletor() {
    while (seletor.firstChild) { seletor.removeChild(seletor.firstChild); }
    catalogo.forEach(function (c, i) {
      if (selecionadas.indexOf(i) === -1) {
        var o = document.createElement('option');
        o.value = String(i);
        o.textContent = c[0];
        seletor.appendChild(o);
      }
    });
  }
  function desenhar() {
    while (lista.firstChild) { lista.removeChild(lista.firstChild); }
    linhas = [];
    if (selecionadas.length === 0) {
      lista.appendChild(el('span', 'color:#64748b;font-size:0.95rem;', 'Nenhuma cidade na lista. Adicione uma cidade abaixo.'));
    }
    selecionadas.forEach(function (idx) {
      var c = catalogo[idx];
      var card = el('div', estCard);
      var esq = el('div', 'min-width:0;');
      var nome = el('strong', 'display:block;color:#3730a3;font-size:1rem;', c[0]);
      var dataEl = el('span', 'display:block;color:#475569;font-size:0.85rem;', '');
      var zonaEl = el('small', 'color:#64748b;', '');
      esq.appendChild(nome);
      esq.appendChild(dataEl);
      esq.appendChild(zonaEl);
      var dir = el('div', 'display:flex;align-items:center;gap:10px;');
      var horaEl = el('span', 'font-size:1.5rem;font-weight:700;color:#166534;', '--:--:--');
      var rem = el('button', estBotaoRemover, '\u00d7');
      rem.type = 'button';
      rem.setAttribute('aria-label', 'Remover ' + c[0]);
      rem.addEventListener('click', function () {
        selecionadas = selecionadas.filter(function (i) { return i !== idx; });
        salvar();
        desenhar();
        preencherSeletor();
      });
      dir.appendChild(horaEl);
      dir.appendChild(rem);
      card.appendChild(esq);
      card.appendChild(dir);
      lista.appendChild(card);
      linhas.push({ zona: c[1], hora: horaEl, data: dataEl, fuso: zonaEl });
    });
    atualizar();
  }
  function atualizar() {
    agora = new Date();
    document.getElementById('hc-local-hora').textContent = fmtHora(zonaLocal);
    document.getElementById('hc-local-data').textContent = fmtData(zonaLocal);
    document.getElementById('hc-local-zona').textContent = zonaLocal.replace(/_/g, ' ') + ' (' + fmtOffset(zonaLocal) + ')';
    linhas.forEach(function (l) {
      l.hora.textContent = fmtHora(l.zona);
      l.data.textContent = fmtData(l.zona);
      l.fuso.textContent = fmtOffset(l.zona);
    });
  }
  function adicionar() {
    if (seletor.value === '') { return; }
    var idx = Number(seletor.value);
    if (selecionadas.indexOf(idx) === -1) { selecionadas.push(idx); }
    salvar();
    desenhar();
    preencherSeletor();
  }
  function restaurar() {
    selecionadas = padrao.slice();
    salvar();
    desenhar();
    preencherSeletor();
  }
  document.getElementById('hc-adicionar').addEventListener('click', adicionar);
  document.getElementById('hc-restaurar').addEventListener('click', restaurar);
  seletor.addEventListener('focus', function () { seletor.style.borderColor = '#6366f1'; });
  seletor.addEventListener('blur', function () { seletor.style.borderColor = '#c7d2fe'; });
  carregar();
  desenhar();
  preencherSeletor();
  setInterval(atualizar, 1000);
})();
</script>

## Como usar a ferramenta

1. Veja no quadro verde a **hora certa** do seu dispositivo, com a data e o fuso horário.
2. Confira na lista **Cidades** a hora atual de cada cidade (Brasília, Manaus, Fernando de Noronha e outras).
3. Para incluir outra cidade, escolha-a no campo **Adicionar cidade** e clique em **Adicionar**.
4. Para tirar uma cidade da lista, clique no botão **×** ao lado do horário dela.
5. Clique em **Restaurar lista** para voltar às cidades mais populares.

A hora é atualizada automaticamente a cada segundo, sem precisar recarregar a página. O horário é calculado a partir do relógio do seu dispositivo, então ele precisa estar com a data e a hora corretas. A lista de cidades fica salva no seu navegador.

## Entendendo os termos

- **Hora certa:** horário exato neste momento em determinado lugar, usado como referência para acertar relógios e marcar compromissos.
- **Fuso horário:** faixa do planeta que adota o mesmo horário oficial. A Terra é dividida em 24 fusos principais, e a hora muda de um fuso para outro.
- **UTC:** sigla de Tempo Universal Coordenado, o padrão mundial de referência para as horas. Os demais fusos são definidos pela diferença em relação a ele, como UTC-03:00.
- **Diferença de fuso (offset):** número de horas que um lugar está adiantado (+) ou atrasado (-) em relação ao UTC. Em Brasília, por exemplo, é de UTC-03:00.
- **Horário de Brasília:** horário oficial do Brasil, usado como referência nacional, equivalente a UTC-03:00.
- **Fernando de Noronha:** arquipélago brasileiro que está um fuso à frente de Brasília (UTC-02:00).
- **Horário de verão:** adiantamento do relógio em uma hora durante o verão. No Brasil ele não é mais aplicado desde 2019, mas outros países ainda o utilizam, o que altera a diferença de horas ao longo do ano.
- **Formato 24 horas:** forma de mostrar as horas de 00 a 23, sem usar AM e PM.
- **Data:** dia da semana, dia do mês, mês e ano correspondentes ao horário da cidade. Ela pode ser diferente entre cidades distantes.