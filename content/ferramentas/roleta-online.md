---
title: "Roleta Online"
seoTitle: "Roleta Online"
description: "Roleta Online: gire a roleta e sorteie uma opção. Grátis e online, sem cadastro."
summary: "Gire a roleta e sorteie uma opção."
date: 2026-11-08
draft: false
category: "aleatorio"
tags: ["roleta", "jogos", "sorteio"]
keywords: ["roleta online", "roleta", "jogos", "sorteio"]
---
Basta digitar as opções abaixo (uma por linha) e depois clicar em **Girar**.

<div id="roleta-online" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎡 Roleta Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite as opções, gire a roleta e veja o resultado na hora.</p>
<canvas id="rol-canvas" width="600" height="600" style="display:block;width:100%;max-width:420px;height:auto;margin:0 auto 20px;"></canvas>
<label for="rol-opcoes" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Opções (uma por linha)</label>
<textarea id="rol-opcoes" rows="6" placeholder="Digite uma opção por linha" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:10px;">
<button type="button" id="rol-ordenar" style="flex:1;min-width:90px;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Ordenar</button>
<button type="button" id="rol-misturar" style="flex:1;min-width:90px;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Misturar</button>
<button type="button" id="rol-limpar" style="flex:1;min-width:90px;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<button type="button" id="rol-girar" style="width:100%;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Girar</button>
<div id="rol-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rol-resultado">preencha as opções e clique em "Girar".</span></div>
</div>
<script>
(function () {
  var campo = document.getElementById('rol-opcoes');
  var canvas = document.getElementById('rol-canvas');
  var ctx = canvas.getContext('2d');
  var resultado = document.getElementById('rol-resultado');
  var caixa = document.getElementById('rol-resposta');
  var btnGirar = document.getElementById('rol-girar');
  var btnOrdenar = document.getElementById('rol-ordenar');
  var btnMisturar = document.getElementById('rol-misturar');
  var btnLimpar = document.getElementById('rol-limpar');
  var cores = ['#4f46e5', '#7c3aed', '#0891b2', '#059669', '#d97706', '#dc2626', '#db2777', '#2563eb'];
  var PI2 = Math.PI * 2;
  var angulo = 0;
  var girando = false;
  var msgInicial = 'preencha as opções e clique em "Girar".';
  function mod(a, b) { return ((a % b) + b) % b; }
  function lerOpcoes() {
    return campo.value.split(/\r?\n/).map(function (t) { return t.trim(); }).filter(function (t) { return t !== ''; });
  }
  function escreverOpcoes(lista) { campo.value = lista.join('\n'); }
  function estadoNormal() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = msgInicial;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function corDaFatia(i, n) {
    var idx = i % cores.length;
    if (i === n - 1) {
      if (n > 1) {
        if (idx === 0) { idx = 1; }
      }
    }
    return cores[idx];
  }
  function cortar(texto) {
    if (texto.length > 16) { return texto.slice(0, 15) + '\u2026'; }
    return texto;
  }
  function desenhar() {
    var w = canvas.width;
    var c = w / 2;
    var r = c - 14;
    var lista = lerOpcoes();
    var n = lista.length;
    ctx.clearRect(0, 0, w, w);
    if (n === 0) {
      ctx.beginPath();
      ctx.arc(c, c, r, 0, PI2);
      ctx.fillStyle = '#e2e8f0';
      ctx.fill();
      ctx.lineWidth = 6;
      ctx.strokeStyle = '#c7d2fe';
      ctx.stroke();
      ctx.fillStyle = '#64748b';
      ctx.font = '600 26px system-ui, sans-serif';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText('Adicione opções', c, c);
    } else {
      var fatia = PI2 / n;
      var tamanho = 26;
      if (n > 8) { tamanho = 22; }
      if (n > 16) { tamanho = 18; }
      if (n > 30) { tamanho = 14; }
      for (var i = 0; i !== n; i++) {
        var ini = angulo + i * fatia;
        ctx.beginPath();
        ctx.moveTo(c, c);
        ctx.arc(c, c, r, ini, ini + fatia);
        ctx.closePath();
        ctx.fillStyle = corDaFatia(i, n);
        ctx.fill();
        ctx.lineWidth = 3;
        ctx.strokeStyle = '#ffffff';
        ctx.stroke();
        ctx.save();
        ctx.translate(c, c);
        ctx.rotate(ini + fatia / 2);
        ctx.textAlign = 'right';
        ctx.textBaseline = 'middle';
        ctx.fillStyle = '#ffffff';
        ctx.font = '700 ' + tamanho + 'px system-ui, sans-serif';
        ctx.fillText(cortar(lista[i]), r - 24, 0);
        ctx.restore();
      }
    }
    ctx.beginPath();
    ctx.arc(c, c, 26, 0, PI2);
    ctx.fillStyle = '#ffffff';
    ctx.fill();
    ctx.lineWidth = 5;
    ctx.strokeStyle = '#c7d2fe';
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(c - 22, 2);
    ctx.lineTo(c + 22, 2);
    ctx.lineTo(c, 46);
    ctx.closePath();
    ctx.fillStyle = '#1e293b';
    ctx.fill();
    ctx.lineWidth = 3;
    ctx.strokeStyle = '#ffffff';
    ctx.stroke();
  }
  function travar(sim) {
    girando = sim;
    campo.readOnly = sim;
    btnGirar.disabled = sim;
    btnOrdenar.disabled = sim;
    btnMisturar.disabled = sim;
    btnLimpar.disabled = sim;
    var op = sim ? '0.6' : '1';
    btnGirar.style.opacity = op;
    btnGirar.style.cursor = sim ? 'not-allowed' : 'pointer';
  }
  function finalizar(lista) {
    var n = lista.length;
    var fatia = PI2 / n;
    var idx = Math.floor(mod(Math.PI * 1.5 - angulo, PI2) / fatia);
    if (idx === n) { idx = n - 1; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode('O resultado do sorteio é '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = lista[idx];
    resultado.appendChild(forte);
    travar(false);
  }
  function girar() {
    if (girando) { return; }
    var lista = lerOpcoes();
    if (lista.length === 0) { erro('adicione pelo menos uma opção para girar a roleta.'); desenhar(); return; }
    travar(true);
    estadoNormal();
    resultado.textContent = 'girando...';
    var inicio = angulo;
    var total = (5 + Math.random() * 3) * PI2 + Math.random() * PI2;
    var duracao = 4500;
    var t0 = null;
    function passo(ts) {
      if (t0 === null) { t0 = ts; }
      var p = (ts - t0) / duracao;
      if (p >= 1) { p = 1; }
      var e = 1 - Math.pow(1 - p, 3);
      angulo = inicio + total * e;
      desenhar();
      if (p === 1) { finalizar(lista); } else { window.requestAnimationFrame(passo); }
    }
    window.requestAnimationFrame(passo);
  }
  function ordenar() {
    var lista = lerOpcoes();
    lista.sort(function (a, b) { return a.localeCompare(b, 'pt-BR', { numeric: true, sensitivity: 'base' }); });
    escreverOpcoes(lista);
    estadoNormal();
    desenhar();
  }
  function misturar() {
    var lista = lerOpcoes();
    for (var i = lista.length - 1; i > 0; i--) {
      var j = Math.floor(Math.random() * (i + 1));
      var tmp = lista[i];
      lista[i] = lista[j];
      lista[j] = tmp;
    }
    escreverOpcoes(lista);
    estadoNormal();
    desenhar();
  }
  function limpar() {
    campo.value = '';
    angulo = 0;
    estadoNormal();
    desenhar();
    campo.focus();
  }
  campo.addEventListener('input', function () { estadoNormal(); desenhar(); });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  btnGirar.addEventListener('click', girar);
  btnOrdenar.addEventListener('click', ordenar);
  btnMisturar.addEventListener('click', misturar);
  btnLimpar.addEventListener('click', limpar);
  escreverOpcoes(['Sim', 'Não']);
  desenhar();
})();
</script>

## Como usar a roleta

1. Digite as opções do sorteio na caixa de texto, **uma opção por linha** (nomes, números, letras, tarefas, "Sim" ou "Não" etc.).
2. Se quiser, clique em **Ordenar** para colocar as opções em ordem alfabética ou numérica, ou em **Misturar** para embaralhar a ordem.
3. Clique em **Girar** e aguarde a roleta parar. A opção apontada pelo ponteiro no topo é a sorteada.
4. O resultado aparece no campo **Resposta**, logo abaixo dos botões.
5. Use o botão **Limpar** para apagar todas as opções e montar uma nova roleta.

Cada opção ocupa uma fatia do mesmo tamanho, então todas têm a mesma chance de ser sorteada. Você pode repetir uma opção em linhas diferentes caso queira aumentar a chance dela. As linhas em branco são ignoradas.

## Entendendo os termos

- **Roleta:** círculo dividido em fatias que gira e para em uma delas, usado para sortear de forma aleatória.
- **Opção:** cada item digitado na lista, que vira uma fatia da roleta.
- **Fatia:** parte da roleta que representa uma opção. Todas têm o mesmo tamanho.
- **Ponteiro:** a seta fixa no topo da roleta que indica qual fatia foi sorteada quando ela para.
- **Girar:** inicia o giro da roleta, que dura alguns segundos e para em uma posição aleatória.
- **Ordenar:** organiza as opções em ordem alfabética (ou numérica, no caso de números).
- **Misturar:** embaralha as opções em uma ordem aleatória, sem apagar nenhuma delas.
- **Limpar:** remove todas as opções para você começar uma nova lista.
- **Sorteio:** escolha feita ao acaso, em que cada opção tem a mesma chance de ser selecionada.
- **Resultado:** a opção sorteada, exibida no campo Resposta ao final do giro.