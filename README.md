# k8artifacts
Laboratório Prático FIAP: Artefatos Kubernetes
# 🚀 Live FIAP: Entendendo Artefatos de Kubernetes no AWS EKS
Este repositório contém o guia prático e os manifestos utilizados na aula sobre Artefatos de Kubernetes. O objetivo é demonstrar a criação de um cluster gerenciado (EKS), o deploy de aplicações e o ciclo de vida dos artefatos (Deployments, Services e Rollouts).

📋 Pré-requisitos
Conta ativa na AWS Academy.

Acesso ao AWS CloudShell na região us-east-1.

#  🏗️ 1. Preparação do Ambiente (CloudShell)
Como o CloudShell é um ambiente temporário, precisamos instalar as ferramentas necessárias (eksctl e k9s).

# Instalação do eksctl
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin

# Instalação do k9s (Interface Visual)
curl -sL https://github.com/derailed/k9s/releases/download/v0.32.4/k9s_Linux_amd64.tar.gz | tar xz
sudo mv k9s /usr/local/bin

# ☁️ 2. Criando o Cluster EKS (Foco AWS Academy)
Para rodar no ambiente da Academy, precisamos utilizar a LabRole pré-existente.

Crie o arquivo cluster.yaml:

nano cluster.yaml

Utilize o conteúdo do arquivo cluster.yaml deste repositório (Substitua o Account ID pelo Account ID da sua conta AWS):
    
Execute a criação (Tempo estimado: 15-20 min):

eksctl create cluster -f cluster.yaml

# 📦 3. Mão na Massa: Artefatos K8s
Deployment e Service (v1)
Crie o arquivo app.yaml para subir nossa aplicação inicial (utilize o arquivo deste repositório)

# Comandos:

# Aplicar artefatos
kubectl apply -f app.yaml

# Verificar DNS do Load Balancer
kubectl get svc web-service

# 🔄 4. Ciclo de Vida: Rolling Update e Rollback
Atualizar Versão (Rolling Update): Observe no k9s os pods sendo substituídos um a um.

kubectl set image deployment/web-server nginx-container=nginx:1.25

Simular Erro:

kubectl set image deployment/web-server nginx-container=nginx:imagem-que-nao-existe

Desfazer Alteração (Rollback):

kubectl rollout undo deployment/web-server

# 🗑️ 5. Limpeza (Obrigatório)
Ao final da aula, delete o cluster para evitar consumo de créditos.

eksctl delete cluster -f cluster.yaml

# 🎓 Instrutor
Luiz Reche Professor FIAP - Cloud Architecture & DevOps
