---
title: "Sorteio Online"
seoTitle: "Sorteio Online"
description: "Sorteio Online: sorteie nomes ou itens de uma lista. Grátis e online, sem cadastro."
summary: "Sorteie nomes ou itens de uma lista."
date: 2026-11-10
draft: false
category: "aleatorio"
tags: ["sorteio", "nomes", "listas", "gerador"]
keywords: ["sorteio online", "sorteio", "nomes", "listas"]
---

<div class="sorteio-tool" id="sorteio-tool">
<style>
.sorteio-tool{--st-bg:#ffffff;--st-border:#d9dee5;--st-text:#1f2933;--st-muted:#6b7785;--st-primary:#1a73e8;--st-primary-hover:#155fc0;--st-result-bg:#f1f6fe;--st-error:#c62828;max-width:640px;margin:0 0 24px;padding:20px;background:var(--st-bg);border:1px solid var(--st-border);border-radius:8px;color:var(--st-text);font-family:inherit;box-sizing:border-box}
@media (prefers-color-scheme:dark){.sorteio-tool{--st-bg:#1b2129;--st-border:#33404f;--st-text:#e6ebf1;--st-muted:#9aa7b5;--st-primary:#4d9bff;--st-primary-hover:#74b0ff;--st-result-bg:#222c38;--st-error:#ff8a80}}
.sorteio-tool *{box-sizing:border-box}
.sorteio-tool .st-title{margin:0 0 16px;font-size:1.15em;font-weight:700}
.sorteio-tool .st-group{margin-bottom:14px}
.sorteio-tool label{display:block;margin-bottom:6px;font-size:.9em;font-weight:600}
.sorteio-tool .st-opt{font-weight:400;color:var(--st-muted)}
.sorteio-tool input[type="text"],.sorteio-tool input[type="datetime-local"],.sorteio-tool textarea{width:100%;padding:10px 12px;border:1px solid var(--st-border);border-radius:6px;background:transparent;color:var(--st-text);font:inherit;font-size:1em}
.sorteio-tool textarea{min-height:160px;resize:vertical}
.sorteio-tool input:focus,.sorteio-tool textarea:focus{outline:2px solid var(--st-primary);outline-offset:0;border-color:var(--st-primary)}
.sorteio-tool .st-check{display:flex;align-items:center;gap:8px;margin:0;font-weight:600;cursor:pointer}
.sorteio-tool .st-check input{width:18px;height:18px;margin:0}
.sorteio-tool .st-schedule{margin-top:10px}
.sorteio-tool .st-hint{margin:6px 0 0;font-size:.85em;color:var(--st-muted)}
.sorteio-tool .st-btn{display:inline-block;padding:11px 28px;border:0;border-radius:6px;background:var(--st-primary);color:#ffffff;font:inherit;font-weight:700;cursor:pointer}
.sorteio-tool .st-btn:hover{background:var(--st-primary-hover)}
.sorteio-tool .st-error{margin:12px 0 0;color:var(--st-error);font-size:.9em;font-weight:600}
.sorteio-tool .st-status{margin:12px 0 0;color:var(--st-muted);font-size:.95em}
.sorteio-tool .st-result{margin-top:18px;padding:18px;background:var(--st-result-bg);border:1px solid var(--st-border);border-radius:8px;text-align:center}
.sorteio-tool .st-result-title{margin:0 0 6px;font-size:.95em;color:var(--st-muted)}
.sorteio-tool .st-result-label{margin:0;font-size:.8em;text-transform:uppercase;letter-spacing:.06em;color:var(--st-muted)}
.sorteio-tool .st-result-name{margin:6px 0 0;font-size:1.8em;font-weight:700;word-break:break-word}
.sorteio-tool [hidden]{display:none}
</style>
<div class="st-title">Sortear nome</div>
<form id="st-form" autocomplete="off">
<div class="st-group">
<label for="st-titulo">Título <span class="st-opt">(opcional)</span></label>
<input type="text" id="st-titulo" maxlength="120">
</div>
<div class="st-group">
<label for="st-lista">Participantes (um nome por linha)</label>
<textarea id="st-lista"></textarea>
</div>
<div class="st-group">
<label class="st-check" for="st-agendar"><input type="checkbox" id="st-agendar"> Agendar para uma data e hora</label>
<div class="st-schedule" id="st-schedule" hidden>
<input type="datetime-local" id="st-data" aria-label="Data e hora do sorteio">
<p class="st-hint">O nome só é sorteado nesse momento. Mantenha esta página aberta até a hora marcada.</p>
</div>
</div>
<button type="submit" class="st-btn" id="st-btn">Sortear</button>
<button type="button" class="st-btn" id="st-cancel" hidden>Cancelar agendamento</button>
</form>
<p class="st-error" id="st-error" role="alert" hidden></p>
<p class="st-status" id="st-status" hidden></p>
<div class="st-result" id="st-result" aria-live="polite" hidden>
<p class="st-result-title" id="st-result-title" hidden></p>
<p class="st-result-label">Sorteado</p>
<p class="st-result-name" id="st-result-name"></p>
</div>
<script>
(function () {
  var $ = function (id) { return document.getElementById(id); };
  var form = $("st-form");
  var agendar = $("st-agendar");
  var scheduleBox = $("st-schedule");
  var dataInput = $("st-data");
  var errorBox = $("st-error");
  var statusBox = $("st-status");
  var resultBox = $("st-result");
  var resultTitle = $("st-result-title");
  var resultName = $("st-result-name");
  var cancelBtn = $("st-cancel");
  var sortBtn = $("st-btn");
  var timer = null;
  function randomInt(max) {
    var cryptoObj = window.crypto || window.msCrypto;
    if (cryptoObj && cryptoObj.getRandomValues) {
      var buf = new Uint32Array(1);
      var limit = Math.floor(4294967296 / max) * max;
      do {
        cryptoObj.getRandomValues(buf);
      } while (buf[0] >= limit);
      return buf[0] % max;
    }
    return Math.floor(Math.random() * max);
  }
  function readNames() {
    return $("st-lista").value
      .split(/\r?\n/)
      .map(function (item) { return item.trim(); })
      .filter(function (item) { return item.length > 0; });
  }
  function showError(msg) {
    errorBox.textContent = msg;
    errorBox.hidden = false;
  }
  function clearError() {
    errorBox.textContent = "";
    errorBox.hidden = true;
  }
  function pad(n) {
    return (n > 9 ? "" : "0") + n;
  }
  function formatCountdown(ms) {
    var total = Math.ceil(ms / 1000);
    var h = Math.floor(total / 3600);
    var m = Math.floor((total % 3600) / 60);
    var s = total % 60;
    return pad(h) + ":" + pad(m) + ":" + pad(s);
  }
  function stopTimer() {
    if (timer !== null) {
      window.clearInterval(timer);
      timer = null;
    }
    statusBox.hidden = true;
    statusBox.textContent = "";
    cancelBtn.hidden = true;
    sortBtn.hidden = false;
  }
  function draw(names, titulo) {
    var winner = names[randomInt(names.length)];
    resultName.textContent = winner;
    if (titulo) {
      resultTitle.textContent = titulo;
      resultTitle.hidden = false;
    } else {
      resultTitle.textContent = "";
      resultTitle.hidden = true;
    }
    resultBox.hidden = false;
  }
  agendar.addEventListener("change", function () {
    scheduleBox.hidden = !agendar.checked;
    clearError();
  });
  cancelBtn.addEventListener("click", function () {
    stopTimer();
  });
  form.addEventListener("submit", function (event) {
    event.preventDefault();
    clearError();
    stopTimer();
    resultBox.hidden = true;
    var names = readNames();
    var titulo = $("st-titulo").value.trim();
    if (names.length === 0) {
      showError("Informe pelo menos um participante.");
      return;
    }
    if (!agendar.checked) {
      draw(names, titulo);
      return;
    }
    if (!dataInput.value) {
      showError("Escolha a data e a hora do sorteio.");
      return;
    }
    var target = new Date(dataInput.value).getTime();
    if (isNaN(target) || !(target - Date.now() > 0)) {
      showError("Escolha uma data e hora no futuro.");
      return;
    }
    sortBtn.hidden = true;
    cancelBtn.hidden = false;
    statusBox.hidden = false;
    var tick = function () {
      var remaining = target - Date.now();
      if (!(remaining > 0)) {
        stopTimer();
        draw(names, titulo);
        return;
      }
      statusBox.textContent = "Sorteio agendado. Tempo restante: " + formatCountdown(remaining);
    };
    tick();
    if (timer === null && !statusBox.hidden) {
      timer = window.setInterval(tick, 1000);
    }
  });
})();
</script>
</div>

## Como usar o sorteio online

1. **Título (opcional):** digite um nome para o sorteio, por exemplo "Sorteio de brindes". Ele aparece junto com o resultado.
2. **Participantes:** escreva um nome ou item por linha. Linhas em branco são ignoradas.
3. **Agendar (opcional):** se quiser que o sorteio aconteça mais tarde, marque a opção de agendamento e escolha a data e a hora.
4. **Sortear:** clique no botão e o resultado aparece logo abaixo. Para sortear de novo, clique outra vez.

Se você agendar, deixe a página aberta até o horário marcado. A contagem regressiva é exibida e você pode cancelar o agendamento a qualquer momento.

## Entenda cada termo

- **Sorteio:** escolha aleatória de um item de uma lista, em que todos têm a mesma chance.
- **Título:** nome opcional do sorteio, mostrado junto com o resultado para identificar de qual sorteio se trata.
- **Participantes:** lista de nomes ou itens que concorrem no sorteio, digitados um por linha.
- **Agendar:** define uma data e uma hora futuras para realizar o sorteio automaticamente.
- **Sortear:** botão que executa o sorteio e mostra o resultado.
- **Sorteado:** nome ou item escolhido ao acaso entre os participantes.
- **Contagem regressiva:** tempo que falta para o sorteio agendado acontecer.
- **Aleatório:** resultado que não pode ser previsto. Esta ferramenta usa o gerador aleatório do navegador.