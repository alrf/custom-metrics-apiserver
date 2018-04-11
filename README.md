# Custom Metrics Adapter Server Boilerplate


# Usage
  * Build the code: `make docker-build`
  * Create the necessary resources: `kubectl apply -f deploy/manifests/`
  * Create the necessary Secrets: `kubectl -n custom-metrics create secret tls cm-adapter-serving-certs --cert=apiserver.local.config/certificates/serving.crt --key=apiserver.local.config/certificates/serving.key`
  * See if our server actually works: `kubectl run -it --rm toolbox --restart=Never --image stevemcquaid/toolbox:latest -- curl -sSk 'https://custom-metrics-apiserver.custom-metrics/apis/custom.metrics.k8s.io/v1beta1/namespaces/default/service/flask/queue-length'`









## Compatibility

The APIs in this repository follow the standard guarantees for Kubernetes
APIs, and will follow Kubernetes releases.

## Community, discussion, contribution, and support

Learn how to engage with the Kubernetes community on the [community
page](http://kubernetes.io/community/).

You can reach the maintainers of this repository at:

- Slack: #sig-instrumentation (on https://kubernetes.slack.com -- get an
  invite at slack.kubernetes.io)
- Mailing List:
  https://groups.google.com/forum/#!forum/kubernetes-sig-instrumentation

### Code of Conduct

Participation in the Kubernetes community is governed by the [Kubernetes
Code of Conduct](code-of-conduct.md).

### Contribution Guidelines

See [CONTRIBUTING.md](CONTRIBUTING.md) for more information.
