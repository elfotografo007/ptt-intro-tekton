# Introducción a Tekton CI/CD

Primero necesitamos un clúster de Kubernetes. Si no tenemos uno, se puede usar `kind`
```
kind create cluster
```

Ahora instalamos Tekton
```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
```

Instalamos el Dashboard de Tekton (opcional)
```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release-full.yaml
```

Ahora le hacemos port-forward al dashboard
```
kubectl --namespace tekton-pipelines port-forward svc/tekton-dashboard 9097:9097
```

Podemos accederlo a través de http://localhost:9097

Ahora procedemos a instalar unas tareas que necesitaremos desde [Tekton Hub](https://hub.tekton.dev/)

```
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.9/git-clone.yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/kaniko/0.6/kaniko.yaml
```

Ahora podemos instalar nuestro primer `Pipeline`

```
kubectl apply -f node-example.yaml
```

Corramos una instancia del pipeline:
```
kubectl apply -f node-example-run.yaml
```

Podemos ver el estado haciendo:
```
kubectl get pr
```

Luego un `Pipeline` más complicado en go usando [GCP Samples](https://github.com/GoogleCloudPlatform/golang-samples/tree/main/run/helloworld):
```
kubectl apply -f go-example.yaml
kubectl apply -f go-example-run.yaml
```