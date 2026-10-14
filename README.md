# Taller 8: CRUD completo con Express + Ionic

Entrega del Taller 8 de Ingeniería Web y Móvil 2026 (Paralelo 1).
Enunciado original: [Taller 8 en el repositorio del curso](https://github.com/FranciscoPonce-PUCV/-IngenieriaWebMovil2026-Paralelo1/tree/main/Taller%208).

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
