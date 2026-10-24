---
title: "Comprimir Imagem"
seoTitle: "Comprimir Imagem: online e grátis"
description: "Comprimir Imagem: reduza o peso de imagens sem perder muita qualidade. Grátis e online, sem cadastro."
summary: "Reduza o peso de imagens sem perder muita qualidade."
date: 2026-10-24
draft: false
category: "midia"
tags: ["imagens", "compressão", "edição de imagem"]
keywords: ["comprimir imagem", "comprimir imagem online", "imagens", "compressão", "edição de imagem"]
---
<!--sudah dikerjakan-->

Basta selecionar as imagens JPG ou PNG abaixo, escolher a qualidade e clicar em **Comprimir**.

<div id="calc-comprimir" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🗜️ Comprimir Imagem</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Reduza o peso de imagens JPG e PNG direto no navegador.</p>
<label for="cmp-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Imagens (JPG ou PNG)</label>
<input id="cmp-arquivo" type="file" accept="image/jpeg,image/png" multiple style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="cmp-qualidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qualidade</label>
<select id="cmp-qualidade" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="baixa">Qualidade Baixa (menor arquivo)</option>
<option value="boa" selected>Qualidade Boa</option>
<option value="otima">Qualidade Ótima (maior arquivo)</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cmp-comprimir" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Comprimir</button>
<button type="button" id="cmp-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cmp-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cmp-resultado">escolha as imagens e clique em "Comprimir".</span><div id="cmp-lista" style="margin-top:12px;"></div></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('cmp-arquivo');
  var qualidade = document.getElementById('cmp-qualidade');
  var botao = document.getElementById('cmp-comprimir');
  var botaoLimpar = document.getElementById('cmp-limpar');
  var resultado = document.getElementById('cmp-resultado');
  var caixa = document.getElementById('cmp-resposta');
  var lista = document.getElementById('cmp-lista');
  var urls = [];
  var ocupado = false;
  var PERFIS = {
    baixa: { jpeg: 0.4, passo: 48 },
    boa: { jpeg: 0.7, passo: 24 },
    otima: { jpeg: 0.88, passo: 12 }
  };
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 2 }); }
  function tamanho(bytes) {
    if (bytes >= 1048576) { return fmt(bytes / 1048576) + ' MB'; }
    if (bytes >= 1024) { return fmt(bytes / 1024) + ' KB'; }
    return fmt(bytes) + ' B';
  }
  function estilo(cor, fundo, texto) {
    caixa.style.borderColor = cor;
    caixa.style.background = fundo;
    resultado.style.color = texto;
  }
  function erro(msg) {
    estilo('#fca5a5', '#fef2f2', '#b91c1c');
    resultado.textContent = msg;
  }
  function liberarUrls() {
    urls.forEach(function (u) { URL.revokeObjectURL(u); });
    urls = [];
  }
  function carregar(arquivo) {
    return new Promise(function (ok, falha) {
      var url = URL.createObjectURL(arquivo);
      var img = new Image();
      img.onload = function () { URL.revokeObjectURL(url); ok(img); };
      img.onerror = function () { URL.revokeObjectURL(url); falha(new Error('Não foi possível ler a imagem ' + arquivo.name + '.')); };
      img.src = url;
    });
  }
  function paraBlob(canvas, tipo, q) {
    return new Promise(function (ok) { canvas.toBlob(ok, tipo, q); });
  }
  function comprimir(arquivo, perfil) {
    return carregar(arquivo).then(function (img) {
      var canvas = document.createElement('canvas');
      canvas.width = img.naturalWidth;
      canvas.height = img.naturalHeight;
      var ctx = canvas.getContext('2d');
      var ehPng = arquivo.type === 'image/png';
      if (!ehPng) {
        ctx.fillStyle = '#ffffff';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
      }
      ctx.drawImage(img, 0, 0);
      if (ehPng) {
        var dados = ctx.getImageData(0, 0, canvas.width, canvas.height);
        var px = dados.data;
        var passo = perfil.passo;
        for (var i = 0; i !== px.length; i += 4) {
          px[i] = Math.min(255, Math.round(px[i] / passo) * passo);
          px[i + 1] = Math.min(255, Math.round(px[i + 1] / passo) * passo);
          px[i + 2] = Math.min(255, Math.round(px[i + 2] / passo) * passo);
        }
        ctx.putImageData(dados, 0, 0);
        return paraBlob(canvas, 'image/png');
      }
      return paraBlob(canvas, 'image/jpeg', perfil.jpeg);
    }).then(function (blob) {
      var reduziu = !!blob && blob.size > 0 && arquivo.size > blob.size;
      return { blob: reduziu ? blob : arquivo, reduziu: reduziu };
    });
  }
  function nomeSaida(nome, tipo) {
    var ext = tipo === 'image/png' ? 'png' : 'jpg';
    var base = nome.replace(/\.[^.]+$/, '');
    return base + '-comprimido.' + ext;
  }
  function criarItem(arquivo, saida) {
    var item = document.createElement('div');
    item.style.cssText = 'padding:12px;margin-top:8px;background:#f8fafc;border:1px solid #c7d2fe;border-radius:10px;color:#1e293b;font-size:0.9rem;line-height:1.5;word-break:break-word;';
    var nome = document.createElement('strong');
    nome.style.color = '#3730a3';
    nome.textContent = arquivo.name;
    item.appendChild(nome);
    var info = document.createElement('div');
    var antes = arquivo.size;
    var depois = saida.blob.size;
    if (saida.reduziu) {
      var pct = (1 - depois / antes) * 100;
      info.textContent = tamanho(antes) + ' → ' + tamanho(depois) + ' (redução de ' + fmt(pct) + '%)';
    } else {
      info.textContent = tamanho(antes) + ' — a imagem já está otimizada, o original foi mantido.';
    }
    item.appendChild(info);
    var url = URL.createObjectURL(saida.blob);
    urls.push(url);
    var link = document.createElement('a');
    link.href = url;
    link.download = nomeSaida(arquivo.name, arquivo.type);
    link.textContent = 'Baixar imagem';
    link.style.cssText = 'display:inline-block;margin-top:8px;padding:8px 14px;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;text-decoration:none;';
    item.appendChild(link);
    return item;
  }
  function executar() {
    if (ocupado) { return; }
    var arquivos = Array.prototype.slice.call(entrada.files || []).filter(function (f) {
      return f.type === 'image/jpeg' || f.type === 'image/png';
    });
    if (arquivos.length === 0) { erro('selecione ao menos uma imagem JPG ou PNG.'); return; }
    var perfil = PERFIS[qualidade.value] || PERFIS.boa;
    ocupado = true;
    botao.disabled = true;
    liberarUrls();
    lista.textContent = '';
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = 'comprimindo ' + arquivos.length + ' imagem(ns)...';
    var totalAntes = 0;
    var totalDepois = 0;
    var cadeia = Promise.resolve();
    arquivos.forEach(function (arquivo) {
      cadeia = cadeia.then(function () {
        return comprimir(arquivo, perfil).then(function (saida) {
          totalAntes += arquivo.size;
          totalDepois += saida.blob.size;
          lista.appendChild(criarItem(arquivo, saida));
        });
      });
    });
    cadeia.then(function () {
      estilo('#86efac', '#f0fdf4', '#166534');
      var pct = totalAntes > 0 ? (1 - totalDepois / totalAntes) * 100 : 0;
      resultado.innerHTML = 'Pronto! Tamanho total: <strong style="font-size:1.2rem;">' + tamanho(totalAntes) + ' → ' + tamanho(totalDepois) + '</strong><br><small style="color:#475569;">Economia de ' + fmt(pct) + '%</small>';
    }).catch(function (e) {
      erro(e && e.message ? e.message : 'ocorreu um erro ao comprimir a imagem.');
    }).then(function () {
      ocupado = false;
      botao.disabled = false;
    });
  }
  function limpar() {
    liberarUrls();
    entrada.value = '';
    qualidade.value = 'boa';
    lista.textContent = '';
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = 'escolha as imagens e clique em "Comprimir".';
  }
  botao.addEventListener('click', executar);
  botaoLimpar.addEventListener('click', limpar);
  [entrada, qualidade].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Clique em **Imagens (JPG ou PNG)** e selecione uma ou mais fotos do seu dispositivo.
2. Escolha o nível de **Qualidade**: Baixa (arquivo menor), Boa (equilíbrio) ou Ótima (mais fiel ao original).
3. Clique em **Comprimir** e aguarde o processamento.
4. Confira o tamanho antes e depois de cada imagem e clique em **Baixar imagem** para salvar o arquivo comprimido.
5. Use o botão **Limpar** para remover os arquivos e começar de novo.

As imagens são processadas no seu próprio navegador e não são enviadas para nenhum servidor. Se a imagem já estiver bem otimizada e não for possível reduzi-la, o arquivo original é mantido.

## Entendendo os termos

- **Compressão de imagem:** técnica que reduz o tamanho (peso) de um arquivo de imagem para ocupar menos espaço e carregar mais rápido.
- **JPG (JPEG):** formato comum para fotos, que usa compressão com perda para gerar arquivos leves.
- **PNG:** formato que preserva bem nitidez e transparência, muito usado em logotipos, ícones e capturas de tela.
- **Compressão com perda:** método que descarta detalhes pouco perceptíveis da imagem para diminuir o arquivo. Quanto mais forte, menor o arquivo e maior a perda.
- **Qualidade:** nível de compressão aplicado. Qualidade menor gera arquivos menores, e qualidade maior mantém mais detalhes.
- **Tamanho do arquivo:** espaço que a imagem ocupa no dispositivo, medido em bytes (B), quilobytes (KB) ou megabytes (MB).
- **Redução:** porcentagem de espaço economizado em relação ao tamanho original.
- **Otimização para web:** preparo das imagens para que o site carregue mais rápido e use menos dados.