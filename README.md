# Firmas de Correo

> Repositorio: https://github.com/MariaSanchezFernandez/FirmasCorreo

Firmas HTML para clientes de correo (Gmail, Outlook, Apple Mail).

---

## Firmas disponibles

| Empresa | Carpeta |
|---|---|
| Cleardent Personal | `cleardent/personal/` |
| Cleardent Clínicas | `cleardent/clinicas/` |
| Cleardent Advance | `cleardent/advance/` |
| Cherry Health | `cherry/` |
| Alynea | `alynea/` |
| Fundación Cleardent | `fundacion/` |

---

## Estructura del repositorio

```
cleardent/
├── personal/          → firmas individuales con foto
├── clinicas/          → firmas por clínica
└── advance/           → firma Advance

cherry/                → firmas Cherry Health (con y sin foto)
alynea/                → firmas Alynea
fundacion/             → firmas Fundación Cleardent

assets/
├── cleardent/
│   ├── personal/      → fondos y fotos Cleardent Personal
│   ├── nerja/         → fondo Cleardent Clínica Nerja
│   └── advance/       → logo y decorativos Advance
├── cherry/            → fondos y fotos Cherry Health
├── alynea/            → fondo e iconos Alynea
└── fundacion/         → logo, fondo y fotos Fundación

inbox/                 → carpeta para subir fotos nuevas (se vacía automáticamente)
```

---

## Cómo añadir una nueva firma

Usa el comando `/nueva-firma` desde Claude Code. Te pedirá los datos de una sola vez y creará el archivo, renombrará la foto y subirá todo a GitHub automáticamente.

Para la foto: arrástrala a la carpeta **`inbox/`** antes de ejecutar el comando. La foto debe estar **recortada sin espacios transparentes en los laterales**.

---

## Cómo instalar la firma en Gmail

1. Abre el HTML en Chrome
2. Selecciona todo: `Ctrl + A`
3. Copia: `Ctrl + C`
4. Gmail → ⚙️ Configuración → Ver toda la configuración → General → Firma
5. Crea una nueva firma y pega: `Ctrl + V`
6. Guarda los cambios

> Las imágenes se cargan desde GitHub (`raw.githubusercontent.com`), funcionan directamente sin servidor propio.

---

## Notas técnicas

- Tabla de **612px**, compatible con Outlook (VML), Gmail y Apple Mail
- Imágenes optimizadas a **2× el tamaño de visualización** para pantallas retina
- Todos los enlaces (email, teléfono, web) son clicables
- Colores y fuentes específicos por empresa, no mezclar entre plantillas
