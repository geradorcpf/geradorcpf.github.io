---
title: "Redimensionar Imagem"
seoTitle: "Redimensionar Imagem"
description: "Redimensionar Imagem: mude a largura e a altura de uma imagem. Grátis e online, sem cadastro."
summary: "Mude a largura e a altura de uma imagem."
date: 2026-11-07
draft: false
category: "midia"
tags: ["imagens", "redimensionar", "edição de imagem"]
keywords: ["redimensionar imagem", "redimensionar imagem online", "imagens", "redimensionar", "edição de imagem"]
---
Basta escolher a imagem abaixo, selecionar o quanto ela deve diminuir e depois clicar em **Redimensionar**.

<div id="calc-redimensionar" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🖼️ Redimensionar Imagem</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a imagem e diminua o tamanho mantendo a proporção.</p>
<label for="red-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Imagem</label>
<input id="red-arquivo" type="file" accept="image/*" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;">
<div style="margin-bottom:8px;font-weight:600;font-size:0.95rem;">Redução do tamanho</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label class="red-opcao" style="flex:1;min-width:110px;padding:12px 14px;text-align:center;font-size:1rem;font-weight:600;color:#1e293b;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" name="red-percentual" value="25" style="margin-right:6px;accent-color:#4f46e5;">25% menor</label>
<label class="red-opcao" style="flex:1;min-width:110px;padding:12px 14px;text-align:center;font-size:1rem;font-weight:600;color:#1e293b;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" name="red-percentual" value="50" checked style="margin-right:6px;accent-color:#4f46e5;">50% menor</label>
<label class="red-opcao" style="flex:1;min-width:110px;padding:12px 14px;text-align:center;font-size:1rem;font-weight:600;color:#1e293b;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" name="red-percentual" value="75" style="margin-right:6px;accent-color:#4f46e5;">75% menor</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="red-redimensionar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Redimensionar</button>
<button type="button" id="red-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="red-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="red-resultado">escolha uma imagem e clique em "Redimensionar".</span><span id="red-detalhe" style="display:block;margin-top:4px;font-size:0.85rem;color:#475569;"></span>
<img id="red-previa" alt="Prévia da imagem redimensionada" style="display:none;max-width:100%;height:auto;margin-top:14px;border:1px solid #c7d2fe;border-radius:10px;background:#f8fafc;">
<a id="red-baixar" href="#" style="display:none;margin-top:14px;padding:12px 18px;font-size:1rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;text-decoration:none;">⬇️ Baixar imagem</a>
</div>
</div>
<script>
(function () {
  var arquivo = document.getElementById('red-arquivo');
  var resultado = document.getElementById('red-resultado');
  var detalhe = document.getElementById('red-detalhe');
  var caixa = document.getElementById('red-resposta');
  var previa = document.getElementById('red-previa');
  var baixar = document.getElementById('red-baixar');
  var opcoes = document.querySelectorAll('input[name="red-percentual"]');
  var imagem = null;
  var arquivoAtual = null;
  var urlOriginal = null;
  var urlNova = null;
  var textoInicial = 'escolha uma imagem e clique em "Redimensionar".';
  function estado(cor, fundo, texto) {
    caixa.style.borderColor = cor;
    caixa.style.background = fundo;
    resultado.style.color = texto;
  }
  function erro(msg) {
    estado('#fca5a5', '#fef2f2', '#b91c1c');
    resultado.textContent = msg;
    detalhe.textContent = '';
    previa.style.display = 'none';
    baixar.style.display = 'none';
  }
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 1 }); }
  function tamanho(bytes) {
    if (bytes >= 1048576) { return fmt(bytes / 1048576) + ' MB'; }
    return fmt(bytes / 1024) + ' KB';
  }
  function destacar() {
    document.querySelectorAll('.red-opcao').forEach(function (rotulo) {
      var radio = rotulo.querySelector('input');
      rotulo.style.borderColor = radio.checked ? '#6366f1' : '#c7d2fe';
      rotulo.style.background = radio.checked ? '#eef2ff' : '#ffffff';
    });
  }
  function percentual() {
    var valor = 50;
    opcoes.forEach(function (o) { if (o.checked) { valor = Number(o.value); } });
    return valor;
  }
  function liberarUrls() {
    if (urlOriginal) { URL.revokeObjectURL(urlOriginal); urlOriginal = null; }
    if (urlNova) { URL.revokeObjectURL(urlNova); urlNova = null; }
  }
  function carregar() {
    var arq = arquivo.files && arquivo.files[0];
    imagem = null;
    arquivoAtual = null;
    previa.style.display = 'none';
    baixar.style.display = 'none';
    detalhe.textContent = '';
    liberarUrls();
    if (!arq) { return; }
    if (!arq.type || arq.type.indexOf('image/') !== 0) { erro('o arquivo escolhido não é uma imagem.'); return; }
    urlOriginal = URL.createObjectURL(arq);
    var img = new Image();
    img.onload = function () {
      imagem = img;
      arquivoAtual = arq;
      estado('#c7d2fe', '#ffffff', '#64748b');
      resultado.textContent = 'imagem carregada (' + img.naturalWidth + ' × ' + img.naturalHeight + ' px). Agora clique em "Redimensionar".';
    };
    img.onerror = function () { erro('não foi possível abrir essa imagem. Tente outro arquivo.'); };
    img.src = urlOriginal;
  }
  function redimensionar() {
    if (!imagem || !arquivoAtual) { erro('escolha uma imagem primeiro.'); return; }
    var fator = (100 - percentual()) / 100;
    var largura = Math.max(1, Math.round(imagem.naturalWidth * fator));
    var altura = Math.max(1, Math.round(imagem.naturalHeight * fator));
    var tipos = ['image/jpeg', 'image/png', 'image/webp'];
    var tipo = tipos.indexOf(arquivoAtual.type) > -1 ? arquivoAtual.type : 'image/png';
    var extensao = tipo === 'image/jpeg' ? 'jpg' : tipo.split('/')[1];
    var base = arquivoAtual.name.replace(/\.[^.]+$/, '') || 'imagem';
    var tela = document.createElement('canvas');
    tela.width = largura;
    tela.height = altura;
    var ctx = tela.getContext('2d');
    ctx.imageSmoothingQuality = 'high';
    ctx.drawImage(imagem, 0, 0, largura, altura);
    tela.toBlob(function (blob) {
      if (!blob) { erro('não foi possível gerar a nova imagem.'); return; }
      if (urlNova) { URL.revokeObjectURL(urlNova); }
      urlNova = URL.createObjectURL(blob);
      estado('#86efac', '#f0fdf4', '#166534');
      resultado.textContent = 'imagem redimensionada de ' + imagem.naturalWidth + ' × ' + imagem.naturalHeight + ' px para ' + largura + ' × ' + altura + ' px.';
      detalhe.textContent = 'Tamanho do arquivo: ' + tamanho(arquivoAtual.size) + ' → ' + tamanho(blob.size);
      previa.src = urlNova;
      previa.style.display = 'block';
      baixar.href = urlNova;
      baixar.download = base + '-redimensionada.' + extensao;
      baixar.style.display = 'inline-block';
    }, tipo, 0.92);
  }
  function limpar() {
    arquivo.value = '';
    imagem = null;
    arquivoAtual = null;
    liberarUrls();
    previa.style.display = 'none';
    baixar.style.display = 'none';
    detalhe.textContent = '';
    estado('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = textoInicial;
  }
  arquivo.addEventListener('change', carregar);
  opcoes.forEach(function (o) { o.addEventListener('change', destacar); });
  document.getElementById('red-redimensionar').addEventListener('click', redimensionar);
  document.getElementById('red-limpar').addEventListener('click', limpar);
  destacar();
})();
</script>

## Como usar a ferramenta

1. Clique em **Imagem** e escolha o arquivo no seu computador ou celular (JPG, PNG, WebP etc.).
2. Selecione o quanto a imagem deve diminuir: **25% menor**, **50% menor** ou **75% menor**.
3. Clique em **Redimensionar** para gerar a nova imagem.
4. Confira a prévia e as novas medidas e clique em **Baixar imagem** para salvar o arquivo.
5. Use o botão **Limpar** para remover a imagem e começar de novo.

A proporção da imagem é mantida: a largura e a altura diminuem na mesma porcentagem, então a foto não fica distorcida. Todo o processo acontece no seu próprio navegador, sem enviar a imagem para nenhum servidor.

## Entendendo os termos

- **Redimensionar:** mudar as dimensões de uma imagem, ou seja, aumentar ou diminuir sua largura e sua altura.
- **Largura:** medida horizontal da imagem, contada em pixels.
- **Altura:** medida vertical da imagem, contada em pixels.
- **Pixel (px):** cada pequeno ponto colorido que forma uma imagem digital. Quanto mais pixels, maior a imagem.
- **Proporção:** relação entre a largura e a altura. Ao manter a proporção, a imagem diminui sem ficar esticada ou achatada.
- **Porcentagem de redução:** quanto a imagem diminui em relação ao tamanho original. Em "50% menor", por exemplo, a largura e a altura ficam com a metade do valor original.
- **Resolução:** quantidade de pixels da imagem (largura × altura). Ao reduzir a resolução, o arquivo geralmente também fica mais leve.
- **Formato (JPG, PNG, WebP):** tipo do arquivo da imagem. A ferramenta mantém o formato original sempre que possível.

## Exemplo

Uma foto de 1200 × 800 px, redimensionada com a opção **50% menor**, resulta em uma nova imagem de 600 × 400 px.