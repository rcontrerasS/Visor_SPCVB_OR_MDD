# Visor SPCVB – Muestra OR Madre de Dios

Visor web de los 8 suministros seleccionados en `Muestra SPCVB_ELSE_T1_202601_OR MDD.xlsx`.

## Qué incluye

- Los 8 suministros de la muestra.
- Coordenadas de los puntos tomadas del archivo geográfico `SUMINISTRO Y RU(7).kml`.
- Búsqueda por suministro, razón social o dirección.
- Vista Calles / Satélite.
- Botón **Mi ubicación** usando el GPS del navegador.
- Ruta desde tu ubicación hasta un suministro seleccionado.
- Ruta sugerida para visitar los 8 suministros, ordenada por proximidad desde tu ubicación.
- Botón para abrir navegación en Google Maps.
- Datos de alimentador, etiqueta de subestación y cantidad de lotes.

## Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub.
2. Sube **todos los archivos de esta carpeta a la raíz del repositorio**.
3. En GitHub abre **Settings > Pages**.
4. En **Build and deployment**, selecciona **Deploy from a branch**.
5. Selecciona la rama `main` y la carpeta `/ (root)`.
6. Guarda. GitHub mostrará la dirección pública del visor.

GitHub Pages usa HTTPS, por lo que el botón **Mi ubicación** puede solicitar el GPS del teléfono o computadora.

## Uso en campo

1. Abre el visor desde GitHub Pages.
2. Pulsa **Mi ubicación** y acepta el permiso.
3. Selecciona un suministro en la lista.
4. Pulsa **Ruta** para dibujar la ruta vial dentro del visor.
5. Si deseas navegación giro a giro, pulsa **Google Maps**.

## Servicios en línea

- Mapa base: Esri.
- Cálculo de ruta vial: servicio público OSRM/OpenStreetMap.
- Navegación externa opcional: Google Maps.

Por lo anterior, el visor necesita conexión a Internet para mapa base y cálculo de rutas.

## Nota sobre coordenadas

El visor prioriza las coordenadas del KML `SUMINISTRO Y RU(7).kml`, que contiene el punto geográfico individual de cada suministro. El Excel de la muestra también contiene campos UTM, pero en algunos registros no coinciden exactamente con el punto individual del KML.


## Versión 2 – mejora de mapa y zoom

Esta versión usa **OpenStreetMap** para la capa Calles y **Esri** para Satélite.

- Calles permite acercamiento hasta zoom 19.
- Se evita el problema de la capa anterior que podía mostrar `Map data not yet available`.
- Si una tesela de OpenStreetMap no carga en niveles bajos/medios, el visor intenta Esri como respaldo.
- El GPS debe usarse desde GitHub Pages (HTTPS) para una mejor compatibilidad con navegadores móviles.


## Versión 3 – modo robusto para GitHub Pages

Esta versión elimina la carga directa de `tile.openstreetmap.org`, que podía devolver error 403 al abrir el visor.

### Mapa
- **Calles:** Esri World Street Map.
- **Fallback:** Esri World Topographic Map.
- **Satélite:** Esri World Imagery.
- **Zoom visual:** hasta nivel 19.
- **Overzoom:** para Calles, el servidor se consulta como máximo a zoom 16 y los niveles 17–19 se amplían localmente. Esto evita solicitar teselas que pueden no existir o devolver “Map data not yet available”.

### GPS
El botón **Mi ubicación** debe usarse preferentemente desde la URL de GitHub Pages (`https://...`), no desde un archivo local `file:///`.

### Rutas
El visor intenta calcular rutas mediante el servicio público OSRM. Si el servicio no responde, muestra una línea directa de referencia y siempre mantiene disponible el botón **Google Maps** para navegación.

### Publicación
Sube todos los archivos de este ZIP a la raíz del repositorio y activa:

`Settings > Pages > Deploy from a branch > main > / (root)`
