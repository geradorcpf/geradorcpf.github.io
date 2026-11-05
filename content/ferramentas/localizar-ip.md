---
title: "Localizar IP"
seoTitle: "Localizar IP"
description: "Localizar IP: descubra a localização aproximada de um endereço IP. Grátis e online, sem cadastro."
summary: "Descubra a localização aproximada de um endereço IP."
date: 2026-11-05
draft: false
category: "rede"
tags: ["ip", "geolocalização", "rede"]
keywords: ["localizar ip", "localizar ip online", "ip", "geolocalização", "rede"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta digitar um endereço IP abaixo e depois clicar em **Localizar IP**. Se deixar o campo vazio, a ferramenta mostra a localização do seu próprio IP.

<div id="calc-localizar-ip" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📍 Localizar IP</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe um endereço IP e veja a localização estimada.</p>
<label for="ip-endereco" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Endereço IP</label>
<input id="ip-endereco" type="text" inputmode="text" placeholder="Ex.: 8.8.8.8" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ip-localizar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Localizar IP</button>
<button type="button" id="ip-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ip-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;">
<div style="margin-bottom:10px;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ip-status">carregando a localização do seu IP...</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Endereço IP</span><span id="ip-r-ip" style="text-align:right;word-break:break-all;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Latitude</span><span id="ip-r-lat" style="text-align:right;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Longitude</span><span id="ip-r-lon" style="text-align:right;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Fuso Horário</span><span id="ip-r-tz" style="text-align:right;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Continente</span><span id="ip-r-cont" style="text-align:right;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">País</span><span id="ip-r-pais" style="text-align:right;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Estado</span><span id="ip-r-estado" style="text-align:right;">—</span></div>
<div style="display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-top:1px solid #e0e7ff;"><span style="font-weight:600;color:#475569;">Cidade</span><span id="ip-r-cidade" style="text-align:right;">—</span></div>
</div>
</div>
<script>
(function () {
  var campo = document.getElementById('ip-endereco');
  var status = document.getElementById('ip-status');
  var caixa = document.getElementById('ip-resposta');
  var ids = ['ip', 'lat', 'lon', 'tz', 'cont', 'pais', 'estado', 'cidade'];
  var continentes = {
    'Africa': 'África', 'Antarctica': 'Antártida', 'Asia': 'Ásia', 'Europe': 'Europa',
    'North America': 'América do Norte', 'South America': 'América do Sul', 'Oceania': 'Oceania',
    'AF': 'África', 'AN': 'Antártida', 'AS': 'Ásia', 'EU': 'Europa',
    'NA': 'América do Norte', 'SA': 'América do Sul', 'OC': 'Oceania'
  };
  var atual = 0;
  function el(id) { return document.getElementById('ip-r-' + id); }
  function zerarCampos() {
    ids.forEach(function (id) { el(id).textContent = '—'; });
  }
  function estado(cor, fundo, borda, msg) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    status.style.color = cor;
    status.textContent = msg;
  }
  function ipv4Valido(t) {
    var p = t.split('.');
    if (p.length !== 4) { return false; }
    return p.every(function (x) { return /^[0-9]{1,3}$/.test(x) && 255 >= Number(x); });
  }
  function ipv6Valido(t) {
    return t.indexOf(':') > -1 && /^[0-9a-fA-F:.]+$/.test(t) && t.length >= 2;
  }
  function pegar(url) {
    return fetch(url).then(function (r) { return r.json(); });
  }
  function viaIpwho(ip) {
    return pegar('https://ipwho.is/' + ip).then(function (d) {
      if (!d || d.success === false) { throw new Error('falha'); }
      return {
        ip: d.ip, lat: d.latitude, lon: d.longitude,
        tz: d.timezone ? d.timezone.id : '',
        cont: continentes[d.continent] || d.continent,
        pais: d.country, estado: d.region, cidade: d.city
      };
    });
  }
  function viaIpapi(ip) {
    return pegar('https://ipapi.co/' + (ip ? ip + '/' : '') + 'json/').then(function (d) {
      if (!d || d.error) { throw new Error('falha'); }
      return {
        ip: d.ip, lat: d.latitude, lon: d.longitude, tz: d.timezone,
        cont: continentes[d.continent_code] || d.continent_code,
        pais: d.country_name, estado: d.region, cidade: d.city
      };
    });
  }
  function mostrar(d) {
    ids.forEach(function (id) {
      var v = d[id];
      el(id).textContent = (v === undefined || v === null || v === '') ? '—' : String(v);
    });
    estado('#166534', '#f0fdf4', '#86efac', 'localização estimada encontrada.');
  }
  function localizar() {
    var ip = campo.value.trim();
    if (ip !== '' && !ipv4Valido(ip) && !ipv6Valido(ip)) {
      zerarCampos();
      estado('#b91c1c', '#fef2f2', '#fca5a5', 'informe um endereço IP válido (ex.: 8.8.8.8).');
      return;
    }
    atual += 1;
    var minha = atual;
    zerarCampos();
    estado('#64748b', '#ffffff', '#c7d2fe', 'buscando a localização...');
    viaIpwho(ip).catch(function () { return viaIpapi(ip); }).then(function (d) {
      if (minha !== atual) { return; }
      mostrar(d);
    }).catch(function () {
      if (minha !== atual) { return; }
      zerarCampos();
      estado('#b91c1c', '#fef2f2', '#fca5a5', 'não foi possível localizar esse IP. Verifique o endereço (IPs privados não são localizáveis) e tente novamente.');
    });
  }
  function limpar() {
    atual += 1;
    campo.value = '';
    zerarCampos();
    estado('#64748b', '#ffffff', '#c7d2fe', 'informe um IP e clique em "Localizar IP".');
    campo.focus();
  }
  document.getElementById('ip-localizar').addEventListener('click', localizar);
  document.getElementById('ip-limpar').addEventListener('click', limpar);
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { localizar(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  localizar();
})();
</script>

## Como usar a ferramenta

1. Digite o **endereço IP** que deseja consultar no campo acima (IPv4, como `8.8.8.8`, ou IPv6, como `2001:4860:4860::8888`).
2. Clique em **Localizar IP** (ou pressione Enter) para ver a localização estimada.
3. Se deixar o campo vazio, a ferramenta consulta o IP da sua própria conexão.
4. Use o botão **Limpar** para apagar o endereço e começar uma nova consulta.

Os dados são **estimados** e baseados em bancos de dados de geolocalização. Por isso, a cidade e as coordenadas podem apontar para o provedor de internet ou para uma região próxima, e não para o endereço exato do usuário. Endereços de rede privada (como `192.168.0.1`) não podem ser localizados.

## Entendendo os termos

- **Endereço IP:** número que identifica um dispositivo ou uma rede na internet, como se fosse o "endereço" usado para enviar e receber dados.
- **IPv4:** formato de IP com quatro números de 0 a 255 separados por pontos, como `192.0.2.1`.
- **IPv6:** formato mais novo de IP, com grupos de números e letras separados por dois-pontos, criado para oferecer muito mais endereços que o IPv4.
- **Geolocalização (GeoIP):** tecnologia que estima a localização geográfica de um IP consultando grandes bancos de dados atualizados com frequência.
- **Latitude:** posição norte-sul no globo, medida em graus a partir da linha do Equador.
- **Longitude:** posição leste-oeste no globo, medida em graus a partir do meridiano de Greenwich.
- **Fuso Horário:** região que adota o mesmo horário oficial, como `America/Sao_Paulo`.
- **Continente:** grande divisão de terra onde fica o país, como América do Sul ou Europa.
- **País:** nação onde o endereço IP está registrado ou sendo usado.
- **Estado:** divisão administrativa do país, como estado, província ou região.
- **Cidade:** município estimado para o IP, normalmente o da central do provedor de internet.