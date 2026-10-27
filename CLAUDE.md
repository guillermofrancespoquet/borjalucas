# Borja Lucas – Contexto del repo

Planificación nutricional de un cliente de Guille (NutriLogos). **Repo público** (GitHub Pages). Este repo es la fuente de verdad del plan; se gestiona desde aquí, no desde el chat.

## Estado
**Borrador** previo a la primera consulta (28/10/2026). Aún no hay datos de báscula, antropometría ni consulta: el menú, las cantidades, los objetivos nutricionales, la lista de compra y las recetas están como "Por definir". Se rellenan tras la consulta.

## Idioma
- Todo en **español** (plan, notas, commits). El plan se redacta en segunda persona ("tu recuperación", "tus gustos").

## Archivos
```
index.html                                    plan del cliente (HTML autónomo, estilo app NutriLogos); se llama index.html para que Pages lo publique
Logo.png                                      icono (apple-touch-icon)
_headers.txt                                  cabeceras de caché (no-cache)
INSTRUCCIONES_NUTRILOGOS_v6.0.txt            guía unificada: estructura, estilo, datos, proceso y checklist
CLAUDE.md                                     este archivo
```
- `index.html` = plan ya en estilo app (sin versión aparte ni sufijo `_app`).

## Estructura de `index.html`
Orden: h1 + subtítulo → Objetivo → Impresiones del profesional → Menú semanal de un vistazo (`#printArea`) → Menú desarrollado por días → Lista de compra semanal → Recetas.
- Datos en JS: `days[]` (7 días; cada comida con `type`, `time`, `name`, `desc` separado por `\n`, `short`, `note`, `libre`), `shopCategories[]` y `recetas[]`.
- La tabla semanal se genera desde `short` de cada comida (`buildSummary()`); si cambia una comida, actualizar `short`, `desc`, `note` **y** la lista de compra.
- Recetas: acordeón al final (`recetas[]`, `buildRecetas()`). Ahora hay una receta de relleno; sustituir o retirar la sección si no aplica.
- Sin suplementación ni batch cooking por ahora (los hooks existen en el JS pero no se usan).
- Fuera del HTML (la app ya los muestra): descripción del cliente, perfil con métricas y próxima revisión.

## Estilo
- Reglas, datos y checklist: `INSTRUCCIONES_NUTRILOGOS_v6.0.txt` (sustituye a la plantilla v5.0 y al estilo app v1.0). El CSS y el JS están dentro de `index.html`.
- Tras cualquier cambio: comprobar JS con `node --check` (extrayendo el `<script>`), revisar en móvil (~430 px) y escritorio, y que el `@media print` siga intacto.

## Contexto del cliente (dado por Guille)
- Juega a fútbol en 3RFEF, CD Soneja. Ha empezado la temporada lesionado (pubalgia) y hace trabajo aparte de recuperación.
- Objetivo: recomposición corporal y hábitos sostenibles, útiles en la recuperación y en el día a día. Según él, el peso y la composición corporal "se le están yendo de las manos".
- Pendiente de la consulta: datos, gustos, aversiones, horarios, estructura de comidas (ahora D, C, Me, Ce de forma provisional), objetivo energético y de macros, y si hace falta suplementación o recetas.

## Perfil máster (a rellenar tras la primera consulta)
Documento de referencia del cliente. Rellenar con los datos reales; la guía v6.0 (Sección 5) indica qué recoger.
- **Descripción:** sexo · edad · talla · peso. Contexto: futbolista, CD Soneja (3RFEF), lesionado por pubalgia. Pendiente: profesión / situación vital.
- **Hábitos:** tabaco · alcohol · sueño → *por definir*.
- **Aversiones / exclusiones:** *por definir*.
- **Valoración inicial** (fecha, profesional): peso, IMC, talla / envergadura, % masa grasa, % masa muscular, LBM, TMB, ratio cintura / cadera → *por definir*.
- **Antropometría:** pliegues (Σ6, Σ8) y perímetros → *por definir*.
- **Bioimpedancia:** agua, proteína, masa ósea, masa grasa, músculo esquelético, grasa visceral → *por definir*.
- **Somatotipo:** *por definir*.
- **Próxima revisión:** *por definir*.

## Privacidad (repo público)
- Todo lo que está aquí es público, **incluido este `CLAUDE.md`**.
- Decisión de Guille: este archivo es el **perfil máster** del cliente. Ahí van la descripción del cliente y el perfil con métricas (composición corporal, antropometría, bioimpedancia, hábitos, aversiones), aunque el repo sea público.
- Siguen **fuera del repo** las analíticas, los hallazgos fuera del ámbito nutricional y las notas internas sensibles; salvo que Guille diga lo contrario, no se escriben aquí. No subir PDFs de pruebas.
- Antes de subir cualquier archivo nuevo, pensar si se publicará por Pages.
- Guille ha decidido mantener en `index.html` la información del cliente que él mismo ha aportado (lesión, club, objetivo).

> ⚠️ **RECORDATORIO (privacidad):** revisar con Guille, cuando lleguen los datos de la primera consulta, si el perfil máster seguirá en este repo público o se pasa a un lugar privado. Cuando se decida, borrar este aviso.

## Reglas de trabajo
- No renombrar archivos del cliente de forma unilateral; si falla un enlace, pedir primero la URL en vivo de GitHub Pages.
- Ramas: desarrollar en la rama asignada a la sesión; no tocar `main` directamente.
- PR y merge: se puede abrir PR siempre que haga falta; **fusionar solo cuando Guille lo diga** en el chat.
