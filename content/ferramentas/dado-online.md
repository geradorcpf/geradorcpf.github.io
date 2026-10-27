---
title: "Dado Online"
seoTitle: "Dado Online"
description: "Dado Online: jogue um ou mais dados online. Grátis e online, sem cadastro."
summary: "Jogue um ou mais dados online."
date: 2026-10-27
draft: false
category: "aleatorio"
tags: ["dado", "jogos", "sorteio"]
keywords: ["dado online", "dado", "jogos", "sorteio"]
---

<!--sudah dikerjakan-->

Escolha a quantidade de dados abaixo e depois clique em **Jogar**.

<div id="dado-online" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎲 Dado Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha quantos dados quer jogar e veja o resultado na hora.</p>
<label for="dado-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade de dados</label>
<select id="dado-quantidade" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="dado-jogar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Jogar</button>
<button type="button" id="dado-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="dado-palco" aria-hidden="true" style="display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:20px;"></div>
<div id="dado-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="dado-resultado">escolha a quantidade e clique em "Jogar".</span></div>
</div>
<script>
(function () {
  var qtd = document.getElementById('dado-quantidade');
  var palco = document.getElementById('dado-palco');
  var resultado = document.getElementById('dado-resultado');
  var caixa = document.getElementById('dado-resposta');
  var botao = document.getElementById('dado-jogar');
  var rolando = false;
  var padroes = {
    1: [4],
    2: [0, 8],
    3: [0, 4, 8],
    4: [0, 2, 6, 8],
    5: [0, 2, 4, 6, 8],
    6: [0, 2, 3, 5, 6, 8]
  };
  var posicoes = [0, 1, 2, 3, 4, 5, 6, 7, 8];
  var opcoes = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14];
  opcoes.forEach(function (n) {
    var o = document.createElement('option');
    o.value = String(n);
    o.textContent = n === 1 ? '1 dado' : n + ' dados';
    qtd.appendChild(o);
  });
  function sortear() {
    return Math.floor(Math.random() * 6) + 1;
  }
  function sortearVarios(n) {
    var lista = [];
    opcoes.slice(0, n).forEach(function () { lista.push(sortear()); });
    return lista;
  }
  function criarDado(valor) {
    var dado = document.createElement('div');
    dado.style.cssText = 'display:grid;grid-template-columns:repeat(3,1fr);grid-template-rows:repeat(3,1fr);gap:3px;width:60px;height:60px;padding:8px;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;box-shadow:0 4px 10px rgba(79,70,229,0.18);box-sizing:border-box;';
    posicoes.forEach(function (p) {
      var celula = document.createElement('div');
      if (padroes[valor].indexOf(p) !== -1) {
        celula.style.cssText = 'background:#4f46e5;border-radius:50%;';
      }
      dado.appendChild(celula);
    });
    return dado;
  }
  function mostrar(valores) {
    palco.textContent = '';
    valores.forEach(function (v) { palco.appendChild(criarDado(v)); });
  }
  function somar(valores) {
    return valores.reduce(function (total, v) { return total + v; }, 0);
  }
  function exibirResultado(valores) {
    var soma = somar(valores);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = String(soma);
    if (valores.length === 1) {
      resultado.appendChild(document.createTextNode('O dado caiu no número '));
      resultado.appendChild(forte);
      return;
    }
    resultado.appendChild(document.createTextNode('A soma dos dados é '));
    resultado.appendChild(forte);
    resultado.appendChild(document.createElement('br'));
    var detalhe = document.createElement('small');
    detalhe.style.color = '#475569';
    detalhe.textContent = valores.join(' + ') + ' = ' + soma;
    resultado.appendChild(detalhe);
  }
  function jogar() {
    if (rolando) { return; }
    rolando = true;
    botao.style.opacity = '0.7';
    var n = Number(qtd.value);
    var passos = 0;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'jogando...';
    var timer = setInterval(function () {
      passos += 1;
      if (passos === 10) {
        clearInterval(timer);
        var final = sortearVarios(n);
        mostrar(final);
        exibirResultado(final);
        rolando = false;
        botao.style.opacity = '1';
        return;
      }
      mostrar(sortearVarios(n));
    }, 80);
  }
  function limpar() {
    if (rolando) { return; }
    palco.textContent = '';
    qtd.value = '1';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'escolha a quantidade e clique em "Jogar".';
  }
  botao.addEventListener('click', jogar);
  document.getElementById('dado-limpar').addEventListener('click', limpar);
  qtd.addEventListener('focus', function () { qtd.style.borderColor = '#6366f1'; });
  qtd.addEventListener('blur', function () { qtd.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o dado online

1. No campo **Quantidade de dados**, escolha de 1 a 14 dados.
2. Clique em **Jogar** para lançar os dados.
3. Aguarde a animação rápida: os dados aparecem com as faces sorteadas.
4. Veja o resultado no quadro **Resposta**. Com mais de um dado, a soma e os valores de cada dado são exibidos.
5. Use o botão **Limpar** para apagar o resultado e voltar para 1 dado.

Você pode jogar quantas vezes quiser. Cada lançamento é independente dos anteriores e não precisa de cadastro.

## Entendendo os termos

- **Dado:** pequeno cubo com seis faces numeradas de 1 a 6, usado em jogos de tabuleiro, RPG e sorteios.
- **Face:** cada lado do dado. A face voltada para cima é o número que "saiu".
- **Jogar (ou lançar):** ação de rolar o dado para obter um número ao acaso.
- **Quantidade de dados:** número de dados lançados ao mesmo tempo, de 1 a 14.
- **Soma:** total obtido ao somar os números de todos os dados lançados.
- **Resultado aleatório:** número sorteado sem padrão previsível, em que cada face tem a mesma chance (1 em 6) de sair.
- **Sorteio:** escolha feita ao acaso, como decidir quem começa um jogo ou resolver um empate.