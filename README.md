# Kubernete for ELK

- Deploy Elasticsearch

```
kubectl apply -f es.yml
```

- Create secret

```
ESPWD=$(kubectl get secret elk-es-elastic-user -o go-template='{{.data.elastic | base64decode}}')
kubectl create secret generic kibana-elasticsearch-credentials --from-literal=elasticsearch.password=$ESPWD
```

- Deploy kibana

```
kubectl apply -f kinana.yml
```
