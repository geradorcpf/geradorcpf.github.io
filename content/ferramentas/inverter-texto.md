---
title: "Inverter Texto"
seoTitle: "Inverter Texto"
description: "Inverter Texto: inverta a ordem dos caracteres de um texto. Grátis e online, sem cadastro."
summary: "Inverta a ordem dos caracteres de um texto."
date: 2026-11-04
draft: false
category: "texto"
tags: ["texto invertido", "divertido", "texto"]
keywords: ["inverter texto", "inverter texto online", "texto invertido", "divertido", "texto"]
---

Basta digitar uma palavra, frase ou texto abaixo e depois clicar em **Inverter Texto**.

<div id="inv-texto-box" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔄 Inverter Texto</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto e veja o resultado invertido na hora.</p>
<label for="inv-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="inv-entrada" rows="4" placeholder="Ex.: Olá, mundo!" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="inv-inverter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Inverter Texto</button>
<button type="button" id="inv-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="inv-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="inv-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="inv-resultado" style="white-space:pre-wrap;word-break:break-word;">digite um texto e clique em "Inverter Texto".</span></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('inv-entrada');
  var resultado = document.getElementById('inv-resultado');
  var caixa = document.getElementById('inv-resposta');
  var botaoCopiar = document.getElementById('inv-copiar');
  var ultimo = '';
  var padrao = 'digite um texto e clique em "Inverter Texto".';
  function partes(texto) {
    var s = texto.normalize('NFC');
    if (typeof Intl !== 'undefined') {
      if (Intl.Segmenter) {
        var seg = new Intl.Segmenter(undefined, { granularity: 'grapheme' });
        return Array.from(seg.segment(s), function (x) { return x.segment; });
      }
    }
    return Array.from(s);
  }
  function inverter(texto) {
    return partes(texto).reverse().join('');
  }
  function erro(msg) {
    ultimo = '';
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var texto = entrada.value;
    if (texto.trim() === '') { erro('digite algum texto para inverter.'); return; }
    ultimo = inverter(texto);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = ultimo;
  }
  function copiarFallback(texto) {
    var tmp = document.createElement('textarea');
    tmp.value = texto;
    tmp.style.position = 'fixed';
    tmp.style.opacity = '0';
    document.body.appendChild(tmp);
    tmp.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(tmp);
  }
  function copiar() {
    if (ultimo === '') { erro('inverta um texto antes de copiar.'); return; }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(ultimo).catch(function () { copiarFallback(ultimo); });
    } else {
      copiarFallback(ultimo);
    }
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function limpar() {
    entrada.value = '';
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    entrada.focus();
  }
  document.getElementById('inv-inverter').addEventListener('click', calcular);
  botaoCopiar.addEventListener('click', copiar);
  document.getElementById('inv-limpar').addEventListener('click', limpar);
  entrada.addEventListener('focus', function () { entrada.style.borderColor = '#6366f1'; });
  entrada.addEventListener('blur', function () { entrada.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole a palavra, frase ou texto no campo **Texto**.
2. Clique em **Inverter Texto** para ver o resultado na hora.
3. Clique em **Copiar** para levar o texto invertido para a área de transferência.
4. Use o botão **Limpar** para apagar o campo e inverter um novo texto.

A ferramenta inverte a ordem dos caracteres, do último para o primeiro. Por exemplo, o texto `Olá, mundo!` vira `!odnum ,álO`. Letras com acento, números, espaços, pontuação e emojis também são invertidos normalmente.

## Entendendo os termos

- **Inverter texto:** escrever um texto de trás para frente, de modo que o último caractere passe a ser o primeiro.
- **Caractere:** cada símbolo individual de um texto, como uma letra, número, espaço, sinal de pontuação ou emoji.
- **String:** termo da programação para uma sequência de caracteres, ou seja, um texto.
- **Texto invertido:** resultado da inversão, também chamado de texto de trás para frente ou texto espelhado.
- **Palíndromo:** palavra ou frase que continua igual quando lida de trás para frente, como "arara" ou "ovo".
- **Espaços e pontuação:** também contam como caracteres, por isso mudam de posição junto com as letras.
- **Copiar:** ação que envia o texto invertido para a área de transferência, pronta para colar em outro lugar.