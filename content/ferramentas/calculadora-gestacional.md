---
title: "Calculadora Gestacional"
seoTitle: "Calculadora Gestacional"
description: "Calculadora Gestacional: estime a data provável do parto e a idade gestacional. Grátis e online, sem cadastro."
summary: "Estime a data provável do parto e a idade gestacional."
date: 2026-10-23
draft: false
category: "saude"
tags: ["gravidez", "saúde", "datas"]
keywords: ["calculadora gestacional", "calculadora gestacional online", "gravidez", "saúde", "datas"]
---

Basta informar o primeiro dia da última menstruação abaixo e depois clicar em **Calcular**.

<div id="calc-gestacional" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🤰 Calculadora Gestacional</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe a data da última menstruação e veja o resultado na hora.</p>
<label for="gest-dia" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Primeiro dia da última menstruação</label>
<div style="display:flex;gap:10px;margin-bottom:20px;">
<select id="gest-dia" aria-label="Dia" style="flex:1;min-width:0;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="gest-mes" aria-label="Mês" style="flex:2;min-width:0;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="gest-ano" aria-label="Ano" style="flex:1.3;min-width:0;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="gest-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular</button>
<button type="button" id="gest-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="gest-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="gest-resultado">selecione a data e clique em "Calcular".</span></div>
</div>
<script>
(function () {
  var dia = document.getElementById('gest-dia');
  var mes = document.getElementById('gest-mes');
  var ano = document.getElementById('gest-ano');
  var resultado = document.getElementById('gest-resultado');
  var caixa = document.getElementById('gest-resposta');
  var MS_DIA = 86400000;
  var meses = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
  var PADRAO = 'selecione a data e clique em "Calcular".';
  function opcao(select, valor, texto) {
    var o = document.createElement('option');
    o.value = valor;
    o.textContent = texto;
    select.appendChild(o);
  }
  function preencher() {
    var i;
    var anoAtual = new Date().getFullYear();
    opcao(dia, '', 'Dia');
    for (i = 1; 31 >= i; i++) { opcao(dia, String(i), String(i)); }
    opcao(mes, '', 'Mês');
    for (i = 0; 12 > i; i++) { opcao(mes, String(i + 1), meses[i]); }
    opcao(ano, '', 'Ano');
    for (i = anoAtual - 1; anoAtual >= i; i++) { opcao(ano, String(i), String(i)); }
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function plural(n, singular, pluralTxt) { return n + ' ' + (n === 1 ? singular : pluralTxt); }
  function trecho(txt, tag, estilo) {
    var el = document.createElement(tag);
    if (estilo) { el.style.cssText = estilo; }
    el.textContent = txt;
    resultado.appendChild(el);
  }
  function quebra() { resultado.appendChild(document.createElement('br')); }
  function calcular() {
    if (!dia.value || !mes.value || !ano.value) { erro('selecione dia, mês e ano da última menstruação.'); return; }
    var d = parseInt(dia.value, 10);
    var m = parseInt(mes.value, 10);
    var y = parseInt(ano.value, 10);
    var dum = new Date(Date.UTC(y, m - 1, d));
    if (dum.getUTCFullYear() !== y || dum.getUTCMonth() !== m - 1 || dum.getUTCDate() !== d) { erro('essa data não existe. Confira o dia e o mês.'); return; }
    var hoje = new Date();
    var hojeUTC = Date.UTC(hoje.getFullYear(), hoje.getMonth(), hoje.getDate());
    var decorridos = Math.round((hojeUTC - dum.getTime()) / MS_DIA);
    if (0 > decorridos) { erro('a data da última menstruação não pode estar no futuro.'); return; }
    if (decorridos > 294) { erro('essa data é anterior a 42 semanas. Confira se informou a data correta.'); return; }
    var dpp = new Date(dum.getTime() + 280 * MS_DIA);
    var dppTxt = dpp.toLocaleDateString('pt-BR', { timeZone: 'UTC', weekday: 'long', day: '2-digit', month: 'long', year: 'numeric' });
    var semanas = Math.floor(decorridos / 7);
    var dias = decorridos % 7;
    var restantes = 280 - decorridos;
    var extra = restantes > 0 ? 'Faltam ' + plural(restantes, 'dia', 'dias') + ' para a data provável do parto.' : 'A data provável do parto já foi atingida.';
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    trecho('Data provável do parto: ', 'span');
    trecho(dppTxt, 'strong', 'font-size:1.2rem;');
    quebra();
    trecho('Você está com ', 'span');
    trecho(plural(semanas, 'semana', 'semanas') + (dias > 0 ? ' e ' + plural(dias, 'dia', 'dias') : ''), 'strong', 'font-size:1.2rem;');
    trecho(' de gravidez.', 'span');
    quebra();
    trecho(extra, 'small', 'color:#475569;');
  }
  function limpar() {
    dia.value = '';
    mes.value = '';
    ano.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = PADRAO;
    dia.focus();
  }
  preencher();
  document.getElementById('gest-calcular').addEventListener('click', calcular);
  document.getElementById('gest-limpar').addEventListener('click', limpar);
  [dia, mes, ano].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Selecione o **dia** do primeiro dia da sua última menstruação no primeiro campo.
2. Selecione o **mês** no segundo campo.
3. Selecione o **ano** no terceiro campo.
4. Clique em **Calcular** (ou pressione Enter) para ver a data provável do parto e as semanas de gravidez.
5. Use o botão **Limpar** para apagar a data e fazer um novo cálculo.

O resultado é uma estimativa. Apenas a data da última menstruação é considerada, e o cálculo parte do princípio de que o ciclo menstrual tem cerca de 28 dias. Para confirmar a idade gestacional e a data do parto, consulte o seu médico e faça o ultrassom.

## Entendendo os termos

- **Gestação:** período em que o bebê se desenvolve dentro do útero, com duração média de 40 semanas.
- **Última menstruação (DUM):** data do primeiro dia da última menstruação, usada como ponto de partida para contar a gravidez.
- **Data provável do parto (DPP):** data estimada para o nascimento do bebê, calculada em 280 dias (40 semanas) após a DUM. O parto pode ocorrer antes ou depois dela.
- **Idade gestacional:** tempo de gravidez contado desde o primeiro dia da última menstruação até hoje, em semanas e dias.
- **Semana de gravidez:** período de 7 dias usado para acompanhar a evolução da gestação.
- **Ciclo menstrual:** intervalo entre o primeiro dia de uma menstruação e o primeiro dia da seguinte, em média de 28 dias.

## Como é feito o cálculo

A data provável do parto é obtida somando 280 dias (40 semanas) à data da última menstruação, método conhecido como regra de Naegele:

**DPP = DUM + 280 dias**

A idade gestacional é o número de dias entre a DUM e a data de hoje, dividido em semanas completas e dias restantes.
