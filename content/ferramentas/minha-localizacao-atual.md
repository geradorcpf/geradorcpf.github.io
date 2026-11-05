---
title: "Minha Localização Atual"
seoTitle: "Minha Localização Atual"
description: "Minha Localização Atual: veja sua localização aproximada no mapa. Grátis e online, sem cadastro."
summary: "Veja sua localização aproximada no mapa."
date: 2026-11-05
draft: false
category: "rede"
tags: ["geolocalização", "localização", "mapas"]
keywords: ["minha localização atual", "minha localização atual online", "geolocalização", "localização", "mapas"]
---

Qual é a minha localização atual? Onde estou? Esta ferramenta mostra suas coordenadas geográficas (latitude e longitude) e a sua posição no mapa. Ao abrir a página, o navegador pede permissão para acessar a localização. Aceite a solicitação para ver o resultado.

<div id="calc-localizacao" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📍 Minha Localização Atual</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Veja suas coordenadas e sua posição no mapa.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<button type="button" id="loc-obter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Obter Localização</button>
<button type="button" id="loc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="loc-resposta" aria-live="polite" style="padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.8;">
<div><strong style="color:#3730a3;">Status:</strong> <span id="loc-status">aguardando...</span></div>
<div><strong style="color:#3730a3;">Latitude:</strong> <span id="loc-lat">-</span></div>
<div><strong style="color:#3730a3;">Longitude:</strong> <span id="loc-lon">-</span></div>
<div><strong style="color:#3730a3;">Precisão:</strong> <span id="loc-prec">-</span></div>
</div>
<div id="loc-mapa-box" style="display:none;margin-top:20px;">
<iframe id="loc-mapa" title="Mapa com a sua localização atual" width="100%" height="280" frameborder="0" loading="lazy" style="display:block;border:2px solid #c7d2fe;border-radius:12px;background:#ffffff;box-sizing:border-box;"></iframe>
<p style="margin:10px 0 0;font-size:0.85rem;"><a id="loc-link" href="https://www.openstreetmap.org/" target="_blank" rel="noopener noreferrer" style="color:#4f46e5;font-weight:600;">Abrir mapa em tela cheia</a></p>
</div>
</div>
<script>
(function () {
  var status = document.getElementById('loc-status');
  var latEl = document.getElementById('loc-lat');
  var lonEl = document.getElementById('loc-lon');
  var precEl = document.getElementById('loc-prec');
  var caixa = document.getElementById('loc-resposta');
  var mapaBox = document.getElementById('loc-mapa-box');
  var mapa = document.getElementById('loc-mapa');
  var link = document.getElementById('loc-link');
  function fmt(n, d) {
    return n.toLocaleString('pt-BR', { minimumFractionDigits: d, maximumFractionDigits: d });
  }
  function estado(cor, fundo, borda, msg) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    status.style.color = cor;
    status.textContent = msg;
  }
  function zerar() {
    latEl.textContent = '-';
    lonEl.textContent = '-';
    precEl.textContent = '-';
    mapa.removeAttribute('src');
    mapaBox.style.display = 'none';
  }
  function sucesso(pos) {
    var lat = pos.coords.latitude;
    var lon = pos.coords.longitude;
    var acc = pos.coords.accuracy;
    var d = 0.005;
    var bbox = (lon - d) + ',' + (lat - d) + ',' + (lon + d) + ',' + (lat + d);
    estado('#166534', '#f0fdf4', '#86efac', 'localização encontrada.');
    latEl.textContent = fmt(lat, 6);
    lonEl.textContent = fmt(lon, 6);
    precEl.textContent = (typeof acc === 'number') ? 'cerca de ' + fmt(Math.round(acc), 0) + ' m' : '-';
    mapa.src = 'https://www.openstreetmap.org/export/embed.html?bbox=' + encodeURIComponent(bbox) + '&layer=mapnik&marker=' + encodeURIComponent(lat + ',' + lon);
    link.href = 'https://www.openstreetmap.org/?mlat=' + lat + '&mlon=' + lon + '#map=16/' + lat + '/' + lon;
    mapaBox.style.display = 'block';
  }
  function falha(err) {
    var msg = 'não foi possível obter a localização.';
    if (err && err.code === 1) { msg = 'permissão negada. Libere o acesso à localização no navegador.'; }
    else if (err && err.code === 2) { msg = 'localização indisponível no momento.'; }
    else if (err && err.code === 3) { msg = 'tempo esgotado. Tente novamente.'; }
    zerar();
    estado('#b91c1c', '#fef2f2', '#fca5a5', msg);
  }
  function obter() {
    zerar();
    if (!navigator.geolocation) {
      estado('#b91c1c', '#fef2f2', '#fca5a5', 'seu navegador não suporta geolocalização.');
      return;
    }
    estado('#64748b', '#ffffff', '#c7d2fe', 'checando...');
    navigator.geolocation.getCurrentPosition(sucesso, falha, { enableHighAccuracy: true, timeout: 15000, maximumAge: 0 });
  }
  function limpar() {
    zerar();
    estado('#64748b', '#ffffff', '#c7d2fe', 'aguardando...');
  }
  document.getElementById('loc-obter').addEventListener('click', obter);
  document.getElementById('loc-limpar').addEventListener('click', limpar);
  obter();
})();
</script>

## Como usar a ferramenta

1. Abra a página e, quando o navegador perguntar, clique em **Permitir** para liberar o acesso à sua localização.
2. Aguarde alguns segundos. O **Status** muda de "checando..." para "localização encontrada".
3. Veja sua **Latitude**, **Longitude** e a **Precisão** estimada, além do mapa com o marcador na sua posição.
4. Se a permissão foi negada ou deu erro, libere a localização nas configurações do navegador e clique em **Obter Localização** para tentar de novo.
5. Use o botão **Limpar** para apagar o resultado exibido.

Para funcionar, use um navegador atualizado e acesse a página por conexão segura (HTTPS). A localização é mais precisa em dispositivos com GPS, como smartphones. Em computadores, ela costuma ser aproximada, pois depende da rede Wi-Fi ou do endereço IP. A leitura acontece apenas no seu navegador.

## Entendendo os termos

- **Localização atual:** posição em que você está agora, informada pelo seu dispositivo.
- **Geolocalização:** tecnologia que identifica a posição geográfica de um dispositivo usando GPS, redes Wi-Fi, torres de celular ou endereço IP.
- **Coordenadas geográficas:** par de números (latitude e longitude) que indica um ponto exato na superfície da Terra.
- **Latitude:** distância angular de um ponto até a linha do Equador, em graus. Valores negativos indicam o hemisfério Sul e positivos, o Norte.
- **Longitude:** distância angular de um ponto até o Meridiano de Greenwich, em graus. Valores negativos indicam o Oeste e positivos, o Leste.
- **GPS:** sistema de satélites que determina a posição com alta precisão, comum em smartphones.
- **Precisão:** margem de erro da localização, em metros. Quanto menor o valor, mais exata é a posição.
- **Permissão de localização:** autorização que você concede ao navegador para compartilhar a sua posição com a página.
- **Status:** situação atual da busca, como "checando...", "localização encontrada" ou uma mensagem de erro.
- **Mapa:** representação visual da região, com um marcador indicando onde você está.