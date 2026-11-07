---
title: "Qual é o meu IP"
seoTitle: "Qual é o meu IP"
description: "Qual é o meu IP: veja seu endereço de IP público na hora. Grátis e online, sem cadastro."
summary: "Veja seu endereço de IP público na hora."
date: 2026-11-07
draft: false
category: "rede"
tags: ["ip", "endereço ip", "rede"]
keywords: ["qual é o meu ip", "qual é o meu ip online", "ip", "endereço ip", "rede"]
---

Veja abaixo o seu endereço de IP público e o DNS reverso correspondente. A consulta é feita automaticamente ao abrir a página; se quiser atualizar, clique em **Descobrir Meu IP**.

<div id="ferramenta-meu-ip" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌐 Qual é o meu IP</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Descubra seu endereço de IP público na hora.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="mip-atualizar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Descobrir Meu IP</button>
<button type="button" id="mip-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar IP</button>
</div>
<div id="mip-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.8;word-break:break-all;">
<div><strong style="color:#3730a3;">Resposta:</strong> <span id="mip-ip" style="color:#64748b;">consultando...</span></div>
<div><strong style="color:#3730a3;">Tipo:</strong> <span id="mip-tipo" style="color:#64748b;">-</span></div>
<div><strong style="color:#3730a3;">DNS Reverso:</strong> <span id="mip-dns" style="color:#64748b;">-</span></div>
</div>
</div>
<script>
(function () {
  var elIp = document.getElementById('mip-ip');
  var elTipo = document.getElementById('mip-tipo');
  var elDns = document.getElementById('mip-dns');
  var caixa = document.getElementById('mip-resposta');
  var btnAtualizar = document.getElementById('mip-atualizar');
  var btnCopiar = document.getElementById('mip-copiar');
  var atual = '';
  var token = 0;
  function cores(borda, fundo, texto) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    elIp.style.color = texto;
    elTipo.style.color = texto;
    elDns.style.color = texto;
  }
  function neutro() { cores('#c7d2fe', '#ffffff', '#64748b'); }
  function sucesso() { cores('#86efac', '#f0fdf4', '#166534'); }
  function falha() { cores('#fca5a5', '#fef2f2', '#b91c1c'); }
  function lerTexto(url) {
    var ctl = (typeof AbortController !== 'undefined') ? new AbortController() : null;
    var timer = setTimeout(function () { if (ctl) { ctl.abort(); } }, 8000);
    return fetch(url, ctl ? { signal: ctl.signal } : {}).then(function (r) {
      clearTimeout(timer);
      return r.text();
    }, function (e) {
      clearTimeout(timer);
      throw e;
    });
  }
  function lerJson(texto) {
    try { return JSON.parse(texto); } catch (e) { return null; }
  }
  function extrairIp(texto) {
    var d = lerJson(texto);
    if (d && d.ip) { return String(d.ip).trim(); }
    throw new Error('resposta invalida');
  }
  function buscarIp() {
    return lerTexto('https://api64.ipify.org?format=json').then(extrairIp).catch(function () {
      return lerTexto('https://api.ipify.org?format=json').then(extrairIp);
    });
  }
  function tipoIp(ip) {
    if (ip.indexOf(':') !== -1) { return 'IPv6'; }
    if (/^(\d{1,3}\.){3}\d{1,3}$/.test(ip)) { return 'IPv4'; }
    return '';
  }
  function nomePtr(ip) {
    if (tipoIp(ip) === 'IPv4') {
      return ip.split('.').reverse().join('.') + '.in-addr.arpa';
    }
    var limpo = ip.split('%')[0];
    var p = limpo.split('::');
    var inicio = p[0] ? p[0].split(':') : [];
    var fim = (p.length === 2 && p[1]) ? p[1].split(':') : [];
    var faltam = Math.max(8 - inicio.length - fim.length, 0);
    var meio = (p.length === 2) ? new Array(faltam + 1).join('0').split('') : [];
    var todos = inicio.concat(meio, fim).map(function (h) { return ('0000' + h).slice(-4); });
    return todos.join('').split('').reverse().join('.') + '.ip6.arpa';
  }
  function buscarDns(ip) {
    var url = 'https://dns.google/resolve?type=PTR&name=' + encodeURIComponent(nomePtr(ip));
    return lerTexto(url).then(function (texto) {
      var d = lerJson(texto);
      if (!d || !d.Answer) { return ''; }
      return d.Answer.filter(function (a) { return a.type === 12; }).map(function (a) {
        return String(a.data).replace(/\.$/, '');
      }).join(', ');
    }).catch(function () { return null; });
  }
  function consultar() {
    token += 1;
    var meu = token;
    atual = '';
    neutro();
    elIp.textContent = 'consultando...';
    elTipo.textContent = '-';
    elDns.textContent = '-';
    btnAtualizar.disabled = true;
    buscarIp().then(function (ip) {
      if (meu !== token) { return; }
      atual = ip;
      elIp.textContent = ip;
      elTipo.textContent = tipoIp(ip) || 'Desconhecido';
      elDns.textContent = 'consultando...';
      sucesso();
      return buscarDns(ip).then(function (nome) {
        if (meu !== token) { return; }
        if (nome === null) { elDns.textContent = 'consulta indisponível no momento'; }
        else if (nome === '') { elDns.textContent = 'nenhum registro encontrado'; }
        else { elDns.textContent = nome; }
      });
    }).catch(function () {
      if (meu !== token) { return; }
      elIp.textContent = 'não foi possível obter o seu IP. Verifique a conexão ou desative bloqueadores e tente de novo.';
      elTipo.textContent = '-';
      elDns.textContent = '-';
      falha();
    }).then(function () {
      if (meu === token) { btnAtualizar.disabled = false; }
    });
  }
  function feedbackCopiado() {
    var original = 'Copiar IP';
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = original; }, 1500);
  }
  function copiarFallback(texto) {
    var campo = document.createElement('textarea');
    campo.value = texto;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); feedbackCopiado(); } catch (e) {}
    document.body.removeChild(campo);
  }
  function copiar() {
    if (!atual) { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(feedbackCopiado, function () { copiarFallback(atual); });
    } else {
      copiarFallback(atual);
    }
  }
  btnAtualizar.addEventListener('click', consultar);
  btnCopiar.addEventListener('click', copiar);
  consultar();
})();
</script>

## Como usar a ferramenta

1. Abra a página: o seu **endereço de IP público** aparece automaticamente no campo de resposta.
2. Confira o **Tipo** (IPv4 ou IPv6) e o **DNS Reverso**, que mostra o nome de domínio associado ao IP, quando existir.
3. Clique em **Descobrir Meu IP** para fazer uma nova consulta, por exemplo depois de trocar de rede ou ligar uma VPN.
4. Clique em **Copiar IP** para copiar o endereço e colar onde precisar.

Se você usa VPN, proxy ou uma rede compartilhada (como Wi-Fi de empresa ou de escola), o IP exibido será o dessa conexão, e não o do seu provedor de internet. Dependendo do provedor, o DNS Reverso pode não ter nenhum registro, e isso é normal.

## Entendendo os termos

- **IP (Internet Protocol):** protocolo e endereço único que identifica um dispositivo ou rede na internet, permitindo que eles se comuniquem.
- **Endereço de IP:** sequência de números (e, às vezes, letras) que funciona como o "endereço" do seu dispositivo ou da sua conexão.
- **IPv4:** formato mais comum, com quatro números de 0 a 255 separados por pontos, como `192.168.0.1`.
- **IPv6:** formato mais novo e mais longo, com números e letras separados por dois-pontos, como `2001:0db8:85a3:0000:0000:8a2e:0370:7334`. Foi criado porque os endereços IPv4 estão se esgotando.
- **IP público:** endereço visto pelos sites e serviços na internet. É atribuído pelo seu provedor e costuma ser compartilhado por todos os aparelhos da mesma rede.
- **IP privado (local):** endereço usado dentro da sua rede doméstica ou da empresa, como `192.168.x.x`. Ele não aparece na internet e não é o resultado desta ferramenta.
- **Provedor de internet (ISP):** empresa que fornece a sua conexão e atribui o IP público.
- **Roteador:** aparelho que distribui a internet (Wi-Fi) para os dispositivos da casa ou do escritório.
- **VPN:** serviço que encaminha sua conexão por outro servidor e, com isso, muda o IP público que os sites enxergam.
- **DNS (Domain Name System):** sistema que converte nomes de sites, como `exemplo.com`, em endereços de IP.
- **DNS Reverso:** o caminho inverso do DNS: a partir de um endereço de IP, descobre o nome de domínio associado a ele.
- **Registro PTR:** tipo de registro de DNS que guarda a ligação entre um IP e o seu nome de domínio, usado na consulta de DNS reverso.