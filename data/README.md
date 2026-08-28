# Visor de Topología — All_polys_UTM18_topology

Mapa interactivo para que colegas sin conocimientos de GIS puedan ver los
polígonos y sus errores de topología directamente en el navegador, sin
instalar nada.

## Estructura del repositorio

```
visor-topologia/
├── index.html                          <- el visor (ya está listo)
└── data/
    └── errores_topologia.geojson       <- TÚ debes copiar este archivo aquí
```

## Paso 1 — Consigue el archivo de datos

Ya lo generaste desde ArcGIS Pro en:
```
C:\Users\GRETTEL\OneDrive\Desktop\Haiti\Topologia\GeoJSON_export\errores_topologia.geojson
```
Cópialo dentro de la carpeta `data/` de este proyecto (mismo nombre exacto).

Si en el futuro quieres actualizar los datos, vuelve a correr en ArcGIS Pro:
```python
import arcpy, os
out_fc = r"C:\Users\GRETTEL\OneDrive\Desktop\Haiti\Topologia\Reporte_Errores.gdb\Errores_Topologia"
out_geojson = r"C:\Users\GRETTEL\OneDrive\Desktop\Haiti\Topologia\GeoJSON_export\errores_topologia.geojson"
arcpy.conversion.FeaturesToJSON(out_fc, out_geojson, "NOT_FORMATTED", geoJSON="GEOJSON", outputToWGS84="WGS84")
```
y vuelve a copiar el archivo sobre el anterior.

## Paso 2 — Crea el repositorio en GitHub

1. Entra a [github.com](https://github.com) → **New repository**.
2. Nómbralo, por ejemplo, `visor-topologia-haiti`.
3. Márcalo como **Public** (GitHub Pages gratuito requiere que sea público,
   salvo que tengas plan de pago con Pages privado).
4. No agregues README ni licencia automáticos (ya los traes).

## Paso 3 — Sube los archivos

Desde tu computadora, con Git instalado:

```bash
cd ruta\a\visor-topologia
git init
git add .
git commit -m "Visor inicial de topologia"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/visor-topologia-haiti.git
git push -u origin main
```

Si no usas la terminal, también puedes arrastrar los archivos directamente
en la página del repositorio en GitHub ("Add file" → "Upload files").

## Paso 4 — Activa GitHub Pages

1. En el repositorio, ve a **Settings** → **Pages**.
2. En "Source", selecciona la rama `main` y la carpeta `/ (root)`.
3. Guarda. En 1–2 minutos tu visor estará disponible en:
   ```
   https://TU-USUARIO.github.io/visor-topologia-haiti/
   ```
4. Comparte ese link con tus colegas — no necesitan cuenta de GitHub ni
   ArcGIS para verlo, solo un navegador.

## Qué pueden hacer tus colegas en el visor

- Ver todos los polígonos coloreados por tipo de error (verde = sin errores).
- Activar/desactivar categorías desde la barra lateral izquierda.
- Hacer clic en cualquier polígono para ver su detalle (duplicado,
  superposición, nivel, multiparte).
- Ver el conteo total y por categoría en la cabecera.
- Funciona en celular también (el menú se colapsa con el botón ☰).

## Actualizar el visor más adelante

Cada vez que cambies `index.html` o el `.geojson`, simplemente:
```bash
git add .
git commit -m "Actualizacion de datos"
git push
```
GitHub Pages se actualiza automáticamente en 1–2 minutos.
