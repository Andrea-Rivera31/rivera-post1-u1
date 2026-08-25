# Análisis 2: Petición GET — API REST (JSONPlaceholder)

## Petición 1: Recurso existente

### Información general
- URL: https://jsonplaceholder.typicode.com/posts/1
- Método: GET
- Código de estado: 200 OK

### Headers de Request

| Header | Valor |
|--------|-------|
| Host (:authority) | jsonplaceholder.typicode.com |
| User-Agent | Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |

### Headers de Response

| Header | Valor | Significado |
|--------|-------|-------------|
| Content-Type | application/json; charset=utf-8 | Indica que el cuerpo de la respuesta es un objeto JSON, no HTML. |
| Server | cloudflare | El sitio está detrás de la CDN de Cloudflare. |
| Cache-Control | max-age=43200 | El recurso puede guardarse en caché hasta por 43,200 segundos (12 horas). |
| Age | 24498 | La copia en caché tiene 24,498 segundos de antigüedad. |
| Cf-Cache-Status | HIT | La respuesta fue servida desde la caché de Cloudflare, no desde el servidor origen. |
| X-Powered-By | Express | Revela que el backend de la API está construido con el framework Express (Node.js). |
| X-Ratelimit-Limit / Remaining / Reset | 1000 / 999 / 1786363494 | Indican el límite de peticiones permitidas, cuántas quedan disponibles y cuándo se reinicia el contador (formato timestamp Unix). |

### Respuesta (Response)
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```
La respuesta es un objeto JSON con datos estructurados (pares clave-valor), muy distinto al documento HTML completo que se recibió en el Análisis 1.

---

## Petición 2: Recurso inexistente

### Información general
- URL: https://jsonplaceholder.typicode.com/posts/999
- Método: GET
- Código de estado: 404 Not Found
- Tamaño: 1.2 kB
- Tiempo: 234 ms

### Respuesta (Response)
```json
{}
```
El servidor responde con un objeto JSON vacío, indicando que no existe ningún recurso con el ID solicitado (999). A diferencia de una página HTML tradicional, que suele mostrar una página de error "404" visual, una API REST bien diseñada simplemente devuelve un código de estado 404 junto con un cuerpo vacío o un mensaje de error en formato JSON.

---

## Comparación: HTML vs API REST

| Aspecto | example.com (Paso 7 - HTML) | JSONPlaceholder (Paso 8 - API REST) |
|---------|------------------------------|----------------------------------------|
| Content-Type | text/html | application/json; charset=utf-8 |
| Formato de la respuesta | Documento HTML completo (etiquetas, estilos) | Objeto JSON estructurado (clave-valor) |
| Propósito de la respuesta | Ser renderizada visualmente por el navegador | Ser consumida y procesada por código (JavaScript, apps, etc.) |
| Manejo de error | Página de error visual (HTML) | Código de estado HTTP (404) con cuerpo JSON vacío o mensaje de error |
| Servidor / tecnología | Cloudflare (estático) | Cloudflare + Express (Node.js) |

## Conclusión

Este análisis permitió comparar dos tipos de respuestas HTTP muy distintas. La petición a `jsonplaceholder.typicode.com/posts/1` devolvió un código 200 OK con un `Content-Type: application/json`, evidenciando que su propósito es entregar datos estructurados para ser consumidos por aplicaciones, a diferencia de la respuesta `text/html` analizada en el Paso 7, que está pensada para ser interpretada visualmente por un navegador. Al solicitar un recurso inexistente (`/posts/999`), la API respondió correctamente con un código 404 Not Found y un cuerpo JSON vacío, demostrando un manejo de errores propio de una API REST bien diseñada, en contraste con las páginas de error HTML tradicionales. Además, los headers de respuesta revelaron información útil sobre la infraestructura del servicio, como el uso de Express como framework backend y políticas de límite de peticiones (`X-Ratelimit-*`), algo que no se observa en peticiones a páginas HTML estáticas simples como example.com.