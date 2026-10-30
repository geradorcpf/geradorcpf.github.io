---
title: "Gerador de Hash SHA1"
seoTitle: "Gerador de Hash SHA1"
description: "Gerador de Hash SHA1: gere o hash SHA1 de um texto. Grátis e online, sem cadastro."
summary: "Gere o hash SHA1 de um texto."
date: 2026-10-30
draft: false
category: "dev"
tags: ["hash", "sha1", "criptografia", "desenvolvimento"]
keywords: ["gerador de hash sha1", "gerador de hash sha1 online", "hash", "sha1", "criptografia"]
---

Basta digitar o texto abaixo e depois clicar em **Codificar SHA1**.

<div id="calc-sha1" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔐 Gerador de Hash SHA1</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto e veja o hash na hora.</p>
<label for="sha-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite seu texto</label>
<textarea id="sha-texto" rows="4" placeholder="Ex.: abc" autocomplete="off" spellcheck="false" style="width:100%;min-height:110px;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sha-codificar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Codificar SHA1</button>
<button type="button" id="sha-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="sha-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sha-resultado" style="word-break:break-all;">digite um texto e clique em "Codificar SHA1".</span></div>
</div>
<script>
(function () {
  var texto = document.getElementById('sha-texto');
  var resultado = document.getElementById('sha-resultado');
  var caixa = document.getElementById('sha-resposta');
  var MENSAGEM_INICIAL = 'digite um texto e clique em "Codificar SHA1".';
  function lsl(x, n) { return Math.imul(x, Math.pow(2, n)); }
  function rotl(x, n) { return lsl(x, n) | (x >>> (32 - n)); }
  function paraBytes(s) {
    if (typeof TextEncoder !== 'undefined') { return new TextEncoder().encode(s); }
    var bin = unescape(encodeURIComponent(s));
    var out = new Uint8Array(bin.length);
    for (var i = 0; i !== bin.length; i++) { out[i] = bin.charCodeAt(i); }
    return out;
  }
  function hex8(n) { return ('00000000' + (n >>> 0).toString(16)).slice(-8); }
  function sha1(bytes) {
    var h0 = 0x67452301, h1 = 0xEFCDAB89 | 0, h2 = 0x98BADCFE | 0, h3 = 0x10325476, h4 = 0xC3D2E1F0 | 0;
    var len = bytes.length;
    var total = (((len + 8) >>> 6) + 1) * 64;
    var buf = new Uint8Array(total);
    buf.set(bytes);
    buf[len] = 0x80;
    var view = new DataView(buf.buffer);
    view.setUint32(total - 8, Math.floor(len / 536870912));
    view.setUint32(total - 4, (len % 536870912) * 8);
    var w = new Array(80);
    for (var off = 0; off !== total; off += 64) {
      for (var i = 0; i !== 16; i++) { w[i] = view.getUint32(off + i * 4); }
      for (var j = 16; j !== 80; j++) { w[j] = rotl(w[j - 3] ^ w[j - 8] ^ w[j - 14] ^ w[j - 16], 1); }
      var a = h0, b = h1, c = h2, d = h3, e = h4;
      for (var t = 0; t !== 80; t++) {
        var f, k, fase = Math.floor(t / 20);
        if (fase === 0) { f = (b & c) | (~b & d); k = 0x5A827999; }
        else if (fase === 1) { f = b ^ c ^ d; k = 0x6ED9EBA1; }
        else if (fase === 2) { f = (b & c) | (b & d) | (c & d); k = 0x8F1BBCDC | 0; }
        else { f = b ^ c ^ d; k = 0xCA62C1D6 | 0; }
        var temp = (rotl(a, 5) + f + e + k + w[t]) | 0;
        e = d; d = c; c = rotl(b, 30); b = a; a = temp;
      }
      h0 = (h0 + a) | 0; h1 = (h1 + b) | 0; h2 = (h2 + c) | 0; h3 = (h3 + d) | 0; h4 = (h4 + e) | 0;
    }
    return hex8(h0) + hex8(h1) + hex8(h2) + hex8(h3) + hex8(h4);
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.style.fontFamily = 'inherit';
    resultado.textContent = msg;
  }
  function codificar() {
    var valor = texto.value;
    if (valor === '') { erro('digite um texto para gerar o hash.'); return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    resultado.textContent = sha1(paraBytes(valor));
  }
  function limpar() {
    texto.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontFamily = 'inherit';
    resultado.textContent = MENSAGEM_INICIAL;
    texto.focus();
  }
  document.getElementById('sha-codificar').addEventListener('click', codificar);
  document.getElementById('sha-limpar').addEventListener('click', limpar);
  texto.addEventListener('keydown', function (e) { if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { codificar(); } });
  texto.addEventListener('focus', function () { texto.style.borderColor = '#6366f1'; });
  texto.addEventListener('blur', function () { texto.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o texto no campo **Digite seu texto**.
2. Clique em **Codificar SHA1** (ou pressione Ctrl + Enter) para gerar o hash.
3. Confira o resultado no quadro **Resposta**, logo abaixo dos botões.
4. Use o botão **Limpar** para apagar o texto e fazer uma nova codificação.

O hash SHA1 sempre tem 40 caracteres hexadecimais, não importa o tamanho do texto. Qualquer mudança no texto, mesmo uma letra maiúscula ou um espaço extra, gera um hash completamente diferente. O mesmo texto sempre gera o mesmo hash.

## Entendendo os termos

- **SHA1:** sigla de *Secure Hash Algorithm 1*, algoritmo que transforma qualquer texto em uma sequência fixa de 160 bits (40 caracteres hexadecimais).
- **Hash:** resultado do algoritmo, uma "impressão digital" do texto. Também é chamado de *digest* ou resumo.
- **Codificar (Encode):** processo de aplicar o algoritmo ao texto para obter o hash.
- **Texto de entrada:** o conteúdo digitado por você, que é processado para gerar o hash.
- **Hexadecimal:** sistema de numeração em base 16, que usa os dígitos de 0 a 9 e as letras de a a f. É o formato em que o hash é exibido.
- **Criptografia:** área que estuda técnicas para proteger e verificar informações. O SHA1 faz parte das funções de hash criptográficas.
- **Função de mão única:** característica do hash: é fácil gerar o hash a partir do texto, mas não é possível recuperar o texto original a partir do hash.
- **UTF-8:** padrão de codificação de caracteres usado para converter o texto em bytes antes do cálculo, o que permite usar acentos e símbolos.
- **Colisão:** situação em que dois textos diferentes geram o mesmo hash. No SHA1 já foram demonstradas colisões, por isso ele não é mais recomendado para segurança.
- **Checksum:** valor usado para conferir se um dado não foi alterado, como em arquivos baixados. O SHA1 ainda é usado com essa finalidade.

## Exemplo resolvido

Qual é o hash SHA1 do texto `abc`?

1. Digite `abc` no campo de texto.
2. Clique em **Codificar SHA1**.

**Resposta:** `a9993e364706816aba3e25717850c26c9cd0d89d`