```
# first keti into test container (/test/man.yaml)
keti pod/metricsmultiplexer-test-6ff8c89c65-jrt27 -c test -- sh

# save token
echo -n "Authorization: Bearer " > /token
cat /var/run/secrets/kubernetes.io/serviceaccount/token >> /token

# test CWA directly
curl --insecure -vsSL -H @/token https://k8s-cloudwatch-adapter.custom-metrics.svc.cluster.local/apis/external.metrics.k8s.io/v1beta1/namespaces/xenos/xenos-activities-count

# test through multiplexer
curl --insecure -vsSL -H @/token https://metricsmultiplexer.external-metrics-multiplexer.svc.cluster.local/apis/external.metrics.k8s.io/v1beta1/namespaces/xenos/xenos-activities-count
```
