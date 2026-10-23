---
title: "Calcular CRC32"
seoTitle: "Calcular CRC32"
description: "Calcular CRC32: calcule o checksum CRC32 de um texto. Grátis e online, sem cadastro."
summary: "Calcule o checksum CRC32 de um texto."
date: 2026-10-23    
draft: false
category: "dev"
tags: ["hash", "crc32", "checksum", "desenvolvimento"]
keywords: ["calcular crc32", "calcular crc32 online", "hash", "crc32", "checksum"]
---
<!--sudah dikerjakan-->

Basta digitar o texto abaixo e depois clicar em **Calcular CRC32**.

<div id="calc-crc32" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔐 Calcular CRC32</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto e veja o checksum CRC32 na hora.</p>
<label for="crc-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o texto</label>
<textarea id="crc-texto" rows="4" placeholder="Ex.: 123456789" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="crc-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular CRC32</button>
<button type="button" id="crc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="crc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-all;"><strong style="color:#3730a3;">Resposta:</strong> <span id="crc-resultado">digite o texto e clique em "Calcular CRC32".</span></div>
</div>
<script>
(function () {
  var texto = document.getElementById('crc-texto');
  var resultado = document.getElementById('crc-resultado');
  var caixa = document.getElementById('crc-resposta');
  var MOD = 4294967296;
  function xor32(a, b) { return ((a ^ b) + MOD) % MOD; }
  var tabela = [];
  (function () {
    for (var n = 0; n !== 256; n++) {
      var c = n;
      for (var k = 0; k !== 8; k++) {
        c = (c % 2 === 1) ? xor32(3988292384, Math.floor(c / 2)) : Math.floor(c / 2);
      }
      tabela.push(c);
    }
  })();
  function crc32(bytes) {
    var crc = MOD - 1;
    for (var i = 0; i !== bytes.length; i++) {
      crc = xor32(tabela[xor32(crc, bytes[i]) % 256], Math.floor(crc / 256));
    }
    return xor32(crc, MOD - 1);
  }
  function linha(rotulo, valor) {
    var div = document.createElement('div');
    var forte = document.createElement('strong');
    forte.style.color = '#166534';
    forte.textContent = rotulo + ': ';
    var span = document.createElement('span');
    span.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    span.style.fontSize = '1.1rem';
    span.textContent = valor;
    div.appendChild(forte);
    div.appendChild(span);
    return div;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var valor = texto.value;
    if (valor === '') { erro('digite um texto para calcular o CRC32.'); return; }
    var bytes = new TextEncoder().encode(valor);
    var soma = crc32(bytes);
    var hex = ('00000000' + soma.toString(16).toUpperCase()).slice(-8);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(linha('Hexadecimal', hex));
    resultado.appendChild(linha('Decimal', String(soma)));
  }
  function limpar() {
    texto.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'digite o texto e clique em "Calcular CRC32".';
    texto.focus();
  }
  document.getElementById('crc-calcular').addEventListener('click', calcular);
  document.getElementById('crc-limpar').addEventListener('click', limpar);
  texto.addEventListener('keydown', function (e) { if (e.key === 'Enter') { if (e.ctrlKey || e.metaKey) { calcular(); } } });
  texto.addEventListener('focus', function () { texto.style.borderColor = '#6366f1'; });
  texto.addEventListener('blur', function () { texto.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o **texto** que você quer verificar no campo acima.
2. Clique em **Calcular CRC32** (ou pressione Ctrl + Enter) para ver o resultado.
3. Confira o checksum na caixa **Resposta**, nos formatos **hexadecimal** e **decimal**.
4. Use o botão **Limpar** para apagar o texto e fazer um novo cálculo.

O cálculo considera cada caractere, inclusive espaços e quebras de linha, e usa a codificação UTF-8. Qualquer diferença no texto, mesmo de uma única letra ou de maiúscula para minúscula, gera um CRC32 diferente.

## Entendendo os termos

- **CRC32:** sigla de *Cyclic Redundancy Check* de 32 bits. É um código de 32 bits calculado a partir de um conjunto de dados.
- **Checksum:** valor curto calculado a partir de um dado, usado para conferir se ele chegou ou foi guardado sem alterações.
- **Verificação de redundância cíclica:** método matemático baseado em divisão de polinômios que detecta erros acidentais em dados.
- **Hash:** resultado de uma função que transforma qualquer texto em um valor de tamanho fixo. O CRC32 serve para detectar erros, não para segurança, e não substitui hashes criptográficos como MD5 ou SHA-1.
- **Hexadecimal:** sistema de numeração de base 16, com os dígitos de 0 a 9 e as letras de A a F. O CRC32 costuma ser mostrado com 8 dígitos hexadecimais.
- **Decimal:** o mesmo valor do CRC32 escrito como um número comum, de 0 a 4.294.967.295.
- **UTF-8:** codificação que transforma os caracteres do texto em bytes antes do cálculo. Textos com acentos geram bytes diferentes dos textos sem acentos.
- **Byte:** unidade de 8 bits. O CRC32 é calculado byte a byte sobre o texto.