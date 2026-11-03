---
title: "Gerador de UUID"
seoTitle: "Gerador de UUID"
description: "Gerador de UUID: gere UUIDs v4 prontos para copiar. Grátis e online, sem cadastro."
summary: "Gere UUIDs v4 prontos para copiar."
date: 2026-11-03
draft: false
category: "dev"
tags: ["uuid", "identificadores", "desenvolvimento", "dados de teste"]
keywords: ["gerador de uuid", "gerador de uuid online", "uuid", "identificadores", "desenvolvimento"]
---

Escolha a versão do UUID, informe a quantidade e clique em **Gerar UUIDs**. Depois é só copiar o resultado.

<div id="gerador-uuid" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔑 Gerador de UUID</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a versão e a quantidade e gere na hora.</p>
<label for="uuid-versao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Versão do UUID</label>
<select id="uuid-versao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="v4">UUID v4 (aleatório)</option>
<option value="v7">UUID v7 (timestamp + aleatório)</option>
<option value="v1">UUID v1 (timestamp + nó)</option>
</select>
<label for="uuid-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade (1 a 100)</label>
<input id="uuid-quantidade" type="text" inputmode="numeric" value="1" placeholder="Ex.: 5" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="uuid-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar UUIDs</button>
<button type="button" id="uuid-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="uuid-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">UUIDs gerados:</strong>
<div id="uuid-resultado" style="margin-top:8px;max-height:260px;overflow:auto;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:0.9rem;white-space:pre-wrap;word-break:break-all;">clique em "Gerar UUIDs".</div></div>
</div>
<script>
(function () {
  var versao = document.getElementById('uuid-versao');
  var qtd = document.getElementById('uuid-quantidade');
  var resultado = document.getElementById('uuid-resultado');
  var caixa = document.getElementById('uuid-resposta');
  var btnCopiar = document.getElementById('uuid-copiar');
  var lista = [];
  function bytes(n) {
    var a = new Uint8Array(n);
    crypto.getRandomValues(a);
    return a;
  }
  function toHex(arr) {
    var s = '';
    for (var i = 0; i !== arr.length; i++) { s += ('0' + arr[i].toString(16)).slice(-2); }
    return s;
  }
  function fmtId(h) {
    return h.slice(0, 8) + '-' + h.slice(8, 12) + '-' + h.slice(12, 16) + '-' + h.slice(16, 20) + '-' + h.slice(20, 32);
  }
  function gerarV4() {
    var b = bytes(16);
    b[6] = b[6] % 16 + 64;
    b[8] = b[8] % 64 + 128;
    return fmtId(toHex(b));
  }
  var ultimoTs = 0;
  function gerarV7() {
    var ts = Date.now();
    ts = ts > ultimoTs ? ts : ultimoTs + 1;
    ultimoTs = ts;
    var r = bytes(10);
    r[0] = r[0] % 16 + 112;
    r[2] = r[2] % 64 + 128;
    var tsHex = ts.toString(16);
    while (tsHex.length !== 12) { tsHex = '0' + tsHex; }
    return fmtId(tsHex + toHex(r));
  }
  function gerarV1(indice, clock, node) {
    var ms = Date.now() + 12219292800000;
    var t = BigInt(ms) * BigInt(10000) + BigInt(indice);
    var h = t.toString(16);
    while (h.length !== 15) { h = '0' + h; }
    var baixo = h.slice(7);
    var meio = h.slice(3, 7);
    var alto = '1' + h.slice(0, 3);
    return baixo + '-' + meio + '-' + alto + '-' + clock + '-' + node;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
    lista = [];
  }
  function gerar() {
    var n = parseInt(String(qtd.value).trim(), 10);
    if (isNaN(n) || n > 100 || 1 > n) { erro('informe uma quantidade inteira entre 1 e 100.'); return; }
    var v = versao.value;
    var saida = [];
    var clock = '';
    var node = '';
    if (v === 'v1') {
      var c = bytes(2);
      c[0] = c[0] % 64 + 128;
      clock = toHex(c);
      var nd = bytes(6);
      nd[0] = nd[0] % 128 * 2 + 1;
      node = toHex(nd);
    }
    for (var i = 0; i !== n; i++) {
      if (v === 'v7') { saida.push(gerarV7()); }
      else if (v === 'v1') { saida.push(gerarV1(i, clock, node)); }
      else { saida.push(gerarV4()); }
    }
    lista = saida;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = saida.join('\n');
  }
  function copiar() {
    if (lista.length === 0) { erro('gere pelo menos um UUID antes de copiar.'); return; }
    var texto = lista.join('\n');
    function feito() {
      btnCopiar.textContent = 'Copiado!';
      setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
    }
    function alternativa() {
      var ta = document.createElement('textarea');
      ta.value = texto;
      ta.style.position = 'fixed';
      ta.style.opacity = '0';
      document.body.appendChild(ta);
      ta.select();
      try { document.execCommand('copy'); feito(); } catch (e) { erro('não foi possível copiar automaticamente.'); }
      document.body.removeChild(ta);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(feito, alternativa);
    } else {
      alternativa();
    }
  }
  document.getElementById('uuid-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  [versao, qtd].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  gerar();
})();
</script>

## Como usar o gerador

1. Escolha a **Versão do UUID** no primeiro campo: v4, v7 ou v1.
2. Informe a **Quantidade** de UUIDs que você quer gerar (de 1 a 100).
3. Clique em **Gerar UUIDs** (ou pressione Enter) para ver o resultado.
4. Clique em **Copiar** para levar todos os UUIDs para a área de transferência, um por linha.

Cada clique em **Gerar UUIDs** cria valores novos. Os UUIDs são gerados no seu navegador, usando números aleatórios seguros, e nada é enviado para servidores. Na dúvida sobre qual versão escolher, use a v4.

## Entendendo os termos

- **UUID:** sigla de *Universally Unique Identifier*, um identificador de 128 bits escrito em 32 caracteres hexadecimais, separados por hífens no formato 8-4-4-4-12.
- **Versão do UUID:** indica como o UUID é construído (aleatório, baseado em tempo etc.). O número da versão aparece no primeiro caractere do terceiro bloco.
- **UUID v4 (aleatório):** gerado quase todo com números aleatórios. É a versão mais comum e atende à maioria dos casos de uso.
- **UUID v7 (timestamp + aleatório):** começa com a data e a hora em milissegundos e termina com dados aleatórios. Por isso, os valores podem ser ordenados pela ordem de criação.
- **UUID v1 (timestamp + nó):** baseado na data e hora e em um identificador do dispositivo. Aqui, o identificador é aleatório, para não expor dados da sua máquina.
- **Timestamp:** marca de tempo, ou seja, o momento exato em que o UUID foi criado.
- **Endereço MAC:** número que identifica a placa de rede de um dispositivo. A v1 original o utiliza, o que pode revelar informações do sistema.
- **Número pseudoaleatório criptograficamente seguro:** número aleatório gerado por um método difícil de prever, adequado para identificadores.
- **Unicidade:** característica de não se repetir. A chance de dois UUIDs v4 iguais é tão pequena que, na prática, é desconsiderada.
- **Chave primária:** coluna de um banco de dados que identifica cada registro de forma única. UUIDs são muito usados nesse papel.
- **Quantidade:** número de UUIDs gerados de uma só vez, de 1 a 100.

## Quando usar cada versão

- **v4:** uso geral, APIs REST e identificadores únicos sem requisitos especiais.
- **v7:** chaves primárias em bancos de dados, logs ordenados e sistemas distribuídos.
- **v1:** sistemas antigos ou casos em que a compatibilidade com a v1 é necessária.

## Exemplo de UUID v4

Um UUID v4 tem este formato:

**47ae6475-66e7-4713-ae54-8aaa5e65bb2f**

O número **4** no início do terceiro bloco (**4713**) indica a versão. O primeiro caractere do quarto bloco (**a**) indica a variante do padrão. Todo o restante é aleatório.