---
title: "Gerador de Inscrição Estadual de Goiás (GO)"
seoTitle: "Gerador de Inscrição Estadual de Goiás (GO)"
description: "Gerador de Inscrição Estadual de Goiás (GO): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "goiás", "documentos"]
keywords: ["gerador de inscrição estadual de goiás (go)", "gerador de inscrição estadual de goiás (go) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-go" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de Goiás (GO)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a opção e gere um número válido na hora.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input id="ie-pont-sim" type="radio" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;">Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input id="ie-pont-nao" type="radio" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radSim = document.getElementById('ie-pont-sim');
  var radNao = document.getElementById('ie-pont-nao');
  var btnGerar = document.getElementById('ie-gerar');
  var btnCopiar = document.getElementById('ie-copiar');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var atual = '';
  function aleatorio(n) { return Math.floor(Math.random() * n); }
  function dentroDoIntervalo(n, min, max) { return Math.min(Math.max(n, min), max) === n; }
  function calcularDigito(base) {
    var soma = 0;
    for (var i = 0; i !== 8; i++) { soma += Number(base.charAt(i)) * (9 - i); }
    var resto = soma % 11;
    if (resto === 0) { return 0; }
    if (resto === 1) { return dentroDoIntervalo(Number(base), 10103105, 10119997) ? 1 : 0; }
    return 11 - resto;
  }
  function gerarNumero() {
    var prefixos = ['10', '11', '15'];
    var base = prefixos[aleatorio(3)];
    for (var i = 0; i !== 6; i++) { base += String(aleatorio(10)); }
    return base + String(calcularDigito(base));
  }
  function formatar(numero) {
    if (radSim.checked) {
      return numero.substr(0, 2) + '.' + numero.substr(2, 3) + '.' + numero.substr(5, 3) + '-' + numero.substr(8, 1);
    }
    return numero;
  }
  function mostrar() {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '0.04em';
    resultado.textContent = formatar(atual);
  }
  function gerar() {
    atual = gerarNumero();
    mostrar();
  }
  function avisoCopiado() {
    var original = 'Copiar';
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = original; }, 1500);
  }
  function copiarAlternativo(texto) {
    var campo = document.createElement('textarea');
    campo.value = texto;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); avisoCopiado(); } catch (e) { }
    document.body.removeChild(campo);
  }
  function copiar() {
    if (atual === '') { gerar(); }
    var texto = formatar(atual);
    var area = navigator.clipboard;
    if (area) {
      area.writeText(texto).then(avisoCopiado, function () { copiarAlternativo(texto); });
    } else {
      copiarAlternativo(texto);
    }
  }
  btnGerar.addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  radSim.addEventListener('change', function () { if (atual !== '') { mostrar(); } });
  radNao.addEventListener('change', function () { if (atual !== '') { mostrar(); } });
})();
</script>

**IMPORTANTE:** esta ferramenta tem como intenção ajudar estudantes, programadores, analistas e testadores a gerar Inscrições Estaduais válidas, normalmente necessárias para testar softwares em desenvolvimento. Os números são gerados de forma aleatória, respeitando as regras de criação do documento no estado de Goiás. A má utilização dos dados gerados é de total responsabilidade do usuário.

## Como usar a ferramenta

1. Em **Gerar com Pontuação?**, escolha **Sim** para o número com pontos e hífen (por exemplo, `10.987.654-7`) ou **Não** para apenas os dígitos (por exemplo, `109876547`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido para Goiás.
3. O número aparece na caixa **Resposta**. Se mudar a opção de pontuação depois de gerar, o formato é atualizado automaticamente.
4. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema de testes.
5. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de uma empresa contribuinte do ICMS junto à Secretaria da Fazenda do seu estado.
- **Goiás (GO):** estado para o qual o número é gerado. Cada estado brasileiro tem seu próprio formato e regra de cálculo.
- **Pontuação:** pontos e hífen usados para separar os dígitos. Em Goiás, o formato é `XX.XXX.XXX-X`.
- **Sem pontuação:** o mesmo número escrito apenas com os 9 dígitos, sem separadores.
- **Dígito verificador:** último dígito do número, calculado a partir dos 8 primeiros. Ele serve para conferir se a inscrição é válida.
- **Prefixo:** os dois primeiros dígitos da inscrição. Em Goiás, os prefixos utilizados são 10, 11 e 15.
- **Número válido para teste:** número que passa na verificação matemática do dígito verificador, mas que não pertence a nenhuma empresa real.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, tributo estadual que exige a inscrição estadual do contribuinte.
- **Copiar:** botão que envia o número exibido para a área de transferência do seu dispositivo.