# Kubernete for ELK

- Deploy Elasticsearch

```
kubectl apply -f es.yml
```

- Create secret

```
ESPWD=$(kubectl get secret elk-es-elastic-user -o go-template='{{.data.elastic | base64decode}}')
kubectl create secret generic kibana-elasticsearch-credentials --from-literal=elasticsearch.password=$ESPWD

kubectl create secret docker-registry docker-secret \
--docker-server="https://index.docker.io/v1/" \
--docker-username=`aws secretsmanager get-secret-value --secret-id  dockerHub --query "SecretString" --output text|jq --raw-output -c '.username'` \
--docker-password=`aws secretsmanager get-secret-value --secret-id  dockerHub --query "SecretString" --output text|jq --raw-output -c '.password'`
```

- Deploy kibana

```
kubectl apply -f kinana.yml
```
