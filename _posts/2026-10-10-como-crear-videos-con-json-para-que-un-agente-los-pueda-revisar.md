---
layout: post
title: "Cómo Crear Videos con JSON para que un Agente los Pueda Revisar"
description: "Una guía práctica para convertir datos en VideoJSON, revisar el borrador y renderizar videos repetibles con VideoFlow."
date: 2026-10-10 08:33:35 +0000
categories: [herramientas, tutoriales]
tags: [video-programatico, automatizacion, typescript, videojson, ia]
canonical_url: ""
image: "/assets/img/posts/2026-10-10-como-crear-videos-con-json-para-que-un-agente-los-pueda-revisar/cover-cf2f9cc99c9c.webp"
---

Cuando un equipo dice que quiere generar videos con IA, casi siempre aparecen dos problemas a la vez: el resultado no se puede revisar con calma y cada cambio obliga a empezar de nuevo. La salida no es pedirle más creatividad al modelo; es darle una estructura que una persona pueda entender, ajustar y aprobar.

[VideoFlow](https://videoflow.dev/) propone una idea útil para ese trabajo: describir el video como datos —VideoJSON— y usar ese mismo documento para previsualizarlo, editarlo y renderizarlo. Así, un agente puede preparar el primer borrador sin convertirse en el dueño de una línea de tiempo imposible de auditar.

![Flujo de datos a VideoJSON, revisión y renderizado](/assets/img/posts/2026-10-10-como-crear-videos-con-json-para-que-un-agente-los-pueda-revisar/image-01-f8e192aba8da.webp)

## La regla que evita videos automáticos difíciles de corregir

Piensa en un video de producto de 15 segundos. Tus datos ya están en algún lugar: título, imágenes, precio, beneficios, una reseña y el enlace de compra. En vez de pedir «haz un video», conviene transformar esa información en un documento con escenas, capas, tiempos y recursos. Ese documento es la fuente de verdad.

El flujo corto queda así:

1. Reúne datos que sí han pasado una revisión: ficha, imágenes y mensajes aprobados.
2. Genera un VideoJSON con una plantilla y variables concretas.
3. Móntalo en una vista previa para detectar textos largos, imágenes mal recortadas o una llamada a la acción confusa.
4. Deja que alguien ajuste lo necesario y apruebe la versión.
5. Renderiza el MP4 solo cuando el documento está listo.

Ese paso intermedio importa. Es el mismo motivo por el que, al [crear una cola de renderizado desde datos de producto](https://how-to.the-lean-ecommerce.com/2026/10/09/how-to-build-a-video-rendering-queue-from-product-data/), no basta con enviar trabajos: hay que saber qué versión se está enviando.

## Qué debe contener un VideoJSON útil

No hace falta que un agente invente una película. Para una pieza repetible, dale una plantilla con límites claros: duración, relación de aspecto, tipografías, zonas para imágenes, orden de escenas y campos que puede completar. VideoFlow permite crear esa estructura con su [API Core](https://videoflow.dev/core), compilarla a VideoJSON y conservarla junto al resto del proyecto.

Una estructura sencilla podría incluir una portada breve, una escena con el beneficio principal, una prueba visual y un cierre con CTA. Para cada capa, guarda el tipo de recurso, el texto, la posición, la duración y las transiciones permitidas. El resultado es mucho más fácil de comparar entre versiones que una exportación de video sin contexto.

También te da una conversación mucho más útil con la IA. En lugar de decir «el video se siente raro», puedes cambiar un campo: acortar el texto de la escena dos, sustituir una imagen, retrasar el CTA o quitar una transición. Si ya has visto por qué conviene [revisar VideoJSON antes de mandarlo a una cola](https://the-lean-ecommerce.gitlab.io/2026/10/05/i-review-videojson-before-it-reaches-the-render-queue/), reconocerás la ventaja: cada corrección queda en el objeto, no perdida en una indicación oral.

![Borrador de video editable sobre una línea de tiempo](/assets/img/posts/2026-10-10-como-crear-videos-con-json-para-que-un-agente-los-pueda-revisar/image-02-4aa655b447a7.webp)

## Dale al agente un trabajo concreto, no control total

Un buen encargo para un agente puede ser: «crea tres escenas a partir de esta ficha, usa solo estos recursos y devuelve JSON válido». Antes de renderizar, valida que están presentes los campos obligatorios, que las URLs son públicas, que la duración total cabe en el formato elegido y que no hay texto fuera de los límites.

Después, presenta ese borrador en una previsualización. VideoFlow tiene un renderer DOM para reproducción y búsqueda de fotogramas, y su [editor de video para React](https://videoflow.dev/react-video-editor) añade una línea de tiempo multipista donde el equipo puede arrastrar, recortar y ordenar capas. Eso no convierte una automatización en una herramienta complicada: convierte el último kilómetro en algo visible.

Es una diferencia práctica si construyes una herramienta interna. En vez de un botón misterioso de «generar», puedes ofrecer «crear borrador», «revisar» y «renderizar». El mismo enfoque sirve para clips de catálogo, resúmenes mensuales, vídeos de onboarding o variaciones localizadas. Para ideas de producto más amplias, mira también esta guía sobre [usar una URL de startup para probar un video de lanzamiento](https://the-lean-ecommerce.github.io/2026/10/06/how-i-use-a-startup-url-to-test-a-launch-video-before-production/): el principio es el mismo, aunque aquí la pieza editable nace de datos estructurados.

## Decide dónde renderizar según el trabajo

Una vez aprobado el JSON, queda una decisión sencilla: dónde producir el archivo final. Para una exportación corta iniciada por un usuario, el renderer de navegador puede evitar subir el proyecto a un servidor. Para lotes, trabajos programados o una API, el renderer de servidor encaja mejor en una cola. La documentación de [renderers de VideoFlow](https://videoflow.dev/renderers) explica ambas rutas sobre el mismo documento.

![Elección entre renderizado en navegador o servidor](/assets/img/posts/2026-10-10-como-crear-videos-con-json-para-que-un-agente-los-pueda-revisar/image-03-8a3fff9c2e0e.webp)

No elijas por moda. El navegador puede simplificar costes y privacidad cuando la persona exporta una pieza pequeña. El servidor ofrece más control para decenas de videos, reintentos y seguimiento. Si tu caso mezcla ambos, conserva VideoJSON como contrato común y cambia solo el renderer.

## Una primera prueba que no se desborda

Empieza con una sola plantilla y cinco registros de prueba. Define qué datos entran, qué puede cambiar el agente y quién aprueba. Mide cuántas correcciones necesita cada borrador y qué campos se repiten. Con esa información podrás mejorar la plantilla antes de automatizar cien trabajos.

VideoFlow es especialmente interesante porque su core y renderers son de código abierto bajo Apache-2.0, pero su ventaja cotidiana no es una lista de funciones: es poder tratar el video como un resultado revisable. Abre la [documentación de VideoFlow](https://videoflow.dev/docs), diseña una plantilla mínima y prueba el ciclo completo: datos, JSON, vista previa, aprobación y render. Cuando ese ciclo funciona una vez, ya tienes una base mucho más segura para automatizarlo.
