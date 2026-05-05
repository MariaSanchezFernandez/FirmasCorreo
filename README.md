# Firmas de Correo · Fundación Cleardent

> Repositorio: https://github.com/Woodsearch/FirmasCorreo

Firmas HTML para clientes de correo (Gmail, Outlook, Apple Mail).

## Estructura

```
FirmasCorree/
├── index.html                        ← Firma activa
└── assets/
    ├── foto_EstefaniaUrena.png       ← Foto con fondo azul integrado
    ├── preview.png                   ← Captura de referencia visual
    └── logos/
        └── logo_fundaciones.png      ← Logo Fundación Cleardent
```

## Firmas disponibles

| Persona | Archivo |
|---|---|
| Estefanía Ureña | `index.html` |

## Cómo añadir la firma en Gmail

1. Abre `index.html` en Chrome
2. Selecciona todo: `Ctrl + A`
3. Copia: `Ctrl + C`
4. Gmail → ⚙️ Configuración → Ver toda la configuración → General → Firma
5. Crea una nueva firma y pega: `Ctrl + V`
6. Guarda los cambios

> Las imágenes se cargan desde GitHub (raw.githubusercontent.com), por lo que funcionan directamente en Gmail sin servidor propio.

## Notas técnicas

- **Desktop** (≥ 500px): tabla de 612px con 3 columnas, compatible con Outlook.
- **Móvil** (< 500px): layout apilado activado por media query. Outlook siempre muestra el desktop.
- El fondo azul forma parte de `foto_EstefaniaUrena.png`, por lo que Gmail no puede eliminarlo.

## Añadir una nueva firma

1. Duplica `index.html` con el nombre `index_NombrePersona.html`
2. Añade la foto con fondo azul en `assets/` con el nombre `foto_NombrePersona.png`
3. Actualiza los datos (nombre, cargo, email, teléfono) en el HTML
4. Actualiza las URLs de las imágenes apuntando al nuevo archivo
5. Añade la entrada en la tabla de firmas de este README
