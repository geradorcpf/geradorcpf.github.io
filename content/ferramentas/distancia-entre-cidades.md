---
title: "Distância Entre Cidades"
seoTitle: "Distância Entre Cidades"
description: "Distância Entre Cidades: calcule a distância entre duas cidades. Grátis e online, sem cadastro."
summary: "Calcule a distância entre duas cidades."
date: 2026-10-27
draft: false
category: "util"
tags: ["mapas", "viagem", "localização"]
keywords: ["distância entre cidades", "distância entre cidades online", "mapas", "viagem", "localização"]
---
<!--sudah dikerjakan-->

Basta digitar a cidade de origem e a cidade de destino abaixo e depois clicar em **Calcular Distância**.

<div id="calc-distancia" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📍 Distância Entre Cidades</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe a origem e o destino e veja o resultado na hora.</p>
<label for="dist-origem" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Origem</label>
<input id="dist-origem" type="text" placeholder="Ex.: São Paulo, SP" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="dist-destino" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Destino</label>
<input id="dist-destino" type="text" placeholder="Ex.: Rio de Janeiro, RJ" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="dist-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Distância</button>
<button type="button" id="dist-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="dist-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="dist-resultado">preencha os campos e clique em "Calcular Distância".</span></div>
</div>
<script>
(function () {
  var origem = document.getElementById('dist-origem');
  var destino = document.getElementById('dist-destino');
  var resultado = document.getElementById('dist-resultado');
  var caixa = document.getElementById('dist-resposta');
  var botao = document.getElementById('dist-calcular');
  var contador = 0;
  var URL_GEO = 'https://nominatim.openstreetmap.org/search?format=json&limit=1&accept-language=pt-BR&q=';
  var URL_ROTA = 'https://router.project-osrm.org/route/v1/driving/';
  function esvaziar() {
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
  }
  function cores(borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
  }
  function texto(msg) {
    esvaziar();
    resultado.textContent = msg;
  }
  function erro(msg) {
    cores('#fca5a5', '#fef2f2', '#b91c1c');
    texto(msg);
  }
  function linha(rotulo, valor) {
    var div = document.createElement('div');
    var rot = document.createElement('span');
    var val = document.createElement('strong');
    rot.textContent = rotulo + ': ';
    val.textContent = valor;
    div.appendChild(rot);
    div.appendChild(val);
    resultado.appendChild(div);
  }
  function nota(msg) {
    var div = document.createElement('div');
    div.style.fontSize = '0.8rem';
    div.style.color = '#475569';
    div.style.marginTop = '8px';
    div.textContent = msg;
    resultado.appendChild(div);
  }
  function fmtKm(n) {
    return n.toLocaleString('pt-BR', { maximumFractionDigits: 1 }) + ' km';
  }
  function fmtTempo(segundos) {
    var min = Math.round(segundos / 60);
    var h = Math.floor(min / 60);
    var m = min - h * 60;
    return (h ? h + ' h ' : '') + m + ' min';
  }
  function nomeCurto(nome) {
    var partes = String(nome).split(',');
    var primeiro = partes[0].trim();
    var ultimo = partes[partes.length - 1].trim();
    return primeiro === ultimo ? primeiro : primeiro + ', ' + ultimo;
  }
  function pegarJson(url) {
    return fetch(url).then(function (resp) {
      return resp.text().then(function (corpo) {
        try {
          return JSON.parse(corpo);
        } catch (e) {
          throw new Error('o serviço de mapas respondeu de forma inesperada. Tente novamente em instantes.');
        }
      });
    });
  }
  function geocodificar(busca) {
    return pegarJson(URL_GEO + encodeURIComponent(busca)).then(function (res) {
      if (!Array.isArray(res) || !res.length) {
        throw new Error('não encontrei "' + busca + '". Tente incluir o estado ou o país.');
      }
      return { lat: parseFloat(res[0].lat), lon: parseFloat(res[0].lon), nome: nomeCurto(res[0].display_name) };
    });
  }
  function buscarRota(a, b) {
    var url = URL_ROTA + a.lon + ',' + a.lat + ';' + b.lon + ',' + b.lat + '?overview=false';
    return pegarJson(url).then(function (dados) {
      if (!dados || dados.code !== 'Ok' || !dados.routes || !dados.routes.length) {
        throw new Error('rota não encontrada');
      }
      return dados.routes[0];
    });
  }
  function linhaReta(a, b) {
    var rad = Math.PI / 180;
    var dLat = (b.lat - a.lat) * rad;
    var dLon = (b.lon - a.lon) * rad;
    var x = Math.sin(dLat / 2) * Math.sin(dLat / 2) + Math.cos(a.lat * rad) * Math.cos(b.lat * rad) * Math.sin(dLon / 2) * Math.sin(dLon / 2);
    return 6371 * 2 * Math.atan2(Math.sqrt(x), Math.sqrt(1 - x));
  }
  function liberarBotao(id) {
    if (id === contador) {
      botao.disabled = false;
      botao.textContent = 'Calcular Distância';
    }
  }
  function calcular() {
    var o = origem.value.trim();
    var d = destino.value.trim();
    if (!o || !d) { erro('informe a cidade de origem e a cidade de destino.'); return; }
    contador += 1;
    var id = contador;
    var pontoA = null;
    var pontoB = null;
    botao.disabled = true;
    botao.textContent = 'Calculando...';
    cores('#c7d2fe', '#ffffff', '#64748b');
    esvaziar();
    linha('Distância por estrada', 'carregando...');
    linha('Duração', 'carregando...');
    geocodificar(o).then(function (r) {
      pontoA = r;
      return geocodificar(d);
    }).then(function (r) {
      pontoB = r;
      return buscarRota(pontoA, pontoB).then(function (rota) { return rota; }, function () { return null; });
    }).then(function (rota) {
      if (id !== contador) { return; }
      cores('#86efac', '#f0fdf4', '#166534');
      esvaziar();
      if (rota) {
        linha('Distância por estrada', fmtKm(rota.distance / 1000));
        linha('Duração', fmtTempo(rota.duration));
      } else {
        linha('Distância por estrada', 'não disponível para este trajeto');
      }
      linha('Distância em linha reta', fmtKm(linhaReta(pontoA, pontoB)));
      nota(pontoA.nome + ' → ' + pontoB.nome);
    }).catch(function (e) {
      if (id !== contador) { return; }
      if (window.console) { console.error('Distância Entre Cidades:', e); }
      var msg = e && e.message ? e.message : '';
      if (e instanceof TypeError) {
        msg = 'não consegui conectar ao serviço de mapas. Verifique a internet, o bloqueador de anúncios ou as restrições do site (CSP/CORS).';
      }
      erro(msg || 'não foi possível calcular agora. Tente novamente.');
    }).then(function () {
      liberarBotao(id);
    });
  }
  function limpar() {
    contador += 1;
    origem.value = '';
    destino.value = '';
    botao.disabled = false;
    botao.textContent = 'Calcular Distância';
    cores('#c7d2fe', '#ffffff', '#64748b');
    texto('preencha os campos e clique em "Calcular Distância".');
    origem.focus();
  }
  botao.addEventListener('click', calcular);
  document.getElementById('dist-limpar').addEventListener('click', limpar);
  [origem, destino].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite a cidade de **Origem** no primeiro campo (por exemplo, `São Paulo, SP`).
2. Digite a cidade de **Destino** no segundo campo (por exemplo, `Rio de Janeiro, RJ`).
3. Clique em **Calcular Distância** (ou pressione Enter) e aguarde alguns segundos.
4. Veja a **distância por estrada**, a **duração** estimada e a **distância em linha reta** entre as duas cidades.
5. Use o botão **Limpar** para apagar os campos e fazer uma nova consulta.

Para evitar confusão entre cidades com o mesmo nome, informe também o estado ou o país (por exemplo, `Santa Cruz, RN`). Se o nome não for encontrado, tente escrevê-lo de outra forma. Os dados de mapa e rota vêm do OpenStreetMap, por isso a ferramenta precisa de conexão com a internet.

## Entendendo os termos

- **Origem:** cidade ou local de onde a viagem começa.
- **Destino:** cidade ou local onde a viagem termina.
- **Distância por estrada:** extensão do trajeto percorrido de carro pelas vias existentes, em quilômetros (km). Costuma ser maior que a distância em linha reta.
- **Distância em linha reta:** menor distância entre os dois pontos no mapa, medida em linha reta sobre a superfície da Terra, sem seguir estradas.
- **Duração:** tempo estimado de viagem de carro, sem considerar trânsito, paradas, pedágios ou condições da pista.
- **Quilômetro (km):** unidade usada para medir a distância. 1 km equivale a 1.000 metros.
- **Rota:** caminho sugerido pelas estradas para ir da origem ao destino.