---
title: "Remover ou Trocar Quebra de Linha"
seoTitle: "Remover ou Trocar Quebra de Linha"
description: "Remover ou Trocar Quebra de Linha: remova ou troque quebras de linha de um texto. Grátis e online, sem cadastro."
summary: "Remova ou troque quebras de linha de um texto."
date: 2026-11-08
draft: false
category: "texto"
tags: ["quebra de linha", "formatação", "texto"]
keywords: ["remover ou trocar quebra de linha", "remover ou trocar quebra de linha online", "quebra de linha", "formatação", "texto"]
---

Basta digitar ou colar o texto abaixo, escolher pelo que as quebras de linha serão trocadas e depois clicar em **Remover Quebra**.

<div id="ferramenta-quebra-linha" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">↩️ Remover ou Trocar Quebra de Linha</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole o texto, escolha a substituição e veja o resultado na hora.</p>
<label for="qbl-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o texto</label>
<textarea id="qbl-texto" rows="6" placeholder="Cole aqui o texto com quebras de linha" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Substituir por</div>
<div style="display:flex;flex-direction:column;gap:8px;margin-bottom:20px;padding:12px 14px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;">
<label style="display:flex;align-items:center;gap:8px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="qbl-modo" value="nada" checked style="accent-color:#4f46e5;"> Nada (remover)</label>
<label style="display:flex;align-items:center;gap:8px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="qbl-modo" value="br" style="accent-color:#4f46e5;"> Tag &lt;br /&gt;</label>
<label style="display:flex;align-items:center;gap:8px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="qbl-modo" value="espaco" style="accent-color:#4f46e5;"> Espaço (" ")</label>
<label style="display:flex;align-items:center;gap:8px;font-size:0.95rem;cursor:pointer;flex-wrap:wrap;"><input type="radio" name="qbl-modo" value="custom" id="qbl-radio-custom" style="accent-color:#4f46e5;"> Este caractere: <input id="qbl-custom" type="text" placeholder="Ex.: ," autocomplete="off" style="width:110px;padding:6px 10px;font-size:0.95rem;border:2px solid #c7d2fe;border-radius:8px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="qbl-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Remover Quebra</button>
<button type="button" id="qbl-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="qbl-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="qbl-resultado">cole o texto e clique em "Remover Quebra".</span>
<textarea id="qbl-saida" rows="6" readonly style="display:none;width:100%;margin-top:12px;padding:12px 14px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #86efac;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="qbl-copiar" style="display:none;margin-top:10px;padding:10px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar resultado</button>
</div>
</div>
<script>
(function () {
  var entrada = document.getElementById('qbl-texto');
  var custom = document.getElementById('qbl-custom');
  var radioCustom = document.getElementById('qbl-radio-custom');
  var radios = document.getElementsByName('qbl-modo');
  var saida = document.getElementById('qbl-saida');
  var botaoCopiar = document.getElementById('qbl-copiar');
  var resultado = document.getElementById('qbl-resultado');
  var caixa = document.getElementById('qbl-resposta');
  var TAG_BR = String.fromCharCode(60) + 'br /' + String.fromCharCode(62);
  var REGEX_QUEBRA = /\r\n|\r|\n/g;
  function modo() {
    for (var i = 0; i !== radios.length; i++) {
      if (radios[i].checked) { return radios[i].value; }
    }
    return 'nada';
  }
  function substituto() {
    var m = modo();
    if (m === 'br') { return TAG_BR; }
    if (m === 'espaco') { return ' '; }
    if (m === 'custom') { return custom.value; }
    return '';
  }
  function esconderSaida() {
    saida.style.display = 'none';
    botaoCopiar.style.display = 'none';
    saida.value = '';
  }
  function erro(msg) {
    esconderSaida();
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function converter() {
    var texto = entrada.value;
    if (texto.trim() === '') { erro('digite ou cole um texto para continuar.'); return; }
    var total = texto.split(REGEX_QUEBRA).length - 1;
    var troca = substituto();
    saida.value = texto.replace(REGEX_QUEBRA, function () { return troca; });
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    if (total === 0) {
      resultado.textContent = 'nenhuma quebra de linha foi encontrada no texto.';
    } else if (total === 1) {
      resultado.textContent = '1 quebra de linha foi tratada.';
    } else {
      resultado.textContent = total + ' quebras de linha foram tratadas.';
    }
    saida.style.display = 'block';
    botaoCopiar.style.display = 'inline-block';
    botaoCopiar.textContent = 'Copiar resultado';
  }
  function copiar() {
    function feito() { botaoCopiar.textContent = 'Copiado!'; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(saida.value).then(feito, function () {
        saida.select();
        document.execCommand('copy');
        feito();
      });
    } else {
      saida.select();
      document.execCommand('copy');
      feito();
    }
  }
  function limpar() {
    entrada.value = '';
    custom.value = '';
    radios[0].checked = true;
    esconderSaida();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'cole o texto e clique em "Remover Quebra".';
    entrada.focus();
  }
  document.getElementById('qbl-calcular').addEventListener('click', converter);
  document.getElementById('qbl-limpar').addEventListener('click', limpar);
  botaoCopiar.addEventListener('click', copiar);
  custom.addEventListener('focus', function () { radioCustom.checked = true; });
  [entrada, custom].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  custom.addEventListener('keydown', function (e) { if (e.key === 'Enter') { converter(); } });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o texto no campo **Digite o texto**.
2. Em **Substituir por**, escolha o que vai ocupar o lugar de cada quebra de linha: nada, a tag `<br />`, um espaço ou um caractere que você mesmo define.
3. Se escolher **Este caractere**, digite o símbolo ou texto desejado (por exemplo, uma vírgula) no campo ao lado.
4. Clique em **Remover Quebra** para ver o texto já convertido na caixa de resposta.
5. Clique em **Copiar resultado** para levar o texto pronto para a área de transferência.
6. Use o botão **Limpar** para apagar tudo e começar de novo.

O texto digitado não é enviado a nenhum servidor: toda a conversão acontece no seu próprio navegador.

## Entendendo os termos

- **Quebra de linha:** ponto do texto em que uma linha termina e a próxima começa, como ao apertar a tecla Enter.
- **\n (nova linha):** caractere invisível, também chamado de LF (Line Feed), usado em sistemas como Linux e macOS para marcar a quebra de linha.
- **\r\n (retorno de carro + nova linha):** combinação, também chamada de CRLF, usada pelo Windows. A ferramenta trata as duas formas do mesmo jeito.
- **Nada (remover):** apaga as quebras de linha e junta as linhas, sem deixar espaço entre elas.
- **Tag `<br />`:** código HTML que cria uma quebra de linha em páginas da web. Útil para levar um texto com várias linhas para dentro de um HTML.
- **Espaço:** troca cada quebra de linha por um espaço em branco, o que evita que as palavras do fim e do começo das linhas fiquem coladas.
- **Este caractere:** permite escolher qualquer símbolo ou texto para ficar no lugar das quebras, como vírgula, ponto e vírgula ou barra.
- **Texto convertido:** resultado final, com as quebras de linha já substituídas conforme a opção escolhida.