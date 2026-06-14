# Visor del Mapa de Ecosistemas de Honduras (v02)

Este repositorio contiene una adaptación especializada de la plataforma SIG de código abierto **GeoLibre**, configurada como un visor web interactivo, serverless y de alto rendimiento para explorar la versión 0.2 del **Mapa de Ecosistemas de Honduras**.

El visor está localizado al español y está diseñado para cargarse de forma instantánea directamente desde **GitHub Pages** sin necesidad de bases de datos centralizadas o servidores de mapas dedicados (como GeoServer).

---

## 🗺️ Características de la Adaptación

Esta versión personalizada del visor incluye las siguientes adaptaciones clave:

1. **Filtro de Área Mínima (MMU) de 1 Hectárea:**
   El visor integra el mapa procesado con un filtro de conectividad de 8 vecinos para eliminar parches menores a 1 ha (11 píxeles de 30m). Esto limpia el ruido espacial (slivers) y optimiza las geometrías vectoriales.
2. **Taxonomía Jerárquica Oficial:**
   El visor y sus capas de atributos conservan la estructura completa de clasificación nacional:
   * **UNESCO-HN:** Clasificación fisionómico-estructural a Nivel 6.
   * **GET-UICN:** Tipología Global de Ecosistemas (Niveles 1, 2 y 3).
3. **Carga Automática de Proyecto:**
   Se modificó el cargador base de la aplicación ([useProjectUrlLoader.ts](file:///apps/geolibre-desktop/src/hooks/useProjectUrlLoader.ts)) para que, por defecto, lea el archivo de configuración del ecosistema nacional: `public/datos/proyecto.geolibre.json`.
4. **Branding y Traducción:**
   Localización completa al español en la página de inicio, menús principales y metadatos de las capas.
5. **Arquitectura Vectorial Distribuida (Serverless):**
   Para evitar el límite de 100 MB de GitHub y optimizar la velocidad en navegadores web, el mapa nacional de 175 clases se divide en archivos GeoPackage (`.gpkg`) específicos por clase. El visor carga dinámicamente solo las clases que el usuario activa en el panel lateral, ahorrando memoria y datos.

---

## 📁 Estructura del Visor en GeoLibre

* **[`apps/geolibre-desktop/index.html`](file:///apps/geolibre-desktop/index.html):** Página de inicio con branding y localización personalizada en español (*Visor de Ecosistemas de Honduras*).
* **[`apps/geolibre-desktop/public/datos/proyecto.geolibre.json`](file:///apps/geolibre-desktop/public/datos/proyecto.geolibre.json):** Configuración del mapa base, extensión espacial inicial (Honduras), estilos oficiales de la leyenda y rutas a las capas vectoriales.
* **[`apps/geolibre-desktop/public/datos/clases_separadas/`](file:///apps/geolibre-desktop/public/datos/clases_separadas/):** Directorio donde se almacenan las capas vectoriales en formato GeoPackage `.gpkg` correspondientes a cada una de las 175 clases.
* **[`.github/workflows/pages.yml`](file:///.github/workflows/pages.yml):** Pipeline de automatización en GitHub Actions. Compila el visor web y lo despliega directamente en la raíz de tu sitio de GitHub Pages de forma automática en cada actualización.

---

## 🚀 Ejecución en Entorno Local

Para ejecutar y probar el visor en tu máquina local:

### Requisitos Previos
* **Node.js** versión 22 o superior.

### Instrucciones
1. Abre tu terminal en la carpeta `GeoLibre/`:
   ```bash
   cd GeoLibre
   ```
2. Instala las dependencias del monorepo:
   ```bash
   npm install
   ```
3. Inicia el servidor de desarrollo local de Vite:
   ```bash
   npm run dev
   ```
4. Abre la dirección que te muestra la terminal en tu navegador (normalmente `http://localhost:5173/`).

---

## 🌐 Despliegue en GitHub Pages

Para publicar este visor de forma gratuita en tu cuenta de GitHub, sigue estos pasos:

### 1. Crear el Repositorio en GitHub
1. Entra a tu cuenta en [GitHub](https://github.com) y crea un nuevo repositorio público (ej: `visor-ecosistemas-honduras`).
2. Déjalo **completamente vacío** (no agregues README, ni .gitignore, ni licencia en el asistente).

### 2. Vincular y Subir el Código
Abre tu terminal en la carpeta `GeoLibre/` de tu máquina local y ejecuta:
```bash
# Cambiar el remoto original de GeoLibre a 'upstream' y añadir tu repositorio como 'origin'
git remote rename origin upstream
git remote add origin https://github.com/TU_USUARIO/TU_REPOSITORIO.git

# Agregar cambios, hacer commit y empujar la rama principal
git add .
git commit -m "Configurar visor de ecosistemas de Honduras para producción"
git branch -M main
git push -u origin main
```
*(Reemplaza `TU_USUARIO` y `TU_REPOSITORIO` por tus datos reales).*

### 3. Activar el Despliegue Automático
1. Ve a la pestaña **Settings** (Configuración) de tu repositorio en la web de GitHub.
2. En el menú de la izquierda, entra a **Pages**.
3. En la sección **Build and deployment -> Source**, selecciona **GitHub Actions**.

A partir de este momento, cada vez que hagas un cambio en los archivos del visor o en los datos y lo subas con `git push`, GitHub Actions compilará la aplicación y la publicará en la URL: `https://TU_USUARIO.github.io/TU_REPOSITORIO/`.

---

## ⚙️ Pipeline de Actualización de Capas de Mapas
Cuando se complete la descarga del GeoTIFF desde Google Earth Engine, puedes actualizar los datos del visor web ejecutando los dos scripts Python en la carpeta raíz del proyecto:

1. **Vectorización:** Convierte el GeoTIFF a formato vectorial GeoPackage y fusiona el diccionario conceptual de clases (`diccionario_clases_ecosistemas_hn_v02.csv`):
   ```bash
   python ../scratch/vectorize_map.py
   ```
2. **Filtro y División:** Reproyecta a UTM 16N, remueve polígonos residuales $< 1\text{ ha}$, y fragmenta la base en los archivos individuales colocándolos automáticamente en la carpeta de distribución del visor:
   ```bash
   python ../scratch/process_and_split.py
   ```

Una vez ejecutados los scripts, solo necesitas hacer:
```bash
git add .
git commit -m "Actualizar capas vectoriales de ecosistemas"
git push
```
Y GitHub Pages reconstruirá el mapa web con las nuevas geometrías en minutos.

---

## ⚖️ Licencia y Créditos
Esta aplicación es una bifurcación y adaptación de la plataforma de código abierto **[GeoLibre](https://github.com/opengeos/GeoLibre)**. Todos los scripts de clasificación en Google Earth Engine, diccionarios de homologación e insumos metodológicos han sido desarrollados para la actualización oficial del **Mapa de Ecosistemas de Honduras (v02)**.
