---
title: "Contador de Inscritos em Tempo Real"
seoTitle: "Contador de Inscritos em Tempo Real"
description: "Contador de Inscritos em Tempo Real: acompanhe o número de inscritos de um canal em tempo real. Grátis e online, sem cadastro."
summary: "Acompanhe o número de inscritos de um canal em tempo real."
date: 2026-10-25
draft: false
category: "social"
tags: ["youtube", "inscritos", "contador", "redes sociais"]
keywords: ["contador de inscritos em tempo real", "contador de inscritos em tempo real online", "youtube", "inscritos", "contador"]
---
<!--sudah dikerjakan-->

Basta digitar o @ do canal (ou o link) abaixo e depois clicar em **Acompanhar Inscritos**.

<div id="calc-inscritos" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📺 Contador de Inscritos em Tempo Real</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o canal e acompanhe os inscritos ao vivo.</p>
<label for="ins-canal" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Canal do YouTube</label>
<input id="ins-canal" type="text" placeholder="Ex.: @MrBeast ou link do canal" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ins-iniciar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Acompanhar Inscritos</button>
<button type="button" id="ins-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ins-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ins-resultado">informe o canal e clique em "Acompanhar Inscritos".</span>
<div id="ins-painel" style="display:none;margin-top:14px;text-align:center;">
<img id="ins-foto" alt="Foto do canal" width="72" height="72" style="width:72px;height:72px;border-radius:50%;border:3px solid #c7d2fe;object-fit:cover;">
<div id="ins-nome" style="margin-top:8px;font-weight:700;color:#3730a3;"></div>
<div id="ins-numero" style="margin:6px 0;font-size:2.2rem;font-weight:800;color:#166534;font-variant-numeric:tabular-nums;"></div>
<div id="ins-ganho" style="font-size:0.9rem;color:#475569;"></div>
<div id="ins-hora" style="font-size:0.8rem;color:#64748b;"></div>
</div>
</div>
</div>
<script>
(function () {
  var API_KEY = 'COLE_SUA_CHAVE_DA_API_AQUI';
  var INTERVALO = 15000;
  var campo = document.getElementById('ins-canal');
  var resultado = document.getElementById('ins-resultado');
  var caixa = document.getElementById('ins-resposta');
  var painel = document.getElementById('ins-painel');
  var foto = document.getElementById('ins-foto');
  var nome = document.getElementById('ins-nome');
  var numero = document.getElementById('ins-numero');
  var ganho = document.getElementById('ins-ganho');
  var hora = document.getElementById('ins-hora');
  var timer = null;
  var base = null;
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function estilo(borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
  }
  function erro(msg) {
    parar();
    painel.style.display = 'none';
    estilo('#fca5a5', '#fef2f2', '#b91c1c');
    resultado.textContent = msg;
  }
  function parar() {
    if (timer) { clearInterval(timer); timer = null; }
  }
  function extrair(v) {
    var t = String(v).trim();
    var m;
    if (t === '') { return null; }
    m = t.match(/channel\/(UC[\w-]{20,})/);
    if (m) { return { id: m[1] }; }
    m = t.match(/@([\w.\-]+)/);
    if (m) { return { handle: '@' + m[1] }; }
    if (/^UC[\w-]{20,}$/.test(t)) { return { id: t }; }
    return { handle: '@' + t.replace(/^@/, '') };
  }
  function buscar(q, primeira) {
    var url = 'https://www.googleapis.com/youtube/v3/channels?part=snippet,statistics&key=' + encodeURIComponent(API_KEY) + '&' + (q.id ? 'id=' + encodeURIComponent(q.id) : 'forHandle=' + encodeURIComponent(q.handle));
    fetch(url).then(function (r) { return r.json(); }).then(function (d) {
      var c, total;
      if (d.error) { erro('não foi possível consultar o canal agora. Tente novamente em instantes.'); return; }
      if (!d.items) { erro('canal não encontrado. Confira o @ ou o link informado.'); return; }
      if (d.items.length === 0) { erro('canal não encontrado. Confira o @ ou o link informado.'); return; }
      c = d.items[0];
      if (c.statistics.hiddenSubscriberCount) { erro('este canal mantém o número de inscritos oculto.'); return; }
      total = Number(c.statistics.subscriberCount);
      if (primeira) { base = total; }
      estilo('#86efac', '#f0fdf4', '#166534');
      resultado.textContent = 'acompanhando ao vivo (atualiza a cada 15 segundos).';
      painel.style.display = 'block';
      foto.src = c.snippet.thumbnails.default.url;
      nome.textContent = c.snippet.title;
      numero.textContent = fmt(total);
      ganho.textContent = 'Variação desde que você começou: ' + (total >= base ? '+' : '') + fmt(total - base);
      hora.textContent = 'Última atualização: ' + new Date().toLocaleTimeString('pt-BR');
    }).catch(function () {
      erro('falha de conexão. Verifique sua internet e tente de novo.');
    });
  }
  function iniciar() {
    var q = extrair(campo.value);
    parar();
    if (!q) { erro('informe o @ ou o link de um canal.'); return; }
    if (API_KEY.indexOf('COLE_') === 0) { erro('a chave da API do YouTube ainda não foi configurada nesta página.'); return; }
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = 'buscando o canal...';
    base = null;
    buscar(q, true);
    timer = setInterval(function () {
      if (!document.hidden) { buscar(q, false); }
    }, INTERVALO);
  }
  function limpar() {
    parar();
    base = null;
    campo.value = '';
    painel.style.display = 'none';
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = 'informe o canal e clique em "Acompanhar Inscritos".';
    campo.focus();
  }
  document.getElementById('ins-iniciar').addEventListener('click', iniciar);
  document.getElementById('ins-limpar').addEventListener('click', limpar);
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { iniciar(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o contador

1. Digite o **@ do canal** (por exemplo, `@MrBeast`) ou cole o **link do canal** do YouTube no campo.
2. Clique em **Acompanhar Inscritos** (ou pressione Enter).
3. Veja o número de inscritos, a foto e o nome do canal. O valor é atualizado sozinho a cada 15 segundos enquanto a aba estiver aberta.
4. Use o botão **Limpar** para parar o acompanhamento e consultar outro canal.

Você pode informar o @ com ou sem o símbolo, o link completo (`youtube.com/@canal`) ou o link com o ID do canal (`youtube.com/channel/UC...`). Canais que ocultam o número de inscritos não podem ser acompanhados.

## Entendendo os termos

- **Inscrito:** pessoa que se inscreveu em um canal para receber os seus vídeos e novidades.
- **Canal:** página de um criador no YouTube, onde ficam os vídeos, a foto e o nome.
- **@ (handle):** nome de usuário único do canal, que começa com @, como `@MrBeast`.
- **ID do canal:** código único do canal, que começa com UC e aparece no link `youtube.com/channel/...`.
- **Tempo real:** acompanhamento contínuo, em que o número é consultado de novo automaticamente em intervalos curtos.
- **Variação:** diferença entre o número atual de inscritos e o número no momento em que você iniciou o acompanhamento.
- **Contagem arredondada:** o YouTube arredonda o número exibido em canais grandes (por exemplo, 12,3 milhões), então a contagem pode avançar em saltos.