---
title: "Gerador de RG"
seoTitle: "Gerador de RG"
description: "Gerador de RG: gere números de RG válidos para testes. Grátis e online, sem cadastro."
summary: "Gere números de RG válidos para testes."
date: 2026-11-03
draft: false
category: "documentos"
tags: ["rg", "gerador", "dados de teste", "cpf", "documentos"]
keywords: ["gerador de rg", "gerador de rg online", "rg", "gerador", "dados de teste"]
---
<!--INI SUDAH DIKERJAKAN-->

Escolha se o RG deve sair com pontuação e depois clique em **Gerar RG**.

<div id="gerador-rg" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🪪 Gerador de RG</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere um RG válido (padrão SSP-SP) para testes de software.</p>
<label for="rg-pontuacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</label>
<select id="rg-pontuacao" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim">Sim</option>
<option value="nao">Não</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="rg-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar RG</button>
<button type="button" id="rg-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="rg-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rg-resultado">escolha a opção e clique em "Gerar RG".</span></div>
</div>
<script>
(function () {
  var pontuacao = document.getElementById('rg-pontuacao');
  var resultado = document.getElementById('rg-resultado');
  var caixa = document.getElementById('rg-resposta');
  var botaoCopiar = document.getElementById('rg-copiar');
  var ultimo = '';
  function gerarDigitos() {
    var d = [];
    for (var i = 0; i !== 8; i++) { d.push(Math.floor(Math.random() * 10)); }
    return d;
  }
  function calcularDV(d) {
    var soma = 0;
    d.forEach(function (n, i) { soma += n * (i + 2); });
    var dv = 11 - (soma % 11);
    if (dv === 10) { return 'X'; }
    if (dv === 11) { return '0'; }
    return String(dv);
  }
  function mostrarErro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar() {
    var d = gerarDigitos();
    var dv = calcularDV(d);
    var base = d.join('');
    if (pontuacao.value === 'sim') {
      ultimo = base.slice(0, 2) + '.' + base.slice(2, 5) + '.' + base.slice(5, 8) + '-' + dv;
    } else {
      ultimo = base + dv;
    }
    var numero = document.createElement('strong');
    numero.style.fontSize = '1.2rem';
    numero.textContent = ultimo;
    var nota = document.createElement('small');
    nota.style.color = '#475569';
    nota.textContent = 'RG gerado de forma aleatória, apenas para testes.';
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode('O RG gerado é '));
    resultado.appendChild(numero);
    resultado.appendChild(document.createElement('br'));
    resultado.appendChild(nota);
    botaoCopiar.textContent = 'Copiar';
  }
  function avisarCopiado() {
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiarAlternativo() {
    var campo = document.createElement('textarea');
    campo.value = ultimo;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); avisarCopiado(); } catch (e) { mostrarErro('não foi possível copiar. Selecione o número e copie manualmente.'); }
    document.body.removeChild(campo);
  }
  function copiar() {
    if (ultimo === '') { mostrarErro('gere um RG antes de copiar.'); return; }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(ultimo).then(avisarCopiado, copiarAlternativo);
    } else {
      copiarAlternativo();
    }
  }
  document.getElementById('rg-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  pontuacao.addEventListener('focus', function () { pontuacao.style.borderColor = '#6366f1'; });
  pontuacao.addEventListener('blur', function () { pontuacao.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. No campo **Gerar com pontuação?**, escolha **Sim** para receber o RG com pontos e hífen (por exemplo, `12.345.678-X`) ou **Não** para receber apenas os números e o dígito (por exemplo, `12345678X`).
2. Clique em **Gerar RG** para criar um novo número válido.
3. Clique em **Copiar** para levar o número para a área de transferência e colar no sistema que você está testando.
4. Para gerar outro número, basta clicar em **Gerar RG** novamente.

Os números são criados de forma aleatória, seguindo a regra de validação do RG emitido em São Paulo. Eles servem apenas para testes de software e não pertencem a pessoas reais.

## Entendendo os termos

- **RG (Registro Geral):** documento de identidade brasileiro, emitido pelos estados, que identifica a pessoa por um número.
- **Órgão emissor:** entidade responsável por emitir o documento. No caso deste gerador, a SSP-SP.
- **SSP-SP:** Secretaria da Segurança Pública do Estado de São Paulo, cuja regra de validação é usada para gerar os números.
- **Dígito verificador:** último caractere do RG, calculado a partir dos oito primeiros números. Serve para conferir se o número é válido e pode ser de 0 a 9 ou a letra **X**.
- **Pontuação:** pontos e hífen que separam os grupos do número, no formato `00.000.000-0`.
- **Número aleatório:** número sorteado pelo gerador, sem ligação com nenhuma pessoa real.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para validar formulários e sistemas durante o desenvolvimento.
- **Validação:** verificação feita pelo sistema para saber se o RG segue a regra de cálculo do dígito verificador.

## Como o dígito verificador é calculado

O cálculo usa os oito primeiros números do RG:

1. Multiplique cada número, da esquerda para a direita, pelos pesos de 2 a 9.
2. Some todos os resultados.
3. Divida a soma por 11 e pegue o resto.
4. Subtraia o resto de 11. Se o resultado for 10, o dígito é **X**. Se for 11, o dígito é **0**. Nos demais casos, o dígito é o próprio resultado.

## Aviso importante

O gerador foi criado para ajudar estudantes, programadores, analistas e testadores que precisam de RGs válidos para testar sistemas em desenvolvimento. O uso inadequado dos dados gerados é de total responsabilidade do usuário.