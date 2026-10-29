# Borja Lucas – Contexto del repo

Planificación nutricional de un cliente de Guille (NutriLogos). **Repo público** (GitHub Pages). Este repo es la fuente de verdad del plan; se gestiona desde aquí, no desde el chat.

## Estado
**Primera versión del plan (v1)**, hecha tras la valoración del 28/10/2026 (bioimpedancia + antropometría) y el cálculo energético del 29/10/2026. Menú de 7 días con cantidades, lista de compra y 3 recetas, pendiente de ajustar con el cliente y de ver qué desayunos le funcionan mejor.

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
- Recetas: acordeón al final (`recetas[]`, `buildRecetas()`). Ahora hay 5: overnight de avena, salteado de tofu marinado con cuscús integral, lentejas estofadas con pollo y dos opciones (tortitas de avena y plátano para el desayuno del domingo; ensalada de cuscús con gazpacho y tofu marinado para la cena del martes).
- Sin suplementación ni batch cooking por ahora (los hooks existen en el JS pero no se usan).
- Fuera del HTML (la app ya los muestra): descripción del cliente, perfil con métricas y próxima revisión.

## Estilo
- Reglas, datos y checklist: `INSTRUCCIONES_NUTRILOGOS_v6.0.txt` (sustituye a la plantilla v5.0 y al estilo app v1.0). El CSS y el JS están dentro de `index.html`.
- Tras cualquier cambio: comprobar JS con `node --check` (extrayendo el `<script>`), revisar en móvil (~430 px) y escritorio, y que el `@media print` siga intacto.

## Contexto del cliente (dado por Guille)
- Juega a fútbol en 3RFEF, CD Soneja. Ha empezado la temporada lesionado (pubalgia) y hace trabajo aparte de recuperación.
- Su "entrenamiento" actual es readaptación de la pubalgia (ejercicios de fuerza + fisioterapia, de ≈ 1 hora cada sesión; la duración exacta no se conoce) los **lunes, miércoles, jueves y viernes**, más algo de actividad física el sábado. Es lo que él llama "fútbol 5 veces por semana" en el cuestionario.
- Objetivo: recomposición corporal y hábitos sostenibles. Meta concreta de este primer mes: **bajar de 94,8 kg a unos 92,5 kg**, reduciendo grasa y conservando músculo.
- Según él, el peso y la composición corporal "se le están yendo de las manos".

## Perfil máster (cuestionarios del 27/10/2026 y valoración del 28/10/2026)
Documento de referencia del cliente. La guía v6.0 (Sección 5) indica qué recoger.
- **Descripción:** hombre · 25 años · 1,93 m · 94,8 kg. Futbolista (CD Soneja, 3RFEF), lesionado por pubalgia. Ocupación: conserje (cubriendo una baja), con semanas alternas de 7:30–14:00 y de 8:00–15:15.
- **Salud (autodeclarada):** sin enfermedad diagnosticada, medicación, alergias ni intolerancias, y sin problemas digestivos. Lesión actual: pubalgia (fase y tratamiento *por definir*).
- **Hábitos de alimentación:**
  - Omnívoro, nunca ha seguido una dieta. 5 comidas al día y a veces come entre horas. Antojos o hambre emocional a veces. Hidratación 6/10.
  - Horarios habituales: desayuno 7:00–7:15 · almuerzo 11:00 · comida 15:00–15:30 · merienda 17:30 · cena 21:30.
  - Qué se prepara cuándo: desayuno y merienda los prepara él (preparación previa o en el momento); el almuerzo tiene que ser transportable (trabaja por la mañana); comida y cena son en casa.
  - En días de trabajo suele comprar el almuerzo en el Mercadona o el Consum.
- **Cocina y logística:** a él le gusta poco cocinar. Más de 45 min disponibles. Horno y microondas (sin air fryer ni Thermomix).
- **Actividad física:** readaptación de la pubalgia (fuerza + fisio, ≈ 1 h por sesión) L, X, J, V + actividad ligera el sábado. Nivel de actividad 5/5 según el cuestionario (antes de la lesión).
- **Objetivos (cuestionario):** perder grasa y mejorar el rendimiento deportivo. Sin fecha ni evento. Mayor reto según él: perder grasa.
- **Aversiones / preferencias:** ninguna por el momento; se irán contemplando según avance el plan.
- **Tabaco · alcohol · sueño:** no fuma; alcohol ocasional y poco; duerme entre 7 y 8 horas.

### Valoración inicial (28/10/2026)
- **Antropometría:** peso 94,8 kg · talla 193,0 cm · envergadura 195,0 cm (relativa 1,01) · talla sentado 100,5 cm (índice córmico 0,52, metriocórmico) · IMC 25,4 (sobrepeso I).
  - Pliegues (mm): tríceps 12,0 · subescapular 11,5 · bíceps 4,5 · cresta ilíaca 19,0 · supraespinal 8,0 · abdominal 20,5 · muslo 20,0 · pierna 7,5. **Σ6 = 79,5 · Σ8 = 103,0**.
  - Perímetros (cm): brazo relajado 32,3 / contraído 34,5 · cintura 90,6 · cadera 104,5 · muslo 60,6 · pierna 40,1. Diámetros (cm): húmero 7,3 · biestiloideo 6,2 · fémur 10,9. **Ratio cintura/cadera 0,87** (riesgo cardiovascular bajo).
  - Composición: masa grasa (Durnin-Womersley) **18,1 % · 17,17 kg** · tejido adiposo (Ross-Kerr) 27,4 % · 25,98 kg · masa muscular (Lee) 39,9 % · 37,81 kg · masa ósea (Rocha) 16,5 % · 15,62 kg · masa residual 16,2 % · 15,34 kg · índice músculo/óseo 2,42. Áreas musculares transversales: brazo 64,8 · muslo 234,8 · pierna 113,4 cm².
- **Bioimpedancia (Arboleaf, 28/10/2026 15:25; dato complementario, se usa con cautela):** peso 94,75 kg · agua 59 L (rango 47,4–61,6) · masa ósea 4,09 kg · masa grasa 12,98 kg · **PBF 13,7 %** · masa libre de grasa 81,8 kg · músculo esquelético 52,9 kg (rango 35,13–42,93) · grasa visceral 8 · índice de grasa subcutánea 11,4 % · BMR 2136 kcal · edad metabólica 25 años · puntuación de condición física 81,2/100. Equilibrio muscular: ligeramente desequilibrado (superior, inferior y superior-inferior). Fuerza superior e inferior normal.
- **Nota de método:** la antropometría (18,1 %) es la referencia; la bioimpedancia (13,7 %) es complementaria. Son métodos distintos y no comparables entre sí: en cada revisión se compara siempre con el mismo. El cálculo energético usa la masa libre de grasa de la antropometría (77,6 kg).
- **Somatotipo:** *por definir*.
- **Próxima revisión:** *por definir*.

## Criterios nutricionales (decididos con Guille)
- **Enfoque:** basado en evidencia; cuanto más vegetal e integral, mejor. Prioridad a integrales, legumbres, frutos secos, fruta y verdura.
- **Cálculo energético (NutriLogos, 29/10/2026):** BMR 2034 kcal (1769–2298) · TDEE 3152 kcal · **objetivo 2679 kcal/día** (déficit ≈ 470 kcal; ritmo ≈ 0,45 % del peso por semana) · **P 152 g (23 %) · G 74 g (25 %) · HC 351 g (52 %)** · masa libre de grasa 77,6 kg. La proteína equivale a 1,6 g/kg de peso y 2,0 g/kg de masa libre de grasa.
- **Menú v1 (cálculo con tablas estándar, orientativo):** media semanal ≈ 2688 kcal · P ≈ 151 g · G ≈ 77 g · HC ≈ 350 g; cada día queda a ±3 % de las kcal objetivo. Es una estimación.
- **Comidas (5):** desayuno 7:00 (lo prepara él) · almuerzo 11:00 (transportable) · comida 15:00 (en casa) · merienda 17:30 (pre-entreno, portable) · cena 21:30 (en casa).
- **Cantidades y medidas:** gramos con su equivalente en medidas caseras (vasos, tazas, cucharadas, cucharaditas, puñados, piezas). La fruta se da en piezas, sin pesar, y cuantas más, mejor (fuente de fibra, vitaminas y minerales: a más fruta entera en la planificación, mejor para la salud). En la tabla semanal aparece como "+ fruta" al final de `short` en las comidas que la llevan.
- **Opciones puntuales** (recetas de NutriLogos ajustadas a su plan, no cambian el cálculo base): desayuno del domingo = tortitas de avena y plátano (plátano 120 g, 2 huevos, avena 30 g; con frutos rojos, fruta y café con soja ≈ 540 kcal, P 28 g); cena del martes = ensalada de cuscús con gazpacho y tofu marinado (cuscús integral 90 g, gazpacho 150 ml, tofu 200 g, sin AOVE añadido; con la fruta ≈ 760 kcal, P 42 g). Con cada opción el día queda a ±2 % de las kcal objetivo.
- **Tofu:** siempre marinado (soja baja en sal, limón, ajo y especias) para mejorar la textura; se introduce poco a poco.
- **Desayunos:** se intercalan overnight de avena (avena, bebida vegetal o leche semi/desnatada, mix de semillas, frutos rojos o fruta, topping en días de más calorías) y tostadas integrales (hummus con aguacate, tomate o pimiento; o mantequilla de cacahuete o mermelada con plátano) para ver qué funciona mejor este mes.
- **Almuerzo:** casi igual cada día: fruta con frutos secos, a veces barrita de dátiles y frutos secos (tipo Nakd o Better) y algún sándwich puntual de pan integral con fiambre de pavo.
- **Comida y cena:** una ración de carbohidrato integral o de alta fibra (patata, boniato, quinoa, cuscús integral, arroz integral), una de proteína (pollo y pavo, pescado blanco, pescado azul y, como última opción, salmón; tofu poco a poco), grasas de AOVE, frutos secos y olivas, y verduras con ensalada o fruta de postre. Platos elaborados (guisos, sopas) alternados con otros rápidos.
- **Legumbres:** al menos 3 días por semana (en el menú v1, 4: lunes, miércoles, viernes y domingo en la comida).
- **Merienda:** fruta como plátano con tortitas de maíz o arroz antes de entrenar; algún día zumo de naranja.
- **Cantidades:** pesos en crudo salvo que se indique, para poder pasárselos a quien cocina.
- **Pendiente:** aversiones que vayan surgiendo y ajuste de cantidades según evolución.

## Privacidad (repo público)
- Todo lo que está aquí es público, **incluido este `CLAUDE.md`**.
- Decisión de Guille: este archivo es el **perfil máster** del cliente. Ahí van la descripción del cliente y el perfil con métricas (composición corporal, antropometría, bioimpedancia, hábitos, aversiones), aunque el repo sea público.
- Siguen **fuera del repo** las analíticas, los hallazgos fuera del ámbito nutricional y las notas internas sensibles; salvo que Guille diga lo contrario, no se escriben aquí. No subir PDFs de pruebas.
- Antes de subir cualquier archivo nuevo, pensar si se publicará por Pages.
- Guille ha decidido mantener en `index.html` la información del cliente que él mismo ha aportado (lesión, club, objetivo).

> ⚠️ **RECORDATORIO (privacidad):** Guille ha decidido no tratar este tema hasta **noviembre de 2026**. Entonces, revisar con él si el perfil máster sigue en este repo público o pasa a un lugar privado. Dato a tener en cuenta: el consentimiento firmado por el cliente (27/10/2026) dice que sus datos "no serán cedidos a terceros salvo obligación legal o consentimiento adicional"; publicarlos puede requerir su permiso expreso. Cuando se decida, borrar este aviso.

## Reglas de trabajo
- No renombrar archivos del cliente de forma unilateral; si falla un enlace, pedir primero la URL en vivo de GitHub Pages.
- Ramas: desarrollar en la rama asignada a la sesión; no tocar `main` directamente.
- PR y merge: se puede abrir PR siempre que haga falta; **fusionar solo cuando Guille lo diga** en el chat.
