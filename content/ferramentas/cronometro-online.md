---
title: "Cronômetro"
seoTitle: "Cronômetro: online e grátis"
description: "Cronômetro: cronômetro com voltas, direto no navegador. Grátis e online, sem cadastro."
summary: "Cronômetro com voltas, direto no navegador."
date: 2026-10-26
draft: false
category: "util"
tags: ["cronômetro", "tempo", "produtividade"]
keywords: ["cronômetro", "cronômetro online", "tempo", "produtividade"]
---

<!--sudah dikerjakan-->

Basta clicar em **Iniciar** para começar a contar o tempo e em **Volta** para marcar cada parcial.

<div id="calc-cronometro" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⏱️ Cronômetro Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Marque o tempo e registre as voltas na hora.</p>
<div aria-live="off" style="margin-bottom:20px;padding:20px 16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;text-align:center;"><span id="cron-visor" style="display:block;font-size:2.4rem;font-weight:700;color:#3730a3;font-variant-numeric:tabular-nums;letter-spacing:1px;line-height:1.2;">00:00:000</span></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cron-iniciar" style="flex:1;min-width:120px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Iniciar</button>
<button type="button" id="cron-volta" disabled style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:not-allowed;opacity:0.5;">Volta</button>
<button type="button" id="cron-zerar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Zerar</button>
</div>
<div id="cron-voltas-box" style="display:none;margin-top:20px;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;overflow:hidden;">
<div style="display:flex;justify-content:space-between;gap:8px;padding:10px 14px;background:#eef2ff;font-size:0.8rem;font-weight:700;color:#3730a3;"><span style="flex:1;">Volta</span><span style="flex:1;text-align:center;">Parcial</span><span style="flex:1;text-align:right;">Total</span></div>
<div id="cron-voltas" style="max-height:240px;overflow-y:auto;"></div>
</div>
</div>
<script>
(function () {
  var visor = document.getElementById('cron-visor');
  var btnIniciar = document.getElementById('cron-iniciar');
  var btnVolta = document.getElementById('cron-volta');
  var btnZerar = document.getElementById('cron-zerar');
  var caixaVoltas = document.getElementById('cron-voltas-box');
  var lista = document.getElementById('cron-voltas');
  var estado = { rodando: false, inicio: 0, base: 0, ultimaVolta: 0, voltas: [], raf: 0 };
  function pad(n, t) { return ('000' + n).slice(-t); }
  function fmt(ms) {
    var total = Math.floor(ms);
    var h = Math.floor(total / 3600000);
    var m = Math.floor(total / 60000) % 60;
    var s = Math.floor(total / 1000) % 60;
    var r = total % 1000;
    var prefixo = h !== 0 ? pad(h, 2) + ':' : '';
    return prefixo + pad(m, 2) + ':' + pad(s, 2) + ':' + pad(r, 3);
  }
  function atual() {
    return estado.rodando ? estado.base + (performance.now() - estado.inicio) : estado.base;
  }
  function habilitarVolta(ativo) {
    btnVolta.disabled = !ativo;
    btnVolta.style.opacity = ativo ? '1' : '0.5';
    btnVolta.style.cursor = ativo ? 'pointer' : 'not-allowed';
  }
  function tick() {
    visor.textContent = fmt(atual());
    estado.raf = requestAnimationFrame(tick);
  }
  function iniciar() {
    estado.inicio = performance.now();
    estado.rodando = true;
    btnIniciar.textContent = 'Pausar';
    habilitarVolta(true);
    tick();
  }
  function pausar() {
    cancelAnimationFrame(estado.raf);
    estado.base = atual();
    estado.rodando = false;
    visor.textContent = fmt(estado.base);
    btnIniciar.textContent = 'Continuar';
    habilitarVolta(false);
  }
  function alternar() {
    if (estado.rodando) { pausar(); } else { iniciar(); }
  }
  function criarCelula(texto, alinhamento, cor, peso) {
    var el = document.createElement('span');
    el.style.cssText = 'flex:1;text-align:' + alinhamento + ';color:' + cor + ';font-weight:' + peso + ';font-variant-numeric:tabular-nums;';
    el.textContent = texto;
    return el;
  }
  function desenhar() {
    lista.textContent = '';
    if (estado.voltas.length === 0) { caixaVoltas.style.display = 'none'; return; }
    caixaVoltas.style.display = 'block';
    var tempos = estado.voltas.map(function (v) { return v.parcial; });
    var menor = Math.min.apply(null, tempos);
    var maior = Math.max.apply(null, tempos);
    var varias = estado.voltas.length !== 1;
    estado.voltas.forEach(function (v, i) {
      var cor = '#1e293b';
      if (varias && v.parcial === menor) { cor = '#166534'; }
      if (varias && v.parcial === maior) { cor = '#b91c1c'; }
      var linha = document.createElement('div');
      linha.style.cssText = 'display:flex;justify-content:space-between;gap:8px;padding:9px 14px;font-size:0.95rem;border-top:1px solid #e0e7ff;';
      linha.appendChild(criarCelula('Volta ' + (i + 1), 'left', '#64748b', '600'));
      linha.appendChild(criarCelula(fmt(v.parcial), 'center', cor, '700'));
      linha.appendChild(criarCelula(fmt(v.total), 'right', '#475569', '400'));
      lista.insertBefore(linha, lista.firstChild);
    });
  }
  function marcarVolta() {
    if (!estado.rodando) { return; }
    var t = atual();
    estado.voltas.push({ parcial: t - estado.ultimaVolta, total: t });
    estado.ultimaVolta = t;
    desenhar();
  }
  function zerar() {
    cancelAnimationFrame(estado.raf);
    estado.rodando = false;
    estado.base = 0;
    estado.inicio = 0;
    estado.ultimaVolta = 0;
    estado.voltas = [];
    visor.textContent = fmt(0);
    btnIniciar.textContent = 'Iniciar';
    habilitarVolta(false);
    desenhar();
  }
  btnIniciar.addEventListener('click', alternar);
  btnVolta.addEventListener('click', marcarVolta);
  btnZerar.addEventListener('click', zerar);
})();
</script>

## Como usar o cronômetro

1. Clique em **Iniciar** para começar a contar o tempo.
2. Clique em **Volta** a qualquer momento para registrar um tempo parcial sem parar a contagem.
3. Clique em **Pausar** para interromper e em **Continuar** para retomar de onde parou.
4. Clique em **Zerar** para apagar o tempo e todas as voltas e começar de novo.

O tempo aparece no formato **minutos:segundos:milésimos** (por exemplo, `01:25:340`). Quando passa de 1 hora, as horas são exibidas na frente (`01:05:25:340`). Na lista de voltas, a mais rápida aparece em verde e a mais lenta em vermelho.

## Entendendo os termos

- **Cronômetro:** instrumento que mede o tempo decorrido a partir do momento em que é iniciado, contando para a frente.
- **Iniciar:** botão que começa a contagem do tempo a partir de zero.
- **Pausar:** botão que interrompe a contagem e mantém o tempo atual na tela.
- **Continuar:** botão que retoma a contagem do ponto em que ela foi pausada.
- **Zerar:** botão que volta o cronômetro para 00:00:000 e apaga as voltas registradas.
- **Volta (lap):** marcação feita durante a contagem, usada para registrar uma etapa sem parar o cronômetro, como cada volta de uma pista.
- **Parcial:** tempo gasto em uma volta específica, contado desde a volta anterior.
- **Total:** tempo acumulado desde o início da contagem até o momento em que a volta foi marcada.
- **Milésimo de segundo:** a milésima parte de um segundo (1 s = 1.000 ms), exibida nos três últimos dígitos do cronômetro.