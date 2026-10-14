# Taller 8: CRUD completo con Express + Ionic

Entrega del Taller 8 de Ingeniería Web y Móvil 2026 (Paralelo 1).
Enunciado original: [Taller 8 en el repositorio del curso](https://github.com/FranciscoPonce-PUCV/-IngenieriaWebMovil2026-Paralelo1/tree/main/Taller%208).

El objetivo era completar las operaciones CRUD de la API, ordenar el servidor con middlewares y rutas en archivos separados, y usar la API desde una aplicación Ionic que lista, crea, edita y elimina publicaciones.

## Lo pedido vs. lo logrado

### Parte 1: Backend (`taller8-backend`)

| Paso | Lo que pedía el taller | Lo logrado |
|---|---|---|
| 1 | Ruta `DELETE /api/posts/:id` | ✅ Responde `204` al eliminar y `404` si la publicación no existe. |
| 2 | Ruta `PUT /api/posts/:id` | ✅ Responde `200` con la publicación reemplazada, `400` si falta `title` o `body` y `404` si no existe. |
| 3 | Registrar `morgan` como primer middleware | ✅ `morgan("tiny")` muestra cada petición en la terminal, incluidas las que tienen el JSON malformado. |
| 4 | Middleware con nombre para rutas inexistentes | ✅ `endpointDesconocido` responde `404` `{ "error": "Ruta no encontrada" }`. |
| 5 | Middleware de manejo de errores | ✅ `manejadorErrores` responde `400` con JSON si el body no es un JSON válido (en vez de la página HTML con las rutas del computador) y `500` ante otros errores. |
| 6 | Organizar las rutas con `express.Router` | ✅ El arreglo `posts` y las rutas están en `routes/posts.js`, montadas en `/api/posts`. `servidor.js` queda solo con la configuración, los middlewares y las rutas `/` y `/saludo/:nombre`. |

### Parte 2: Frontend (`taller8-frontend`)

| Paso | Lo que pedía el taller | Lo logrado |
|---|---|---|
| 7 | Enviar el filtro `?userId=` en `obtenerPublicaciones` | ✅ El filtro por usuario funciona. |
| 8 | Completar `actualizarPublicacion` (`PUT`) | ✅ Se pueden editar publicaciones; si falta un campo, se muestra el mensaje `400` del servidor y el formulario queda abierto. |
| 9 | Completar `eliminarPublicacion` (`DELETE`) | ✅ Se pueden eliminar publicaciones deslizándolas o desde el formulario de edición. |

### Desafío (opcional)

| Desafío | Lo logrado |
|---|---|
| 1. Ruta `PATCH /api/posts/:id` | ✅ Actualiza solo los campos enviados. Responde `400` si el body viene vacío y `404` si la publicación no existe. |
| 2. Botón **Deshacer** al eliminar | ✅ Un `IonToast` con el botón **Deshacer** vuelve a crear la publicación con `POST`. |

Las respuestas a las preguntas del desafío (diferencia entre `PATCH` y `PUT`, y por qué la publicación recuperada cambia de `id`) están en [DESAFIO.md](DESAFIO.md).

## Archivos modificados

```text
taller8-backend/
├── routes/posts.js      → nuevo: arreglo posts + rutas GET, POST, PUT, PATCH y DELETE
├── servidor.js          → morgan, router, endpointDesconocido y manejadorErrores
└── package.json         → dependencia morgan
taller8-frontend/src/
├── services/api.ts                → pasos 7, 8 y 9
└── pages/PublicacionesPage.tsx    → botón Deshacer (desafío 2)
```

## Cómo ejecutarlo

```bash
# Terminal 1 (backend) → http://localhost:3000
cd taller8-backend
npm install
npm run dev

# Terminal 2 (frontend) → http://localhost:8100
cd taller8-frontend
npm install
ionic serve
```

Las peticiones para probar la API están en `Taller8.postman_collection.json` (se importa en Postman con **Import**).

## Verificación

- Todas las peticiones de la colección de Postman responden con los códigos que indica el enunciado (`200`, `201`, `204`, `400` y `404`).
- El frontend compila sin errores de TypeScript (`tsc`) ni de ESLint.
