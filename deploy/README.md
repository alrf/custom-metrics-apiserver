Example Deployment
==================

1. Make sure you've built the included Dockerfile with `make docker-build`.
   
2. `kubectl create namespace custom-metrics`

3. `openssl req -newkey rsa:2048 -x509 -out /tmp/serving.crt -keyout /tmp/serving.key -nodes -days 9999`

4. `kubectl -n custom-metrics create secret tls cm-adapter-serving-certs --cert=/tmp/serving.crt --key=/tmp/serving.key`

5. `kubectl apply -f manifests/`

```
$ kubectl api-versions |grep cus
custom.metrics.k8s.io/v1beta1
```


Build flask service:

1. `kubectl apply -f scaler/flask.yaml` - flask
2. `kubectl apply -f scaler/horizontalpodautoscaler.yaml` - HPA
