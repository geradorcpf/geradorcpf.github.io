---
title: "Gerador de Números da Megasena"
seoTitle: "Gerador de Números da Megasena"
description: "Gerador de Números da Megasena: gere palpites de seis dezenas para a Mega-Sena. Grátis e online, sem cadastro."
summary: "Gere palpites de seis dezenas para a Mega-Sena."
date: 2026-11-02
draft: false
category: "aleatorio"
tags: ["loteria", "mega-sena", "números aleatórios", "sorteio"]
keywords: ["gerador de números da megasena", "gerador de números da megasena online", "loteria", "mega-sena", "números aleatórios"]
---

Basta escolher quantos números você quer no seu jogo e depois clicar em **Gerar Números**.

<div id="calc-megasena" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🍀 Gerador de Números da Megasena</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a quantidade de dezenas e gere seu palpite na hora.</p>
<label for="mega-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade de números</label>
<select id="mega-quantidade" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="6">6 Números</option>
<option value="7">7 Números</option>
<option value="8">8 Números</option>
<option value="9">9 Números</option>
<option value="10">10 Números</option>
<option value="11">11 Números</option>
<option value="12">12 Números</option>
<option value="13">13 Números</option>
<option value="14">14 Números</option>
<option value="15">15 Números</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="mega-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Números</button>
<button type="button" id="mega-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="mega-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="mega-resultado">escolha a quantidade e clique em "Gerar Números".</span></div>
</div>
<script>
(function () {
  var seletor = document.getElementById('mega-quantidade');
  var resultado = document.getElementById('mega-resultado');
  var caixa = document.getElementById('mega-resposta');
  var textoInicial = 'escolha a quantidade e clique em "Gerar Números".';
  function aleatorio() {
    try {
      var buf = new Uint32Array(1);
      window.crypto.getRandomValues(buf);
      return buf[0] / 4294967296;
    } catch (e) {
      return Math.random();
    }
  }
  function sortear(qtd) {
    var pool = [];
    var i;
    for (i = 1; i !== 61; i++) { pool.push(i); }
    for (i = 59; i > 0; i--) {
      var j = Math.floor(aleatorio() * (i + 1));
      var t = pool[i];
      pool[i] = pool[j];
      pool[j] = t;
    }
    return pool.slice(0, qtd).sort(function (x, y) { return x - y; });
  }
  function dois(n) { return n > 9 ? String(n) : '0' + n; }
  function bola(n) {
    var el = document.createElement('span');
    el.textContent = dois(n);
    el.style.cssText = 'display:inline-flex;align-items:center;justify-content:center;width:44px;height:44px;margin:4px;border-radius:50%;background:linear-gradient(135deg,#4f46e5,#6366f1);color:#ffffff;font-weight:700;font-size:1.05rem;box-shadow:0 4px 10px rgba(79,70,229,0.35);';
    return el;
  }
  function gerar() {
    var qtd = parseInt(seletor.value, 10);
    var numeros = sortear(qtd);
    var rotulo = document.createElement('div');
    var forte = document.createElement('strong');
    var lista = document.createElement('div');
    var i;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    forte.style.fontSize = '1.1rem';
    forte.textContent = 'Seu palpite com ' + qtd + ' números:';
    rotulo.appendChild(forte);
    for (i = 0; i !== numeros.length; i++) { lista.appendChild(bola(numeros[i])); }
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
    resultado.appendChild(rotulo);
    resultado.appendChild(lista);
  }
  function limpar() {
    seletor.value = '6';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
    resultado.textContent = textoInicial;
    seletor.focus();
  }
  document.getElementById('mega-gerar').addEventListener('click', gerar);
  document.getElementById('mega-limpar').addEventListener('click', limpar);
  seletor.addEventListener('focus', function () { seletor.style.borderColor = '#6366f1'; });
  seletor.addEventListener('blur', function () { seletor.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. No campo **Quantidade de números**, escolha quantas dezenas terá o seu jogo, de 6 a 15.
2. Clique em **Gerar Números** para sortear o palpite.
3. Os números aparecem em ordem crescente, dentro das bolinhas, prontos para você marcar no volante.
4. Clique em **Gerar Números** de novo quantas vezes quiser para obter novos palpites.
5. Use o botão **Limpar** para apagar o resultado e voltar à opção de 6 números.

Os números são sorteados entre 1 e 60, sem repetição dentro do mesmo jogo. Lembre-se de que o gerador cria palpites aleatórios: ele não aumenta nem diminui a chance de ganhar, e todas as combinações têm a mesma probabilidade.

## Entendendo os termos

- **Mega-Sena:** loteria da Caixa Econômica Federal em que se escolhem dezenas entre 1 e 60 e se concorre a prêmios ao acertar 4, 5 ou 6 delas.
- **Dezena:** cada um dos números que podem ser marcados no volante, de 01 a 60.
- **Palpite:** conjunto de dezenas escolhido para apostar, neste caso gerado de forma aleatória.
- **Aposta simples:** jogo com 6 dezenas, a quantidade mínima permitida.
- **Aposta com mais dezenas:** jogo com 7 a 15 dezenas. Quanto mais dezenas, maiores as combinações cobertas e também o valor da aposta.
- **Volante:** cartela da loteria onde as dezenas escolhidas são marcadas.
- **Sorteio:** extração das seis dezenas vencedoras feita pela Caixa.
- **Número aleatório:** número escolhido ao acaso, sem padrão e sem influência de sorteios anteriores.
- **Ordem crescente:** organização dos números do menor para o maior, que facilita a conferência do jogo.