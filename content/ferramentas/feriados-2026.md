---
title: "Feriados 2026"
seoTitle: "Feriados 2026"
description: "Feriados 2026: lista de feriados nacionais de 2026. Grátis e online, sem cadastro."
summary: "Lista de feriados nacionais de 2026."
date: 2026-10-28
draft: false
category: "datas"
tags: ["feriados", "calendário", "datas", "trabalho"]
keywords: ["feriados 2026", "feriados 2026 online", "feriados", "calendário", "datas"]
---

Escolha o ano e o tipo abaixo e depois clique em **Ver Feriados** para consultar os feriados nacionais e pontos facultativos do Brasil.

<div id="calc-feriados" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📅 Feriados 2026</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Feriados nacionais e pontos facultativos do Brasil.</p>
<label for="fer-ano" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ano</label>
<select id="fer-ano" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="2024">2024</option>
<option value="2025">2025</option>
<option value="2026" selected>2026</option>
<option value="2027">2027</option>
<option value="2028">2028</option>
</select>
<label for="fer-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo</label>
<select id="fer-tipo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="Todos" selected>Todos</option>
<option value="Feriado">Feriado</option>
<option value="Ponto Facultativo">Ponto Facultativo</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="fer-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Ver Feriados</button>
<button type="button" id="fer-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="fer-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="fer-resultado">clique em "Ver Feriados".</span><div id="fer-proximo" style="margin-top:6px;font-size:0.95rem;color:#475569;"></div><div id="fer-tabela" style="margin-top:12px;overflow-x:auto;"></div></div>
</div>
<script>
(function () {
  var anoSel = document.getElementById('fer-ano');
  var tipoSel = document.getElementById('fer-tipo');
  var resultado = document.getElementById('fer-resultado');
  var proximo = document.getElementById('fer-proximo');
  var tabela = document.getElementById('fer-tabela');
  var caixa = document.getElementById('fer-resposta');
  var meses = ['janeiro', 'fevereiro', 'março', 'abril', 'maio', 'junho', 'julho', 'agosto', 'setembro', 'outubro', 'novembro', 'dezembro'];
  var dias = ['DOM', 'SEG', 'TER', 'QUA', 'QUI', 'SEX', 'SÁB'];
  function pascoa(ano) {
    var a = ano % 19;
    var b = Math.floor(ano / 100);
    var c = ano % 100;
    var d = Math.floor(b / 4);
    var e = b % 4;
    var f = Math.floor((b + 8) / 25);
    var g = Math.floor((b - f + 1) / 3);
    var h = (19 * a + b - d - g + 15) % 30;
    var i = Math.floor(c / 4);
    var k = c % 4;
    var l = (32 + 2 * e + 2 * i - h - k) % 7;
    var m = Math.floor((a + 11 * h + 22 * l) / 451);
    var mes = Math.floor((h + l - 7 * m + 114) / 31);
    var dia = ((h + l - 7 * m + 114) % 31) + 1;
    return new Date(ano, mes - 1, dia);
  }
  function somar(data, n) {
    return new Date(data.getFullYear(), data.getMonth(), data.getDate() + n);
  }
  function lista(ano) {
    var p = pascoa(ano);
    var itens = [
      { d: new Date(ano, 0, 1), n: 'Confraternização Universal', t: 'Feriado' },
      { d: somar(p, -48), n: 'Carnaval', t: 'Ponto Facultativo' },
      { d: somar(p, -47), n: 'Carnaval', t: 'Ponto Facultativo' },
      { d: somar(p, -46), n: 'Quarta-feira de Cinzas', t: 'Ponto Facultativo' },
      { d: somar(p, -2), n: 'Sexta-feira Santa', t: 'Feriado' },
      { d: new Date(ano, 3, 21), n: 'Tiradentes', t: 'Feriado' },
      { d: new Date(ano, 4, 1), n: 'Dia do Trabalhador', t: 'Feriado' },
      { d: somar(p, 60), n: 'Corpus Christi', t: 'Ponto Facultativo' },
      { d: new Date(ano, 8, 7), n: 'Independência do Brasil', t: 'Feriado' },
      { d: new Date(ano, 9, 12), n: 'Nossa Senhora Aparecida', t: 'Feriado' },
      { d: new Date(ano, 9, 28), n: 'Dia do Servidor Público', t: 'Ponto Facultativo' },
      { d: new Date(ano, 10, 2), n: 'Finados', t: 'Feriado' },
      { d: new Date(ano, 10, 15), n: 'Proclamação da República', t: 'Feriado' },
      { d: new Date(ano, 10, 20), n: 'Dia Nacional de Zumbi e da Consciência Negra', t: 'Feriado' },
      { d: new Date(ano, 11, 24), n: 'Véspera de Natal', t: 'Ponto Facultativo' },
      { d: new Date(ano, 11, 25), n: 'Natal', t: 'Feriado' },
      { d: new Date(ano, 11, 31), n: 'Véspera de Ano-Novo', t: 'Ponto Facultativo' }
    ];
    itens.sort(function (x, y) { return x.d.getTime() - y.d.getTime(); });
    return itens;
  }
  function dois(n) { return n > 9 ? String(n) : '0' + n; }
  function dataTexto(d) { return dois(d.getDate()) + ' de ' + meses[d.getMonth()]; }
  function celula(tag, texto, estilo) {
    var el = document.createElement(tag);
    el.textContent = texto;
    el.style.cssText = estilo;
    return el;
  }
  function mostrar() {
    var ano = Number(anoSel.value);
    var filtro = tipoSel.value;
    var todos = lista(ano);
    var qtdF = 0;
    var qtdP = 0;
    todos.forEach(function (it) {
      if (it.t === 'Feriado') { qtdF = qtdF + 1; } else { qtdP = qtdP + 1; }
    });
    var itens = todos.filter(function (it) { return filtro === 'Todos' || it.t === filtro; });
    var hoje = new Date();
    hoje = new Date(hoje.getFullYear(), hoje.getMonth(), hoje.getDate());
    var prox = null;
    todos.forEach(function (it) {
      if (prox === null) {
        if (it.d.getTime() >= hoje.getTime()) { prox = it; }
      }
    });
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = 'Em ' + ano + ' há ' + qtdF + ' feriados e ' + qtdP + ' pontos facultativos.';
    if (prox === null) {
      proximo.textContent = 'Todos os feriados de ' + ano + ' já passaram.';
    } else {
      var falta = Math.round((prox.d.getTime() - hoje.getTime()) / 86400000);
      var quando = 'hoje';
      if (falta === 1) { quando = 'falta 1 dia'; }
      if (falta > 1) { quando = 'faltam ' + falta + ' dias'; }
      proximo.textContent = 'Próximo: ' + prox.n + ', ' + dataTexto(prox.d) + ' (' + dias[prox.d.getDay()] + '), ' + quando + '.';
    }
    tabela.textContent = '';
    var tb = document.createElement('table');
    tb.style.cssText = 'width:100%;border-collapse:collapse;font-size:0.92rem;color:#1e293b;';
    var cab = document.createElement('tr');
    var estCab = 'text-align:left;padding:8px 10px;background:#eef2ff;color:#3730a3;border-bottom:2px solid #c7d2fe;';
    cab.appendChild(celula('th', 'Data', estCab));
    cab.appendChild(celula('th', 'Dia', estCab));
    cab.appendChild(celula('th', 'Feriado', estCab));
    cab.appendChild(celula('th', 'Tipo', estCab));
    tb.appendChild(cab);
    itens.forEach(function (it) {
      var tr = document.createElement('tr');
      var est = 'padding:8px 10px;border-bottom:1px solid #e2e8f0;';
      var cor = it.t === 'Feriado' ? 'color:#166534;font-weight:600;' : 'color:#b45309;font-weight:600;';
      tr.appendChild(celula('td', dataTexto(it.d), est));
      tr.appendChild(celula('td', dias[it.d.getDay()], est));
      tr.appendChild(celula('td', it.n, est));
      tr.appendChild(celula('td', it.t, est + cor));
      tb.appendChild(tr);
    });
    tabela.appendChild(tb);
  }
  function limpar() {
    anoSel.value = '2026';
    tipoSel.value = 'Todos';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'clique em "Ver Feriados".';
    proximo.textContent = '';
    tabela.textContent = '';
    anoSel.focus();
  }
  document.getElementById('fer-calcular').addEventListener('click', mostrar);
  document.getElementById('fer-limpar').addEventListener('click', limpar);
  [anoSel, tipoSel].forEach(function (el) {
    el.addEventListener('change', mostrar);
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  mostrar();
})();
</script>

## Como usar a calculadora

1. Escolha o **Ano** que deseja consultar (de 2024 a 2028). O padrão é 2026.
2. Escolha o **Tipo**: *Todos*, *Feriado* ou *Ponto Facultativo*.
3. Clique em **Ver Feriados** (a lista também se atualiza ao trocar o ano ou o tipo).
4. Veja o resumo com a quantidade de feriados, o **próximo feriado** e a tabela com data, dia da semana, nome e tipo.
5. Use o botão **Limpar** para voltar ao ano 2026 e esconder a lista.

## Entendendo os termos

- **Feriado nacional:** data comemorativa definida em lei federal, válida em todo o Brasil. Em geral, é dia de folga para quem trabalha.
- **Ponto facultativo:** dia em que o expediente do serviço público federal pode ser dispensado. Empresas privadas decidem por conta própria se dão folga ou não.
- **Dia da semana:** dia em que a data cai no ano escolhido (DOM, SEG, TER, QUA, QUI, SEX, SÁB). Feriados em fim de semana não geram folga extra.
- **Próximo feriado:** primeira data da lista que é igual ou posterior ao dia de hoje, com a contagem de dias que faltam.
- **Feriados fixos:** datas que caem no mesmo dia e mês todo ano, como Natal (25 de dezembro) e Tiradentes (21 de abril).
- **Feriados móveis:** datas que mudam de ano para ano porque dependem da Páscoa, como Carnaval, Sexta-feira Santa e Corpus Christi.
- **Páscoa:** domingo calculado pelo calendário lunar da Igreja. Serve de base para as datas móveis.
- **Carnaval:** segunda e terça-feira que antecedem a Quarta-feira de Cinzas, 48 e 47 dias antes da Páscoa. É ponto facultativo.
- **Quarta-feira de Cinzas:** dia que encerra o Carnaval, 46 dias antes da Páscoa. É ponto facultativo.
- **Sexta-feira Santa:** sexta-feira anterior à Páscoa (2 dias antes). É feriado nacional.
- **Corpus Christi:** quinta-feira 60 dias depois da Páscoa. É ponto facultativo.
- **Véspera:** dia anterior a uma data comemorativa, como Véspera de Natal (24/12) e Véspera de Ano-Novo (31/12). São pontos facultativos.
- **Dia do Servidor Público:** celebrado em 28 de outubro e tratado como ponto facultativo.