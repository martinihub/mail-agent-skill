---
name: mail-desuscribe
description: Encuentra todas las promociones, newsletters y envíos masivos que llegan a tu Gmail, los agrupa por remitente con cuántos correos manda cada uno y te da de baja de los que elijas con un solo "sí", limpiando también los correos antiguos. Úsala cuando el usuario pida "desuscríbeme", "date de baja de las newsletters", "me llegan demasiadas promociones" o "limpia las suscripciones".
---

# /mail-desuscribe — Skill 2 de Mail Agent

Te permite desuscribirte de promociones, newsletters y envíos masivos de correos con un solo clic.

## Reglas que no se rompen
1. **No se da de baja de nada sin el "sí" del usuario** a la lista concreta que ha visto.
2. **Nunca** se desuscribe de bancos, pasarelas de pago, Hacienda, Seguridad Social, tu hosting o tu tienda, ni de las "newsletters que SÍ quiero conservar" de `perfil.md`.
3. **Solo se usa el enlace de baja del propio remitente** (cabecera *List-Unsubscribe* o el enlace "darse de baja" del pie del correo). Si el correo huele a phishing, NO se abre su enlace: se marca como spam (los enlaces de baja falsos confirman que tu dirección existe).
4. En el formulario de baja no se escribe ningún dato que no sea tu dirección de correo.

## Paso 0 — Preparar
- Lee `~/.claude/mail-agent/perfil.md` si existe.
- Conector de Gmail cargado (buscar, leer, etiquetar, papelera). Para abrir los enlaces de baja hace falta navegador: **Claude in Chrome** o el navegador integrado de Claude. Si no hay, se prepara la lista de enlaces para que el usuario los pulse él.

## Paso 1 — Encontrar suscripciones
- Busca `category:promotions OR "unsubscribe" OR "darse de baja" OR "cancelar suscripción" newer_than:60d` (más el rango que pida el usuario).
- Agrupa por remitente: nombre, dominio, nº de correos en el periodo, si el usuario ha abierto o respondido alguno, y el enlace de baja.
- Clasifica cada grupo en **Promociones**, **Newsletters** o **Envíos masivos**.

## Paso 2 — Proponer
```
📬 Suscripciones encontradas: N remitentes · X correos en 60 días

Promociones
☐ Tienda X — 23 correos — nunca abiertos
Newsletters
☐ Blog Y — 8 correos — abriste 1
Envíos masivos
☐ Plataforma Z — 41 correos

Propuesta: darte de baja de las marcadas (las que nunca abres).
→ ✅ Darme de baja de todas | ✏️ Elegir cuáles | ❌ Nada
```
Usa AskUserQuestion si está disponible.

## Paso 3 — Darse de baja (tras el "sí")
Para cada remitente aprobado, en este orden:
1. Si la cabecera *List-Unsubscribe* trae un enlace https de baja en un clic, ábrelo y confirma.
2. Si no, abre el enlace "darse de baja" del pie y pulsa el botón de confirmar. Si pide algo más que tu email o una casilla, para y apúntalo como "baja manual".
3. Si no hay enlace de baja: crea la etiqueta `Mail Agent/Silenciados` y propón al usuario un filtro de Gmail (en Gmail → buscar `from:remitente` → Crear filtro → Omitir bandeja). Explícale los 3 clics.
4. Mueve a la papelera los correos antiguos de ese remitente (recuperables 30 días).

## Paso 4 — Cierre
```
✅ Desuscrito de X · 🗑️ Y correos antiguos a la papelera · ✋ Z bajas manuales (enlaces abajo)
```
Las bajas tardan hasta 2 días en hacerse efectivas en algunos remitentes: dilo.
