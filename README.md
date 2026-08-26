# Post-contenido — Unidad 1: Fundamentos de la Web

## Descripción
Repositorio del laboratorio de la Unidad 1 de Programación Web. Contiene dos partes: configuración del entorno de desarrollo (`parte-1-entorno/`) y análisis de peticiones HTTP con Chrome DevTools y Postman (`parte-2-analisis-http/`).

## Parte 1 — Entorno de desarrollo

Se configuró el entorno de desarrollo web con VS Code (extensiones Live Server, Prettier, GitLens y ESLint), Git y GitHub. Se construyó una página HTML básica ("Fundamentos de la Web") con estilos CSS y un script JS, la cual fue inspeccionada con Chrome DevTools: se recorrió el árbol del DOM en el panel *Elements*, se verificaron los estilos aplicados al `header`, y se confirmaron en la *Console* los mensajes registrados por `main.js` (carga de la página, título del documento y cantidad de secciones encontradas).

Ver [parte-1-entorno/](./parte-1-entorno/).

## Parte 2 — Análisis de peticiones HTTP

| # | Tipo | URL | Código |
|---|------|-----|--------|
| 1 | GET HTML | https://example.com | 200 OK |
| 2 | GET JSON (exitoso) | /posts/1 | 200 OK |
| 3 | GET JSON (fallido) | /posts/999 | 404 Not Found |
| 4 | POST JSON | /posts | 201 Created |

Ver [parte-2-analisis-http/analisis/](./parte-2-analisis-http/analisis/).

## Herramientas utilizadas
- VS Code, Git, GitHub
- Google Chrome + DevTools (panel Network)
- Postman (petición POST con tests)

## Conclusiones

Este laboratorio permitió configurar de principio a fin un entorno de desarrollo web funcional y aplicar ese entorno para analizar tráfico HTTP real. Se pudo comprobar en la práctica la diferencia entre una respuesta pensada para el navegador (`text/html`) y una respuesta pensada para ser consumida por código (`application/json`), así como el distinto propósito de los métodos GET (consultar datos, sin modificar el servidor) y POST (crear un nuevo recurso). El uso de Postman permitió además automatizar la verificación de una API mediante tests, evidenciando cómo estas herramientas son fundamentales para depurar aplicaciones y diseñar comunicaciones cliente-servidor eficientes en el desarrollo web profesional.