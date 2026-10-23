---
title: "Calcular Idade"
seoTitle: "Calcular Idade: online e grátis"
description: "Calcular Idade: descubra sua idade exata em anos, meses e dias. Grátis e online, sem cadastro."
summary: "Descubra sua idade exata em anos, meses e dias."
date: 2026-10-23
draft: false
category: "datas"
tags: ["idade", "datas", "calculadora", "aniversário"]
keywords: ["calcular idade", "calcular idade online", "idade", "datas", "calculadora"]
---

<!--sudah dikerjakan-->

Basta escolher a sua data de nascimento abaixo e depois clicar em **Calcular Idade**.

<div id="calc-idade" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎂 Calculadora de Idade</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe sua data de nascimento e veja a idade exata na hora.</p>
<label for="idade-dia" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data de Nascimento</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<select id="idade-dia" aria-label="Dia" style="flex:1;min-width:80px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="idade-mes" aria-label="Mês" style="flex:2;min-width:130px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<input id="idade-ano" type="text" inputmode="numeric" maxlength="4" placeholder="Ano" aria-label="Ano" autocomplete="off" style="flex:1;min-width:90px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="idade-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Idade</button>
<button type="button" id="idade-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="idade-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Sua Idade:</strong> <span id="idade-resultado">escolha a data e clique em "Calcular Idade".</span></div>
</div>
<script>
(function () {
  var dia = document.getElementById('idade-dia');
  var mes = document.getElementById('idade-mes');
  var ano = document.getElementById('idade-ano');
  var resultado = document.getElementById('idade-resultado');
  var caixa = document.getElementById('idade-resposta');
  var nomesMes = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
  var textoInicial = 'escolha a data e clique em "Calcular Idade".';
  function opcao(sel, valor, texto) {
    var o = document.createElement('option');
    o.value = valor;
    o.textContent = texto;
    sel.appendChild(o);
  }
  function preencher() {
    var i;
    opcao(dia, '', 'Dia');
    for (i = 1; 32 > i; i++) { opcao(dia, String(i), i > 9 ? String(i) : '0' + i); }
    opcao(mes, '', 'Mês');
    for (i = 0; nomesMes.length > i; i++) { opcao(mes, String(i + 1), nomesMes[i]); }
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function plural(n, singular, plur) { return fmt(n) + ' ' + (n === 1 ? singular : plur); }
  function esvaziar() { while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); } }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    esvaziar();
    resultado.appendChild(document.createTextNode(msg));
  }
  function calcular() {
    var d = parseInt(dia.value, 10);
    var m = parseInt(mes.value, 10);
    var textoAno = ano.value.trim();
    if (isNaN(d) || isNaN(m) || !/^\d{4}$/.test(textoAno)) { erro('informe o dia, o mês e um ano com 4 dígitos.'); return; }
    var a = parseInt(textoAno, 10);
    if (1900 > a) { erro('informe um ano a partir de 1900.'); return; }
    var nasc = new Date(a, m - 1, d);
    if (nasc.getFullYear() !== a || nasc.getMonth() !== m - 1 || nasc.getDate() !== d) { erro('essa data não existe no calendário.'); return; }
    var agora = new Date();
    var ta = agora.getFullYear();
    var tm = agora.getMonth();
    var td = agora.getDate();
    if (nasc.getTime() > new Date(ta, tm, td).getTime()) { erro('a data de nascimento não pode estar no futuro.'); return; }
    var anos = ta - a;
    var meses = tm - (m - 1);
    var dias = td - d;
    if (0 > dias) {
      dias += new Date(ta, tm, 0).getDate();
      meses -= 1;
    }
    if (0 > meses) {
      meses += 12;
      anos -= 1;
    }
    var hojeUTC = Date.UTC(ta, tm, td);
    var totalDias = Math.round((hojeUTC - Date.UTC(a, m - 1, d)) / 86400000);
    var proximo = Date.UTC(ta, m - 1, d);
    if (hojeUTC > proximo) { proximo = Date.UTC(ta + 1, m - 1, d); }
    var faltam = Math.round((proximo - hojeUTC) / 86400000);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    esvaziar();
    resultado.appendChild(document.createTextNode('Você tem '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = plural(anos, 'ano', 'anos') + ', ' + plural(meses, 'mês', 'meses') + ' e ' + plural(dias, 'dia', 'dias');
    resultado.appendChild(forte);
    resultado.appendChild(document.createElement('br'));
    var pequeno = document.createElement('small');
    pequeno.style.color = '#475569';
    var extra = 'Total: ' + plural(totalDias, 'dia vivido', 'dias vividos') + '. ';
    extra += faltam === 0 ? 'Hoje é o seu aniversário! 🎉' : 'Faltam ' + plural(faltam, 'dia', 'dias') + ' para o próximo aniversário.';
    pequeno.textContent = extra;
    resultado.appendChild(pequeno);
  }
  function limpar() {
    dia.value = '';
    mes.value = '';
    ano.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    esvaziar();
    resultado.appendChild(document.createTextNode(textoInicial));
    dia.focus();
  }
  preencher();
  document.getElementById('idade-calcular').addEventListener('click', calcular);
  document.getElementById('idade-limpar').addEventListener('click', limpar);
  ano.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
  [dia, mes, ano].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Escolha o **dia** do seu nascimento no primeiro campo.
2. Escolha o **mês** no segundo campo.
3. Digite o **ano** com 4 dígitos no terceiro campo (por exemplo, `1990`).
4. Clique em **Calcular Idade** (ou pressione Enter no campo do ano) para ver o resultado.
5. Use o botão **Limpar** para apagar a data e fazer um novo cálculo.

A idade é calculada com base na data de hoje e mostrada em anos, meses e dias. A calculadora também informa o total de dias vividos e quantos dias faltam para o próximo aniversário. Datas inexistentes (como 31 de abril) ou no futuro não são aceitas.

## Entendendo os termos

- **Data de nascimento:** dia, mês e ano em que a pessoa nasceu. É o ponto de partida do cálculo.
- **Idade:** tempo decorrido entre a data de nascimento e a data de hoje.
- **Anos:** quantidade de aniversários completos já comemorados.
- **Meses:** meses completos que se passaram desde o último aniversário. O valor vai de 0 a 11.
- **Dias:** dias completos que se passaram desde o último mês completado.
- **Dias vividos:** total de dias entre o nascimento e hoje, contando todos os anos e meses.
- **Próximo aniversário:** a próxima vez em que o dia e o mês de nascimento voltam a coincidir com o calendário.
- **Ano bissexto:** ano de 366 dias, com 29 de fevereiro. Ele ocorre a cada 4 anos e é considerado no cálculo dos dias.