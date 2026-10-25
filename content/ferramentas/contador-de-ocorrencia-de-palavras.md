---
title: "Contador de Ocorrência de Palavra"
seoTitle: "Contador de Ocorrência de Palavra"
description: "Contador de Ocorrência de Palavra: conte quantas vezes cada palavra aparece no texto. Grátis e online, sem cadastro."
summary: "Conte quantas vezes cada palavra aparece no texto."
date: 2026-10-25
draft: false
category: "texto"
tags: ["contador", "palavras", "análise de texto", "texto"]
keywords: ["contador de ocorrência de palavra", "contador de ocorrência de palavra online", "contador", "palavras", "análise de texto"]
---
<!--sudah dikerjakan-->

Basta digitar o texto e a palavra procurada abaixo e depois clicar em **Contar Palavras**.

<div id="contador-palavra" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔎 Contador de Ocorrência de Palavra</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto, a palavra procurada e veja o resultado na hora.</p>
<label for="oc-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o texto</label>
<textarea id="oc-texto" rows="6" placeholder="Cole ou digite o texto aqui..." style="width:100%;min-height:140px;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="oc-palavra" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite a palavra procurada</label>
<input id="oc-palavra" type="text" placeholder="Ex.: casa" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="margin-bottom:20px;">
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Diferenciar letras maiúsculas de minúsculas?</span>
<label for="oc-sim" style="display:inline-flex;align-items:center;gap:6px;margin-right:18px;font-size:0.95rem;cursor:pointer;"><input type="radio" id="oc-sim" name="oc-diferenciar" value="sim" style="accent-color:#4f46e5;width:18px;height:18px;margin:0;cursor:pointer;">Sim</label>
<label for="oc-nao" style="display:inline-flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" id="oc-nao" name="oc-diferenciar" value="nao" checked style="accent-color:#4f46e5;width:18px;height:18px;margin:0;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="oc-contar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Contar Palavras</button>
<button type="button" id="oc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="oc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="oc-resultado">preencha os campos e clique em "Contar Palavras".</span></div>
</div>
<script>
(function () {
  var texto = document.getElementById('oc-texto');
  var palavra = document.getElementById('oc-palavra');
  var sim = document.getElementById('oc-sim');
  var caixa = document.getElementById('oc-resposta');
  var resultado = document.getElementById('oc-resultado');
  var PADRAO = 'preencha os campos e clique em "Contar Palavras".';
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function igualar(s, diferenciar) { return diferenciar ? s : s.toLocaleLowerCase('pt-BR'); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function add(pai, tag, conteudo, estilo) {
    var el = document.createElement(tag);
    if (conteudo) { el.textContent = conteudo; }
    if (estilo) { el.setAttribute('style', estilo); }
    pai.appendChild(el);
    return el;
  }
  function contar() {
    var t = texto.value;
    var p = palavra.value.trim();
    if (t.trim() === '') { erro('digite o texto.'); return; }
    if (p === '') { erro('digite a palavra procurada.'); return; }
    if (!/^[\p{L}\p{N}]+$/u.test(p)) { erro('digite apenas uma palavra (somente letras e números, sem espaços).'); return; }
    var diferenciar = sim.checked;
    var lista = t.match(/[\p{L}\p{N}]+/gu) || [];
    var alvo = igualar(p, diferenciar);
    var total = 0;
    lista.forEach(function (w) {
      if (igualar(w, diferenciar) === alvo) { total += 1; }
    });
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode('A palavra '));
    add(resultado, 'strong', p);
    resultado.appendChild(document.createTextNode(' aparece '));
    add(resultado, 'strong', fmt(total) + (total === 1 ? ' vez' : ' vezes'), 'font-size:1.2rem;');
    resultado.appendChild(document.createTextNode(' no texto.'));
    add(resultado, 'br');
    add(resultado, 'small', 'Total de palavras no texto: ' + fmt(lista.length), 'color:#475569;');
  }
  function limpar() {
    texto.value = '';
    palavra.value = '';
    document.getElementById('oc-nao').checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = PADRAO;
    texto.focus();
  }
  document.getElementById('oc-contar').addEventListener('click', contar);
  document.getElementById('oc-limpar').addEventListener('click', limpar);
  palavra.addEventListener('keydown', function (e) { if (e.key === 'Enter') { contar(); } });
  [texto, palavra].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o texto no campo **Digite o texto**.
2. Digite a palavra que você quer contar no campo **Digite a palavra procurada**.
3. Escolha se deseja diferenciar letras maiúsculas de minúsculas: **Sim** ou **Não**.
4. Clique em **Contar Palavras** (ou pressione Enter no campo da palavra) para ver o resultado.
5. Use o botão **Limpar** para apagar os campos e fazer uma nova contagem.

A ferramenta conta apenas palavras inteiras. Por exemplo, ao procurar por `casa`, a palavra `casamento` não é contada. Informe uma palavra por vez, sem espaços.

## Entendendo os termos

- **Ocorrência:** cada vez que a palavra procurada aparece no texto.
- **Texto:** conjunto de palavras e frases em que a busca será feita.
- **Palavra procurada:** a palavra que você quer encontrar e contar dentro do texto.
- **Diferenciar maiúsculas de minúsculas:** opção que faz a busca tratar `Casa` e `casa` como palavras diferentes. Com **Não**, as duas são contadas juntas.
- **Palavra inteira:** sequência de letras e números separada das outras por espaços ou pontuação. `casa` dentro de `casamento` não conta como palavra inteira.
- **Total de palavras:** quantidade de todas as palavras do texto, incluindo as repetidas.