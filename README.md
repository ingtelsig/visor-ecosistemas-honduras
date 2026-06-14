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

## 🏢 Despliegue en Infraestructura Propia (Autohospedaje)

Si alguna institución desea clonar este visor y alojarlo en su propio servidor de intranet o sitio web institucional, puede hacerlo fácilmente debido a su naturaleza estática y serverless:

### 1. Compilación del Código Fuente
Para compilar la aplicación desde cero, se requiere tener instalado **Node.js** (versión 22 o superior):

```bash
# Instalar dependencias del monorepo
npm install

# Compilar el visor para producción
npm run build
```

La compilación generará los archivos finales optimizados en la carpeta `apps/geolibre-desktop/dist/`.

### 2. Alojamiento en Servidores Web
La carpeta `dist/` contiene exclusivamente archivos estáticos (HTML, JS, CSS y recursos). Puede copiarse directamente al directorio raíz de cualquier servidor web estándar:
* **Servidores tradicionales:** Nginx, Apache, o Internet Information Services (IIS).
* **Servicios en la nube:** AWS S3, Azure Blob Storage, Cloudflare Pages, o Vercel.

*Nota: No es necesario instalar bases de datos relacionales ni servidores de mapas activos (como GeoServer) en la infraestructura de la institución.*

### 3. Personalización del Mapa Institucional
Para adaptar el visor a las necesidades específicas de la institución, solo es necesario editar el archivo de configuración:
`apps/geolibre-desktop/public/datos/proyecto.geolibre.json`

En este archivo se puede configurar:
* El centro geográfico y el zoom inicial del mapa.
* Los estilos de color, etiquetas y simbología de la leyenda.
* Los enlaces a las capas de datos o servicios adicionales.
