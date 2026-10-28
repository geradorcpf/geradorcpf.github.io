---
title: "Fase da Lua Hoje"
seoTitle: "Fase da Lua Hoje"
description: "Fase da Lua Hoje: veja a fase da lua de hoje. Grátis e online, sem cadastro."
summary: "Veja a fase da lua de hoje."
date: 2026-10-28
draft: false
category: "datas"
tags: ["lua", "astronomia", "calendário"]
keywords: ["fase da lua hoje", "fase da lua hoje online", "lua", "astronomia", "calendário"]
---

Veja abaixo a fase da lua de hoje. Se quiser, escolha outra data e clique em **Ver Fase**.

<div id="calc-lua" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌙 Fase da Lua Hoje</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Veja a fase, a visibilidade e a idade da lua na hora.</p>
<label for="lua-data" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data (opcional)</label>
<input id="lua-data" type="date" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="lua-ver" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Ver Fase</button>
<button type="button" id="lua-hoje" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Hoje</button>
</div>
<div id="lua-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;">
<div id="lua-imagem" style="text-align:center;margin-bottom:8px;"></div>
<div style="text-align:center;font-size:1.3rem;font-weight:700;color:#3730a3;" id="lua-fase">Calculando...</div>
<div style="margin-top:12px;"><strong style="color:#3730a3;">Visibilidade:</strong> <span id="lua-visib">-</span></div>
<div><strong style="color:#3730a3;">Distância:</strong> <span id="lua-dist">-</span></div>
<div><strong style="color:#3730a3;">Idade:</strong> <span id="lua-idade">-</span></div>
<div style="margin-top:12px;" id="lua-desc"></div>
<div id="lua-prox"></div>
</div>
</div>
<script>
(function () {
  var SINODICO = 29.530588853;
  var NS = 'http://www.w3.org/2000/svg';
  var campoData = document.getElementById('lua-data');
  var caixa = document.getElementById('lua-resposta');
  function el(id) { return document.getElementById(id); }
  function fmt(n, d) { return n.toLocaleString('pt-BR', { minimumFractionDigits: d, maximumFractionDigits: d }); }
  function rad(g) { return g * Math.PI / 180; }
  function plural(n, s, p) { return n + ' ' + (n === 1 ? s : p); }
  function doisDigitos(n) { return (n > 9 ? '' : '0') + n; }
  function dataIso(d) { return d.getFullYear() + '-' + doisDigitos(d.getMonth() + 1) + '-' + doisDigitos(d.getDate()); }
  function juliano(d) { return d.getTime() / 86400000 + 2440587.5; }
  function idadeLua(jd) {
    var x = (jd - 2451550.1) % SINODICO;
    return x >= 0 ? x : x + SINODICO;
  }
  function distanciaLua(jd) {
    var t = (jd - 2451545) / 36525;
    var d = rad(297.8502 + 445267.1115 * t);
    var m = rad(134.9634 + 477198.8676 * t);
    return 385000.56
      - 20905.355 * Math.cos(m)
      - 3699.111 * Math.cos(2 * d - m)
      - 2955.968 * Math.cos(2 * d)
      - 569.925 * Math.cos(2 * m)
      + 246.158 * Math.cos(2 * d - 2 * m)
      - 170.733 * Math.cos(2 * d + m);
  }
  function nomeFase(vis, crescendo) {
    if (5 >= vis) { return 'Lua Nova'; }
    if (vis >= 95) { return 'Lua Cheia'; }
    if (crescendo) {
      if (45 >= vis) { return 'Lua Crescente'; }
      if (55 >= vis) { return 'Quarto Crescente'; }
      return 'Gibosa Crescente';
    }
    if (45 >= vis) { return 'Lua Minguante'; }
    if (55 >= vis) { return 'Quarto Minguante'; }
    return 'Gibosa Minguante';
  }
  function proximaFase(idade) {
    var alvos = [[0, 'Lua Nova'], [7.382647, 'Quarto Crescente'], [14.765294, 'Lua Cheia'], [22.147941, 'Quarto Minguante'], [SINODICO, 'Lua Nova']];
    for (var i = 0; alvos.length > i; i++) {
      if (alvos[i][0] > idade) { return { nome: alvos[i][1], falta: alvos[i][0] - idade }; }
    }
    return { nome: 'Lua Nova', falta: 0 };
  }
  function criar(tag, attrs) {
    var e = document.createElementNS(NS, tag);
    Object.keys(attrs).forEach(function (k) { e.setAttribute(k, attrs[k]); });
    return e;
  }
  function desenhar(fracao, crescendo) {
    var r = 60, c = 70;
    var rx = r * Math.abs(1 - 2 * fracao);
    var gibosa = fracao > 0.5;
    var svg = criar('svg', { viewBox: '0 0 140 140', width: '140', height: '140', role: 'img', 'aria-label': 'Imagem da fase da lua' });
    svg.appendChild(criar('circle', { cx: c, cy: c, r: r, fill: '#1e293b', stroke: '#c7d2fe', 'stroke-width': '2' }));
    if (fracao > 0.005) {
      var varreExterno = crescendo ? 0 : 1;
      var varreInterno = crescendo ? (gibosa ? 0 : 1) : (gibosa ? 1 : 0);
      var d = 'M ' + c + ' ' + (c - r) + ' A ' + r + ' ' + r + ' 0 0 ' + varreExterno + ' ' + c + ' ' + (c + r) + ' A ' + rx + ' ' + r + ' 0 0 ' + varreInterno + ' ' + c + ' ' + (c - r) + ' Z';
      svg.appendChild(criar('path', { d: d, fill: '#fef9c3' }));
    }
    var alvo = el('lua-imagem');
    alvo.textContent = '';
    alvo.appendChild(svg);
  }
  var DESCRICOES = {
    'Lua Nova': 'A lua está entre a Terra e o Sol, com o lado iluminado voltado para longe de nós. Ela quase não aparece no céu.',
    'Lua Crescente': 'Uma pequena parte da lua já aparece iluminada e essa parte aumenta a cada noite.',
    'Quarto Crescente': 'Metade do disco lunar está iluminada e a parte visível continua aumentando.',
    'Gibosa Crescente': 'Mais da metade da lua está iluminada e ela caminha para a lua cheia.',
    'Lua Cheia': 'Todo o lado voltado para a Terra está iluminado. É a fase mais brilhante da lua.',
    'Gibosa Minguante': 'Mais da metade da lua ainda está iluminada, mas a parte visível diminui a cada noite.',
    'Quarto Minguante': 'Metade do disco lunar está iluminada e a parte visível continua diminuindo.',
    'Lua Minguante': 'Só uma pequena parte da lua está iluminada e ela caminha para a lua nova.'
  };
  function calcular(data, hoje) {
    var jd = juliano(data);
    var idade = idadeLua(jd);
    var fracao = (1 - Math.cos(2 * Math.PI * idade / SINODICO)) / 2;
    var vis = fracao * 100;
    var crescendo = SINODICO / 2 > idade;
    var fase = nomeFase(vis, crescendo);
    var prox = proximaFase(idade);
    var horas = Math.round(prox.falta * 24);
    var dias = Math.floor(horas / 24);
    var resto = horas % 24;
    desenhar(fracao, crescendo);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    el('lua-fase').textContent = fase;
    el('lua-visib').textContent = fmt(vis, 2) + '%';
    el('lua-dist').textContent = fmt(distanciaLua(jd), 0) + ' km (estimativa)';
    el('lua-idade').textContent = fmt(idade, 2) + ' dias';
    var quando = hoje ? 'A lua de hoje' : 'A lua nesse dia';
    var sentido = crescendo ? 'crescendo' : 'decrescendo';
    el('lua-desc').textContent = quando + ' está ' + fmt(vis, 2) + '% visível e está ' + sentido + '. ' + DESCRICOES[fase];
    el('lua-prox').textContent = 'Faltam ' + plural(dias, 'dia', 'dias') + ' e ' + plural(resto, 'hora', 'horas') + ' para a fase ' + prox.nome + '.';
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    el('lua-fase').textContent = msg;
  }
  function verFase() {
    var v = campoData.value;
    if (v === '') { mostrarHoje(); return; }
    var p = v.split('-');
    var data = new Date(Number(p[0]), Number(p[1]) - 1, Number(p[2]), 12, 0, 0);
    if (isNaN(data.getTime())) { erro('informe uma data válida.'); return; }
    calcular(data, v === dataIso(new Date()));
  }
  function mostrarHoje() {
    campoData.value = dataIso(new Date());
    calcular(new Date(), true);
  }
  el('lua-ver').addEventListener('click', verFase);
  el('lua-hoje').addEventListener('click', mostrarHoje);
  campoData.addEventListener('keydown', function (e) { if (e.key === 'Enter') { verFase(); } });
  campoData.addEventListener('focus', function () { campoData.style.borderColor = '#6366f1'; });
  campoData.addEventListener('blur', function () { campoData.style.borderColor = '#c7d2fe'; });
  mostrarHoje();
})();
</script>

## Como usar a ferramenta

1. Ao abrir a página, a ferramenta já mostra a fase da lua de hoje.
2. Para ver outro dia, escolha uma data no campo **Data (opcional)**.
3. Clique em **Ver Fase** (ou pressione Enter) para atualizar o resultado.
4. Use o botão **Hoje** para voltar à data atual.

O resultado traz a imagem da lua, o nome da fase, a visibilidade, a distância, a idade, uma breve descrição e o tempo que falta para a próxima fase principal. Os valores são calculados por aproximação e podem ter pequenas diferenças em relação a outros sites ou observatórios.

## Entendendo os termos

- **Fase da lua:** aparência da lua vista da Terra, que muda conforme a posição dela em relação ao Sol e à Terra.
- **Lua Nova:** fase em que a lua não é visível, pois o lado iluminado está voltado para o Sol.
- **Lua Crescente:** fase em que uma pequena parte da lua está iluminada e aumenta a cada dia.
- **Quarto Crescente:** fase em que metade da lua está iluminada e a parte visível está aumentando.
- **Gibosa Crescente:** fase em que mais da metade da lua está iluminada e ainda aumenta.
- **Lua Cheia:** fase em que todo o disco lunar voltado para a Terra está iluminado.
- **Gibosa Minguante:** fase em que mais da metade da lua está iluminada, mas a parte visível diminui.
- **Quarto Minguante:** fase em que metade da lua está iluminada e a parte visível está diminuindo.
- **Lua Minguante:** fase em que uma pequena parte da lua está iluminada e diminui a cada dia.
- **Visibilidade:** porcentagem do disco lunar que aparece iluminada para quem está na Terra.
- **Distância:** espaço entre a Terra e a lua, em quilômetros. Ele varia porque a órbita da lua não é um círculo perfeito.
- **Idade:** número de dias desde a última lua nova. Um ciclo completo dura cerca de 29,5 dias.
- **Crescendo / decrescendo:** indica se a parte iluminada visível está aumentando (da lua nova até a cheia) ou diminuindo (da lua cheia até a nova).
- **Próxima fase:** tempo restante até a próxima fase principal: lua nova, quarto crescente, lua cheia ou quarto minguante.