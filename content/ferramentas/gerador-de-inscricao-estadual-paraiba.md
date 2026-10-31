---
title: "Gerador de Inscrição Estadual da Paraíba (PB)"
seoTitle: "Gerador de Inscrição Estadual da Paraíba (PB)"
description: "Gerador de Inscrição Estadual da Paraíba (PB): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "paraíba", "documentos"]
keywords: ["gerador de inscrição estadual da paraíba (pb)", "gerador de inscrição estadual da paraíba (pb) online", "inscrição estadual", "estados", "empresas"]
compact: true
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher se quer a numeração com pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-pb" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual da Paraíba (PB)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testes de software.</p>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div role="radiogroup" aria-label="Gerar com pontuação?" style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;font-weight:600;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;">Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;font-weight:600;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
<p style="margin:14px 0 0;font-size:0.8rem;line-height:1.5;color:#64748b;">Os números são gerados de forma aleatória, seguindo a regra de cálculo do dígito verificador da Paraíba. Use apenas para testes de software.</p>
</div>
<script>
(function () {
  var radioSim = document.getElementById('ie-pont-sim');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoCopiar = document.getElementById('ie-copiar');
  var ultimo = '';
  function digitoVerificador(base) {
    var soma = 0;
    for (var i = 0; i !== 8; i++) {
      soma += base[i] * (9 - i);
    }
    var dv = 11 - (soma % 11);
    if (dv === 10 || dv === 11) { dv = 0; }
    return dv;
  }
  function aleatorio() {
    return Math.floor(Math.random() * 10);
  }
  function mostrarNumero(texto) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.style.letterSpacing = '1px';
    forte.textContent = texto;
    resultado.appendChild(forte);
  }
  function aviso(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar() {
    var base = [1, 6];
    for (var i = 0; i !== 6; i++) {
      base.push(aleatorio());
    }
    var dv = digitoVerificador(base);
    var corpo = base.join('');
    ultimo = radioSim.checked ? corpo + '-' + dv : corpo + String(dv);
    mostrarNumero(ultimo);
  }
  function copiarFallback() {
    var campo = document.createElement('textarea');
    campo.value = ultimo;
    campo.setAttribute('readonly', '');
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(campo);
    return ok;
  }
  function confirmarCopia(ok) {
    if (!ok) { aviso('não foi possível copiar. Selecione o número e copie manualmente.'); return; }
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiar() {
    if (ultimo === '') { aviso('gere uma inscrição estadual antes de copiar.'); return; }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(ultimo).then(
        function () { confirmarCopia(true); },
        function () { confirmarCopia(copiarFallback()); }
      );
    } else {
      confirmarCopia(copiarFallback());
    }
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para o número com hífen (por exemplo, `16000001-5`) ou **Não** para apenas dígitos (por exemplo, `160000015`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido para a Paraíba.
3. Clique em **Copiar** para levar o número para a área de transferência e colar no seu sistema ou formulário de teste.
4. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

Cada clique gera um número diferente. Os números servem apenas para testes: eles passam na validação do dígito verificador, mas não pertencem a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de uma empresa contribuinte do ICMS junto à Secretaria da Fazenda do seu estado.
- **Paraíba (PB):** estado cuja regra de formação da inscrição estadual é usada pelo gerador. Ela tem 9 dígitos: 8 dígitos-base e 1 dígito verificador.
- **Pontuação:** formatação do número com o hífen que separa o dígito verificador, como em `16000001-5`. Sem pontuação, aparecem só os 9 dígitos.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos 8 primeiros para confirmar que a inscrição é válida.
- **Número válido:** número que respeita a regra de cálculo do estado e, por isso, é aceito por validadores e sistemas que conferem o dígito verificador.
- **Dados de teste:** informações fictícias usadas por estudantes, programadores e testadores para experimentar softwares sem usar documentos reais.
- **Gerar:** criar um novo número aleatório que segue a regra da Paraíba.
- **Copiar:** enviar o número gerado para a área de transferência, pronto para colar em outro lugar.