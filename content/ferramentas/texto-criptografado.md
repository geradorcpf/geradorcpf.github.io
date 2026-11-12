---
title: "Texto Criptografado"
seoTitle: "Texto Criptografado"
description: "Texto Criptografado: criptografe e descriptografe mensagens com uma senha. Grátis e online, sem cadastro."
summary: "Criptografe e descriptografe mensagens com uma senha."
date: 2026-11-12
draft: false
category: "dev"
tags: ["criptografia", "segurança", "texto"]
keywords: ["texto criptografado", "texto criptografado online", "criptografia", "segurança", "texto"]
---

Escreva o texto e uma chave abaixo e clique em **Criptografar**. Para ler o texto depois, cole o código, digite a mesma chave e clique em **Descriptografar**.

<div id="calc-criptografia" style="max-width:560px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔐 Texto Criptografado</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Criptografe e descriptografe mensagens com uma chave. Tudo é feito no seu navegador.</p>
<label for="cri-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto para criptografar</label>
<textarea id="cri-texto" rows="4" placeholder="Ex.: minha mensagem secreta" autocomplete="off" style="width:100%;min-height:96px;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="cri-chave-enc" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Chave para criptografar</label>
<input id="cri-chave-enc" type="password" placeholder="Ex.: uma frase longa e difícil" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cri-criptografar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Criptografar</button>
<button type="button" id="cri-limpar-enc" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cri-resposta-enc" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cri-resultado-enc">preencha os campos e clique em "Criptografar".</span></div>
<label for="cri-codigo-gerado" style="display:block;margin:16px 0 6px;font-weight:600;font-size:0.95rem;">Código gerado</label>
<textarea id="cri-codigo-gerado" rows="3" readonly placeholder="O código criptografado aparece aqui." style="width:100%;min-height:78px;padding:12px 14px;margin-bottom:12px;font-size:0.9rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;word-break:break-all;"></textarea>
<button type="button" id="cri-copiar" style="padding:11px 18px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar código</button>
<hr style="margin:28px 0;border:none;border-top:1px solid #c7d2fe;">
<label for="cri-codigo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código para descriptografar</label>
<textarea id="cri-codigo" rows="3" placeholder="Cole aqui o código gerado." autocomplete="off" style="width:100%;min-height:78px;padding:12px 14px;margin-bottom:16px;font-size:0.9rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;word-break:break-all;"></textarea>
<label for="cri-chave-dec" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Chave para descriptografar</label>
<input id="cri-chave-dec" type="password" placeholder="Digite a mesma chave usada" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cri-descriptografar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Descriptografar</button>
<button type="button" id="cri-limpar-dec" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cri-resposta-dec" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-word;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cri-resultado-dec">cole o código, digite a chave e clique em "Descriptografar".</span></div>
</div>
<script>
(function () {
  var ITERACOES = 250000;
  var TAM_SALT = 16;
  var TAM_IV = 12;
  var TAM_TAG = 16;
  var codificador = new TextEncoder();
  var decodificador = new TextDecoder();
  function el(id) { return document.getElementById(id); }
  var texto = el('cri-texto');
  var chaveEnc = el('cri-chave-enc');
  var codigoGerado = el('cri-codigo-gerado');
  var codigo = el('cri-codigo');
  var chaveDec = el('cri-chave-dec');
  var caixaEnc = el('cri-resposta-enc');
  var resultadoEnc = el('cri-resultado-enc');
  var caixaDec = el('cri-resposta-dec');
  var resultadoDec = el('cri-resultado-dec');
  function temCripto() {
    return !!(window.crypto && window.crypto.subtle);
  }
  function mostrar(caixa, span, tipo, msg) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      span.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      span.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      span.style.color = '#64748b';
    }
    span.textContent = msg;
  }
  function paraBase64(bytes) {
    var s = '';
    bytes.forEach(function (b) { s += String.fromCharCode(b); });
    return btoa(s);
  }
  function deBase64(str) {
    var s = atob(str.replace(/\s/g, ''));
    var saida = new Uint8Array(s.length);
    for (var i = 0; i !== s.length; i++) { saida[i] = s.charCodeAt(i); }
    return saida;
  }
  function derivarChave(chave, salt) {
    return window.crypto.subtle.importKey('raw', codificador.encode(chave), 'PBKDF2', false, ['deriveKey']).then(function (base) {
      return window.crypto.subtle.deriveKey(
        { name: 'PBKDF2', salt: salt, iterations: ITERACOES, hash: 'SHA-256' },
        base,
        { name: 'AES-GCM', length: 256 },
        false,
        ['encrypt', 'decrypt']
      );
    });
  }
  function criptografar() {
    var t = texto.value;
    var c = chaveEnc.value;
    if (t === '') { mostrar(caixaEnc, resultadoEnc, 'erro', 'digite o texto que será criptografado.'); return; }
    if (c === '') { mostrar(caixaEnc, resultadoEnc, 'erro', 'digite uma chave para criptografar.'); return; }
    if (!temCripto()) { mostrar(caixaEnc, resultadoEnc, 'erro', 'seu navegador não oferece suporte à criptografia. Use uma versão atual com conexão segura (https).'); return; }
    var salt = window.crypto.getRandomValues(new Uint8Array(TAM_SALT));
    var iv = window.crypto.getRandomValues(new Uint8Array(TAM_IV));
    mostrar(caixaEnc, resultadoEnc, 'neutro', 'criptografando...');
    derivarChave(c, salt).then(function (chave) {
      return window.crypto.subtle.encrypt({ name: 'AES-GCM', iv: iv }, chave, codificador.encode(t));
    }).then(function (cifra) {
      var dados = new Uint8Array(TAM_SALT + TAM_IV + cifra.byteLength);
      dados.set(salt, 0);
      dados.set(iv, TAM_SALT);
      dados.set(new Uint8Array(cifra), TAM_SALT + TAM_IV);
      codigoGerado.value = paraBase64(dados);
      mostrar(caixaEnc, resultadoEnc, 'ok', 'texto criptografado! Copie o código abaixo e guarde a chave.');
    }).catch(function () {
      mostrar(caixaEnc, resultadoEnc, 'erro', 'não foi possível criptografar o texto.');
    });
  }
  function descriptografar() {
    var cod = codigo.value.trim();
    var c = chaveDec.value;
    if (cod === '') { mostrar(caixaDec, resultadoDec, 'erro', 'cole o código que será descriptografado.'); return; }
    if (c === '') { mostrar(caixaDec, resultadoDec, 'erro', 'digite a chave para descriptografar.'); return; }
    if (!temCripto()) { mostrar(caixaDec, resultadoDec, 'erro', 'seu navegador não oferece suporte à criptografia. Use uma versão atual com conexão segura (https).'); return; }
    var bytes;
    try {
      bytes = deBase64(cod);
    } catch (e) {
      mostrar(caixaDec, resultadoDec, 'erro', 'o código informado não é válido.');
      return;
    }
    if (!(bytes.length > TAM_SALT + TAM_IV + TAM_TAG)) {
      mostrar(caixaDec, resultadoDec, 'erro', 'o código informado não é válido.');
      return;
    }
    var salt = bytes.slice(0, TAM_SALT);
    var iv = bytes.slice(TAM_SALT, TAM_SALT + TAM_IV);
    var cifra = bytes.slice(TAM_SALT + TAM_IV);
    mostrar(caixaDec, resultadoDec, 'neutro', 'descriptografando...');
    derivarChave(c, salt).then(function (chave) {
      return window.crypto.subtle.decrypt({ name: 'AES-GCM', iv: iv }, chave, cifra);
    }).then(function (claro) {
      mostrar(caixaDec, resultadoDec, 'ok', decodificador.decode(claro));
    }).catch(function () {
      mostrar(caixaDec, resultadoDec, 'erro', 'chave incorreta ou código inválido.');
    });
  }
  function copiar() {
    var valor = codigoGerado.value;
    if (valor === '') { mostrar(caixaEnc, resultadoEnc, 'erro', 'gere um código antes de copiar.'); return; }
    function fallback() {
      codigoGerado.select();
      try { document.execCommand('copy'); mostrar(caixaEnc, resultadoEnc, 'ok', 'código copiado!'); } catch (e) { mostrar(caixaEnc, resultadoEnc, 'erro', 'não foi possível copiar. Copie manualmente.'); }
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(valor).then(function () {
        mostrar(caixaEnc, resultadoEnc, 'ok', 'código copiado!');
      }).catch(fallback);
    } else {
      fallback();
    }
  }
  function limparEnc() {
    texto.value = '';
    chaveEnc.value = '';
    codigoGerado.value = '';
    mostrar(caixaEnc, resultadoEnc, 'neutro', 'preencha os campos e clique em "Criptografar".');
    texto.focus();
  }
  function limparDec() {
    codigo.value = '';
    chaveDec.value = '';
    mostrar(caixaDec, resultadoDec, 'neutro', 'cole o código, digite a chave e clique em "Descriptografar".');
    codigo.focus();
  }
  el('cri-criptografar').addEventListener('click', criptografar);
  el('cri-descriptografar').addEventListener('click', descriptografar);
  el('cri-copiar').addEventListener('click', copiar);
  el('cri-limpar-enc').addEventListener('click', limparEnc);
  el('cri-limpar-dec').addEventListener('click', limparDec);
  chaveEnc.addEventListener('keydown', function (e) { if (e.key === 'Enter') { criptografar(); } });
  chaveDec.addEventListener('keydown', function (e) { if (e.key === 'Enter') { descriptografar(); } });
  [texto, chaveEnc, codigoGerado, codigo, chaveDec].forEach(function (campo) {
    campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
    campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

**Para criptografar:**

1. Digite a mensagem no campo **Texto para criptografar**.
2. Escreva uma **chave** no campo **Chave para criptografar**. Ela funciona como uma senha.
3. Clique em **Criptografar** (ou pressione Enter no campo da chave).
4. Copie o **Código gerado** com o botão **Copiar código** e envie ou guarde onde quiser.

**Para descriptografar:**

1. Cole o código no campo **Código para descriptografar**.
2. Digite a mesma chave usada na criptografia no campo **Chave para descriptografar**.
3. Clique em **Descriptografar** para ver o texto original na área de resposta.
4. Use os botões **Limpar** para apagar os campos e começar de novo.

Sem a chave certa, não há como descobrir o texto. Guarde bem a chave: se ela for perdida, o texto não pode ser recuperado.

## Entendendo os termos

- **Criptografia:** processo que transforma um texto legível em um código embaralhado, que só pode ser lido por quem tem a chave.
- **Descriptografia:** processo inverso, que devolve o código ao texto original usando a mesma chave.
- **Texto original:** a mensagem escrita normalmente, antes de ser criptografada.
- **Código (texto cifrado):** resultado da criptografia, uma sequência de letras, números e símbolos sem sentido aparente.
- **Chave:** senha usada para criptografar e descriptografar. A mesma chave é necessária nas duas etapas.
- **AES-256-GCM:** algoritmo de criptografia moderno e muito usado. O GCM também detecta se o código foi alterado ou se a chave está errada.
- **PBKDF2:** método que transforma a chave digitada em uma chave forte, repetindo o cálculo muitas vezes. Isso torna lentas as tentativas de adivinhar a chave.
- **Salt:** valor aleatório misturado à chave a cada criptografia. Por causa dele, o mesmo texto com a mesma chave gera códigos diferentes.
- **IV (vetor de inicialização):** outro valor aleatório usado pelo AES-GCM para que cada criptografia seja única.
- **Base64:** forma de representar dados em letras, números e alguns símbolos, o que facilita copiar e colar o código.

## A criptografia é segura?

Sim. O texto é criptografado no seu navegador, com AES-256-GCM, e nem o texto nem a chave são enviados a um servidor. Mesmo assim, prefira uma chave longa e difícil de adivinhar, como uma frase com números e símbolos.

## Para que serve?

- Guardar senhas e anotações pessoais em lugares que outras pessoas podem ver, como o e-mail ou a nuvem.
- Enviar uma informação sigilosa por um canal e a chave por outro, por exemplo o código por e-mail e a chave por telefone.
- Fazer brincadeiras, jogos e caças ao tesouro com mensagens secretas.