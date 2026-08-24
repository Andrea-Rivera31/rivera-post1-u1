# Análisis 1: Petición GET — example.com

## Información general
- URL: https://example.com/
- Método: GET
- Código de estado: 304 Not Modified

## Headers de Request
| Header | Valor |
|--------|-------|
| Host | example.com |
| User-Agent | Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |

## Headers de Response
| Header | Valor | Significado |
|--------|-------|-------------|
| Content-Type | text/html; charset=UTF-8 | Especifica que el documento entregado es un archivo HTML codificado en UTF-8. |
| Cache-Control | max-age=0 | Indica al navegador que la respuesta debe revalidarse con el servidor antes de ser reutilizada de la caché. |
| ETag | "6a84bb52-22f" | Identificador único para una versión específica del recurso que permite la validación de caché. |

## Tiempos de carga
| Fase | Tiempo (ms) |
|------|------------|
| DNS Lookup | 0.00 ms |
| TTFB | 67.70 ms |
| Content Download | 0.43 ms |

## Conclusión
Al realizar la petición GET hacia example.com, el servidor respondió con un código de estado 304 Not Modified, lo que indica que los recursos no sufrieron cambios y el navegador utilizó su copia almacenada en la memoria caché. El encabezado Cache-Control obliga a comprobar la validez del recurso antes de presentarlo, utilizando el identificador ETag para la verificación. El tiempo hasta el primer byte (TTFB) de 67.70 ms demuestra una baja latencia en la conexión inicial, mientras que la descarga del contenido tomó apenas 0.43 ms debido al ligero tamaño de la estructura HTML.