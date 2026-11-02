---
title: "Gerador de Link para WhatsApp"
seoTitle: "Gerador de Link para WhatsApp"
description: "Gerador de Link para WhatsApp: crie um link para abrir conversa no WhatsApp com mensagem pronta. Grátis e online, sem cadastro."
summary: "Crie um link para abrir conversa no WhatsApp com mensagem pronta."
date: 2026-11-02
draft: false
category: "rede"
tags: ["whatsapp", "links", "mensagens"]
keywords: ["gerador de link para whatsapp", "gerador de link para whatsapp online", "whatsapp", "links", "mensagens"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta digitar o número e, se quiser, uma mensagem pronta. Depois clique em **Gerar Link** ou em **Iniciar Conversa**.

<div id="calc-whatsapp" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💬 Gerador de Link para WhatsApp</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o número e a mensagem e gere o link na hora.</p>
<label for="wa-ddi" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código do País (DDI)</label>
<input id="wa-ddi" type="text" inputmode="numeric" value="55" placeholder="Ex.: 55" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="wa-numero" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número (com DDD)</label>
<input id="wa-numero" type="text" inputmode="tel" placeholder="Ex.: (11) 91234-5678" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="wa-mensagem" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Mensagem (opcional)</label>
<textarea id="wa-mensagem" rows="4" placeholder="Ex.: Olá! Gostaria de mais informações." style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="wa-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Link</button>
<button type="button" id="wa-iniciar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Iniciar Conversa</button>
<button type="button" id="wa-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="wa-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-all;"><strong style="color:#3730a3;">Resposta:</strong> <span id="wa-resultado">preencha os campos e clique em "Gerar Link".</span></div>
</div>
<script>
(function () {
  var ddi = document.getElementById('wa-ddi');
  var numero = document.getElementById('wa-numero');
  var mensagem = document.getElementById('wa-mensagem');
  var resultado = document.getElementById('wa-resultado');
  var caixa = document.getElementById('wa-resposta');
  var textoInicial = 'preencha os campos e clique em "Gerar Link".';
  function apenasDigitos(v) {
    return String(v).replace(/\D/g, '');
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function montarLink() {
    var codigo = apenasDigitos(ddi.value).replace(/^0+/, '');
    var fone = apenasDigitos(numero.value).replace(/^0+/, '');
    if (codigo.length === 0 || codigo.length > 3) {
      erro('informe um código de país válido (de 1 a 3 dígitos).');
      return '';
    }
    if (!(fone.length > 5) || (codigo + fone).length > 15) {
      erro('número de telefone inválido.');
      return '';
    }
    var link = 'https://wa.me/' + codigo + fone;
    var texto = mensagem.value.trim();
    if (texto.length > 0) {
      link = link + '?text=' + encodeURIComponent(texto);
    }
    return link;
  }
  function copiar(texto, botao) {
    function ok() {
      botao.textContent = 'Copiado!';
      setTimeout(function () { botao.textContent = 'Copiar Link'; }, 1800);
    }
    function alternativo() {
      var area = document.createElement('textarea');
      area.value = texto;
      area.style.position = 'fixed';
      area.style.opacity = '0';
      document.body.appendChild(area);
      area.select();
      try { document.execCommand('copy'); ok(); } catch (e) { botao.textContent = 'Não foi possível copiar'; }
      document.body.removeChild(area);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(ok, alternativo);
    } else {
      alternativo();
    }
  }
  function gerar() {
    var link = montarLink();
    if (link === '') { return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var rotulo = document.createElement('span');
    rotulo.textContent = 'Seu link está pronto:';
    var quebra = document.createElement('br');
    var a = document.createElement('a');
    a.href = link;
    a.target = '_blank';
    a.rel = 'noopener noreferrer';
    a.textContent = link;
    a.style.color = '#4f46e5';
    a.style.fontWeight = '700';
    var quebra2 = document.createElement('br');
    var botao = document.createElement('button');
    botao.type = 'button';
    botao.textContent = 'Copiar Link';
    botao.style.cssText = 'margin-top:10px;padding:9px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
    botao.addEventListener('click', function () { copiar(link, botao); });
    resultado.appendChild(rotulo);
    resultado.appendChild(quebra);
    resultado.appendChild(a);
    resultado.appendChild(quebra2);
    resultado.appendChild(botao);
  }
  function iniciar() {
    var link = montarLink();
    if (link === '') { return; }
    gerar();
    window.open(link, '_blank', 'noopener,noreferrer');
  }
  function limpar() {
    ddi.value = '55';
    numero.value = '';
    mensagem.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
    numero.focus();
  }
  document.getElementById('wa-gerar').addEventListener('click', gerar);
  document.getElementById('wa-iniciar').addEventListener('click', iniciar);
  document.getElementById('wa-limpar').addEventListener('click', limpar);
  [ddi, numero].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  });
  [ddi, numero, mensagem].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o gerador

1. Confira o **Código do País (DDI)**. Por padrão ele vem preenchido com `55` (Brasil). Altere se o número for de outro país.
2. Digite o **Número** com DDD no segundo campo. Pode usar parênteses, espaços e hífen, como em `(11) 91234-5678`.
3. Se quiser, escreva uma **Mensagem** que já aparecerá preenchida na conversa.
4. Clique em **Gerar Link** para criar o endereço e use **Copiar Link** para copiá-lo.
5. Clique em **Iniciar Conversa** para abrir o WhatsApp direto na conversa, sem precisar salvar o contato.
6. Use o botão **Limpar** para apagar os campos e começar de novo.

O link gerado funciona no celular e no computador (WhatsApp Web ou aplicativo). Você pode colocá-lo em bio de redes sociais, site, e-mail ou cartão de visita digital.

## Entendendo os termos

- **WhatsApp:** aplicativo de mensagens que usa o número de telefone para identificar cada conta.
- **Link direto (wa.me):** endereço que abre uma conversa com um número específico no WhatsApp ao ser clicado.
- **DDI (código do país):** prefixo que identifica o país do telefone. No Brasil é `55`, em Portugal `351` e nos Estados Unidos `1`.
- **DDD:** código de área da cidade ou região, com dois dígitos no Brasil, como `11` para São Paulo.
- **Número:** telefone completo com DDD. No Brasil, celulares têm 9 dígitos após o DDD.
- **Mensagem pronta:** texto opcional que já aparece escrito na caixa de conversa, bastando enviar.
- **Codificação da URL:** conversão de espaços, acentos e símbolos da mensagem para um formato aceito em endereços de internet. O gerador faz isso automaticamente.
- **Iniciar conversa:** abre o link gerado em uma nova aba, levando você direto ao chat do número informado.

## Formato do link

O link segue este padrão:

`https://wa.me/` + DDI + DDD + número + `?text=` + mensagem codificada

## Exemplo resolvido

Você quer que clientes entrem em contato com o número (11) 91234-5678, do Brasil, já com a mensagem "Olá! Quero um orçamento."

1. DDI: `55`
2. Número com DDD: `11912345678`
3. Mensagem: `Olá! Quero um orçamento.` (codificada como `Ol%C3%A1!%20Quero%20um%20or%C3%A7amento.`)

**Resposta:** o link gerado é `https://wa.me/5511912345678?text=Ol%C3%A1!%20Quero%20um%20or%C3%A7amento.`