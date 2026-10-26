---
title: "Conversor de Timestamp"
seoTitle: "Conversor de Timestamp"
description: "Conversor de Timestamp: converta timestamp Unix em data e vice-versa. Grátis e online, sem cadastro."
summary: "Converta timestamp Unix em data e vice-versa."
date: 2026-10-26
draft: false
category: "dev"
tags: ["timestamp", "datas", "conversão", "desenvolvimento"]
keywords: ["conversor de timestamp", "conversor de timestamp online", "timestamp", "datas", "conversão"]
---

<!--sudah dikerjakan-->

Veja o timestamp atual, digite um timestamp Unix para descobrir a data ou escolha uma data para obter o timestamp e depois clique em **Converter**.

<div id="calc-timestamp" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🕒 Conversor de Timestamp</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Converta timestamp Unix em data e vice-versa na hora.</p>
<h3 style="margin:0 0 10px;font-size:1.05rem;color:#3730a3;">Timestamp Atual</h3>
<div id="ts-atual" style="margin-bottom:12px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#1e293b;font-size:1rem;line-height:1.6;">
<div><span style="color:#475569;">Segundos: </span><strong id="ts-atual-s" style="font-size:1.2rem;color:#3730a3;word-break:break-all;">-</strong></div>
<div><span style="color:#475569;">Milissegundos: </span><strong id="ts-atual-ms" style="word-break:break-all;">-</strong></div>
<div><span style="color:#475569;">Data local: </span><strong id="ts-atual-local">-</strong></div>
<div><span style="color:#475569;">Data UTC: </span><strong id="ts-atual-utc">-</strong></div>
</div>
<button type="button" id="ts-copiar" style="padding:11px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar timestamp atual</button>
<div style="height:1px;background:#c7d2fe;margin:22px 0;"></div>
<h3 style="margin:0 0 10px;font-size:1.05rem;color:#3730a3;">Timestamp para Data</h3>
<label for="ts-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Timestamp Unix (segundos)</label>
<input id="ts-entrada" type="text" inputmode="numeric" placeholder="Ex.: 1700000000" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ts-converter-data" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter</button>
<button type="button" id="ts-usar-atual" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Usar atual</button>
<button type="button" id="ts-limpar-data" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ts-resposta-data" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span>digite um timestamp e clique em "Converter".</span></div>
<div style="height:1px;background:#c7d2fe;margin:22px 0;"></div>
<h3 style="margin:0 0 10px;font-size:1.05rem;color:#3730a3;">Data para Timestamp</h3>
<label for="ts-data" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data</label>
<input id="ts-data" type="date" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ts-hora" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Hora (opcional)</label>
<input id="ts-hora" type="time" step="1" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ts-fuso" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Fuso horário</label>
<select id="ts-fuso" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="local">Horário local do navegador</option>
<option value="utc">UTC</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ts-converter-ts" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter</button>
<button type="button" id="ts-limpar-ts" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ts-resposta-ts" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span>escolha uma data e clique em "Converter".</span></div>
</div>
<script>
(function () {
  function $(id) { return document.getElementById(id); }
  function p2(n) { return String(n).padStart(2, '0'); }
  function maiorIgual(a, b) { return Math.max(a, b) === a; }
  var PLACEHOLDER_DATA = 'digite um timestamp e clique em "Converter".';
  var PLACEHOLDER_TS = 'escolha uma data e clique em "Converter".';
  var fusoNome = 'local';
  try { fusoNome = Intl.DateTimeFormat().resolvedOptions().timeZone || 'local'; } catch (e) { fusoNome = 'local'; }
  function fmtData(d, utc) {
    var ano = utc ? d.getUTCFullYear() : d.getFullYear();
    var mes = (utc ? d.getUTCMonth() : d.getMonth()) + 1;
    var dia = utc ? d.getUTCDate() : d.getDate();
    var h = utc ? d.getUTCHours() : d.getHours();
    var mi = utc ? d.getUTCMinutes() : d.getMinutes();
    var s = utc ? d.getUTCSeconds() : d.getSeconds();
    return p2(dia) + '/' + p2(mes) + '/' + String(ano).padStart(4, '0') + ' ' + p2(h) + ':' + p2(mi) + ':' + p2(s);
  }
  function offset(d) {
    var m = -d.getTimezoneOffset();
    var sinal = Math.sign(m) === -1 ? '-' : '+';
    var a = Math.abs(m);
    return 'UTC' + sinal + p2(Math.floor(a / 60)) + ':' + p2(a % 60);
  }
  function relativo(ms) {
    var diff = Math.round((Date.now() - ms) / 1000);
    var futuro = Math.sign(diff) === -1;
    var abs = Math.abs(diff);
    if (abs === 0) { return 'agora'; }
    var unidades = [['ano', 'anos', 31536000], ['mês', 'meses', 2592000], ['dia', 'dias', 86400], ['hora', 'horas', 3600], ['minuto', 'minutos', 60], ['segundo', 'segundos', 1]];
    for (var i = 0; i !== unidades.length; i++) {
      var n = Math.floor(abs / unidades[i][2]);
      if (n !== 0) {
        var nome = n === 1 ? unidades[i][0] : unidades[i][1];
        return (futuro ? 'em ' : 'há ') + n + ' ' + nome;
      }
    }
    return 'agora';
  }
  function limparCaixa(box) { while (box.firstChild) { box.removeChild(box.firstChild); } }
  function cabecalho(box) {
    limparCaixa(box);
    var s = document.createElement('strong');
    s.style.color = '#3730a3';
    s.textContent = 'Resposta:';
    box.appendChild(s);
    box.appendChild(document.createTextNode(' '));
  }
  function estilo(box, borda, fundo, cor) {
    box.style.borderColor = borda;
    box.style.background = fundo;
    box.style.color = cor;
  }
  function neutro(box, texto) {
    cabecalho(box);
    estilo(box, '#c7d2fe', '#ffffff', '#64748b');
    var sp = document.createElement('span');
    sp.textContent = texto;
    box.appendChild(sp);
  }
  function erro(box, msg) {
    cabecalho(box);
    estilo(box, '#fca5a5', '#fef2f2', '#b91c1c');
    var sp = document.createElement('span');
    sp.textContent = msg;
    box.appendChild(sp);
  }
  function sucesso(box, itens) {
    cabecalho(box);
    estilo(box, '#86efac', '#f0fdf4', '#166534');
    itens.forEach(function (it) {
      var linha = document.createElement('div');
      linha.style.marginTop = '6px';
      var r = document.createElement('span');
      r.style.color = '#475569';
      r.textContent = it[0] + ': ';
      var v = document.createElement('strong');
      v.style.wordBreak = 'break-all';
      if (it[2]) { v.style.fontSize = '1.2rem'; }
      v.textContent = it[1];
      linha.appendChild(r);
      linha.appendChild(v);
      box.appendChild(linha);
    });
  }
  function atualizar() {
    var agora = new Date();
    $('ts-atual-s').textContent = String(Math.floor(agora.getTime() / 1000));
    $('ts-atual-ms').textContent = String(agora.getTime());
    $('ts-atual-local').textContent = fmtData(agora, false);
    $('ts-atual-utc').textContent = fmtData(agora, true);
  }
  function copiar(texto, botao) {
    var original = botao.textContent;
    function feito() {
      botao.textContent = 'Copiado!';
      setTimeout(function () { botao.textContent = original; }, 1500);
    }
    try {
      if (navigator.clipboard) {
        navigator.clipboard.writeText(texto).then(feito, function () {});
        return;
      }
    } catch (e) {}
    var ta = document.createElement('textarea');
    ta.value = texto;
    document.body.appendChild(ta);
    ta.select();
    try { document.execCommand('copy'); feito(); } catch (e2) {}
    document.body.removeChild(ta);
  }
  function converterParaData() {
    var box = $('ts-resposta-data');
    var bruto = $('ts-entrada').value.trim().replace(/[\s.,]/g, '');
    if (!/^-?\d+$/.test(bruto)) { erro(box, 'informe um timestamp válido (apenas números).'); return; }
    var n = Number(bruto);
    var emMs = maiorIgual(Math.abs(n), 1e11);
    var ms = emMs ? n : n * 1000;
    var d = new Date(ms);
    if (isNaN(d.getTime())) { erro(box, 'esse timestamp está fora do intervalo de datas suportado.'); return; }
    sucesso(box, [
      ['Data local (' + fusoNome + ', ' + offset(d) + ')', fmtData(d, false), true],
      ['Data UTC', fmtData(d, true)],
      ['ISO 8601', d.toISOString()],
      ['Relativo', relativo(ms)],
      ['Unidade detectada', emMs ? 'milissegundos' : 'segundos']
    ]);
  }
  function converterParaTimestamp() {
    var box = $('ts-resposta-ts');
    var dv = $('ts-data').value;
    if (!dv) { erro(box, 'escolha uma data.'); return; }
    var tv = $('ts-hora').value || '00:00:00';
    var dp = dv.split('-').map(Number);
    var hp = tv.split(':').map(Number);
    var h = hp[0] || 0;
    var mi = hp[1] || 0;
    var s = hp[2] || 0;
    var utc = $('ts-fuso').value === 'utc';
    var ms = utc ? Date.UTC(dp[0], dp[1] - 1, dp[2], h, mi, s) : new Date(dp[0], dp[1] - 1, dp[2], h, mi, s).getTime();
    if (isNaN(ms)) { erro(box, 'data ou hora inválida.'); return; }
    var d = new Date(ms);
    sucesso(box, [
      ['Timestamp (segundos)', String(Math.floor(ms / 1000)), true],
      ['Timestamp (milissegundos)', String(ms)],
      ['ISO 8601', d.toISOString()]
    ]);
  }
  function limparData() {
    $('ts-entrada').value = '';
    neutro($('ts-resposta-data'), PLACEHOLDER_DATA);
    $('ts-entrada').focus();
  }
  function limparTs() {
    $('ts-data').value = '';
    $('ts-hora').value = '';
    $('ts-fuso').value = 'local';
    neutro($('ts-resposta-ts'), PLACEHOLDER_TS);
    $('ts-data').focus();
  }
  function usarAtual() {
    $('ts-entrada').value = String(Math.floor(Date.now() / 1000));
    converterParaData();
  }
  $('ts-copiar').addEventListener('click', function () { copiar($('ts-atual-s').textContent, $('ts-copiar')); });
  $('ts-converter-data').addEventListener('click', converterParaData);
  $('ts-converter-ts').addEventListener('click', converterParaTimestamp);
  $('ts-usar-atual').addEventListener('click', usarAtual);
  $('ts-limpar-data').addEventListener('click', limparData);
  $('ts-limpar-ts').addEventListener('click', limparTs);
  $('ts-entrada').addEventListener('keydown', function (e) { if (e.key === 'Enter') { converterParaData(); } });
  [$('ts-data'), $('ts-hora')].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { converterParaTimestamp(); } });
  });
  [$('ts-entrada'), $('ts-data'), $('ts-hora'), $('ts-fuso')].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  atualizar();
  setInterval(atualizar, 1000);
})();
</script>

## Como usar o conversor

1. Veja o **Timestamp Atual** no topo da ferramenta. Ele é atualizado a cada segundo e pode ser copiado com o botão **Copiar timestamp atual**.
2. Para descobrir a data de um timestamp, digite o número no campo **Timestamp Unix (segundos)** e clique em **Converter**. O botão **Usar atual** preenche o campo com o timestamp de agora.
3. Para descobrir o timestamp de uma data, escolha a **Data**, informe a **Hora** (opcional) e selecione o **Fuso horário**. Depois clique em **Converter**.
4. Use o botão **Limpar** de cada seção para apagar os campos e fazer uma nova conversão.

Se você digitar um timestamp com 11 dígitos ou mais, o conversor entende que o valor está em milissegundos e avisa isso no resultado. Se a hora ficar em branco, será usado 00:00:00.

## Entendendo os termos

- **Timestamp Unix:** número de segundos passados desde 1º de janeiro de 1970, às 00:00:00 UTC.
- **Epoch time:** outro nome do timestamp Unix. A "época" (epoch) é a data de origem da contagem, 01/01/1970.
- **UTC:** horário universal coordenado, usado como referência para todos os fusos horários e sem horário de verão.
- **Fuso horário:** diferença de horas de uma região em relação ao UTC, como UTC-03:00 em Brasília.
- **Horário local:** data e hora no fuso horário configurado no seu navegador ou dispositivo.
- **Segundos:** unidade padrão do timestamp Unix, com 10 dígitos para datas atuais.
- **Milissegundos:** milésimos de segundo. Muitas linguagens, como JavaScript, usam timestamps com 13 dígitos nessa unidade.
- **ISO 8601:** formato padrão internacional de data e hora, como `2023-11-14T22:13:20.000Z`. A letra Z indica UTC.
- **Tempo relativo:** distância entre a data convertida e o momento atual, como "há 2 dias" ou "em 3 horas".

## O que é Timestamp Unix?

O timestamp Unix é uma forma simples e universal de representar data e hora com um único número. Ele é muito usado em programação, por exemplo:

- Armazenamento de datas em bancos de dados.
- APIs e sistemas de sincronização.
- Logs e registros de eventos.
- Cálculos de diferença entre datas.

## Exemplo resolvido

Qual é a data do timestamp **1700000000**?

1. Digite `1700000000` no campo **Timestamp Unix (segundos)**.
2. Clique em **Converter**.
3. O resultado em UTC é **14/11/2023 22:13:20**.

**Resposta:** o timestamp 1700000000 corresponde a 14 de novembro de 2023, às 22:13:20 (UTC).