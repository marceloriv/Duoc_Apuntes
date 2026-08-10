Sí, puedo utilizar **Skills** especializadas. Los Skills son herramientas y conjuntos de instrucciones avanzadas que tengo integradas para realizar auditorías, optimizaciones y mejoras profundas en la calidad del proyecto.

Tengo disponibles los siguientes Skills en tu entorno de trabajo:

1. **`web-quality-audit` (Auditoría de Calidad Web)**: Para realizar un análisis completo que abarca rendimiento, accesibilidad, buenas prácticas y SEO a la vez.
2. **`performance` (Rendimiento)**: Para optimizar tiempos de carga, acelerar la página y mejorar la velocidad de respuesta del frontend.
3. **`accessibility` (Accesibilidad - a11y)**: Para evaluar y corregir el soporte a lectores de pantalla, navegación por teclado y cumplimiento de las pautas WCAG 2.2.
4. **`seo` (Optimización para Buscadores)**: Para mejorar la visibilidad en motores de búsqueda, optimizar meta-etiquetas, datos estructurados y sitemaps.
5. **`best-practices` (Buenas Prácticas)**: Para auditar la seguridad, modernizar código JavaScript/React, corregir vulnerabilidades y asegurar compatibilidad de navegadores.
6. **`core-web-vitals` (Core Web Vitals)**: Para corregir problemas específicos de experiencia de usuario en carga (LCP), interactividad (INP) y estabilidad visual (CLS).

---

### ¿Cómo los usamos?

Si me lo pides, puedo ejecutar cualquiera de ellos en las páginas del frontend (como la página de inicio, de eventos o de perfil de usuario) para buscar fallos y darte un reporte detallado junto con un plan de acción para solucionarlos.

¿Te gustaría que ejecutemos una **auditoría completa de calidad** (`web-quality-audit`) o alguna en particular sobre el frontend de Ticketti?****

---

## Audit results

### Critical issues (2 found)

- **[Security]** Contraseñas en texto plano en Docker Compose. File: `ms-carrito/docker-compose.yml:6-7,31-32`
  - **Impact:** Las contraseñas de MySQL están expuestas en texto plano en el archivo docker-compose.yml, lo cual es un riesgo de seguridad significativo.
  - **Fix:** Usar variables de entorno o secrets de Docker para gestionar las contraseñas. Ejemplo:

    ```yaml
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      SPRING_DATASOURCE_PASSWORD: ${DB_PASSWORD}
    ```

- **[Security]** Contraseñas en texto plano en Docker Compose. File: `ms-carrito/docker-compose.yml:35-36`
  - **Impact:** Las credenciales de RabbitMQ están expuestas en texto plano.
  - **Fix:** Usar variables de entorno para gestionar las credenciales de RabbitMQ.

### High priority (4 found)

- **[SEO]** Idioma incorrecto en HTML. File: `Ticketti/index.html:2`
  - **Impact:** El atributo `lang="en"` indica inglés pero el sistema es en español (Chile), lo cual afecta SEO y accesibilidad.
  - **Fix:** Cambiar a `lang="es-CL"`:

    ```html
    <html lang="es-CL">
    ```

- **[SEO]** Falta meta description. File: [Ticketti/index.html](cci:7://file:///c:/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/Ticketti/index.html:0:0-0:0)
  - **Impact:** Sin meta description, los motores de búsqueda no tienen contexto sobre el contenido de la página.
  - **Fix:** Agregar meta description:

    ```html
    <meta name="description" content="Ticketti - Compra entradas para eventos, conciertos y experiencias únicas en Chile.">
    ```

- **[Performance]** Bootstrap CSS completo cargado. File: `Ticketti/src/main.jsx:3`
  - **Impact:** Cargar todo Bootstrap CSS (~200KB) incluye estilos no utilizados, aumentando el tiempo de carga.
  - **Fix:** Usar tree-shaking o cargar solo los componentes necesarios, o considerar una librería CSS más ligera.

- **[Performance]** @import en CSS bloquea renderizado. File: `Ticketti/src/index.css:1`
  - **Impact:** `@import` bloquea el renderizado hasta que el archivo importado se descargue.
  - **Fix:** Mover el import a un `<link>` en el HTML o usar un bundler que combine los CSS.

### Medium priority (5 found)

- **[SEO]** Falta meta tags para redes sociales. File: [Ticketti/index.html](cci:7://file:///c:/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/Ticketti/index.html:0:0-0:0)
  - **Impact:** Sin Open Graph tags, los enlaces compartidos no muestran preview rico.
  - **Fix:** Agregar meta tags Open Graph:

    ```html
    <meta property="og:title" content="Ticketti">
    <meta property="og:description" content="Compra entradas para eventos en Chile">
    <meta property="og:image" content="/img/og-image.jpg">
    ```

- **[Performance]** Falta preconnect/preload para recursos críticos. File: [Ticketti/index.html](cci:7://file:///c:/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/Ticketti/index.html:0:0-0:0)
  - **Impact:** Sin preconnect, el navegador no establece conexiones tempranas a orígenes externos.
  - **Fix:** Agregar preconnect para orígenes externos:

    ```html
    <link rel="preconnect" href="http://localhost:8081">
    ```

- **[Best Practices]** Console.logs en código de producción. File: `Ticketti/src/api/api.js:50,57,60,66,71`
  - **Impact:** Los console.logs exponen información sensible y afectan performance.
  - **Fix:** Remover o usar un logger condicional para desarrollo únicamente.

- **[Best Practices]** Console.logs en código de producción. File: `Ticketti/src/components/layout/Header.jsx:128,129,132,140,142,149,152,158,162,166`
  - **Impact:** Los console.logs afectan performance y exponen información del flujo del carrito.
  - **Fix:** Remover o usar un logger condicional para desarrollo únicamente.

- **[Best Practices]** Console.logs en código de producción. File: `Ticketti/src/pages/Inicio.jsx:104,169,170`
  - **Impact:** Los console.logs afectan performance.
  - **Fix:** Remover o usar un logger condicional para desarrollo únicamente.

### Low priority (2 found)

- **[Best Practices]** Falta meta viewport optimizado. File: `Ticketti/index.html:6`
  - **Impact:** El viewport actual es básico pero funcional.
  - **Fix:** Considerar agregar `maximum-scale=1, user-scalable=no` para mejor UX móvil.

- **[Accessibility]** Falta skip link para navegación por teclado. File: [Ticketti/index.html](cci:7://file:///c:/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/Ticketti/index.html:0:0-0:0)
  - **Impact:** Usuarios de teclado no pueden saltar directamente al contenido principal.
  - **Fix:** Agregar skip link:

    ```html
    <a href="#main-content" class="skip-link">Saltar al contenido principal</a>
    ```

### Summary

- **Performance:** 4 issues (0 critical)
- **Accessibility:** 2 issues (0 critical)
- **SEO:** 3 issues (0 critical)
- **Best Practices:** 4 issues (0 critical)
- **Security:** 2 issues (2 critical)

### Recommended priority

1. **Primero corregir las contraseñas en texto plano** - Es un riesgo de seguridad crítico que debe ser resuelto inmediatamente.
2. **Corregir el idioma del HTML** - Cambiar `lang="en"` a `lang="es-CL"` para SEO y accesibilidad.
3. **Agregar meta description y Open Graph tags** - Mejora significativa de SEO.
4. **Optimizar Bootstrap CSS** - Mejora de performance eliminando CSS no utilizado.
5. **Remover console.logs de producción** - Mejora de performance y seguridad.
6. **Agregar preconnect/preload** - Mejora de performance para recursos externos.
7. **Agregar skip link** - Mejora de accesibilidad para usuarios de teclado.
