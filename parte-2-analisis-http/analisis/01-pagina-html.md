# Análisis 1: Petición GET — example.com

## Información general
- URL: https://example.com/
- Método: GET
- Código de estado: 200 OK

## Headers de Request

| Header | Valor |
|--------|-------|
| Host | example.com |
| User-Agent | Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |

## Headers de Response

| Header | Valor | Significado |
|--------|-------|-------------|
| Content-Type | text/html | Indica que el cuerpo de la respuesta es un documento HTML, para que el navegador sepa cómo interpretarlo. |
| Content-Encoding | br | El contenido fue comprimido con el algoritmo Brotli antes de enviarse, para reducir el peso de la transferencia. |
| Server | cloudflare | Indica que el sitio está detrás de la red de distribución de contenido (CDN) Cloudflare, y no directamente del servidor origen. |
| Cf-Cache-Status | HIT | Confirma que la respuesta fue servida desde la caché de Cloudflare y no desde el servidor original, lo que acelera la entrega. |
| Age | 9 | Indica que el recurso guardado en caché tiene 9 segundos de antigüedad al momento de la petición. |
| Transfer-Encoding | chunked | El servidor envía el contenido en fragmentos ("chunks") en lugar de anunciar de antemano el tamaño total con `Content-Length`. |

> **Nota:** en esta petición no aparece el header `Content-Length` porque el servidor usa `Transfer-Encoding: chunked`. Con esta técnica, el servidor no necesita conocer ni anunciar el tamaño total del contenido antes de enviarlo, ya que lo transmite en partes.

## Tiempos de carga

| Fase | Tiempo (ms) |
|------|-------------|
| DNS Lookup | 105.27 ms |
| Initial connection | 102.14 ms |
| SSL | 54.05 ms |
| TTFB (Time to First Byte / Waiting for server response) | 54.49 ms |
| Content Download | 1.39 ms |
| **Tiempo total** | **265.22 ms** |

## Conclusión

La petición GET a `https://example.com` obtuvo un código de estado 200 OK, indicando que el recurso se entregó correctamente. Se observa que el sitio utiliza Cloudflare como CDN, lo cual se confirma con los headers `Server: cloudflare` y `Cf-Cache-Status: HIT`, este último indicando que la respuesta fue servida desde la caché del CDN en lugar del servidor origen, reduciendo la carga sobre este último. La mayor parte del tiempo de carga se concentró en el establecimiento de la conexión (DNS Lookup e Initial connection), mientras que el tiempo de espera de respuesta del servidor (TTFB) y la descarga del contenido fueron considerablemente más rápidos, lo cual es típico de un recurso HTML ligero servido desde una CDN. El uso de compresión Brotli (`Content-Encoding: br`) y de `Transfer-Encoding: chunked` en lugar de `Content-Length` evidencian buenas prácticas de optimización en la entrega del contenido web.