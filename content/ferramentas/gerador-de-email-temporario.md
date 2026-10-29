---
title: "Gerador de Email Temporário"
seoTitle: "Gerador de Email Temporário"
description: "Gerador de Email Temporário: crie um e-mail descartável para receber mensagens. Grátis e online, sem cadastro."
summary: "Crie um e-mail descartável para receber mensagens."
date: 2026-10-29
draft: false
category: "rede"
tags: ["e-mail", "privacidade", "segurança"]
keywords: ["gerador de email temporário", "gerador de email temporário online", "e-mail", "privacidade", "segurança"]
---

Basta clicar em **Novo Email** abaixo para gerar um endereço temporário e receber mensagens na hora.

<div id="calc-email-temp" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✉️ Gerador de Email Temporário</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere um endereço descartável e receba mensagens na hora.</p>
<label for="et-endereco" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seu endereço de email temporário</label>
<input id="et-endereco" type="text" readonly placeholder="Gerando endereço..." autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="et-copiar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar</button>
<button type="button" id="et-novo" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Novo Email</button>
<button type="button" id="et-atualizar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Atualizar</button>
</div>
<div id="et-status" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="et-status-txt">gerando seu endereço, aguarde...</span><br><small style="color:#475569;">Expira em: <span id="et-relogio">--:--</span></small></div>
<div style="margin-top:16px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;font-size:0.95rem;line-height:1.5;">
<strong style="color:#3730a3;">Caixa de entrada</strong>
<div id="et-lista" style="margin-top:10px;"><span style="color:#64748b;">Aguardando recebimento de e-mail</span></div>
<div id="et-detalhe" style="display:none;margin-top:10px;"></div>
</div>
</div>
<script>
(function () {
  /* API Guerrilla Mail via JSONP (tag <script>): não depende de CORS nem de proxy */
  var API = 'https://api.guerrillamail.com/ajax.php';
  var DURACAO = 60 * 60 * 1000;
  var CHAVE = 'et-email-temporario-v2';
  var campo = document.getElementById('et-endereco');
  var btnCopiar = document.getElementById('et-copiar');
  var btnNovo = document.getElementById('et-novo');
  var btnAtualizar = document.getElementById('et-atualizar');
  var caixa = document.getElementById('et-status');
  var texto = document.getElementById('et-status-txt');
  var relogio = document.getElementById('et-relogio');
  var lista = document.getElementById('et-lista');
  var detalhe = document.getElementById('et-detalhe');
  var estado = { endereco: '', token: '', expira: 0 };
  var timerRelogio = null;
  var timerCaixa = null;
  var ESTILO_ITEM = 'display:block;width:100%;text-align:left;margin-bottom:8px;padding:10px 12px;background:#f8fafc;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;color:#1e293b;font-size:0.9rem;box-sizing:border-box;';
  var ESTILO_BTN = 'padding:8px 14px;margin-bottom:12px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
  function criar(tag, css, txt) {
    var e = document.createElement(tag);
    if (css) { e.style.cssText = css; }
    if (txt) { e.textContent = txt; }
    return e;
  }
  function pad(n) {
    var s = String(n);
    return s.length === 1 ? '0' + s : s;
  }
  function aviso(msg, tipo) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      texto.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      texto.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      texto.style.color = '#64748b';
    }
    texto.textContent = msg;
  }
  function requisitar(params) {
    return new Promise(function (resolve, reject) {
      var cb = '__et_cb_' + Date.now() + '_' + Math.floor(Math.random() * 1000000);
      var s = document.createElement('script');
      var t = setTimeout(function () { limpar(); reject(new Error('timeout')); }, 15000);
      function limpar() {
        clearTimeout(t);
        try { delete window[cb]; } catch (e) { window[cb] = undefined; }
        if (s.parentNode) { s.parentNode.removeChild(s); }
      }
      window[cb] = function (dados) { limpar(); resolve(dados); };
      s.onerror = function () { limpar(); reject(new Error('rede')); };
      var q = Object.keys(params).map(function (k) {
        return encodeURIComponent(k) + '=' + encodeURIComponent(params[k]);
      }).join('&');
      s.src = API + '?' + q + '&callback=' + cb + '&_=' + Date.now();
      document.head.appendChild(s);
    });
  }
  function htmlParaTexto(html) {
    var d = new DOMParser().parseFromString(html || '', 'text/html');
    var rm = d.querySelectorAll('script,style');
    for (var i = 0; i < rm.length; i++) { rm[i].parentNode.removeChild(rm[i]); }
    return (d.body.textContent || '').replace(/[ \t]+\n/g, '\n').replace(/\n{3,}/g, '\n\n').trim();
  }
  function salvar() {
    try { localStorage.setItem(CHAVE, JSON.stringify(estado)); } catch (e) {}
  }
  function apagarSalvo() {
    try { localStorage.removeItem(CHAVE); } catch (e) {}
  }
  function pararTimers() {
    if (timerRelogio) { clearInterval(timerRelogio); timerRelogio = null; }
    if (timerCaixa) { clearInterval(timerCaixa); timerCaixa = null; }
  }
  function mostrarVazio() {
    lista.textContent = '';
    lista.appendChild(criar('span', 'color:#64748b;', 'Aguardando recebimento de e-mail'));
    lista.style.display = 'block';
    detalhe.style.display = 'none';
    detalhe.textContent = '';
  }
  function expirar() {
    pararTimers();
    apagarSalvo();
    estado = { endereco: '', token: '', expira: 0 };
    campo.value = '';
    relogio.textContent = '--:--';
    mostrarVazio();
    aviso('o e-mail expirou. Clique em "Novo Email" para gerar outro.', 'erro');
  }
  function tick() {
    var restante = estado.expira - Date.now();
    if (Math.max(0, restante) === 0) { expirar(); return; }
    var s = Math.floor(restante / 1000);
    relogio.textContent = pad(Math.floor(s / 60)) + ':' + pad(s % 60);
  }
  function hora(ts) {
    var d = new Date(Number(ts) * 1000);
    if (isNaN(d.getTime())) { return ''; }
    return d.toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' });
  }
  function desenhar(itens) {
    if (detalhe.style.display === 'block') { return; }
    if (!itens.length) { mostrarVazio(); return; }
    lista.textContent = '';
    itens.forEach(function (m) {
      var b = criar('button', ESTILO_ITEM);
      b.type = 'button';
      var de = m.mail_from || 'Remetente desconhecido';
      b.appendChild(criar('strong', 'display:block;color:#3730a3;', m.mail_subject || '(sem assunto)'));
      b.appendChild(criar('span', 'display:block;color:#475569;', de + ' · ' + hora(m.mail_timestamp)));
      b.addEventListener('click', function () { abrir(m.mail_id); });
      lista.appendChild(b);
    });
  }
  async function atualizar() {
    if (!estado.token) { return; }
    try {
      var dados = await requisitar({ f: 'check_email', seq: 0, sid_token: estado.token });
      desenhar(dados.list || []);
    } catch (e) {
      aviso('não foi possível atualizar a caixa de entrada agora.', 'erro');
    }
  }
  function voltar() {
    detalhe.style.display = 'none';
    detalhe.textContent = '';
    lista.style.display = 'block';
    atualizar();
  }
  async function abrir(id) {
    try {
      var m = await requisitar({ f: 'fetch_email', email_id: id, sid_token: estado.token });
      var de = m.mail_from || 'Remetente desconhecido';
      var corpo = htmlParaTexto(m.mail_body);
      detalhe.textContent = '';
      var voltarBtn = criar('button', ESTILO_BTN, 'Voltar para a lista');
      voltarBtn.type = 'button';
      voltarBtn.addEventListener('click', voltar);
      detalhe.appendChild(voltarBtn);
      detalhe.appendChild(criar('div', 'font-weight:700;color:#3730a3;', 'Assunto: ' + (m.mail_subject || '(sem assunto)')));
      detalhe.appendChild(criar('div', 'color:#475569;margin-bottom:10px;', 'De: ' + de + ' · ' + hora(m.mail_timestamp)));
      detalhe.appendChild(criar('div', 'white-space:pre-wrap;word-break:break-word;color:#1e293b;', corpo || '(mensagem sem conteúdo em texto)'));
      lista.style.display = 'none';
      detalhe.style.display = 'block';
    } catch (e) {
      aviso('não foi possível abrir a mensagem.', 'erro');
    }
  }
  function iniciar() {
    pararTimers();
    campo.value = estado.endereco;
    mostrarVazio();
    aviso('endereço pronto! Use-o em qualquer cadastro e aguarde as mensagens.', 'ok');
    tick();
    timerRelogio = setInterval(tick, 1000);
    timerCaixa = setInterval(atualizar, 10000);
    atualizar();
  }
  async function gerar() {
    pararTimers();
    btnNovo.disabled = true;
    campo.value = '';
    relogio.textContent = '--:--';
    mostrarVazio();
    aviso('gerando seu endereço, aguarde...', 'neutro');
    try {
      var r = await requisitar({ f: 'get_email_address', lang: 'en', ip: '127.0.0.1', agent: 'gerador-email-temporario' });
      if (!r || !r.email_addr || !r.sid_token) { throw new Error('resposta inválida'); }
      estado = { endereco: r.email_addr, token: r.sid_token, expira: Date.now() + DURACAO };
      salvar();
      iniciar();
    } catch (e) {
      aviso('não foi possível gerar o endereço agora. Tente novamente em instantes.', 'erro');
    }
    btnNovo.disabled = false;
  }
  function copiar() {
    if (!campo.value) { aviso('ainda não há endereço para copiar.', 'erro'); return; }
    function ok() { aviso('endereço copiado: ' + campo.value, 'ok'); }
    function alternativo() {
      campo.select();
      try { document.execCommand('copy'); ok(); } catch (e) { aviso('copie o endereço manualmente.', 'erro'); }
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(campo.value).then(ok, alternativo);
    } else {
      alternativo();
    }
  }
  btnCopiar.addEventListener('click', copiar);
  btnNovo.addEventListener('click', gerar);
  btnAtualizar.addEventListener('click', atualizar);
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  var salvo = null;
  try { salvo = JSON.parse(localStorage.getItem(CHAVE)); } catch (e) { salvo = null; }
  if (salvo && salvo.token && Math.max(0, salvo.expira - Date.now()) !== 0) {
    estado = salvo;
    iniciar();
  } else {
    gerar();
  }
})();
</script>

## Como usar o gerador de email temporário

1. Ao abrir a página, um endereço de e-mail temporário é gerado automaticamente no campo **Seu endereço de email temporário**.
2. Clique em **Copiar** para copiar o endereço e cole-o no cadastro, sorteio ou site onde você precisa informar um e-mail.
3. Aguarde as mensagens chegarem na **Caixa de entrada**. A lista é atualizada sozinha a cada 10 segundos, ou você pode clicar em **Atualizar**.
4. Clique em uma mensagem para ler o conteúdo e use **Voltar para a lista** para retornar.
5. Clique em **Novo Email** para descartar o endereço atual e gerar outro.

O endereço fica válido por **1 hora**, e o tempo restante aparece em **Expira em**. Depois disso, o e-mail e as mensagens deixam de estar disponíveis e você precisa gerar um novo. Por ser um domínio temporário conhecido, alguns sites podem bloquear o cadastro ou não enviar a mensagem de verificação. Nesses casos, use um e-mail pessoal.

## Entendendo os termos

- **E-mail temporário:** endereço de e-mail criado para uso rápido, que deixa de funcionar depois de um tempo.
- **E-mail descartável:** outro nome para o e-mail temporário, pois pode ser jogado fora sem perder nada importante.
- **Endereço de e-mail:** identificação da caixa de mensagens, no formato nome@domínio.
- **Domínio:** a parte do endereço depois do @, que indica o serviço responsável pela caixa de mensagens.
- **Caixa de entrada:** lugar onde as mensagens recebidas aparecem.
- **Remetente:** pessoa ou serviço que enviou a mensagem.
- **Assunto:** título da mensagem, que resume o motivo do contato.
- **Validade:** tempo em que o endereço funciona. Aqui, são 1 hora a partir da criação.
- **Spam:** mensagens indesejadas, geralmente propagandas, enviadas em massa.
- **Verificação de conta:** etapa em que um site envia um código ou link ao seu e-mail para confirmar o cadastro.