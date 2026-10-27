---
title: "Dividir PDF"
seoTitle: "Dividir PDF: online e grátis"
description: "Dividir PDF: separe as páginas de um PDF em arquivos menores. Grátis e online, sem cadastro."
summary: "Separe as páginas de um PDF em arquivos menores."
date: 2026-10-27
draft: false
category: "midia"
tags: ["pdf", "edição de pdf"]
keywords: ["dividir pdf", "dividir pdf online", "pdf", "edição de pdf"]
---
<!--sudah dikerjakan-->

Basta enviar o arquivo PDF abaixo, escolher as páginas e depois clicar em **Dividir PDF**.

<div id="div-pdf" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✂️ Dividir PDF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Envie o PDF, escolha as páginas e baixe tudo em um arquivo ZIP.</p>
<input id="div-arquivo" type="file" accept=".pdf,application/pdf" style="display:none;">
<div id="div-upload" role="button" tabindex="0" style="padding:22px 16px;margin-bottom:16px;text-align:center;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.5;cursor:pointer;box-sizing:border-box;">📄 <strong style="color:#3730a3;">Clique aqui</strong> ou arraste o arquivo PDF para cá</div>
<div id="div-contador" style="margin-bottom:12px;font-weight:600;font-size:0.95rem;">0 páginas • 0 selecionadas</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px;">
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.95rem;font-weight:600;cursor:pointer;"><input type="radio" name="div-modo" value="todas" checked> Todas as páginas</label>
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.95rem;font-weight:600;cursor:pointer;"><input type="radio" name="div-modo" value="selecionadas"> Páginas selecionadas</label>
</div>
<div id="div-paginas" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(52px,1fr));gap:8px;margin-bottom:20px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="div-dividir" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Dividir PDF</button>
<button type="button" id="div-resetar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Resetar</button>
</div>
<div id="div-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="div-resultado">envie um arquivo PDF para começar.</span></div>
</div>
<script>
(function () {
  var URLS_PDFLIB = [
    'https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js',
    'https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js'
  ];
  var MENOR_QUE = String.fromCharCode(60);
  function porId(id) { return document.getElementById(id); }
  var entrada = porId('div-arquivo');
  var areaUpload = porId('div-upload');
  var contador = porId('div-contador');
  var grade = porId('div-paginas');
  var btnDividir = porId('div-dividir');
  var btnResetar = porId('div-resetar');
  var caixa = porId('div-resposta');
  var resultado = porId('div-resultado');
  var radios = document.getElementsByName('div-modo');
  var estado = { nome: '', bytes: null, total: 0, marcadas: {}, ocupado: false };
  var promessaLib = null;
  function modoAtual() {
    var m = 'todas';
    Array.prototype.forEach.call(radios, function (r) { if (r.checked) { m = r.value; } });
    return m;
  }
  function definirModo(m) {
    Array.prototype.forEach.call(radios, function (r) { r.checked = (r.value === m); });
  }
  function mensagem(tipo, texto) {
    var cores = {
      neutro: ['#c7d2fe', '#ffffff', '#64748b'],
      ok: ['#86efac', '#f0fdf4', '#166534'],
      erro: ['#fca5a5', '#fef2f2', '#b91c1c']
    };
    var c = cores[tipo] || cores.neutro;
    caixa.style.borderColor = c[0];
    caixa.style.background = c[1];
    resultado.style.color = c[2];
    resultado.textContent = texto;
  }
  function totalMarcadas() { return Object.keys(estado.marcadas).length; }
  function atualizarContador() {
    var n = modoAtual() === 'todas' ? estado.total : totalMarcadas();
    contador.textContent = estado.total + (estado.total === 1 ? ' página' : ' páginas') + ' • ' + n + (n === 1 ? ' selecionada' : ' selecionadas');
  }
  function estilizarPagina(btn, ativa) {
    btn.style.padding = '10px 0';
    btn.style.fontSize = '0.95rem';
    btn.style.fontWeight = '700';
    btn.style.borderRadius = '10px';
    btn.style.cursor = 'pointer';
    btn.style.border = '2px solid ' + (ativa ? '#4f46e5' : '#c7d2fe');
    btn.style.background = ativa ? 'linear-gradient(135deg,#4f46e5,#6366f1)' : '#ffffff';
    btn.style.color = ativa ? '#ffffff' : '#4f46e5';
  }
  function atualizarPaginas() {
    var todas = modoAtual() === 'todas';
    Array.prototype.forEach.call(grade.children, function (btn) {
      var n = Number(btn.getAttribute('data-n'));
      estilizarPagina(btn, todas ? true : Boolean(estado.marcadas[n]));
    });
    atualizarContador();
  }
  function desenharPaginas() {
    grade.innerHTML = '';
    for (var i = 1; i !== estado.total + 1; i += 1) {
      var b = document.createElement('button');
      b.type = 'button';
      b.setAttribute('data-n', String(i));
      b.textContent = String(i);
      b.addEventListener('click', function (e) {
        var n = Number(e.currentTarget.getAttribute('data-n'));
        if (modoAtual() === 'todas') { definirModo('selecionadas'); estado.marcadas = {}; }
        if (estado.marcadas[n]) { delete estado.marcadas[n]; } else { estado.marcadas[n] = true; }
        atualizarPaginas();
      });
      grade.appendChild(b);
    }
    atualizarPaginas();
  }
  function bloquear(sim) {
    estado.ocupado = sim;
    var inativo = sim || !estado.bytes;
    btnDividir.disabled = inativo;
    btnDividir.style.opacity = inativo ? '0.55' : '1';
    btnDividir.style.cursor = inativo ? 'not-allowed' : 'pointer';
  }
  function pausa() { return new Promise(function (ok) { setTimeout(ok, 0); }); }
  function carregarBiblioteca() {
    if (window.PDFLib) { return Promise.resolve(window.PDFLib); }
    if (promessaLib) { return promessaLib; }
    var idx = 0;
    function tentar() {
      if (idx === URLS_PDFLIB.length) { return Promise.reject(new Error('lib')); }
      var url = URLS_PDFLIB[idx];
      idx += 1;
      return fetch(url).then(function (r) {
        if (!r.ok) { throw new Error('http'); }
        return r.text();
      }).then(function (txt) {
        if (txt.trim().charAt(0) === MENOR_QUE) { throw new Error('html'); }
        var s = document.createElement('script');
        s.text = txt;
        document.head.appendChild(s);
        if (!window.PDFLib) { throw new Error('lib'); }
        return window.PDFLib;
      }).catch(tentar);
    }
    promessaLib = tentar().catch(function (e) { promessaLib = null; throw e; });
    return promessaLib;
  }
  var tabelaCrc = (function () {
    var t = [];
    for (var n = 0; n !== 256; n += 1) {
      var c = n;
      for (var k = 0; k !== 8; k += 1) { c = (c & 1) ? (0xEDB88320 ^ (c >>> 1)) : (c >>> 1); }
      t.push(c >>> 0);
    }
    return t;
  })();
  function crc32(dados) {
    var c = 0xFFFFFFFF;
    for (var i = 0; i !== dados.length; i += 1) { c = tabelaCrc[(c ^ dados[i]) & 255] ^ (c >>> 8); }
    return (c ^ 0xFFFFFFFF) >>> 0;
  }
  function criarZip(arquivos) {
    var enc = new TextEncoder();
    var partes = [];
    var central = [];
    var deslocamento = 0;
    arquivos.forEach(function (a) {
      var nome = enc.encode(a.nome);
      var crc = crc32(a.dados);
      var tam = a.dados.length;
      var lh = new DataView(new ArrayBuffer(30));
      lh.setUint32(0, 0x04034b50, true);
      lh.setUint16(4, 20, true);
      lh.setUint16(6, 0x0800, true);
      lh.setUint16(8, 0, true);
      lh.setUint16(10, 0, true);
      lh.setUint16(12, 33, true);
      lh.setUint32(14, crc, true);
      lh.setUint32(18, tam, true);
      lh.setUint32(22, tam, true);
      lh.setUint16(26, nome.length, true);
      lh.setUint16(28, 0, true);
      partes.push(new Uint8Array(lh.buffer), nome, a.dados);
      var ch = new DataView(new ArrayBuffer(46));
      ch.setUint32(0, 0x02014b50, true);
      ch.setUint16(4, 20, true);
      ch.setUint16(6, 20, true);
      ch.setUint16(8, 0x0800, true);
      ch.setUint16(10, 0, true);
      ch.setUint16(12, 0, true);
      ch.setUint16(14, 33, true);
      ch.setUint32(16, crc, true);
      ch.setUint32(20, tam, true);
      ch.setUint32(24, tam, true);
      ch.setUint16(28, nome.length, true);
      ch.setUint16(30, 0, true);
      ch.setUint16(32, 0, true);
      ch.setUint16(34, 0, true);
      ch.setUint16(36, 0, true);
      ch.setUint32(38, 0, true);
      ch.setUint32(42, deslocamento, true);
      central.push(new Uint8Array(ch.buffer), nome);
      deslocamento += 30 + nome.length + tam;
    });
    var tamCentral = 0;
    central.forEach(function (p) { tamCentral += p.length; });
    var fim = new DataView(new ArrayBuffer(22));
    fim.setUint32(0, 0x06054b50, true);
    fim.setUint16(4, 0, true);
    fim.setUint16(6, 0, true);
    fim.setUint16(8, arquivos.length, true);
    fim.setUint16(10, arquivos.length, true);
    fim.setUint32(12, tamCentral, true);
    fim.setUint32(16, deslocamento, true);
    fim.setUint16(20, 0, true);
    return new Blob(partes.concat(central, [new Uint8Array(fim.buffer)]), { type: 'application/zip' });
  }
  function baixar(blob, nome) {
    var url = URL.createObjectURL(blob);
    var a = document.createElement('a');
    a.href = url;
    a.download = nome;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    setTimeout(function () { URL.revokeObjectURL(url); }, 4000);
  }
  function nomeBase(nome) {
    var b = nome.replace(/\.pdf$/i, '').normalize('NFD').replace(/[\u0300-\u036f]/g, '');
    b = b.replace(/[^A-Za-z0-9_\-]+/g, '-').replace(/^-+|-+$/g, '');
    return b || 'documento';
  }
  async function abrirArquivo(arquivo) {
    if (!arquivo) { return; }
    var ehPdf = arquivo.type === 'application/pdf' || /\.pdf$/i.test(arquivo.name);
    if (!ehPdf) { mensagem('erro', 'selecione um arquivo no formato PDF.'); return; }
    bloquear(true);
    mensagem('neutro', 'lendo o arquivo...');
    try {
      var lib = await carregarBiblioteca();
      var bytes = new Uint8Array(await arquivo.arrayBuffer());
      var doc = await lib.PDFDocument.load(bytes, { ignoreEncryption: true });
      estado.nome = arquivo.name;
      estado.bytes = bytes;
      estado.total = doc.getPageCount();
      estado.marcadas = {};
      definirModo('todas');
      areaUpload.textContent = '📄 ' + arquivo.name;
      areaUpload.style.color = '#3730a3';
      areaUpload.style.fontWeight = '600';
      desenharPaginas();
      mensagem('neutro', 'arquivo carregado. Escolha as páginas e clique em "Dividir PDF".');
    } catch (e) {
      estado.bytes = null;
      estado.total = 0;
      grade.innerHTML = '';
      atualizarContador();
      mensagem('erro', 'não foi possível ler este PDF. Verifique se o arquivo não está protegido ou corrompido e sua conexão com a internet.');
    }
    bloquear(false);
  }
  async function dividir() {
    if (!estado.bytes || estado.ocupado) { return; }
    var paginas = [];
    var i;
    if (modoAtual() === 'todas') {
      for (i = 1; i !== estado.total + 1; i += 1) { paginas.push(i); }
    } else {
      paginas = Object.keys(estado.marcadas).map(Number).sort(function (a, b) { return a - b; });
    }
    if (paginas.length === 0) { mensagem('erro', 'selecione pelo menos uma página.'); return; }
    bloquear(true);
    try {
      var lib = await carregarBiblioteca();
      var origem = await lib.PDFDocument.load(estado.bytes, { ignoreEncryption: true });
      var base = nomeBase(estado.nome);
      var largura = String(estado.total).length;
      var arquivos = [];
      for (i = 0; i !== paginas.length; i += 1) {
        mensagem('neutro', 'dividindo página ' + (i + 1) + ' de ' + paginas.length + '...');
        await pausa();
        var novo = await lib.PDFDocument.create();
        var copiadas = await novo.copyPages(origem, [paginas[i] - 1]);
        novo.addPage(copiadas[0]);
        var dados = await novo.save();
        var num = String(paginas[i]);
        while (num.length !== largura) { num = '0' + num; }
        arquivos.push({ nome: base + '-pagina-' + num + '.pdf', dados: dados });
      }
      baixar(criarZip(arquivos), base + '-dividido.zip');
      mensagem('ok', 'pronto! ' + arquivos.length + (arquivos.length === 1 ? ' página separada' : ' páginas separadas') + ' no arquivo ZIP.');
    } catch (e) {
      mensagem('erro', 'ocorreu um erro ao dividir o PDF. Tente novamente.');
    }
    bloquear(false);
  }
  function resetar() {
    estado.nome = '';
    estado.bytes = null;
    estado.total = 0;
    estado.marcadas = {};
    entrada.value = '';
    grade.innerHTML = '';
    definirModo('todas');
    areaUpload.textContent = '📄 Clique aqui ou arraste o arquivo PDF para cá';
    areaUpload.style.color = '#64748b';
    areaUpload.style.fontWeight = '400';
    atualizarContador();
    mensagem('neutro', 'envie um arquivo PDF para começar.');
    bloquear(false);
  }
  areaUpload.addEventListener('click', function () { entrada.click(); });
  areaUpload.addEventListener('keydown', function (e) {
    if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); entrada.click(); }
  });
  areaUpload.addEventListener('dragover', function (e) {
    e.preventDefault();
    areaUpload.style.borderColor = '#6366f1';
    areaUpload.style.background = '#eef2ff';
  });
  areaUpload.addEventListener('dragleave', function () {
    areaUpload.style.borderColor = '#c7d2fe';
    areaUpload.style.background = '#ffffff';
  });
  areaUpload.addEventListener('drop', function (e) {
    e.preventDefault();
    areaUpload.style.borderColor = '#c7d2fe';
    areaUpload.style.background = '#ffffff';
    if (e.dataTransfer && e.dataTransfer.files && e.dataTransfer.files[0]) { abrirArquivo(e.dataTransfer.files[0]); }
  });
  entrada.addEventListener('change', function () { abrirArquivo(entrada.files[0]); });
  Array.prototype.forEach.call(radios, function (r) {
    r.addEventListener('change', function () { atualizarPaginas(); });
  });
  btnDividir.addEventListener('click', dividir);
  btnResetar.addEventListener('click', resetar);
  bloquear(false);
})();
</script>

## Como usar a ferramenta

1. Clique na área de upload (ou arraste o arquivo para ela) e escolha o **PDF** que deseja dividir.
2. Deixe marcado **Todas as páginas** para separar o documento inteiro, ou escolha **Páginas selecionadas** e clique nos números das páginas que você quer extrair.
3. Clique em **Dividir PDF** e aguarde o processamento.
4. O download do **arquivo ZIP** começa automaticamente, com cada página em um PDF separado.
5. Use o botão **Resetar** para remover o arquivo atual e começar de novo com outro PDF.

O arquivo é processado diretamente no seu navegador. Ele não é enviado para nenhum servidor.

## Entendendo os termos

- **PDF:** formato de documento que mantém o texto, as imagens e o layout iguais em qualquer dispositivo.
- **Dividir PDF:** separar um arquivo PDF em partes menores, neste caso uma página por arquivo.
- **Página:** cada folha do documento PDF, identificada por um número a partir da primeira.
- **Todas as páginas:** modo que separa o documento inteiro, gerando um arquivo para cada página.
- **Páginas selecionadas:** modo que separa somente as páginas que você marcou.
- **Arquivo ZIP:** pasta compactada que reúne todos os PDFs gerados em um único download.
- **Resetar:** limpa o arquivo e a seleção para você recomeçar do zero.
- **Upload:** envio do arquivo do seu dispositivo para a ferramenta, feito ao clicar ou arrastar o PDF para a área indicada.