---
title: "Gerador de Texto Lorem Ipsum"
seoTitle: "Gerador de Texto Lorem Ipsum"
description: "Gerador de Texto Lorem Ipsum: gere texto Lorem Ipsum para layouts e protótipos. Grátis e online, sem cadastro."
summary: "Gere texto Lorem Ipsum para layouts e protótipos."
date: 2026-11-03
draft: false
category: "dev"
tags: ["lorem ipsum", "placeholder", "texto", "design", "dados de teste"]
keywords: ["gerador de texto lorem ipsum", "gerador de texto lorem ipsum online", "lorem ipsum", "placeholder", "texto"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher as opções abaixo e depois clicar em **Gerar Texto**.

<div id="calc-lorem" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📝 Gerador de Texto Lorem Ipsum</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere o texto na hora.</p>
<label for="lip-qtd" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade</label>
<input id="lip-qtd" type="text" inputmode="numeric" placeholder="Ex.: 3" value="3" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div id="lip-t-unidade" style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar em</div>
<div role="radiogroup" aria-labelledby="lip-t-unidade" style="margin-bottom:16px;">
<label style="display:inline-flex;align-items:center;gap:6px;margin-right:18px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="lip-unidade" value="paragrafos" checked style="accent-color:#4f46e5;"> Parágrafos</label>
<label style="display:inline-flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="lip-unidade" value="palavras" style="accent-color:#4f46e5;"> Palavras</label>
</div>
<div id="lip-t-tipo" style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo de Texto</div>
<div role="radiogroup" aria-labelledby="lip-t-tipo" style="margin-bottom:16px;">
<label style="display:inline-flex;align-items:center;gap:6px;margin-right:18px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="lip-tipo" value="texto" checked style="accent-color:#4f46e5;"> Texto</label>
<label style="display:inline-flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="lip-tipo" value="html" style="accent-color:#4f46e5;"> HTML</label>
</div>
<div id="lip-t-inicio" style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Iniciar texto com "Lorem Ipsum"</div>
<div role="radiogroup" aria-labelledby="lip-t-inicio" style="margin-bottom:20px;">
<label style="display:inline-flex;align-items:center;gap:6px;margin-right:18px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="lip-inicio" value="sim" checked style="accent-color:#4f46e5;"> Sim</label>
<label style="display:inline-flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="lip-inicio" value="nao" style="accent-color:#4f46e5;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="lip-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Texto</button>
<button type="button" id="lip-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="lip-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="lip-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="lip-resultado">escolha as opções e clique em "Gerar Texto".</span><textarea id="lip-saida" readonly rows="9" aria-label="Texto Lorem Ipsum gerado" style="display:none;width:100%;margin-top:12px;padding:12px 14px;font-size:0.9rem;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;resize:vertical;font-family:inherit;"></textarea></div>
</div>
<script>
(function () {
  var qtd = document.getElementById('lip-qtd');
  var saida = document.getElementById('lip-saida');
  var resultado = document.getElementById('lip-resultado');
  var caixa = document.getElementById('lip-resposta');
  var BASE = ('lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua enim ad minim veniam quis nostrud exercitation ullamco laboris nisi aliquip ex ea commodo consequat duis aute irure in reprehenderit voluptate velit esse cillum eu fugiat nulla pariatur excepteur sint occaecat cupidatat non proident sunt culpa qui officia deserunt mollit anim id est laborum').split(' ');
  var INICIO = ['lorem', 'ipsum', 'dolor', 'sit', 'amet', 'consectetur', 'adipiscing', 'elit'];
  var ABRE_P = '\u003cp\u003e';
  var FECHA_P = '\u003c/p\u003e';
  function rnd(a, b) { return a + Math.floor(Math.random() * (b - a + 1)); }
  function palavra() { return BASE[rnd(0, BASE.length - 1)]; }
  function maiuscula(s) { return s.charAt(0).toUpperCase() + s.slice(1); }
  function escolha(nome) {
    var el = document.querySelector('input[name="' + nome + '"]:checked');
    return el ? el.value : '';
  }
  function frase() {
    var n = rnd(8, 16), w = [], i, p;
    for (i = 0; n > i; i++) { w.push(palavra()); }
    p = rnd(3, n - 3);
    w[p] = w[p] + ',';
    return maiuscula(w.join(' ')) + '.';
  }
  function paragrafo(primeiro, inicio) {
    var n = rnd(4, 7), f = [], i;
    if (primeiro && inicio) {
      f.push('Lorem ipsum dolor sit amet, consectetur adipiscing elit.');
      i = 1;
    } else {
      i = 0;
    }
    for (; n > i; i++) { f.push(frase()); }
    var t = f.join(' ');
    if (!inicio) { t = t.replace(/^Lorem/, 'Dolor'); }
    return t;
  }
  function textoPalavras(n, inicio) {
    var w = inicio ? INICIO.slice(0, n) : [];
    var out = [], novaFrase = true, restante = rnd(8, 16), i, p;
    while (n > w.length) { w.push(palavra()); }
    if (!inicio && w[0] === 'lorem') { w[0] = 'consequat'; }
    for (i = 0; n > i; i++) {
      p = w[i];
      if (novaFrase) { p = maiuscula(p); novaFrase = false; }
      restante--;
      if (i === n - 1 || restante === 0) {
        p = p + '.';
        novaFrase = true;
        restante = rnd(8, 16);
      } else if (i > 2 && n - i > 3 && rnd(1, 6) === 1) {
        p = p + ',';
      }
      out.push(p);
    }
    return out.join(' ');
  }
  function mostrarSaida(texto) {
    saida.value = texto;
    saida.style.display = 'block';
  }
  function esconderSaida() {
    saida.value = '';
    saida.style.display = 'none';
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
  function gerar() {
    var txt = qtd.value.trim();
    var unidade = escolha('lip-unidade');
    var tipo = escolha('lip-tipo');
    var inicio = escolha('lip-inicio') === 'sim';
    var max = unidade === 'paragrafos' ? 100 : 5000;
    var n, i, partes = [], texto;
    if (!/^\d+$/.test(txt)) { esconderSaida(); erro('informe uma quantidade válida (número inteiro).'); return; }
    n = parseInt(txt, 10);
    if (1 > n || n > max) { esconderSaida(); erro('a quantidade deve estar entre 1 e ' + max + '.'); return; }
    if (unidade === 'paragrafos') {
      for (i = 0; n > i; i++) { partes.push(paragrafo(i === 0, inicio)); }
      if (tipo === 'html') {
        texto = partes.map(function (p) { return ABRE_P + p + FECHA_P; }).join('\n');
      } else {
        texto = partes.join('\n\n');
      }
    } else {
      texto = textoPalavras(n, inicio);
      if (tipo === 'html') { texto = ABRE_P + texto + FECHA_P; }
    }
    mostrarSaida(texto);
    sucesso('texto gerado com ' + n + (unidade === 'paragrafos' ? (n === 1 ? ' parágrafo' : ' parágrafos') : (n === 1 ? ' palavra' : ' palavras')) + (tipo === 'html' ? ' (HTML).' : ' (texto).'));
  }
  function copiar() {
    if (!saida.value) { erro('gere um texto primeiro para poder copiá-lo.'); return; }
    function ok() { sucesso('texto copiado para a área de transferência!'); }
    function alternativa() {
      saida.focus();
      saida.select();
      try { document.execCommand('copy'); ok(); } catch (e) { erro('não foi possível copiar. Selecione o texto e copie manualmente.'); }
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(saida.value).then(ok, alternativa);
    } else {
      alternativa();
    }
  }
  function limpar() {
    qtd.value = '3';
    document.querySelector('input[name="lip-unidade"][value="paragrafos"]').checked = true;
    document.querySelector('input[name="lip-tipo"][value="texto"]').checked = true;
    document.querySelector('input[name="lip-inicio"][value="sim"]').checked = true;
    esconderSaida();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'escolha as opções e clique em "Gerar Texto".';
    qtd.focus();
  }
  document.getElementById('lip-gerar').addEventListener('click', gerar);
  document.getElementById('lip-copiar').addEventListener('click', copiar);
  document.getElementById('lip-limpar').addEventListener('click', limpar);
  qtd.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  qtd.addEventListener('focus', function () { qtd.style.borderColor = '#6366f1'; });
  qtd.addEventListener('blur', function () { qtd.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Digite a **Quantidade** de texto que você precisa no primeiro campo.
2. Escolha se deseja gerar em **Parágrafos** ou em **Palavras**.
3. Escolha o **Tipo de Texto**: **Texto** (puro) ou **HTML** (com as tags `p`).
4. Informe se o texto deve **iniciar com "Lorem Ipsum"** (Sim ou Não).
5. Clique em **Gerar Texto** (ou pressione Enter) para ver o resultado.
6. Clique em **Copiar** para levar o texto para a área de transferência e cole onde precisar.
7. Use o botão **Limpar** para voltar às opções iniciais e fazer uma nova geração.

Você pode gerar de 1 a 100 parágrafos ou de 1 a 5.000 palavras por vez. A cada clique o texto é sorteado de novo, então o resultado muda a cada geração.

## Entendendo os termos

- **Lorem Ipsum:** texto fictício em latim usado há séculos pela indústria gráfica e tipográfica. As palavras não formam um sentido coerente, mas imitam o ritmo de um texto real.
- **Placeholder:** conteúdo provisório que ocupa o lugar do texto definitivo até que ele fique pronto.
- **Layout:** organização visual de uma página ou tela, com a posição de títulos, textos, imagens e botões.
- **Protótipo:** versão preliminar de um site, app ou material gráfico, usada para testar o design antes da versão final.
- **Parágrafo:** bloco de texto formado por várias frases. Aqui, cada parágrafo gerado tem de 4 a 7 frases.
- **Palavra:** unidade do texto separada por espaços. Na opção Palavras, você define exatamente quantas quer.
- **Texto:** formato puro, sem marcações, pronto para colar em editores, ferramentas de design e documentos.
- **HTML:** formato com as marcações de página web. Cada parágrafo sai dentro de uma tag `p`, pronto para colar no código.
- **Iniciar com "Lorem Ipsum":** quando marcado como Sim, o texto começa com a frase clássica "Lorem ipsum dolor sit amet, consectetur adipiscing elit".
- **Dados de teste:** informações fictícias usadas para verificar se um sistema ou layout funciona corretamente.