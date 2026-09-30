# SigmaTech Apps · Prototipo comercial

MVP demostrativo con datos ficticios. No es un sistema productivo listo para vender.

## A. Arquitectura y dependencias

Aplicación estática: HTML semántico + CSS responsive + JavaScript ES modules. Navegación por fragmentos de URL. El estado de cada escenario se conserva en localStorage, exclusivamente en el navegador actual. Manifest y service worker cachean los archivos de interfaz. No hay dependencias npm, llamadas a servicios de terceros, backend, autenticación, pagos ni datos personales reales. No se envían los registros a un servidor.

La separación entre los escenarios es una organización local de datos, no una frontera de seguridad. Siguiente etapa multiempresa: API con sesiones verificadas en servidor, tabla de empresas, membresías y roles; cada registro ligado a tenant_id. Validar permisos y pertenencia en cada operación, políticas de base de datos, pruebas de aislamiento, copias de seguridad verificadas, registros de auditoría y límites de uso. Nunca confiar en un tenant_id elegido por el navegador. Evaluar cifrado, secretos de servidor, borrado/exportación y revisión de privacidad antes de incorporar información real. No cachear respuestas privadas con el service worker de esta demo.

## B. Estructura

- dist/index.html: estructura, navegación, diálogo.
- dist/styles.css: identidad y adaptaciones móvil/escritorio.
- dist/app.js: escenarios, formularios, inventario, reportes, personalización y almacenamiento local.
- dist/manifest.webmanifest: metadatos PWA.
- dist/sw.js: caché de archivos estáticos; actualizar el nombre de caché en cada versión.
- dist/icon.svg y PNG: iconos propios.

## C y D. Código y ejecución

Requiere navegador moderno. Para desarrollo local requiere Python 3 o un servidor HTTP estático ya instalado; no abrir index.html directamente desde el explorador.

```bash
cd sigmatech-demo
python3 -m http.server 8000 --directory dist
```

Abrir http://localhost:8000. No se requieren npm install, claves ni base de datos. En Chromebook se puede abrir desde Chrome una vez iniciado el servidor en Linux. HTTPS o localhost habilitan service workers en navegadores compatibles. La opción de instalar depende del navegador/dispositivo; probar antes de prometer compatibilidad. La interfaz se puede reutilizar sin conexión tras una primera carga y caché exitosa; cambios se guardan localmente y no se sincronizan. Si se borran datos del navegador se pierden los registros.

## E. Despliegue

Publicar únicamente el contenido de dist en un alojamiento estático con HTTPS que admita manifest y service worker. No hay comando de compilación. Configurar el directorio público dist; mantener las rutas relativas. Abrir la URL y verificar navegación, formularios y descarga CSV. Probar recarga y offline tras primera carga. Para una nueva versión cambiar CACHE en sw.js y revisar la actualización en dispositivos instalados.

La ejecución local no genera cargos de nube. No se garantiza alojamiento gratuito permanente. Vercel Hobby está limitado a uso personal no comercial según su documentación; no asumir que cubre una demo comercial. Antes de usar cualquier proveedor comprobar precios, tráfico, almacenamiento, dominios, términos y continuidad del plan. Referencias consultadas: https://vercel.com/docs/plans/hobby y https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable .

## F. Funcionalidades reales y simuladas

| Elemento | Alcance de la demo |
|---|---|
| Dashboard | Indicadores calculados con registros locales; no analítica histórica real. |
| Clientes / alumnos | Crear, editar, eliminar y buscar registros ficticios. |
| Productos / menú / grupos | Crear, editar y eliminar; precios y existencias/cupos locales. |
| Ventas / pedidos | Registrar un producto y cantidad; validar stock, calcular importe y descontar existencias; cambiar estado. No carrito de varios productos ni reversión automática. |
| Seguimiento escolar | Registro y estados ficticios; sin calificaciones, asistencia, cobros ni datos reales de menores. |
| Inventario / cupos | Ajustes manuales de una unidad. No almacén real ni reservas escolares. |
| Reportes | Gráfico de importes actuales y CSV local. Porcentaje escolar ilustrativo según estados. No utilidad ni impuestos. |
| Configuración | Nombre, acento y logotipo local PNG/JPEG/WebP hasta 300 KB. |
| Escenarios | Tres conjuntos de datos locales; no multiempresa segura. |
| PWA | Manifest y caché estática. Instalación/offline dependen de compatibilidad y primera carga. |
| Seguridad, pagos y notificaciones | No implementados. Sin pantalla de login ficticia que implique seguridad real. |

## G. Guion de demostración de cinco minutos

1. 0:00–0:40: presentar el resumen y la etiqueta Demo. Explicar que las cifras son ficticias y el alcance es demostrativo.
2. 0:40–1:30: abrir Clientes, añadir un registro ficticio y buscarlo; mostrar edición.
3. 1:30–2:30: crear un producto de prueba con precio y cinco unidades, registrar venta de dos unidades y comprobar inventario en tres. Cambiar estado a Completado y ver el dashboard actualizado.
4. 2:30–3:20: pasar a Restaurante; mostrar menú y estados de pedidos. Luego Escuela, grupos y seguimiento sin datos reales.
5. 3:20–4:10: personalizar el nombre, el acento y un logotipo autorizado; mostrar navegación móvil o reducir ventana.
6. 4:10–5:00: exportar reporte CSV, explicar límites de la demo y acordar diagnóstico, alcance, cotización y validación técnica. No prometer módulos ya productivos ni gratis permanente.

## H. Personalizar para un prospecto

Elegir el escenario adecuado, entrar a Configuración, cambiar nombre/colores y cargar logo autorizado. Editar textos de ejemplo y productos usando datos ficticios. Mantener visibles las etiquetas Demo. No introducir datos personales, listas reales de alumnos, contraseñas ni datos bancarios. Antes de mostrar a otro prospecto, usar Restablecer y preparar una identidad nueva. Para cambiar los datos iniciales editar fresh() en app.js y versionar la caché; el contenido local previo se mantiene hasta restablecerlo.

## Verificación y límites

Se revisan sintaxis JS, rutas de assets y flujos locales. No se ha certificado instalación/offline en todos los navegadores ni probado WebMCP en un contexto compatible. La demo no sustituye pruebas de carga, accesibilidad formal, seguridad ni revisión jurídica de un producto multiempresa.
