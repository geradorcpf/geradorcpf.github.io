---
title: "Meu Sistema Operacional"
seoTitle: "Meu Sistema Operacional"
description: "Meu Sistema Operacional: veja qual sistema operacional seu dispositivo está usando. Grátis e online, sem cadastro."
summary: "Veja qual sistema operacional seu dispositivo está usando."
date: 2026-11-05
draft: false
category: "rede"
tags: ["sistema operacional", "diagnóstico", "rede"]
keywords: ["meu sistema operacional", "meu sistema operacional online", "sistema operacional", "diagnóstico", "rede"]
---

Basta abrir esta página: o sistema operacional do seu dispositivo é detectado automaticamente. Se quiser, clique em **Detectar Novamente** para atualizar o resultado.

<div id="calc-sistema-operacional" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💻 Meu Sistema Operacional</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Veja qual sistema operacional seu dispositivo está usando.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="so-detectar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Detectar Novamente</button>
<button type="button" id="so-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="so-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Sistema Operacional:</strong> <span id="so-resultado">detectando...</span><div id="so-detalhes" style="margin-top:8px;"></div></div>
</div>
<script>
(function () {
var caixa = document.getElementById('so-resposta');
var resultado = document.getElementById('so-resultado');
var detalhes = document.getElementById('so-detalhes');
var botaoCopiar = document.getElementById('so-copiar');
var textoCopia = '';
function windowsPorNt(nt) {
var mapa = { '10.0': 'Windows 10', '6.3': 'Windows 8.1', '6.2': 'Windows 8', '6.1': 'Windows 7', '6.0': 'Windows Vista', '5.2': 'Windows XP', '5.1': 'Windows XP' };
return mapa[nt] || ('Windows (NT ' + nt + ')');
}
function identificar(ua, plataforma, toques) {
var m;
if (/Windows Phone/i.test(ua)) { return { nome: 'Windows Phone', versao: '' }; }
if (/Windows NT/i.test(ua)) {
m = ua.match(/Windows NT ([0-9.]+)/i);
return { nome: windowsPorNt(m ? m[1] : ''), versao: m ? 'NT ' + m[1] : '' };
}
if (/Android/i.test(ua)) {
m = ua.match(/Android ([0-9.]+)/i);
return { nome: 'Android', versao: m ? m[1] : '' };
}
if (/iPhone|iPod/i.test(ua)) {
m = ua.match(/OS ([0-9_]+)/i);
return { nome: 'iOS', versao: m ? m[1].replace(/_/g, '.') : '' };
}
if (/iPad/i.test(ua)) {
m = ua.match(/OS ([0-9_]+)/i);
return { nome: 'iPadOS', versao: m ? m[1].replace(/_/g, '.') : '' };
}
if (/Macintosh|Mac OS X/i.test(ua)) {
if (/Mac/i.test(plataforma) && toques > 1) { return { nome: 'iPadOS', versao: '' }; }
return { nome: 'macOS', versao: '' };
}
if (/CrOS/i.test(ua)) { return { nome: 'Chrome OS', versao: '' }; }
if (/Ubuntu/i.test(ua)) { return { nome: 'Linux (Ubuntu)', versao: '' }; }
if (/Fedora/i.test(ua)) { return { nome: 'Linux (Fedora)', versao: '' }; }
if (/Debian/i.test(ua)) { return { nome: 'Linux (Debian)', versao: '' }; }
if (/Linux|X11/i.test(ua)) { return { nome: 'Linux', versao: '' }; }
if (/FreeBSD/i.test(ua)) { return { nome: 'FreeBSD', versao: '' }; }
if (/OpenBSD/i.test(ua)) { return { nome: 'OpenBSD', versao: '' }; }
return { nome: 'Não identificado', versao: '' };
}
function arquiteturaPorUa(ua) {
if (/aarch64|arm64|ARM/i.test(ua)) { return 'ARM'; }
if (/WOW64|Win64|x64|x86_64|amd64/i.test(ua)) { return '64 bits (x64)'; }
if (/i[3-6]86|x86/i.test(ua)) { return '32 bits (x86)'; }
return 'Não informada pelo navegador';
}
function linha(rotulo, valor) {
var d = document.createElement('div');
d.style.cssText = 'margin-top:6px;font-size:0.9rem;color:#475569;word-break:break-word;';
var s = document.createElement('strong');
s.textContent = rotulo + ': ';
var t = document.createElement('span');
t.textContent = valor;
d.appendChild(s);
d.appendChild(t);
detalhes.appendChild(d);
}
function mostrar(info, plataforma, arquitetura, ua) {
caixa.style.borderColor = '#86efac';
caixa.style.background = '#f0fdf4';
resultado.style.color = '#166534';
resultado.style.fontWeight = '700';
resultado.style.fontSize = '1.2rem';
resultado.textContent = info.nome;
detalhes.textContent = '';
if (info.versao) { linha('Versão', info.versao); }
linha('Plataforma', plataforma || 'Não informada pelo navegador');
linha('Arquitetura', arquitetura);
linha('User Agent', ua);
textoCopia = 'Sistema Operacional: ' + info.nome + (info.versao ? ' (' + info.versao + ')' : '') + ' | Plataforma: ' + (plataforma || 'Não informada') + ' | Arquitetura: ' + arquitetura;
}
function detectar() {
var nav = window.navigator || {};
var ua = String(nav.userAgent || '');
var dados = nav.userAgentData;
var plataforma = (dados && dados.platform) ? dados.platform : String(nav.platform || '');
var toques = Number(nav.maxTouchPoints || 0);
var info = identificar(ua, plataforma, toques);
var arq = arquiteturaPorUa(ua);
mostrar(info, plataforma, arq, ua);
if (dados && typeof dados.getHighEntropyValues === 'function') {
dados.getHighEntropyValues(['platformVersion', 'architecture', 'bitness']).then(function (v) {
var info2 = { nome: info.nome, versao: info.versao };
var principal = parseInt(String(v.platformVersion || '').split('.')[0], 10);
if (info.nome.indexOf('Windows') === 0 && !isNaN(principal)) {
info2.nome = principal >= 13 ? 'Windows 11' : 'Windows 10';
info2.versao = v.platformVersion;
} else if (v.platformVersion && info.nome !== 'Não identificado') {
info2.versao = v.platformVersion;
}
var arq2 = arq;
if (v.architecture) {
if (v.architecture === 'arm') { arq2 = v.bitness ? 'ARM ' + v.bitness + ' bits' : 'ARM'; }
else if (v.architecture === 'x86') { arq2 = v.bitness === '64' ? '64 bits (x64)' : '32 bits (x86)'; }
else { arq2 = v.architecture; }
}
mostrar(info2, plataforma, arq2, ua);
}).catch(function () {});
}
}
function copiar() {
var original = botaoCopiar.textContent;
function aviso(t) {
botaoCopiar.textContent = t;
setTimeout(function () { botaoCopiar.textContent = original; }, 1500);
}
try {
navigator.clipboard.writeText(textoCopia).then(function () { aviso('Copiado!'); }).catch(function () { aviso('Falhou'); });
} catch (e) {
aviso('Falhou');
}
}
document.getElementById('so-detectar').addEventListener('click', detectar);
botaoCopiar.addEventListener('click', copiar);
detectar();
})();
</script>

## Como usar a ferramenta

1. Abra esta página no dispositivo que você quer verificar (computador, celular ou tablet).
2. Veja o campo **Sistema Operacional**: o resultado aparece sozinho, sem precisar digitar nada.
3. Confira os detalhes logo abaixo, como versão, plataforma, arquitetura e User Agent.
4. Clique em **Detectar Novamente** para atualizar o resultado, caso tenha mudado o modo do navegador (por exemplo, "versão para computador" no celular).
5. Use o botão **Copiar** para copiar o resultado e enviar para o suporte técnico ou colar em um chamado.

A detecção é feita direto no seu navegador. Nenhuma informação é enviada para servidores e não há cadastro.

## Entendendo os termos

- **Sistema operacional:** programa principal que controla o dispositivo e permite rodar os outros aplicativos. Exemplos: Windows, macOS, Linux, Android e iOS.
- **Windows:** sistema operacional da Microsoft, muito usado em computadores e notebooks.
- **macOS:** sistema operacional da Apple para computadores Mac.
- **Linux:** sistema operacional de código aberto, com várias distribuições como Ubuntu, Debian e Fedora.
- **Android:** sistema operacional do Google para celulares e tablets.
- **iOS / iPadOS:** sistemas operacionais da Apple para iPhone e iPad.
- **Versão:** número que indica a edição do sistema operacional, útil para saber se ele está atualizado.
- **Plataforma:** nome da família do sistema informado pelo navegador, como Windows, Android ou Linux.
- **Arquitetura:** tipo de processador que o sistema usa, como x86 (32 bits), x64 (64 bits) ou ARM.
- **User Agent:** texto que o navegador envia aos sites para se identificar, com dados do navegador e do sistema operacional.
- **Navegador:** programa usado para acessar sites, como Chrome, Firefox, Edge e Safari.