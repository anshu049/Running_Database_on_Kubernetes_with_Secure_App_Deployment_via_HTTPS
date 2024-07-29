## Install nginx ingress controller 
[link](https://kubernetes.github.io/ingress-nginx/deploy/#azure)
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
```

************************************************************************************************************************************************************************************


## Install cloudnative PG
[link](https://cloudnative-pg.io/documentation/current/installation_upgrade/)
```
kubectl apply --server-side -f \
  https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/release-1.23/releases/cnpg-1.23.1.yaml
```

====================================================================================================================================================================================


## create Database cluster
`kubectl apply -f postgres-cluster.yaml`
## Create secret 
```
kubectl create secret generic my-postgresql-credentials --from-literal=password='new_password'  --from-literal=username='goals_user'  --dry-run=client -o yaml | kubectl apply -f -
```

## Exec into pod to create table

```
kubectl exec -it my-postgresql-1 -- psql -U postgres -c "ALTER USER goals_user WITH PASSWORD 'new_password';"
kubectl port-forward my-postgresql-1 5432:5432
PGPASSWORD='new_password' psql -h 127.0.0.1 -U goals_user -d goals_database -c "

CREATE TABLE goals (
    id SERIAL PRIMARY KEY,
    goal_name VARCHAR(255) NOT NULL
);
"
```

====================================================================================================================================================================================


## Install CERT MANAGER
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.14.5/cert-manager.yaml


## Install Metrics server
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
