---
title: "Comprimir PDF"
seoTitle: "Comprimir PDF: online e grátis"
description: "Comprimir PDF: reduza o tamanho de um arquivo PDF. Grátis e online, sem cadastro."
summary: "Reduza o tamanho de um arquivo PDF."
date: 2026-10-25
draft: false
category: "midia"
tags: ["pdf", "edição de pdf", "compressão"]
keywords: ["comprimir pdf", "comprimir pdf online", "pdf", "edição de pdf", "compressão"]
---
<!--sudah dikerjakan-->

Basta selecionar o arquivo PDF abaixo, escolher a qualidade e depois clicar em **Comprimir**.

<div id="comp-pdf" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🗜️ Comprimir PDF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o arquivo e a qualidade. Tudo é feito no seu navegador.</p>
<label for="cp-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Arquivo PDF</label>
<input id="cp-arquivo" type="file" accept="application/pdf,.pdf" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qualidade</span>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px;">
<button type="button" id="cp-q-baixa" aria-pressed="false" style="flex:1;min-width:90px;padding:11px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Baixa</button>
<button type="button" id="cp-q-boa" aria-pressed="true" style="flex:1;min-width:90px;padding:11px 12px;font-size:0.95rem;font-weight:600;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid #4f46e5;border-radius:10px;cursor:pointer;">Boa</button>
<button type="button" id="cp-q-otima" aria-pressed="false" style="flex:1;min-width:90px;padding:11px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Ótima</button>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cp-comprimir" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Comprimir</button>
<button type="button" id="cp-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cp-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cp-resultado">selecione um PDF e clique em "Comprimir".</span></div>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js"></script>
<script>
(function () {
  var arquivo = document.getElementById('cp-arquivo');
  var botao = document.getElementById('cp-comprimir');
  var caixa = document.getElementById('cp-resposta');
  var resultado = document.getElementById('cp-resultado');
  var niveis = {
    baixa: { escala: 1, jpeg: 0.5 },
    boa: { escala: 1.5, jpeg: 0.7 },
    otima: { escala: 2, jpeg: 0.85 }
  };
  var atual = 'boa';
  var ocupado = false;
  var urlAtual = null;
  var cores = {
    info: { borda: '#c7d2fe', fundo: '#ffffff', texto: '#64748b' },
    ok: { borda: '#86efac', fundo: '#f0fdf4', texto: '#166534' },
    aviso: { borda: '#fcd34d', fundo: '#fffbeb', texto: '#92400e' },
    erro: { borda: '#fca5a5', fundo: '#fef2f2', texto: '#b91c1c' }
  };
  if (window.pdfjsLib) {
    window.pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  }
  function formatar(n) {
    if (n >= 1048576) { return (n / 1048576).toLocaleString('pt-BR', { maximumFractionDigits: 2 }) + ' MB'; }
    if (n >= 1024) { return (n / 1024).toLocaleString('pt-BR', { maximumFractionDigits: 1 }) + ' KB'; }
    return n + ' bytes';
  }
  function mostrar(tipo, linhas) {
    var c = cores[tipo];
    caixa.style.borderColor = c.borda;
    caixa.style.background = c.fundo;
    resultado.style.color = c.texto;
    resultado.textContent = '';
    if (typeof linhas === 'string') { linhas = [linhas]; }
    linhas.forEach(function (linha, i) {
      if (i > 0) { resultado.appendChild(document.createElement('br')); }
      resultado.appendChild(document.createTextNode(linha));
    });
  }
  function soltarUrl() {
    if (urlAtual) { URL.revokeObjectURL(urlAtual); urlAtual = null; }
  }
  function marcarBotoes() {
    Object.keys(niveis).forEach(function (k) {
      var b = document.getElementById('cp-q-' + k);
      var ativo = (k === atual);
      b.setAttribute('aria-pressed', ativo ? 'true' : 'false');
      b.style.color = ativo ? '#ffffff' : '#4f46e5';
      b.style.background = ativo ? 'linear-gradient(135deg,#4f46e5,#6366f1)' : '#ffffff';
      b.style.borderColor = ativo ? '#4f46e5' : '#c7d2fe';
    });
  }
  function pausa() {
    return new Promise(function (ok) { setTimeout(ok, 20); });
  }
  function paraJpeg(canvas, qualidade) {
    return new Promise(function (ok) { canvas.toBlob(ok, 'image/jpeg', qualidade); });
  }
  function adicionarDownload(blob, nome) {
    soltarUrl();
    urlAtual = URL.createObjectURL(blob);
    var link = document.createElement('a');
    link.href = urlAtual;
    link.download = nome;
    link.textContent = 'Baixar PDF comprimido';
    link.style.cssText = 'display:inline-block;margin-top:12px;padding:11px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border-radius:10px;text-decoration:none;box-shadow:0 4px 12px rgba(79,70,229,0.35);';
    resultado.appendChild(document.createElement('br'));
    resultado.appendChild(link);
  }
  async function comprimir() {
    if (ocupado) { return; }
    var f = arquivo.files && arquivo.files[0];
    if (!f) { mostrar('erro', 'selecione um arquivo PDF.'); return; }
    if (f.type !== 'application/pdf' && !/\.pdf$/i.test(f.name)) {
      mostrar('erro', 'o arquivo selecionado não é um PDF.');
      return;
    }
    if (!window.pdfjsLib || !window.PDFLib) {
      mostrar('erro', 'não foi possível carregar os recursos da ferramenta. Verifique sua conexão e recarregue a página.');
      return;
    }
    ocupado = true;
    botao.disabled = true;
    botao.style.opacity = '0.6';
    soltarUrl();
    try {
      var cfg = niveis[atual];
      mostrar('info', 'Lendo o arquivo...');
      await pausa();
      var dados = await f.arrayBuffer();
      var pdf = await window.pdfjsLib.getDocument({ data: dados }).promise;
      var total = pdf.numPages;
      var novo = await window.PDFLib.PDFDocument.create();
      for (var i = 1; total >= i; i++) {
        mostrar('info', 'Processando página ' + i + ' de ' + total + '...');
        await pausa();
        var pagina = await pdf.getPage(i);
        var base = pagina.getViewport({ scale: 1 });
        var escala = cfg.escala;
        var maiorLado = Math.max(base.width, base.height) * escala;
        if (maiorLado > 4096) { escala = escala * 4096 / maiorLado; }
        var vp = pagina.getViewport({ scale: escala });
        var canvas = document.createElement('canvas');
        canvas.width = Math.max(1, Math.floor(vp.width));
        canvas.height = Math.max(1, Math.floor(vp.height));
        var ctx = canvas.getContext('2d');
        ctx.fillStyle = '#ffffff';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        await pagina.render({ canvasContext: ctx, viewport: vp }).promise;
        var blobImg = await paraJpeg(canvas, cfg.jpeg);
        var bytesImg = new Uint8Array(await blobImg.arrayBuffer());
        var img = await novo.embedJpg(bytesImg);
        var nova = novo.addPage([base.width, base.height]);
        nova.drawImage(img, { x: 0, y: 0, width: base.width, height: base.height });
        canvas.width = 0;
        canvas.height = 0;
        pagina.cleanup();
      }
      mostrar('info', 'Gerando o novo PDF...');
      await pausa();
      var saida = await novo.save();
      var blob = new Blob([saida], { type: 'application/pdf' });
      var nome = f.name.replace(/\.pdf$/i, '') + '-comprimido.pdf';
      var reducao = Math.round((1 - blob.size / f.size) * 100);
      if (blob.size >= f.size) {
        mostrar('aviso', [
          'O arquivo comprimido (' + formatar(blob.size) + ') não ficou menor que o original (' + formatar(f.size) + ').',
          'Tente a qualidade Baixa ou mantenha o arquivo original.'
        ]);
      } else {
        mostrar('ok', [
          'Arquivo comprimido com sucesso!',
          'Original: ' + formatar(f.size),
          'Comprimido: ' + formatar(blob.size) + ' (redução de ' + reducao + '%)'
        ]);
      }
      adicionarDownload(blob, nome);
    } catch (e) {
      var nomeErro = e && e.name ? e.name : '';
      if (nomeErro === 'PasswordException') {
        mostrar('erro', 'este PDF é protegido por senha. Remova a senha e tente novamente.');
      } else if (nomeErro === 'InvalidPDFException') {
        mostrar('erro', 'o arquivo PDF está corrompido ou é inválido.');
      } else {
        mostrar('erro', 'não foi possível comprimir este arquivo.');
      }
    } finally {
      ocupado = false;
      botao.disabled = false;
      botao.style.opacity = '1';
    }
  }
  function limpar() {
    if (ocupado) { return; }
    soltarUrl();
    arquivo.value = '';
    mostrar('info', 'selecione um PDF e clique em "Comprimir".');
  }
  Object.keys(niveis).forEach(function (k) {
    document.getElementById('cp-q-' + k).addEventListener('click', function () {
      atual = k;
      marcarBotoes();
    });
  });
  botao.addEventListener('click', comprimir);
  document.getElementById('cp-limpar').addEventListener('click', limpar);
  arquivo.addEventListener('focus', function () { arquivo.style.borderColor = '#6366f1'; });
  arquivo.addEventListener('blur', function () { arquivo.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Clique em **Arquivo PDF** e selecione o documento que você quer comprimir.
2. Escolha a **Qualidade**: **Baixa** gera o menor arquivo, **Boa** equilibra tamanho e nitidez, e **Ótima** preserva mais detalhes.
3. Clique em **Comprimir** e aguarde o processamento de todas as páginas.
4. Confira o tamanho original, o tamanho final e a porcentagem de redução.
5. Clique em **Baixar PDF comprimido** para salvar o novo arquivo.
6. Use o botão **Limpar** para remover o arquivo e comprimir outro.

O processamento acontece no seu próprio navegador, então o arquivo não é enviado para nenhum servidor. Cada página é convertida em imagem otimizada, por isso o texto do PDF comprimido deixa de ser selecionável e pesquisável. Se o resultado ficar maior que o original, tente a qualidade **Baixa** ou mantenha o arquivo original. PDFs protegidos por senha precisam ser desbloqueados antes.

## Entendendo os termos

- **PDF:** sigla de Portable Document Format, formato de documento que mantém o mesmo visual em qualquer dispositivo.
- **Compressão:** processo que reduz o tamanho de um arquivo para ocupar menos espaço e ser enviado mais rápido.
- **Qualidade Baixa:** gera o menor arquivo possível, com perda maior de nitidez. Indicada para envio por e-mail ou formulários com limite de tamanho.
- **Qualidade Boa:** equilíbrio entre tamanho do arquivo e legibilidade. É a opção recomendada para a maioria dos documentos.
- **Qualidade Ótima:** mantém mais detalhes, com redução de tamanho menor. Indicada para documentos com imagens ou textos pequenos.
- **Resolução:** quantidade de detalhes de cada página. Quanto maior, mais nítida a imagem e mais pesado o arquivo.
- **JPEG:** formato de imagem com compressão, usado para gravar cada página do PDF de forma mais leve.
- **Tamanho do arquivo:** espaço que o arquivo ocupa no dispositivo, medido em KB (kilobytes) ou MB (megabytes).
- **Redução:** porcentagem de espaço economizado em relação ao arquivo original.