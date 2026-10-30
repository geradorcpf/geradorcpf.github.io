---
title: "Gerador de Inscrição Estadual de Alagoas (AL)"
seoTitle: "Gerador de Inscrição Estadual de Alagoas (AL)"
description: "Gerador de Inscrição Estadual de Alagoas (AL): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "alagoas", "documentos"]
keywords: ["gerador de inscrição estadual de alagoas (al)", "gerador de inscrição estadual de alagoas (al) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se deseja o número com pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-al" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de Alagoas (AL)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testar seu software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-al-pontuacao-sim" style="display:flex;align-items:center;gap:8px;padding:10px 16px;font-size:1rem;font-weight:600;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;"><input id="ie-al-pontuacao-sim" type="radio" name="ie-al-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;">Sim</label>
<label for="ie-al-pontuacao-nao" style="display:flex;align-items:center;gap:8px;padding:10px 16px;font-size:1rem;font-weight:600;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;"><input id="ie-al-pontuacao-nao" type="radio" name="ie-al-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-al-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-al-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ie-al-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ie-al-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-al-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var sim = document.getElementById('ie-al-pontuacao-sim');
  var nao = document.getElementById('ie-al-pontuacao-nao');
  var resultado = document.getElementById('ie-al-resultado');
  var caixa = document.getElementById('ie-al-resposta');
  var btnCopiar = document.getElementById('ie-al-copiar');
  var tipos = [0, 3, 5, 7, 8];
  var atual = '';
  var textoInicial = 'clique em "Gerar Inscrição Estadual".';
  function aleatorio(max) { return Math.floor(Math.random() * max); }
  function criar() {
    var d = [2, 4, tipos[aleatorio(tipos.length)]];
    for (var i = 0; i !== 5; i++) { d.push(aleatorio(10)); }
    var soma = 0;
    d.forEach(function (n, idx) { soma += n * (9 - idx); });
    var resto = (soma * 10) % 11;
    d.push(resto === 10 ? 0 : resto);
    return d.join('');
  }
  function formatar(s) {
    if (sim.checked) {
      return s.substr(0, 2) + '.' + s.substr(2, 1) + '.' + s.substr(3, 5) + '-' + s.substr(8, 1);
    }
    return s;
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
    atual = criar();
    btnCopiar.textContent = 'Copiar';
    mostrar();
  }
  function copiar() {
    if (atual === '') { return; }
    var texto = formatar(atual);
    function ok() {
      btnCopiar.textContent = 'Copiado!';
      setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
    }
    function alternativa() {
      var campo = document.createElement('textarea');
      campo.value = texto;
      campo.style.position = 'fixed';
      campo.style.opacity = '0';
      document.body.appendChild(campo);
      campo.select();
      try { document.execCommand('copy'); ok(); } catch (e) {}
      document.body.removeChild(campo);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(ok, alternativa);
    } else {
      alternativa();
    }
  }
  function limpar() {
    atual = '';
    sim.checked = true;
    btnCopiar.textContent = 'Copiar';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontWeight = '400';
    resultado.style.fontSize = '1rem';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = textoInicial;
  }
  function aoMudar() { if (atual !== '') { mostrar(); } }
  document.getElementById('ie-al-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('ie-al-limpar').addEventListener('click', limpar);
  sim.addEventListener('change', aoMudar);
  nao.addEventListener('change', aoMudar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com Pontuação?**, escolha **Sim** para receber o número formatado (por exemplo, `24.0.12345-6`) ou **Não** para receber apenas os dígitos (por exemplo, `240123456`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido de Alagoas.
3. Se quiser trocar o formato depois de gerar, basta alternar entre **Sim** e **Não**: o mesmo número é exibido com ou sem pontuação.
4. Clique em **Copiar** para levar o número para a área de transferência e colar no seu sistema ou formulário de teste.
5. Use **Limpar** para apagar o resultado e voltar às opções iniciais. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

Os números são gerados de forma aleatória, seguindo a regra de formação de Alagoas. Eles servem para testes de software e não correspondem a empresas reais. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do estado, usado para o controle do ICMS (imposto sobre circulação de mercadorias e serviços).
- **Alagoas (AL):** estado para o qual o número é gerado. Cada estado brasileiro tem seu próprio formato e sua própria regra de cálculo.
- **Pontuação:** pontos e traço usados para separar os blocos do número e facilitar a leitura. Sem pontuação, o número aparece apenas com os dígitos.
- **Dígito verificador:** último dígito do número, calculado a partir dos dígitos anteriores. Ele serve para conferir se a inscrição é válida.
- **Número válido:** número que respeita a regra de formação e de cálculo do estado, e por isso passa nos validadores, mesmo sem pertencer a uma empresa real.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar o funcionamento de sistemas sem usar dados reais.
- **Gerar:** criar um novo número aleatório a cada clique no botão.
- **Copiar:** enviar o número exibido para a área de transferência, pronto para ser colado em outro lugar.
- **Limpar:** apagar o resultado atual e restaurar as opções padrão do gerador.