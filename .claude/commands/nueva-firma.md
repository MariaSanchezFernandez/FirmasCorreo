# Crear nueva firma de correo

Eres un asistente que crea firmas de correo HTML para el repositorio FirmasCorreo. Sigue estos pasos en orden, preguntando al usuario interactivamente.

---

## PASO 1 — Empresa

Pregunta: **¿Para qué empresa es la firma?**

Opciones:
1. Cleardent Personal (persona individual con foto)
2. Cleardent Clínica (clínica sin foto de persona)
3. Cherry Health
4. Alynea
5. Advance
6. Fundación Cleardent

Guarda la elección para los pasos siguientes.

Si elige **Cherry Health**, pregunta a continuación: **¿La firma lleva foto de la persona?** (sí / no). Según la respuesta, usarás la plantilla con foto o sin foto.

---

## PASO 2 — Datos básicos

Pide al usuario los siguientes datos:

- **Nombre completo** (ej: María García López)
- **Cargo / puesto** (ej: Directora de Marketing)
- **Email** (ej: maria.garcia@cleardent.es)
- **Teléfono** — pide solo los dígitos (ej: 611 222 333). Siempre formatea como `+34 XXX XXX XXX` en el texto visible y como `tel:+34XXXXXXXXX` en el href, independientemente de si el usuario incluye o no el prefijo.
- **Dirección** — muestra la dirección estándar de la empresa y pregunta si es diferente:
  - Cleardent / Advance / Alynea: `Avenida de la Innovación, Manzana 21A, Edificio Cleardent, Geolit, Mengíbar, Jaén 23620`
  - Cherry: `Avenida de la Innovación, Manzana 21A, Edificio Cleardent, Geolit, Mengíbar, Jaén 23620`
  - Fundación: `Avenida de la Innovación 2, Edificio Eureka, Planta 2 · Geolit, Mengíbar, Jaén · 23620`
  - Clínicas Cleardent: preguntar dirección de la clínica específica

---

## PASO 3 — Foto personal (solo si aplica)

Si la empresa elegida usa foto de persona (Cleardent Personal, Cherry Health con foto, Fundación Cleardent):

Pregunta: **¿Tienes una foto para adjuntar?**
- Si sí → pide que indique la ruta del archivo PNG en su equipo. **Independientemente del nombre original del archivo**, cópialo renombrándolo siempre como `foto-<nombre-apellido>.png` (minúsculas, guiones, sin tildes ni espacios). Guárdalo en `assets/<carpeta-empresa>/`.
- Si no → usa la foto de la persona de referencia como placeholder y avisa al usuario.

---

## PASO 4 — Generar el HTML

Usa como plantilla el HTML de referencia de esa empresa:

| Empresa | Plantilla |
|---|---|
| Cleardent Personal | `cleardent/personal/juan-antonio-perez.html` |
| Cleardent Clínica | `cleardent/clinicas/nerja.html` |
| Cherry Health con foto | `cherry/amaia-lopez.html` |
| Cherry Health sin foto | `cherry/jesus-rayo.html` |
| Alynea | `alynea/marisa-quesada.html` |
| Advance | `cleardent/advance/advance.html` |
| Fundación | `fundacion/estefania-urena.html` |

Lee la plantilla y reemplaza:
- Nombre completo
- Cargo
- Email (texto visible + href mailto:)
- Teléfono (texto visible + href tel: sin espacios)
- Dirección
- URL de la foto (si aplica) → nueva ruta en `assets/`
- Alt de la imagen con el nombre de la persona

Guarda el nuevo archivo con nombre `<nombre-apellido>.html` (minúsculas, guiones) en la misma carpeta que la plantilla.

---

## PASO 5 — Subir a GitHub

```bash
git add <ruta-html> <ruta-foto-si-existe>
git commit -m "Add firma <Nombre Apellido> (<Empresa>)"
git push origin main
```

Confirma al usuario que la firma está disponible en:
`https://raw.githubusercontent.com/MariaSanchezFernandez/FirmasCorreo/main/<ruta-del-html>`

---

## Reglas importantes

- Todos los enlaces (email, teléfono, web) deben ser clicables con `<a href>` y `style="text-decoration:none;color:heredado"`
- Respetar exactamente los colores y fuentes de la plantilla
- No modificar la estructura de tablas ni los estilos MSO/Outlook
- El nombre del archivo HTML y de la foto siempre en minúsculas con guiones, sin tildes ni caracteres especiales (ej: `ana-martinez-lopez.html`, `foto-ana-martinez-lopez.png`). Nunca uses el nombre original del archivo que proporcione el usuario — siempre renombra usando el nombre de la persona.
