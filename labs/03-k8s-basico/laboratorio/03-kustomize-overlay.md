# Step 03 - Using a Service to expose your app (con manifiestos)

## Objetivo del step

Replicar el tercer lab oficial (Service + labels + borrado), pero sin `kubectl expose`.

## Fundamento del step

`Service` da red estable y balanceo para Pods efimeros. Lo definimos en YAML para poder versionarlo.

## Ejecución guiada

### 1) Crear manifiesto `02-service.yaml`

Archivo: `labs/03-k8s-basico/trabajo/k8s/manifests/02-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: kubernetes-bootcamp
  namespace: k8s-basics
  labels:
    app: kubernetes-bootcamp
spec:
  type: NodePort
  selector:
    app: kubernetes-bootcamp
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30080
```

### 2) Aplicar el Service y verificar

```bash
kubectl apply -f labs/03-k8s-basico/trabajo/k8s/manifests/02-service.yaml
kubectl -n k8s-basics get services
kubectl -n k8s-basics describe services kubernetes-bootcamp
```

### 3) Consultar por labels

```bash
kubectl -n k8s-basics get pods -l app=kubernetes-bootcamp
kubectl -n k8s-basics get services -l app=kubernetes-bootcamp
```

### 4) Añadir label al Pod (como en lab oficial)

```bash
POD_NAME="$(kubectl -n k8s-basics get pods -o go-template='{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}' | head -n 1)"
kubectl -n k8s-basics label pods "$POD_NAME" version=v1 --overwrite
kubectl -n k8s-basics get pods -l version=v1
```

### 5) Validar acceso de la app

Opcion A (NodePort, kind):

```bash
curl -sS http://localhost:30080/
```

Opcion B (si no abre NodePort en tu host):

```bash
kubectl -n k8s-basics port-forward service/kubernetes-bootcamp 8080:8080
curl -sS http://127.0.0.1:8080/
```

### 6) Eliminar Service y comprobar efecto

```bash
kubectl -n k8s-basics delete service -l app=kubernetes-bootcamp
kubectl -n k8s-basics get services
```

La app seguira viva porque el `Deployment` sigue gestionando los Pods.

## Qué validas y qué debes ver

- `Service` creado con `NodePort`.
- Labels funcionando para filtrar pods/services.
- Tras borrar Service, Pods siguen en `Running`.

## Errores comunes

- `nodePort` fuera de rango.
- Selector no coincide con label `app`.
- Probar `localhost:30080` cuando tu entorno no publica NodePort al host.

## Reto

Recrear el Service cambiando `nodePort` a `30081` y validar de nuevo.

## Solución del reto

Edita el YAML y cambia:

```yaml
nodePort: 30081
```

Luego:

```bash
kubectl apply -f labs/03-k8s-basico/trabajo/k8s/manifests/02-service.yaml
kubectl -n k8s-basics get svc kubernetes-bootcamp
```

## Navegacion del libro

- [Anterior](02-deploy-y-validar.md)
- [Siguiente](../../04-k8s-analitica/README.md)
