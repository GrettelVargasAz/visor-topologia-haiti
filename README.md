# 🌾 Visor con los polígonos correspondientes a Fincas identificadas en campo para el GEF-6 

**Mapa interactivo para que cualquier persona, sin conocimientos de GIS, entienda de un vistazo el estado real de los polígonos del proyecto GEF-6 en Mont-Organisé, Haití — y ayude a tomar mejores decisiones.**

No requiere instalar nada. Funciona en cualquier navegador, computadora o celular.

---

## 🎯 ¿Por qué existe este visor?

De **651 parcelas** digitalizadas para el proyecto, un diagnóstico técnico encontró que **el 66% tiene al menos un problema geométrico** — la mayoría originado por un solo error de proceso: una comuna completa (Mont-Organisé) se cargó **dos veces** al combinar las capas de origen.

Este visor traduce ese diagnóstico técnico (hecho en ArcGIS Pro) a un mapa que **cualquiera puede explorar sin capacitación previa**, para apoyar la toma de decisiones sobre qué corregir primero.

## ✨ Qué puedes hacer con él

| Función | Descripción |
|---|---|
| 🎨 **Colores por tipo de error** | Cada combinación de errores (duplicado, superpuesto, multiparte, muesca) tiene su propio color, calculado automáticamente |
| 🔍 **Filtros independientes** | Activa o desactiva cada categoría de error por separado, y combínalas como quieras |
| 🏘️ **Navegación por comuna** | Pestañas arriba del mapa para saltar directo a Carice, Mont-Organisé, Vallières, Sainte-Suzanne o Plaine-du-Nord |
| ⚠️ **Comuna incorrecta** | Resalta los 142 polígonos cuya geometría no coincide con la comuna que declara su propio atributo |
| 🗺️ **Límites administrativos** | Superpón los límites oficiales de comuna como referencia visual |
| 🛰️ **Calles o satélite** | Cambia el mapa base según lo que necesites ver |
| 📊 **Resumen por comuna** | Tabla en vivo con el total, los que están OK, y el % de error de cada comuna |
| 🌐 **Español / English** | Toda la interfaz cambia de idioma con un clic |
| 📱 **Responsive** | Se adapta a celular con un menú colapsable |

## 🚦 Cómo leer los colores

- 🟢 **Verde** — sin errores, confiable
- 🟣 **Morado** — geometría duplicada exacta
- 🟠 **Naranja/rojo** — superposición con otra parcela (más intenso = más parcelas encimadas)
- 🌸 **Magenta** — polígono multiparte
- 🟡 **Dorado, borde punteado** — muesca o aguja sospechosa en el borde

> Un mismo polígono puede tener varios errores a la vez. Haz clic en cualquiera para ver su combinación exacta.

## 📂 Estructura del repositorio

```
visor-topologia/
├── index.html                          ← el visor (listo para usar)
├── README.md                           ← este archivo
└── data/
    ├── errores_topologia.geojson       ← capa de diagnóstico (ArcGIS Pro)
    └── limites_admin.geojson           ← límites de comuna (opcional)
```

## 🔄 Cómo actualizar los datos

Cada vez que se corrija algo en la capa original (ArcGIS Pro), hay que volver a exportar y reemplazar el `.geojson`:

```python
import arcpy

out_fc = r"C:\Users\GRETTEL\OneDrive\Desktop\Haiti\Topologia\Reporte_Errores.gdb\Errores_Topologia"
out_geojson = r"C:\Users\GRETTEL\OneDrive\Desktop\Haiti\Topologia\GeoJSON_export\errores_topologia.geojson"

arcpy.conversion.FeaturesToJSON(
    out_fc, out_geojson,
    "NOT_FORMATTED",
    geoJSON="GEOJSON",
    outputToWGS84="WGS84"
)
```

Luego sube ese archivo a `data/errores_topologia.geojson` en GitHub (Add file → Upload files es más confiable que copiar/pegar texto, ya que el archivo pesa más de 1 MB).

## 🚀 Publicar en GitHub Pages

1. Sube todo el contenido de esta carpeta a un repositorio público
2. **Settings → Pages** → Source: rama `main`, carpeta `/ (root)`
3. En 1–2 minutos tu visor estará en `https://tu-usuario.github.io/tu-repo/`

## 🧪 Probarlo en tu computadora antes de publicar

Los navegadores bloquean `fetch()` de archivos locales abiertos con doble clic (`file://`). Usa un servidor local:

```bash
cd visor-topologia
python -m http.server 8000
```

Y abre `http://localhost:8000` (no `file://`).

## 🛠️ Hecho con

[Leaflet](https://leafletjs.com/) · datos de [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro) · mapas base de OpenStreetMap / Esri / Google Maps

---

**Desarrollado por Grettel Vargas** · Proyecto GEF-6, Haití

