---
title: "Gerador de Inscrição Estadual de São Paulo (SP)"
seoTitle: "Gerador de Inscrição Estadual de São Paulo (SP)"
description: "Gerador de Inscrição Estadual de São Paulo (SP): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "são paulo", "documentos"]
keywords: ["gerador de inscrição estadual de são paulo (sp)", "gerador de inscrição estadual de são paulo (sp) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se quer a pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-sp" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de São Paulo (SP)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testar seus sistemas.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="sp-pont-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="sp-pont-sim" name="sp-pontuacao" value="sim" checked style="accent-color:#4f46e5;width:18px;height:18px;margin:0;cursor:pointer;"> Sim</label>
<label for="sp-pont-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="sp-pont-nao" name="sp-pontuacao" value="nao" style="accent-color:#4f46e5;width:18px;height:18px;margin:0;cursor:pointer;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sp-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="sp-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="sp-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sp-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radioSim = document.getElementById('sp-pont-sim');
  var radioNao = document.getElementById('sp-pont-nao');
  var resultado = document.getElementById('sp-resultado');
  var caixa = document.getElementById('sp-resposta');
  var botaoCopiar = document.getElementById('sp-copiar');
  var atual = '';
  function aleatorio(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }
  function digito(lista, pesos) {
    var soma = 0;
    for (var i = 0; i !== pesos.length; i++) {
      soma += lista[i] * pesos[i];
    }
    return (soma % 11) % 10;
  }
  function gerarNumero(comPontuacao) {
    var d = [aleatorio(1, 9)];
    var i;
    for (i = 1; i !== 8; i++) {
      d.push(aleatorio(0, 9));
    }
    d.push(digito(d, [1, 3, 4, 5, 6, 7, 8, 10]));
    for (i = 0; i !== 2; i++) {
      d.push(aleatorio(0, 9));
    }
    d.push(digito(d, [3, 2, 10, 9, 8, 7, 6, 5, 4, 3, 2]));
    var s = d.join('');
    if (comPontuacao) {
      return s.substring(0, 3) + '.' + s.substring(3, 6) + '.' + s.substring(6, 9) + '.' + s.substring(9, 12);
    }
    return s;
  }
  function mostrar(texto) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = texto;
  }
  function gerar() {
    atual = gerarNumero(radioSim.checked);
    mostrar(atual);
  }
  function copiarFallback() {
    var area = document.createElement('textarea');
    area.value = atual;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(area);
  }
  function copiar() {
    if (atual === '') { return; }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).catch(copiarFallback);
    } else {
      copiarFallback();
    }
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function trocarFormato() {
    if (atual !== '') { gerar(); }
  }
  document.getElementById('sp-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  radioSim.addEventListener('change', trocarFormato);
  radioNao.addEventListener('change', trocarFormato);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para o número com pontos (por exemplo, `110.042.490.114`) ou **Não** para apenas os dígitos (`110042490114`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido.
3. Se quiser trocar o formato, basta alterar a opção de pontuação: o número é gerado novamente.
4. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
5. Clique em **Gerar Inscrição Estadual** quantas vezes precisar para obter outros números.

Os números são gerados de forma aleatória e respeitam a regra de cálculo dos dígitos verificadores de São Paulo. Eles servem apenas para testes de software e **não** são inscrições de empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de uma empresa contribuinte do ICMS no cadastro da Secretaria da Fazenda do estado.
- **São Paulo (SP):** estado cujas regras de formação do número são usadas neste gerador. Cada estado brasileiro tem o seu próprio formato.
- **Pontuação:** pontos que separam o número em grupos de três dígitos (`000.000.000.000`). Sem pontuação, o número aparece só com os 12 dígitos.
- **Dígito verificador:** dígito calculado a partir dos demais números, usado para conferir se a inscrição é válida. A IE de São Paulo tem dois: o 9º e o 12º dígitos.
- **Número válido:** número que passa na conferência dos dígitos verificadores, mesmo sem existir de fato no cadastro da Fazenda.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar sistemas em desenvolvimento.
- **Copiar:** botão que copia o número gerado para a área de transferência do seu dispositivo.