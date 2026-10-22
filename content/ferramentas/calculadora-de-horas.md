---
title: "Calculadora de Horas"
seoTitle: "Calculadora de Horas"
description: "Calculadora de Horas: some e subtraia horas e minutos. Grátis e online, sem cadastro."
summary: "Some e subtraia horas e minutos."
date: 2026-10-22
draft: false
category: "datas"
tags: ["horas", "calculadora", "trabalho"]
keywords: ["calculadora de horas", "calculadora de horas online", "horas", "calculadora", "trabalho"]
---
<!--sudah dikerjakan-->

Basta digitar as horas e os minutos abaixo, escolher se cada valor será somado (+) ou subtraído (−) e depois clicar em **Calcular Horas**.

<div id="calc-horas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⏱️ Calculadora de Horas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Some e subtraia horas e minutos e veja o resultado na hora.</p>
<div style="display:flex;gap:8px;margin-bottom:6px;font-weight:600;font-size:0.95rem;">
<span style="width:64px;flex:none;">Operação</span>
<span style="flex:1;">Horas</span>
<span style="width:10px;flex:none;"></span>
<span style="flex:1;">Minutos</span>
</div>
<div style="display:flex;gap:8px;align-items:center;margin-bottom:10px;">
<select id="hrs-op-1" aria-label="Operação da linha 1" style="width:64px;flex:none;padding:12px 6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="+">+</option><option value="-">−</option></select>
<input id="hrs-h-1" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Horas da linha 1" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">:</span>
<input id="hrs-m-1" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Minutos da linha 1" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:8px;align-items:center;margin-bottom:10px;">
<select id="hrs-op-2" aria-label="Operação da linha 2" style="width:64px;flex:none;padding:12px 6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="+">+</option><option value="-">−</option></select>
<input id="hrs-h-2" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Horas da linha 2" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">:</span>
<input id="hrs-m-2" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Minutos da linha 2" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:8px;align-items:center;margin-bottom:10px;">
<select id="hrs-op-3" aria-label="Operação da linha 3" style="width:64px;flex:none;padding:12px 6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="+">+</option><option value="-">−</option></select>
<input id="hrs-h-3" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Horas da linha 3" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">:</span>
<input id="hrs-m-3" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Minutos da linha 3" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:8px;align-items:center;margin-bottom:10px;">
<select id="hrs-op-4" aria-label="Operação da linha 4" style="width:64px;flex:none;padding:12px 6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="+">+</option><option value="-">−</option></select>
<input id="hrs-h-4" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Horas da linha 4" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">:</span>
<input id="hrs-m-4" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Minutos da linha 4" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:8px;align-items:center;margin-bottom:10px;">
<select id="hrs-op-5" aria-label="Operação da linha 5" style="width:64px;flex:none;padding:12px 6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="+">+</option><option value="-">−</option></select>
<input id="hrs-h-5" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Horas da linha 5" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">:</span>
<input id="hrs-m-5" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Minutos da linha 5" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:8px;align-items:center;margin-bottom:20px;">
<select id="hrs-op-6" aria-label="Operação da linha 6" style="width:64px;flex:none;padding:12px 6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="+">+</option><option value="-">−</option></select>
<input id="hrs-h-6" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Horas da linha 6" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">:</span>
<input id="hrs-m-6" type="text" inputmode="numeric" placeholder="00" autocomplete="off" aria-label="Minutos da linha 6" style="flex:1;min-width:0;width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="hrs-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Horas</button>
<button type="button" id="hrs-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="hrs-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="hrs-resultado">preencha os campos e clique em "Calcular Horas".</span></div>
</div>
<script>
(function () {
  var TOTAL = 6;
  var resultado = document.getElementById('hrs-resultado');
  var caixa = document.getElementById('hrs-resposta');
  var linhas = [];
  for (var i = 1; i <= TOTAL; i++) {
    linhas.push({
      op: document.getElementById('hrs-op-' + i),
      h: document.getElementById('hrs-h-' + i),
      m: document.getElementById('hrs-m-' + i)
    });
  }
  function inteiro(v) {
    var t = String(v).trim();
    if (t === '') { return 0; }
    if (!/^\d+$/.test(t)) { return NaN; }
    return parseInt(t, 10);
  }
  function dois(n) { return (n < 10 ? '0' : '') + n; }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var total = 0;
    var usadas = 0;
    for (var i = 0; i < linhas.length; i++) {
      var l = linhas[i];
      var vazia = l.h.value.trim() === '' && l.m.value.trim() === '';
      if (vazia) { continue; }
      var h = inteiro(l.h.value);
      var m = inteiro(l.m.value);
      if (isNaN(h) || isNaN(m)) { erro('informe apenas números inteiros (sem sinais) nas horas e nos minutos da linha ' + (i + 1) + '.'); return; }
      var minutos = h * 60 + m;
      total += (l.op.value === '-' ? -1 : 1) * minutos;
      usadas++;
    }
    if (usadas === 0) { erro('informe pelo menos um valor de horas ou minutos.'); return; }
    var negativo = total < 0;
    var abs = Math.abs(total);
    var hh = Math.floor(abs / 60);
    var mm = abs % 60;
    var sinal = negativo ? '-' : '';
    var decimal = (abs / 60).toLocaleString('pt-BR', { maximumFractionDigits: 2 });
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'O resultado é <strong style="font-size:1.2rem;">' + sinal + dois(hh) + ':' + dois(mm) + '</strong> (' + sinal + hh + ' h e ' + mm + ' min)<br><small style="color:#475569;">Total: ' + sinal + abs.toLocaleString('pt-BR') + ' minutos = ' + sinal + decimal + ' horas decimais</small>';
  }
  function limpar() {
    linhas.forEach(function (l) {
      l.op.value = '+';
      l.h.value = '';
      l.m.value = '';
    });
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular Horas".';
    linhas[0].h.focus();
  }
  document.getElementById('hrs-calcular').addEventListener('click', calcular);
  document.getElementById('hrs-limpar').addEventListener('click', limpar);
  linhas.forEach(function (l) {
    [l.h, l.m].forEach(function (el) {
      el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    });
    [l.h, l.m, l.op].forEach(function (el) {
      el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
      el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
    });
  });
})();
</script>

## Como usar a calculadora

1. Digite as **Horas** e os **Minutos** do primeiro valor na primeira linha.
2. Escolha a **Operação** de cada linha: **+** para somar ou **−** para subtrair aquele valor.
3. Preencha as demais linhas que precisar. As linhas em branco são ignoradas.
4. Clique em **Calcular Horas** (ou pressione Enter) para ver o resultado.
5. Use o botão **Limpar** para apagar tudo e fazer um novo cálculo.

Use apenas números inteiros nos campos de horas e minutos. Os minutos podem passar de 59 (por exemplo, 90 minutos valem 1 hora e 30 minutos). O resultado aparece no formato **HH:MM** e também em minutos totais e em horas decimais. Se o resultado for negativo, ele é exibido com o sinal de menos.

## Entendendo os termos

- **Hora:** unidade de tempo equivalente a 60 minutos.
- **Minuto:** unidade de tempo equivalente a 60 segundos. Cada hora tem 60 minutos.
- **Operação:** define se o valor da linha será somado (+) ou subtraído (−) do total.
- **HH:MM:** formato de exibição do tempo, com as horas antes dos dois pontos e os minutos depois (por exemplo, 08:30).
- **Horas trabalhadas:** tempo total que uma pessoa dedicou ao trabalho em um dia ou período.
- **Horas extras:** tempo trabalhado além da jornada normal, obtido ao subtrair a jornada do total trabalhado.
- **Horas decimais:** forma de representar o tempo com casas decimais, em que 30 minutos equivalem a 0,5 hora. É útil para multiplicar por valor-hora.