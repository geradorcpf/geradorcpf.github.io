---
title: "Gerador de PIS/PASEP"
seoTitle: "Gerador de PIS/PASEP"
description: "Gerador de PIS/PASEP: gere números de PIS/PASEP válidos para testes. Grátis e online, sem cadastro."
summary: "Gere números de PIS/PASEP válidos para testes."
date: 2026-11-02
draft: false
category: "documentos"
tags: ["pis/pasep", "trabalho", "gerador", "dados de teste", "cpf", "documentos"]
keywords: ["gerador de pis/pasep", "gerador de pis/pasep online", "pis/pasep", "trabalho", "gerador"]
---

Basta escolher se quer a pontuação e depois clicar em **Gerar PIS**.

<div id="gerador-pis" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔢 Gerador de PIS/PASEP</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere um número válido para testes na hora.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="pis-pont-sim" style="display:flex;align-items:center;gap:8px;padding:10px 16px;font-size:1rem;font-weight:600;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;"><input id="pis-pont-sim" type="radio" name="pis-pontuacao" value="sim" checked style="margin:0;accent-color:#4f46e5;">Sim</label>
<label for="pis-pont-nao" style="display:flex;align-items:center;gap:8px;padding:10px 16px;font-size:1rem;font-weight:600;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;"><input id="pis-pont-nao" type="radio" name="pis-pontuacao" value="nao" style="margin:0;accent-color:#4f46e5;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="pis-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar PIS</button>
<button type="button" id="pis-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="pis-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="pis-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">PIS/PASEP gerado:</strong> <span id="pis-resultado">clique em "Gerar PIS" para criar um número.</span><div id="pis-status" style="margin-top:6px;font-size:0.85rem;color:#475569;"></div></div>
</div>
<script>
(function () {
  var radSim = document.getElementById('pis-pont-sim');
  var radNao = document.getElementById('pis-pont-nao');
  var resultado = document.getElementById('pis-resultado');
  var caixa = document.getElementById('pis-resposta');
  var status = document.getElementById('pis-status');
  var textoInicial = 'clique em "Gerar PIS" para criar um número.';
  var pesos = [3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
  var atual = '';
  function aleatorio(n) {
    var v;
    var c = window.crypto;
    if (c) {
      if (c.getRandomValues) {
        var arr = new Uint32Array(1);
        c.getRandomValues(arr);
        v = arr[0];
      }
    }
    if (v === undefined) { v = Math.floor(Math.random() * 4294967296); }
    return v % n;
  }
  function gerarNumero() {
    var digitos = [];
    var soma = 0;
    pesos.forEach(function (peso) {
      var d = aleatorio(10);
      digitos.push(d);
      soma += d * peso;
    });
    var dv = 11 - (soma % 11);
    if (dv === 10 || dv === 11) { dv = 0; }
    digitos.push(dv);
    return digitos.join('');
  }
  function formatar(n) {
    if (radSim.checked) {
      return n.slice(0, 3) + '.' + n.slice(3, 8) + '.' + n.slice(8, 10) + '-' + n.slice(10);
    }
    return n;
  }
  function mensagem(msg) { status.textContent = msg; }
  function mostrar() {
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.4rem';
    forte.style.letterSpacing = '1px';
    forte.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    forte.textContent = formatar(atual);
    resultado.textContent = '';
    resultado.appendChild(forte);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
  }
  function gerar() {
    atual = gerarNumero();
    mensagem('');
    mostrar();
  }
  function copiarAntigo(texto) {
    var area = document.createElement('textarea');
    area.value = texto;
    area.setAttribute('readonly', '');
    area.style.position = 'fixed';
    area.style.top = '0';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(area);
    mensagem(ok ? 'Número copiado!' : 'Não foi possível copiar. Selecione o número e copie manualmente.');
  }
  function copiar() {
    if (atual === '') { mensagem('Gere um número antes de copiar.'); return; }
    var texto = formatar(atual);
    if (navigator.clipboard) {
      navigator.clipboard.writeText(texto).then(
        function () { mensagem('Número copiado!'); },
        function () { copiarAntigo(texto); }
      );
    } else {
      copiarAntigo(texto);
    }
  }
  function limpar() {
    atual = '';
    radSim.checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
    mensagem('');
  }
  function trocarOpcao() {
    if (atual !== '') { mostrar(); }
  }
  document.getElementById('pis-gerar').addEventListener('click', gerar);
  document.getElementById('pis-copiar').addEventListener('click', copiar);
  document.getElementById('pis-limpar').addEventListener('click', limpar);
  radSim.addEventListener('change', trocarOpcao);
  radNao.addEventListener('change', trocarOpcao);
})();
</script>

## Como usar o gerador

1. Escolha **Sim** ou **Não** em "Gerar com pontuação?" para definir se o número terá pontos e hífen (`123.45678.90-1`) ou apenas dígitos (`12345678901`).
2. Clique em **Gerar PIS** (ou em **Gerar PIS** novamente) para criar um novo número válido.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Se trocar a opção de pontuação depois de gerar, o mesmo número é exibido no novo formato, sem precisar gerar outro.
5. Use o botão **Limpar** para apagar o resultado e voltar ao estado inicial.

Os números são gerados de forma aleatória no seu navegador, respeitando a regra de cálculo do dígito verificador. Use-os apenas para testes de software, demonstrações e estudos.

## Entendendo os termos

- **PIS (Programa de Integração Social):** programa que cadastra o trabalhador de empresa privada e dá acesso a benefícios como o abono salarial e o seguro-desemprego.
- **PASEP (Programa de Formação do Patrimônio do Servidor Público):** programa equivalente ao PIS, voltado aos servidores públicos.
- **PIS/PASEP:** número de 11 dígitos que identifica o trabalhador em um desses programas. Na prática, ele segue o mesmo formato nos dois casos.
- **NIS (Número de Identificação Social):** número de identificação do cidadão nos programas sociais. O PIS/PASEP é um dos tipos de NIS.
- **Dígito verificador:** o último dígito do número, calculado a partir dos 10 primeiros. Ele serve para detectar erros de digitação e de validação.
- **Pontuação:** a máscara com pontos e hífen aplicada ao número, no formato `000.00000.00-0`.
- **Número válido:** número que passa na conta do dígito verificador. Ele pode ser aceito por um sistema, mas isso não significa que pertença a uma pessoa real.
- **Dados de teste:** informações fictícias usadas por programadores e testadores para verificar o funcionamento de formulários, cadastros e sistemas.