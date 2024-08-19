
![Screenshot 2024-07-30 at 6 25 34 AM](https://github.com/user-attachments/assets/615c0e6b-c4c2-499d-ae8e-0542af2becea)

## Install nginx ingress controller 
[link](https://kubernetes.github.io/ingress-nginx/deploy/#azure)
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
```

## Install CERT MANAGER
[link](https://cert-manager.io/docs/installation/kubectl/)
```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.14.5/cert-manager.yaml
```

## Install Metrics server
[link](https://github.com/kubernetes-sigs/metrics-server)
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

************************************************************************************************************************************************************************************


## Install cloudnative PG
[link](https://cloudnative-pg.io/documentation/current/installation_upgrade/)
```
kubectl apply --server-side -f \
  https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/release-1.23/releases/cnpg-1.23.1.yaml
```

************************************************************************************************************************************************************************************


## create Database cluster
```
kubectl apply -f postgres-cluster.yaml
```

## Exec into pod to create table
```
kubectl exec -it my-postgresql-1 -- /bin/sh
```

```
psql -U postgres -c "ALTER USER goals_user WITH PASSWORD 'new_password';"
```

```
PGPASSWORD='new_password' psql -h my-postgresql-1 -U goals_user -d goals_database -c "
CREATE TABLE goals (
    id SERIAL PRIMARY KEY,
    goal_name VARCHAR(255) NOT NULL
);
"
```
