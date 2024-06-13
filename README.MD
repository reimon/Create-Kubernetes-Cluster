# 🚀 Kubernetes Cluster Initialization Script

<p align="center">
<a href="https://github.com/reimon"><img title="Author" src="https://img.shields.io/badge/Author-DeepSociety-svg?style=for-the-badge&logo=github"></a>
<a href="#"><img title="Open Source" src="https://img.shields.io/badge/Open%20Source-%E2%9D%A4-green?style=for-the-badge"></a>
</p>

![Kubernetes Logo](https://kubernetes.io/images/kubernetes-horizontal-color.png)

Este repositório contém um script para inicializar um cluster Kubernetes usando kubeadm, com containerd como runtime e configurações de rede necessárias.

### 📋 Pré-requisitos

Antes de executar o script, certifique-se de ter:

- Acesso root ou sudo no sistema
- Sistema operacional baseado em Linux (testado no Ubuntu 22.04)
- git instalado (apt-get install git -y )

### 🔧 Instalação

Clone este repositório e navegue até o diretório:

```bash
git clone https://github.com/reimon/Create-Kubernetes-Cluster.git
cd kubernetes-cluster-init

chmod +x setup_k8s_cluster.sh
./setup_k8s_cluster.sh
```

## Passos do Script

### 1. Configuração do Diretório .kube

O script cria o diretório .kube e copia o arquivo de configuração do Kubernetes para ele.

### 2. Carregamento dos Módulos Necessários

Carregamos os módulos overlay e br_netfilter necessários para o funcionamento do Kubernetes.

### 3. Configuração dos Parâmetros sysctl

Configurações sysctl são aplicadas para permitir o roteamento de pacotes IP e o processamento de iptables no tráfego de ponte de rede.

### 4. Instalação do containerd

O runtime containerd é instalado e configurado.

### 5. Desativação do Swap

O swap é desativado, pois não é suportado pelo Kubernetes.

### 6. Instalação das Dependências do Kubernetes

Instalamos o kubeadm, kubelet e kubectl nas versões especificadas.

### 7. Inicialização do Cluster Kubernetes

Finalmente, inicializamos o cluster Kubernetes com o kubeadm.

### 8. Aplica a configuração de rede Calico

```sh
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

```

Contribuições
Sinta-se à vontade para abrir issues e pull requests para melhorias e correções.

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo LICENSE para mais informações.
