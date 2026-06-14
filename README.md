# Visor del Mapa de Ecosistemas de Honduras

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
