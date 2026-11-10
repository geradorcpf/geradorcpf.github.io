---
title: "Sorteador de Números Aleatórios"
seoTitle: "Sorteador de Números Aleatórios"
description: "Sorteador de Números Aleatórios: sorteie um ou vários números aleatórios. Grátis e online, sem cadastro."
summary: "Sorteie um ou vários números aleatórios."
date: 2026-11-10
draft: false
category: "aleatorio"
tags: ["sorteio", "números aleatórios", "gerador"]
keywords: ["sorteador de números aleatórios", "sorteador de números aleatórios online", "sorteio", "números aleatórios", "gerador"]
---
<!--INI SUDAH DIKERJAKAN-->

Defina o intervalo e a quantidade de números abaixo e depois clique em **Sortear**.

<div id="calc-sorteador" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎲 Sorteador de Números Aleatórios</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o intervalo e veja os números sorteados na hora.</p>
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:16px;">
<div style="flex:1;min-width:140px;">
<label for="sor-min" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Sortear entre</label>
<input id="sor-min" type="text" inputmode="numeric" placeholder="Ex.: 1" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:140px;">
<label for="sor-max" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">e</label>
<input id="sor-max" type="text" inputmode="numeric" placeholder="Ex.: 60" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<label for="sor-qtd" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade de números</label>
<input id="sor-qtd" type="text" inputmode="numeric" value="1" placeholder="Ex.: 6" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="sor-nome" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Nome do sorteio (opcional)</label>
<input id="sor-nome" type="text" placeholder="Ex.: Sorteio de brindes" autocomplete="off" maxlength="80" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="sor-sem-repetir" style="display:flex;align-items:center;gap:8px;margin-bottom:10px;font-size:0.95rem;cursor:pointer;"><input id="sor-sem-repetir" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não repetir números</label>
<label for="sor-ordenar" style="display:flex;align-items:center;gap:8px;margin-bottom:20px;font-size:0.95rem;cursor:pointer;"><input id="sor-ordenar" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Ordenar do menor para o maior</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sor-sortear" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Sortear</button>
<button type="button" id="sor-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="sor-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="sor-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-word;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sor-resultado">preencha os campos e clique em "Sortear".</span></div>
</div>
<script>
(function () {
  var minEl = document.getElementById('sor-min');
  var maxEl = document.getElementById('sor-max');
  var qtdEl = document.getElementById('sor-qtd');
  var nomeEl = document.getElementById('sor-nome');
  var semRepetirEl = document.getElementById('sor-sem-repetir');
  var ordenarEl = document.getElementById('sor-ordenar');
  var btnCopiar = document.getElementById('sor-copiar');
  var resultado = document.getElementById('sor-resultado');
  var caixa = document.getElementById('sor-resposta');
  var ultimo = '';
  var LIMITE = 1000000000000;
  function inteiro(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (/^-?\d{1,3}(\.\d{3})+$/.test(t)) { t = t.replace(/\./g, ''); }
    if (!/^-?\d+$/.test(t)) { return NaN; }
    return Number(t);
  }
  function aleatorio() {
    var buf = new Uint32Array(2);
    if (window.crypto ? window.crypto.getRandomValues : false) {
      window.crypto.getRandomValues(buf);
    } else {
      buf[0] = Math.floor(Math.random() * 4294967296);
      buf[1] = Math.floor(Math.random() * 4294967296);
    }
    return ((buf[0] >>> 5) * 67108864 + (buf[1] >>> 6)) / 9007199254740992;
  }
  function sortearInteiro(a, b) {
    return a + Math.floor(aleatorio() * (b - a + 1));
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar(a, b, q, repetir) {
    var lista = [];
    var total = b - a + 1;
    var i, j, t, n;
    if (repetir) {
      for (i = 0; i !== q; i++) { lista.push(sortearInteiro(a, b)); }
      return lista;
    }
    if (total > 100000) {
      var usados = {};
      while (lista.length !== q) {
        n = sortearInteiro(a, b);
        if (!usados[n]) { usados[n] = true; lista.push(n); }
      }
      return lista;
    }
    var pool = [];
    for (i = 0; i !== total; i++) { pool.push(a + i); }
    for (i = 0; i !== q; i++) {
      j = i + Math.floor(aleatorio() * (total - i));
      t = pool[i];
      pool[i] = pool[j];
      pool[j] = t;
      lista.push(pool[i]);
    }
    return lista;
  }
  function sortear() {
    var a = inteiro(minEl.value);
    var b = inteiro(maxEl.value);
    var q = inteiro(qtdEl.value);
    var nome = nomeEl.value.trim();
    var repetir = !semRepetirEl.checked;
    if (isNaN(a) || isNaN(b)) { erro('informe números inteiros válidos no intervalo.'); return; }
    if (Math.abs(a) > LIMITE || Math.abs(b) > LIMITE) { erro('use valores entre -1.000.000.000.000 e 1.000.000.000.000.'); return; }
    if (a > b) { erro('o primeiro valor não pode ser maior que o segundo.'); return; }
    if (isNaN(q) || !(q >= 1)) { erro('informe uma quantidade de números maior ou igual a 1.'); return; }
    if (q > 1000) { erro('a quantidade máxima é de 1.000 números por sorteio.'); return; }
    var total = b - a + 1;
    if (q > total ? !repetir : false) {
      erro('sem repetição, a quantidade (' + fmt(q) + ') não pode ser maior que o total de números do intervalo (' + fmt(total) + ').');
      return;
    }
    var lista = gerar(a, b, q, repetir);
    if (ordenarEl.checked) { lista.sort(function (x, y) { return x - y; }); }
    ultimo = lista.join(', ');
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    if (nome !== '') {
      var titulo = document.createElement('div');
      titulo.style.fontWeight = '700';
      titulo.style.color = '#3730a3';
      titulo.textContent = nome;
      resultado.appendChild(titulo);
    }
    var rotulo = document.createElement('span');
    rotulo.textContent = (q === 1 ? 'O número sorteado é ' : 'Os números sorteados são ');
    var destaque = document.createElement('strong');
    destaque.style.fontSize = '1.2rem';
    destaque.textContent = ultimo;
    var info = document.createElement('small');
    info.style.color = '#475569';
    info.textContent = 'Sorteio gerado para o intervalo de ' + a + ' a ' + b + ', realizado em ' + new Date().toLocaleString('pt-BR') + '.';
    resultado.appendChild(rotulo);
    resultado.appendChild(destaque);
    resultado.appendChild(document.createElement('br'));
    resultado.appendChild(info);
  }
  function copiarFallback(texto) {
    var area = document.createElement('textarea');
    area.value = texto;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) { }
    document.body.removeChild(area);
  }
  function copiar() {
    if (ultimo === '') { erro('faça um sorteio antes de copiar o resultado.'); return; }
    var texto = ultimo;
    if (navigator.clipboard ? navigator.clipboard.writeText : false) {
      navigator.clipboard.writeText(texto).catch(function () { copiarFallback(texto); });
    } else {
      copiarFallback(texto);
    }
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function limpar() {
    minEl.value = '';
    maxEl.value = '';
    qtdEl.value = '1';
    nomeEl.value = '';
    semRepetirEl.checked = false;
    ordenarEl.checked = false;
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Sortear".';
    minEl.focus();
  }
  document.getElementById('sor-sortear').addEventListener('click', sortear);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('sor-limpar').addEventListener('click', limpar);
  [minEl, maxEl, qtdEl, nomeEl].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { sortear(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o sorteador

1. Digite o menor número do intervalo no campo **Sortear entre** (por exemplo, `1`).
2. Digite o maior número do intervalo no campo **e** (por exemplo, `60`).
3. Informe a **Quantidade de números** que você quer sortear (por exemplo, `6`).
4. Se quiser, dê um nome ao sorteio no campo **Nome do sorteio**. Esse passo é opcional.
5. Marque **Não repetir números** se cada número só pode aparecer uma vez, e **Ordenar do menor para o maior** se quiser o resultado em ordem crescente.
6. Clique em **Sortear** (ou pressione Enter) para ver o resultado.
7. Use **Copiar** para copiar os números sorteados e **Limpar** para apagar tudo e começar de novo.

Use apenas números inteiros, positivos ou negativos. Os dois extremos do intervalo também podem ser sorteados. Por exemplo, ao sortear entre 1 e 10, tanto o 1 quanto o 10 entram no sorteio.

## Entendendo os termos

- **Sorteio:** escolha de um ou mais números ao acaso, sem que ninguém possa prever ou controlar o resultado.
- **Número aleatório:** número escolhido ao acaso dentro de um conjunto de possibilidades, em que todos têm a mesma chance de sair.
- **Intervalo:** faixa de números entre um valor inicial e um valor final. No intervalo de 1 a 100, qualquer inteiro de 1 até 100 pode ser sorteado.
- **Valor inicial e valor final:** o menor e o maior número que podem sair no sorteio. Os dois estão incluídos no intervalo.
- **Quantidade de números:** quantos números serão sorteados de uma vez. Neste sorteador, o limite é de 1.000 por sorteio.
- **Não repetir números:** opção que impede o mesmo número de sair duas vezes. Nesse caso, a quantidade não pode ser maior que o total de números do intervalo.
- **Ordenar:** opção que organiza o resultado do menor para o maior número, o que facilita a leitura quando saem muitos valores.
- **Nome do sorteio:** título opcional exibido junto ao resultado, útil para identificar o sorteio, como "Sorteio de brindes" ou "Rifa da turma".
- **Número inteiro:** número sem parte decimal, como -3, 0, 7 ou 250.

## Para que serve

- **Sorteios e promoções:** escolher vencedores de forma justa, por exemplo, sorteando o número de um cupom ou de um comentário.
- **Loterias e rifas:** gerar números de apostas ou o número vencedor de uma rifa.
- **Jogos e brincadeiras:** definir a ordem dos jogadores ou simular um dado com qualquer número de lados.
- **Distribuição de tarefas:** decidir quem faz o quê numa equipe ou turma, atribuindo um número a cada pessoa.

## Exemplo resolvido

Uma professora tem 30 alunos numerados de 1 a 30 e quer escolher 3 deles para apresentar o trabalho, sem que nenhum seja escolhido duas vezes. Como ela deve configurar o sorteio?

1. Defina o intervalo: sortear entre **1** e **30**.
2. Defina a quantidade: **3** números.
3. Marque **Não repetir números**, para que nenhum aluno seja escolhido duas vezes.
4. Clique em **Sortear**.

**Resposta:** o sorteador mostra 3 números diferentes entre 1 e 30, por exemplo `7, 19, 24`. Os alunos com esses números apresentam o trabalho.