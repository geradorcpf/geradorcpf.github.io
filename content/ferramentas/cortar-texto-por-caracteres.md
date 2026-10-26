---
title: "Cortar Texto em X Letras"
seoTitle: "Cortar Texto em X Letras"
description: "Cortar Texto em X Letras: corte um texto no número de letras que você escolher. Grátis e online, sem cadastro."
summary: "Corte um texto no número de letras que você escolher."
date: 2026-10-26
draft: false
category: "texto"
tags: ["caracteres", "formatação", "texto"]
keywords: ["cortar texto em x letras", "cortar texto em x letras online", "caracteres", "formatação", "texto"]
---

<!--sudah dikerjakan-->

Basta colar o texto abaixo, informar quantas letras quer manter e clicar em **Cortar Texto**.

<div id="calc-cortar" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✂️ Cortar Texto em X Letras</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto, escolha o limite e veja o resultado na hora.</p>
<label for="cor-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o texto</label>
<textarea id="cor-texto" rows="6" placeholder="Cole ou digite o seu texto aqui..." style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="cor-qtd" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cortar em quantas letras?</label>
<input id="cor-qtd" type="text" inputmode="numeric" placeholder="Ex.: 100" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="margin-bottom:20px;font-size:0.95rem;">
<span style="display:block;margin-bottom:6px;font-weight:600;">Adicionar "..." (reticências)?</span>
<label for="cor-ret-sim" style="margin-right:18px;cursor:pointer;"><input type="radio" id="cor-ret-sim" name="cor-ret" value="sim" checked style="margin-right:6px;accent-color:#4f46e5;">Sim</label>
<label for="cor-ret-nao" style="cursor:pointer;"><input type="radio" id="cor-ret-nao" name="cor-ret" value="nao" style="margin-right:6px;accent-color:#4f46e5;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cor-cortar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Cortar Texto</button>
<button type="button" id="cor-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="cor-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cor-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cor-resultado" style="white-space:pre-wrap;word-break:break-word;">preencha os campos e clique em "Cortar Texto".</span><br><small id="cor-info" style="color:#475569;"></small></div>
</div>
<script>
(function () {
  var texto = document.getElementById('cor-texto');
  var qtd = document.getElementById('cor-qtd');
  var resultado = document.getElementById('cor-resultado');
  var info = document.getElementById('cor-info');
  var caixa = document.getElementById('cor-resposta');
  var btnCopiar = document.getElementById('cor-copiar');
  var padrao = 'preencha os campos e clique em "Cortar Texto".';
  var ultimo = '';
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function erro(msg) {
    ultimo = '';
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
    info.textContent = '';
  }
  function cortar() {
    var letras = Array.from(texto.value);
    var q = String(qtd.value).trim();
    if (letras.length === 0) { erro('digite o texto que você quer cortar.'); return; }
    if (!/^\d+$/.test(q) || Number(q) === 0) { erro('informe um número inteiro maior que zero.'); return; }
    var n = Number(q);
    var foiCortado = letras.length > n;
    var saida = letras.slice(0, n).join('');
    if (foiCortado) {
      if (document.getElementById('cor-ret-sim').checked) { saida = saida + '...'; }
    }
    ultimo = saida;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = saida;
    if (foiCortado) {
      info.textContent = 'Texto original: ' + fmt(letras.length) + ' letras | Mantidas: ' + fmt(n) + ' letras';
    } else {
      info.textContent = 'O texto tem ' + fmt(letras.length) + ' letras, então nada foi cortado.';
    }
  }
  function copiar() {
    if (ultimo === '') { return; }
    function feito() {
      btnCopiar.textContent = 'Copiado!';
      setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
    }
    function alternativa() {
      var t = document.createElement('textarea');
      t.value = ultimo;
      document.body.appendChild(t);
      t.select();
      try { document.execCommand('copy'); feito(); } catch (e) {}
      document.body.removeChild(t);
    }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(ultimo).then(feito).catch(alternativa);
    } else {
      alternativa();
    }
  }
  function limpar() {
    texto.value = '';
    qtd.value = '';
    ultimo = '';
    document.getElementById('cor-ret-sim').checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    info.textContent = '';
    texto.focus();
  }
  document.getElementById('cor-cortar').addEventListener('click', cortar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('cor-limpar').addEventListener('click', limpar);
  qtd.addEventListener('keydown', function (e) { if (e.key === 'Enter') { cortar(); } });
  [texto, qtd].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Cole ou digite o texto no campo **Digite o texto**.
2. Informe em **Cortar em quantas letras?** o número de letras que você quer manter (por exemplo, `100`).
3. Escolha se quer **Adicionar "..." (reticências)** no final do texto cortado: **Sim** ou **Não**.
4. Clique em **Cortar Texto** (ou pressione Enter no campo de número) para ver o resultado.
5. Use **Copiar** para levar o texto cortado para a área de transferência e **Limpar** para começar de novo.

Espaços, vírgulas, pontos e quebras de linha também contam como letra. Se o texto já for menor ou igual ao limite, ele permanece inteiro e as reticências não são adicionadas.

## Entendendo os termos

- **Texto:** o conteúdo que você quer encurtar, como uma frase, um parágrafo, uma legenda ou uma descrição.
- **Letra (caractere):** cada símbolo do texto, incluindo letras, números, espaços, pontuação e emojis. É a unidade usada para medir o corte.
- **Cortar em X letras:** limite máximo de letras que serão mantidas, contando a partir do início do texto.
- **Reticências ("..."):** três pontos adicionados ao final para indicar que o texto continua. Elas só aparecem quando houve corte e não entram na contagem do limite.
- **Texto cortado:** resultado final, com apenas as primeiras X letras do texto original.
- **Contagem de letras:** total de caracteres do texto original e do trecho mantido, exibido abaixo do resultado.