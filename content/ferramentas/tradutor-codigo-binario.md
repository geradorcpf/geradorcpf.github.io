---
title: "Tradutor de Código Binário"
seoTitle: "Tradutor de Código Binário"
description: "Tradutor de Código Binário: converta texto em código binário e vice-versa. Grátis e online, sem cadastro."
summary: "Converta texto em código binário e vice-versa."
date: 2026-11-12
draft: false
category: "dev"
tags: ["binário", "codificação", "conversão", "desenvolvimento"]
keywords: ["tradutor de código binário", "tradutor de código binário online", "binário", "codificação", "conversão"]
---

Digite um texto e clique em **Codificar em Binário**, ou cole um código binário e clique em **Decodificar Texto**.

<div id="tradutor-binario" style="max-width:560px;margin:24px 0;font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<div style="margin-bottom:24px;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💻 Texto para Codificar</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto e converta para binário na hora.</p>
<label for="bin-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="bin-texto" rows="4" placeholder="Ex.: Olá, mundo!" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="bin-codificar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Codificar em Binário</button>
<button type="button" id="bin-limpar-1" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="bin-caixa-1" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Texto codificado em binário:</strong> <span id="bin-resultado-1" style="white-space:pre-wrap;word-break:break-word;">preencha o campo e clique em "Codificar em Binário".</span></div>
<button type="button" id="bin-copiar-1" style="margin-top:12px;padding:10px 16px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar resultado</button>
</div>
<div style="padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔢 Binário para Traduzir</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole o código binário e veja o texto original.</p>
<label for="bin-codigo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código binário</label>
<textarea id="bin-codigo" rows="4" placeholder="Ex.: 01001111 01101100 11000011 10100001" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="bin-decodificar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Decodificar Texto</button>
<button type="button" id="bin-limpar-2" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="bin-caixa-2" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta em texto:</strong> <span id="bin-resultado-2" style="white-space:pre-wrap;word-break:break-word;">preencha o campo e clique em "Decodificar Texto".</span></div>
<button type="button" id="bin-copiar-2" style="margin-top:12px;padding:10px 16px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar resultado</button>
</div>
</div>
<script>
(function () {
  var MSG1 = 'preencha o campo e clique em "Codificar em Binário".';
  var MSG2 = 'preencha o campo e clique em "Decodificar Texto".';
  var texto = document.getElementById('bin-texto');
  var codigo = document.getElementById('bin-codigo');
  var caixa1 = document.getElementById('bin-caixa-1');
  var caixa2 = document.getElementById('bin-caixa-2');
  var res1 = document.getElementById('bin-resultado-1');
  var res2 = document.getElementById('bin-resultado-2');
  var ultimo1 = '';
  var ultimo2 = '';
  function erro(caixa, res, msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    res.style.color = '#b91c1c';
    res.textContent = msg;
  }
  function ok(caixa, res, valor) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    res.style.color = '#166534';
    res.textContent = valor;
  }
  function neutro(caixa, res, msg) {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    res.style.color = '#64748b';
    res.textContent = msg;
  }
  function codificar() {
    var v = texto.value;
    ultimo1 = '';
    if (v.length === 0) { erro(caixa1, res1, 'digite um texto para codificar.'); return; }
    var bytes = Array.prototype.slice.call(new TextEncoder().encode(v));
    var binario = bytes.map(function (b) {
      var s = b.toString(2);
      while (s.length !== 8) { s = '0' + s; }
      return s;
    }).join(' ');
    ultimo1 = binario;
    ok(caixa1, res1, binario);
  }
  function decodificar() {
    var v = codigo.value;
    ultimo2 = '';
    if (v.trim().length === 0) { erro(caixa2, res2, 'informe o código binário para decodificar.'); return; }
    if (/[^01\s]/.test(v)) { erro(caixa2, res2, 'use apenas os dígitos 0 e 1 (separados por espaço ou não).'); return; }
    var limpo = v.replace(/\s/g, '');
    if (limpo.length % 8 !== 0) { erro(caixa2, res2, 'o código binário deve ter grupos completos de 8 bits (' + limpo.length + ' dígitos informados).'); return; }
    var grupos = limpo.match(/[01]{8}/g);
    var bytes = grupos.map(function (g) { return parseInt(g, 2); });
    var texto2;
    try {
      texto2 = new TextDecoder('utf-8', { fatal: true }).decode(new Uint8Array(bytes));
    } catch (e) {
      erro(caixa2, res2, 'não foi possível converter: a sequência de bits não é um texto UTF-8 válido.');
      return;
    }
    ultimo2 = texto2;
    ok(caixa2, res2, texto2);
  }
  function copiar(valor, botao) {
    if (valor === '') { return; }
    var original = botao.textContent;
    try {
      navigator.clipboard.writeText(valor).then(function () {
        botao.textContent = 'Copiado!';
        setTimeout(function () { botao.textContent = original; }, 1500);
      });
    } catch (e) {
      botao.textContent = 'Não foi possível copiar';
      setTimeout(function () { botao.textContent = original; }, 1500);
    }
  }
  document.getElementById('bin-codificar').addEventListener('click', codificar);
  document.getElementById('bin-decodificar').addEventListener('click', decodificar);
  document.getElementById('bin-limpar-1').addEventListener('click', function () {
    texto.value = '';
    ultimo1 = '';
    neutro(caixa1, res1, MSG1);
    texto.focus();
  });
  document.getElementById('bin-limpar-2').addEventListener('click', function () {
    codigo.value = '';
    ultimo2 = '';
    neutro(caixa2, res2, MSG2);
    codigo.focus();
  });
  document.getElementById('bin-copiar-1').addEventListener('click', function (e) { copiar(ultimo1, e.currentTarget); });
  document.getElementById('bin-copiar-2').addEventListener('click', function (e) { copiar(ultimo2, e.currentTarget); });
  texto.addEventListener('keydown', function (e) { if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { codificar(); } });
  codigo.addEventListener('keydown', function (e) { if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { decodificar(); } });
  [texto, codigo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o tradutor

**Para converter texto em binário:**

1. Digite ou cole o texto no campo **Texto**.
2. Clique em **Codificar em Binário** (ou pressione Ctrl + Enter).
3. O código binário aparece na caixa de resposta, com cada caractere representado por grupos de 8 bits separados por espaço.
4. Use **Copiar resultado** para copiar o código ou **Limpar** para recomeçar.

**Para converter binário em texto:**

1. Cole o código no campo **Código binário**. Ele deve conter apenas os dígitos `0` e `1`, com ou sem espaços entre os grupos.
2. Clique em **Decodificar Texto** (ou pressione Ctrl + Enter).
3. O texto original aparece na caixa de resposta.
4. Se o código tiver dígitos diferentes de 0 e 1, ou se a quantidade de dígitos não for múltipla de 8, o tradutor mostra uma mensagem de erro indicando o problema.

O tradutor usa a codificação UTF-8, então letras acentuadas, símbolos e emojis também são convertidos corretamente. Nesses casos, um único caractere pode ocupar mais de um grupo de 8 bits.

## Entendendo os termos

- **Código binário:** sistema de numeração que usa apenas dois dígitos, 0 e 1, para representar qualquer informação em computadores.
- **Bit:** a menor unidade de informação digital, que pode valer 0 ou 1.
- **Byte:** conjunto de 8 bits. Cada byte pode representar um valor de 0 a 255.
- **Codificar:** transformar um texto legível em outra representação, neste caso uma sequência de bits.
- **Decodificar:** fazer o caminho inverso, transformando o código binário de volta em texto legível.
- **Caractere:** cada letra, número, símbolo ou espaço de um texto.
- **ASCII:** tabela clássica que associa 128 caracteres básicos (letras sem acento, números e sinais) a números de 0 a 127.
- **UTF-8:** padrão de codificação que inclui todo o ASCII e também acentos, símbolos e emojis, usando de 1 a 4 bytes por caractere.
- **Texto binário:** o resultado da codificação, formado por grupos de 8 dígitos como `01001111`.