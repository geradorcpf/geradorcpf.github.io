---
title: "Nuvem de Palavras"
seoTitle: "Nuvem de Palavras"
description: "Nuvem de Palavras: transforme um texto em nuvem de palavras. Grátis e online, sem cadastro."
summary: "Transforme um texto em nuvem de palavras."
date: 2026-11-06
draft: false
category: "texto"
tags: ["palavras", "análise de texto", "texto"]
keywords: ["nuvem de palavras", "nuvem de palavras online", "palavras", "análise de texto", "texto"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta colar o seu texto abaixo, ajustar as opções e clicar em **Gerar**. Depois, é só **Baixar** a imagem.

<div id="calc-nuvem" style="max-width:720px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">☁️ Nuvem de Palavras</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole um texto e gere a sua nuvem de palavras na hora.</p>
<label for="nv-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="nv-texto" rows="6" placeholder="Cole ou digite o seu texto aqui..." style="width:100%;min-height:140px;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:14px;flex-wrap:wrap;">
<div style="flex:1;min-width:200px;">
<label for="nv-esquema" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Esquema de cores</label>
<select id="nv-esquema" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="colorido">Colorido</option>
<option value="azul">Tons de azul</option>
<option value="verde">Tons de verde</option>
<option value="quente">Tons quentes</option>
<option value="mono">Preto e branco</option>
</select>
</div>
<div style="flex:1;min-width:200px;">
<label for="nv-fundo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cor de fundo</label>
<select id="nv-fundo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="branco">Branco</option>
<option value="preto">Preto</option>
<option value="cinza-claro">Cinza claro</option>
<option value="cinza-escuro">Cinza escuro</option>
<option value="transparente">Transparente</option>
</select>
</div>
</div>
<div style="display:flex;gap:14px;flex-wrap:wrap;">
<div style="flex:1;min-width:200px;">
<label for="nv-fonte" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Fonte</label>
<select id="nv-fonte" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="Impact">Impact</option>
<option value="Arial">Arial</option>
<option value="Helvetica">Helvetica</option>
<option value="Georgia">Georgia</option>
<option value="Times New Roman">Times New Roman</option>
<option value="Courier New">Courier New</option>
<option value="Verdana">Verdana</option>
</select>
</div>
<div style="flex:1;min-width:200px;">
<label for="nv-rotacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Rotação das palavras</label>
<select id="nv-rotacao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="nenhuma">Sem rotação</option>
<option value="aleatoria" selected>Aleatória</option>
<option value="vertical">Apenas vertical</option>
</select>
</div>
</div>
<div style="display:flex;gap:14px;flex-wrap:wrap;">
<div style="flex:1;min-width:200px;">
<label for="nv-max" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número máximo de palavras</label>
<input id="nv-max" type="text" inputmode="numeric" value="100" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:200px;">
<label for="nv-peso" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Fator de peso</label>
<input id="nv-peso" type="text" inputmode="decimal" value="1" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<label style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Resolução da imagem (Largura × Altura, em pixels)</label>
<div style="display:flex;gap:10px;align-items:center;margin-bottom:16px;">
<input id="nv-largura" type="text" inputmode="numeric" value="800" aria-label="Largura em pixels" autocomplete="off" style="flex:1;min-width:0;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="font-weight:700;color:#3730a3;">×</span>
<input id="nv-altura" type="text" inputmode="numeric" value="600" aria-label="Altura em pixels" autocomplete="off" style="flex:1;min-width:0;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<label for="nv-stop" style="display:flex;align-items:center;gap:8px;margin-bottom:20px;font-size:0.95rem;cursor:pointer;"><input id="nv-stop" type="checkbox" checked style="width:18px;height:18px;cursor:pointer;accent-color:#4f46e5;"> Ignorar palavras comuns (de, a, o, que, para...)</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="nv-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar</button>
<button type="button" id="nv-baixar" disabled style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:not-allowed;opacity:0.5;">Baixar</button>
<button type="button" id="nv-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="nv-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="nv-resultado">cole um texto e clique em "Gerar".</span></div>
<div id="nv-saida" style="display:none;margin-top:16px;border:2px solid #c7d2fe;border-radius:12px;overflow:hidden;background-color:#ffffff;background-image:conic-gradient(#e2e8f0 25%,#ffffff 0 50%,#e2e8f0 0 75%,#ffffff 0);background-size:16px 16px;">
<canvas id="nv-canvas" width="800" height="600" style="display:block;width:100%;height:auto;"></canvas>
</div>
</div>
<script>
(function () {
  var texto = document.getElementById('nv-texto');
  var esquema = document.getElementById('nv-esquema');
  var fundo = document.getElementById('nv-fundo');
  var fonte = document.getElementById('nv-fonte');
  var rotacao = document.getElementById('nv-rotacao');
  var maxPal = document.getElementById('nv-max');
  var peso = document.getElementById('nv-peso');
  var largura = document.getElementById('nv-largura');
  var altura = document.getElementById('nv-altura');
  var stop = document.getElementById('nv-stop');
  var btnGerar = document.getElementById('nv-gerar');
  var btnBaixar = document.getElementById('nv-baixar');
  var btnLimpar = document.getElementById('nv-limpar');
  var caixa = document.getElementById('nv-resposta');
  var resultado = document.getElementById('nv-resultado');
  var saida = document.getElementById('nv-saida');
  var canvas = document.getElementById('nv-canvas');
  var ctx = canvas.getContext('2d');
  var STOP = 'a o as os um uma uns umas de do da dos das em no na nos nas por para com sem sob sobre e ou mas que se como ao aos à às pelo pela pelos pelas seu sua seus suas meu minha meus minhas é são foi era ser ter tem há já não mais muito também até isso isto esse essa esses essas este esta estes estas ele ela eles elas eu tu nós vocês você me te lhe quando onde quem qual entre depois só então assim ainda pois porque num numa dele dela deles delas aquele aquela aqui lá nem mesmo está estão foram seja tinha'.split(' ');
  var stopSet = Object.create(null);
  STOP.forEach(function (w) { stopSet[w] = true; });
  var PALETAS = {
    colorido: ['#4f46e5', '#db2777', '#059669', '#d97706', '#0891b2', '#7c3aed', '#dc2626', '#2563eb'],
    azul: ['#1e3a8a', '#1d4ed8', '#2563eb', '#0284c7', '#0891b2', '#3b82f6'],
    verde: ['#14532d', '#166534', '#15803d', '#16a34a', '#0d9488', '#65a30d'],
    quente: ['#b91c1c', '#dc2626', '#ea580c', '#d97706', '#f59e0b', '#be185d']
  };
  var FUNDOS = { 'branco': '#ffffff', 'preto': '#000000', 'cinza-claro': '#e5e7eb', 'cinza-escuro': '#374151', 'transparente': '' };
  function lerInt(el, padrao, min, max) {
    var n = parseInt(String(el.value).trim(), 10);
    if (isNaN(n)) { n = padrao; }
    return Math.max(min, Math.min(max, n));
  }
  function lerNum(el, padrao, min, max) {
    var t = String(el.value).trim().replace(',', '.');
    var n = Number(t);
    if (t === '' || isNaN(n)) { n = padrao; }
    return Math.max(min, Math.min(max, n));
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
  function contar() {
    var palavras = texto.value.toLowerCase().match(/[\p{L}\p{N}]+/gu) || [];
    var mapa = Object.create(null);
    palavras.forEach(function (p) {
      if (p.length === 1 || /^[0-9]+$/.test(p)) { return; }
      if (stop.checked && stopSet[p]) { return; }
      mapa[p] = (mapa[p] || 0) + 1;
    });
    var lista = Object.keys(mapa).map(function (k) { return [k, mapa[k]]; });
    lista.sort(function (a, b) { return (b[1] - a[1]) || a[0].localeCompare(b[0]); });
    return lista;
  }
  function habilitarBaixar(sim) {
    btnBaixar.disabled = !sim;
    btnBaixar.style.opacity = sim ? '1' : '0.5';
    btnBaixar.style.cursor = sim ? 'pointer' : 'not-allowed';
  }
  function gerar() {
    var W = lerInt(largura, 800, 200, 4000);
    var H = lerInt(altura, 600, 200, 4000);
    var limite = lerInt(maxPal, 100, 1, 300);
    var fator = lerNum(peso, 1, 0.2, 5);
    var lista = contar();
    if (lista.length === 0) {
      habilitarBaixar(false);
      saida.style.display = 'none';
      erro('digite ou cole um texto com pelo menos uma palavra válida.');
      return;
    }
    var total = lista.length;
    lista = lista.slice(0, limite);
    largura.value = W;
    altura.value = H;
    canvas.width = W;
    canvas.height = H;
    var fam = '"' + fonte.value + '", sans-serif';
    var rot = rotacao.value;
    var corFundo = FUNDOS[fundo.value];
    var escuro = fundo.value === 'preto' || fundo.value === 'cinza-escuro';
    var paleta = PALETAS[esquema.value];
    if (!paleta) { paleta = escuro ? ['#ffffff', '#e5e7eb', '#cbd5e1', '#f1f5f9'] : ['#111827', '#374151', '#4b5563', '#1f2937']; }
    var maxC = lista[0][1];
    var minC = lista[lista.length - 1][1];
    var faixa = maxC - minC;
    var fMax = Math.max(24, Math.min(H * 0.2, W * 0.12));
    var fMin = Math.max(10, H * 0.025);
    var asp = W / H;
    var colocadas = [];
    var puladas = 0;
    function posicionar(palavra, tam, vert) {
      ctx.font = tam + 'px ' + fam;
      var w = ctx.measureText(palavra).width + 4;
      var h = tam * 1.05;
      var bw = vert ? h : w;
      var bh = vert ? w : h;
      for (var i = 0; 4000 > i; i++) {
        var ang = i * 0.15;
        var r = i * 0.5;
        var x = W / 2 + r * Math.cos(ang) * asp;
        var y = H / 2 + r * Math.sin(ang);
        var esq = x - bw / 2;
        var topo = y - bh / 2;
        if (!(esq >= 2 && topo >= 2 && W - 2 >= esq + bw && H - 2 >= topo + bh)) { continue; }
        var bate = false;
        for (var j = 0; colocadas.length > j; j++) {
          var c = colocadas[j];
          if (c.l + c.w + 2 > esq && esq + bw + 2 > c.l && c.t + c.h + 2 > topo && topo + bh + 2 > c.t) { bate = true; break; }
        }
        if (!bate) { return { x: x, y: y, l: esq, t: topo, w: bw, h: bh }; }
      }
      return null;
    }
    lista.forEach(function (item, idx) {
      var t = faixa > 0 ? (item[1] - minC) / faixa : 0.5;
      var tam = fMin + Math.pow(t, fator) * (fMax - fMin);
      var vert = rot === 'vertical' || (rot === 'aleatoria' && Math.random() > 0.7);
      var pos = null;
      while (!pos && tam >= 8) {
        pos = posicionar(item[0], tam, vert);
        if (!pos) { tam = tam * 0.88; }
      }
      if (!pos) { puladas++; return; }
      pos.palavra = item[0];
      pos.tam = tam;
      pos.vert = vert;
      pos.cor = paleta[idx % paleta.length];
      colocadas.push(pos);
    });
    ctx.clearRect(0, 0, W, H);
    if (corFundo) {
      ctx.fillStyle = corFundo;
      ctx.fillRect(0, 0, W, H);
    }
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    colocadas.forEach(function (p) {
      ctx.font = p.tam + 'px ' + fam;
      ctx.fillStyle = p.cor;
      ctx.save();
      ctx.translate(p.x, p.y);
      if (p.vert) { ctx.rotate(-Math.PI / 2); }
      ctx.fillText(p.palavra, 0, 0);
      ctx.restore();
    });
    saida.style.display = 'block';
    habilitarBaixar(true);
    var msg = 'Nuvem gerada com ' + colocadas.length + ' palavra(s), de ' + total + ' palavra(s) única(s) no texto.';
    if (puladas > 0) { msg += ' ' + puladas + ' não coube(ram) na imagem; aumente a resolução ou reduza o número máximo de palavras.'; }
    sucesso(msg);
  }
  function baixar() {
    if (btnBaixar.disabled) { return; }
    if (canvas.toBlob) {
      canvas.toBlob(function (blob) {
        if (!blob) { return; }
        var url = URL.createObjectURL(blob);
        var a = document.createElement('a');
        a.href = url;
        a.download = 'nuvem-de-palavras.png';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        setTimeout(function () { URL.revokeObjectURL(url); }, 1000);
      }, 'image/png');
    } else {
      var b = document.createElement('a');
      b.href = canvas.toDataURL('image/png');
      b.download = 'nuvem-de-palavras.png';
      document.body.appendChild(b);
      b.click();
      document.body.removeChild(b);
    }
  }
  function limpar() {
    texto.value = '';
    saida.style.display = 'none';
    habilitarBaixar(false);
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'cole um texto e clique em "Gerar".';
    texto.focus();
  }
  btnGerar.addEventListener('click', gerar);
  btnBaixar.addEventListener('click', baixar);
  btnLimpar.addEventListener('click', limpar);
  [texto, esquema, fundo, fonte, rotacao, maxPal, peso, largura, altura].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Cole ou digite o seu texto no campo **Texto**.
2. Escolha o **Esquema de cores**, a **Cor de fundo** e a **Fonte** da nuvem.
3. Defina a **Rotação das palavras**: sem rotação, aleatória ou apenas vertical.
4. Informe o **Número máximo de palavras** e o **Fator de peso**. Quanto maior o fator, maior a diferença de tamanho entre as palavras mais e menos frequentes.
5. Defina a **Resolução da imagem** (largura × altura em pixels).
6. Clique em **Gerar** para criar a nuvem de palavras.
7. Clique em **Baixar** para salvar a imagem em PNG. Use **Limpar** para começar de novo.

Se quiser desconsiderar palavras muito comuns, como "de", "que" e "para", deixe marcada a opção **Ignorar palavras comuns**.

## Entendendo os termos

- **Nuvem de palavras:** imagem em que as palavras de um texto aparecem em tamanhos diferentes. Quanto mais uma palavra se repete, maior ela fica.
- **Frequência:** quantidade de vezes que uma palavra aparece no texto.
- **Esquema de cores:** conjunto de cores usado para pintar as palavras, como colorido, tons de azul ou preto e branco.
- **Cor de fundo:** cor atrás das palavras. Com a opção Transparente, a imagem baixada fica sem fundo.
- **Fonte:** tipo de letra usado nas palavras, como Impact, Arial ou Georgia.
- **Rotação das palavras:** define se as palavras ficam na horizontal (sem rotação), misturadas entre horizontal e vertical (aleatória) ou todas na vertical.
- **Número máximo de palavras:** limite de palavras exibidas na nuvem, começando pelas mais frequentes.
- **Fator de peso:** controla o contraste de tamanho entre as palavras. Valores maiores destacam ainda mais as palavras mais frequentes.
- **Resolução da imagem:** tamanho da imagem gerada, em pixels. Quanto maior, mais nítida a imagem e mais espaço para palavras.
- **Largura × Altura:** dimensões da imagem em pixels, na ordem largura e depois altura.
- **Palavras comuns:** termos muito usados no idioma, como artigos, preposições e pronomes, que quase não trazem informação e por isso podem ser ignorados.
- **PNG:** formato de imagem do arquivo baixado, que mantém a qualidade e permite fundo transparente.