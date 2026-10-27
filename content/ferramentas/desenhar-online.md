---
title: "Desenhar Online"
seoTitle: "Desenhar Online"
description: "Desenhar Online: quadro de desenho livre no navegador. Grátis e online, sem cadastro."
summary: "Quadro de desenho livre no navegador."
date: 2026-10-27
draft: false
category: "util"
tags: ["desenho", "criatividade", "produtividade"]
keywords: ["desenhar online", "desenho", "criatividade", "produtividade"]
---

<!--sudah dikerjakan-->

Escolha uma ferramenta, selecione a cor e desenhe no quadro abaixo. Depois, clique em **Salvar Imagem** para baixar o seu desenho.

<div id="desenhar-online" style="max-width:720px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎨 Desenhar Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Desenhe à mão livre ou crie formas direto no navegador.</p>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ferramentas</div>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px;">
<button type="button" data-ferr="pincel" style="flex:1;min-width:110px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid #4f46e5;border-radius:10px;cursor:pointer;">✏️ Pincel</button>
<button type="button" data-ferr="apagador" style="flex:1;min-width:110px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">🧽 Apagador</button>
<button type="button" data-ferr="retangulo" style="flex:1;min-width:110px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">▭ Retângulo</button>
<button type="button" data-ferr="circulo" style="flex:1;min-width:110px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">◯ Círculo</button>
<button type="button" data-ferr="triangulo" style="flex:1;min-width:110px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">△ Triângulo</button>
</div>
<div style="display:flex;gap:20px;flex-wrap:wrap;align-items:center;margin-bottom:16px;">
<label for="des-tamanho" style="font-weight:600;font-size:0.95rem;">Tamanho: <span id="des-tam-valor">5</span> px</label>
<input id="des-tamanho" type="range" min="1" max="40" value="5" style="flex:1;min-width:140px;accent-color:#4f46e5;">
<label for="des-preencher" style="display:flex;align-items:center;gap:8px;font-weight:600;font-size:0.95rem;cursor:pointer;"><input id="des-preencher" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;">Preencher cor</label>
</div>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cores</div>
<div id="des-cores" style="display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:16px;">
<button type="button" data-cor="#000000" aria-label="Preto" style="width:34px;height:34px;background:#000000;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#ef4444" aria-label="Vermelho" style="width:34px;height:34px;background:#ef4444;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#f97316" aria-label="Laranja" style="width:34px;height:34px;background:#f97316;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#eab308" aria-label="Amarelo" style="width:34px;height:34px;background:#eab308;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#22c55e" aria-label="Verde" style="width:34px;height:34px;background:#22c55e;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#3b82f6" aria-label="Azul" style="width:34px;height:34px;background:#3b82f6;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#8b5cf6" aria-label="Roxo" style="width:34px;height:34px;background:#8b5cf6;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<button type="button" data-cor="#ec4899" aria-label="Rosa" style="width:34px;height:34px;background:#ec4899;border:3px solid #c7d2fe;border-radius:50%;cursor:pointer;padding:0;"></button>
<label for="des-cor-livre" style="margin-left:6px;font-size:0.9rem;color:#64748b;">Outra cor:</label>
<input id="des-cor-livre" type="color" value="#000000" style="width:42px;height:34px;padding:0;border:2px solid #c7d2fe;border-radius:8px;background:#ffffff;cursor:pointer;">
</div>
<canvas id="des-canvas" width="800" height="500" style="display:block;width:100%;height:auto;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;cursor:crosshair;touch-action:none;box-sizing:border-box;"></canvas>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:20px;">
<button type="button" id="des-salvar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Salvar Imagem</button>
<button type="button" id="des-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar Tela</button>
</div>
</div>
<script>
(function () {
  var cv = document.getElementById('des-canvas');
  var ctx = cv.getContext('2d');
  var tamanho = document.getElementById('des-tamanho');
  var rotuloTam = document.getElementById('des-tam-valor');
  var preencher = document.getElementById('des-preencher');
  var corLivre = document.getElementById('des-cor-livre');
  var botoesFerr = document.querySelectorAll('[data-ferr]');
  var botoesCor = document.querySelectorAll('[data-cor]');
  var ferramenta = 'pincel';
  var cor = '#000000';
  var desenhando = false;
  var ix = 0;
  var iy = 0;
  var snap = null;
  function fundo() {
    ctx.globalCompositeOperation = 'source-over';
    ctx.fillStyle = '#ffffff';
    ctx.fillRect(0, 0, cv.width, cv.height);
  }
  function pos(e) {
    var r = cv.getBoundingClientRect();
    return { x: (e.clientX - r.left) * (cv.width / r.width), y: (e.clientY - r.top) * (cv.height / r.height) };
  }
  function marcarFerramenta() {
    botoesFerr.forEach(function (b) {
      var ativo = b.getAttribute('data-ferr') === ferramenta;
      b.style.background = ativo ? 'linear-gradient(135deg,#4f46e5,#6366f1)' : '#ffffff';
      b.style.color = ativo ? '#ffffff' : '#4f46e5';
      b.style.borderColor = ativo ? '#4f46e5' : '#c7d2fe';
    });
  }
  function marcarCor() {
    botoesCor.forEach(function (b) {
      var ativo = b.getAttribute('data-cor') === cor;
      b.style.borderColor = ativo ? '#4f46e5' : '#c7d2fe';
      b.style.transform = ativo ? 'scale(1.15)' : 'scale(1)';
    });
  }
  function desenharForma(x, y) {
    ctx.beginPath();
    if (ferramenta === 'retangulo') {
      ctx.rect(ix, iy, x - ix, y - iy);
    } else if (ferramenta === 'circulo') {
      ctx.arc(ix, iy, Math.sqrt(Math.pow(x - ix, 2) + Math.pow(y - iy, 2)), 0, Math.PI * 2);
    } else {
      ctx.moveTo(ix + (x - ix) / 2, iy);
      ctx.lineTo(x, y);
      ctx.lineTo(ix, y);
      ctx.closePath();
    }
    if (preencher.checked) { ctx.fill(); }
    ctx.stroke();
  }
  function iniciar(e) {
    e.preventDefault();
    var p = pos(e);
    desenhando = true;
    ix = p.x;
    iy = p.y;
    try { cv.setPointerCapture(e.pointerId); } catch (err) {}
    ctx.globalCompositeOperation = 'source-over';
    ctx.lineWidth = Number(tamanho.value);
    ctx.lineCap = 'round';
    ctx.lineJoin = 'round';
    ctx.strokeStyle = ferramenta === 'apagador' ? '#ffffff' : cor;
    ctx.fillStyle = cor;
    if (ferramenta === 'pincel' || ferramenta === 'apagador') {
      ctx.beginPath();
      ctx.moveTo(ix, iy);
      ctx.lineTo(ix + 0.01, iy);
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(ix, iy);
    } else {
      snap = ctx.getImageData(0, 0, cv.width, cv.height);
    }
  }
  function mover(e) {
    if (!desenhando) { return; }
    var p = pos(e);
    if (ferramenta === 'pincel' || ferramenta === 'apagador') {
      ctx.lineTo(p.x, p.y);
      ctx.stroke();
    } else {
      ctx.putImageData(snap, 0, 0);
      desenharForma(p.x, p.y);
    }
  }
  function terminar() {
    desenhando = false;
    snap = null;
  }
  function limpar() {
    fundo();
  }
  function salvar() {
    var a = document.createElement('a');
    a.href = cv.toDataURL('image/png');
    a.download = 'desenho.png';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
  }
  botoesFerr.forEach(function (b) {
    b.addEventListener('click', function () {
      ferramenta = b.getAttribute('data-ferr');
      marcarFerramenta();
    });
  });
  botoesCor.forEach(function (b) {
    b.addEventListener('click', function () {
      cor = b.getAttribute('data-cor');
      corLivre.value = cor;
      marcarCor();
    });
  });
  corLivre.addEventListener('input', function () {
    cor = corLivre.value;
    marcarCor();
  });
  tamanho.addEventListener('input', function () {
    rotuloTam.textContent = tamanho.value;
  });
  cv.addEventListener('pointerdown', iniciar);
  cv.addEventListener('pointermove', mover);
  cv.addEventListener('pointerup', terminar);
  cv.addEventListener('pointercancel', terminar);
  document.getElementById('des-limpar').addEventListener('click', limpar);
  document.getElementById('des-salvar').addEventListener('click', salvar);
  fundo();
  marcarFerramenta();
  marcarCor();
})();
</script>

## Como usar a ferramenta

1. Escolha uma **ferramenta**: Pincel, Apagador, Retângulo, Círculo ou Triângulo.
2. Ajuste o **Tamanho** da linha com o controle deslizante.
3. Clique em uma das **cores** da paleta ou use **Outra cor** para escolher qualquer tom.
4. Clique e arraste com o mouse (ou deslize o dedo no celular) sobre o quadro para desenhar.
5. Para formas, marque **Preencher cor** se quiser que o interior seja colorido. Sem essa opção, só o contorno é desenhado.
6. Clique em **Limpar Tela** para apagar tudo e começar de novo.
7. Clique em **Salvar Imagem** para baixar o desenho em formato PNG.

Nas formas, o desenho aparece enquanto você arrasta e só fica fixo quando você solta o mouse ou o dedo. No Círculo, o ponto onde você clica é o centro, e a distância até onde você arrastar define o raio.

## Entendendo os termos

- **Pincel:** ferramenta de desenho à mão livre. Traça uma linha seguindo o movimento do mouse ou do dedo.
- **Apagador:** ferramenta que apaga o que foi desenhado, pintando por cima com a cor do fundo (branco).
- **Retângulo:** forma de quatro lados com ângulos retos, desenhada a partir de dois cantos opostos.
- **Círculo:** forma redonda desenhada a partir do centro, com o raio definido pela distância do arrasto.
- **Triângulo:** forma de três lados, desenhada dentro da área marcada pelo arrasto.
- **Preencher cor:** opção que pinta o interior das formas com a cor selecionada, além do contorno.
- **Tamanho:** espessura da linha do pincel, do apagador e dos contornos das formas, medida em pixels (px).
- **Cores:** paleta de cores prontas. A opção **Outra cor** permite escolher qualquer cor.
- **Limpar Tela:** botão que apaga todo o desenho e deixa o quadro em branco.
- **Salvar Imagem:** botão que baixa o desenho como arquivo de imagem PNG.
- **Quadro (canvas):** área branca onde o desenho é feito.