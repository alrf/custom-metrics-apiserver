Example Deployment
==================

Create k8s cluster using kops, for example:

```
kops create cluster --zones=us-east-2a --image=ami-e1496384 --node-count=3 --node-size=t2.large --master-size=t2.small $NAME --cloud=aws --topology=public --kubernetes-version=1.10.1
```
`$NAME` - is your cluster name.

Edit the cluster by:
```
kops edit cluster $NAME
```
Add the following lines into `spec`:
```
  kubeControllerManager:
    horizontalPodAutoscalerSyncPeriod: 15s
    horizontalPodAutoscalerUseRestClients: true
  kubelet:
    enableCustomMetrics: true
```
Save the cluster settings. 
Update cluster with creation:

```
kops update cluster $NAME --yes
```


1. Make sure you've built the included Dockerfile with `make docker-build`.
Push your image to Docker Hub:
```
docker login
```
```
docker push alrf/custom-metrics-apiserver-amd64
```
   
2. `kubectl create namespace custom-metrics`

3. `openssl req -newkey rsa:2048 -x509 -out /tmp/serving.crt -keyout /tmp/serving.key -nodes -days 9999`

4. `kubectl -n custom-metrics create secret tls cm-adapter-serving-certs --cert=/tmp/serving.crt --key=/tmp/serving.key`

5. `kubectl apply -f deploy/manifests`

```
$ kubectl api-versions |grep cus
custom.metrics.k8s.io/v1beta1
```

```
kubectl get svc --all-namespaces
```


```
kubectl get --raw /apis/external.metrics.k8s.io/v1beta1/namespaces/default/mongo-queue
```

Build flask service:

1. `kubectl apply -f scaler/flask.yaml` - flask
2. `kubectl apply -f scaler/horizontalpodautoscaler.yaml` - HPA
