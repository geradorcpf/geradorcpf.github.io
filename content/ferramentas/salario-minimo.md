---
title: "Valor do Salário Mínimo em 2026"
seoTitle: "Valor do Salário Mínimo em 2026"
description: "Valor do Salário Mínimo em 2026: consulte o valor do salário mínimo em 2026. Grátis e online, sem cadastro."
summary: "Consulte o valor do salário mínimo em 2026."
date: 2026-11-08
draft: false
category: "financas"
tags: ["salário mínimo", "trabalho", "finanças"]
keywords: ["valor do salário mínimo em 2026", "valor do salário mínimo em 2026 online", "salário mínimo", "trabalho", "finanças"]
---

O salário mínimo nacional em <span class="sm-ano-atual">2026</span> é de <strong class="sm-valor-atual">R$ 1.621,00</strong>. Para ver o valor de outros anos, selecione o ano abaixo e clique em **Consultar Valor**.

<div id="calc-salario-minimo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💰 Valor do Salário Mínimo em <span class="sm-ano-atual">2026</span></h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Consulte o valor atual e o histórico de reajustes.</p>
<div style="margin-bottom:20px;padding:16px;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;text-align:center;">
<div style="font-size:0.9rem;color:#64748b;margin-bottom:4px;">Salário mínimo atual (desde <span class="sm-vigencia-atual">01/01/2026</span>)</div>
<div style="font-size:1.75rem;font-weight:700;color:#3730a3;" class="sm-valor-atual">R$ 1.621,00</div>
</div>
<label for="sm-ano" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ano de consulta</label>
<select id="sm-ano" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="">Selecione o ano</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sm-consultar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Consultar Valor</button>
<button type="button" id="sm-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="sm-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sm-resultado">selecione um ano e clique em "Consultar Valor".</span></div>
</div>
<script>
(function () {
  // O ano exibido segue o relógio do visitante. O valor atual e a vigência vêm da
  // linha mais recente já em vigor. Para novo reajuste, adicione uma linha no TOPO.
  var dados = [
    ['2026', '01/01/2026', 1621],
    ['2025', '01/01/2025', 1518],
    ['2024', '01/01/2024', 1412],
    ['2023', '01/05/2023', 1320],
    ['2023', '01/01/2023', 1302],
    ['2022', '01/01/2022', 1212],
    ['2021', '01/01/2021', 1100],
    ['2020', '01/02/2020', 1045],
    ['2020', '01/01/2020', 1039],
    ['2019', '01/01/2019', 998],
    ['2018', '01/01/2018', 954],
    ['2017', '01/01/2017', 937],
    ['2016', '01/01/2016', 880],
    ['2015', '01/01/2015', 788],
    ['2014', '01/01/2014', 724],
    ['2013', '01/01/2013', 678],
    ['2012', '01/01/2012', 622],
    ['2011', '01/03/2011', 545],
    ['2011', '01/01/2011', 540],
    ['2010', '01/01/2010', 510],
    ['2009', '01/02/2009', 465],
    ['2008', '01/03/2008', 415],
    ['2007', '01/04/2007', 380],
    ['2006', '01/04/2006', 350],
    ['2005', '01/05/2005', 300],
    ['2004', '01/05/2004', 260],
    ['2003', '01/04/2003', 240],
    ['2002', '01/04/2002', 200],
    ['2001', '01/04/2001', 180],
    ['2000', '03/04/2000', 151]
  ];
  var select = document.getElementById('sm-ano');
  var resultado = document.getElementById('sm-resultado');
  var caixa = document.getElementById('sm-resposta');
  var padrao = 'selecione um ano e clique em "Consultar Valor".';
  var anoAtual = new Date().getFullYear();
  var vigentes = dados.filter(function (d) { return anoAtual >= Number(d[0]); });
  var ultimo = vigentes.length > 0 ? vigentes[0] : dados[0];
  var anoExibido = vigentes.length > 0 ? String(anoAtual) : ultimo[0];
  function trocar(classe, conteudo) {
    Array.prototype.forEach.call(document.querySelectorAll('.' + classe), function (el) {
      el.textContent = conteudo;
    });
  }
  function montarHistorico() {
    var alvo = document.getElementById('sm-historico');
    if (!alvo) { return; }
    var tabela = document.createElement('table');
    tabela.setAttribute('style', 'width:100%;border-collapse:collapse;font-size:0.95rem;color:#1e293b;');
    var cabeca = document.createElement('thead');
    var trCabeca = document.createElement('tr');
    ['Ano', 'Data da Vigência', 'Salário Mínimo'].forEach(function (t) {
      var th = document.createElement('th');
      th.textContent = t;
      th.setAttribute('style', 'text-align:left;padding:10px 12px;background:#eef2ff;color:#3730a3;border-bottom:2px solid #c7d2fe;');
      trCabeca.appendChild(th);
    });
    cabeca.appendChild(trCabeca);
    tabela.appendChild(cabeca);
    var corpo = document.createElement('tbody');
    dados.forEach(function (d) {
      var linha = document.createElement('tr');
      [d[0], d[1], moeda(d[2])].forEach(function (t) {
        var td = document.createElement('td');
        td.textContent = t;
        td.setAttribute('style', 'padding:10px 12px;border-bottom:1px solid #e0e7ff;');
        linha.appendChild(td);
      });
      corpo.appendChild(linha);
    });
    tabela.appendChild(corpo);
    alvo.textContent = '';
    alvo.appendChild(tabela);
  }
  function atualizarPagina() {
    trocar('sm-ano-atual', anoExibido);
    trocar('sm-vigencia-atual', ultimo[1]);
    trocar('sm-valor-atual', moeda(ultimo[2]));
    montarHistorico();
  }
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', atualizarPagina);
  } else {
    atualizarPagina();
  }
  dados.forEach(function (d, i) {
    var op = document.createElement('option');
    op.value = String(i);
    op.textContent = d[0] + ' (vigência ' + d[1] + ')';
    select.appendChild(op);
  });
  function moeda(n) { return n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }); }
  function pct(n) { return n.toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 }); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function texto(pai, conteudo, tag, estilo) {
    var el = document.createElement(tag || 'span');
    el.textContent = conteudo;
    if (estilo) { el.setAttribute('style', estilo); }
    pai.appendChild(el);
    return el;
  }
  function consultar() {
    if (select.value === '') { erro('selecione um ano na lista.'); return; }
    var i = Number(select.value);
    var d = dados[i];
    var valor = d[2];
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    texto(resultado, 'O salário mínimo em ' + d[0] + ' é de ');
    texto(resultado, moeda(valor), 'strong', 'font-size:1.2rem;');
    texto(resultado, ' (vigência desde ' + d[1] + ').');
    var detalhes = document.createElement('small');
    detalhes.setAttribute('style', 'color:#475569;');
    resultado.appendChild(document.createElement('br'));
    if (dados.length > i + 1) {
      var anterior = dados[i + 1][2];
      var reajuste = (valor / anterior - 1) * 100;
      texto(detalhes, 'Reajuste de ' + pct(reajuste) + '% sobre o valor anterior (' + moeda(anterior) + ').');
      detalhes.appendChild(document.createElement('br'));
    }
    texto(detalhes, 'Valor diário: ' + moeda(valor / 30) + ' | Valor por hora: ' + moeda(valor / 220));
    resultado.appendChild(detalhes);
  }
  function limpar() {
    select.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    select.focus();
  }
  document.getElementById('sm-consultar').addEventListener('click', consultar);
  document.getElementById('sm-limpar').addEventListener('click', limpar);
  select.addEventListener('change', function () { if (select.value !== '') { consultar(); } });
  select.addEventListener('focus', function () { select.style.borderColor = '#6366f1'; });
  select.addEventListener('blur', function () { select.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Veja no destaque do topo o valor do **salário mínimo atual**, em vigor desde <span class="sm-vigencia-atual">01/01/2026</span>.
2. Para consultar outro período, escolha o **ano** na lista de seleção.
3. Clique em **Consultar Valor** (a consulta também é feita automaticamente ao escolher o ano).
4. Leia o resultado: valor do salário mínimo, data de vigência, percentual de reajuste, valor diário e valor por hora.
5. Use o botão **Limpar** para apagar a seleção e fazer uma nova consulta.

Em alguns anos houve mais de um valor (2011, 2020 e 2023). Nesses casos, cada valor aparece na lista com a sua data de vigência.

## Entendendo os termos

- **Salário mínimo:** menor valor mensal que um empregador pode pagar a um trabalhador com carteira assinada no Brasil.
- **Salário mínimo nacional:** valor único, definido pelo governo federal, que vale para todo o país.
- **Vigência:** data a partir da qual um novo valor do salário mínimo passa a valer.
- **Reajuste:** aumento aplicado ao salário mínimo em relação ao valor anterior, geralmente expresso em porcentagem.
- **Valor diário:** salário mínimo dividido por 30 dias.
- **Valor por hora:** salário mínimo dividido por 220 horas, que correspondem à jornada mensal de 44 horas semanais.

## Histórico do salário mínimo

<div id="sm-historico" style="overflow-x:auto;margin:16px 0;"></div>