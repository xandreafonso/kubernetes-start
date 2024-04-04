# INSTALAR O K3D

```shell
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

# COMANDOS K3D

```shell
# Cria um cluster com nome padrão
k3d cluster create

# Cria um cluster com um nome específico
k3d cluster create meucluster

# Servers são os control planes e agents são so worker nodes
k3d cluster create meucluster --servers 3 --agents 3

# fazer o bind de porta com uma máquina do cluster
# para verficar esse bind basta rodar docker ps
k3d cluster create meucluster -p "30000:30000@loadbalancer"

k3d cluster list

# Deleta o cluster de nome padrão
k3d cluster delete
```

# INSTALAR O KUBECTL

```shell
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

# COMANDOS KUBECTL

```shell
# lista as máquinas do cluster
kubectl get nodes

# lista os pods
kubectl get pods

# acessar o container
kubectl port-forward pod/nomepodevejagetpods 8080:80

# remover
kubectl delete pod nginx
kubectl delete rs nginx-replicaset

# listar replicaset
kubctl get rs

# listar deployments (deployment ou deployments)
kubectl get deployments

# listar serviços
kubctl get svc

# acessar o serviço (acessar os container pelo serviço)
kubectl port-forward service/nomeservico 8080:80

# lista tudo
kubectl get all

# Lista os recursos (tem a ver com apiVersion e kind do yaml)
kubectl api-resources | grep deployment

# listar histórico
kubectl rollout history deployment web

# voltar versão anterior (se a nova der problema)
kubectl rollout undo deployment web & watch 'kubectl get pod'
```

## COMANDOS PARA APLICAR

```shell
# caso queira rodar apenas os pods
kubectl apply -f pod.yaml

# caso queira rodar os pods pelo replicaset
kubectl apply -f replicaset.yaml

# caso queira rodar os pods pelo deployment
kubectl apply -f deployment.yaml

# para rodar o service que fará o balanceamento de carga
kubectl apply -f service.yaml
```