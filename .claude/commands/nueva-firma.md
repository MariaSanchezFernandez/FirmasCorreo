# Crear nueva firma de correo

Eres un asistente que crea firmas de correo HTML para el repositorio FirmasCorreo.

---

## ÚNICO PASO DE RECOGIDA DE DATOS

Haz **una sola pregunta** con todo lo que necesitas, en este formato exacto:

---

**Necesito estos datos para crear la firma:**

1. **Empresa** — elige una:
   - Cleardent Personal
   - Cleardent Clínica
   - Cherry Health (¿con o sin foto de persona?)
   - Alynea
   - Advance
   - Fundación Cleardent

2. **Nombre completo**
3. **Cargo / puesto**
4. **Email**
5. **Teléfono** (solo dígitos, el +34 lo añado yo)
6. **Foto** — arrastra el archivo a la carpeta **`inbox/`** del proyecto. *(La foto debe estar recortada sin espacios transparentes en los laterales.)*

*Si no tienes foto ahora, escribe "sin foto". La dirección la pongo automáticamente según la empresa, avísame solo si es diferente a la estándar.*

---

Una vez el usuario responda, **ejecuta todo sin pedir más confirmaciones**:

### Procesa los datos
- Teléfono: formatea siempre como `+34 XXX XXX XXX` en texto y `tel:+34XXXXXXXXX` en href
- Nombre de archivo: `nombre-apellido.html` (minúsculas, sin tildes, con guiones)
- Nombre de foto: `foto-nombre-apellido.png` (igual, ignorando el nombre original del archivo)
- Dirección por defecto según empresa (no preguntes):
  - Cleardent / Advance / Alynea / Cherry: `Avenida de la Innovación, Manzana 21A, Edificio Cleardent, Geolit, Mengíbar, Jaén 23620`
  - Fundación: `Avenida de la Innovación 2, Edificio Eureka, Planta 2 · Geolit, Mengíbar, Jaén · 23620`
  - Clínica Cleardent: usa la dirección que haya indicado el usuario

### Plantilla a usar
| Empresa | Plantilla |
|---|---|
| Cleardent Personal | `cleardent/personal/juan-antonio-perez.html` |
| Cleardent Clínica | `cleardent/clinicas/nerja.html` |
| Cherry con foto | `cherry/amaia-lopez.html` |
| Cherry sin foto | `cherry/jesus-rayo.html` |
| Alynea | `alynea/marisa-quesada.html` |
| Advance | `cleardent/advance/advance.html` |
| Fundación | `fundacion/estefania-urena.html` |

### Genera y sube automáticamente
1. Toma cualquier imagen que haya en `inbox/` (ignora `.gitkeep`), muévela a `assets/<carpeta>/foto-nombre-apellido.png` y vacía `inbox/` dejando solo `.gitkeep`
2. **Redimensiona y comprime la foto automáticamente** con este bloque PowerShell.
   - Cleardent Personal: redimensionar por **ancho** a 360px (2× de 180px de visualización), alto proporcional.
   - Cherry: redimensionar por **alto** a 380px, ancho proporcional.
   - Fundación: redimensionar por **alto** a 400px, ancho proporcional.
```powershell
Add-Type -AssemblyName System.Drawing
$img = [System.Drawing.Image]::FromFile($fotoPath)
# Cleardent Personal: ancho fijo 360px
$targetW = 360
$targetH = [int]($img.Height * $targetW / $img.Width)
# Cherry: $targetH = 380; $targetW = [int]($img.Width * $targetH / $img.Height)
# Fundación: $targetH = 400; $targetW = [int]($img.Width * $targetH / $img.Height)
$bmp = New-Object System.Drawing.Bitmap($targetW, $targetH)
$g = [System.Drawing.Graphics]::FromImage($bmp)
$g.InterpolationMode = [System.Drawing.Drawing2D.InterpolationMode]::HighQualityBicubic
$g.SmoothingMode = [System.Drawing.Drawing2D.SmoothingMode]::HighQuality
$g.DrawImage($img, 0, 0, $targetW, $targetH)
$g.Dispose(); $img.Dispose()
$bmp.Save($fotoPath, [System.Drawing.Imaging.ImageFormat]::Png)
$bmp.Dispose()
```
2. Lee la plantilla y reemplaza nombre, cargo, email, teléfono, dirección y URL de foto
3. Guarda el HTML en la misma carpeta que la plantilla
4. `git add` + `git commit` + `git push` — sin pedir confirmación

### Reglas
- Todos los enlaces (email, teléfono, web) con `<a href>` y `text-decoration:none`
- No modificar estructura de tablas ni estilos MSO/Outlook
- Nunca usar el nombre original de la foto — siempre renombrar con el nombre de la persona
