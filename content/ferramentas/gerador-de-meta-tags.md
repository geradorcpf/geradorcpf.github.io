---
title: "Gerador de Meta Tags"
seoTitle: "Gerador de Meta Tags"
description: "Gerador de Meta Tags: monte as meta tags de título, descrição e redes sociais. Grátis e online, sem cadastro."
summary: "Monte as meta tags de título, descrição e redes sociais."
date: 2026-11-02
draft: false
category: "dev"
tags: ["meta tags", "seo", "html", "desenvolvimento"]
keywords: ["gerador de meta tags", "gerador de meta tags online", "meta tags", "seo", "html"]
---

Basta preencher os campos abaixo e depois clicar em **Gerar Meta Tags**. O contador de caracteres ajuda a manter cada campo no tamanho ideal para o SEO.

<div id="calc-metatags" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏷️ Gerador de Meta Tags</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Preencha os campos e gere o código para colocar no head do seu site.</p>
<label for="mt-titulo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Título do site</label>
<input id="mt-titulo" type="text" placeholder="Ex.: Gerador Meta Tag" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div id="mt-titulo-cont" style="margin-bottom:16px;font-size:0.85rem;color:#64748b;">0 caracteres (ideal até 63)</div>
<label for="mt-autor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Meta Tag - Autor</label>
<input id="mt-autor" type="text" placeholder="Ex.: Seu Nome" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div id="mt-autor-cont" style="margin-bottom:16px;font-size:0.85rem;color:#64748b;">0 caracteres</div>
<label for="mt-keywords" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Meta Tag - Keywords</label>
<input id="mt-keywords" type="text" placeholder="Ex.: gerador meta tag, meta autor, seo" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div id="mt-keywords-cont" style="margin-bottom:16px;font-size:0.85rem;color:#64748b;">0 caracteres (sugestão até 200, separe por vírgula)</div>
<label for="mt-descricao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Meta Tag - Description</label>
<textarea id="mt-descricao" rows="4" placeholder="Ex.: Gera as meta tags do seu site contando os caracteres." style="width:100%;padding:12px 14px;margin-bottom:6px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div id="mt-descricao-cont" style="margin-bottom:20px;font-size:0.85rem;color:#64748b;">0 caracteres (ideal até 160)</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="mt-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Meta Tags</button>
<button type="button" id="mt-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="mt-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="mt-resultado">preencha os campos e clique em "Gerar Meta Tags".</span>
<textarea id="mt-codigo" rows="8" readonly style="display:none;width:100%;margin-top:12px;padding:12px 14px;font-size:0.9rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#f8fafc;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="mt-copiar" style="display:none;margin-top:10px;padding:11px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar código</button>
</div>
</div>
<script>
(function () {
  var LT = '\x3c';
  var GT = '\x3e';
  var AMP = '\x26';
  var titulo = document.getElementById('mt-titulo');
  var autor = document.getElementById('mt-autor');
  var keywords = document.getElementById('mt-keywords');
  var descricao = document.getElementById('mt-descricao');
  var contTitulo = document.getElementById('mt-titulo-cont');
  var contAutor = document.getElementById('mt-autor-cont');
  var contKeywords = document.getElementById('mt-keywords-cont');
  var contDescricao = document.getElementById('mt-descricao-cont');
  var caixa = document.getElementById('mt-resposta');
  var resultado = document.getElementById('mt-resultado');
  var codigo = document.getElementById('mt-codigo');
  var copiar = document.getElementById('mt-copiar');
  function esc(s) {
    return String(s)
      .replace(/\x26/g, AMP + 'amp;')
      .replace(/\x3c/g, AMP + 'lt;')
      .replace(/\x3e/g, AMP + 'gt;')
      .replace(/"/g, AMP + 'quot;');
  }
  function contar(campo, saida, ideal, maximo, dica) {
    var n = campo.value.length;
    var cor = '#64748b';
    if (ideal) {
      cor = '#166534';
      if (n > ideal) { cor = '#b45309'; }
      if (n > maximo) { cor = '#b91c1c'; }
    }
    saida.style.color = cor;
    saida.textContent = n + (n === 1 ? ' caractere' : ' caracteres') + dica;
  }
  function atualizar() {
    contar(titulo, contTitulo, 63, 90, ' (ideal até 63)');
    contar(autor, contAutor, 0, 0, '');
    contar(keywords, contKeywords, 200, 200, ' (sugestão até 200, separe por vírgula)');
    contar(descricao, contDescricao, 160, 250, ' (ideal até 160)');
  }
  function aviso(msg, ok) {
    caixa.style.borderColor = ok ? '#86efac' : '#fca5a5';
    caixa.style.background = ok ? '#f0fdf4' : '#fef2f2';
    resultado.style.color = ok ? '#166534' : '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar() {
    var t = titulo.value.trim();
    var a = autor.value.trim();
    var d = descricao.value.replace(/\s+/g, ' ').trim();
    var k = keywords.value.split(',').map(function (x) { return x.trim(); }).filter(function (x) { return x.length > 0; }).join(', ');
    if (t === '') {
      codigo.style.display = 'none';
      copiar.style.display = 'none';
      aviso('informe pelo menos o título do site.', false);
      return;
    }
    var linhas = [];
    linhas.push(LT + 'head' + GT);
    linhas.push(LT + 'title' + GT + esc(t) + LT + '/title' + GT);
    if (a !== '') { linhas.push(LT + 'meta name="author" content="' + esc(a) + '" /' + GT); }
    if (k !== '') { linhas.push(LT + 'meta name="keywords" content="' + esc(k) + '" /' + GT); }
    if (d !== '') { linhas.push(LT + 'meta name="description" content="' + esc(d) + '" /' + GT); }
    linhas.push(LT + '/head' + GT);
    codigo.value = linhas.join('\n');
    codigo.style.display = 'block';
    copiar.style.display = 'inline-block';
    copiar.textContent = 'Copiar código';
    aviso('meta tags geradas! Copie o código abaixo e cole dentro do head da sua página.', true);
  }
  function copiarCodigo() {
    var feito = function () { copiar.textContent = 'Copiado!'; };
    codigo.select();
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(codigo.value).then(feito, function () {
        document.execCommand('copy');
        feito();
      });
    } else {
      document.execCommand('copy');
      feito();
    }
  }
  function limpar() {
    titulo.value = '';
    autor.value = '';
    keywords.value = '';
    descricao.value = '';
    codigo.value = '';
    codigo.style.display = 'none';
    copiar.style.display = 'none';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Gerar Meta Tags".';
    atualizar();
    titulo.focus();
  }
  document.getElementById('mt-gerar').addEventListener('click', gerar);
  document.getElementById('mt-limpar').addEventListener('click', limpar);
  copiar.addEventListener('click', copiarCodigo);
  [titulo, autor, keywords, descricao].forEach(function (el) {
    el.addEventListener('input', atualizar);
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  [titulo, autor, keywords].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  });
  atualizar();
})();
</script>

## Como usar o gerador

1. Digite o **Título do site** no primeiro campo. Ele é obrigatório e aparece na aba do navegador e nos resultados de busca.
2. Se quiser, informe o nome do responsável no campo **Meta Tag - Autor**.
3. Preencha o campo **Meta Tag - Keywords** com as palavras-chave separadas por vírgula.
4. Escreva um resumo da página no campo **Meta Tag - Description**.
5. Acompanhe o contador abaixo de cada campo: verde indica tamanho ideal, laranja indica que passou do recomendado e vermelho indica excesso.
6. Clique em **Gerar Meta Tags** (ou pressione Enter) para ver o código pronto.
7. Use **Copiar código** e cole o resultado dentro da tag `head` do seu HTML.
8. Use o botão **Limpar** para apagar os campos e começar de novo.

Campos deixados em branco (exceto o título) simplesmente não entram no código gerado.

## Entendendo os termos

- **Meta tag:** linha de código HTML, colocada no `head` da página, que passa informações sobre ela para navegadores e buscadores sem aparecer na tela.
- **Head:** parte do HTML que guarda as informações da página, como título e meta tags. O conteúdo do `head` não é exibido no corpo do site.
- **Título (title):** nome da página exibido na aba do navegador e como link principal nos resultados do Google. O Google costuma mostrar até cerca de 63 caracteres.
- **Autor (author):** meta tag que identifica quem criou ou é responsável pelo conteúdo da página.
- **Keywords:** lista de palavras-chave relacionadas ao tema da página, separadas por vírgula. Os buscadores atuais dão pouco peso a ela, mas ainda é usada por alguns sistemas.
- **Description:** resumo da página que costuma aparecer abaixo do título nos resultados de busca. O Google costuma exibir até cerca de 160 caracteres.
- **Contador de caracteres:** indicador que mostra quantas letras, números e espaços já foram digitados em cada campo.
- **SEO:** conjunto de práticas para melhorar a posição de um site nos resultados de busca, como o Google.

## Exemplo de resultado

Para o título "Gerador Meta Tag", autor "Seu Nome", keywords "gerador meta tag, meta autor, meta keywords" e uma descrição curta, o código gerado fica assim:

```html
<head>
<title>Gerador Meta Tag</title>
<meta name="author" content="Seu Nome" />
<meta name="keywords" content="gerador meta tag, meta autor, meta keywords" />
<meta name="description" content="Gera as meta tags do seu site contando os caracteres para facilitar sua vida" />
</head>
```