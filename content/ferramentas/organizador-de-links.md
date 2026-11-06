---
title: "Organizador de Links"
seoTitle: "Organizador de Links"
description: "Organizador de Links: reúna e organize seus links em uma lista. Grátis e online, sem cadastro."
summary: "Reúna e organize seus links em uma lista."
date: 2026-11-06
draft: false
category: "util"
tags: ["links", "organização", "produtividade"]
keywords: ["organizador de links", "organizador de links online", "links", "organização", "produtividade"]
---

Basta colar o link, escolher uma categoria e clicar em **Salvar Link**. Seus links ficam organizados abaixo, por categoria.

<div id="org-links" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔗 Organizador de Links</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Salve seus links favoritos em categorias e acesse quando precisar.</p>
<label for="org-url" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Link (URL)</label>
<input id="org-url" type="text" inputmode="url" placeholder="Ex.: https://www.exemplo.com.br" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="org-titulo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Título (opcional)</label>
<input id="org-titulo" type="text" placeholder="Ex.: Meu site favorito" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="org-categoria" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Categoria</label>
<select id="org-categoria" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="org-salvar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Salvar Link</button>
<button type="button" id="org-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="org-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="org-resultado">preencha o link e clique em "Salvar Link".</span></div>
<hr style="margin:24px 0;border:none;border-top:1px solid #c7d2fe;">
<label for="org-nova-cat" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Nova categoria</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<input id="org-nova-cat" type="text" placeholder="Ex.: Trabalho" autocomplete="off" style="flex:1;min-width:140px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<button type="button" id="org-add-cat" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Adicionar categoria</button>
</div>
<label for="org-busca" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Buscar nos seus links</label>
<input id="org-busca" type="text" placeholder="Digite parte do título ou do link" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div id="org-lista"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:16px;">
<button type="button" id="org-copiar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar lista</button>
<button type="button" id="org-apagar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#b91c1c;background:#ffffff;border:2px solid #fca5a5;border-radius:10px;cursor:pointer;">Apagar tudo</button>
</div>
</div>
<script>
(function () {
  var KEY = 'organizador-de-links-v1';
  var urlEl = document.getElementById('org-url');
  var tituloEl = document.getElementById('org-titulo');
  var catEl = document.getElementById('org-categoria');
  var novaCatEl = document.getElementById('org-nova-cat');
  var buscaEl = document.getElementById('org-busca');
  var listaEl = document.getElementById('org-lista');
  var resultado = document.getElementById('org-resultado');
  var caixa = document.getElementById('org-resposta');
  var dados = carregar();
  function carregar() {
    try {
      var raw = window.localStorage.getItem(KEY);
      if (raw) {
        var d = JSON.parse(raw);
        if (d && Array.isArray(d.cats) && Array.isArray(d.links) && d.cats.length > 0) { return d; }
      }
    } catch (e) {}
    return { cats: ['Geral'], links: [] };
  }
  function salvarDados() {
    try { window.localStorage.setItem(KEY, JSON.stringify(dados)); } catch (e) {}
  }
  function el(tag, estilo, texto) {
    var n = document.createElement(tag);
    if (estilo) { n.setAttribute('style', estilo); }
    if (texto !== undefined) { n.textContent = texto; }
    return n;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function ok(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = msg;
  }
  function neutro(msg) {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = msg;
  }
  function normalizarUrl(v) {
    var t = String(v).trim();
    if (t === '' || /\s/.test(t)) { return ''; }
    if (!/^https?:\/\//i.test(t)) { t = 'https://' + t; }
    try {
      var u = new URL(t);
      if (u.hostname.indexOf('.') === -1) { return ''; }
      return u.href;
    } catch (e) { return ''; }
  }
  function atualizarSelect() {
    var atual = catEl.value;
    while (catEl.firstChild) { catEl.removeChild(catEl.firstChild); }
    dados.cats.forEach(function (c) {
      var o = document.createElement('option');
      o.value = c;
      o.textContent = c;
      catEl.appendChild(o);
    });
    if (dados.cats.indexOf(atual) !== -1) { catEl.value = atual; }
  }
  function botaoPequeno(texto, cor) {
    return el('button', 'padding:6px 10px;font-size:0.85rem;font-weight:600;color:' + cor + ';background:#ffffff;border:1px solid #c7d2fe;border-radius:8px;cursor:pointer;', texto);
  }
  function renderizar() {
    atualizarSelect();
    while (listaEl.firstChild) { listaEl.removeChild(listaEl.firstChild); }
    var termo = buscaEl.value.trim().toLowerCase();
    dados.cats.forEach(function (cat) {
      var itens = dados.links.filter(function (l) {
        if (l.cat !== cat) { return false; }
        if (termo === '') { return true; }
        return (l.titulo + ' ' + l.url).toLowerCase().indexOf(termo) !== -1;
      });
      if (termo !== '' && itens.length === 0) { return; }
      var bloco = el('div', 'margin-bottom:16px;padding:14px;background:#ffffff;border:1px solid #c7d2fe;border-radius:12px;');
      var cab = el('div', 'display:flex;justify-content:space-between;align-items:center;gap:8px;margin-bottom:8px;');
      cab.appendChild(el('strong', 'color:#3730a3;font-size:1rem;', cat + ' (' + itens.length + ')'));
      if (dados.cats.length > 1) {
        var delCat = botaoPequeno('Excluir categoria', '#b91c1c');
        delCat.type = 'button';
        delCat.addEventListener('click', function () {
          if (window.confirm('Excluir a categoria "' + cat + '" e todos os links dela?')) {
            dados.cats = dados.cats.filter(function (c) { return c !== cat; });
            dados.links = dados.links.filter(function (l) { return l.cat !== cat; });
            salvarDados();
            renderizar();
            ok('categoria "' + cat + '" excluída.');
          }
        });
        cab.appendChild(delCat);
      }
      bloco.appendChild(cab);
      if (itens.length === 0) {
        bloco.appendChild(el('p', 'margin:0;font-size:0.9rem;color:#64748b;', 'Nenhum link nesta categoria.'));
      }
      itens.forEach(function (l) {
        var linha = el('div', 'display:flex;justify-content:space-between;align-items:center;gap:8px;padding:8px 0;border-top:1px solid #eef2ff;');
        var info = el('div', 'min-width:0;flex:1;');
        var a = el('a', 'display:block;font-weight:600;color:#4f46e5;text-decoration:none;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;', l.titulo);
        a.href = l.url;
        a.target = '_blank';
        a.rel = 'noopener noreferrer';
        info.appendChild(a);
        info.appendChild(el('small', 'display:block;color:#64748b;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;', l.url));
        var del = botaoPequeno('Remover', '#b91c1c');
        del.type = 'button';
        del.addEventListener('click', function () {
          dados.links = dados.links.filter(function (x) { return x.id !== l.id; });
          salvarDados();
          renderizar();
          ok('link removido.');
        });
        linha.appendChild(info);
        linha.appendChild(del);
        bloco.appendChild(linha);
      });
      listaEl.appendChild(bloco);
    });
  }
  function salvarLink() {
    var url = normalizarUrl(urlEl.value);
    if (url === '') { erro('informe um link válido, por exemplo https://www.exemplo.com.br.'); return; }
    var titulo = tituloEl.value.trim();
    if (titulo === '') { titulo = url.replace(/^https?:\/\//i, '').replace(/\/$/, ''); }
    var cat = catEl.value;
    var repetido = dados.links.some(function (l) { return l.url === url; });
    dados.links.push({ id: String(Date.now()) + String(Math.random()).slice(2, 8), url: url, titulo: titulo, cat: cat });
    salvarDados();
    urlEl.value = '';
    tituloEl.value = '';
    renderizar();
    ok(repetido ? 'link salvo em "' + cat + '" (atenção: ele já estava na sua lista).' : 'link salvo em "' + cat + '".');
    urlEl.focus();
  }
  function adicionarCategoria() {
    var nome = novaCatEl.value.trim();
    if (nome === '') { erro('digite o nome da nova categoria.'); return; }
    var existe = dados.cats.some(function (c) { return c.toLowerCase() === nome.toLowerCase(); });
    if (existe) { erro('essa categoria já existe.'); return; }
    dados.cats.push(nome);
    salvarDados();
    novaCatEl.value = '';
    renderizar();
    catEl.value = nome;
    ok('categoria "' + nome + '" criada.');
  }
  function textoLista() {
    var partes = [];
    dados.cats.forEach(function (cat) {
      var itens = dados.links.filter(function (l) { return l.cat === cat; });
      if (itens.length > 0) {
        partes.push(cat);
        itens.forEach(function (l) { partes.push('- ' + l.titulo + ': ' + l.url); });
        partes.push('');
      }
    });
    return partes.join('\n').trim();
  }
  function copiarLista() {
    var texto = textoLista();
    if (texto === '') { erro('você ainda não tem links para copiar.'); return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(function () {
        ok('lista copiada para a área de transferência.');
      }, function () {
        erro('não foi possível copiar automaticamente.');
      });
    } else {
      erro('seu navegador não permite copiar automaticamente.');
    }
  }
  function apagarTudo() {
    if (window.confirm('Apagar todos os links e categorias?')) {
      dados = { cats: ['Geral'], links: [] };
      salvarDados();
      renderizar();
      neutro('tudo foi apagado. Preencha o link e clique em "Salvar Link".');
    }
  }
  function limpar() {
    urlEl.value = '';
    tituloEl.value = '';
    buscaEl.value = '';
    renderizar();
    neutro('preencha o link e clique em "Salvar Link".');
    urlEl.focus();
  }
  document.getElementById('org-salvar').addEventListener('click', salvarLink);
  document.getElementById('org-limpar').addEventListener('click', limpar);
  document.getElementById('org-add-cat').addEventListener('click', adicionarCategoria);
  document.getElementById('org-copiar').addEventListener('click', copiarLista);
  document.getElementById('org-apagar').addEventListener('click', apagarTudo);
  buscaEl.addEventListener('input', renderizar);
  [urlEl, tituloEl].forEach(function (e1) {
    e1.addEventListener('keydown', function (ev) { if (ev.key === 'Enter') { salvarLink(); } });
  });
  novaCatEl.addEventListener('keydown', function (ev) { if (ev.key === 'Enter') { adicionarCategoria(); } });
  [urlEl, tituloEl, novaCatEl, buscaEl, catEl].forEach(function (e2) {
    e2.addEventListener('focus', function () { e2.style.borderColor = '#6366f1'; });
    e2.addEventListener('blur', function () { e2.style.borderColor = '#c7d2fe'; });
  });
  renderizar();
})();
</script>

## Como usar o organizador de links

1. Cole o endereço do site no campo **Link (URL)**. Se você esquecer o `https://`, ele é adicionado automaticamente.
2. Se quiser, digite um **Título** para identificar o link. Sem título, o próprio endereço é usado como nome.
3. Escolha a **Categoria** em que o link será guardado.
4. Clique em **Salvar Link** (ou pressione Enter). O link aparece na lista abaixo, dentro da categoria escolhida.
5. Para criar uma categoria nova, digite o nome em **Nova categoria** e clique em **Adicionar categoria**.
6. Use o campo **Buscar nos seus links** para filtrar a lista pelo título ou pelo endereço.
7. Clique em **Copiar lista** para copiar todos os links organizados por categoria, ou em **Remover** para excluir um link específico.

Seus links ficam salvos no próprio navegador do aparelho que você está usando, sem necessidade de cadastro. Se você limpar os dados do navegador ou trocar de aparelho, a lista não será carregada automaticamente, então use **Copiar lista** para guardar uma cópia.

## Entendendo os termos

- **Link (URL):** endereço de uma página na internet, como `https://www.exemplo.com.br`. É o que você digita no navegador para acessar um site.
- **Título:** nome que você dá ao link para reconhecê-lo com facilidade na lista.
- **Categoria:** grupo em que os links são organizados por assunto, como Trabalho, Estudos ou Lazer.
- **Organizador de links:** ferramenta que reúne vários endereços em um só lugar, separados por categorias.
- **Busca:** filtro que mostra apenas os links cujo título ou endereço contém o texto digitado.
- **Copiar lista:** recurso que copia todos os seus links, agrupados por categoria, para colar em outro lugar.
- **Armazenamento local:** espaço do navegador onde os links são guardados no seu aparelho, sem enviar nada para um servidor.