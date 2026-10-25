---
title: "Contagem Regressiva"
seoTitle: "Contagem Regressiva: online e grátis"
description: "Contagem Regressiva: crie uma contagem regressiva para qualquer data. Grátis e online, sem cadastro."
summary: "Crie uma contagem regressiva para qualquer data."
date: 2026-10-25
draft: false
category: "datas"
tags: ["contagem regressiva", "tempo", "datas", "produtividade"]
keywords: ["contagem regressiva", "contagem regressiva online", "tempo", "datas"]
---

<!--sudah dikerjakan-->

Basta informar o nome do evento, escolher a data e o horário e depois clicar em **Começar**.

<div id="calc-contagem" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⏳ Contagem Regressiva</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a data do evento e acompanhe o tempo que falta.</p>
<label for="cr-nome" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Contagem regressiva para</label>
<input id="cr-nome" type="text" placeholder="Ex.: Meu aniversário" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="cr-data" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data e horário</label>
<input id="cr-data" type="datetime-local" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cr-comecar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Começar</button>
<button type="button" id="cr-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div style="margin-top:16px;font-size:0.9rem;color:#64748b;">
<span style="font-weight:600;">Exemplos:</span>
<button type="button" id="cr-ex-2027" style="margin:4px 4px 0 0;padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:999px;cursor:pointer;">2027</button>
<button type="button" id="cr-ex-2028" style="margin:4px 4px 0 0;padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:999px;cursor:pointer;">2028</button>
<button type="button" id="cr-ex-natal" style="margin:4px 4px 0 0;padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:999px;cursor:pointer;">Natal</button>
</div>
<div id="cr-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cr-resultado">preencha os campos e clique em "Começar".</span>
<div id="cr-placar" style="display:none;grid-template-columns:repeat(4,1fr);gap:8px;margin-top:14px;">
<div style="padding:10px 4px;text-align:center;background:#eef2ff;border-radius:10px;"><span id="cr-d" style="display:block;font-size:1.5rem;font-weight:700;color:#3730a3;">0</span><small style="color:#64748b;">dias</small></div>
<div style="padding:10px 4px;text-align:center;background:#eef2ff;border-radius:10px;"><span id="cr-h" style="display:block;font-size:1.5rem;font-weight:700;color:#3730a3;">0</span><small style="color:#64748b;">horas</small></div>
<div style="padding:10px 4px;text-align:center;background:#eef2ff;border-radius:10px;"><span id="cr-m" style="display:block;font-size:1.5rem;font-weight:700;color:#3730a3;">0</span><small style="color:#64748b;">minutos</small></div>
<div style="padding:10px 4px;text-align:center;background:#eef2ff;border-radius:10px;"><span id="cr-s" style="display:block;font-size:1.5rem;font-weight:700;color:#3730a3;">0</span><small style="color:#64748b;">segundos</small></div>
</div>
</div>
</div>
<script>
(function () {
  var nome = document.getElementById('cr-nome');
  var data = document.getElementById('cr-data');
  var caixa = document.getElementById('cr-resposta');
  var resultado = document.getElementById('cr-resultado');
  var placar = document.getElementById('cr-placar');
  var elD = document.getElementById('cr-d');
  var elH = document.getElementById('cr-h');
  var elM = document.getElementById('cr-m');
  var elS = document.getElementById('cr-s');
  var alvo = null;
  var timer = null;
  function pad(n) { return n > 9 ? String(n) : '0' + n; }
  function paraInput(dt) {
    return dt.getFullYear() + '-' + pad(dt.getMonth() + 1) + '-' + pad(dt.getDate()) + 'T' + pad(dt.getHours()) + ':' + pad(dt.getMinutes());
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function estado(tipo, texto) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    }
    resultado.textContent = texto;
  }
  function parar() {
    if (timer !== null) { clearInterval(timer); timer = null; }
  }
  function mostrar(d, h, m, s) {
    elD.textContent = fmt(d);
    elH.textContent = String(h);
    elM.textContent = String(m);
    elS.textContent = String(s);
  }
  function atualizar() {
    var diff = alvo.getTime() - Date.now();
    var titulo = nome.value.trim() === '' ? 'o evento' : nome.value.trim();
    if (diff > 0) {
      var total = Math.floor(diff / 1000);
      var d = Math.floor(total / 86400);
      var h = Math.floor((total % 86400) / 3600);
      var m = Math.floor((total % 3600) / 60);
      var s = total % 60;
      mostrar(d, h, m, s);
      estado('ok', 'faltam ' + fmt(d) + ' dias, ' + h + ' horas, ' + m + ' minutos e ' + s + ' segundos para ' + titulo + '.');
    } else {
      mostrar(0, 0, 0, 0);
      parar();
      estado('ok', 'o momento de ' + titulo + ' chegou! 🎉');
    }
  }
  function comecar() {
    if (data.value === '') { parar(); placar.style.display = 'none'; estado('erro', 'escolha a data e o horário do evento.'); return; }
    var dt = new Date(data.value);
    if (isNaN(dt.getTime())) { parar(); placar.style.display = 'none'; estado('erro', 'informe uma data e um horário válidos.'); return; }
    if (!(dt.getTime() > Date.now())) { parar(); placar.style.display = 'none'; estado('erro', 'escolha uma data e um horário no futuro.'); return; }
    alvo = dt;
    parar();
    placar.style.display = 'grid';
    atualizar();
    timer = setInterval(atualizar, 1000);
  }
  function limpar() {
    parar();
    alvo = null;
    nome.value = '';
    data.value = '';
    placar.style.display = 'none';
    estado('neutro', 'preencha os campos e clique em "Começar".');
    nome.focus();
  }
  function exemplo(rotulo, dt) {
    nome.value = rotulo;
    data.value = paraInput(dt);
    comecar();
  }
  function proximoNatal() {
    var agora = new Date();
    var natal = new Date(agora.getFullYear(), 11, 25, 0, 0, 0);
    if (!(natal.getTime() > agora.getTime())) { natal = new Date(agora.getFullYear() + 1, 11, 25, 0, 0, 0); }
    return natal;
  }
  document.getElementById('cr-comecar').addEventListener('click', comecar);
  document.getElementById('cr-limpar').addEventListener('click', limpar);
  document.getElementById('cr-ex-2027').addEventListener('click', function () { exemplo('2027', new Date(2027, 0, 1, 0, 0, 0)); });
  document.getElementById('cr-ex-2028').addEventListener('click', function () { exemplo('2028', new Date(2028, 0, 1, 0, 0, 0)); });
  document.getElementById('cr-ex-natal').addEventListener('click', function () { exemplo('o Natal', proximoNatal()); });
  [nome, data].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { comecar(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a contagem regressiva

1. Digite o nome do evento no campo **Contagem regressiva para** (por exemplo, "Meu aniversário"). Esse campo é opcional.
2. Escolha a **Data e horário** em que o evento vai acontecer.
3. Clique em **Começar** (ou pressione Enter) para iniciar a contagem.
4. Acompanhe os dias, horas, minutos e segundos restantes, que se atualizam a cada segundo.
5. Use os botões de **Exemplos** (2027, 2028 e Natal) para testar a ferramenta rapidamente.
6. Use o botão **Limpar** para parar a contagem e começar uma nova.

A data escolhida precisa estar no futuro e o cálculo usa o fuso horário do seu dispositivo. Mantenha a página aberta para ver a contagem andando. Quando o tempo chegar a zero, a ferramenta avisa que o momento do evento chegou.

## Entendendo os termos

- **Contagem regressiva:** contagem do tempo que falta para um evento, que diminui até chegar a zero.
- **Contagem regressiva para:** nome do evento que você está esperando, como aniversário, viagem, prova ou festa.
- **Data e horário:** momento exato em que a contagem termina, com dia, mês, ano, hora e minuto.
- **Começar:** botão que inicia a contagem regressiva com a data escolhida.
- **Limpar:** botão que para a contagem e apaga os campos preenchidos.
- **Exemplos:** atalhos que preenchem a data automaticamente para 2027, 2028 ou o próximo Natal.
- **Dias:** quantidade de períodos completos de 24 horas que faltam para o evento.
- **Horas:** horas restantes além dos dias completos, de 0 a 23.
- **Minutos:** minutos restantes além das horas completas, de 0 a 59.
- **Segundos:** segundos restantes além dos minutos completos, de 0 a 59.
- **Fuso horário:** região de referência para o horário. A ferramenta usa o do seu dispositivo.