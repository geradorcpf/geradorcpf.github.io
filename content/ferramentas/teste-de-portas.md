---
title: "Teste de Portas"
seoTitle: "Teste de Portas"
description: "Teste de Portas: verifique se uma porta está aberta em um endereço. Grátis e online, sem cadastro."
summary: "Verifique se uma porta está aberta em um endereço."
date: 2026-11-11
draft: false
category: "rede"
tags: ["portas", "segurança", "diagnóstico", "rede"]
keywords: ["teste de portas", "teste de portas online", "portas", "segurança", "diagnóstico"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta digitar o IP ou domínio e a porta abaixo e depois clicar em **Verificar**.

<div id="teste-portas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔌 Teste de Portas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o endereço e a porta TCP e veja se ela está aberta.</p>
<label for="prt-host" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">IP ou domínio</label>
<input id="prt-host" type="text" placeholder="Ex.: exemplo.com.br ou 203.0.113.10" autocomplete="off" autocapitalize="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="prt-porta" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Porta</label>
<input id="prt-porta" type="text" inputmode="numeric" placeholder="Ex.: 443" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Portas comuns</div>
<div id="prt-comuns" style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="prt-verificar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Verificar</button>
<button type="button" id="prt-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="prt-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="prt-resultado">preencha os campos e clique em "Verificar".</span></div>
</div>
<script>
(function () {
  var API_URL = '';
  var host = document.getElementById('prt-host');
  var porta = document.getElementById('prt-porta');
  var btn = document.getElementById('prt-verificar');
  var btnLimpar = document.getElementById('prt-limpar');
  var caixa = document.getElementById('prt-resposta');
  var resultado = document.getElementById('prt-resultado');
  var lista = document.getElementById('prt-comuns');
  var textoInicial = 'preencha os campos e clique em "Verificar".';
  var ocupado = false;
  var comuns = [['21', 'FTP'], ['22', 'SSH'], ['23', 'Telnet'], ['25', 'SMTP'], ['53', 'DNS'], ['80', 'HTTP'], ['110', 'POP3'], ['143', 'IMAP'], ['443', 'HTTPS'], ['587', 'SMTP'], ['3306', 'MySQL'], ['3389', 'RDP']];
  var estilos = {
    neutro: ['#c7d2fe', '#ffffff', '#64748b'],
    ok: ['#86efac', '#f0fdf4', '#166534'],
    erro: ['#fca5a5', '#fef2f2', '#b91c1c']
  };
  function estado(tipo) {
    var e = estilos[tipo];
    caixa.style.borderColor = e[0];
    caixa.style.background = e[1];
    resultado.style.color = e[2];
  }
  function mostrar(tipo, titulo, detalhe) {
    estado(tipo);
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = titulo;
    resultado.appendChild(forte);
    if (detalhe) {
      resultado.appendChild(document.createElement('br'));
      var pequeno = document.createElement('small');
      pequeno.style.color = '#475569';
      pequeno.textContent = detalhe;
      resultado.appendChild(pequeno);
    }
  }
  function erro(msg) {
    estado('erro');
    resultado.textContent = msg;
  }
  function limparHost(v) {
    var t = String(v).trim().replace(/^[a-zA-Z][a-zA-Z0-9+.-]*:\/\//, '');
    t = t.split('/')[0].split('?')[0].split('#')[0];
    if (t.indexOf('@') > -1) { t = t.split('@').pop(); }
    if (t.split(':').length === 2) { t = t.split(':')[0]; }
    return t.toLowerCase();
  }
  function hostValido(h) {
    if (h === '' || h.length > 253) { return false; }
    if (h.indexOf(':') > -1) { return /^[0-9a-f:.]+$/.test(h); }
    return /^[a-z0-9]([a-z0-9.-]*[a-z0-9])?$/.test(h);
  }
  function verificar() {
    if (ocupado) { return; }
    var h = limparHost(host.value);
    var p = String(porta.value).trim();
    if (!hostValido(h)) { erro('informe um IP ou domínio válido.'); return; }
    if (!/^[0-9]+$/.test(p)) { erro('informe uma porta válida, entre 1 e 65535.'); return; }
    var n = Number(p);
    if (!(n >= 1) || n > 65535) { erro('informe uma porta válida, entre 1 e 65535.'); return; }
    if (API_URL === '') {
      mostrar('erro', 'Serviço de verificação não configurado.', 'Defina a variável API_URL no script da ferramenta.');
      return;
    }
    ocupado = true;
    btn.disabled = true;
    btn.textContent = 'Verificando...';
    mostrar('neutro', 'Verificando...', h + ':' + n);
    var controle = new AbortController();
    var timer = setTimeout(function () { controle.abort(); }, 15000);
    fetch(API_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ host: h, port: n }),
      signal: controle.signal
    }).then(function (r) {
      if (!r.ok) { throw new Error('http'); }
      return r.json();
    }).then(function (d) {
      if (d.open === true) {
        mostrar('ok', 'A porta ' + n + ' está aberta', h + ':' + n + ' aceita conexões TCP.');
      } else {
        mostrar('erro', 'A porta ' + n + ' está fechada', h + ':' + n + ' não respondeu à conexão TCP.');
      }
    }).catch(function () {
      erro('não foi possível fazer a verificação agora. Tente novamente em instantes.');
    }).then(function () {
      clearTimeout(timer);
      ocupado = false;
      btn.disabled = false;
      btn.textContent = 'Verificar';
    });
  }
  function limpar() {
    host.value = '';
    porta.value = '';
    estado('neutro');
    resultado.textContent = textoInicial;
    host.focus();
  }
  comuns.forEach(function (item) {
    var b = document.createElement('button');
    b.type = 'button';
    b.textContent = item[0] + ' ' + item[1];
    b.style.cssText = 'padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:1px solid #c7d2fe;border-radius:999px;cursor:pointer;';
    b.addEventListener('click', function () {
      porta.value = item[0];
      porta.focus();
    });
    lista.appendChild(b);
  });
  btn.addEventListener('click', verificar);
  btnLimpar.addEventListener('click', limpar);
  [host, porta].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { verificar(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite o **IP ou domínio** que você quer testar no primeiro campo (por exemplo, `exemplo.com.br` ou `203.0.113.10`).
2. Digite o número da **porta** no segundo campo ou clique em uma das **portas comuns** para preenchê-la automaticamente.
3. Clique em **Verificar** (ou pressione Enter) para ver se a porta está aberta ou fechada.
4. Use o botão **Limpar** para apagar os valores e fazer um novo teste.

Se você colar um endereço completo, como `https://exemplo.com.br/pagina`, a ferramenta usa só o domínio. A porta deve ser um número entre 1 e 65535. O teste verifica portas TCP, as usadas pela maioria dos serviços.

## Entendendo os termos

- **Porta:** número que identifica o serviço que recebe conexões em um computador ou servidor, como a 80 para sites (HTTP) e a 22 para SSH.
- **Porta aberta:** porta em que há um programa esperando conexões e nada no caminho bloqueia o acesso.
- **Porta fechada:** porta que não aceita conexões, porque nenhum programa a usa ou porque um firewall ou o roteador a bloqueia.
- **IP:** endereço numérico que identifica um dispositivo na internet ou em uma rede, como `203.0.113.10`.
- **Domínio:** nome fácil de lembrar que aponta para um IP, como `exemplo.com.br`.
- **TCP:** protocolo de comunicação que estabelece uma conexão confiável entre dois dispositivos. É o usado neste teste.
- **UDP:** protocolo mais simples, sem conexão fixa, que não pode ser testado por este método.
- **Firewall:** programa ou equipamento que controla quais conexões podem entrar e sair, e pode bloquear portas.
- **Roteador:** equipamento que conecta a rede local à internet e pode redirecionar portas para um computador específico.
- **Redirecionamento de portas (port forwarding):** configuração do roteador que encaminha uma porta para um computador da rede local.
- **CGNAT:** técnica em que a operadora divide um mesmo IP público entre vários clientes, o que impede abrir portas.
- **HTTP e HTTPS (80 e 443):** portas usadas por sites, sendo a 443 a versão segura.
- **SSH (22):** porta usada para acesso remoto seguro a servidores.
- **SMTP, POP3 e IMAP (25/587, 110 e 143):** portas usadas para envio e recebimento de e-mails.
- **DNS (53):** porta usada para converter nomes de domínio em endereços IP.
- **FTP (21):** porta usada para transferência de arquivos.
- **Telnet (23):** porta de acesso remoto sem criptografia, pouco recomendada hoje.
- **MySQL (3306):** porta padrão do banco de dados MySQL.
- **RDP (3389):** porta do acesso remoto à área de trabalho do Windows.