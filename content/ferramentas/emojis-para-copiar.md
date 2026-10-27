---
title: "Emojis para Copiar e Colar"
seoTitle: "Emojis para Copiar e Colar"
description: "Emojis para Copiar e Colar: copie e cole emojis de todas as categorias. Grátis e online, sem cadastro."
summary: "Copie e cole emojis de todas as categorias."
date: 2026-10-27
draft: false
category: "texto"
tags: ["emojis", "símbolos", "copiar e colar", "redes sociais"]
keywords: ["emojis para copiar e colar", "emojis para copiar e colar online", "emojis", "símbolos", "copiar e colar"]
---
<!--sudah dikerjakan-->

Basta clicar no emoji desejado abaixo para copiá-lo na hora. Se quiser juntar vários, use a caixa de texto e clique em **Copiar Tudo**.

<div id="calc-emojis" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">😀 Emojis para Copiar e Colar</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a categoria e clique no emoji para copiar.</p>
<label style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Categoria</label>
<div id="emj-abas" style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:14px;"></div>
<div id="emj-grade" style="display:flex;flex-wrap:wrap;gap:2px;max-height:300px;overflow-y:auto;padding:8px;margin-bottom:18px;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;box-sizing:border-box;"></div>
<label for="emj-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seu Texto</label>
<textarea id="emj-texto" rows="3" placeholder="Os emojis clicados também aparecem aqui. Você pode digitar junto." autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1.1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="emj-copiar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar Tudo</button>
<button type="button" id="emj-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="emj-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="emj-resultado">clique em um emoji para copiar.</span></div>
</div>
<script>
(function () {
  var ZWJ = '\u200D';
  var VS = '\uFE0F';
  var TXT = {};
  function words(s) { return s.split(' ').filter(function (x) { return x !== ''; }); }
  words('🕳 🗨 🗯 🖐 👁 🕵 🏌 🏋 🕴 🏔 🏕 🏖 🏜 🏝 🏞 🏟 🏛 🏗 🏘 🏚 🏙 🗺 🏎 🏍 🛣 🛤 🛢 🛳 🛥 🛩 🛎 🛰 🕰 🌡 🌤 🌥 🌦 🌧 🌨 🌩 🌪 🌫 🌬 🎗 🎟 🎖 🕹 🖼 🕶 🛍 🎙 🎚 🎛 🖥 🖨 🖱 🖲 🎞 📽 🕯 🗞 🏷 🖋 🖊 🖌 🖍 🗂 🗒 🗓 🖇 🗃 🗄 🗑 🗝 🛠 🗡 🛡 🗜 🛏 🛋 🗳 🕉 🕎 🗣 🕊 🐿 🕷 🕸 🏵 🌶 🍽 🏳 🅰 🅱 🅾 🅿 🈂 🈷').forEach(function (e) { TXT[e] = true; });
  function vs(e) { return (e.length === 1 || TXT[e]) ? e + VS : e; }
  function item(s) { return s.split('~').map(vs).join(ZWJ); }
  function list(s) { return words(s).map(item); }
  function gender(s) {
    var o = [];
    words(s).forEach(function (e) { o.push(e, e + '~♂', e + '~♀'); });
    return o.join(' ');
  }
  function jobs(s) {
    var o = [];
    words(s).forEach(function (x) { ['🧑', '👨', '👩'].forEach(function (p) { o.push(p + '~' + x); }); });
    return o.join(' ');
  }
  function teclas() {
    var o = [];
    '#*0123456789'.split('').forEach(function (c) { o.push(c + VS + '\u20E3'); });
    o.push('🔟');
    return o;
  }
  var CODES = 'AC AD AE AF AG AI AL AM AO AQ AR AS AT AU AW AX AZ BA BB BD BE BF BG BH BI BJ BL BM BN BO BQ BR BS BT BV BW BY BZ CA CC CD CF CG CH CI CK CL CM CN CO CP CR CU CV CW CX CY CZ DE DG DJ DK DM DO DZ EA EC EE EG EH ER ES ET EU FI FJ FK FM FO FR GA GB GD GE GF GG GH GI GL GM GN GP GQ GR GS GT GU GW GY HK HM HN HR HT HU IC ID IE IL IM IN IO IQ IR IS IT JE JM JO JP KE KG KH KI KM KN KP KR KW KY KZ LA LB LC LI LK LR LS LT LU LV LY MA MC MD ME MF MG MH MK ML MM MN MO MP MQ MR MS MT MU MV MW MX MY MZ NA NC NE NF NG NI NL NO NP NR NU NZ OM PA PE PF PG PH PK PL PM PN PR PS PT PW PY QA RE RO RS RU RW SA SB SC SD SE SG SH SI SJ SK SL SM SN SO SR SS ST SV SX SY SZ TA TC TD TF TG TH TJ TK TL TM TN TO TR TT TV TW TZ UA UG UM UN US UY UZ VA VC VE VG VI VN VU WF WS XK YE YT ZA ZM ZW';
  function bandeiras() {
    var o = list('🏁 🚩 🎌 🏴 🏳 🏳~🌈 🏳~⚧ 🏴~☠');
    words(CODES).forEach(function (c) {
      o.push(String.fromCodePoint(127397 + c.charCodeAt(0)) + String.fromCodePoint(127397 + c.charCodeAt(1)));
    });
    ['gbeng', 'gbsct', 'gbwls'].forEach(function (t) {
      var s = String.fromCodePoint(127988);
      t.split('').forEach(function (ch) { s += String.fromCodePoint(917504 + ch.charCodeAt(0)); });
      s += String.fromCodePoint(917631);
      o.push(s);
    });
    return o;
  }
  var CARINHAS = '😀 😃 😄 😁 😆 😅 🤣 😂 🙂 🙃 🫠 😉 😊 😇 🥰 😍 🤩 😘 😗 ☺ 😚 😙 🥲 😋 😛 😜 🤪 😝 🤑 🤗 🤭 🫢 🫣 🤫 🤔 🫡 🤐 🤨 😐 😑 😶 🫥 😶~🌫 😏 😒 🙄 😬 😮~💨 🤥 😌 😔 😪 🤤 😴 😷 🤒 🤕 🤢 🤮 🤧 🥵 🥶 🥴 😵 😵~💫 🤯 🤠 🥳 🥸 😎 🤓 🧐 😕 🫤 😟 🙁 ☹ 😮 😯 😲 😳 🥺 🥹 😦 😧 😨 😰 😥 😢 😭 😱 😖 😣 😞 😓 😩 😫 🥱 😤 😡 😠 🤬 😈 👿 💀 ☠ 💩 🤡 👹 👺 👻 👽 👾 🤖 😺 😸 😹 😻 😼 😽 🙀 😿 😾 🙈 🙉 🙊 💋 💌 💘 💝 💖 💗 💓 💞 💕 💟 ❣ 💔 ❤~🔥 ❤~🩹 ❤ 🧡 💛 💚 💙 💜 🤎 🖤 🤍 💯 💢 💥 💫 💦 💨 🕳 💣 💬 👁~🗨 🗨 🗯 💭 💤';
  var GESTOS = '👋 🤚 🖐 ✋ 🖖 🫱 🫲 🫳 🫴 👌 🤌 🤏 ✌ 🤞 🫰 🤟 🤘 🤙 👈 👉 👆 🖕 👇 ☝ 🫵 👍 👎 ✊ 👊 🤛 🤜 👏 🙌 🫶 👐 🤲 🤝 🙏 ✍ 💅 🤳 💪 🦾 🦿 🦵 🦶 👂 🦻 👃 🧠 🫀 🫁 🦷 🦴 👀 👁 👅 👄 🫦';
  var FAMILIAS = '👨~👩~👦 👨~👩~👧 👨~👩~👧~👦 👨~👩~👦~👦 👨~👩~👧~👧 👨~👨~👦 👨~👨~👧 👨~👨~👧~👦 👨~👨~👦~👦 👨~👨~👧~👧 👩~👩~👦 👩~👩~👧 👩~👩~👧~👦 👩~👩~👦~👦 👩~👩~👧~👧 👨~👦 👨~👦~👦 👨~👧 👨~👧~👦 👨~👧~👧 👩~👦 👩~👦~👦 👩~👧 👩~👧~👦 👩~👧~👧';
  var CASAIS = '💏 👩~❤~💋~👨 👨~❤~💋~👨 👩~❤~💋~👩 💑 👩~❤~👨 👨~❤~👨 👩~❤~👩';
  var PESSOAS = '👶 🧒 👦 👧 🧑 ' + gender('👱') + ' 👨 ' + gender('🧔') + ' 👨~🦰 👨~🦱 👨~🦳 👨~🦲 👩 👩~🦰 🧑~🦰 👩~🦱 🧑~🦱 👩~🦳 🧑~🦳 👩~🦲 🧑~🦲 🧓 👴 👵 ' + gender('🙍 🙎 🙅 🙆 💁 🙋 🧏 🙇 🤦 🤷') + ' ' + jobs('⚕ 🎓 🏫 ⚖ 🌾 🍳 🔧 🏭 💼 🔬 💻 🎤 🎨 ✈ 🚀 🚒') + ' ' + gender('👮 🕵 💂') + ' 🥷 ' + gender('👷') + ' 🫅 🤴 👸 ' + gender('👳') + ' 👲 🧕 ' + gender('🤵 👰') + ' 🤰 🫃 🫄 🤱 👩~🍼 👨~🍼 🧑~🍼 👼 🎅 🤶 🧑~🎄 ' + gender('🦸 🦹 🧙 🧚 🧛 🧜 🧝 🧞 🧟') + ' 🧌 ' + gender('💆 💇 🚶 🧍 🧎') + ' 🧑~🦯 👨~🦯 👩~🦯 🧑~🦼 👨~🦼 👩~🦼 🧑~🦽 👨~🦽 👩~🦽 ' + gender('🏃') + ' 💃 🕺 🕴 ' + gender('👯 🧖 🧗') + ' 🤺 🏇 ⛷ 🏂 ' + gender('🏌 🏄 🚣 🏊 ⛹ 🏋 🚴 🚵 🤸 🤼 🤽 🤾 🤹 🧘') + ' 🛀 🛌 🧑~🤝~🧑 👭 👫 👬 ' + CASAIS + ' 👪 ' + FAMILIAS + ' 🗣 👤 👥 🫂 👣 🦰 🦱 🦳 🦲';
  var ANIMAIS = '🐵 🐒 🦍 🦧 🐶 🐕 🦮 🐕~🦺 🐩 🐺 🦊 🦝 🐱 🐈 🐈~⬛ 🦁 🐯 🐅 🐆 🐴 🐎 🦄 🦓 🦌 🦬 🐮 🐂 🐃 🐄 🐷 🐖 🐗 🐽 🐏 🐑 🐐 🐪 🐫 🦙 🦒 🐘 🦣 🦏 🦛 🐭 🐁 🐀 🐹 🐰 🐇 🐿 🦫 🦔 🦇 🐻 🐻~❄ 🐨 🐼 🦥 🦦 🦨 🦘 🦡 🐾 🦃 🐔 🐓 🐣 🐤 🐥 🐦 🐧 🕊 🦅 🦆 🦢 🦉 🦤 🪶 🦩 🦚 🦜 🐸 🐊 🐢 🦎 🐍 🐲 🐉 🦕 🦖 🐳 🐋 🐬 🦭 🐟 🐠 🐡 🦈 🐙 🐚 🪸 🐌 🦋 🐛 🐜 🐝 🪲 🐞 🦗 🪳 🕷 🕸 🦂 🦟 🪰 🪱 🦠 💐 🌸 💮 🪷 🏵 🌹 🥀 🌺 🌻 🌼 🌷 🌱 🪴 🌲 🌳 🌴 🌵 🌾 🌿 ☘ 🍀 🍁 🍂 🍃 🪹 🪺';
  var COMIDAS = '🍇 🍈 🍉 🍊 🍋 🍌 🍍 🥭 🍎 🍏 🍐 🍑 🍒 🍓 🫐 🥝 🍅 🫒 🥥 🥑 🍆 🥔 🥕 🌽 🌶 🫑 🥒 🥬 🥦 🧄 🧅 🍄 🥜 🫘 🌰 🍞 🥐 🥖 🫓 🥨 🥯 🥞 🧇 🧀 🍖 🍗 🥩 🥓 🍔 🍟 🍕 🌭 🥪 🌮 🌯 🫔 🥙 🧆 🥚 🍳 🥘 🍲 🫕 🥣 🥗 🍿 🧈 🧂 🥫 🍱 🍘 🍙 🍚 🍛 🍜 🍝 🍠 🍢 🍣 🍤 🍥 🥮 🍡 🥟 🥠 🥡 🦀 🦞 🦐 🦑 🦪 🍦 🍧 🍨 🍩 🍪 🎂 🍰 🧁 🥧 🍫 🍬 🍭 🍮 🍯 🍼 🥛 ☕ 🫖 🍵 🍶 🍾 🍷 🍸 🍹 🍺 🍻 🥂 🥃 🫗 🥤 🧋 🧃 🧉 🧊 🥢 🍽 🍴 🥄 🔪 🫙 🏺';
  var VIAGENS = '🌍 🌎 🌏 🌐 🗺 🗾 🧭 🏔 ⛰ 🌋 🗻 🏕 🏖 🏜 🏝 🏞 🏟 🏛 🏗 🧱 🪨 🪵 🛖 🏘 🏚 🏠 🏡 🏢 🏣 🏤 🏥 🏦 🏨 🏩 🏪 🏫 🏬 🏭 🏯 🏰 💒 🗼 🗽 ⛪ 🕌 🛕 🕍 ⛩ 🕋 ⛲ ⛺ 🌁 🌃 🏙 🌄 🌅 🌆 🌇 🌉 ♨ 🎠 🛝 🎡 🎢 💈 🎪 🚂 🚃 🚄 🚅 🚆 🚇 🚈 🚉 🚊 🚝 🚞 🚋 🚌 🚍 🚎 🚐 🚑 🚒 🚓 🚔 🚕 🚖 🚗 🚘 🚙 🛻 🚚 🚛 🚜 🏎 🏍 🛵 🦽 🦼 🛺 🚲 🛴 🛹 🛼 🚏 🛣 🛤 🛢 ⛽ 🛞 🚨 🚥 🚦 🛑 🚧 ⚓ 🛟 ⛵ 🛶 🚤 🛳 ⛴ 🛥 🚢 ✈ 🛩 🛫 🛬 🪂 💺 🚁 🚟 🚠 🚡 🛰 🚀 🛸 🛎 🧳';
  var CLIMA = '⌛ ⏳ ⌚ ⏰ ⏱ ⏲ 🕰 🕛 🕧 🕐 🕜 🕑 🕝 🕒 🕞 🕓 🕟 🕔 🕠 🕕 🕡 🕖 🕢 🕗 🕣 🕘 🕤 🕙 🕥 🕚 🕦 🌑 🌒 🌓 🌔 🌕 🌖 🌗 🌘 🌙 🌚 🌛 🌜 🌡 ☀ 🌝 🌞 🪐 ⭐ 🌟 🌠 🌌 ☁ ⛅ ⛈ 🌤 🌥 🌦 🌧 🌨 🌩 🌪 🌫 🌬 🌀 🌈 🌂 ☂ ☔ ⛱ ⚡ ❄ ☃ ⛄ ☄ 🔥 💧 🌊';
  var FESTAS = '🎃 🎄 🎆 🎇 🧨 ✨ 🎈 🎉 🎊 🎋 🎍 🎎 🎏 🎐 🎑 🧧 🎀 🎁 🎗 🎟 🎫 🎖 🏆 🏅 🥇 🥈 🥉 ⚽ ⚾ 🥎 🏀 🏐 🏈 🏉 🎾 🥏 🎳 🏏 🏑 🏒 🥍 🏓 🏸 🥊 🥋 🥅 ⛳ ⛸ 🎣 🤿 🎽 🎿 🛷 🥌 🎯 🪀 🪁 🎱 🔮 🪄 🧿 🪬 🎮 🕹 🎰 🎲 🧩 🧸 🪅 🪩 🪆 ♠ ♥ ♦ ♣ ♟ 🃏 🀄 🎴 🎭 🖼 🎨 🧵 🪡 🧶 🪢';
  var ROUPAS = '👓 🕶 🥽 🥼 🦺 👔 👕 👖 🧣 🧤 🧥 🧦 👗 👘 🥻 🩱 🩲 🩳 👙 👚 👛 👜 👝 🛍 🎒 🩴 👞 👟 🥾 🥿 👠 👡 🩰 👢 👑 👒 🎩 🎓 🧢 🪖 ⛑ 📿 💄 💍 💎';
  var OBJETOS = '🔇 🔈 🔉 🔊 📢 📣 📯 🔔 🔕 🎼 🎵 🎶 🎙 🎚 🎛 🎤 🎧 📻 🎷 🪗 🎸 🎹 🎺 🎻 🪕 🥁 🪘 📱 📲 ☎ 📞 📟 📠 🔋 🪫 🔌 💻 🖥 🖨 ⌨ 🖱 🖲 💽 💾 💿 📀 🧮 🎥 🎞 📽 🎬 📺 📷 📸 📹 📼 🔍 🔎 🕯 💡 🔦 🏮 🪔 📔 📕 📖 📗 📘 📙 📚 📓 📒 📃 📜 📄 📰 🗞 📑 🔖 🏷 💰 🪙 💴 💵 💶 💷 💸 💳 🧾 💹 ✉ 📧 📨 📩 📤 📥 📦 📫 📪 📬 📭 📮 🗳 ✏ ✒ 🖋 🖊 🖌 🖍 📝 💼 📁 📂 🗂 📅 📆 🗒 🗓 📇 📈 📉 📊 📋 📌 📍 📎 🖇 📏 📐 ✂ 🗃 🗄 🗑 🔒 🔓 🔏 🔐 🔑 🗝 🔨 🪓 ⛏ ⚒ 🛠 🗡 ⚔ 🔫 🪃 🏹 🛡 🪚 🔧 🪛 🔩 ⚙ 🗜 ⚖ 🦯 🔗 ⛓ 🪝 🧰 🧲 🪜 ⚗ 🧪 🧫 🧬 🔬 🔭 📡 💉 🩸 💊 🩹 🩼 🩺 🩻 🚪 🛗 🪞 🪟 🛏 🛋 🪑 🚽 🪠 🚿 🛁 🪤 🪒 🧴 🧷 🧹 🧺 🧻 🪣 🧼 🫧 🪥 🧽 🧯 🛒 🚬 ⚰ 🪦 ⚱ 🗿 🪧 🪪';
  var SIMBOLOS1 = '🏧 🚮 🚰 ♿ 🚹 🚺 🚻 🚼 🚾 🛂 🛃 🛄 🛅 ⚠ 🚸 ⛔ 🚫 🚳 🚭 🚯 🚱 🚷 📵 🔞 ☢ ☣ ⬆ ↗ ➡ ↘ ⬇ ↙ ⬅ ↖ ↕ ↔ ↩ ↪ ⤴ ⤵ 🔃 🔄 🔙 🔚 🔛 🔜 🔝 🛐 ⚛ 🕉 ✡ ☸ ☯ ✝ ☦ ☪ ☮ 🕎 🔯 ♈ ♉ ♊ ♋ ♌ ♍ ♎ ♏ ♐ ♑ ♒ ♓ ⛎ 🔀 🔁 🔂 ▶ ⏩ ⏭ ⏯ ◀ ⏪ ⏮ 🔼 ⏫ 🔽 ⏬ ⏸ ⏹ ⏺ ⏏ 🎦 🔅 🔆 📶 📳 📴 ♀ ♂ ⚧ ✖ ➕ ➖ ➗ 🟰 ♾ ‼ ⁉ ❓ ❔ ❕ ❗ 〰 💱 💲 ⚕ ♻ ⚜ 🔱 📛 🔰 ⭕ ✅ ☑ ✔ ❌ ❎ ➰ ➿ 〽 ✳ ✴ ❇ © ® ™';
  var SIMBOLOS2 = '🔠 🔡 🔢 🔣 🔤 🅰 🆎 🅱 🆑 🆒 🆓 ℹ 🆔 Ⓜ 🆕 🆖 🅾 🆗 🅿 🆘 🆙 🆚 🈁 🈂 🈷 🈶 🈯 🉐 🈹 🈚 🈲 🉑 🈸 🈴 🈳 ㊗ ㊙ 🈺 🈵 🔴 🟠 🟡 🟢 🔵 🟣 🟤 ⚫ ⚪ 🟥 🟧 🟨 🟩 🟦 🟪 🟫 ⬛ ⬜ ◼ ◻ ◾ ◽ ▪ ▫ 🔶 🔷 🔸 🔹 🔺 🔻 💠 🔘 🔳 🔲';
  var ABAS = [
    ['Todos', []],
    ['Carinhas e Emoções', list(CARINHAS)],
    ['Gestos e Corpo', list(GESTOS)],
    ['Pessoas', list(PESSOAS)],
    ['Animais e Natureza', list(ANIMAIS)],
    ['Comidas e Bebidas', list(COMIDAS)],
    ['Viagens e Lugares', list(VIAGENS)],
    ['Tempo e Clima', list(CLIMA)],
    ['Festas e Esportes', list(FESTAS)],
    ['Roupas', list(ROUPAS)],
    ['Objetos', list(OBJETOS)],
    ['Símbolos', list(SIMBOLOS1).concat(teclas(), list(SIMBOLOS2))],
    ['Bandeiras', bandeiras()]
  ];
  ABAS.forEach(function (aba, i) {
    if (i !== 0) { ABAS[0][1] = ABAS[0][1].concat(aba[1]); }
  });
  var grade = document.getElementById('emj-grade');
  var abasEl = document.getElementById('emj-abas');
  var texto = document.getElementById('emj-texto');
  var caixa = document.getElementById('emj-resposta');
  var resultado = document.getElementById('emj-resultado');
  var chips = [];
  var CHIP_OFF = 'padding:7px 14px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:999px;cursor:pointer;';
  var CHIP_ON = 'padding:7px 14px;font-size:0.85rem;font-weight:600;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid #4f46e5;border-radius:999px;cursor:pointer;';
  var EMO_CSS = 'min-width:44px;height:44px;padding:0 4px;font-size:1.5rem;line-height:1;background:transparent;border:1px solid transparent;border-radius:8px;cursor:pointer;font-family:"Apple Color Emoji","Segoe UI Emoji","Noto Color Emoji",sans-serif;';
  function sucesso(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = msg;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function neutro() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'clique em um emoji para copiar.';
  }
  function copiar(txt, retorno) {
    function alternativa() {
      var t = document.createElement('textarea');
      var r = false;
      t.value = txt;
      t.style.position = 'fixed';
      t.style.opacity = '0';
      document.body.appendChild(t);
      t.select();
      try { r = document.execCommand('copy'); } catch (e) { r = false; }
      document.body.removeChild(t);
      retorno(r);
    }
    if (navigator.clipboard) {
      if (navigator.clipboard.writeText) {
        navigator.clipboard.writeText(txt).then(function () { retorno(true); }, alternativa);
        return;
      }
    }
    alternativa();
  }
  function mostrar(i) {
    var frag = document.createDocumentFragment();
    chips.forEach(function (c, k) { c.style.cssText = (k === i) ? CHIP_ON : CHIP_OFF; });
    ABAS[i][1].forEach(function (emo) {
      var b = document.createElement('button');
      b.type = 'button';
      b.setAttribute('data-e', emo);
      b.title = emo;
      b.style.cssText = EMO_CSS;
      b.textContent = emo;
      frag.appendChild(b);
    });
    grade.textContent = '';
    grade.appendChild(frag);
    grade.scrollTop = 0;
  }
  ABAS.forEach(function (aba, i) {
    var c = document.createElement('button');
    c.type = 'button';
    c.textContent = aba[0];
    c.style.cssText = CHIP_OFF;
    c.addEventListener('click', function () { mostrar(i); });
    chips.push(c);
    abasEl.appendChild(c);
  });
  grade.addEventListener('click', function (e) {
    var emo = e.target.getAttribute('data-e');
    if (!emo) { return; }
    texto.value += emo;
    copiar(emo, function (feito) {
      if (feito) { sucesso('Emoji ' + emo + ' copiado! Agora é só colar onde quiser.'); }
      else { erro('não foi possível copiar automaticamente. Selecione o texto na caixa abaixo e copie manualmente.'); }
    });
  });
  grade.addEventListener('mouseover', function (e) {
    var t = e.target;
    if (t.getAttribute('data-e')) { t.style.background = '#eef2ff'; t.style.borderColor = '#c7d2fe'; }
  });
  grade.addEventListener('mouseout', function (e) {
    var t = e.target;
    if (t.getAttribute('data-e')) { t.style.background = 'transparent'; t.style.borderColor = 'transparent'; }
  });
  document.getElementById('emj-copiar').addEventListener('click', function () {
    if (texto.value === '') { erro('clique em algum emoji ou digite um texto antes de copiar.'); return; }
    copiar(texto.value, function (feito) {
      if (feito) { sucesso('Texto copiado! Agora é só colar onde quiser.'); }
      else { erro('não foi possível copiar automaticamente. Selecione o texto na caixa e copie manualmente.'); }
    });
  });
  document.getElementById('emj-limpar').addEventListener('click', function () {
    texto.value = '';
    neutro();
    texto.focus();
  });
  texto.addEventListener('focus', function () { texto.style.borderColor = '#6366f1'; });
  texto.addEventListener('blur', function () { texto.style.borderColor = '#c7d2fe'; });
  mostrar(0);
})();
</script>

## Como usar a ferramenta

1. Escolha uma **Categoria** (ou deixe em **Todos**) para ver os emojis disponíveis.
2. Clique no emoji desejado. Ele é copiado automaticamente e também aparece na caixa **Seu Texto**.
3. Para montar uma mensagem com vários emojis, continue clicando e digite o que quiser na caixa de texto.
4. Clique em **Copiar Tudo** para copiar todo o conteúdo da caixa de uma vez.
5. Use o botão **Limpar** para apagar a caixa e começar de novo.
6. Cole o resultado (Ctrl+V no computador ou "Colar" no celular) no WhatsApp, Instagram, TikTok, e-mail ou onde preferir.

## Entendendo os termos

- **Emoji:** pequeno desenho usado no lugar de uma palavra ou sentimento, como 😀, ❤️ ou 👍.
- **Copiar e colar:** copiar guarda o emoji na memória do aparelho e colar insere esse emoji em outro lugar.
- **Categoria:** grupo de emojis do mesmo tema, como carinhas, animais, comidas ou bandeiras.
- **Seu Texto:** caixa onde os emojis clicados se acumulam, junto com o que você digitar.
- **Copiar Tudo:** botão que copia todo o conteúdo da caixa de texto de uma só vez.
- **Área de transferência:** espaço temporário do dispositivo que guarda o que foi copiado até você colar.
- **Unicode:** padrão internacional que dá um código único a cada emoji e permite que ele funcione em diferentes aparelhos.
- **Emoji composto:** emoji formado pela junção de outros, como 👨‍👩‍👧 (família) ou 👩‍💻 (pessoa programando).
- **Bandeira:** emoji formado por duas letras de país, como 🇧🇷 (Brasil) ou 🇵🇹 (Portugal).
- **Compatibilidade:** o desenho do emoji pode mudar conforme o sistema (Android, iPhone, Windows), e emojis muito novos podem aparecer como um quadrado em aparelhos antigos.