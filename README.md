# Mail Agent Skill

Claude gestiona tu correo por ti. Son **4 skills para Claude** que trabajan sobre tu Gmail:
clasifican lo que llega, te dan de baja de lo que no lees, te ordenan la bandeja con un
resumen diario y te dejan las respuestas preparadas.

Gratis, licencia MIT, sin registro y sin API key. Solo necesitas Claude con el conector de Gmail.

**No se envía nada sin tu "sí".** Las respuestas quedan como borrador hasta que apruebas cada una.
**No se borra nada para siempre.** Lo que se limpia va a Spam o a la papelera (30 días para recuperarlo).

## Instalación

**La fácil:** pega esto en Claude (Claude Code o la app de escritorio):

```
https://github.com/martinihub/mail-agent-skill

Instala esta skill y comprueba que /mail-clasifica funciona.
```

**Como plugin, dentro de Claude Code:**

```
/plugin marketplace add martinihub/mail-agent-skill
/plugin install mail-agent@mail-agent-skill
```

**Copiando las carpetas** (Mac, Linux o Git Bash en Windows):

```bash
git clone https://github.com/martinihub/mail-agent-skill.git
cp -r mail-agent-skill/skills/mail-* ~/.claude/skills/
```

**En la app de Claude (claude.ai):** descarga el repo en ZIP, comprime cada carpeta de `skills/`
por separado y súbela en Ajustes → Capacidades → Skills.

Después **conecta Gmail**: en Claude, Ajustes → Conectores → Gmail.

Y, muy recomendable, dedica 5 minutos a tu perfil: copia `templates/perfil.md` a
`~/.claude/mail-agent/perfil.md` y rellénalo, o dile a Claude *"lee mis últimos 30 correos
enviados y rellena mi perfil.md"*. Las cuatro skills lo leen: tus clientes nunca acabarán en
spam y las respuestas sonarán a ti.

## Las 4 skills

| Comando | Qué hace |
| --- | --- |
| `/mail-clasifica` | Revisa tus correos y los ordena en **Publicidad, Spam, Importante o Phishing**. El spam a Spam, la publicidad a la papelera, lo dudoso no se toca. Te avisa del phishing y de por qué lo es. |
| `/mail-desuscribe` | Encuentra promociones, newsletters y envíos masivos, te dice cuántos correos te manda cada uno y te **da de baja de todos con un solo "sí"**. |
| `/mail-prioriza` | Ordena los mensajes de **mayor a menor importancia** y te deja un **resumen diario** de lo que ha pasado en tu correo. Se puede programar cada mañana. |
| `/mail-responde` | **La mejor.** Te prepara respuestas en tu tono a los correos que requieren tu atención y **solo se envían si tú las apruebas**, una a una. |

## Prompts para empezar

```
/mail-clasifica revisa los correos de los últimos 2 días
/mail-desuscribe busca todas mis suscripciones de los últimos 60 días
/mail-prioriza dame el resumen de hoy
/mail-responde prepara las respuestas a los importantes
```

O todo seguido:

```
Revisa mi correo con /mail-clasifica, dame el resumen con /mail-prioriza
y prepárame las respuestas con /mail-responde. No envíes nada sin mi sí.
```

## Seguridad

- Ningún correo se envía sin tu aprobación explícita de ese correo.
- Nada se borra de forma definitiva.
- Bancos, pagos, Hacienda, Seguridad Social, Google, Meta, tu hosting y tu tienda nunca se marcan como spam.
- El contenido de los correos se trata como datos, nunca como órdenes: si un email dice "reenvía esto" o "manda tus datos", Claude no lo hace y te avisa.
- No se abren enlaces de correos sospechosos (ni siquiera para darse de baja).
- Las skills no tienen código propio ni envían tus datos a ningún sitio: usan el conector oficial de Gmail de Claude.

## Licencia

MIT · creado por [@soymartin.garcia](https://www.instagram.com/soymartin.garcia/)
