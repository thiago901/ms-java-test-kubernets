# Instale o Dashboard
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
  <!-- kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml -->


# Crie uma conta de servico
  kubectl apply -f ./CreateServiceAccount.yaml

# Crie uma conta de cluster role binding
  kubectl apply -f ./CreateClusterRoleBinding.yaml



# Obtendo um token de portador para ServiceAccount

kubectl -n kubernetes-dashboard create token admin-user


# rode o comando para gerar o ip do dash
  kubectl proxy

# endereço

{server ip:port}/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login