# Análisis 3: Petición POST — Postman

## Información general
- URL: https://jsonplaceholder.typicode.com/posts
- Método: POST
- Código de estado: 201 Created

## Configuración de la petición

**Headers enviados**

| Header | Valor |
|--------|-------|
| Content-Type | application/json |

**Cuerpo enviado (Request Body)**
```json
{
  "title": "Laboratorio Programacion Web",
  "body": "Analisis de peticiones HTTP con Postman.",
  "userId": 1
}
```

## Respuesta recibida

**Cuerpo de la respuesta (Response Body)**
```json
{
  "title": "Laboratorio Programacion Web",
  "body": "Analisis de peticiones HTTP con Postman.",
  "userId": 1,
  "id": 101
}
```

El servidor devolvió exactamente el mismo objeto enviado, agregando un campo **`id: 101`** generado automáticamente, confirmando que el recurso fue "creado" (de forma simulada, ya que JSONPlaceholder no persiste los datos realmente).

## Headers relevantes de la respuesta

| Header | Valor | Significado |
|--------|-------|-------------|
| Content-Type | application/json; charset=utf-8 | El cuerpo de la respuesta es un objeto JSON. |
| Content-Length | 127 | Tamaño en bytes del cuerpo de la respuesta. |
| Location | https://jsonplaceholder.typicode.com/posts/101 | URL del nuevo recurso creado, apuntando al ID 101 asignado por el servidor. |
| Cache-Control | no-cache | Indica que esta respuesta no debe almacenarse en caché, ya que corresponde a una creación de recurso. |
| Date | Wed, 26 Aug 2026 03:23:07 GMT | Fecha y hora en que el servidor generó la respuesta. |

## Resultados de los Tests

Se ejecutaron dos pruebas automatizadas en la pestaña **Scripts → Post-response**:

```javascript
pm.test("Status 201 Created", () => {
    pm.response.to.have.status(201);
});

pm.test("Respuesta incluye id asignado", () => {
    const json = pm.response.json();
    pm.expect(json).to.have.property("id");
    pm.expect(json.title).to.equal("Laboratorio Programacion Web");
});
```

**Resultado (Test Results 2/2):**
- ✅ **PASSED** — Status 201 Created
- ✅ **PASSED** — Respuesta incluye id asignado

## Comparación GET vs POST

| Aspecto | GET (Pasos 7 y 8) | POST (Paso 9) |
|---------|--------------------|----------------|
| Propósito | Obtener/consultar un recurso existente | Crear un recurso nuevo en el servidor |
| Cuerpo (Body) | No lleva cuerpo en la petición | Lleva un cuerpo (Body) con los datos a crear, en este caso en formato JSON |
| Código de éxito típico | 200 OK | 201 Created |
| Header de respuesta distintivo | Content-Type según el recurso solicitado | Location, indicando la URL del nuevo recurso creado |
| Idempotencia | Sí — repetir la petición no cambia el estado del servidor | No — cada envío puede crear un recurso distinto (nuevo `id`) |
| Efecto en el servidor | Ninguno (solo lectura) | Modifica el estado del servidor (agrega datos) |

## Conclusión

La petición POST enviada a `https://jsonplaceholder.typicode.com/posts` fue procesada correctamente, devolviendo un código **201 Created**, el código estándar que indica que un nuevo recurso fue creado exitosamente. La respuesta incluyó el objeto enviado más un campo `id` autogenerado por el servidor, y el header `Location` señaló la URL del nuevo recurso. Los dos tests automatizados en Postman confirmaron que el estado de la respuesta y la estructura del cuerpo eran los esperados, demostrando cómo Postman permite no solo enviar peticiones, sino también validar automáticamente el comportamiento de una API. A diferencia de las peticiones GET analizadas en los pasos anteriores, esta petición sí modifica (de forma simulada) el estado del servidor, lo cual se refleja en el uso de un cuerpo (Body) en la petición y en el código de estado 201 en lugar de 200. Esto evidencia una diferencia fundamental en el diseño de las APIs REST: los métodos GET están destinados a la lectura, mientras que POST está destinado a la creación de nuevos recursos.