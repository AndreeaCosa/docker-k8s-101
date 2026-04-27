# Docker y Kubernetes Inicial (Hospital de Bellvitge)

Curso de entrada, orientado a analistas y perfiles de datos, con enfoque de uso practico:

- 70% laboratorio guiado.
- 30% teoria minima y contextual.
- Sin necesidad de experiencia previa en DevOps.

## Objetivo del repositorio

Este repositorio esta preparado para que cada alumno:

1. Haga un fork.
2. Lance un Codespace.
3. Complete los labs paso a paso con instrucciones claras.

## Estructura

- `docs/modulos/`: guias por modulo (teoria breve + practica).
- `docs/guias/`: hojas de ruta para alumnos.
- `docs/instructor/`: notas para dinamica de sesiones.
- `labs/`: practicas por bloques, incluyendo prework y proyecto final.
- `plantillas/`: base reusable para Dockerfile, Compose y Kubernetes.
- `soluciones/`: referencia para instructor (o publicacion diferida).
- `assets/datasets/`: datasets de ejemplo.

## Ruta de aprendizaje

1. `labs/00-prework`: validacion de entorno.
2. `labs/01-docker-basico`: contenedores, imagenes, volumenes.
3. `labs/02-docker-analitica`: notebook + API + base de datos.
4. `labs/03-k8s-basico`: Pods, Deployments, Services.
5. `labs/04-k8s-analitica`: Jobs, CronJobs, ConfigMaps, Secrets.
6. `labs/05-proyecto-final`: flujo end-to-end guiado.

## Modo de trabajo recomendado para alumnos

- Leer objetivo del lab.
- Ejecutar pasos guiados.
- Validar con checklist.
- Entregar evidencia minima (captura/log/comando).

## GitHub y Codespaces

Repositorio oficial del curso:

- https://github.com/davidpestana/docker-kubernetes-inicial-bellvitge

Flujo recomendado para alumnos:

1. Entrar al repo y pulsar `Fork`.
2. Abrir el fork y pulsar `Code` -> `Codespaces` -> `Create codespace on main`.
3. Ejecutar `labs/00-prework` para validar el entorno del curso.
