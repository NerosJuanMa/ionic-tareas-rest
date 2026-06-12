# ionic-tareas-rest
# Tareas REST API

API REST sencilla para la gestión de tareas, desarrollada con Node.js y Express, preparada para ejecutarse en contenedores Docker durante el desarrollo.

## Características

* API REST construida con Express 5.
* Gestión básica de tareas en memoria.
* Soporte para Docker y Docker Compose.
* Recarga automática de cambios mediante `node --watch`.
* Uso de Yarn como gestor de dependencias.

## Estructura del proyecto

```text
docker/
├── app/
│   ├── package.json
│   └── src/
│       ├── server.js
│       ├── tasks.js
│       └── test.js
├── Dockerfile
└── compose.yml
```

## Requisitos

* Docker
* Docker Compose

Opcionalmente para ejecución local:

* Node.js 20+
* Yarn

## Puesta en marcha con Docker

### 1. Crear archivo `.env`

Crear un archivo `.env` en la carpeta `docker`:

```env
PORT=3000
```

### 2. Construir y arrancar los contenedores

```bash
docker compose up --build
```

La API quedará disponible en:

```text
http://localhost:3000
```

## Ejecución local

Instalar dependencias:

```bash
cd app
yarn install
```

Iniciar el servidor en modo desarrollo:

```bash
yarn start
```

O ejecutar sin modo watch:

```bash
yarn serve
```

## Endpoints disponibles

### Obtener todas las tareas

**GET** `/tasks`

Ejemplo:

```bash
curl http://localhost:3000/tasks
```

Respuesta:

```json
[
  {
    "id": 1,
    "title": "Mi 1a TASK",
    "is_done": false
  },
  {
    "id": 2,
    "title": "Mi 2a TASK",
    "is_done": true
  }
]
```

---

### Obtener una tarea por ID

**GET** `/tasks/:taskId`

Ejemplo:

```bash
curl http://localhost:3000/tasks/1
```

Respuesta:

```json
{
  "id": 1,
  "title": "Mi 1a TASK",
  "is_done": false
}
```

Si la tarea no existe:

```http
404 Not Found
```

## Modelo de datos

Las tareas utilizan la siguiente estructura:

```json
{
  "id": 1,
  "title": "Título de la tarea",
  "is_done": false
}
```

### Validación

La clase `Task` filtra automáticamente las propiedades no permitidas. Actualmente solo se conservan:

* `id`
* `title`
* `is_done`

Cualquier otro campo recibido será descartado.

## Datos iniciales

Al arrancar la aplicación se cargan dos tareas de ejemplo:

```json
[
  {
    "id": 1,
    "title": "Mi 1a TASK",
    "is_done": false
  },
  {
    "id": 2,
    "title": "Mi 2a TASK",
    "is_done": true
  }
]
```

## Limitaciones actuales

* Los datos se almacenan únicamente en memoria.
* No existe persistencia en base de datos.
* Solo están implementadas operaciones de consulta (`GET`).
* No hay autenticación ni autorización.

## Mejoras futuras

* Crear tareas (`POST /tasks`)
* Actualizar tareas (`PUT /tasks/:id`)
* Eliminar tareas (`DELETE /tasks/:id`)
* Persistencia en base de datos
* Validación avanzada de datos
* Tests automatizados
* Documentación OpenAPI / Swagger

## Tecnologías utilizadas

* Node.js 20
* Express 5
* Yarn
* Docker
* Docker Compose

```
```
