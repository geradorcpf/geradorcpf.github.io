---
title: "Comparar Textos"
seoTitle: "Comparar Textos: online e grátis"
description: "Comparar Textos: compare dois textos e veja as diferenças. Grátis e online, sem cadastro."
summary: "Compare dois textos e veja as diferenças."
date: 2026-10-24
draft: false
category: "texto"
tags: ["comparação", "análise de texto", "texto"]
keywords: ["comparar textos", "comparar textos online", "comparação", "análise de texto", "texto"]
---

<!--sudah dikerjakan-->

Basta colar o texto original e o texto novo abaixo e depois clicar em **Comparar Textos**.

<div id="comp-textos" style="max-width:760px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📝 Comparar Textos</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole os dois textos e veja as diferenças na hora.</p>
<label for="ct-base" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto Base</label>
<textarea id="ct-base" rows="7" placeholder="Cole aqui o texto original" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="ct-novo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Novo Texto</label>
<textarea id="ct-novo" rows="7" placeholder="Cole aqui o texto modificado" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:18px;flex-wrap:wrap;margin-bottom:20px;font-size:0.95rem;">
<label style="display:flex;align-items:center;gap:6px;cursor:pointer;"><input type="checkbox" id="ct-caixa" style="width:16px;height:16px;cursor:pointer;"> Ignorar maiúsculas e minúsculas</label>
<label style="display:flex;align-items:center;gap:6px;cursor:pointer;"><input type="checkbox" id="ct-espacos" style="width:16px;height:16px;cursor:pointer;"> Ignorar espaços extras</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ct-comparar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Comparar Textos</button>
<button type="button" id="ct-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar Tudo</button>
</div>
<div id="ct-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ct-resultado">preencha os campos e clique em "Comparar Textos".</span><div id="ct-diff" style="margin-top:12px;"></div></div>
</div>
<script>
(function () {
  var base = document.getElementById('ct-base');
  var novo = document.getElementById('ct-novo');
  var caixaOpt = document.getElementById('ct-caixa');
  var espacosOpt = document.getElementById('ct-espacos');
  var resultado = document.getElementById('ct-resultado');
  var caixa = document.getElementById('ct-resposta');
  var saida = document.getElementById('ct-diff');
  var LIMITE = 4000000;
  function chave(s) {
    var t = s;
    if (caixaOpt.checked) { t = t.toLowerCase(); }
    if (espacosOpt.checked) { t = t.replace(/\s+/g, ' ').trim(); }
    return t;
  }
  function chaves(lista) {
    return lista.map(function (s) { return chave(s); });
  }
  function diff(A, B) {
    var KA = chaves(A);
    var KB = chaves(B);
    var n = A.length;
    var m = B.length;
    var i, j;
    var L = [];
    for (i = 0; i !== n + 1; i++) { L.push(new Int32Array(m + 1)); }
    for (i = n - 1; i >= 0; i--) {
      for (j = m - 1; j >= 0; j--) {
        if (KA[i] === KB[j]) { L[i][j] = L[i + 1][j + 1] + 1; }
        else { L[i][j] = Math.max(L[i + 1][j], L[i][j + 1]); }
      }
    }
    var ops = [];
    i = 0;
    j = 0;
    while (i !== n && j !== m) {
      if (KA[i] === KB[j]) { ops.push({ t: 'eq', a: A[i], b: B[j] }); i++; j++; }
      else if (L[i + 1][j] >= L[i][j + 1]) { ops.push({ t: 'del', a: A[i] }); i++; }
      else { ops.push({ t: 'add', b: B[j] }); j++; }
    }
    while (i !== n) { ops.push({ t: 'del', a: A[i] }); i++; }
    while (j !== m) { ops.push({ t: 'add', b: B[j] }); j++; }
    return ops;
  }
  var ESTILO = {
    eq: { bg: '#ffffff', borda: '#e2e8f0', cor: '#475569', marca: '#e2e8f0', sinal: ' ' },
    del: { bg: '#fef2f2', borda: '#fca5a5', cor: '#b91c1c', marca: '#fecaca', sinal: '-' },
    add: { bg: '#f0fdf4', borda: '#86efac', cor: '#166534', marca: '#bbf7d0', sinal: '+' }
  };
  function linha(tipo, partes) {
    var e = ESTILO[tipo];
    var row = document.createElement('div');
    row.style.cssText = 'display:flex;gap:10px;padding:6px 10px;margin-bottom:4px;border-left:4px solid ' + e.borda + ';border-radius:6px;background:' + e.bg + ';color:' + e.cor + ';font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:0.9rem;line-height:1.5;';
    var sinal = document.createElement('span');
    sinal.style.cssText = 'flex:none;font-weight:700;white-space:pre;';
    sinal.textContent = e.sinal;
    var corpo = document.createElement('span');
    corpo.style.cssText = 'flex:1;white-space:pre-wrap;word-break:break-word;';
    partes.forEach(function (p) {
      var s = document.createElement('span');
      if (p.destaque) { s.style.cssText = 'background:' + e.marca + ';font-weight:700;border-radius:3px;'; }
      s.textContent = p.texto;
      corpo.appendChild(s);
    });
    if (partes.length === 0) { corpo.textContent = ' '; }
    row.appendChild(sinal);
    row.appendChild(corpo);
    return row;
  }
  function simples(texto) {
    return [{ texto: texto, destaque: false }];
  }
  function palavras(a, b) {
    var ta = a.split(/(\s+)/).filter(function (x) { return x !== ''; });
    var tb = b.split(/(\s+)/).filter(function (x) { return x !== ''; });
    if (ta.length * tb.length > LIMITE) { return { a: simples(a), b: simples(b) }; }
    var ops = diff(ta, tb);
    var pa = [];
    var pb = [];
    ops.forEach(function (o) {
      if (o.t === 'eq') { pa.push({ texto: o.a, destaque: false }); pb.push({ texto: o.b, destaque: false }); }
      else if (o.t === 'del') { pa.push({ texto: o.a, destaque: true }); }
      else { pb.push({ texto: o.b, destaque: true }); }
    });
    return { a: pa, b: pb };
  }
  function descarregar(dels, adds) {
    var k = Math.min(dels.length, adds.length);
    var i;
    var pares = [];
    for (i = 0; i !== k; i++) { pares.push(palavras(dels[i], adds[i])); }
    for (i = 0; i !== dels.length; i++) {
      saida.appendChild(linha('del', i >= k ? simples(dels[i]) : pares[i].a));
    }
    for (i = 0; i !== adds.length; i++) {
      saida.appendChild(linha('add', i >= k ? simples(adds[i]) : pares[i].b));
    }
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
    saida.textContent = '';
  }
  function comparar() {
    var va = base.value;
    var vb = novo.value;
    if (va.trim() === '' && vb.trim() === '') { erro('digite ou cole pelo menos um dos textos.'); return; }
    var A = va.split(/\r\n|\r|\n/);
    var B = vb.split(/\r\n|\r|\n/);
    if (A.length * B.length > LIMITE) { erro('os textos são muito grandes para comparar de uma vez. Tente comparar trechos menores.'); return; }
    var ops = diff(A, B);
    var iguais = 0;
    var removidas = 0;
    var adicionadas = 0;
    saida.textContent = '';
    var dels = [];
    var adds = [];
    ops.forEach(function (o) {
      if (o.t === 'eq') {
        descarregar(dels, adds);
        dels = [];
        adds = [];
        iguais++;
        saida.appendChild(linha('eq', simples(o.b)));
      } else if (o.t === 'del') { dels.push(o.a); removidas++; }
      else { adds.push(o.b); adicionadas++; }
    });
    descarregar(dels, adds);
    if (removidas === 0 && adicionadas === 0) {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
      resultado.textContent = 'os textos são idênticos. Nenhuma diferença encontrada.';
      saida.textContent = '';
      return;
    }
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#1e293b';
    resultado.textContent = 'foram encontradas diferenças: ' + removidas + ' linha(s) removida(s), ' + adicionadas + ' linha(s) adicionada(s) e ' + iguais + ' linha(s) sem alteração.';
  }
  function limpar() {
    base.value = '';
    novo.value = '';
    caixaOpt.checked = false;
    espacosOpt.checked = false;
    saida.textContent = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Comparar Textos".';
    base.focus();
  }
  document.getElementById('ct-comparar').addEventListener('click', comparar);
  document.getElementById('ct-limpar').addEventListener('click', limpar);
  [base, novo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Cole ou digite o texto original no campo **Texto Base**.
2. Cole ou digite a versão modificada no campo **Novo Texto**.
3. Se quiser, marque **Ignorar maiúsculas e minúsculas** e/ou **Ignorar espaços extras** para desconsiderar esses detalhes na comparação.
4. Clique em **Comparar Textos** para ver as diferenças linha por linha.
5. Use o botão **Limpar Tudo** para apagar os dois textos e fazer uma nova comparação.

Você pode comparar textos comuns, listas, trechos de documentos ou códigos de programação. As linhas em vermelho existem só no Texto Base, as linhas em verde existem só no Novo Texto e as linhas em branco são iguais nos dois. Quando uma linha foi alterada, as palavras que mudaram aparecem com um destaque mais forte.

## Entendendo os termos

- **Texto Base:** o texto original, usado como ponto de partida da comparação.
- **Novo Texto:** a versão modificada, que será comparada com o Texto Base.
- **Comparar Textos:** botão que executa a comparação e mostra o resultado.
- **Limpar Tudo:** botão que apaga os dois campos e o resultado, para começar de novo.
- **Diferença:** qualquer trecho que foi removido, adicionado ou alterado entre o Texto Base e o Novo Texto.
- **Linha removida:** linha que está no Texto Base, mas não aparece no Novo Texto. É mostrada em vermelho, com o sinal de menos (-).
- **Linha adicionada:** linha que está no Novo Texto, mas não existia no Texto Base. É mostrada em verde, com o sinal de mais (+).
- **Linha sem alteração:** linha idêntica nos dois textos. É mostrada em branco, sem destaque.
- **Destaque de palavras:** realce das palavras exatas que mudaram dentro de uma linha alterada.
- **Ignorar maiúsculas e minúsculas:** opção que trata letras maiúsculas e minúsculas como iguais, então "Casa" e "casa" não contam como diferença.
- **Ignorar espaços extras:** opção que desconsidera espaços repetidos e espaços no início ou no fim da linha.

## Exemplo resolvido

Compare os dois textos abaixo.

**Texto Base:**

```
O gato dorme no sofá.
A casa é grande.
```

**Novo Texto:**

```
O gato dorme na cama.
A casa é grande.
```

1. Cole o primeiro texto em **Texto Base** e o segundo em **Novo Texto**.
2. Clique em **Comparar Textos**.
3. A primeira linha aparece como removida (vermelho) e como adicionada (verde), com as palavras "no sofá." e "na cama." destacadas.
4. A segunda linha é igual nos dois textos e aparece sem alteração.

**Resposta:** foi encontrada 1 linha removida, 1 linha adicionada e 1 linha sem alteração.