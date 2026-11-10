---
title: "Subtrair Dias em Datas"
seoTitle: "Subtrair Dias em Datas"
description: "Subtrair Dias em Datas: descubra a data resultante ao subtrair dias de uma data. Grátis e online, sem cadastro."
summary: "Descubra a data resultante ao subtrair dias de uma data."
date: 2026-11-10
draft: false
category: "datas"
tags: ["datas", "calendário", "calculadora"]
keywords: ["subtrair dias em datas", "subtrair dias em datas online", "datas", "calendário", "calculadora"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher a data, digitar quantos dias deseja subtrair e depois clicar em **Subtrair Dias**.

<div id="calc-subtrair-dias" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📅 Subtrair Dias em Datas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a data, informe os dias e veja o resultado na hora.</p>
<label for="sub-data" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data base para subtração</label>
<input id="sub-data" type="date" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;font-family:inherit;">
<label for="sub-dias" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantos dias subtrair?</label>
<input id="sub-dias" type="text" inputmode="numeric" placeholder="Ex.: 30" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sub-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Subtrair Dias</button>
<button type="button" id="sub-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="sub-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sub-resultado">escolha a data, digite os dias e clique em "Subtrair Dias".</span></div>
</div>
<script>
(function () {
  var campoData = document.getElementById('sub-data');
  var campoDias = document.getElementById('sub-dias');
  var resultado = document.getElementById('sub-resultado');
  var caixa = document.getElementById('sub-resposta');
  var semana = ['domingo', 'segunda-feira', 'terça-feira', 'quarta-feira', 'quinta-feira', 'sexta-feira', 'sábado'];
  var MAX_DIAS = 3000000;
  var MSG_PADRAO = 'escolha a data, digite os dias e clique em "Subtrair Dias".';
  function dois(n) { return ('0' + n).slice(-2); }
  function quatro(n) { return ('000' + n).slice(-4); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function sucesso(dataTexto, diaSemana, detalhe) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var destaque = document.createElement('strong');
    destaque.style.fontSize = '1.2rem';
    destaque.textContent = dataTexto;
    resultado.appendChild(destaque);
    resultado.appendChild(document.createTextNode(' (' + diaSemana + ')'));
    resultado.appendChild(document.createElement('br'));
    var nota = document.createElement('small');
    nota.style.color = '#475569';
    nota.textContent = detalhe;
    resultado.appendChild(nota);
  }
  function calcular() {
    var valorData = campoData.value;
    if (!valorData) { erro('selecione uma data válida.'); return; }
    var partes = valorData.split('-');
    var ano = parseInt(partes[0], 10);
    var mes = parseInt(partes[1], 10);
    var dia = parseInt(partes[2], 10);
    if (isNaN(ano) || isNaN(mes) || isNaN(dia)) { erro('selecione uma data válida.'); return; }
    var textoDias = campoDias.value.trim().replace(/\s/g, '');
    if (textoDias === '' || !/^[0-9]+$/.test(textoDias)) { erro('informe um número inteiro de dias, igual ou maior que zero.'); return; }
    var dias = parseInt(textoDias, 10);
    if (dias > MAX_DIAS) { erro('informe uma quantidade de dias menor ou igual a ' + MAX_DIAS.toLocaleString('pt-BR') + '.'); return; }
    var data = new Date(0);
    data.setUTCFullYear(ano, mes - 1, dia - dias);
    if (isNaN(data.getTime()) || data.getUTCFullYear() > 0 === false) { erro('o resultado ficou fora do intervalo de datas suportado (anterior ao ano 1).'); return; }
    var texto = dois(data.getUTCDate()) + '/' + dois(data.getUTCMonth() + 1) + '/' + quatro(data.getUTCFullYear());
    var origem = dois(dia) + '/' + dois(mes) + '/' + quatro(ano);
    var rotulo = dias === 1 ? 'dia' : 'dias';
    sucesso(texto, semana[data.getUTCDay()], origem + ' − ' + dias.toLocaleString('pt-BR') + ' ' + rotulo + ' = ' + texto);
  }
  function limpar() {
    campoData.value = '';
    campoDias.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = MSG_PADRAO;
    campoData.focus();
  }
  document.getElementById('sub-calcular').addEventListener('click', calcular);
  document.getElementById('sub-limpar').addEventListener('click', limpar);
  [campoData, campoDias].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Escolha a **Data base para subtração**: clique no campo e use o calendário, ou digite a data diretamente.
2. Digite no segundo campo **Quantos dias subtrair?** (apenas números inteiros, como `30` ou `365`).
3. Clique em **Subtrair Dias** (ou pressione Enter) para ver a data resultante e o dia da semana.
4. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

O cálculo considera o calendário real, incluindo meses com 28, 29, 30 ou 31 dias e anos bissextos. Se a subtração atravessar a virada de mês ou de ano, a data resultante é ajustada automaticamente.

## Entendendo os termos

- **Data base:** data de partida, a partir da qual os dias serão subtraídos.
- **Dias a subtrair:** quantidade de dias que você quer voltar no calendário a partir da data base.
- **Data resultante:** data obtida depois de voltar a quantidade de dias informada.
- **Dia da semana:** nome do dia (segunda-feira, terça-feira etc.) correspondente à data resultante.
- **Ano bissexto:** ano com 366 dias, em que fevereiro tem 29 dias. Ocorre a cada 4 anos, exceto anos de século que não sejam divisíveis por 400.
- **Calendário gregoriano:** sistema de calendário usado no Brasil e na maior parte do mundo, base para o cálculo das datas.

## Como subtrair dias de uma data

Subtrair dias é voltar no tempo a partir de uma data de referência:

**data resultante = data base − quantidade de dias**

O calendário não tem um número fixo de dias por mês, então a conta precisa respeitar o tamanho de cada mês e os anos bissextos. Por isso a calculadora faz esse ajuste por você.

## Exemplo resolvido

Qual é a data 30 dias antes de 10/11/2026?

1. Data base: 10/11/2026.
2. Dias a subtrair: 30.
3. Voltando 10 dias, chega-se a 31/10/2026. Faltam 20 dias para subtrair.
4. Voltando mais 20 dias a partir de 31/10/2026, chega-se a 11/10/2026.

**Resposta:** 30 dias antes de 10/11/2026 é **11/10/2026** (domingo).