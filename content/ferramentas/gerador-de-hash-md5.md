---
title: "Gerador de Hash MD5"
seoTitle: "Gerador de Hash MD5"
description: "Gerador de Hash MD5: gere o hash MD5 de um texto. Grátis e online, sem cadastro."
summary: "Gere o hash MD5 de um texto."
date: 2026-10-30
draft: false
category: "dev"
tags: ["hash", "md5", "criptografia", "desenvolvimento"]
keywords: ["gerador de hash md5", "gerador de hash md5 online", "hash", "md5", "criptografia"]
---

Basta digitar o texto abaixo e depois clicar em **Codificar MD5**.

<div id="calc-md5" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔐 Gerador de Hash MD5</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite um texto e veja o hash MD5 na hora.</p>
<label for="md5-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite seu texto</label>
<textarea id="md5-texto" rows="4" placeholder="Ex.: Olá, mundo!" autocomplete="off" spellcheck="false" style="width:100%;min-height:110px;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="md5-codificar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Codificar MD5</button>
<button type="button" id="md5-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="md5-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="md5-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="md5-resultado" style="word-break:break-all;">digite um texto e clique em "Codificar MD5".</span></div>
</div>
<script>
(function () {
  var texto = document.getElementById('md5-texto');
  var resultado = document.getElementById('md5-resultado');
  var caixa = document.getElementById('md5-resposta');
  var hashAtual = '';
  var SHIFT = [7, 12, 17, 22, 5, 9, 14, 20, 4, 11, 16, 23, 6, 10, 15, 21];
  var K = [];
  var n;
  for (n = 0; 64 > n; n++) { K[n] = Math.floor(Math.abs(Math.sin(n + 1)) * 4294967296); }
  function rotl(x, c) { return Math.imul(x, Math.pow(2, c)) | (x >>> (32 - c)); }
  function md5(bytes) {
    var len = bytes.length;
    var total = (Math.floor((len + 8) / 64) + 1) * 64;
    var buf = new Uint8Array(total);
    var i, j, o, p;
    buf.set(bytes);
    buf[len] = 128;
    var bitsLow = (len * 8) % 4294967296;
    var bitsHigh = Math.floor((len * 8) / 4294967296);
    for (i = 0; 4 > i; i++) {
      buf[total - 8 + i] = (bitsLow >>> (8 * i)) & 255;
      buf[total - 4 + i] = (bitsHigh >>> (8 * i)) & 255;
    }
    var a0 = 1732584193, b0 = -271733879, c0 = -1732584194, d0 = 271733878;
    for (o = 0; total > o; o += 64) {
      var M = [];
      for (j = 0; 16 > j; j++) {
        p = o + j * 4;
        M[j] = buf[p] | (buf[p + 1] * 256) | (buf[p + 2] * 65536) | (buf[p + 3] * 16777216);
      }
      var A = a0, B = b0, C = c0, D = d0, F, g;
      for (i = 0; 64 > i; i++) {
        if (16 > i) { F = (B & C) | (~B & D); g = i; }
        else if (32 > i) { F = (D & B) | (~D & C); g = (5 * i + 1) % 16; }
        else if (48 > i) { F = B ^ C ^ D; g = (3 * i + 5) % 16; }
        else { F = C ^ (B | ~D); g = (7 * i) % 16; }
        F = (F + A + K[i] + M[g]) | 0;
        A = D;
        D = C;
        C = B;
        B = (B + rotl(F, SHIFT[(i >>> 4) * 4 + (i % 4)])) | 0;
      }
      a0 = (a0 + A) | 0;
      b0 = (b0 + B) | 0;
      c0 = (c0 + C) | 0;
      d0 = (d0 + D) | 0;
    }
    var out = '';
    var words = [a0, b0, c0, d0];
    for (i = 0; 4 > i; i++) {
      for (j = 0; 4 > j; j++) {
        out += (((words[i] >>> (8 * j)) & 255) + 256).toString(16).slice(1);
      }
    }
    return out;
  }
  function erro(msg) {
    hashAtual = '';
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.style.fontFamily = 'inherit';
    resultado.textContent = msg;
  }
  function codificar() {
    var valor = texto.value;
    if (valor === '') { erro('digite um texto para gerar o hash.'); return; }
    hashAtual = md5(new TextEncoder().encode(valor));
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    resultado.textContent = hashAtual;
  }
  function copiar() {
    var botao = document.getElementById('md5-copiar');
    if (hashAtual === '') { erro('gere um hash antes de copiar.'); return; }
    function ok() {
      botao.textContent = 'Copiado!';
      setTimeout(function () { botao.textContent = 'Copiar'; }, 1500);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(hashAtual).then(ok, function () {});
    }
  }
  function limpar() {
    texto.value = '';
    hashAtual = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontFamily = 'inherit';
    resultado.textContent = 'digite um texto e clique em "Codificar MD5".';
    texto.focus();
  }
  document.getElementById('md5-codificar').addEventListener('click', codificar);
  document.getElementById('md5-copiar').addEventListener('click', copiar);
  document.getElementById('md5-limpar').addEventListener('click', limpar);
  texto.addEventListener('keydown', function (e) { if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { codificar(); } });
  texto.addEventListener('focus', function () { texto.style.borderColor = '#6366f1'; });
  texto.addEventListener('blur', function () { texto.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Digite ou cole o texto que você quer codificar no campo **Digite seu texto**.
2. Clique em **Codificar MD5** (ou pressione Ctrl + Enter) para gerar o hash.
3. Confira o resultado no quadro **Resposta**, logo abaixo dos botões.
4. Clique em **Copiar** para copiar o hash para a área de transferência.
5. Use o botão **Limpar** para apagar o texto e fazer uma nova codificação.

O mesmo texto sempre gera o mesmo hash. Qualquer mudança, até de uma letra maiúscula, espaço ou acento, gera um hash completamente diferente. Tudo é calculado no seu navegador: o texto digitado não é enviado a nenhum servidor.

## Entendendo os termos

- **MD5:** sigla de Message-Digest Algorithm 5, algoritmo que transforma qualquer texto em uma sequência fixa de 32 caracteres hexadecimais.
- **Hash:** "impressão digital" de um texto, ou seja, o resultado do algoritmo. Textos iguais geram hashes iguais.
- **Codificar:** processo de converter o texto digitado em seu hash MD5. É um caminho de mão única: não é possível recuperar o texto original a partir do hash.
- **Hexadecimal:** sistema de numeração que usa os dígitos de 0 a 9 e as letras de a até f. O hash MD5 é escrito nesse formato.
- **Criptografia:** área que estuda técnicas para proteger e verificar informações. O MD5 faz parte dela, mas hoje não é recomendado para proteger senhas.
- **Integridade:** garantia de que um dado não foi alterado. Comparar o hash MD5 de dois arquivos ou textos é uma forma simples de verificar isso.
- **UTF-8:** padrão de codificação de caracteres usado pelo gerador, que garante o mesmo hash para textos com acentos e símbolos, como "ação" ou "😀".