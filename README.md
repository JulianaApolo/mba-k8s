# Exercício da Aula de Kubernetes

Subir dois pods, nginx e mysql, mapeando a porta 80 do nginx para acesso externo ao cluster e permitir que o contêiner do nginx tenha comunicação de rede no contêiner mysql pela porta 3306.


# Resolução

- Instale o [minikube](https://minikube.sigs.k8s.io/docs/start/) para prover um cluster kubernetes local em sua máquina e o [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) em seu computador

- Inicie o minikube
```
minikube start
```

- Inicie o pod do nginx
```
kubectl apply -f pod-nginx.yaml
```

- Inicie o serviço
```
kubectl apply -f service-nginx.yaml
```

- Inicie o volume para o mysql
```
kubectl apply -f pv-mysql.yaml
```

- Inicie o pod do mysql
```
kubectl apply -f pod-mysql.yaml
```

## Acessando o servidor nginx

- Pegue o ip do serviço no minikube
```
minikube service nginx --url
```

- Abra no navegador a url para acessar o nginx

## Acessando o mysql através do container ngix

- Pegue o ip do pod do Mysql
```
kubectl get all -o wide
```

- Acesse a linha de comando do pod do nginx
```
kubectl exec -it pod/pod-nginx -- bash
```

- Instale o cliente mysql
```
apt update && apt install -y default-mysql-client
```

- Acesse o mysql
```
mysql -h <IP_DO_POD_MYSQL> -u root -ppassword
```

## Removendo e desligando o cluster
```
minikube delete
minikube stop
```
