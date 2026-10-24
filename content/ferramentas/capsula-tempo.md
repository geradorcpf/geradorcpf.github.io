---
title: "Cápsula do Tempo"
seoTitle: "Cápsula do Tempo"
description: "Cápsula do Tempo: escreva uma mensagem hoje para ser aberta no futuro. Grátis e online, sem cadastro."
summary: "Escreva uma mensagem hoje para ser aberta no futuro."
date: 2026-10-24
draft: false
category: "util"
tags: ["cápsula do tempo", "mensagens", "datas", "produtividade"]
keywords: ["cápsula do tempo", "cápsula do tempo online", "mensagens", "datas"]
---
<!--sudah dikerjakan-->

Escolha a data de abertura, escreva sua mensagem (com imagem, se quiser) e clique em **Enviar para o futuro**.

<div id="calc-capsula" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⏳ Cápsula do Tempo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escreva hoje e abra só na data escolhida.</p>
<label style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data de abertura</label>
<div style="display:flex;gap:8px;margin-bottom:16px;">
<select id="ct-dia" aria-label="Dia" style="flex:1;min-width:0;padding:12px 10px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="ct-mes" aria-label="Mês" style="flex:1;min-width:0;padding:12px 10px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="ct-ano" aria-label="Ano" style="flex:1;min-width:0;padding:12px 10px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
</div>
<label for="ct-email" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">E-mail (opcional)</label>
<input id="ct-email" type="text" inputmode="email" placeholder="Ex.: voce@email.com" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ct-assunto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Assunto</label>
<input id="ct-assunto" type="text" placeholder="Ex.: Uma carta para mim em 2030" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ct-imagem" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Imagem (opcional)</label>
<input id="ct-imagem" type="file" accept="image/*" style="width:100%;padding:10px 12px;margin-bottom:6px;font-size:0.95rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;">
<div id="ct-imagem-info" style="margin-bottom:16px;font-size:0.85rem;color:#64748b;">Nenhuma imagem selecionada.</div>
<label for="ct-mensagem" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Mensagem</label>
<textarea id="ct-mensagem" placeholder="Escreva aqui a mensagem para o seu eu do futuro..." style="width:100%;min-height:120px;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ct-enviar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Enviar para o futuro</button>
<button type="button" id="ct-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ct-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ct-resultado">preencha os campos e clique em "Enviar para o futuro".</span></div>
<div id="ct-lista" style="margin-top:20px;"></div>
</div>
<script>
(function () {
  var CHAVE = 'capsula-tempo-v1';
  var MESES = ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez'];
  var elDia = document.getElementById('ct-dia');
  var elMes = document.getElementById('ct-mes');
  var elAno = document.getElementById('ct-ano');
  var elEmail = document.getElementById('ct-email');
  var elAssunto = document.getElementById('ct-assunto');
  var elImagem = document.getElementById('ct-imagem');
  var elImagemInfo = document.getElementById('ct-imagem-info');
  var elMsg = document.getElementById('ct-mensagem');
  var elLista = document.getElementById('ct-lista');
  var resultado = document.getElementById('ct-resultado');
  var caixa = document.getElementById('ct-resposta');
  var imagemDados = '';
  var TEXTO_PADRAO = 'preencha os campos e clique em "Enviar para o futuro".';
  function pad2(n) { return n > 9 ? String(n) : '0' + n; }
  function criar(tag, estilo, texto) {
    var e = document.createElement(tag);
    if (estilo) { e.setAttribute('style', estilo); }
    if (texto !== undefined) { e.textContent = texto; }
    return e;
  }
  function popular(select, de, ate, rotulo) {
    while (select.firstChild) { select.removeChild(select.firstChild); }
    for (var i = de; ate >= i; i++) {
      var op = document.createElement('option');
      op.value = String(i);
      op.textContent = rotulo(i);
      select.appendChild(op);
    }
  }
  function atualizarDias() {
    var m = Number(elMes.value);
    var y = Number(elAno.value);
    var total = new Date(y, m + 1, 0).getDate();
    var atual = Number(elDia.value) || 1;
    popular(elDia, 1, total, pad2);
    elDia.value = String(Math.min(atual, total));
  }
  function formatarData(ms) {
    var d = new Date(ms);
    return pad2(d.getDate()) + '/' + pad2(d.getMonth() + 1) + '/' + d.getFullYear();
  }
  function mostrar(tipo, texto) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    }
    resultado.textContent = texto;
  }
  function lerCapsulas() {
    try {
      var v = localStorage.getItem(CHAVE);
      return v ? JSON.parse(v) : [];
    } catch (e) { return []; }
  }
  function salvarCapsulas(lista) {
    try {
      localStorage.setItem(CHAVE, JSON.stringify(lista));
      return true;
    } catch (e) { return false; }
  }
  function excluir(id) {
    if (!window.confirm('Excluir esta cápsula? Essa ação não pode ser desfeita.')) { return; }
    var lista = lerCapsulas().filter(function (c) { return c.id !== id; });
    salvarCapsulas(lista);
    renderizar();
  }
  function cartao(c) {
    var agora = Date.now();
    var aberta = agora >= c.abre;
    var box = criar('div', 'margin-bottom:12px;padding:14px 16px;background:#ffffff;border:2px solid ' + (aberta ? '#86efac' : '#c7d2fe') + ';border-radius:12px;line-height:1.5;font-size:0.95rem;');
    if (aberta) {
      box.appendChild(criar('div', 'font-weight:700;color:#166534;', '🔓 Aberta · ' + formatarData(c.abre)));
      box.appendChild(criar('div', 'font-weight:700;margin-top:6px;color:#1e293b;', c.assunto || '(sem assunto)'));
      box.appendChild(criar('div', 'margin-top:6px;white-space:pre-wrap;word-wrap:break-word;color:#334155;', c.mensagem));
      if (c.imagem) {
        var img = criar('img', 'display:block;max-width:100%;margin-top:10px;border-radius:10px;');
        img.src = c.imagem;
        img.alt = 'Imagem da cápsula';
        box.appendChild(img);
      }
    } else {
      var dias = Math.ceil((c.abre - agora) / 86400000);
      box.appendChild(criar('div', 'font-weight:700;color:#3730a3;', '🔒 Fechada · abre em ' + formatarData(c.abre)));
      box.appendChild(criar('div', 'margin-top:4px;color:#64748b;', 'Faltam ' + dias + (dias === 1 ? ' dia.' : ' dias.')));
    }
    var acoes = criar('div', 'display:flex;gap:8px;flex-wrap:wrap;margin-top:10px;');
    if (aberta) {
      if (c.email) {
        var link = criar('a', 'padding:8px 12px;font-size:0.9rem;font-weight:600;color:#ffffff;background:#4f46e5;border-radius:8px;text-decoration:none;', 'Enviar por e-mail');
        link.href = 'mailto:' + c.email + '?subject=' + encodeURIComponent(c.assunto || 'Minha cápsula do tempo') + '&body=' + encodeURIComponent(c.mensagem);
        acoes.appendChild(link);
      }
    }
    var bt = criar('button', 'padding:8px 12px;font-size:0.9rem;font-weight:600;color:#b91c1c;background:#ffffff;border:2px solid #fca5a5;border-radius:8px;cursor:pointer;', 'Excluir');
    bt.type = 'button';
    bt.addEventListener('click', function () { excluir(c.id); });
    acoes.appendChild(bt);
    box.appendChild(acoes);
    return box;
  }
  function renderizar() {
    while (elLista.firstChild) { elLista.removeChild(elLista.firstChild); }
    var lista = lerCapsulas().sort(function (a, b) { return a.abre - b.abre; });
    if (lista.length === 0) { return; }
    elLista.appendChild(criar('h3', 'margin:0 0 10px;font-size:1.05rem;color:#3730a3;', 'Suas cápsulas'));
    lista.forEach(function (c) { elLista.appendChild(cartao(c)); });
  }
  function comprimir(arquivo, cb) {
    var leitor = new FileReader();
    leitor.onerror = function () { cb(''); };
    leitor.onload = function () {
      var img = new Image();
      img.onerror = function () { cb(''); };
      img.onload = function () {
        var max = 800;
        var escala = Math.min(1, max / Math.max(img.width, img.height));
        var canvas = document.createElement('canvas');
        canvas.width = Math.round(img.width * escala);
        canvas.height = Math.round(img.height * escala);
        var ctx = canvas.getContext('2d');
        ctx.fillStyle = '#ffffff';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
        cb(canvas.toDataURL('image/jpeg', 0.7));
      };
      img.src = leitor.result;
    };
    leitor.readAsDataURL(arquivo);
  }
  function trocarImagem() {
    var arq = elImagem.files ? elImagem.files[0] : null;
    imagemDados = '';
    if (!arq) { elImagemInfo.textContent = 'Nenhuma imagem selecionada.'; return; }
    if (arq.type.indexOf('image/') !== 0) {
      elImagem.value = '';
      elImagemInfo.textContent = 'Nenhuma imagem selecionada.';
      mostrar('erro', 'o arquivo escolhido não é uma imagem.');
      return;
    }
    elImagemInfo.textContent = 'Processando imagem...';
    comprimir(arq, function (dados) {
      if (!dados) {
        elImagem.value = '';
        elImagemInfo.textContent = 'Nenhuma imagem selecionada.';
        mostrar('erro', 'não foi possível ler essa imagem. Tente outro arquivo.');
        return;
      }
      imagemDados = dados;
      elImagemInfo.textContent = 'Imagem pronta: ' + arq.name;
    });
  }
  function enviar() {
    var msg = elMsg.value.trim();
    var email = elEmail.value.trim();
    if (msg === '') { mostrar('erro', 'escreva uma mensagem para o futuro.'); return; }
    if (email !== '') {
      if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) { mostrar('erro', 'informe um e-mail válido ou deixe o campo em branco.'); return; }
    }
    var alvo = new Date(Number(elAno.value), Number(elMes.value), Number(elDia.value));
    var hoje = new Date();
    hoje.setHours(0, 0, 0, 0);
    if (hoje.getTime() >= alvo.getTime()) { mostrar('erro', 'escolha uma data de abertura no futuro.'); return; }
    var lista = lerCapsulas();
    lista.push({
      id: Date.now(),
      abre: alvo.getTime(),
      email: email,
      assunto: elAssunto.value.trim(),
      mensagem: msg,
      imagem: imagemDados
    });
    if (!salvarCapsulas(lista)) {
      mostrar('erro', 'não foi possível salvar a cápsula (espaço do navegador cheio ou armazenamento bloqueado). Tente sem imagem ou com uma imagem menor.');
      return;
    }
    mostrar('ok', 'Cápsula selada! Ela poderá ser aberta em ' + formatarData(alvo.getTime()) + '.');
    elMsg.value = '';
    elAssunto.value = '';
    elEmail.value = '';
    elImagem.value = '';
    imagemDados = '';
    elImagemInfo.textContent = 'Nenhuma imagem selecionada.';
    renderizar();
  }
  function limpar() {
    elMsg.value = '';
    elAssunto.value = '';
    elEmail.value = '';
    elImagem.value = '';
    imagemDados = '';
    elImagemInfo.textContent = 'Nenhuma imagem selecionada.';
    mostrar('neutro', TEXTO_PADRAO);
    elMsg.focus();
  }
  var anoAtual = new Date().getFullYear();
  var amanha = new Date();
  amanha.setDate(amanha.getDate() + 1);
  popular(elMes, 0, 11, function (i) { return MESES[i]; });
  popular(elAno, anoAtual, anoAtual + 10, String);
  elMes.value = String(amanha.getMonth());
  elAno.value = String(amanha.getFullYear());
  atualizarDias();
  elDia.value = String(amanha.getDate());
  elMes.addEventListener('change', atualizarDias);
  elAno.addEventListener('change', atualizarDias);
  elImagem.addEventListener('change', trocarImagem);
  document.getElementById('ct-enviar').addEventListener('click', enviar);
  document.getElementById('ct-limpar').addEventListener('click', limpar);
  [elDia, elMes, elAno, elEmail, elAssunto, elMsg].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  renderizar();
})();
</script>

## Como usar a Cápsula do Tempo

1. Escolha a **Data de abertura** (dia, mês e ano). Ela precisa ser posterior a hoje.
2. Se quiser, informe seu **E-mail**. Ele serve para enviar a mensagem para você quando a cápsula for aberta.
3. Digite o **Assunto** da mensagem.
4. Se desejar, anexe uma **Imagem** (ela é reduzida automaticamente para ocupar pouco espaço).
5. Escreva sua **Mensagem** no campo de texto.
6. Clique em **Enviar para o futuro** para selar a cápsula. Use **Limpar** para apagar os campos.
7. Role a página até **Suas cápsulas**: as fechadas mostram quantos dias faltam e, a partir da data escolhida, a cápsula se abre e exibe a mensagem.

As cápsulas ficam salvas somente neste navegador e neste aparelho. Se você limpar os dados do navegador ou usar outro dispositivo, elas não aparecerão.

## Entendendo os termos

- **Cápsula do tempo:** mensagem guardada hoje para ser lida em uma data futura.
- **Data de abertura:** dia em que a cápsula passa a poder ser aberta e lida.
- **E-mail:** endereço usado para enviar a mensagem para você depois que a cápsula abrir. É opcional.
- **Assunto:** título curto que identifica a mensagem, como o assunto de um e-mail.
- **Imagem:** foto ou figura anexada à cápsula, exibida junto com a mensagem quando ela for aberta.
- **Mensagem:** texto principal que você escreve para o seu eu do futuro.
- **Cápsula fechada:** cápsula cuja data de abertura ainda não chegou. O conteúdo fica oculto.
- **Cápsula aberta:** cápsula cuja data de abertura já chegou. A mensagem e a imagem ficam visíveis.
- **Armazenamento do navegador:** espaço do próprio navegador onde as cápsulas são guardadas, sem cadastro e sem envio dos dados para um servidor.

## Para que serve?

Você pode usar a cápsula do tempo para lembrar de algo importante, registrar um momento especial, escrever uma carta para si mesmo ou deixar uma mensagem de metas e sonhos para ler daqui a alguns anos.