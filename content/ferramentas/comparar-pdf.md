---
title: "Comparar PDF"
seoTitle: "Comparar PDF: online e grátis"
description: "Comparar PDF: compare dois PDFs e veja o que mudou. Grátis e online, sem cadastro."
summary: "Compare dois PDFs e veja o que mudou."
date: 2026-10-24
draft: false
category: "midia"
tags: ["pdf", "edição de pdf", "comparação"]
keywords: ["comparar pdf", "comparar pdf online", "pdf", "edição de pdf", "comparação"]
---
<!--sudah dikerjakan-->

Basta selecionar os dois arquivos PDF abaixo e depois clicar em **Comparar PDFs**.

<div id="calc-comparar-pdf" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Comparar PDF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha dois PDFs e veja o que mudou no texto.</p>
<label for="cmp-pdf-a" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">PDF Original</label>
<input id="cmp-pdf-a" type="file" accept="application/pdf,.pdf" style="width:100%;padding:10px 12px;margin-bottom:16px;font-size:0.95rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="cmp-pdf-b" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">PDF Modificado</label>
<input id="cmp-pdf-b" type="file" accept="application/pdf,.pdf" style="width:100%;padding:10px 12px;margin-bottom:16px;font-size:0.95rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label style="display:block;margin-bottom:8px;font-size:0.95rem;cursor:pointer;"><input id="cmp-ignorar-caixa" type="checkbox" style="margin-right:8px;"> Ignorar maiúsculas e minúsculas</label>
<label style="display:block;margin-bottom:20px;font-size:0.95rem;cursor:pointer;"><input id="cmp-mostrar-iguais" type="checkbox" style="margin-right:8px;"> Mostrar linhas iguais</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cmp-comparar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Comparar PDFs</button>
<button type="button" id="cmp-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cmp-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cmp-resultado">selecione os dois PDFs e clique em "Comparar PDFs".</span><div id="cmp-diff" style="margin-top:12px;max-height:420px;overflow:auto;"></div></div>
</div>
<script>
(function () {
  var PDFJS_URL = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js';
  var WORKER_URL = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  var inA = document.getElementById('cmp-pdf-a');
  var inB = document.getElementById('cmp-pdf-b');
  var chkCaixa = document.getElementById('cmp-ignorar-caixa');
  var chkIguais = document.getElementById('cmp-mostrar-iguais');
  var btnComparar = document.getElementById('cmp-comparar');
  var btnLimpar = document.getElementById('cmp-limpar');
  var caixa = document.getElementById('cmp-resposta');
  var resultado = document.getElementById('cmp-resultado');
  var diffBox = document.getElementById('cmp-diff');
  var ultimo = null;
  var ocupado = false;
  function estado(tipo, msg) {
    var cores = {
      neutro: ['#c7d2fe', '#ffffff', '#64748b'],
      ok: ['#86efac', '#f0fdf4', '#166534'],
      dif: ['#fcd34d', '#fffbeb', '#92400e'],
      erro: ['#fca5a5', '#fef2f2', '#b91c1c']
    };
    var c = cores[tipo];
    caixa.style.borderColor = c[0];
    caixa.style.background = c[1];
    resultado.style.color = c[2];
    resultado.textContent = msg;
  }
  function carregarPdfJs() {
    return new Promise(function (resolve, reject) {
      if (window.pdfjsLib) { resolve(); return; }
      var s = document.createElement('script');
      s.src = PDFJS_URL;
      s.onload = function () {
        if (!window.pdfjsLib) { reject(new Error('pdfjs')); return; }
        window.pdfjsLib.GlobalWorkerOptions.workerSrc = WORKER_URL;
        resolve();
      };
      s.onerror = function () { reject(new Error('pdfjs')); };
      document.head.appendChild(s);
    });
  }
  function limparTexto(t) {
    return String(t).replace(/\s+/g, ' ').trim();
  }
  async function lerPdf(arquivo) {
    var buf = await arquivo.arrayBuffer();
    var pdf = await window.pdfjsLib.getDocument({ data: buf }).promise;
    var linhas = [];
    function empurrar(txt) {
      var l = limparTexto(txt);
      if (l !== '') { linhas.push(l); }
    }
    for (var p = 1; pdf.numPages >= p; p++) {
      var pagina = await pdf.getPage(p);
      var conteudo = await pagina.getTextContent();
      var atual = '';
      var ultimoY = null;
      conteudo.items.forEach(function (it) {
        if (typeof it.str !== 'string') { return; }
        var y = it.transform[5];
        if (ultimoY !== null && Math.abs(y - ultimoY) > 3) {
          empurrar(atual);
          atual = '';
        }
        atual += it.str;
        ultimoY = y;
        if (it.hasEOL) {
          empurrar(atual);
          atual = '';
          ultimoY = null;
        }
      });
      empurrar(atual);
    }
    return { linhas: linhas, paginas: pdf.numPages };
  }
  function chave(t) {
    var k = limparTexto(t);
    return chkCaixa.checked ? k.toLowerCase() : k;
  }
  function diffSeq(kx, ky) {
    var ops = [];
    var n = kx.length;
    var m = ky.length;
    var s = 0;
    var e = 0;
    var i;
    var j;
    var k;
    while (n > s && m > s && kx[s] === ky[s]) { s++; }
    while (n - e > s && m - e > s && kx[n - 1 - e] === ky[m - 1 - e]) { e++; }
    var N = n - s - e;
    var M = m - s - e;
    if (N * M > 16000000) { return null; }
    var t = [];
    for (i = 0; N >= i; i++) { t.push(new Uint16Array(M + 1)); }
    for (i = N - 1; i >= 0; i--) {
      for (j = M - 1; j >= 0; j--) {
        if (kx[s + i] === ky[s + j]) {
          t[i][j] = t[i + 1][j + 1] + 1;
        } else {
          t[i][j] = t[i + 1][j] >= t[i][j + 1] ? t[i + 1][j] : t[i][j + 1];
        }
      }
    }
    for (k = 0; s > k; k++) { ops.push(['=', k, k]); }
    i = 0;
    j = 0;
    while (N > i && M > j) {
      if (kx[s + i] === ky[s + j]) {
        ops.push(['=', s + i, s + j]);
        i++;
        j++;
      } else if (t[i + 1][j] >= t[i][j + 1]) {
        ops.push(['-', s + i, -1]);
        i++;
      } else {
        ops.push(['+', -1, s + j]);
        j++;
      }
    }
    while (N > i) { ops.push(['-', s + i, -1]); i++; }
    while (M > j) { ops.push(['+', -1, s + j]); j++; }
    for (k = 0; e > k; k++) { ops.push(['=', n - e + k, m - e + k]); }
    return ops;
  }
  function diffPalavras(a, b) {
    var ta = a.split(' ');
    var tb = b.split(' ');
    var ca = ta.map(function () { return true; });
    var cb = tb.map(function () { return true; });
    var ops = diffSeq(ta.map(chave), tb.map(chave));
    if (ops) {
      ops.forEach(function (op) {
        if (op[0] === '=') { ca[op[1]] = false; cb[op[2]] = false; }
      });
    }
    return {
      a: ta.map(function (w, idx) { return { t: w, c: ca[idx] }; }),
      b: tb.map(function (w, idx) { return { t: w, c: cb[idx] }; })
    };
  }
  function linha(tipo, partes) {
    var estilos = {
      '-': ['#fef2f2', '#fca5a5', '#b91c1c', '#fecaca'],
      '+': ['#f0fdf4', '#86efac', '#166534', '#bbf7d0'],
      '=': ['#f8fafc', '#e2e8f0', '#475569', '#e2e8f0']
    };
    var c = estilos[tipo];
    var d = document.createElement('div');
    d.style.cssText = 'padding:6px 10px;margin-bottom:4px;border-left:4px solid ' + c[1] + ';border-radius:6px;background:' + c[0] + ';color:' + c[2] + ';font-size:0.9rem;line-height:1.5;word-break:break-word;';
    var sinal = document.createElement('strong');
    sinal.textContent = (tipo === '-' ? '−' : (tipo === '+' ? '+' : '=')) + ' ';
    d.appendChild(sinal);
    partes.forEach(function (p, idx) {
      var sp = document.createElement('span');
      sp.textContent = p.t;
      if (p.c) { sp.style.cssText = 'font-weight:700;background:' + c[3] + ';border-radius:3px;padding:0 2px;'; }
      d.appendChild(sp);
      if (partes.length - 1 > idx && p.sep !== false) { d.appendChild(document.createTextNode(' ')); }
    });
    return d;
  }
  function desenhar() {
    if (!ultimo) { return; }
    var mostrarIguais = chkIguais.checked;
    var la = ultimo.a.linhas;
    var lb = ultimo.b.linhas;
    var ops = ultimo.ops;
    var removidas = 0;
    var adicionadas = 0;
    var k = 0;
    diffBox.textContent = '';
    while (ops.length > k) {
      var op = ops[k];
      if (op[0] === '=') {
        if (mostrarIguais) { diffBox.appendChild(linha('=', [{ t: la[op[1]], c: false }])); }
        k++;
        continue;
      }
      var rem = [];
      var add = [];
      while (ops.length > k && ops[k][0] !== '=') {
        if (ops[k][0] === '-') { rem.push(ops[k][1]); } else { add.push(ops[k][2]); }
        k++;
      }
      var pares = Math.min(rem.length, add.length);
      var remPartes = [];
      var addPartes = [];
      var q;
      for (q = 0; rem.length > q; q++) {
        if (pares > q) {
          var wd = diffPalavras(la[rem[q]], lb[add[q]]);
          remPartes.push(wd.a);
          addPartes.push(wd.b);
        } else {
          remPartes.push([{ t: la[rem[q]], c: false }]);
        }
      }
      for (q = pares; add.length > q; q++) {
        addPartes.push([{ t: lb[add[q]], c: false }]);
      }
      remPartes.forEach(function (p) { diffBox.appendChild(linha('-', p)); });
      addPartes.forEach(function (p) { diffBox.appendChild(linha('+', p)); });
      removidas += rem.length;
      adicionadas += add.length;
    }
    if (removidas === 0 && adicionadas === 0) {
      estado('ok', 'os dois PDFs têm o mesmo texto (' + ultimo.a.paginas + ' e ' + ultimo.b.paginas + ' páginas).');
    } else {
      estado('dif', 'foram encontradas ' + removidas + ' linha(s) removida(s) e ' + adicionadas + ' linha(s) adicionada(s).');
    }
  }
  function ehPdf(f) {
    return f.type === 'application/pdf' || /\.pdf$/i.test(f.name);
  }
  async function comparar() {
    if (ocupado) { return; }
    var fa = inA.files[0];
    var fb = inB.files[0];
    diffBox.textContent = '';
    ultimo = null;
    if (!fa || !fb) { estado('erro', 'selecione os dois arquivos PDF.'); return; }
    if (!ehPdf(fa) || !ehPdf(fb)) { estado('erro', 'os dois arquivos precisam estar no formato PDF.'); return; }
    ocupado = true;
    btnComparar.disabled = true;
    estado('neutro', 'lendo e comparando os PDFs...');
    try {
      await carregarPdfJs();
      var a = await lerPdf(fa);
      var b = await lerPdf(fb);
      if (a.linhas.length === 0 && b.linhas.length === 0) {
        estado('erro', 'não foi encontrado texto nos PDFs. Arquivos escaneados (imagens) não são suportados.');
        return;
      }
      var ops = diffSeq(a.linhas.map(chave), b.linhas.map(chave));
      if (!ops) {
        estado('erro', 'os documentos são grandes demais para serem comparados aqui.');
        return;
      }
      ultimo = { a: a, b: b, ops: ops };
      desenhar();
    } catch (err) {
      estado('erro', 'não foi possível ler os PDFs. Verifique se os arquivos não estão protegidos por senha ou corrompidos.');
    } finally {
      ocupado = false;
      btnComparar.disabled = false;
    }
  }
  function limpar() {
    inA.value = '';
    inB.value = '';
    chkCaixa.checked = false;
    chkIguais.checked = false;
    ultimo = null;
    diffBox.textContent = '';
    estado('neutro', 'selecione os dois PDFs e clique em "Comparar PDFs".');
  }
  btnComparar.addEventListener('click', comparar);
  btnLimpar.addEventListener('click', limpar);
  chkIguais.addEventListener('change', desenhar);
  chkCaixa.addEventListener('change', function () { if (ultimo) { comparar(); } });
  [inA, inB].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Clique no primeiro campo e selecione o **PDF Original**, ou seja, a versão mais antiga do documento.
2. Clique no segundo campo e selecione o **PDF Modificado**, ou seja, a versão mais nova.
3. Se quiser, marque **Ignorar maiúsculas e minúsculas** para que mudanças apenas de caixa não sejam contadas como diferença.
4. Clique em **Comparar PDFs** e aguarde a leitura dos arquivos.
5. Veja o resultado: linhas em vermelho (−) foram removidas e linhas em verde (+) foram adicionadas. As palavras alteradas aparecem em destaque.
6. Marque **Mostrar linhas iguais** para ver também o texto que não mudou, e use o botão **Limpar** para começar uma nova comparação.

A comparação é feita no seu próprio navegador, então os arquivos não são enviados para nenhum servidor. A ferramenta compara o texto dos PDFs, não o layout, as imagens ou as cores.

## Entendendo os termos

- **PDF:** formato de documento (Portable Document Format) que mantém a aparência do arquivo em qualquer dispositivo.
- **PDF Original:** a versão de referência, usada como ponto de partida da comparação.
- **PDF Modificado:** a versão alterada, que será comparada com o original.
- **Texto extraído:** o conteúdo em texto lido de dentro do PDF, linha por linha, para ser comparado.
- **Diferença:** qualquer trecho de texto que existe em um PDF e não existe, ou é diferente, no outro.
- **Linha removida:** linha presente no PDF original que não aparece no modificado (marcada em vermelho, com o sinal −).
- **Linha adicionada:** linha nova no PDF modificado que não existia no original (marcada em verde, com o sinal +).
- **Linha igual:** linha que aparece sem alteração nos dois PDFs.
- **Ignorar maiúsculas e minúsculas:** opção que trata letras maiúsculas e minúsculas como iguais, por exemplo "Contrato" e "contrato".
- **PDF escaneado:** PDF formado apenas por imagens de páginas, sem texto selecionável. Ele não pode ser comparado sem antes passar por um programa de OCR.