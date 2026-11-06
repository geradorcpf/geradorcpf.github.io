---
title: "Notepad Online"
seoTitle: "Notepad Online"
description: "Notepad Online: bloco de notas no navegador, com salvamento automático. Grátis e online, sem cadastro."
summary: "Bloco de notas no navegador, com salvamento automático."
date: 2026-11-06
draft: false
category: "util"
tags: ["bloco de notas", "produtividade", "texto"]
keywords: ["notepad online", "bloco de notas", "produtividade", "texto"]
---

Basta digitar suas anotações no campo abaixo. O texto é salvo automaticamente enquanto você escreve.

<div id="notepad-online" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📝 Notepad Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escreva suas notas. Tudo fica salvo no seu navegador.</p>
<label for="np-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Sua anotação</label>
<textarea id="np-texto" placeholder="Digite ou cole seu texto aqui..." spellcheck="true" style="width:100%;min-height:240px;padding:12px 14px;margin-bottom:16px;font-size:1rem;line-height:1.5;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="np-copiar" style="flex:1;min-width:120px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar</button>
<button type="button" id="np-baixar" style="flex:1;min-width:120px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Baixar .txt</button>
<button type="button" id="np-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="np-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resumo:</strong> <span id="np-resultado">0 caracteres, 0 palavras, 0 linhas.</span><br><small id="np-status" style="color:#475569;">Nenhum texto salvo ainda.</small></div>
</div>
<script>
(function () {
  var CHAVE = 'notepad-online-texto';
  var texto = document.getElementById('np-texto');
  var resultado = document.getElementById('np-resultado');
  var status = document.getElementById('np-status');
  var caixa = document.getElementById('np-resposta');
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function guardar(valor) {
    try { window.localStorage.setItem(CHAVE, valor); return true; } catch (e) { return false; }
  }
  function ler() {
    try { return window.localStorage.getItem(CHAVE) || ''; } catch (e) { return ''; }
  }
  function mostrarStatus(msg, cor) {
    status.style.color = cor || '#475569';
    status.textContent = msg;
  }
  function atualizar() {
    var v = texto.value;
    var chars = v.length;
    var limpo = v.trim();
    var palavras = limpo === '' ? 0 : limpo.split(/\s+/).length;
    var linhas = v === '' ? 0 : v.split('\n').length;
    resultado.style.color = '#166534';
    resultado.textContent = fmt(chars) + ' caracteres, ' + fmt(palavras) + ' palavras, ' + fmt(linhas) + ' linhas.';
    if (chars === 0) {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    } else {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
    }
  }
  function aoDigitar() {
    atualizar();
    if (guardar(texto.value)) {
      mostrarStatus('Salvo automaticamente neste navegador.', '#166534');
    } else {
      mostrarStatus('Não foi possível salvar automaticamente neste navegador.', '#b91c1c');
    }
  }
  function copiar() {
    if (texto.value === '') { mostrarStatus('Não há texto para copiar.', '#b91c1c'); return; }
    function alternativa() {
      texto.select();
      var ok = false;
      try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
      mostrarStatus(ok ? 'Texto copiado!' : 'Não foi possível copiar. Selecione e copie manualmente.', ok ? '#166534' : '#b91c1c');
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto.value).then(function () {
        mostrarStatus('Texto copiado!', '#166534');
      }, alternativa);
    } else {
      alternativa();
    }
  }
  function baixar() {
    if (texto.value === '') { mostrarStatus('Não há texto para baixar.', '#b91c1c'); return; }
    var blob = new Blob([texto.value], { type: 'text/plain;charset=utf-8' });
    var url = URL.createObjectURL(blob);
    var a = document.createElement('a');
    a.href = url;
    a.download = 'notepad.txt';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    setTimeout(function () { URL.revokeObjectURL(url); }, 1000);
    mostrarStatus('Arquivo notepad.txt baixado.', '#166534');
  }
  function limpar() {
    if (texto.value !== '' && !window.confirm('Apagar todo o texto? Essa ação não pode ser desfeita.')) { return; }
    texto.value = '';
    guardar('');
    atualizar();
    mostrarStatus('Texto apagado.', '#475569');
    texto.focus();
  }
  texto.value = ler();
  atualizar();
  if (texto.value !== '') { mostrarStatus('Texto anterior restaurado deste navegador.', '#166534'); }
  texto.addEventListener('input', aoDigitar);
  texto.addEventListener('focus', function () { texto.style.borderColor = '#6366f1'; });
  texto.addEventListener('blur', function () { texto.style.borderColor = '#c7d2fe'; });
  document.getElementById('np-copiar').addEventListener('click', copiar);
  document.getElementById('np-baixar').addEventListener('click', baixar);
  document.getElementById('np-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o Notepad Online

1. Clique no campo **Sua anotação** e digite ou cole o texto que desejar.
2. O texto é salvo automaticamente no seu navegador a cada alteração. Ao voltar à página, ele será restaurado.
3. Acompanhe o **Resumo** logo abaixo para ver a quantidade de caracteres, palavras e linhas.
4. Clique em **Copiar** para enviar o texto para a área de transferência.
5. Clique em **Baixar .txt** para guardar uma cópia como arquivo de texto no seu dispositivo.
6. Use o botão **Limpar** para apagar tudo e começar uma nova anotação.

O salvamento é feito apenas neste navegador e neste dispositivo. Se você limpar os dados do navegador ou usar outro aparelho, o texto não estará disponível. Para não perder uma nota importante, baixe uma cópia em .txt.

## Entendendo os termos

- **Notepad (bloco de notas):** programa simples para escrever e guardar textos rápidos, sem formatação.
- **Online:** que funciona direto no navegador, sem instalar nada.
- **Salvamento automático:** recurso que guarda o texto sozinho a cada alteração, sem precisar clicar em salvar.
- **Navegador:** programa usado para acessar sites, como Chrome, Firefox, Edge ou Safari.
- **Armazenamento local:** espaço do próprio navegador onde o texto fica guardado no seu dispositivo.
- **Caractere:** cada letra, número, símbolo ou espaço digitado no texto.
- **Palavra:** sequência de caracteres separada por espaços ou quebras de linha.
- **Linha:** trecho do texto que termina quando você pressiona Enter.
- **Área de transferência:** memória temporária do dispositivo usada ao copiar e colar textos.
- **Arquivo .txt:** formato de arquivo de texto puro, que abre em qualquer dispositivo.