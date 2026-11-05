---
title: "Mensagem Autodestrutiva"
seoTitle: "Mensagem Autodestrutiva"
description: "Mensagem Autodestrutiva: envie uma mensagem que se apaga depois de lida. Grátis e online, sem cadastro."
summary: "Envie uma mensagem que se apaga depois de lida."
date: 2026-11-05
draft: false
category: "dev"
tags: ["segurança", "privacidade", "mensagens"]
keywords: ["mensagem autodestrutiva", "mensagem autodestrutiva online", "segurança", "privacidade", "mensagens"]
---

Basta escrever a mensagem abaixo, escolher o prazo de validade e clicar em **Criar Link**.

<div id="calc-autodestrutiva" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔥 Mensagem Autodestrutiva</h2>
<div id="aut-criar">
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escreva sua mensagem e gere um link de uso único.</p>
<label for="aut-msg" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Mensagem</label>
<textarea id="aut-msg" rows="5" maxlength="2000" placeholder="Digite aqui a sua mensagem secreta..." style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="aut-prazo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Destruir automaticamente caso não seja vista</label>
<select id="aut-prazo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<optgroup label="Minutos">
<option value="30">30 minutos</option>
<option value="60">60 minutos</option>
</optgroup>
<optgroup label="Horas">
<option value="120">2 horas</option>
<option value="240">4 horas</option>
<option value="480">8 horas</option>
</optgroup>
<optgroup label="Dias">
<option value="1440">1 dia</option>
<option value="10080" selected>7 dias</option>
<option value="43200">30 dias</option>
</optgroup>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="aut-criar-btn" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Criar Link</button>
<button type="button" id="aut-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="aut-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="aut-resultado">escreva a mensagem e clique em "Criar Link".</span></div>
<div id="aut-link-area" style="display:none;margin-top:16px;">
<label for="aut-link" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">URL de uso único</label>
<input id="aut-link" type="text" readonly autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:0.9rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="aut-copiar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar Link</button>
<button type="button" id="aut-outra" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Criar Outra</button>
</div>
</div>
</div>
<div id="aut-ler" style="display:none;">
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Você recebeu uma mensagem autodestrutiva.</p>
<div id="aut-ler-resposta" aria-live="polite" style="padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Aviso:</strong> <span id="aut-ler-texto">ao revelar, a mensagem será exibida uma única vez e depois destruída.</span></div>
<div id="aut-mensagem" style="display:none;margin-top:16px;padding:16px;background:#ffffff;border:2px solid #86efac;border-radius:12px;color:#1e293b;font-size:1rem;line-height:1.6;white-space:pre-wrap;word-break:break-word;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:20px;">
<button type="button" id="aut-revelar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Revelar Mensagem</button>
<button type="button" id="aut-nova" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Criar Outra</button>
</div>
</div>
</div>
<script>
(function () {
  function $(id) { return document.getElementById(id); }
  var secCriar = $('aut-criar');
  var secLer = $('aut-ler');
  var msg = $('aut-msg');
  var prazo = $('aut-prazo');
  var caixa = $('aut-resposta');
  var resultado = $('aut-resultado');
  var linkArea = $('aut-link-area');
  var linkInput = $('aut-link');
  var lerCaixa = $('aut-ler-resposta');
  var lerTexto = $('aut-ler-texto');
  var mensagemBox = $('aut-mensagem');
  var btnRevelar = $('aut-revelar');
  var partesAtuais = null;
  var CORES = {
    ok: ['#86efac', '#f0fdf4', '#166534'],
    erro: ['#fca5a5', '#fef2f2', '#b91c1c'],
    neutro: ['#c7d2fe', '#ffffff', '#64748b']
  };
  function estilo(box, span, tipo, texto) {
    var c = CORES[tipo];
    box.style.borderColor = c[0];
    box.style.background = c[1];
    span.style.color = c[2];
    span.textContent = texto;
  }
  function temCrypto() {
    var c = window.crypto;
    if (!c) { return false; }
    if (!c.subtle) { return false; }
    return typeof window.TextEncoder === 'function';
  }
  function b64e(buf) {
    var b = new Uint8Array(buf);
    var s = '';
    for (var i = 0; i !== b.length; i++) { s += String.fromCharCode(b[i]); }
    return btoa(s).split('+').join('-').split('/').join('_').split('=').join('');
  }
  function b64d(str) {
    var t = str.split('-').join('+').split('_').join('/');
    while (t.length % 4 !== 0) { t += '='; }
    var s = atob(t);
    var b = new Uint8Array(s.length);
    for (var i = 0; i !== s.length; i++) { b[i] = s.charCodeAt(i); }
    return b;
  }
  function jaLida(id) {
    try { return window.localStorage.getItem('aut-lida-' + id) === '1'; } catch (e) { return false; }
  }
  function marcarLida(id) {
    try { window.localStorage.setItem('aut-lida-' + id, '1'); } catch (e) {}
  }
  async function criarLink() {
    var texto = msg.value.trim();
    if (texto === '') { estilo(caixa, resultado, 'erro', 'escreva uma mensagem antes de criar o link.'); linkArea.style.display = 'none'; return; }
    if (!temCrypto()) { estilo(caixa, resultado, 'erro', 'seu navegador não suporta criptografia. Use uma conexão segura (https) e um navegador atual.'); return; }
    try {
      var exp = Date.now() + Number(prazo.value) * 60000;
      var enc = new TextEncoder();
      var chave = await window.crypto.subtle.generateKey({ name: 'AES-GCM', length: 256 }, true, ['encrypt', 'decrypt']);
      var iv = window.crypto.getRandomValues(new Uint8Array(12));
      var cifrado = await window.crypto.subtle.encrypt({ name: 'AES-GCM', iv: iv, additionalData: enc.encode(String(exp)) }, chave, enc.encode(texto));
      var bruta = await window.crypto.subtle.exportKey('raw', chave);
      var hash = '#m=' + b64e(iv) + '.' + b64e(cifrado) + '.' + b64e(bruta) + '.' + exp;
      linkInput.value = window.location.origin + window.location.pathname + window.location.search + hash;
      linkArea.style.display = 'block';
      estilo(caixa, resultado, 'ok', 'link criado! Envie-o ao destinatário. Ele só abrirá uma vez.');
    } catch (e) {
      estilo(caixa, resultado, 'erro', 'não foi possível criar o link. Tente novamente.');
    }
  }
  function copiar() {
    var texto = linkInput.value;
    function fallback() {
      linkInput.focus();
      linkInput.select();
      try { document.execCommand('copy'); } catch (e) {}
    }
    var cb = navigator.clipboard;
    if (cb) {
      if (cb.writeText) {
        cb.writeText(texto).then(function () {
          estilo(caixa, resultado, 'ok', 'link copiado para a área de transferência.');
        }, fallback);
        return;
      }
    }
    fallback();
  }
  function limpar() {
    msg.value = '';
    prazo.value = '10080';
    linkInput.value = '';
    linkArea.style.display = 'none';
    estilo(caixa, resultado, 'neutro', 'escreva a mensagem e clique em "Criar Link".');
    msg.focus();
  }
  function novaMensagem() {
    window.history.replaceState(null, '', window.location.pathname + window.location.search);
    iniciar();
    limpar();
  }
  function falhaLeitura(texto) {
    btnRevelar.style.display = 'none';
    mensagemBox.style.display = 'none';
    estilo(lerCaixa, lerTexto, 'erro', texto);
  }
  async function revelar() {
    var p = partesAtuais;
    if (!p) { return; }
    if (!temCrypto()) { falhaLeitura('seu navegador não suporta criptografia. Use uma conexão segura (https) e um navegador atual.'); return; }
    if (jaLida(p[0])) { falhaLeitura('esta mensagem já foi lida e foi destruída.'); return; }
    try {
      var chave = await window.crypto.subtle.importKey('raw', b64d(p[2]), { name: 'AES-GCM' }, false, ['decrypt']);
      var claro = await window.crypto.subtle.decrypt({ name: 'AES-GCM', iv: b64d(p[0]), additionalData: new TextEncoder().encode(p[3]) }, chave, b64d(p[1]));
      marcarLida(p[0]);
      window.history.replaceState(null, '', window.location.pathname + window.location.search);
      partesAtuais = null;
      mensagemBox.textContent = new TextDecoder().decode(claro);
      mensagemBox.style.display = 'block';
      btnRevelar.style.display = 'none';
      estilo(lerCaixa, lerTexto, 'ok', 'mensagem revelada. Ela foi destruída e não poderá ser aberta novamente neste link.');
    } catch (e) {
      falhaLeitura('link inválido ou danificado. Peça ao remetente para gerar outro.');
    }
  }
  function iniciar() {
    var h = window.location.hash;
    if (h.indexOf('#m=') !== 0) {
      secCriar.style.display = 'block';
      secLer.style.display = 'none';
      return;
    }
    secCriar.style.display = 'none';
    secLer.style.display = 'block';
    mensagemBox.style.display = 'none';
    btnRevelar.style.display = 'block';
    estilo(lerCaixa, lerTexto, 'neutro', 'ao revelar, a mensagem será exibida uma única vez e depois destruída.');
    var p = h.slice(3).split('.');
    if (p.length !== 4) { falhaLeitura('link inválido ou incompleto.'); return; }
    var exp = Number(p[3]);
    if (isNaN(exp)) { falhaLeitura('link inválido ou incompleto.'); return; }
    if (jaLida(p[0])) { falhaLeitura('esta mensagem já foi lida e foi destruída.'); return; }
    if (Math.sign(Date.now() - exp) === 1) { falhaLeitura('esta mensagem expirou e foi destruída.'); return; }
    partesAtuais = p;
  }
  $('aut-criar-btn').addEventListener('click', criarLink);
  $('aut-limpar').addEventListener('click', limpar);
  $('aut-copiar').addEventListener('click', copiar);
  $('aut-outra').addEventListener('click', limpar);
  $('aut-nova').addEventListener('click', novaMensagem);
  btnRevelar.addEventListener('click', revelar);
  [msg, prazo, linkInput].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  window.addEventListener('hashchange', iniciar);
  iniciar();
})();
</script>

## Como usar a ferramenta

1. Digite a sua mensagem no campo **Mensagem** (até 2.000 caracteres).
2. Escolha em **Destruir automaticamente caso não seja vista** por quanto tempo o link continuará válido: de 30 minutos até 30 dias.
3. Clique em **Criar Link** para gerar a **URL de uso único**.
4. Clique em **Copiar Link** e envie a URL ao destinatário por qualquer aplicativo de mensagens ou e-mail.
5. O destinatário abre o link e clica em **Revelar Mensagem**. O texto aparece uma única vez e, depois disso, o link deixa de funcionar.
6. Use **Criar Outra** ou **Limpar** para começar uma nova mensagem.

## Entendendo os termos

- **Mensagem autodestrutiva:** mensagem que deixa de ficar disponível depois de ser lida pela primeira vez.
- **Criptografia:** processo que embaralha o texto para que ele só possa ser lido por quem tem a chave. Aqui é usado o padrão AES-256 (modo GCM), executado no próprio navegador.
- **Chave:** código secreto usado para trancar e destrancar a mensagem. Ela fica dentro do link gerado.
- **URL de uso único:** endereço que abre a mensagem apenas uma vez. Depois da primeira leitura, ele passa a mostrar que a mensagem foi destruída.
- **Prazo de validade:** tempo máximo em que o link pode ser aberto. Se ninguém abrir dentro desse período, a mensagem expira.
- **Revelar mensagem:** ação que descriptografa e exibe o texto. É o momento em que a mensagem é considerada lida e destruída.
- **Destinatário:** pessoa que recebe o link e lê a mensagem.

## Como funciona

A mensagem é criptografada no seu navegador e todo o conteúdo cifrado, junto com a chave, fica dentro do próprio link. Nada é enviado para um servidor, então só quem tem o link consegue ler. A destruição acontece no navegador de quem abre o link: depois da leitura, o aviso de "já lida" é guardado ali e o conteúdo é removido do endereço. Por isso, não envie o link para mais de uma pessoa nem o publique em locais abertos.