# Visor del Mapa de Ecosistemas de Honduras (v02)

Este repositorio contiene una adaptación de la plataforma SIG de código abierto **GeoLibre**, configurada como un visor web interactivo, serverless y de alto rendimiento para el **Mapa de Ecosistemas de Honduras**.

El visor está traducido al español y optimizado para cargarse de forma instantánea directamente desde **GitHub Pages** sin necesidad de servidores de mapas dedicados.

---

## 🛠️ Estructura y Funcionamiento del Visor

El visor funciona bajo una arquitectura web estática y serverless, utilizando los siguientes archivos clave:

* **[`apps/geolibre-desktop/index.html`](file:///apps/geolibre-desktop/index.html):** Página de inicio con branding y localización personalizada en español (*Visor de Ecosistemas de Honduras*).
* **[`apps/geolibre-desktop/public/datos/proyecto.geolibre.json`](file:///apps/geolibre-desktop/public/datos/proyecto.geolibre.json):** Archivo de configuración que define el mapa base, extensión espacial inicial (Honduras), estilos oficiales de la leyenda y las rutas a las capas.
* **[`apps/geolibre-desktop/public/datos/clases_separadas/`](file:///apps/geolibre-desktop/public/datos/clases_separadas/):** Directorio donde se almacenan las capas vectoriales en formato GeoPackage `.gpkg` correspondientes a cada clase.
* **[`.github/workflows/pages.yml`](file:///.github/workflows/pages.yml):** Pipeline de GitHub Actions que compila y despliega el visor automáticamente en la raíz de tu sitio de GitHub Pages en cada actualización.

---

## 🌐 Despliegue en GitHub Pages

Para publicar este visor de forma gratuita en tu cuenta de GitHub, sigue estos pasos:

### 1. Vincular y Subir el Código
Abre tu terminal en la carpeta `GeoLibre/` y ejecuta los comandos para subir el código a tu repositorio de GitHub:
```bash
# Agregar cambios, hacer commit y subir todo el código a tu repositorio de GitHub
git add .
git commit -m "Configurar visor de ecosistemas de Honduras para producción"
git branch -M main
git push -u origin main
```

### 2. Activar el Despliegue Automático
1. Ve a la pestaña **Settings** (Configuración) de tu repositorio en la web de GitHub.
2. En el menú de la izquierda, entra a **Pages**.
3. En la sección **Build and deployment -> Source**, selecciona **GitHub Actions**.

GitHub Actions compilará la aplicación y la publicará en la URL: `https://TU_USUARIO.github.io/TU_REPOSITORIO/`.
