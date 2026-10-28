---
title: "Estação do Ano Hoje"
seoTitle: "Estação do Ano Hoje"
description: "Estação do Ano Hoje: veja em qual estação do ano estamos e quando muda. Grátis e online, sem cadastro."
summary: "Veja em qual estação do ano estamos e quando muda."
date: 2026-10-28
draft: false
category: "datas"
tags: ["estações do ano", "calendário", "datas"]
keywords: ["estação do ano hoje", "estação do ano hoje online", "estações do ano", "calendário", "datas"]
---

Veja abaixo em qual estação do ano estamos hoje e quando começa a próxima. Se quiser, clique em **Atualizar** para recalcular com a data e a hora atuais.

<div id="calc-estacao" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌤️ Estação do Ano Hoje</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Estação atual, próximas estações e contagem regressiva.</p>
<div id="est-atual" aria-live="polite" style="padding:16px;margin-bottom:16px;background:#f0fdf4;border:2px solid #86efac;border-radius:12px;color:#166534;font-size:1rem;line-height:1.6;"><strong style="color:#166534;">Estação atual:</strong> <span id="est-atual-nome" style="font-size:1.2rem;font-weight:700;">carregando...</span><br><span id="est-atual-data" style="font-size:0.9rem;color:#475569;"></span></div>
<div id="est-contagem" aria-live="polite" style="padding:16px;margin-bottom:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Contagem:</strong> <span id="est-contagem-texto">carregando...</span></div>
<div style="margin-bottom:8px;font-weight:600;font-size:0.95rem;">Próximas estações</div>
<div id="est-lista" style="margin-bottom:20px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="est-atualizar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Atualizar</button>
</div>
<p style="margin:16px 0 0;font-size:0.8rem;color:#64748b;">Os dados apresentados são do hemisfério sul e horário de Brasília.</p>
</div>
<script>
(function () {
  var TERMOS = [
    [485, 324.96, 1934.136], [203, 337.23, 32964.467], [199, 342.08, 20.186],
    [182, 27.85, 445267.112], [156, 73.14, 45036.886], [136, 171.52, 22518.443],
    [77, 222.54, 65928.934], [74, 296.72, 3034.906], [70, 243.58, 9037.513],
    [58, 119.81, 33718.147], [52, 297.17, 150.678], [50, 21.02, 2281.226],
    [45, 247.54, 29929.562], [44, 325.15, 31555.956], [29, 60.93, 4443.417],
    [18, 155.12, 67555.328], [17, 288.79, 4562.452], [16, 198.04, 62894.029],
    [14, 199.76, 31436.921], [12, 95.39, 14577.848], [12, 287.11, 31931.756],
    [12, 320.81, 34777.259], [9, 227.73, 1222.114], [8, 15.45, 16859.074]
  ];
  var NOMES = ['Outono', 'Inverno', 'Primavera', 'Verão'];
  var ICONES = ['🍂', '❄️', '🌸', '☀️'];
  var MESES = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
  var RAD = Math.PI / 180;
  var OFFSET_BRASILIA = 3 * 3600000;
  var DELTA_T = 69 * 1000;
  var elAtualNome = document.getElementById('est-atual-nome');
  var elAtualData = document.getElementById('est-atual-data');
  var elContagem = document.getElementById('est-contagem-texto');
  var elLista = document.getElementById('est-lista');
  function jdeBase(ano, tipo) {
    var y = (ano - 2000) / 1000;
    if (tipo === 0) { return 2451623.80984 + 365242.37404 * y + 0.05169 * y * y - 0.00411 * y * y * y - 0.00057 * y * y * y * y; }
    if (tipo === 1) { return 2451716.56767 + 365241.62603 * y + 0.00325 * y * y + 0.00888 * y * y * y - 0.0003 * y * y * y * y; }
    if (tipo === 2) { return 2451810.21715 + 365242.01767 * y - 0.11575 * y * y + 0.00337 * y * y * y + 0.00078 * y * y * y * y; }
    return 2451900.05952 + 365242.74049 * y - 0.06223 * y * y - 0.00823 * y * y * y + 0.00032 * y * y * y * y;
  }
  function instante(ano, tipo) {
    var j0 = jdeBase(ano, tipo);
    var t = (j0 - 2451545.0) / 36525;
    var w = 35999.373 * t - 2.47;
    var dl = 1 + 0.0334 * Math.cos(w * RAD) + 0.0007 * Math.cos(2 * w * RAD);
    var s = 0;
    TERMOS.forEach(function (x) { s += x[0] * Math.cos((x[1] + x[2] * t) * RAD); });
    var jde = j0 + (0.00001 * s) / dl;
    return (jde - 2440587.5) * 86400000 - DELTA_T;
  }
  function eventos(ano) {
    var lista = [];
    [ano - 1, ano, ano + 1].forEach(function (a) {
      [0, 1, 2, 3].forEach(function (k) {
        lista.push({ ms: instante(a, k), tipo: k, ano: a });
      });
    });
    return lista;
  }
  function rotulo(ev) {
    return NOMES[ev.tipo] + ' ' + (ev.tipo === 3 ? ev.ano + '-' + (ev.ano + 1) : ev.ano);
  }
  function dataBrasilia(ms) {
    var d = new Date(ms - OFFSET_BRASILIA);
    var hh = String(d.getUTCHours()).padStart(2, '0');
    var mm = String(d.getUTCMinutes()).padStart(2, '0');
    return d.getUTCDate() + ' de ' + MESES[d.getUTCMonth()] + ' ' + hh + ':' + mm;
  }
  function plural(n, um, varios) { return n + ' ' + (n === 1 ? um : varios); }
  function criar(tag, estilo, texto) {
    var e = document.createElement(tag);
    if (estilo) { e.style.cssText = estilo; }
    if (texto) { e.textContent = texto; }
    return e;
  }
  function atualizar() {
    var agora = Date.now();
    var ano = new Date(agora - OFFSET_BRASILIA).getUTCFullYear();
    var todos = eventos(ano);
    var passados = todos.filter(function (e) { return agora >= e.ms; });
    var futuros = todos.filter(function (e) { return e.ms > agora; });
    var atual = passados[passados.length - 1];
    var proximos = futuros.slice(0, 3);
    elAtualNome.textContent = ICONES[atual.tipo] + ' ' + rotulo(atual);
    elAtualData.textContent = 'Começou em ' + dataBrasilia(atual.ms) + ' (horário de Brasília).';
    var falta = Math.floor((proximos[0].ms - agora) / 3600000);
    var dias = Math.floor(falta / 24);
    var horas = falta % 24;
    elContagem.textContent = 'Faltam ' + plural(dias, 'dia', 'dias') + ' e ' + plural(horas, 'hora', 'horas') + ' para o ' + NOMES[proximos[0].tipo] + '.';
    elLista.textContent = '';
    proximos.forEach(function (ev) {
      var linha = criar('div', 'display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap;padding:12px 14px;margin-bottom:8px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;');
      linha.appendChild(criar('span', 'font-weight:600;color:#3730a3;', ICONES[ev.tipo] + ' ' + rotulo(ev)));
      linha.appendChild(criar('span', 'font-size:0.9rem;color:#475569;', dataBrasilia(ev.ms)));
      elLista.appendChild(linha);
    });
  }
  document.getElementById('est-atualizar').addEventListener('click', atualizar);
  atualizar();
})();
</script>

## Como usar a ferramenta

1. Abra a página: a ferramenta já mostra automaticamente a **estação atual** com base na data e na hora do momento.
2. Veja a **contagem regressiva** para saber quantos dias e horas faltam para a próxima estação.
3. Consulte a lista **Próximas estações** para ver o dia e o horário em que cada uma começa.
4. Clique em **Atualizar** se a página ficou aberta por muito tempo e você quer recalcular tudo com a data e a hora atuais.

Os dados são do **hemisfério sul** e usam o **horário de Brasília**. Por isso, as estações e os horários valem para o Brasil.

## Entendendo os termos

- **Estação do ano:** cada um dos quatro períodos do ano (outono, inverno, primavera e verão), com características climáticas próprias.
- **Estação atual:** a estação em que estamos agora, desde o seu início até o começo da seguinte.
- **Próxima estação:** a estação que começa logo depois da atual.
- **Equinócio:** momento em que o dia e a noite têm duração quase igual. Marca o início do outono (março) e da primavera (setembro) no hemisfério sul.
- **Solstício:** momento em que o Sol atinge o ponto mais alto ou mais baixo no céu ao meio-dia. Marca o início do inverno (junho) e do verão (dezembro) no hemisfério sul.
- **Hemisfério sul:** metade da Terra ao sul da linha do Equador, onde fica a maior parte do Brasil. As estações são opostas às do hemisfério norte.
- **Horário de Brasília:** fuso horário de referência do Brasil (UTC-3), usado para mostrar o horário exato em que cada estação começa.
- **Contagem regressiva:** tempo que falta, em dias e horas, até o início da próxima estação.

## Quando começa cada estação

No hemisfério sul, as estações começam nos equinócios e solstícios:

- **Outono:** equinócio de março, por volta do dia 20.
- **Inverno:** solstício de junho, por volta do dia 21.
- **Primavera:** equinócio de setembro, por volta do dia 22.
- **Verão:** solstício de dezembro, por volta do dia 21.

As datas e os horários mudam um pouco de um ano para outro, e a ferramenta calcula o momento exato de cada um.