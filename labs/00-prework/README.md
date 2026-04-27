# Lab 00 - Prework

## Objetivo

Dejar el entorno del Codespace listo para trabajar con Docker y Kubernetes, instalando herramientas de forma guiada para entender que hace cada una.

## Pasos guiados

### Paso 1 - Verificar Docker y Compose

Por que: Docker es la base sobre la que `kind` crea nodos Kubernetes como contenedores.

```bash
docker --version
docker compose version
docker ps
```

Resultado esperado:

- `docker --version` devuelve version sin error.
- `docker compose version` devuelve version sin error.
- `docker ps` responde (aunque no haya contenedores).

### Paso 2 - Instalar kubectl

Por que: `kubectl` es el cliente para enviar comandos al cluster Kubernetes.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

Resultado esperado:

- `kubectl version --client` muestra version del cliente.

### Paso 3 - Instalar kind

Por que: `kind` permite crear un cluster Kubernetes local para practicar sin infraestructura externa.

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
kind --version
```

Resultado esperado:

- `kind --version` devuelve la version instalada.

### Paso 4 - Instalar Helm

Por que: Helm simplifica despliegues repetibles sobre Kubernetes mediante charts.

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm version
```

Resultado esperado:

- `helm version` muestra version sin error.

### Paso 5 - Crear cluster local con kind

Por que: validar que todas las piezas (Docker + kind + kubectl) estan conectadas correctamente.

```bash
kind create cluster --name k8s-101
kubectl cluster-info
kubectl get nodes
```

Resultado esperado:

- `kubectl cluster-info` muestra endpoint del cluster.
- `kubectl get nodes` muestra al menos 1 nodo en estado `Ready`.

### Paso 6 - Test rapido de despliegue

Por que: comprobar que el cluster ejecuta workloads reales.

```bash
kubectl create deployment hello-nginx --image=nginx:1.27
kubectl expose deployment hello-nginx --port=80 --target-port=80 --type=ClusterIP
kubectl get deploy,pods,svc
```

Resultado esperado:

- Deployment y pod en estado estable.
- Servicio `hello-nginx` creado.

### Paso 7 - Limpieza para comenzar labs oficiales

Por que: dejar entorno limpio para los labs 01-05.

```bash
kubectl delete service hello-nginx
kubectl delete deployment hello-nginx
```

## Comprobacion

Checklist final:

- [ ] Docker y Compose operativos.
- [ ] kubectl instalado y funcional.
- [ ] kind instalado y cluster `k8s-101` creado.
- [ ] helm instalado y funcional.
- [ ] Test de despliegue realizado y eliminado.

Si todo esta en verde, pasa a `labs/01-docker-basico`.
