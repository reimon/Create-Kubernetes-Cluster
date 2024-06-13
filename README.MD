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

# Configuração da INFRA no Azure

Este guia descreve os comandos necessários para criar um grupo de recursos, uma rede virtual e uma máquina virtual no Azure, incluindo a configuração necessária para um cluster Kubernetes.

## Comandos

### 1. Criar um Grupo de Recursos

```sh
az group create --name cluster-k8s --location brazilSouth
```

--az group create: Cria um novo grupo de recursos no Azure.
--name cluster-k8s: Define o nome do grupo de recursos como "cluster-k8s".
--location brazilSouth: Especifica a localização do grupo de recursos como "Brazil South".

### 2. Criar uma Virtual Network

Este comando criará a VNet "VNET-K8S" no grupo de recursos "cluster-k8s" na região "Brazil South".

```sh
az network vnet create --resource-group cluster-k8s --name VNET-K8S --address-prefix 10.0.0.0/16 --location brazilSouth
```

-- `az network vnet create`: Comando para criar uma Virtual Network no Azure.
-- `resource-group cluster-k8s`: Especifica o grupo de recursos onde a VNet será criada.
-- `name VNET-K8S`: Define o nome da VNet como "VNET-K8S".
-- `address-prefix 10.0.0.0/16`: Define o prefixo de endereço da VNet.
-- `location brazilSouth`: Especifica a localização da VNet como "Brazil South".

### 3. Criar uma VM no Azure

```sh
az vm create \
  --resource-group cluster-k8s \
  --name VM-K8S-CP \
  --image Canonical:0001-com-ubuntu-minimal-jammy:minimal-22_04-lts-gen2:22.04.202305240 \
  --size Standard_B2s \
  --vnet-name VNET-K8S \
  --subnet default \
  --public-ip-address "" \
  --public-ip-address-allocation static \
  --public-ip-sku Standard \
  --os-disk-size-gb 30 \
  --os-disk-type StandardSSD_LRS \
  --admin-username svc_Linux \
  --admin-password FIAP@MBA@K8S@2024! \
  --location brazilSouth
```

`--az vm create`: Cria uma nova máquina virtual no Azure.
--resource-group cluster-k8s: Especifica o grupo de recursos.
--name VM-K8S-CP: Define o nome da VM.
--image Canonical:0001-com-ubuntu-minimal-jammy:minimal-22_04-lts-gen2:22.04.202305240: Usa a imagem Ubuntu 22.04 minimal gen2.
--size Standard_B2s: Especifica o tamanho da VM com 2 vCPUs e 4 GiB de RAM.
--vnet-name VNET-K8S: Conecta a VM à VNet existente.
--subnet default: Usa a sub-rede padrão.
--public-ip-address "": Cria um IP público para a VM.
--public-ip-address-allocation static: Define o IP público como estático.
--public-ip-sku Standard: Usa o SKU Standard para o IP público.
--os-disk-size-gb 30: Define o tamanho do disco do SO para 30 GB.
--os-disk-type StandardSSD_LRS: Usa o tipo de disco SSD Standard.
--admin-username svc_Linux: Define o nome de usuário administrador.
--admin-password FIAP@MBA@K8S@2024!: Define a senha do usuário administrador.
--location brazilSouth: Especifica a localização..
-- location brazilSouth: Especifica a localização.

### 🔧 Instalação do Kubernetes

Clone este repositório e navegue até o diretório:

```bash
git clone https://github.com/reimon/Create-Kubernetes-Cluster.git
cd Create-Kubernetes-Cluster

chmod +x setup_k8s_cluster
./setup_k8s_cluster
```

## Passos do Script

### 1. Carregamento dos Módulos Necessários

Carregamos os módulos overlay e br_netfilter necessários para o funcionamento do Kubernetes.

### 2. Configuração dos Parâmetros sysctl

Configurações sysctl são aplicadas para permitir o roteamento de pacotes IP e o processamento de iptables no tráfego de ponte de rede.

### 3. Instalação do containerd

O runtime containerd é instalado e configurado.

### 4. Desativação do Swap

O swap é desativado.

### 5. Instalação das Dependências do Kubernetes

Instalamos o kubeadm, kubelet e kubectl nas versões especificadas.

### 6. Inicialização do Cluster Kubernetes

Finalmente, inicializamos o cluster Kubernetes com o kubeadm.

### 7. Configuração do Diretório .kube

O script cria o diretório .kube e copia o arquivo de configuração do Kubernetes para ele.

### 8. Aplica a configuração de rede Calico

```sh
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

```

Contribuições
Sinta-se à vontade para abrir issues e pull requests para melhorias e correções.

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo LICENSE para mais informações.
