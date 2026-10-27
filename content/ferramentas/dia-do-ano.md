---
title: "Dia do Ano"
seoTitle: "Dia do Ano"
description: "Dia do Ano: descubra qual é o dia do ano de hoje. Grátis e online, sem cadastro."
summary: "Descubra qual é o dia do ano de hoje."
date: 2026-10-27
draft: false
category: "datas"
tags: ["calendário", "datas"]
keywords: ["dia do ano", "dia do ano online", "calendário", "datas"]
---

<!--INI SUDAH DIKERJAKAN-->

Veja abaixo em qual dia do ano estamos hoje. O resultado é atualizado automaticamente, sem precisar digitar nada.

<div id="calc-dia-ano" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📅 Dia do Ano</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Descubra qual é o dia do ano de hoje.</p>
<div id="dda-resposta" aria-live="polite" style="padding:16px;background:#f0fdf4;border:2px dashed #86efac;border-radius:12px;color:#166534;font-size:1rem;line-height:1.6;text-align:center;">
<div style="font-size:0.9rem;font-weight:600;color:#3730a3;">Hoje é o</div>
<div style="font-size:2.4rem;font-weight:800;line-height:1.2;color:#166534;">Dia <span id="dda-numero">--</span></div>
<div id="dda-data" style="margin-top:4px;font-size:1rem;color:#475569;">carregando...</div>
</div>
<div style="margin-top:18px;">
<div style="height:10px;background:#ffffff;border:2px solid #c7d2fe;border-radius:999px;overflow:hidden;box-sizing:content-box;">
<div id="dda-barra" style="height:100%;width:0%;background:linear-gradient(135deg,#4f46e5,#6366f1);border-radius:999px;"></div>
</div>
<p id="dda-resumo" style="margin:10px 0 0;font-size:0.9rem;color:#64748b;text-align:center;"></p>
</div>
</div>
<script>
(function () {
  var numeroEl = document.getElementById('dda-numero');
  var dataEl = document.getElementById('dda-data');
  var barraEl = document.getElementById('dda-barra');
  var resumoEl = document.getElementById('dda-resumo');
  var semana = ['Domingo', 'Segunda-feira', 'Terça-feira', 'Quarta-feira', 'Quinta-feira', 'Sexta-feira', 'Sábado'];
  var meses = ['janeiro', 'fevereiro', 'março', 'abril', 'maio', 'junho', 'julho', 'agosto', 'setembro', 'outubro', 'novembro', 'dezembro'];
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function atualizar() {
    var hoje = new Date();
    var ano = hoje.getFullYear();
    var mes = hoje.getMonth();
    var dia = hoje.getDate();
    var numero = Math.round((Date.UTC(ano, mes, dia) - Date.UTC(ano, 0, 0)) / 86400000);
    var bissexto = new Date(ano, 1, 29).getMonth() === 1;
    var total = bissexto ? 366 : 365;
    var restantes = total - numero;
    var percentual = Math.round((numero / total) * 1000) / 10;
    numeroEl.textContent = fmt(numero);
    dataEl.textContent = semana[hoje.getDay()] + ', ' + dia + ' de ' + meses[mes] + ' de ' + ano;
    barraEl.style.width = percentual + '%';
    resumoEl.textContent = 'Dia ' + fmt(numero) + ' de ' + fmt(total) + ' (' + String(percentual).replace('.', ',') + '% do ano). Restam ' + fmt(restantes) + (restantes === 1 ? ' dia' : ' dias') + '.';
  }
  atualizar();
  setInterval(atualizar, 60000);
})();
</script>

## Como usar a ferramenta

1. Abra esta página: o **Dia do Ano** de hoje aparece automaticamente na caixa acima.
2. Veja o número do dia em destaque, junto com o dia da semana e a data completa.
3. Confira a barra de progresso e o resumo logo abaixo para saber quanto do ano já passou e quantos dias ainda restam.
4. Mantenha a página aberta se quiser: ela se atualiza sozinha quando a data muda.

A ferramenta usa a data e o fuso horário configurados no seu dispositivo, então não é necessário digitar nem informar nada.

## Entendendo os termos

- **Dia do ano:** número de ordem do dia dentro do ano, contando o dia 1º de janeiro como dia 1. Também é chamado de data ordinal.
- **Dia da semana:** nome do dia dentro da semana, de domingo a sábado.
- **Calendário gregoriano:** calendário usado na maior parte do mundo, que divide o ano em 12 meses.
- **Ano bissexto:** ano com 366 dias, porque fevereiro tem 29 dias. Ocorre, em geral, a cada 4 anos.
- **Ano comum:** ano com 365 dias, em que fevereiro tem 28 dias.
- **Dias restantes:** quantidade de dias que faltam para terminar o ano, sem contar o dia de hoje.
- **Progresso do ano:** porcentagem do ano que já passou, calculada dividindo o dia do ano pelo total de dias do ano.