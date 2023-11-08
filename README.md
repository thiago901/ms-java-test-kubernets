
**PT:**

```markdown
# Criar o Cluster com as Configurações do Ingress
## Requisitos

- Docker
- kind
- helm
- kubectl

Será configurado um Ingress para receber as requisições na porta 8080 do host e encaminhá-las para a porta 80 do container

```bash
kind create cluster -n ms-test-java-cluster --config=createClusterWithIngress.yaml
```

# Instalar o Controlador Nginx
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

# Instalar a Aplicação via Helm
Tem um arquivo chamado "env.yaml.exemple" você deve fornecer as variaveis do Rabbit e do Mongo e renomear para env.yaml
```bash
helm install ms-java-test ./helm-application/ms-java-test-helm/ --values=./env.yaml
```

## Painel de Controle
### Instale o Dashboard
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
<!-- kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml -->
```

### Crie uma Conta de Serviço
```bash
kubectl apply -f ./dashboard/CreateServiceAccount.yaml
```

### Crie uma Associação de Função de Cluster
```bash
kubectl apply -f ./dashboard/CreateClusterRoleBinding.yaml
```

### Obtenção de um Token de Portador para a Conta de Serviço
Guarde o token gerado, pois será utilizado na interface como login
```bash
kubectl -n kubernetes-dashboard create token admin-user
```

### Execute o Comando para Obter o IP do Painel
```bash
kubectl proxy
```

### Endereço
```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
```

**EN:**

```markdown
# Create the Cluster with Ingress Configuration
## Requirements

- Docker
- kind
- helm
- kubectl

An Ingress will be configured to receive requests on port 80 of the host and forward them to port 8080 (the port the image exposes).

```bash
kind create cluster -n ms-test-java-cluster --config=createClusterWithIngress.yaml
```

# Install Nginx Controller
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

# Install Application via Helm
```bash
helm install ms-java-test ./helm-application/ms-java-test-helm/ --values=./env.yaml
```

## Dashboard
### Install the Dashboard
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
<!-- kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml -->
```

### Create a Service Account
```bash
kubectl apply -f ./dashboard/CreateServiceAccount.yaml
```

### Create a Cluster Role Binding
```bash
kubectl apply -f ./dashboard/CreateClusterRoleBinding.yaml
```

### Obtain a Bearer Token for the Service Account
```bash
kubectl -n kubernetes-dashboard create token admin-user
```

### Run the Command to Get the Dashboard IP
```bash
kubectl proxy
```

### Address
```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
```