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
6. **Foto** — arrastra el archivo a la carpeta **`inbox/`** del proyecto. *(Cualquier formato; preferiblemente en **formato vertical/retrato** para que quede bien en la firma.)*

*Si no tienes foto ahora, escribe "sin foto". La dirección la pongo automáticamente según la empresa, avísame solo si es diferente a la estándar.*

---

Una vez el usuario responda, **ejecuta todo sin pedir más confirmaciones**:

### Procesa los datos
- Teléfono: formatea siempre como `+34 XXX XXX XXX` en texto y `tel:+34XXXXXXXXX` en href
- Nombre de archivo: `nombre-apellido.html` (minúsculas, sin tildes, con guiones)
- Nombre de foto: `foto-nombre-apellido.png` (igual, ignorando el nombre original del archivo)
- Dirección por defecto según empresa (no preguntes):
  - Cleardent / Advance / Alynea / Cherry: `Avenida de la Innovación, Manzana 21A, Edificio Cleardent, Geolit, Mengíbar, Jaén`
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
2. **Redimensiona la foto** usando el bloque PowerShell correspondiente a la empresa elegida:

#### Cleardent Personal — fit 360×400px, anclado abajo
La foto se escala para caber dentro del canvas (sin recorte). El padding transparente queda arriba; la persona siempre toca el borde inferior de la firma.
```powershell
Add-Type -AssemblyName System.Drawing
$img = [System.Drawing.Image]::FromFile($fotoPath)
$targetW = 360; $targetH = 400
$scale = [Math]::Min($targetW / $img.Width, $targetH / $img.Height)
$resW = [int]($img.Width * $scale); $resH = [int]($img.Height * $scale)
$canvas = New-Object System.Drawing.Bitmap($targetW, $targetH)
$g = [System.Drawing.Graphics]::FromImage($canvas)
$g.Clear([System.Drawing.Color]::Transparent)
$g.InterpolationMode = [System.Drawing.Drawing2D.InterpolationMode]::HighQualityBicubic
$g.SmoothingMode = [System.Drawing.Drawing2D.SmoothingMode]::HighQuality
$offsetX = [int](($targetW - $resW) / 2)
$offsetY = $targetH - $resH
$g.DrawImage($img, $offsetX, $offsetY, $resW, $resH)
$g.Dispose(); $img.Dispose()
$canvas.Save($fotoPath, [System.Drawing.Imaging.ImageFormat]::Png)
$canvas.Dispose()
```

#### Cherry con foto — cover 344×342px, recorte centrado, anclado arriba
Canvas fijo que ocupa exactamente la columna de foto (172px × 171px a 2x). La columna tiene 180px de alto con 9px de padding-top, así que la imagen se muestra a 171px — usar 344×342 evita que la firma se estire. La escala usa `Max` para cubrir (nunca deja huecos); el exceso se recorta centrado en X y desde arriba en Y (la cara siempre aparece).
```powershell
Add-Type -AssemblyName System.Drawing
$img = [System.Drawing.Image]::FromFile($fotoPath)
$targetW = 344; $targetH = 342
$scale = [Math]::Max($targetW / $img.Width, $targetH / $img.Height)
$resW = [int]($img.Width * $scale); $resH = [int]($img.Height * $scale)
$canvas = New-Object System.Drawing.Bitmap($targetW, $targetH)
$g = [System.Drawing.Graphics]::FromImage($canvas)
$g.Clear([System.Drawing.Color]::Transparent)
$g.InterpolationMode = [System.Drawing.Drawing2D.InterpolationMode]::HighQualityBicubic
$g.SmoothingMode = [System.Drawing.Drawing2D.SmoothingMode]::HighQuality
$offsetX = -[int](($resW - $targetW) / 2)
$offsetY = 0
$g.DrawImage($img, $offsetX, $offsetY, $resW, $resH)
$g.Dispose(); $img.Dispose()
$canvas.Save($fotoPath, [System.Drawing.Imaging.ImageFormat]::Png)
$canvas.Dispose()
```

#### Fundación — escala por alto a 400px, ancho proporcional
La foto se renderiza con `height:200px; width:auto` en el HTML, así que solo importa la proporción. Sin canvas fijo.
```powershell
Add-Type -AssemblyName System.Drawing
$img = [System.Drawing.Image]::FromFile($fotoPath)
$targetH = 400
$targetW = [int]($img.Width * $targetH / $img.Height)
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
