# Taller 8 — Respuestas del desafío

## 1. `PATCH /api/posts/:id`

Implementado en `taller8-backend/routes/posts.js`. Actualiza **solo** los campos enviados en el body; los que no se envían conservan su valor.

Prueba en Postman (`PATCH http://localhost:3000/api/posts/1`):

```json
{ "title": "Solo cambio el título" }
```

| Petición con solo `title` | Respuesta |
|---|---|
| `PATCH /api/posts/1` | `200` con la publicación: cambia el `title` y se mantienen `body` y `userId`. |
| `PUT /api/posts/1` | `400` `{ "error": "Debes enviar title y body" }`. |

**Diferencia:** `PUT` **reemplaza** la publicación completa, por eso exige todos los datos (`title` y `body`). `PATCH` hace una **actualización parcial**: modifica solo lo que se envía.

Otros casos de `PATCH`: body vacío `{}` → `400`; id inexistente → `404`.

## 2. Botón "Deshacer" al eliminar

Implementado en `taller8-frontend/src/pages/PublicacionesPage.tsx`. Después de eliminar aparece un `IonToast` con el botón **Deshacer**, que vuelve a crear la publicación con `POST` (`crearPublicacion`).

**¿La publicación recuperada tiene el mismo `id`?** No (en general). `POST` no toma el `id` del body: el servidor lo asigna como el mayor `id` existente + 1. Por ejemplo, si se elimina la publicación 3 y se deshace, vuelve como la publicación 6.

La única excepción es cuando se elimina la publicación con el `id` más alto: al recrearla, el mayor `id` restante + 1 coincide con el que tenía, pero es una coincidencia y no porque se haya "restaurado". Para recuperar el mismo `id` haría falta otra operación (por ejemplo, un `PUT` que pueda crear el recurso si no existe).
