---
title: "DNS Lookup"
seoTitle: "DNS Lookup"
description: "DNS Lookup: consulte registros DNS (A, MX, TXT e outros) de um domínio. Grátis e online, sem cadastro."
summary: "Consulte registros DNS (A, MX, TXT e outros) de um domínio."
date: 2026-10-27
draft: false
category: "rede"
tags: ["dns", "domínios", "diagnóstico", "rede"]
keywords: ["dns lookup", "dns lookup online", "dns", "domínios", "diagnóstico"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta digitar o domínio abaixo, escolher o tipo de registro e clicar em **Consultar DNS**.

<div id="calc-dns" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌐 DNS Lookup</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe um domínio e veja os registros DNS na hora.</p>
<label for="dns-dominio" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Domínio</label>
<input id="dns-dominio" type="text" inputmode="url" placeholder="Ex.: exemplo.com.br" autocomplete="off" autocapitalize="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="dns-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo de registro</label>
<select id="dns-tipo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="ALL">Todos os tipos</option>
<option value="A">A - Endereço IPv4</option>
<option value="AAAA">AAAA - Endereço IPv6</option>
<option value="MX">MX - Servidor de Email</option>
<option value="NS">NS - Servidor de Nomes</option>
<option value="TXT">TXT - Registro de Texto</option>
<option value="CNAME">CNAME - Nome Canônico</option>
<option value="SOA">SOA - Autoridade da Zona</option>
<option value="CAA">CAA - Autorização de Certificado</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="dns-consultar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Consultar DNS</button>
<button type="button" id="dns-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="dns-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;box-sizing:border-box;"><strong style="color:#3730a3;">Resposta:</strong> <span id="dns-resultado">preencha o domínio e clique em "Consultar DNS".</span></div>
</div>
<script>
(function () {
  var dominio = document.getElementById('dns-dominio');
  var tipo = document.getElementById('dns-tipo');
  var botao = document.getElementById('dns-consultar');
  var caixa = document.getElementById('dns-resposta');
  var resultado = document.getElementById('dns-resultado');
  var MSG_INICIAL = 'preencha o domínio e clique em "Consultar DNS".';
  var TIPOS = [
    { n: 'A', c: 1, d: 'Endereço IPv4' },
    { n: 'AAAA', c: 28, d: 'Endereço IPv6' },
    { n: 'MX', c: 15, d: 'Servidor de Email' },
    { n: 'NS', c: 2, d: 'Servidor de Nomes' },
    { n: 'TXT', c: 16, d: 'Registro de Texto' },
    { n: 'CNAME', c: 5, d: 'Nome Canônico' },
    { n: 'SOA', c: 6, d: 'Autoridade da Zona' },
    { n: 'CAA', c: 257, d: 'Autorização de Certificado' }
  ];
  function esvaziar(el) {
    while (el.firstChild) { el.removeChild(el.firstChild); }
  }
  function estilo(borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
  }
  function mensagem(texto, borda, fundo, cor) {
    estilo(borda, fundo, cor);
    esvaziar(resultado);
    resultado.textContent = texto;
  }
  function erro(texto) { mensagem(texto, '#fca5a5', '#fef2f2', '#b91c1c'); }
  function limparDominio(v) {
    var t = String(v).trim().toLowerCase();
    t = t.replace(/^[a-z]+:\/\//, '');
    t = t.replace(/[\/?#].*$/, '');
    t = t.replace(/:\d+$/, '');
    t = t.replace(/\.+$/, '');
    if (t === '') { return ''; }
    try { t = new URL('http://' + t).hostname; } catch (e) { return ''; }
    if (t.indexOf('.') === -1) { return ''; }
    if (!/^[a-z0-9_.-]+$/.test(t)) { return ''; }
    return t;
  }
  function consultar(nome, codigo) {
    var parametros = '?' + new URLSearchParams({ name: nome, type: String(codigo) }).toString();
    return fetch('https://dns.google/resolve' + parametros)
      .then(function (r) { return r.json(); })
      .catch(function () {
        return fetch('https://cloudflare-dns.com/dns-query' + parametros, { headers: { 'Accept': 'application/dns-json' } })
          .then(function (r) { return r.json(); });
      });
  }
  function criar(tag, css, texto) {
    var el = document.createElement(tag);
    if (css) { el.style.cssText = css; }
    if (texto) { el.textContent = texto; }
    return el;
  }
  function nx(r) { return r ? r.Status === 3 : false; }
  function mostrar(nome, respostas) {
    var vistos = {};
    var grupos = {};
    var total = 0;
    respostas.forEach(function (r) {
      if (r) {
        (r.Answer || []).forEach(function (a) {
          var chave = a.type + '#' + a.name + '#' + a.data;
          if (!vistos[chave]) {
            vistos[chave] = true;
            if (!grupos[a.type]) { grupos[a.type] = []; }
            grupos[a.type].push(a);
          }
        });
      }
    });
    estilo('#86efac', '#f0fdf4', '#166534');
    esvaziar(resultado);
    resultado.style.display = 'block';
    var titulo = criar('div', 'margin-bottom:12px;');
    titulo.appendChild(document.createTextNode('Resultados para '));
    titulo.appendChild(criar('strong', 'font-size:1.1rem;word-break:break-all;', nome));
    resultado.appendChild(titulo);
    TIPOS.forEach(function (t) {
      var lista = grupos[t.c];
      if (!lista) { return; }
      total += lista.length;
      var cab = criar('div', 'margin:14px 0 6px;font-weight:700;color:#3730a3;');
      cab.textContent = t.n + ' - ' + t.d + ' (' + lista.length + ')';
      resultado.appendChild(cab);
      lista.forEach(function (a) {
        var linha = criar('div', 'padding:10px 12px;margin-bottom:6px;background:#ffffff;border:1px solid #c7d2fe;border-radius:8px;color:#1e293b;');
        linha.appendChild(criar('div', 'font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:0.9rem;word-break:break-all;', a.data));
        linha.appendChild(criar('div', 'margin-top:4px;font-size:0.8rem;color:#64748b;word-break:break-all;', a.name + ' · TTL ' + a.TTL + 's'));
        resultado.appendChild(linha);
      });
    });
    if (total === 0) {
      mensagem('nenhum registro encontrado para ' + nome + ' neste tipo de consulta.', '#fca5a5', '#fef2f2', '#b91c1c');
    }
  }
  function executar() {
    var nome = limparDominio(dominio.value);
    if (nome === '') { erro('informe um domínio válido, como exemplo.com.br.'); return; }
    var escolhido = tipo.value;
    var lista = TIPOS.filter(function (t) { return escolhido === 'ALL' ? true : t.n === escolhido; });
    mensagem('consultando registros DNS...', '#c7d2fe', '#ffffff', '#64748b');
    botao.disabled = true;
    botao.style.opacity = '0.6';
    Promise.all(lista.map(function (t) {
      return consultar(nome, t.c).catch(function () { return null; });
    })).then(function (respostas) {
      botao.disabled = false;
      botao.style.opacity = '1';
      var falhas = respostas.filter(function (r) { return r === null; }).length;
      if (falhas === respostas.length) {
        erro('não foi possível consultar o DNS agora. Verifique sua conexão e tente novamente.');
        return;
      }
      if (respostas.some(nx)) {
        erro('o domínio ' + nome + ' não existe (NXDOMAIN).');
        return;
      }
      mostrar(nome, respostas);
    });
  }
  function limpar() {
    dominio.value = '';
    tipo.value = 'ALL';
    estilo('#c7d2fe', '#ffffff', '#64748b');
    esvaziar(resultado);
    resultado.textContent = MSG_INICIAL;
    dominio.focus();
  }
  botao.addEventListener('click', executar);
  document.getElementById('dns-limpar').addEventListener('click', limpar);
  dominio.addEventListener('keydown', function (e) { if (e.key === 'Enter') { executar(); } });
  [dominio, tipo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite o **domínio** que você quer consultar no primeiro campo, por exemplo `exemplo.com.br`. Também funciona com subdomínios, como `mail.exemplo.com.br`.
2. Escolha o **tipo de registro** na lista. Deixe em **Todos os tipos** para ver tudo de uma vez.
3. Clique em **Consultar DNS** (ou pressione Enter) para ver os registros encontrados.
4. Use o botão **Limpar** para apagar os campos e fazer uma nova consulta.

Você pode colar o endereço completo (como `https://www.exemplo.com.br/pagina`): a ferramenta usa apenas o domínio. Os resultados vêm de servidores DNS públicos e podem estar em cache, então uma alteração recente pode demorar um pouco para aparecer.

## Entendendo os termos

- **DNS (Domain Name System):** sistema que funciona como uma agenda telefônica da internet, traduzindo nomes de domínio em endereços IP.
- **Domínio:** nome que identifica um site ou serviço na internet, como `exemplo.com.br`.
- **Subdomínio:** parte adicional antes do domínio principal, como `blog` em `blog.exemplo.com.br`.
- **Registro DNS:** informação cadastrada na zona de um domínio, que diz para onde ele aponta ou como seus serviços funcionam.
- **Registro A:** aponta o domínio para um endereço IPv4 (por exemplo, `192.0.2.1`).
- **Registro AAAA:** aponta o domínio para um endereço IPv6, o formato mais novo de endereço IP.
- **Registro MX:** indica quais servidores recebem os emails do domínio e a prioridade de cada um (menor número, maior prioridade).
- **Registro NS:** informa os servidores de nomes autoritativos, responsáveis por responder sobre o domínio.
- **Registro TXT:** guarda texto livre, muito usado para verificar a posse do domínio e configurar SPF, DKIM e DMARC.
- **Registro CNAME:** cria um apelido, fazendo um nome apontar para outro nome em vez de um IP.
- **Registro SOA:** reúne dados da zona, como o servidor primário, o email do responsável e o número de série.
- **Registro CAA:** define quais autoridades certificadoras podem emitir certificados SSL/TLS para o domínio.
- **SPF, DKIM e DMARC:** configurações publicadas em registros TXT que ajudam a comprovar que um email é legítimo.
- **TTL (Time To Live):** tempo, em segundos, que um registro pode ficar guardado em cache antes de ser consultado de novo.
- **Propagação de DNS:** tempo que uma alteração leva para ser vista em todos os servidores, de acordo com o TTL.
- **NXDOMAIN:** resposta que indica que o domínio consultado não existe.