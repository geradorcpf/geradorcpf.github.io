---
title: "Foto em Preto e Branco"
seoTitle: "Foto em Preto e Branco"
description: "Foto em Preto e Branco: transforme uma foto em preto e branco. Grátis e online, sem cadastro."
summary: "Transforme uma foto em preto e branco."
date: 2026-10-28
draft: false
category: "midia"
tags: ["imagens", "preto e branco", "edição de imagem"]
keywords: ["foto em preto e branco", "foto em preto e branco online", "imagens", "preto e branco", "edição de imagem"]
---
<!--INI SUDAH DIKERJAKAN-->

Arraste suas fotos para a área abaixo (ou clique para selecionar) e depois clique em **Converter e Baixar**.

<div id="ferramenta-pb" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🖤 Foto em Preto e Branco</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Converta suas fotos para tons de cinza direto no navegador.</p>
<label for="pb-arquivos" id="pb-area" style="display:block;margin-bottom:16px;padding:28px 14px;text-align:center;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;cursor:pointer;box-sizing:border-box;">Arraste as imagens ou clique aqui.</label>
<input id="pb-arquivos" type="file" accept="image/*" multiple style="display:none;">
<div style="margin-bottom:16px;">
<div style="width:100%;height:12px;background:#e0e7ff;border-radius:999px;overflow:hidden;">
<div id="pb-barra" style="width:0%;height:100%;background:linear-gradient(135deg,#4f46e5,#6366f1);border-radius:999px;"></div>
</div>
<div id="pb-percentual" style="margin-top:6px;font-size:0.85rem;color:#64748b;text-align:right;">0%</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="pb-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter e Baixar</button>
<button type="button" id="pb-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="pb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="pb-resultado">selecione uma ou mais imagens e clique em "Converter e Baixar".</span></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('pb-arquivos');
  var area = document.getElementById('pb-area');
  var barra = document.getElementById('pb-barra');
  var percentual = document.getElementById('pb-percentual');
  var botao = document.getElementById('pb-converter');
  var limpa = document.getElementById('pb-limpar');
  var caixa = document.getElementById('pb-resposta');
  var resultado = document.getElementById('pb-resultado');
  var textoPadrao = 'selecione uma ou mais imagens e clique em "Converter e Baixar".';
  var arquivos = [];
  var ocupado = false;
  function estilo(borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
  }
  function erro(msg) { estilo('#fca5a5', '#fef2f2', '#b91c1c'); resultado.textContent = msg; }
  function ok(msg) { estilo('#86efac', '#f0fdf4', '#166534'); resultado.textContent = msg; }
  function progresso(p) {
    var v = Math.round(p);
    barra.style.width = v + '%';
    percentual.textContent = v + '%';
  }
  function receber(lista) {
    var novos = Array.prototype.slice.call(lista).filter(function (f) {
      return String(f.type).indexOf('image/') === 0;
    });
    if (novos.length === 0) { erro('nenhuma imagem válida foi selecionada.'); return; }
    arquivos = novos;
    progresso(0);
    estilo('#c7d2fe', '#ffffff', '#64748b');
    area.textContent = novos.length === 1 ? novos[0].name : novos.length + ' imagens selecionadas';
    resultado.textContent = 'pronto para converter. Clique em "Converter e Baixar".';
  }
  function carregar(arquivo) {
    return new Promise(function (resolve, reject) {
      var url = URL.createObjectURL(arquivo);
      var img = new Image();
      img.onload = function () { resolve({ img: img, url: url }); };
      img.onerror = function () { URL.revokeObjectURL(url); reject(new Error(arquivo.name)); };
      img.src = url;
    });
  }
  function converter(arquivo) {
    return carregar(arquivo).then(function (r) {
      var c = document.createElement('canvas');
      c.width = r.img.naturalWidth;
      c.height = r.img.naturalHeight;
      var ctx = c.getContext('2d');
      ctx.drawImage(r.img, 0, 0);
      var dados = ctx.getImageData(0, 0, c.width, c.height);
      var px = dados.data;
      var total = px.length;
      for (var i = 0; i !== total; i += 4) {
        var g = Math.round(0.299 * px[i] + 0.587 * px[i + 1] + 0.114 * px[i + 2]);
        px[i] = g;
        px[i + 1] = g;
        px[i + 2] = g;
      }
      ctx.putImageData(dados, 0, 0);
      URL.revokeObjectURL(r.url);
      var jpg = arquivo.type === 'image/jpeg';
      return new Promise(function (resolve) {
        c.toBlob(function (blob) { resolve({ blob: blob, jpg: jpg }); }, jpg ? 'image/jpeg' : 'image/png', 0.92);
      });
    });
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
  function pausa() { return new Promise(function (r) { setTimeout(r, 250); }); }
  function processar() {
    if (ocupado) { return; }
    if (arquivos.length === 0) { erro('selecione pelo menos uma imagem antes de converter.'); return; }
    ocupado = true;
    botao.disabled = true;
    progresso(0);
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = 'convertendo...';
    var feitos = 0;
    var falhas = 0;
    var cadeia = Promise.resolve();
    arquivos.forEach(function (arq) {
      cadeia = cadeia.then(function () {
        return converter(arq).then(function (r) {
          var base = arq.name.replace(/\.[^.]+$/, '');
          baixar(r.blob, base + '-preto-e-branco.' + (r.jpg ? 'jpg' : 'png'));
          feitos += 1;
        }).catch(function () {
          falhas += 1;
        }).then(function () {
          progresso(((feitos + falhas) / arquivos.length) * 100);
          return pausa();
        });
      });
    });
    cadeia.then(function () {
      ocupado = false;
      botao.disabled = false;
      if (feitos === 0) { erro('não foi possível converter as imagens selecionadas.'); return; }
      var msg = feitos + (feitos === 1 ? ' imagem convertida e baixada.' : ' imagens convertidas e baixadas.');
      if (falhas !== 0) { msg += ' ' + falhas + ' arquivo(s) com falha.'; }
      ok(msg);
    });
  }
  function limpar() {
    arquivos = [];
    entrada.value = '';
    area.textContent = 'Arraste as imagens ou clique aqui.';
    progresso(0);
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = textoPadrao;
  }
  entrada.addEventListener('change', function () { receber(entrada.files); });
  ['dragenter', 'dragover'].forEach(function (ev) {
    area.addEventListener(ev, function (e) {
      e.preventDefault();
      area.style.borderColor = '#6366f1';
      area.style.background = '#eef2ff';
    });
  });
  ['dragleave', 'drop'].forEach(function (ev) {
    area.addEventListener(ev, function (e) {
      e.preventDefault();
      area.style.borderColor = '#c7d2fe';
      area.style.background = '#ffffff';
    });
  });
  area.addEventListener('drop', function (e) {
    if (e.dataTransfer && e.dataTransfer.files) { receber(e.dataTransfer.files); }
  });
  botao.addEventListener('click', processar);
  limpa.addEventListener('click', limpar);
})();
</script>

## Como usar a ferramenta

1. Arraste uma ou mais fotos para a área tracejada, ou clique nela para escolher os arquivos no seu dispositivo.
2. Confira o nome do arquivo (ou a quantidade de imagens) exibido na área.
3. Clique em **Converter e Baixar** e acompanhe a barra de progresso até chegar a 100%.
4. As fotos em preto e branco são baixadas automaticamente, com o sufixo `-preto-e-branco` no nome.
5. Use o botão **Limpar** para remover a seleção e converter novas imagens.

O processamento acontece 100% no seu navegador: suas fotos não são enviadas para nenhum servidor. Formatos comuns como JPG, PNG, GIF e WebP são aceitos, e você pode converter várias fotos de uma só vez. Se o navegador pedir permissão para baixar vários arquivos, autorize para receber todas as imagens.

## Entendendo os termos

- **Preto e branco:** imagem sem cores, formada apenas por variações entre o preto e o branco.
- **Tons de cinza:** os níveis intermediários de brilho entre o preto e o branco. É o que dá forma e detalhe à foto sem cor.
- **Conversão:** processo de transformar uma imagem colorida em uma versão em tons de cinza.
- **Processamento local:** a conversão é feita no próprio navegador, sem enviar a foto para a internet, o que preserva sua privacidade.
- **Processamento em lote:** converter várias fotos de uma vez, em vez de uma por uma.
- **Luminosidade:** brilho percebido de cada cor. Ela define qual tom de cinza substitui cada pixel colorido.
- **Pixel:** menor ponto de uma imagem digital. A conversão calcula um tom de cinza para cada pixel.
- **JPG:** formato de imagem comprimido, muito usado em fotografias e de menor tamanho.
- **PNG:** formato de imagem sem perda de qualidade, que também suporta transparência.
- **GIF e WebP:** formatos de imagem comuns na web; nesta ferramenta, são baixados como PNG após a conversão.

## Como a conversão funciona

Para cada pixel da foto, a ferramenta calcula um valor de cinza que considera a sensibilidade do olho humano às cores, dando mais peso ao verde, depois ao vermelho e por último ao azul:

**cinza = 0,299 × vermelho + 0,587 × verde + 0,114 × azul**

Em seguida, os três canais do pixel recebem esse mesmo valor, resultando em uma imagem em tons de cinza com aparência natural.