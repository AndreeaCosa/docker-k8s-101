# Step 01 - Using kubectl to create a Deployment (con manifiestos)

## Objetivo del step

Replicar el lab oficial de "create deployment", pero en modo declarativo:

- crear `Namespace`
- definir `Deployment` en YAML
- aplicar con `kubectl apply`

## Fundamento del step

En el tutorial oficial se usa `kubectl create deployment`. Aqui conseguimos el mismo resultado, pero con manifiestos versionables.

## Ejecución guiada

### 1) Verificar cluster y nodos

```bash
kubectl version
kubectl get nodes
```

### 2) Crear estructura de manifiestos

```bash
mkdir -p labs/03-k8s-basico/trabajo/k8s/manifests
```

### 3) Crear `00-namespace.yaml`

Archivo: `labs/03-k8s-basico/trabajo/k8s/manifests/00-namespace.yaml`

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: k8s-basics
```

### 4) Crear `01-deployment.yaml`

Archivo: `labs/03-k8s-basico/trabajo/k8s/manifests/01-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubernetes-bootcamp
  namespace: k8s-basics
  labels:
    app: kubernetes-bootcamp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kubernetes-bootcamp
  template:
    metadata:
      labels:
        app: kubernetes-bootcamp
    spec:
      containers:
        - name: kubernetes-bootcamp
          image: gcr.io/google-samples/kubernetes-bootcamp:v1
          ports:
            - containerPort: 8080
```

### 5) Aplicar manifiestos

```bash
kubectl apply -f labs/03-k8s-basico/trabajo/k8s/manifests/00-namespace.yaml
kubectl apply -f labs/03-k8s-basico/trabajo/k8s/manifests/01-deployment.yaml
```

### 6) Verificar el deployment creado

```bash
kubectl -n k8s-basics get deployments
kubectl -n k8s-basics get pods
```

## Qué validas y qué debes ver

- `kubernetes-bootcamp` aparece en `get deployments`.
- Se crea al menos 1 Pod en `Running`.

## Errores comunes

- Olvidar `namespace: k8s-basics` en el Deployment.
- Error tipografico en la imagen.

## Reto

Sube replicas a 2 en el manifiesto y vuelve a aplicar.

## Solución del reto

En `01-deployment.yaml`:

```yaml
replicas: 2
```

Y aplica:

```bash
kubectl apply -f labs/03-k8s-basico/trabajo/k8s/manifests/01-deployment.yaml
```

## Navegacion del libro

- [Anterior](../03-kustomize-base-overlays.md)
- [Siguiente](02-deploy-y-validar.md)
