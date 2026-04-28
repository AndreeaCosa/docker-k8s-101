# Step 01 - Estructura del stack

## Objetivo del step

Crear una base de proyecto limpia y consistente para levantar un stack analítico con API, base de datos y ETL.

## Contexto

Antes de ejecutar servicios, necesitas una estructura clara. Esto evita errores de rutas en Dockerfile/Compose y facilita depuración.

## Preparación

Trabaja desde la raíz del repositorio.

```bash
pwd
```

## Ejecución guiada

### 1) Crear carpetas principales

```bash
mkdir -p labs/02-docker-analitica/trabajo/stack-analitica/api/app
mkdir -p labs/02-docker-analitica/trabajo/stack-analitica/etl
```

### 2) Crear archivo de variables de entorno

Crea `labs/02-docker-analitica/trabajo/stack-analitica/.env`:

```env
POSTGRES_USER=analytics
POSTGRES_PASSWORD=analytics
POSTGRES_DB=analytics
DATABASE_URL=postgresql+psycopg://analytics:analytics@db:5432/analytics
```

### 3) Crear esqueleto de archivos de servicios

```bash
touch labs/02-docker-analitica/trabajo/stack-analitica/api/Dockerfile
touch labs/02-docker-analitica/trabajo/stack-analitica/api/requirements.txt
touch labs/02-docker-analitica/trabajo/stack-analitica/api/app/main.py
touch labs/02-docker-analitica/trabajo/stack-analitica/etl/Dockerfile
touch labs/02-docker-analitica/trabajo/stack-analitica/etl/requirements.txt
touch labs/02-docker-analitica/trabajo/stack-analitica/etl/etl.py
touch labs/02-docker-analitica/trabajo/stack-analitica/docker-compose.yml
```

## Qué validas y qué debes ver

- La carpeta `stack-analitica` contiene `api/`, `etl/` y `docker-compose.yml`.
- El archivo `.env` existe con valores completos.

```bash
ls -R labs/02-docker-analitica/trabajo/stack-analitica
```

## Errores comunes

- Crear carpetas en la ruta equivocada (solución: rehacer desde la raíz).
- Escribir `DATABASE_URL` con `localhost` en lugar de `db`.

## Reto

Añade una carpeta `docs/` dentro de `stack-analitica` y crea un `README.md` con una línea explicando la arquitectura.

## Solución del reto

```bash
mkdir -p labs/02-docker-analitica/trabajo/stack-analitica/docs
echo "Stack: API + DB + ETL" > labs/02-docker-analitica/trabajo/stack-analitica/docs/README.md
```

## Navegacion del libro

- [Anterior](../03-compose-api-db-etl.md)
- [Siguiente](02-compose-up.md)
