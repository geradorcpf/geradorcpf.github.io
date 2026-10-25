---
title: "Conversão de Base Numérica"
seoTitle: "Conversão de Base Numérica"
description: "Conversão de Base Numérica: converta números entre binário, decimal e hexadecimal. Grátis e online, sem cadastro."
summary: "Converta números entre binário, decimal e hexadecimal."
date: 2026-10-25
draft: false
category: "dev"
tags: ["binário", "hexadecimal", "conversão", "matemática", "desenvolvimento"]
keywords: ["conversão de base numérica", "conversão de base numérica online", "binário", "hexadecimal", "conversão"]
---

<!--sudah dikerjakan-->


Basta digitar um número em qualquer um dos campos abaixo e os outros são convertidos na hora.

<div id="calc-base-numerica" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔢 Conversão de Base Numérica</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite em qualquer campo e veja a conversão na hora.</p>
<label for="bn-dec" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Decimal (base 10)</label>
<input id="bn-dec" type="text" inputmode="numeric" placeholder="Ex.: 255" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="bn-bin" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Binário (base 2)</label>
<input id="bn-bin" type="text" inputmode="numeric" placeholder="Ex.: 11111111" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="bn-oct" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Octal (base 8)</label>
<input id="bn-oct" type="text" inputmode="numeric" placeholder="Ex.: 377" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="bn-hex" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Hexadecimal (base 16)</label>
<input id="bn-hex" type="text" inputmode="text" placeholder="Ex.: FF" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="bn-limpar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Limpar</button>
</div>
<div id="bn-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-all;"><strong style="color:#3730a3;">Resposta:</strong> <span id="bn-resultado">digite um número em qualquer um dos campos.</span></div>
</div>
<script>
(function () {
  var padrao = 'digite um número em qualquer um dos campos.';
  var resultado = document.getElementById('bn-resultado');
  var caixa = document.getElementById('bn-resposta');
  var campos = {
    dec: { el: document.getElementById('bn-dec'), base: 10, nome: 'decimal', rx: /^[0-9]+$/, pre: '', dica: 'os dígitos de 0 a 9' },
    bin: { el: document.getElementById('bn-bin'), base: 2, nome: 'binário', rx: /^[01]+$/, pre: '0b', dica: 'os dígitos 0 e 1' },
    oct: { el: document.getElementById('bn-oct'), base: 8, nome: 'octal', rx: /^[0-7]+$/, pre: '0o', dica: 'os dígitos de 0 a 7' },
    hex: { el: document.getElementById('bn-hex'), base: 16, nome: 'hexadecimal', rx: /^[0-9a-fA-F]+$/, pre: '0x', dica: 'os dígitos de 0 a 9 e as letras de A a F' }
  };
  var ordem = ['dec', 'bin', 'oct', 'hex'];
  function normalizar(v) {
    return String(v).trim().replace(/[\s_]/g, '');
  }
  function lerNumero(texto, chave) {
    var c = campos[chave];
    var negativo = texto.charAt(0) === '-';
    var corpo = negativo ? texto.slice(1) : texto;
    if (c.pre !== '') {
      if (corpo.slice(0, 2).toLowerCase() === c.pre) { corpo = corpo.slice(2); }
    }
    if (corpo === '') { return null; }
    if (!c.rx.test(corpo)) { return null; }
    var n = BigInt(c.pre + corpo);
    return negativo ? -n : n;
  }
  function formatar(n, chave) {
    var t = n.toString(campos[chave].base);
    return chave === 'hex' ? t.toUpperCase() : t;
  }
  function estadoPadrao() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function sucesso(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = msg;
  }
  function limparOutros(origem) {
    ordem.forEach(function (k) {
      if (k !== origem) { campos[k].el.value = ''; }
    });
  }
  function atualizar(origem) {
    if (typeof BigInt === 'undefined') {
      erro('seu navegador não suporta este conversor. Atualize o navegador e tente novamente.');
      return;
    }
    var texto = normalizar(campos[origem].el.value);
    if (texto === '' || texto === '-') {
      limparOutros(origem);
      estadoPadrao();
      return;
    }
    var n = lerNumero(texto, origem);
    if (n === null) {
      limparOutros(origem);
      erro('valor inválido para ' + campos[origem].nome + '. Use apenas ' + campos[origem].dica + '.');
      return;
    }
    ordem.forEach(function (k) {
      if (k !== origem) { campos[k].el.value = formatar(n, k); }
    });
    sucesso(formatar(n, 'dec') + ' (decimal) = ' + formatar(n, 'bin') + ' (binário) = ' + formatar(n, 'oct') + ' (octal) = ' + formatar(n, 'hex') + ' (hexadecimal)');
  }
  function limpar() {
    ordem.forEach(function (k) { campos[k].el.value = ''; });
    estadoPadrao();
    campos.dec.el.focus();
  }
  ordem.forEach(function (k) {
    var el = campos[k].el;
    el.addEventListener('input', function () { atualizar(k); });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  document.getElementById('bn-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o conversor

1. Escolha o campo da base em que você já tem o número: **Decimal**, **Binário**, **Octal** ou **Hexadecimal**.
2. Digite o número nesse campo. Os outros três campos são preenchidos automaticamente enquanto você digita.
3. Confira o resumo da conversão na caixa **Resposta**, que mostra o mesmo valor nas quatro bases.
4. Use o botão **Limpar** para apagar todos os campos e fazer uma nova conversão.

Cada campo aceita apenas os dígitos da sua base: o binário aceita 0 e 1, o octal aceita de 0 a 7, o decimal aceita de 0 a 9 e o hexadecimal aceita de 0 a 9 e as letras de A a F (maiúsculas ou minúsculas). Também é possível digitar um sinal de menos para números negativos, usar os prefixos `0b`, `0o` e `0x`, e separar os dígitos com espaços ou underscores (por exemplo, `1111 1111`). Se aparecer uma mensagem em vermelho, revise os dígitos digitados.

## Entendendo os termos

- **Base numérica:** quantidade de símbolos diferentes usados para escrever os números em um sistema de numeração. Também é chamada de sistema de numeração.
- **Decimal (base 10):** sistema usado no dia a dia, com os dígitos de 0 a 9.
- **Binário (base 2):** sistema com apenas os dígitos 0 e 1, usado internamente por computadores e circuitos digitais.
- **Octal (base 8):** sistema com os dígitos de 0 a 7. Cada dígito octal equivale a 3 dígitos binários.
- **Hexadecimal (base 16):** sistema com os dígitos de 0 a 9 e as letras de A a F, em que A vale 10 e F vale 15. Cada dígito hexadecimal equivale a 4 dígitos binários e é muito usado em cores, endereços de memória e programação.
- **Dígito:** cada símbolo individual de um número. O valor de um dígito depende da sua posição.
- **Bit:** menor unidade de informação de um computador, com valor 0 ou 1. Um conjunto de 8 bits forma um byte.
- **Prefixo:** marca no início do número que indica sua base, como `0b` para binário, `0o` para octal e `0x` para hexadecimal.
- **Conversão de base:** processo de escrever o mesmo valor em outra base numérica, sem mudar a quantidade que ele representa.