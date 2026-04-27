# Lab 03 - Kubernetes Basico

## Objetivo

Desplegar una aplicacion en Kubernetes y exponerla por servicio interno.

## Prerrequisitos

- Haber completado `labs/00-prework`.
- Tener cluster `kind` activo:

```bash
kind get clusters
kubectl get nodes
```

## Pasos guiados

1. Aplicar `deployment.base.yaml`.
2. Aplicar `service.base.yaml`.
3. Verificar pods y replicas.
4. Escalar deployment y validar.
