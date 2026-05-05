# Step 02 - Viewing Pods and Nodes (troubleshooting basico)

## Objetivo del step

Seguir el flujo del segundo lab oficial para inspeccionar la app desplegada:

- revisar Pods y Node
- usar `describe`, `logs`, `exec`
- acceder via `kubectl proxy`

## Fundamento del step

Antes de exponer servicios, hay que dominar diagnostico basico del workload.

## Ejecución guiada

### 1) Ver Pods del namespace

```bash
kubectl -n k8s-basics get pods
```

### 2) Inspeccionar detalle del Pod

```bash
kubectl -n k8s-basics describe pods
```

### 3) Ver logs del contenedor

```bash
kubectl -n k8s-basics logs -l app=kubernetes-bootcamp
```

### 4) Levantar proxy de API (terminal 1)

```bash
kubectl proxy
```

### 5) Consultar app via proxy (terminal 2)

```bash
POD_NAME="$(kubectl -n k8s-basics get pods -o go-template='{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}' | head -n 1)"
echo "POD_NAME=$POD_NAME"
curl "http://localhost:8001/api/v1/namespaces/k8s-basics/pods/${POD_NAME}:8080/proxy/"
```

### 6) Ejecutar comando dentro del Pod

```bash
kubectl -n k8s-basics exec "$POD_NAME" -- env
```

## Qué validas y qué debes ver

- `describe` muestra imagen y eventos de scheduling.
- `logs` devuelve salida de la app.
- `curl` por proxy responde correctamente.

## Errores comunes

- No dejar `kubectl proxy` corriendo mientras haces `curl`.
- Olvidar `-n k8s-basics`.

## Reto

Abre shell interactiva en el pod y prueba `curl http://localhost:8080`.

## Solución del reto

```bash
kubectl -n k8s-basics exec -ti "$POD_NAME" -- bash
curl http://localhost:8080
exit
```

## Navegacion del libro

- [Anterior](01-manifests-base.md)
- [Siguiente](03-kustomize-overlay.md)
