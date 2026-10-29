---
title: "Gerador de CNPJ"
seoTitle: "Gerador de CNPJ"
description: "Gerador de CNPJ: gere CNPJs válidos, com ou sem pontuação, para testes. Grátis e online, sem cadastro."
summary: "Gere CNPJs válidos, com ou sem pontuação, para testes."
date: 2026-10-29
draft: false
category: "documentos"
tags: ["cnpj", "empresas", "gerador", "dados de teste", "cpf", "documentos"]
keywords: ["gerador de cnpj", "gerador de cnpj online", "cnpj", "empresas", "gerador"]
---

Basta escolher as opções abaixo e depois clicar em **Gerar CNPJ**.

<div id="gerador-cnpj" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de CNPJ</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere um CNPJ válido para testes.</p>
<label for="cnpj-pontuacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</label>
<select id="cnpj-pontuacao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim">Sim</option>
<option value="nao">Não</option>
</select>
<label for="cnpj-formato" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Formato</label>
<select id="cnpj-formato" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="num">Numérico (atual)</option>
<option value="alfa">Alfanumérico (IN RFB 2.229/2024)</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cnpj-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar CNPJ</button>
<button type="button" id="cnpj-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="cnpj-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">CNPJ gerado:</strong> <span id="cnpj-resultado">clique em "Gerar CNPJ".</span></div>
</div>
<script>
(function () {
  var selPontuacao = document.getElementById('cnpj-pontuacao');
  var selFormato = document.getElementById('cnpj-formato');
  var resultado = document.getElementById('cnpj-resultado');
  var caixa = document.getElementById('cnpj-resposta');
  var btnCopiar = document.getElementById('cnpj-copiar');
  var atual = '';
  var NUMEROS = '0123456789';
  var ALFANUM = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  var PESOS1 = [5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
  var PESOS2 = [6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
  function sorteio(n) { return Math.floor(Math.random() * n); }
  function digito(base, pesos) {
    var soma = 0;
    for (var i = 0; i !== base.length; i++) {
      soma += (base.charCodeAt(i) - 48) * pesos[i];
    }
    var resto = soma % 11;
    return resto === 0 ? 0 : (resto === 1 ? 0 : 11 - resto);
  }
  function raizAleatoria(alfabeto) {
    var raiz = '';
    for (var i = 0; i !== 8; i++) { raiz += alfabeto.charAt(sorteio(alfabeto.length)); }
    return raiz;
  }
  function todosIguais(t) { return t === new Array(t.length + 1).join(t.charAt(0)); }
  function formatar(c) {
    return c.substr(0, 2) + '.' + c.substr(2, 3) + '.' + c.substr(5, 3) + '/' + c.substr(8, 4) + '-' + c.substr(12, 2);
  }
  function gerar() {
    var alfabeto = selFormato.value === 'alfa' ? ALFANUM : NUMEROS;
    var raiz = raizAleatoria(alfabeto);
    while (todosIguais(raiz)) { raiz = raizAleatoria(alfabeto); }
    var base = raiz + '0001';
    var d1 = digito(base, PESOS1);
    var d2 = digito(base + d1, PESOS2);
    var cnpj = base + d1 + d2;
    atual = selPontuacao.value === 'sim' ? formatar(cnpj) : cnpj;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = '<strong style="font-size:1.2rem;letter-spacing:0.5px;">' + atual + '</strong>';
    btnCopiar.textContent = 'Copiar';
  }
  function copiado() { btnCopiar.textContent = 'Copiado!'; }
  function copiarFallback(texto) {
    var ta = document.createElement('textarea');
    ta.value = texto;
    ta.style.position = 'fixed';
    ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.select();
    try { document.execCommand('copy'); copiado(); } catch (e) { }
    document.body.removeChild(ta);
  }
  function copiar() {
    if (atual === '') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
      resultado.textContent = 'gere um CNPJ antes de copiar.';
      return;
    }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).then(copiado, function () { copiarFallback(atual); });
    } else {
      copiarFallback(atual);
    }
  }
  document.getElementById('cnpj-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  [selPontuacao, selFormato].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o CNPJ com pontos, barra e traço (`12.345.678/0001-95`) ou **Não** para receber apenas os caracteres (`12345678000195`).
2. Em **Formato**, escolha **Numérico (atual)** para o CNPJ tradicional, só com números, ou **Alfanumérico (IN RFB 2.229/2024)** para o novo padrão, que também usa letras.
3. Clique em **Gerar CNPJ** para criar um novo número válido. Clique de novo sempre que quiser outro.
4. Clique em **Copiar** para levar o CNPJ para a área de transferência e colar onde precisar.

Os números são gerados de forma aleatória, respeitando as regras de criação do documento. Eles servem para **testes e desenvolvimento** e não pertencem a empresas reais. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **CNPJ:** Cadastro Nacional da Pessoa Jurídica, número que identifica uma empresa perante a Receita Federal do Brasil.
- **CNPJ válido:** número cujos dígitos verificadores batem com o cálculo oficial. Isso não significa que a empresa exista de fato.
- **Raiz (base):** os 8 primeiros caracteres, que identificam a empresa em si.
- **Ordem (filial):** os 4 caracteres seguintes, que identificam o estabelecimento. Aqui usamos `0001`, que indica a matriz.
- **Dígitos verificadores:** os 2 últimos dígitos, calculados a partir dos anteriores para conferir se o número é válido.
- **Com pontuação:** CNPJ escrito no formato `XX.XXX.XXX/XXXX-XX`, com pontos, barra e traço.
- **Sem pontuação:** CNPJ escrito apenas com os 14 caracteres, sem separadores.
- **Formato numérico:** padrão atual, em que os 12 primeiros caracteres são apenas números de 0 a 9.
- **Formato alfanumérico:** novo padrão da Receita Federal (IN RFB 2.229/2024), em que os 12 primeiros caracteres podem ser números ou letras de A a Z. Os dois dígitos verificadores continuam sendo números.
- **Dados de teste:** informações fictícias usadas para testar sistemas, formulários e cadastros sem precisar de documentos reais.