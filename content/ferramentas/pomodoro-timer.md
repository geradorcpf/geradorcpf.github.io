---
title: "Pomodoro Timer"
seoTitle: "Pomodoro Timer"
description: "Pomodoro Timer: temporizador Pomodoro para estudar e trabalhar com foco. Grátis e online, sem cadastro."
summary: "Temporizador Pomodoro para estudar e trabalhar com foco."
date: 2026-11-07
draft: false
category: "util"
tags: ["pomodoro", "tempo", "estudos", "produtividade"]
keywords: ["pomodoro timer", "pomodoro timer online", "pomodoro", "tempo", "estudos"]
---

Escolha o modo, clique em **Iniciar** e foque na sua tarefa até o alarme tocar.

<div id="pomodoro-timer" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🍅 Pomodoro Timer</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Foque por 25 minutos e descanse em seguida.</p>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px;">
<button type="button" id="pom-modo-pomodoro" style="flex:1;min-width:100px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Pomodoro</button>
<button type="button" id="pom-modo-curta" style="flex:1;min-width:100px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Pausa Curta</button>
<button type="button" id="pom-modo-longa" style="flex:1;min-width:100px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Pausa Longa</button>
</div>
<div style="padding:20px;margin-bottom:16px;text-align:center;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;">
<div id="pom-tempo" aria-live="off" style="font-size:3.5rem;font-weight:800;color:#3730a3;line-height:1.1;font-variant-numeric:tabular-nums;">25:00</div>
<div id="pom-foco" aria-live="polite" style="margin-top:8px;font-size:0.95rem;color:#64748b;">Adicione uma tarefa ou comece a focar.</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:24px;">
<button type="button" id="pom-iniciar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Iniciar</button>
<button type="button" id="pom-desistir" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Desistir</button>
</div>
<h3 style="margin:0 0 10px;font-size:1rem;color:#3730a3;">Tarefas</h3>
<div id="pom-lista" style="margin-bottom:10px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:24px;">
<input id="pom-nova" type="text" placeholder="Ex.: Estudar capítulo 3" autocomplete="off" maxlength="80" style="flex:1;min-width:160px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<button type="button" id="pom-adicionar" style="padding:12px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Adicionar Tarefa</button>
</div>
<h3 style="margin:0 0 10px;font-size:1rem;color:#3730a3;">Estatísticas</h3>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px;">
<button type="button" id="pom-per-semana" style="flex:1;min-width:80px;padding:8px 10px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Semana</button>
<button type="button" id="pom-per-mes" style="flex:1;min-width:80px;padding:8px 10px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Mês</button>
<button type="button" id="pom-per-ano" style="flex:1;min-width:80px;padding:8px 10px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Ano</button>
</div>
<div style="padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;font-size:1rem;line-height:1.7;">
<div><strong style="color:#3730a3;">Total:</strong> <span id="pom-total">0 pomodoros (0 min)</span></div>
<div><strong style="color:#3730a3;">Média por dia:</strong> <span id="pom-media">0 pomodoros</span></div>
</div>
</div>
<script>
(function () {
  var MODOS = {
    pomodoro: { min: 25, texto: 'Hora de focar!' },
    curta: { min: 5, texto: 'Respire e descanse um pouco.' },
    longa: { min: 15, texto: 'Hora de uma pausa longa.' }
  };
  var modo = 'pomodoro';
  var restante = MODOS.pomodoro.min * 60;
  var rodando = false;
  var fim = 0;
  var relogio = null;
  var periodo = 'semana';
  var ciclo = 0;
  var tarefas = [];
  function el(id) { return document.getElementById(id); }
  var tempo = el('pom-tempo');
  var foco = el('pom-foco');
  var btnIniciar = el('pom-iniciar');
  var lista = el('pom-lista');
  var campo = el('pom-nova');
  function ler(chave, padrao) {
    try {
      var bruto = window.localStorage.getItem(chave);
      if (bruto === null) { return padrao; }
      return JSON.parse(bruto);
    } catch (e) { return padrao; }
  }
  function gravar(chave, valor) {
    try { window.localStorage.setItem(chave, JSON.stringify(valor)); } catch (e) {}
  }
  function dois(n) { return n > 9 ? String(n) : '0' + n; }
  function chaveHoje() {
    var d = new Date();
    return d.getFullYear() + '-' + dois(d.getMonth() + 1) + '-' + dois(d.getDate());
  }
  function dec(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 1 }); }
  function tarefaAtiva() {
    for (var i = 0; tarefas.length !== i; i++) {
      if (!tarefas[i].feita) { return tarefas[i]; }
    }
    return null;
  }
  function mostrar() {
    var m = Math.floor(restante / 60);
    var s = restante % 60;
    var texto = dois(m) + ':' + dois(s);
    tempo.textContent = texto;
    document.title = (rodando ? texto + ' - ' : '') + 'Pomodoro Timer';
  }
  function mensagem() {
    var ativa = tarefaAtiva();
    if (modo === 'pomodoro') {
      foco.textContent = ativa ? 'Focando em: ' + ativa.texto : MODOS.pomodoro.texto;
    } else {
      foco.textContent = MODOS[modo].texto;
    }
  }
  function estilizarAbas() {
    ['pomodoro', 'curta', 'longa'].forEach(function (nome) {
      var b = el('pom-modo-' + nome);
      var ativo = nome === modo;
      b.style.background = ativo ? 'linear-gradient(135deg,#4f46e5,#6366f1)' : '#ffffff';
      b.style.color = ativo ? '#ffffff' : '#4f46e5';
      b.style.borderColor = ativo ? '#4f46e5' : '#c7d2fe';
    });
    ['semana', 'mes', 'ano'].forEach(function (nome) {
      var b = el('pom-per-' + nome);
      var ativo = nome === periodo;
      b.style.background = ativo ? 'linear-gradient(135deg,#4f46e5,#6366f1)' : '#ffffff';
      b.style.color = ativo ? '#ffffff' : '#4f46e5';
      b.style.borderColor = ativo ? '#4f46e5' : '#c7d2fe';
    });
  }
  function parar() {
    if (relogio !== null) { clearInterval(relogio); relogio = null; }
    rodando = false;
    btnIniciar.textContent = 'Iniciar';
  }
  function trocarModo(novo) {
    parar();
    modo = novo;
    restante = MODOS[modo].min * 60;
    estilizarAbas();
    mensagem();
    mostrar();
  }
  function apitar() {
    try {
      var Ctx = window.AudioContext || window.webkitAudioContext;
      if (!Ctx) { return; }
      var ctx = new Ctx();
      [0, 0.35, 0.7].forEach(function (atraso) {
        var osc = ctx.createOscillator();
        var ganho = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.value = 880;
        ganho.gain.value = 0.15;
        osc.connect(ganho);
        ganho.connect(ctx.destination);
        osc.start(ctx.currentTime + atraso);
        osc.stop(ctx.currentTime + atraso + 0.25);
      });
    } catch (e) {}
  }
  function registrar() {
    var hist = ler('pom-historico', {});
    var k = chaveHoje();
    hist[k] = (hist[k] || 0) + 1;
    gravar('pom-historico', hist);
    var ativa = tarefaAtiva();
    if (ativa) {
      ativa.pomos = (ativa.pomos || 0) + 1;
      gravar('pom-tarefas', tarefas);
      renderTarefas();
    }
    estatisticas();
  }
  function concluir() {
    parar();
    apitar();
    if (modo === 'pomodoro') {
      registrar();
      ciclo = ciclo + 1;
      trocarModo(ciclo % 4 === 0 ? 'longa' : 'curta');
    } else {
      trocarModo('pomodoro');
    }
  }
  function tick() {
    var r = Math.round((fim - Date.now()) / 1000);
    if (0 >= r) { restante = 0; mostrar(); concluir(); return; }
    restante = r;
    mostrar();
  }
  function iniciarOuPausar() {
    if (rodando) {
      parar();
      mostrar();
      return;
    }
    rodando = true;
    fim = Date.now() + restante * 1000;
    btnIniciar.textContent = 'Pausar';
    relogio = setInterval(tick, 250);
    mensagem();
    mostrar();
  }
  function desistir() {
    parar();
    restante = MODOS[modo].min * 60;
    mensagem();
    mostrar();
  }
  function renderTarefas() {
    lista.textContent = '';
    if (tarefas.length === 0) {
      var vazio = document.createElement('p');
      vazio.style.cssText = 'margin:0;font-size:0.9rem;color:#64748b;';
      vazio.textContent = 'Nenhuma tarefa ainda.';
      lista.appendChild(vazio);
    }
    tarefas.forEach(function (t, i) {
      var linha = document.createElement('div');
      linha.style.cssText = 'display:flex;align-items:center;gap:10px;padding:10px 12px;margin-bottom:8px;background:#ffffff;border:1px solid #c7d2fe;border-radius:10px;';
      var cb = document.createElement('input');
      cb.type = 'checkbox';
      cb.checked = !!t.feita;
      cb.setAttribute('aria-label', 'Concluir tarefa');
      cb.addEventListener('change', function () {
        t.feita = cb.checked;
        gravar('pom-tarefas', tarefas);
        renderTarefas();
        if (!rodando) { mensagem(); }
      });
      var txt = document.createElement('span');
      txt.style.cssText = 'flex:1;font-size:0.95rem;word-break:break-word;' + (t.feita ? 'text-decoration:line-through;color:#94a3b8;' : '');
      txt.textContent = t.texto + (t.pomos > 0 ? '  ·  ' + t.pomos + ' 🍅' : '');
      var rem = document.createElement('button');
      rem.type = 'button';
      rem.textContent = '✕';
      rem.setAttribute('aria-label', 'Remover tarefa');
      rem.style.cssText = 'padding:4px 10px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;';
      rem.addEventListener('click', function () {
        tarefas.splice(i, 1);
        gravar('pom-tarefas', tarefas);
        renderTarefas();
        if (!rodando) { mensagem(); }
      });
      linha.appendChild(cb);
      linha.appendChild(txt);
      linha.appendChild(rem);
      lista.appendChild(linha);
    });
  }
  function adicionar() {
    var texto = campo.value.trim();
    if (texto === '') { campo.focus(); return; }
    tarefas.push({ texto: texto, feita: false, pomos: 0 });
    gravar('pom-tarefas', tarefas);
    campo.value = '';
    renderTarefas();
    if (!rodando) { mensagem(); }
    campo.focus();
  }
  function estatisticas() {
    var hist = ler('pom-historico', {});
    var agora = new Date();
    var hoje = new Date(agora.getFullYear(), agora.getMonth(), agora.getDate());
    var total = 0;
    for (var k in hist) {
      var p = k.split('-');
      var d = new Date(Number(p[0]), Number(p[1]) - 1, Number(p[2]));
      var diff = Math.round((hoje - d) / 86400000);
      var ok = false;
      if (periodo === 'semana') { ok = diff >= 0 ? (7 > diff) : false; }
      if (periodo === 'mes') { ok = d.getFullYear() === hoje.getFullYear() ? d.getMonth() === hoje.getMonth() : false; }
      if (periodo === 'ano') { ok = d.getFullYear() === hoje.getFullYear(); }
      if (ok) { total = total + Number(hist[k]); }
    }
    var dias = 7;
    if (periodo === 'mes') { dias = hoje.getDate(); }
    if (periodo === 'ano') { dias = Math.round((hoje - new Date(hoje.getFullYear(), 0, 1)) / 86400000) + 1; }
    el('pom-total').textContent = total + (total === 1 ? ' pomodoro' : ' pomodoros') + ' (' + (total * MODOS.pomodoro.min) + ' min)';
    el('pom-media').textContent = dec(total / dias) + ' pomodoros';
  }
  btnIniciar.addEventListener('click', iniciarOuPausar);
  el('pom-desistir').addEventListener('click', desistir);
  el('pom-adicionar').addEventListener('click', adicionar);
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { adicionar(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  ['pomodoro', 'curta', 'longa'].forEach(function (nome) {
    el('pom-modo-' + nome).addEventListener('click', function () { trocarModo(nome); });
  });
  ['semana', 'mes', 'ano'].forEach(function (nome) {
    el('pom-per-' + nome).addEventListener('click', function () {
      periodo = nome;
      estilizarAbas();
      estatisticas();
    });
  });
  var salvas = ler('pom-tarefas', []);
  tarefas = Array.isArray(salvas) ? salvas : [];
  estilizarAbas();
  renderTarefas();
  mensagem();
  mostrar();
  estatisticas();
})();
</script>

## Como usar o Pomodoro Timer

1. Escolha o modo no topo: **Pomodoro** para focar, **Pausa Curta** ou **Pausa Longa** para descansar.
2. (Opcional) Digite o nome de uma tarefa no campo de tarefas e clique em **Adicionar Tarefa**. A primeira tarefa não concluída aparece como o foco atual.
3. Clique em **Iniciar** para começar a contagem regressiva. Use o mesmo botão (que vira **Pausar**) para interromper e retomar depois.
4. Trabalhe até o alarme tocar. Ao terminar um Pomodoro, o timer troca sozinho para uma pausa: curta a cada ciclo e longa a cada 4 Pomodoros.
5. Marque a caixinha da tarefa quando concluí-la. Use o botão ✕ para removê-la da lista.
6. Clique em **Desistir** para zerar o tempo do modo atual e recomeçar.
7. Acompanhe seu progresso em **Estatísticas**, alternando entre **Semana**, **Mês** e **Ano**.

Suas tarefas e estatísticas ficam salvas no próprio navegador, sem cadastro. Se você limpar os dados do navegador, elas serão apagadas.

## Entendendo os termos

- **Técnica Pomodoro:** método de gestão de tempo que alterna períodos de foco total com pausas curtas, para manter a concentração e evitar o cansaço.
- **Pomodoro:** um período de foco de 25 minutos, sem interrupções, dedicado a uma única tarefa.
- **Pausa Curta:** descanso de 5 minutos após cada Pomodoro, para levantar, beber água ou alongar.
- **Pausa Longa:** descanso de 15 minutos, feito depois de completar 4 Pomodoros seguidos.
- **Ciclo:** sequência de 4 Pomodoros intercalados com pausas curtas, encerrada por uma pausa longa.
- **Iniciar / Pausar:** botão que começa a contagem regressiva e também a interrompe temporariamente.
- **Desistir:** botão que cancela a contagem atual e volta o relógio ao tempo inicial do modo escolhido.
- **Tarefas:** lista das atividades que você pretende fazer. Cada Pomodoro concluído é somado à tarefa em foco.
- **Estatísticas:** resumo dos Pomodoros que você completou, filtrado por semana, mês ou ano.
- **Total:** quantidade de Pomodoros concluídos no período escolhido, com o tempo de foco equivalente em minutos.
- **Média por dia:** total de Pomodoros dividido pelo número de dias do período, mostrando seu ritmo diário de foco.