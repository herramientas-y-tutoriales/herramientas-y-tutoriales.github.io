---
layout: post
title: "Cómo comprobar un export de Webflow antes de alojarlo fuera"
description: "Aprende a comprobar un export de Webflow antes de alojarlo fuera: rutas, CMS, recursos, formularios y metadatos en una revisión corta."
date: 2026-11-19 17:27:52 +0000
categories: [herramientas, tutoriales]
tags: [webflow, hosting-estatico, exportacion-web, webflow-cms, exflow]
canonical_url: ""
image: "/assets/img/posts/2026-11-19-como-comprobar-un-export-de-webflow-antes-de-alojarlo-fuera/cover-ae2145ca1dba.webp"
---

# Cómo comprobar un export de Webflow antes de alojarlo fuera

Antes de mover una web de Webflow a otro alojamiento, no basta con abrir la portada y ver que parece correcta. Un buen export debe conservar las rutas, las páginas CMS, los recursos, las interacciones y los metadatos que la web necesita para seguir siendo útil. La forma más segura es probar una copia estática en una URL temporal y pasar una lista breve de comprobaciones antes de tocar DNS.

Si tu objetivo es obtener una copia estática de un sitio publicado —incluidas sus páginas CMS—, el [exportador de Webflow de ExFlow](https://exflow.site/webflow) descarga HTML, CSS, JavaScript, imágenes y las rutas públicas en un paquete que puedes revisar y alojar por tu cuenta. Eso resuelve la parte de sacar los archivos; la revisión evita descubrir fallos cuando ya hay visitas reales.

![Panel de comprobaciones para un export estático de Webflow](/assets/img/posts/2026-11-19-como-comprobar-un-export-de-webflow-antes-de-alojarlo-fuera/image-01-efd62d27b8d7.webp)

## La regla útil: prueba el destino, no solo el archivo ZIP

Un ZIP puede contener todos los archivos y aun así fallar al publicarse. Una ruta puede depender de una barra final, una imagen puede tener una ruta absoluta, o un script puede cargarse distinto detrás de un subdirectorio. Por eso conviene publicar el export en un dominio de prueba o en el entorno de staging del host elegido.

Antes de empezar, apunta qué significa “listo” para tu sitio. No todos los elementos tienen la misma prioridad:

| Área | Qué comprobar | Qué hacer si falla |
| --- | --- | --- |
| Rutas | Inicio, navegación, páginas legales y campañas abren sin 404 | Corrige enlaces relativos o configura redirecciones antes del cambio |
| CMS | Una muestra de fichas, artículos y categorías abre desde enlaces internos | Revisa el inventario de URLs y vuelve a exportar las páginas faltantes |
| Recursos | Imágenes, tipografías, vídeo, CSS y JavaScript cargan sin errores | Busca rutas externas o recursos que no entraron en el paquete |
| Funciones | Formularios, buscador, pagos, área privada y analítica tienen un plan propio | Sustituye o reconecta los servicios que dependían del servidor de Webflow |
| Descubrimiento | Título, descripción, canonical y previsualización social siguen presentes | Corrige la plantilla o la configuración del host antes de indexar |

Esta separación importa porque una web estática conserva lo que el navegador puede servir como archivos, pero no reemplaza automáticamente servicios que trabajan en un servidor. ExFlow lo explica de forma concreta: la salida incluye el marcado, recursos y scripts publicados; funcionalidades como formularios nativos, checkout, búsqueda o el editor requieren un destino o servicio alternativo.

## 1. Congela un inventario pequeño de rutas críticas

No hace falta revisar cada URL a mano en un sitio grande. Empieza con una muestra representativa: la portada, una página de cada plantilla, las cinco rutas con más tráfico y una URL profunda que llegue desde Google o una campaña. Si hay CMS, añade una ficha reciente, una antigua y una categoría.

Esta es una versión reducida del trabajo de [crear un inventario de URLs CMS antes de un export estático](https://how-to.the-lean-ecommerce.com/2026/11/16/how-to-create-a-webflow-cms-url-inventory-before-a-static-export/). La idea no es producir una hoja interminable: es tener una lista de control que permita comparar la web publicada con la copia.

Para que el inventario funcione, guarda tres datos por ruta: URL actual, tipo de página y resultado esperado. Por ejemplo: “/blog/nombre-del-articulo/ — artículo CMS — carga imagen destacada y enlaces relacionados”. Ese detalle hace que una prueba sea repetible y evita el clásico “creo que antes se veía bien”.

![Archivo de páginas CMS antes de un export de Webflow](/assets/img/posts/2026-11-19-como-comprobar-un-export-de-webflow-antes-de-alojarlo-fuera/image-02-3ce679115bf6.webp)

## 2. Haz un export que incluya la web publicada, no una reconstrucción

Cuando uses ExFlow, pega la URL publicada, activa la exportación de páginas, CSS, JavaScript y recursos multimedia, y conserva la opción de seguir las rutas públicas. Según su documentación, el proceso puede usar el sitemap y los enlaces internos para incorporar páginas públicas y páginas de colección CMS como HTML estático.

El primer resultado que debes mirar no es el diseño: es la lista de archivos. Busca carpetas coherentes para estilos, scripts y medios, y confirma que hay una salida para las rutas críticas del inventario. Para una web con blog, esto es especialmente importante: una portada impecable no demuestra que las entradas antiguas hayan viajado con ella.

Si estás preparando un rediseño, puede ayudarte la misma lógica de un [archivo de contenido CMS antes de rediseñar Webflow](https://how-to.the-lean-ecommerce.com/2026/11/05/how-to-create-a-webflow-cms-content-freeze-archive-before-a-redesign/): fija una versión conocida antes de cambiar diseño, alojamiento o colecciones.

## 3. Prueba enlaces, recursos y responsive como tres controles distintos

Abre la copia en el alojamiento de prueba y pasa el inventario. Primero, navega con el menú y los enlaces internos; después pega directamente varias URLs profundas en una ventana nueva. Son pruebas distintas: la primera detecta enlaces rotos; la segunda descubre problemas del servidor al resolver rutas.

Luego abre las herramientas del navegador. No necesitas convertirte en desarrolladora: basta con mirar si aparecen errores claros de recursos no encontrados y comprobar que las imágenes principales, fuentes y elementos interactivos se cargan. Cambia también el ancho de la ventana para revisar una página de contenido y una página de conversión.

Este paso merece atención porque Webflow usa estilos y scripts publicados para las interacciones. ExFlow documenta que incluye esos recursos y reescribe los enlaces a archivos locales; aun así, el host elegido y la estructura de rutas son parte de tu propia prueba. Para una comparación práctica, el control de animaciones de un [export de Framer a HTML](https://how-to.the-lean-ecommerce.com/2026/11/18/how-to-export-a-framer-site-to-static-html-with-an-animation-qa-pass/) ilustra bien el hábito: confirmar la experiencia en el destino, no asumirla por el archivo descargado.

## 4. Decide qué servicios deben sobrevivir al cambio

Aquí aparece el límite saludable de una exportación estática. Haz una lista de las funciones que envían o reciben datos: formularios de contacto, newsletter, buscador, reservas, checkout, login, analítica y cookies. Para cada una, elige una de estas decisiones:

- Se mantiene mediante un servicio externo o una API.
- Se reemplaza por una alternativa sencilla.
- Se retira porque ya no cumple una función real.
- Obliga a conservar la web en su plataforma actual.

No ocultes esta decisión al cliente o al equipo. Un formulario bonito que ya no entrega mensajes no es un detalle de QA; es un cambio de producto. Si vas a alojar un sitio estático, deja por escrito dónde enviará cada formulario y quién comprobará la primera entrada real.

## 5. Revisa metadatos y prepara la vuelta atrás

Antes de cambiar el dominio, abre el código fuente de dos o tres páginas y confirma que siguen existiendo el título, la meta descripción, la imagen social y la URL canonical. Comprueba además favicon, sitemap y cualquier redirección importante. Es la parte menos vistosa, pero protege el tráfico que ya has ganado.

Guarda el ZIP, el inventario y una fecha de exportación. Si sincronizas a Git desde ExFlow, cada versión puede quedar como un punto de revisión y reversión; si prefieres una entrega manual, conserva también una copia fuera del ordenador local. La misma precaución aparece al [entregar una web Squarespace como archivos estáticos sin perder servicios esenciales](https://how-to.the-lean-ecommerce.com/2026/11/19/how-to-hand-off-a-squarespace-site-as-static-files-without-losing-esse/): los archivos son solo una parte de la entrega.

![Opciones de alojamiento para una web estática exportada](/assets/img/posts/2026-11-19-como-comprobar-un-export-de-webflow-antes-de-alojarlo-fuera/image-03-948cfa5442cc.webp)

## Dónde alojar el resultado

Cuando la copia supera la revisión, puedes descargar el ZIP y subirlo a tu host, o sincronizar el export con Git, S3, FTP o el alojamiento de ExFlow. La opción correcta depende de quién actualizará el sitio, qué flujo de revisión necesita el equipo y si ya existe una infraestructura de despliegue.

Si buscas un camino corto, empieza con el [exportador de Webflow de ExFlow](https://exflow.site/webflow), pruébalo en un entorno separado y cambia el dominio solo cuando la lista crítica esté en verde. ExFlow también ofrece exportadores específicos para [Framer](https://exflow.site/framer) y [Squarespace](https://exflow.site/squarespace), pero conviene tratar cada plataforma con su propio control de calidad.

## Conclusión

Exportar una web de Webflow te da portabilidad; comprobarla antes de alojarla fuera te da tranquilidad. Haz un inventario pequeño, prueba rutas profundas y recursos en el destino, decide qué ocurrirá con cada servicio dinámico y conserva una vuelta atrás. El siguiente paso es simple: elige cinco URLs críticas de tu sitio y pruébalas hoy en una copia estática antes de mover una sola DNS.
