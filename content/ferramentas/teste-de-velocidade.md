---
title: "Teste de Velocidade"
seoTitle: "Teste de Velocidade"
description: "Teste de Velocidade: meça a velocidade de download e upload da sua internet. Grátis e online, sem cadastro."
summary: "Meça a velocidade de download e upload da sua internet."
date: 2026-11-11
draft: false
category: "rede"
tags: ["velocidade", "internet", "diagnóstico", "rede"]
keywords: ["teste de velocidade", "teste de velocidade online", "velocidade", "internet", "diagnóstico"]
---

Basta clicar em **Iniciar Teste** abaixo e aguardar o resultado da sua conexão.

<div id="teste-velocidade" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🚀 Teste de Velocidade</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Meça o download, o upload e a latência da sua internet.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="vel-iniciar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Iniciar Teste</button>
<button type="button" id="vel-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="vel-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="vel-resultado">clique em "Iniciar Teste" para medir sua velocidade.</span><div id="vel-quadro" style="margin-top:12px;"></div></div>
<p style="margin:14px 0 0;font-size:0.85rem;color:#64748b;">Se o teste não aparecer, <a id="vel-link" href="https://fast.com/pt/" target="_blank" rel="noopener noreferrer" style="color:#4f46e5;font-weight:600;">abra o teste em outra aba</a>.</p>
</div>
<script>
(function () {
  var iniciar = document.getElementById('vel-iniciar');
  var limpar = document.getElementById('vel-limpar');
  var caixa = document.getElementById('vel-resposta');
  var resultado = document.getElementById('vel-resultado');
  var quadro = document.getElementById('vel-quadro');
  function carregar() {
    quadro.innerHTML = '';
    var frame = document.createElement('iframe');
    frame.src = 'https://fast.com/pt/';
    frame.title = 'Teste de velocidade da internet';
    frame.setAttribute('allow', 'fullscreen');
    frame.style.cssText = 'width:100%;height:380px;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;box-sizing:border-box;';
    quadro.appendChild(frame);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = 'teste em andamento. Aguarde o número final (em Mbps).';
    iniciar.textContent = 'Testar Novamente';
  }
  function reiniciar() {
    quadro.innerHTML = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'clique em "Iniciar Teste" para medir sua velocidade.';
    iniciar.textContent = 'Iniciar Teste';
    iniciar.focus();
  }
  iniciar.addEventListener('click', carregar);
  limpar.addEventListener('click', reiniciar);
})();
</script>

## Como usar o teste

1. Clique em **Iniciar Teste** para abrir o medidor de velocidade.
2. Aguarde alguns segundos: o teste baixa e envia dados de servidores próximos para medir sua conexão.
3. Veja o número grande, que é a velocidade de **download**, em Mbps.
4. Clique em **Mostrar mais informações** dentro do teste para ver também o **upload** e a **latência**.
5. Clique em **Testar Novamente** para repetir a medição ou em **Limpar** para fechar o teste.

Para um resultado mais confiável, ligue o computador ao roteador por cabo (ou fique perto do roteador, se usar Wi-Fi), feche downloads, vídeos e atualizações e confira se outros aparelhos não estão usando a internet. Repita o teste em horários e dias diferentes, pois à noite a rede costuma ficar mais carregada.

## Entendendo os termos

- **Velocidade de download:** rapidez com que dados chegam até você. É usada para assistir a vídeos, abrir sites e baixar arquivos.
- **Velocidade de upload:** rapidez com que você envia dados. É usada para enviar arquivos e fazer videochamadas.
- **Latência:** tempo de resposta da conexão, medido em milissegundos (ms). É importante em jogos online e chamadas.
- **Mbps (megabits por segundo):** unidade usada para medir a velocidade da internet.
- **MB/s (megabytes por segundo):** unidade usada para medir a taxa de transferência de arquivos. 1 byte tem 8 bits, então 1 MB/s equivale a 8 Mbps.
- **Velocidade contratada:** velocidade máxima prometida pela operadora no seu plano de internet.
- **Roteador:** aparelho que distribui o sinal da internet para os dispositivos da casa, por cabo ou Wi-Fi.
- **Horário de pico:** período em que muitas pessoas usam a internet ao mesmo tempo, o que pode reduzir a velocidade.
- **Fast.com:** ferramenta de teste de velocidade da Netflix, que mede a conexão com os mesmos servidores que entregam os vídeos da Netflix.
- **Anatel:** agência que regula as operadoras de telecomunicações no Brasil e exige uma velocidade mínima em relação à contratada.

## Mbps não é MB/s

A velocidade da internet é medida em megabits por segundo (Mbps), e o tamanho dos arquivos, em megabytes (MB). Como 1 byte tem 8 bits, basta dividir os Mbps por 8 para saber quantos MB por segundo você baixa.

**MB/s = Mbps ÷ 8**

Por exemplo, uma internet de 100 Mbps baixa, no máximo, cerca de **12,5 MB por segundo**.

## Por que o resultado é menor que a velocidade contratada?

O Wi-Fi, a distância até o roteador, o próprio aparelho e o horário de pico costumam reduzir a velocidade. Se o teste feito por cabo, sem nada mais usando a internet, também ficar bem abaixo do contratado, o problema pode estar na operadora. Nesse caso, guarde os resultados de vários testes, com data e hora, e reclame com a operadora. Se ela não resolver, registre a reclamação na Anatel ou no consumidor.gov.br.