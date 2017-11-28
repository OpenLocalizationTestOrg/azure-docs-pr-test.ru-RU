---
title: "Использование файловых ресурсов для кластера DC/OS Azure | Документация Майкрософт"
description: "Создание и подключение файлового ресурса к кластеру DC/OS в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 549b52bfb0a0268f754da26c6a374b267861f6d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="4a9d8-104">Создание и подключение файлового ресурса к кластеру DC/OS</span><span class="sxs-lookup"><span data-stu-id="4a9d8-104">Create and mount a file share to a DC/OS cluster</span></span>
<span data-ttu-id="4a9d8-105">В этом руководстве рассматривается создание файлового ресурса в Azure и его подключение к каждому узлу агента и главному узлу кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-105">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="4a9d8-106">Настройка файлового ресурса упрощает обмен файлами в кластере, в том числе настройку, доступ, использование журналов и многое другое.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="4a9d8-107">В этом руководстве выполняются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-107">The following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a9d8-108">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="4a9d8-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="4a9d8-109">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="4a9d8-109">Create a file share</span></span>
> * <span data-ttu-id="4a9d8-110">Подключение ресурса к кластеру DC/OS</span><span class="sxs-lookup"><span data-stu-id="4a9d8-110">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="4a9d8-111">Для выполнения действий, описанных в этом руководстве, потребуется кластер ACS DC/OS.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="4a9d8-112">При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).</span><span class="sxs-lookup"><span data-stu-id="4a9d8-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="4a9d8-113">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4a9d8-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="4a9d8-115">Если вам необходимо выполнить обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4a9d8-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="4a9d8-116">Создание файлового ресурса в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4a9d8-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="4a9d8-117">Перед использованием файлового ресурса Azure с кластером ACS DC/OS необходимо создать учетную запись хранения и файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-117">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span></span> <span data-ttu-id="4a9d8-118">Чтобы создать хранилище и файловый ресурс, выполните следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-118">Run the following script to create the storage and file share.</span></span> <span data-ttu-id="4a9d8-119">Обновите параметры данными из вашей среды.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-119">Update the parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="4a9d8-120">Подключение ресурса к кластеру</span><span class="sxs-lookup"><span data-stu-id="4a9d8-120">Mount the share in your cluster</span></span>

<span data-ttu-id="4a9d8-121">Затем файловый ресурс необходимо подключить на каждой виртуальной машине кластера.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-121">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="4a9d8-122">Эта задача выполняется с помощью средства/протокола cifs.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-122">This task is completed using the cifs tool/protocol.</span></span> <span data-ttu-id="4a9d8-123">Операцию подключения можно выполнить вручную на каждом узле кластера либо запустить сценарий на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-123">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span></span>

<span data-ttu-id="4a9d8-124">В следующем примере выполняются два сценария: первый — для подключения файлового ресурса Azure, а второй — для запуска этого сценария на каждом узле кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-124">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span></span>

<span data-ttu-id="4a9d8-125">Для начала требуются имя учетной записи хранения Azure и ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-125">First, the Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="4a9d8-126">Чтобы получить эти сведения, выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-126">Run the following commands to get this information.</span></span> <span data-ttu-id="4a9d8-127">Запомните или запишите эти значения — они будут использоваться в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="4a9d8-128">Имя учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="4a9d8-129">Ключ доступа к учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="4a9d8-130">Затем получите полное доменное имя главного кластера DC/OS и сохраните его в переменной.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-130">Next, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="4a9d8-131">Скопируйте свой закрытый ключ на главный узел.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-131">Copy your private key to the master node.</span></span> <span data-ttu-id="4a9d8-132">Этот ключ необходим для создания ssh-подключения ко всем узлам кластера.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-132">This key is needed to create an ssh connection with all nodes in the cluster.</span></span> <span data-ttu-id="4a9d8-133">Измените имя пользователя, если при создании кластера использовалось значение не по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-133">Update the user name if a non-default value was used when creating the cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="4a9d8-134">Создайте SSH-подключение к главному узлу (или первому главному узлу) кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-134">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="4a9d8-135">Измените имя пользователя, если при создании кластера использовалось значение не по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-135">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="4a9d8-136">Создайте файл с именем **cifsMount.sh** и скопируйте в него следующие данные.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-136">Create a file named **cifsMount.sh**, and copy the following contents into it.</span></span> 

<span data-ttu-id="4a9d8-137">Этот сценарий используется для подключения файлового ресурса Azure.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-137">This script is used to mount the Azure file share.</span></span> <span data-ttu-id="4a9d8-138">Обновите значения переменных `STORAGE_ACCT_NAME` и `ACCESS_KEY` ранее собранными данными.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-138">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="4a9d8-139">Создайте второй файл с именем **getNodesRunScript.sh** и скопируйте в него следующие данные.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-139">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span></span> 

<span data-ttu-id="4a9d8-140">Этот сценарий обнаруживает все узлы кластера, а затем запускает сценарий **cifsMount.sh** для подключения файлового ресурса на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-140">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for the next command
sudo apt-get install jq -y

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="4a9d8-141">Выполните этот сценарий, чтобы подключить файловый ресурс Azure на всех узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-141">Run the script to mount the Azure file share on all nodes of the cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="4a9d8-142">Файловый ресурс теперь доступен по адресу `/mnt/share/dcosshare` на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-142">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a9d8-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a9d8-143">Next steps</span></span>

<span data-ttu-id="4a9d8-144">В этом руководстве была обеспечена доступность файлового ресурса Azure на кластере DC/OS с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-144">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a9d8-145">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="4a9d8-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="4a9d8-146">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="4a9d8-146">Create a file share</span></span>
> * <span data-ttu-id="4a9d8-147">Подключение ресурса к кластеру DC/OS</span><span class="sxs-lookup"><span data-stu-id="4a9d8-147">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="4a9d8-148">Переходите к следующему руководству, чтобы узнать об интеграции реестра контейнеров Azure с DC/OS в Azure.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-148">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a9d8-149">Приложения балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="4a9d8-149">Load balance applications</span></span>](container-service-dcos-acr.md)