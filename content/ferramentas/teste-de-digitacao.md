---
title: "Teste de Digitação"
seoTitle: "Teste de Digitação"
description: "Teste de Digitação: meça sua velocidade de digitação em palavras por minuto. Grátis e online, sem cadastro."
summary: "Meça sua velocidade de digitação em palavras por minuto."
date: 2026-11-11
draft: false
category: "util"
tags: ["digitação", "velocidade", "estudos", "produtividade"]
keywords: ["teste de digitação", "teste de digitação online", "digitação", "velocidade", "estudos"]
---

Escolha o tipo de texto e a duração, clique no campo de digitação e comece a escrever. O tempo começa a contar assim que você digitar a primeira tecla.

<div id="calc-digitacao" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⌨️ Teste de Digitação</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite as palavras abaixo o mais rápido que conseguir.</p>
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:16px;">
<div style="flex:1;min-width:180px;">
<label for="dig-acentos" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo de texto</label>
<select id="dig-acentos" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="com" selected>Com acentos</option>
<option value="sem">Sem acentos</option>
</select>
</div>
<div style="flex:1;min-width:180px;">
<label for="dig-duracao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Duração</label>
<select id="dig-duracao" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="15">15 segundos</option>
<option value="30">30 segundos</option>
<option value="60" selected>1 minuto</option>
<option value="120">2 minutos</option>
<option value="180">3 minutos</option>
<option value="300">5 minutos</option>
<option value="600">10 minutos</option>
</select>
</div>
</div>
<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px;">
<span style="font-weight:600;font-size:0.95rem;">Tempo restante</span>
<span id="dig-tempo" aria-live="off" style="padding:4px 14px;font-size:1.3rem;font-weight:700;color:#3730a3;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-variant-numeric:tabular-nums;">01:00</span>
</div>
<div id="dig-texto" style="position:relative;height:120px;overflow:hidden;margin-bottom:12px;padding:10px 12px;font-size:1.2rem;line-height:2;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;box-sizing:border-box;"></div>
<input id="dig-campo" type="text" placeholder="Comece a digitar aqui e use a barra de espaço para avançar" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="dig-novo" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Novo Teste</button>
<button type="button" id="dig-reiniciar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Reiniciar</button>
</div>
<div id="dig-resultado" aria-live="polite" style="display:none;margin-top:20px;padding:16px;background:#f0fdf4;border:2px dashed #86efac;border-radius:12px;color:#166534;font-size:1rem;line-height:1.6;">
<strong style="display:block;margin-bottom:12px;color:#166534;font-size:1.1rem;">Teste de Digitação Finalizado!</strong>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px;">
<div style="flex:1;min-width:130px;padding:12px;text-align:center;background:#ffffff;border:1px solid #bbf7d0;border-radius:10px;"><span id="dig-ppm" style="display:block;font-size:1.8rem;font-weight:700;color:#166534;">0</span><small style="color:#475569;">palavras por minuto</small></div>
<div style="flex:1;min-width:130px;padding:12px;text-align:center;background:#ffffff;border:1px solid #bbf7d0;border-radius:10px;"><span id="dig-tpm" style="display:block;font-size:1.8rem;font-weight:700;color:#166534;">0</span><small style="color:#475569;">toques por minuto</small></div>
<div style="flex:1;min-width:130px;padding:12px;text-align:center;background:#ffffff;border:1px solid #bbf7d0;border-radius:10px;"><span id="dig-prec" style="display:block;font-size:1.8rem;font-weight:700;color:#166534;">0%</span><small style="color:#475569;">precisão</small></div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="dig-tentar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Tentar Novamente</button>
<button type="button" id="dig-fechar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Fechar</button>
</div>
</div>
</div>
<script>
(function () {
  var POOL = ('casa tempo pessoa trabalho caminho escola amigo família cidade janela livro música lembrança história manhã noite coração vida mundo sempre ainda agora depois porque também então além através última único próximo ótimo câmera exercício saúde preço começo serviço ciência experiência memória jogo ação informação atenção educação você não até já são país três lição número rápido prática difícil fácil hábito português café pão avó irmã maçã sol lua mar rio terra água fogo vento chuva campo flor árvore pedra estrada ponte praça rua bairro cozinha quarto sala jardim porta mesa cadeira papel caneta caderno tela teclado mouse telefone computador internet mensagem resposta pergunta ideia projeto plano meta objetivo resultado sucesso esforço treino foco paciência coragem alegria saudade sonho verdade palavra frase texto leitura escrita aprender ensinar estudar escrever ler falar ouvir ver andar correr parar começar terminar continuar tentar conseguir precisar querer poder dever saber fazer dizer olhar pensar sentir viver bom bem grande pequeno novo velho forte leve claro simples certo ligado primeiro segundo mesmo outro cada todo muito pouco mais menos aqui ali hoje ontem amanhã cedo tarde').split(' ');
  var duracaoSel = document.getElementById('dig-duracao');
  var acentoSel = document.getElementById('dig-acentos');
  var tempoEl = document.getElementById('dig-tempo');
  var texto = document.getElementById('dig-texto');
  var campo = document.getElementById('dig-campo');
  var painel = document.getElementById('dig-resultado');
  var rPpm = document.getElementById('dig-ppm');
  var rTpm = document.getElementById('dig-tpm');
  var rPrec = document.getElementById('dig-prec');
  var palavras = [];
  var spans = [];
  var idx = 0;
  var tempo = 60;
  var timer = null;
  var iniciou = false;
  var terminou = false;
  var totalToques = 0;
  var toquesCertos = 0;
  var palavrasCertas = 0;
  var BASE = 'display:inline-block;padding:2px 6px;margin:2px 2px;border-radius:6px;';
  var ESTILO = {
    pend: 'color:#64748b;background:transparent;',
    atual: 'color:#3730a3;background:#e0e7ff;',
    ok: 'color:#166534;background:#f0fdf4;',
    erro: 'color:#b91c1c;background:#fef2f2;text-decoration:underline;'
  };
  function pintar(i, estado) { spans[i].style.cssText = BASE + ESTILO[estado]; }
  function semAcento(s) { return s.normalize('NFD').replace(/[\u0300-\u036f]/g, ''); }
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 0 }); }
  function mostrarTempo() {
    var m = Math.floor(tempo / 60);
    var s = tempo % 60;
    tempoEl.textContent = (m > 9 ? m : '0' + m) + ':' + (s > 9 ? s : '0' + s);
  }
  function addWords(n) {
    for (var k = 0; n > k; k++) {
      var w = POOL[Math.floor(Math.random() * POOL.length)];
      if (acentoSel.value === 'sem') { w = semAcento(w); }
      if (palavras.length > 0 && palavras[palavras.length - 1] === w) { w = w + 's'; }
      var sp = document.createElement('span');
      sp.textContent = w;
      palavras.push(w);
      spans.push(sp);
      texto.appendChild(sp);
      texto.appendChild(document.createTextNode(' '));
      pintar(spans.length - 1, 'pend');
    }
  }
  function reiniciar(novas, semFoco) {
    clearInterval(timer);
    timer = null;
    iniciou = false;
    terminou = false;
    idx = 0;
    totalToques = 0;
    toquesCertos = 0;
    palavrasCertas = 0;
    tempo = parseInt(duracaoSel.value, 10);
    painel.style.display = 'none';
    if (novas || spans.length === 0) {
      palavras = [];
      spans = [];
      texto.textContent = '';
      addWords(120);
    } else {
      for (var i = 0; spans.length > i; i++) { pintar(i, 'pend'); }
    }
    pintar(0, 'atual');
    texto.scrollTop = 0;
    campo.disabled = false;
    campo.value = '';
    mostrarTempo();
    if (!semFoco) { campo.focus(); }
  }
  function comparar(digitado, esperado) {
    var certos = 0;
    for (var k = 0; digitado.length > k; k++) {
      if (esperado.charAt(k) === digitado.charAt(k)) { certos++; }
    }
    return certos;
  }
  function confirmar(digitado, comEspaco, marcar) {
    var esperado = palavras[idx];
    var ok = digitado === esperado;
    totalToques += digitado.length + (comEspaco ? 1 : 0);
    toquesCertos += comparar(digitado, esperado) + (ok && comEspaco ? 1 : 0);
    if (ok) { palavrasCertas++; }
    if (marcar) {
      pintar(idx, ok ? 'ok' : 'erro');
      idx++;
      if (40 > palavras.length - idx) { addWords(60); }
      pintar(idx, 'atual');
      texto.scrollTop = Math.max(0, spans[idx].offsetTop - 12);
    }
  }
  function finalizar() {
    terminou = true;
    clearInterval(timer);
    timer = null;
    var resto = campo.value.replace(/\s+/g, '');
    if (resto !== '') { confirmar(resto, false, false); }
    campo.disabled = true;
    var minutos = parseInt(duracaoSel.value, 10) / 60;
    var ppm = Math.round(palavrasCertas / minutos);
    var tpm = Math.round(toquesCertos / minutos);
    var prec = totalToques > 0 ? Math.round((toquesCertos / totalToques) * 100) : 0;
    rPpm.textContent = fmt(ppm);
    rTpm.textContent = fmt(tpm);
    rPrec.textContent = prec + '%';
    painel.style.display = 'block';
  }
  function iniciar() {
    iniciou = true;
    timer = setInterval(function () {
      tempo -= 1;
      mostrarTempo();
      if (1 > tempo) { finalizar(); }
    }, 1000);
  }
  campo.addEventListener('input', function () {
    if (terminou) { return; }
    if (!iniciou) { iniciar(); }
    var v = campo.value;
    if (v.indexOf(' ') > -1) {
      var palavra = v.replace(/\s+/g, '');
      campo.value = '';
      if (palavra !== '') { confirmar(palavra, true, true); }
      return;
    }
    pintar(idx, palavras[idx].indexOf(v) === 0 ? 'atual' : 'erro');
  });
  document.getElementById('dig-novo').addEventListener('click', function () { reiniciar(true, false); });
  document.getElementById('dig-reiniciar').addEventListener('click', function () { reiniciar(false, false); });
  document.getElementById('dig-tentar').addEventListener('click', function () { reiniciar(true, false); });
  document.getElementById('dig-fechar').addEventListener('click', function () { painel.style.display = 'none'; });
  duracaoSel.addEventListener('change', function () { reiniciar(false, true); });
  acentoSel.addEventListener('change', function () { reiniciar(true, true); });
  [campo, duracaoSel, acentoSel].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  reiniciar(true, true);
})();
</script>

## Como usar o teste de digitação

1. Escolha o **tipo de texto**: **Com acentos** para palavras como "coração" e "você", ou **Sem acentos** para treinar sem acentuação.
2. Escolha a **duração** do teste, de 15 segundos até 10 minutos.
3. Clique no campo de digitação e comece a escrever a palavra destacada. O cronômetro inicia na primeira tecla.
4. Pressione a **barra de espaço** ao terminar cada palavra para passar para a próxima. Palavras corretas ficam verdes e erradas ficam vermelhas.
5. Quando o tempo acabar, veja seu resultado em **palavras por minuto**, **toques por minuto** e **precisão**.
6. Use **Novo Teste** para sortear outras palavras, **Reiniciar** para repetir as mesmas palavras ou **Tentar Novamente** na tela de resultado.

Dica: mantenha as mãos na posição correta do teclado e priorize a precisão antes da velocidade. Com o tempo, a velocidade aumenta naturalmente.

## Entendendo os termos

- **Teste de digitação:** exercício cronometrado que mede a rapidez e a exatidão com que você escreve no teclado.
- **Palavras por minuto (PPM):** quantidade de palavras digitadas corretamente em um minuto. É a medida mais usada de velocidade de digitação.
- **Toques por minuto (TPM):** quantidade de teclas corretas pressionadas em um minuto, incluindo os espaços entre as palavras.
- **Precisão:** porcentagem de toques corretos em relação ao total de toques feitos. Quanto mais perto de 100%, menos erros você cometeu.
- **Com acentos:** modo em que as palavras trazem acentos e cedilha (á, ã, é, ç etc.), como na escrita normal em português.
- **Sem acentos:** modo em que as palavras aparecem sem acentos e sem cedilha, útil para quem digita sem acentuar ou usa teclado estrangeiro.
- **Duração:** tempo total do teste. Testes mais longos mostram melhor sua velocidade constante.
- **Novo Teste:** sorteia um novo conjunto de palavras e reinicia o cronômetro.
- **Reiniciar:** zera o cronômetro e mantém as mesmas palavras, para você tentar superar o resultado anterior.