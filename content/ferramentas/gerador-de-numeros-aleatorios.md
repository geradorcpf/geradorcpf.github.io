---
title: "Gerador de Números Aleatórios"
seoTitle: "Gerador de Números Aleatórios"
description: "Gerador de Números Aleatórios: sorteie números aleatórios dentro do intervalo que quiser. Grátis e online, sem cadastro."
summary: "Sorteie números aleatórios dentro do intervalo que quiser."
date: 2026-11-02
draft: false
category: "aleatorio"
tags: ["números aleatórios", "sorteio", "gerador"]
keywords: ["gerador de números aleatórios", "gerador de números aleatórios online", "números aleatórios", "sorteio", "gerador"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher as opções abaixo e depois clicar em **Gerar Números**.

<div id="gerador-aleatorio" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎲 Gerador de Números Aleatórios</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Defina as opções e gere seus números na hora.</p>
<label for="rng-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade de números</label>
<input id="rng-quantidade" type="text" inputmode="numeric" value="6" placeholder="Ex.: 6" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="rng-minimo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número Mínimo</label>
<input id="rng-minimo" type="text" inputmode="numeric" value="1" placeholder="Ex.: 1" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="rng-maximo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número Máximo</label>
<input id="rng-maximo" type="text" inputmode="numeric" value="60" placeholder="Ex.: 60" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="rng-colunas" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Resultado em (colunas)</label>
<input id="rng-colunas" type="text" inputmode="numeric" value="1" placeholder="Ex.: 1" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="rng-ordem-lista" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ordem da lista</label>
<select id="rng-ordem-lista" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="aleatoria">Aleatória</option>
<option value="crescente">Crescente</option>
<option value="decrescente">Decrescente</option>
</select>
<label for="rng-ordem-numeros" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ordem dos números</label>
<select id="rng-ordem-numeros" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="linha">Linha</option>
<option value="coluna">Coluna</option>
</select>
<label for="rng-unicos" style="display:flex;align-items:center;gap:10px;margin-bottom:20px;font-weight:600;font-size:0.95rem;cursor:pointer;">
<input id="rng-unicos" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">
Números únicos (sem repetição)
</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="rng-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Números</button>
<button type="button" id="rng-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="rng-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rng-resultado">defina as opções e clique em "Gerar Números".</span><div id="rng-tabela" style="margin-top:12px;overflow-x:auto;"></div></div>
</div>
<script>
(function () {
  var qtdEl = document.getElementById('rng-quantidade');
  var minEl = document.getElementById('rng-minimo');
  var maxEl = document.getElementById('rng-maximo');
  var colEl = document.getElementById('rng-colunas');
  var listaEl = document.getElementById('rng-ordem-lista');
  var numerosEl = document.getElementById('rng-ordem-numeros');
  var unicosEl = document.getElementById('rng-unicos');
  var resultado = document.getElementById('rng-resultado');
  var caixa = document.getElementById('rng-resposta');
  var tabela = document.getElementById('rng-tabela');
  var TEXTO_INICIAL = 'defina as opções e clique em "Gerar Números".';
  function inteiro(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (!/^-?[0-9]+$/.test(t)) { return NaN; }
    return Number(t);
  }
  function digitos(v) { return String(v).replace(/[^0-9]/g, '').length; }
  function erro(msg) {
    tabela.textContent = '';
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function sortear(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }
  function gerar(qtd, min, max, unicos) {
    var lista = [];
    var faixa = max - min + 1;
    var i, j, tmp;
    if (unicos) {
      if (200000 >= faixa) {
        var pool = [];
        for (i = 0; faixa > i; i++) { pool.push(min + i); }
        for (i = 0; qtd > i; i++) {
          j = i + Math.floor(Math.random() * (faixa - i));
          tmp = pool[i];
          pool[i] = pool[j];
          pool[j] = tmp;
          lista.push(pool[i]);
        }
      } else {
        var usados = {};
        while (qtd !== lista.length) {
          var n = sortear(min, max);
          if (!usados[n]) {
            usados[n] = true;
            lista.push(n);
          }
        }
      }
    } else {
      for (i = 0; qtd > i; i++) { lista.push(sortear(min, max)); }
    }
    return lista;
  }
  function desenharTabela(lista, colunas, porColuna) {
    var total = lista.length;
    var linhas = Math.ceil(total / colunas);
    var tb = document.createElement('table');
    tb.style.cssText = 'width:100%;border-collapse:collapse;font-size:1rem;color:#166534;';
    var r, c, idx, td, tr;
    for (r = 0; linhas > r; r++) {
      tr = document.createElement('tr');
      for (c = 0; colunas > c; c++) {
        idx = porColuna ? (c * linhas + r) : (r * colunas + c);
        td = document.createElement('td');
        td.style.cssText = 'padding:8px 10px;border:1px solid #bbf7d0;text-align:center;font-weight:600;font-variant-numeric:tabular-nums;';
        td.textContent = (total > idx) ? String(lista[idx]) : '';
        tr.appendChild(td);
      }
      tb.appendChild(tr);
    }
    tabela.textContent = '';
    tabela.appendChild(tb);
  }
  function calcular() {
    var qtd = inteiro(qtdEl.value);
    var min = inteiro(minEl.value);
    var max = inteiro(maxEl.value);
    var colunas = inteiro(colEl.value);
    if (isNaN(qtd) || isNaN(min) || isNaN(max) || isNaN(colunas)) { erro('informe números inteiros válidos em todos os campos.'); return; }
    if (digitos(qtdEl.value) > 4) { erro('a quantidade de números deve ter no máximo 4 dígitos.'); return; }
    if (digitos(minEl.value) > 11 || digitos(maxEl.value) > 11) { erro('os números mínimo e máximo devem ter no máximo 11 dígitos.'); return; }
    if (digitos(colEl.value) > 5) { erro('a quantidade de colunas deve ter no máximo 5 dígitos.'); return; }
    if (1 > qtd) { erro('a quantidade de números deve ser pelo menos 1.'); return; }
    if (1 > colunas) { erro('a quantidade de colunas deve ser pelo menos 1.'); return; }
    if (min > max) { erro('o número mínimo não pode ser maior que o número máximo.'); return; }
    var unicos = unicosEl.checked;
    var faixa = max - min + 1;
    if (unicos) {
      if (qtd > faixa) { erro('não é possível gerar ' + qtd + ' números únicos em um intervalo com apenas ' + faixa + ' números.'); return; }
    }
    var lista = gerar(qtd, min, max, unicos);
    if (listaEl.value === 'crescente') { lista.sort(function (a, b) { return a - b; }); }
    if (listaEl.value === 'decrescente') { lista.sort(function (a, b) { return b - a; }); }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = qtd + (qtd === 1 ? ' número gerado' : ' números gerados') + ' entre ' + min + ' e ' + max + ':';
    desenharTabela(lista, colunas, numerosEl.value === 'coluna');
  }
  function limpar() {
    qtdEl.value = '6';
    minEl.value = '1';
    maxEl.value = '60';
    colEl.value = '1';
    listaEl.value = 'aleatoria';
    numerosEl.value = 'linha';
    unicosEl.checked = false;
    tabela.textContent = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = TEXTO_INICIAL;
    qtdEl.focus();
  }
  document.getElementById('rng-gerar').addEventListener('click', calcular);
  document.getElementById('rng-limpar').addEventListener('click', limpar);
  [qtdEl, minEl, maxEl, colEl].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  [listaEl, numerosEl].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o gerador

1. Digite a **Quantidade de números** que você quer sortear (até 4 dígitos, ou seja, no máximo 9999).
2. Informe o **Número Mínimo** e o **Número Máximo** do intervalo (até 11 dígitos cada). Os dois valores entram no sorteio.
3. Em **Resultado em (colunas)**, escolha em quantas colunas a lista será exibida (até 5 dígitos).
4. Escolha a **Ordem da lista**: aleatória, crescente ou decrescente.
5. Escolha a **Ordem dos números**: preenchendo por linha ou por coluna.
6. Marque **Números únicos** se não quiser números repetidos no resultado.
7. Clique em **Gerar Números** (ou pressione Enter) para ver o resultado.
8. Use o botão **Limpar** para restaurar as opções originais e começar de novo.

Use apenas números inteiros, positivos ou negativos. Ao marcar números únicos, a quantidade pedida não pode ser maior que o total de números do intervalo. Por exemplo, não dá para sortear 10 números únicos entre 1 e 5.

## Entendendo os termos

- **Número aleatório:** número escolhido ao acaso dentro de um intervalo, sem padrão previsível.
- **Quantidade de números:** quantos números serão gerados de uma só vez.
- **Número Mínimo:** menor valor que pode ser sorteado. Ele faz parte do intervalo.
- **Número Máximo:** maior valor que pode ser sorteado. Ele também faz parte do intervalo.
- **Número inteiro:** número sem casas decimais, como 3, 42 ou -7.
- **Resultado em (colunas):** quantidade de colunas usada para organizar os números na tabela de resultado.
- **Números únicos:** opção que impede repetições, de modo que cada número aparece no máximo uma vez.
- **Ordem da lista:** define como os números aparecem: na ordem em que foram sorteados (aleatória), do menor para o maior (crescente) ou do maior para o menor (decrescente).
- **Ordem dos números:** define se a tabela é preenchida da esquerda para a direita, linha por linha, ou de cima para baixo, coluna por coluna.