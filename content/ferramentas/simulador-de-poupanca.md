---
title: "Simulador de Poupança"
seoTitle: "Simulador de Poupança"
description: "Simulador de Poupança: simule quanto rende um depósito na poupança. Grátis e online, sem cadastro."
summary: "Simule quanto rende um depósito na poupança."
date: 2026-11-09
draft: false
category: "financas"
tags: ["poupança", "investimentos", "finanças", "simulador"]
keywords: ["simulador de poupança", "simulador de poupança online", "poupança", "investimentos", "finanças"]
---

Basta preencher os campos abaixo e depois clicar em **Calcular** para saber quanto você terá se guardar uma quantia todo mês a uma taxa de juros.

<div id="calc-poupanca" style="max-width:560px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💰 Simulador de Poupança</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os valores e veja o resultado na hora.</p>
<label for="pou-inicial" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Valor inicial (R$)</label>
<input id="pou-inicial" type="text" inputmode="decimal" placeholder="Ex.: 1000" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pou-aporte" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Aporte mensal (R$)</label>
<input id="pou-aporte" type="text" inputmode="decimal" placeholder="Ex.: 200" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pou-prazo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Prazo em anos</label>
<input id="pou-prazo" type="text" inputmode="decimal" placeholder="Ex.: 1" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pou-taxa" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Taxa de juros (% ao mês)</label>
<input id="pou-taxa" type="text" inputmode="decimal" placeholder="Ex.: 0,5" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="pou-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular</button>
<button type="button" id="pou-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="pou-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="pou-mensagem">preencha os campos e clique em "Calcular".</span>
<div id="pou-resumo" style="display:none;margin-top:8px;">
<div>Total poupado: <strong id="pou-total-poupado" style="font-size:1.1rem;"></strong></div>
<div>Juros ganhos: <strong id="pou-juros" style="font-size:1.1rem;"></strong></div>
<div>Quanto você terá: <strong id="pou-final" style="font-size:1.2rem;"></strong></div>
</div>
</div>
<div id="pou-tabela-wrap" style="display:none;margin-top:20px;max-height:360px;overflow:auto;background:#ffffff;border:1px solid #c7d2fe;border-radius:12px;">
<table style="width:100%;border-collapse:collapse;font-size:0.9rem;color:#1e293b;">
<thead>
<tr id="pou-cabecalho"></tr>
</thead>
<tbody id="pou-corpo"></tbody>
</table>
</div>
</div>
<script>
(function () {
  function el(id) { return document.getElementById(id); }
  var inicial = el('pou-inicial');
  var aporte = el('pou-aporte');
  var prazo = el('pou-prazo');
  var taxa = el('pou-taxa');
  var caixa = el('pou-resposta');
  var mensagem = el('pou-mensagem');
  var resumo = el('pou-resumo');
  var tabelaWrap = el('pou-tabela-wrap');
  var cabecalho = el('pou-cabecalho');
  var corpo = el('pou-corpo');
  var colunas = ['Mês', 'Poupado', 'Juros por mês', 'Juros acumulado', 'Total acumulado'];
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') !== -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function opcional(v) {
    return String(v).trim() === '' ? 0 : numero(v);
  }
  function brl(n) { return n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }); }
  function negativo(n) { return Math.sign(n) === -1; }
  function positivo(n) { return Math.sign(n) === 1; }
  function celula(tag, texto, esquerda) {
    var c = document.createElement(tag);
    c.textContent = texto;
    var estilo = 'padding:8px 10px;border-bottom:1px solid #e0e7ff;white-space:nowrap;text-align:' + (esquerda ? 'left' : 'right') + ';';
    if (tag === 'th') { estilo += 'position:sticky;top:0;background:#eef2ff;color:#3730a3;font-weight:700;'; }
    c.style.cssText = estilo;
    return c;
  }
  function montarCabecalho() {
    cabecalho.textContent = '';
    colunas.forEach(function (nome, i) { cabecalho.appendChild(celula('th', nome, i === 0)); });
  }
  function esconderResultados() {
    resumo.style.display = 'none';
    tabelaWrap.style.display = 'none';
    corpo.textContent = '';
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    mensagem.style.color = '#b91c1c';
    mensagem.textContent = msg;
    esconderResultados();
  }
  function calcular() {
    var vi = opcional(inicial.value);
    var va = opcional(aporte.value);
    var anos = numero(prazo.value);
    var juros = numero(taxa.value);
    if (isNaN(vi) || isNaN(va) || isNaN(anos) || isNaN(juros)) { erro('informe números válidos em todos os campos (valor inicial e aporte podem ficar vazios).'); return; }
    if (negativo(vi) || negativo(va) || negativo(juros)) { erro('os valores não podem ser negativos.'); return; }
    if (!positivo(anos)) { erro('o prazo deve ser maior que zero.'); return; }
    if (Math.min(anos, 100) !== anos) { erro('o prazo máximo é de 100 anos.'); return; }
    if (!positivo(vi + va)) { erro('informe um valor inicial ou um aporte mensal maior que zero.'); return; }
    var meses = Math.round(anos * 12);
    if (!positivo(meses)) { erro('o prazo deve ter pelo menos 1 mês.'); return; }
    var taxaMes = juros / 100;
    var saldo = vi;
    var poupado = vi;
    var jurosAcum = 0;
    var frag = document.createDocumentFragment();
    for (var m = 1; m !== meses + 1; m++) {
      var jurosMes = saldo * taxaMes;
      saldo = saldo + jurosMes + va;
      poupado = poupado + va;
      jurosAcum = jurosAcum + jurosMes;
      var tr = document.createElement('tr');
      tr.appendChild(celula('td', String(m), true));
      tr.appendChild(celula('td', brl(poupado), false));
      tr.appendChild(celula('td', brl(jurosMes), false));
      tr.appendChild(celula('td', brl(jurosAcum), false));
      tr.appendChild(celula('td', brl(saldo), false));
      frag.appendChild(tr);
    }
    corpo.textContent = '';
    corpo.appendChild(frag);
    montarCabecalho();
    el('pou-total-poupado').textContent = brl(poupado);
    el('pou-juros').textContent = brl(jurosAcum);
    el('pou-final').textContent = brl(saldo);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    mensagem.style.color = '#166534';
    mensagem.textContent = 'simulação de ' + meses + (meses === 1 ? ' mês.' : ' meses.');
    resumo.style.color = '#166534';
    resumo.style.display = 'block';
    tabelaWrap.style.display = 'block';
  }
  function limpar() {
    inicial.value = '';
    aporte.value = '';
    prazo.value = '';
    taxa.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    mensagem.style.color = '#64748b';
    mensagem.textContent = 'preencha os campos e clique em "Calcular".';
    esconderResultados();
    inicial.focus();
  }
  montarCabecalho();
  el('pou-calcular').addEventListener('click', calcular);
  el('pou-limpar').addEventListener('click', limpar);
  [inicial, aporte, prazo, taxa].forEach(function (campo) {
    campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
    campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o simulador

1. Digite o **Valor inicial**, ou seja, quanto você já tem para depositar agora (pode deixar vazio se estiver começando do zero).
2. Digite o **Aporte mensal**, o valor que você pretende depositar todo mês (também pode ficar vazio).
3. Informe o **Prazo em anos** durante o qual o dinheiro ficará aplicado (aceita decimais, como `1,5` para um ano e meio).
4. Informe a **Taxa de juros (% ao mês)**, por exemplo `0,5` para 0,5% ao mês.
5. Clique em **Calcular** (ou pressione Enter) para ver o total poupado, os juros ganhos, quanto você terá no final e a evolução mês a mês na tabela.
6. Use o botão **Limpar** para apagar os valores e fazer uma nova simulação.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `1500,50` ou `1500.50`). Preencha ao menos o valor inicial ou o aporte mensal com um número maior que zero.

## Entendendo os termos

- **Poupança:** aplicação financeira simples em que você deposita dinheiro e recebe juros periodicamente sobre o saldo.
- **Valor inicial:** quantia depositada no começo da simulação, antes dos aportes mensais.
- **Aporte mensal:** valor depositado todos os meses ao longo do prazo.
- **Prazo em anos:** tempo total em que o dinheiro fica aplicado. Cada ano equivale a 12 meses.
- **Taxa de juros (% ao mês):** percentual que o saldo rende a cada mês.
- **Juros compostos:** juros calculados sobre o saldo já acumulado, ou seja, os juros de um mês também rendem nos meses seguintes.
- **Total poupado:** soma de tudo o que você depositou do próprio bolso (valor inicial + aportes mensais), sem contar os juros.
- **Juros ganhos:** quanto o dinheiro rendeu no total ao longo do prazo.
- **Quanto você terá:** saldo final, igual ao total poupado mais os juros ganhos.
- **Juros por mês:** rendimento obtido em cada mês específico.
- **Juros acumulado:** soma dos juros recebidos desde o primeiro mês até o mês da linha.
- **Total acumulado:** saldo da aplicação ao final de cada mês, já com depósitos e juros.

## Fórmula da poupança com aportes mensais

A cada mês, os juros são calculados sobre o saldo do mês anterior e depois o aporte é somado:

**Saldo do mês = saldo anterior × (1 + taxa) + aporte mensal**

Em que a **taxa** é o percentual mensal dividido por 100 (0,5% = 0,005). Para um prazo de **n** meses, o saldo final também pode ser escrito como:

**Saldo final = valor inicial × (1 + taxa)^n + aporte × ((1 + taxa)^n − 1) ÷ taxa**

Os **juros ganhos** são o saldo final menos o total poupado. Este simulador usa uma taxa fixa por mês e serve como estimativa: o rendimento real da poupança pode variar conforme a Selic, a TR e a data de aniversário do depósito.

## Exemplo resolvido

Você começa com R$ 1.000, deposita R$ 200 por mês durante 1 ano e a taxa é de 0,5% ao mês. Quanto você terá no final?

1. Prazo: 1 ano = 12 meses. Taxa: 0,5% = 0,005.
2. Total poupado: 1.000 + (200 × 12) = R$ 3.400,00.
3. Valor inicial corrigido: 1.000 × (1,005)^12 ≈ R$ 1.061,68.
4. Aportes corrigidos: 200 × ((1,005)^12 − 1) ÷ 0,005 ≈ R$ 2.467,11.
5. Saldo final: 1.061,68 + 2.467,11 ≈ R$ 3.528,79.
6. Juros ganhos: 3.528,79 − 3.400,00 ≈ R$ 128,79.

**Resposta:** ao final de 1 ano você terá cerca de **R$ 3.528,79**, sendo R$ 3.400,00 poupados e **R$ 128,79** de juros.