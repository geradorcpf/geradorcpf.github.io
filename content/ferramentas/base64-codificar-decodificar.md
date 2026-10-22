---
title: "Base64 Decodificar e Codificar"
seoTitle: "Base64 Decodificar e Codificar"
description: "Base64 Decodificar e Codificar: codifique texto em Base64 ou decodifique de volta. Grátis e online, sem cadastro."
summary: "Codifique texto em Base64 ou decodifique de volta."
date: 2026-10-22
draft: false
category: "dev"
tags: ["base64", "codificação", "desenvolvimento", "texto"]
keywords: ["base64 decodificar e codificar", "base64 decodificar e codificar online", "base64", "codificação", "desenvolvimento"]
---

<!--SUDAH DIKERJAKAN-->

Basta digitar o código Base64 ou o texto nos campos abaixo e depois clicar em **Converter para Texto** ou **Converter para Base64**.

<div id="calc-base64" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔐 Base64 Decodificar e Codificar</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Converta código Base64 em texto ou texto em Base64 na hora.</p>
<h3 style="margin:0 0 4px;font-size:1.05rem;color:#3730a3;">Decodificar: Base64 para texto</h3>
<p style="margin:0 0 12px;font-size:0.9rem;color:#64748b;">Digite o código que quer decifrar.</p>
<label for="b64-dec-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código Base64</label>
<textarea id="b64-dec-entrada" rows="4" placeholder="Ex.: T2zDoSwgbXVuZG8h" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="b64-dec-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para Texto</button>
<button type="button" id="b64-dec-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="b64-dec-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta Decodificada:</strong> <span id="b64-dec-resultado" style="white-space:pre-wrap;word-break:break-all;">preencha o campo e clique em "Converter para Texto".</span></div>
<hr style="margin:28px 0;border:none;border-top:1px solid #c7d2fe;">
<h3 style="margin:0 0 4px;font-size:1.05rem;color:#3730a3;">Codificar: texto para Base64</h3>
<p style="margin:0 0 12px;font-size:0.9rem;color:#64748b;">Digite o texto que quer converter para Base64.</p>
<label for="b64-cod-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="b64-cod-entrada" rows="4" placeholder="Ex.: Olá, mundo!" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="b64-cod-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para Base64</button>
<button type="button" id="b64-cod-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="b64-cod-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta Codificada:</strong> <span id="b64-cod-resultado" style="white-space:pre-wrap;word-break:break-all;">preencha o campo e clique em "Converter para Base64".</span></div>
</div>
<script>
(function () {
  var MSG_DEC = 'preencha o campo e clique em "Converter para Texto".';
  var MSG_COD = 'preencha o campo e clique em "Converter para Base64".';
  var decEntrada = document.getElementById('b64-dec-entrada');
  var decResultado = document.getElementById('b64-dec-resultado');
  var decCaixa = document.getElementById('b64-dec-resposta');
  var codEntrada = document.getElementById('b64-cod-entrada');
  var codResultado = document.getElementById('b64-cod-resultado');
  var codCaixa = document.getElementById('b64-cod-resposta');
  function estado(caixa, resultado, tipo, msg) {
    var cores = {
      ok: ['#86efac', '#f0fdf4', '#166534'],
      erro: ['#fca5a5', '#fef2f2', '#b91c1c'],
      neutro: ['#c7d2fe', '#ffffff', '#64748b']
    }[tipo];
    caixa.style.borderColor = cores[0];
    caixa.style.background = cores[1];
    resultado.style.color = cores[2];
    resultado.textContent = msg;
  }
  function paraBase64(texto) {
    var bytes = new TextEncoder().encode(texto);
    var bin = '';
    for (var i = 0; i < bytes.length; i++) { bin += String.fromCharCode(bytes[i]); }
    return btoa(bin);
  }
  function deBase64(codigo) {
    var t = codigo.replace(/\s/g, '').replace(/-/g, '+').replace(/_/g, '/');
    while (t.length % 4) { t += '='; }
    var bin = atob(t);
    var bytes = new Uint8Array(bin.length);
    for (var i = 0; i < bin.length; i++) { bytes[i] = bin.charCodeAt(i); }
    return new TextDecoder('utf-8', { fatal: true }).decode(bytes);
  }
  function decodificar() {
    var valor = decEntrada.value;
    if (valor.trim() === '') { estado(decCaixa, decResultado, 'erro', 'informe o código Base64 que deseja decodificar.'); return; }
    try {
      estado(decCaixa, decResultado, 'ok', deBase64(valor));
    } catch (e) {
      estado(decCaixa, decResultado, 'erro', 'código Base64 inválido. Verifique se o código foi digitado corretamente.');
    }
  }
  function codificar() {
    var valor = codEntrada.value;
    if (valor === '') { estado(codCaixa, codResultado, 'erro', 'informe o texto que deseja codificar.'); return; }
    try {
      estado(codCaixa, codResultado, 'ok', paraBase64(valor));
    } catch (e) {
      estado(codCaixa, codResultado, 'erro', 'não foi possível codificar este texto.');
    }
  }
  function limparDec() {
    decEntrada.value = '';
    estado(decCaixa, decResultado, 'neutro', MSG_DEC);
    decEntrada.focus();
  }
  function limparCod() {
    codEntrada.value = '';
    estado(codCaixa, codResultado, 'neutro', MSG_COD);
    codEntrada.focus();
  }
  document.getElementById('b64-dec-converter').addEventListener('click', decodificar);
  document.getElementById('b64-cod-converter').addEventListener('click', codificar);
  document.getElementById('b64-dec-limpar').addEventListener('click', limparDec);
  document.getElementById('b64-cod-limpar').addEventListener('click', limparCod);
  [[decEntrada, decodificar], [codEntrada, codificar]].forEach(function (par) {
    var el = par[0];
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { par[1](); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

Para **decodificar** (Base64 para texto):

1. Cole ou digite o código no campo **Código Base64**.
2. Clique em **Converter para Texto** (ou pressione Ctrl + Enter).
3. Confira o texto original em **Resposta Decodificada**.

Para **codificar** (texto para Base64):

1. Digite ou cole o conteúdo no campo **Texto**.
2. Clique em **Converter para Base64** (ou pressione Ctrl + Enter).
3. Confira o código gerado em **Resposta Codificada**.

Use o botão **Limpar** de cada bloco para apagar o campo e fazer uma nova conversão. A ferramenta aceita acentos e caracteres especiais (UTF-8), e a conversão acontece no seu navegador, sem enviar nada para a internet.

## Entendendo os termos

- **Base64:** método de codificação que representa dados usando apenas 64 caracteres (letras, números, `+` e `/`), o que permite transmitir o conteúdo com segurança por meios que aceitam só texto.
- **Codificar (encode):** transformar um texto comum em código Base64.
- **Decodificar (decode):** converter um código Base64 de volta para o texto original.
- **Texto:** conteúdo legível que você quer converter, como uma frase, um nome ou um trecho de código.
- **Código Base64:** sequência de caracteres gerada pela codificação, muitas vezes terminada em um ou dois sinais de `=`.
- **Padding (`=`):** sinal de igual no final do código, usado para completar o tamanho correto da sequência.
- **UTF-8:** padrão de caracteres que permite representar acentos, símbolos e emojis corretamente na conversão.
- **Resposta Decodificada / Resposta Codificada:** áreas onde aparece o resultado de cada conversão.
- **Base64 não é criptografia:** qualquer pessoa pode decodificar o código, portanto não use Base64 para proteger senhas ou dados sensíveis.