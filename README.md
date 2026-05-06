# Firmas de Correo

> Repositorio: https://github.com/MariaSanchezFernandez/FirmasCorreo

Firmas HTML para clientes de correo (Gmail, Outlook, Apple Mail).

## Firmas disponibles

| Persona | Empresa | Archivo |
|---|---|---|
| Estefanía Ureña | Fundación Cleardent | `index.html` |
| Amaia López | The Cherry Health | `cherry-con-foto.html` |
| Jesús Rayo | The Cherry Health | `cherry-sin-foto.html` |
| Mª Luisa Quesada | Alynea | `alynea.html` |
| Dirección Advance | Advance | `advance.html` |

## Estructura de assets

```
assets/                     ← Fundación Cleardent
assets-cherry-foto/         ← The Cherry Health (con foto)
assets-cherry/              ← The Cherry Health (sin foto)
assets-alynea/              ← Alynea
assets-advance/             ← Advance
logos/                      ← Logos compartidos
```

## Cómo añadir la firma en Gmail

1. Abre el HTML en Chrome
2. Selecciona todo: `Ctrl + A`
3. Copia: `Ctrl + C`
4. Gmail → ⚙️ Configuración → Ver toda la configuración → General → Firma
5. Crea una nueva firma y pega: `Ctrl + V`
6. Guarda los cambios

> Las imágenes se cargan desde GitHub (raw.githubusercontent.com), por lo que funcionan directamente en Gmail sin servidor propio.

## Notas técnicas

- **Desktop** (≥ 500px): tabla de 612px, compatible con Outlook.
- **Móvil** (< 500px): layout apilado activado por media query.
- Los fondos genéricos (`fondo_cherry_confoto.png`, `fondo_cherry_sinfoto.png`) se reutilizan entre personas — solo cambia la foto y los datos de texto.

## Añadir una nueva firma

1. Duplica el HTML más similar al perfil de la persona
2. Añade la foto en la carpeta `assets-*` correspondiente con el nombre `foto_NombrePersona.png`
3. Actualiza nombre, cargo, email, teléfono en el HTML
4. Actualiza las URLs de las imágenes apuntando al nuevo archivo
5. Añade la entrada en la tabla de este README
