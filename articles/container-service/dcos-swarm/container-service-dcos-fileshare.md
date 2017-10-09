---
title: "aaaFile общего ресурса для кластера DC/ОС Azure | Документы Microsoft"
description: "Создать и подключить tooa DC/OS файл общего ресурса кластера в службе контейнера Azure"
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
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="adb70-104">Создать и подключить tooa DC/OS файл общего ресурса кластера</span><span class="sxs-lookup"><span data-stu-id="adb70-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="adb70-105">Подробное описание этого учебника, как toocreate файл общего доступа в Azure и подключить его для каждого агента и образец hello DC/OS кластера.</span><span class="sxs-lookup"><span data-stu-id="adb70-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="adb70-106">Настройка общей папки позволяет проще tooshare файлы в кластере, например конфигурации, доступ, журналы и многое другое.</span><span class="sxs-lookup"><span data-stu-id="adb70-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="adb70-107">в этом учебнике выполняются Hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="adb70-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="adb70-108">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="adb70-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="adb70-109">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="adb70-109">Create a file share</span></span>
> * <span data-ttu-id="adb70-110">Подключить hello общего ресурса в кластере DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="adb70-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="adb70-111">Вы должны ACS DC/OS hello toocomplete кластера шаги в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="adb70-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="adb70-112">При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).</span><span class="sxs-lookup"><span data-stu-id="adb70-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="adb70-113">Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="adb70-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="adb70-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="adb70-115">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="adb70-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="adb70-116">Создание файлового ресурса в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="adb70-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="adb70-117">Перед использованием Azure файловый ресурс кластера с ACS DC/OS, hello хранилища учетной записи и общей папки должен быть создан.</span><span class="sxs-lookup"><span data-stu-id="adb70-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="adb70-118">Запустите следующий скрипт toocreate hello хранилища и общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="adb70-119">Обновление параметров hello с данными из вашей среды.</span><span class="sxs-lookup"><span data-stu-id="adb70-119">Update hello parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="adb70-120">Подключить hello общего ресурса в кластере</span><span class="sxs-lookup"><span data-stu-id="adb70-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="adb70-121">Далее hello общего файла требуется toobe на каждой виртуальной машине внутри кластера.</span><span class="sxs-lookup"><span data-stu-id="adb70-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="adb70-122">Эта задача выполняется с помощью средства cifs hello и протокола.</span><span class="sxs-lookup"><span data-stu-id="adb70-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="adb70-123">на каждом узле кластера hello, или путем выполнения сценария для каждого узла в кластере hello Hello операции подключения можно выполнить вручную.</span><span class="sxs-lookup"><span data-stu-id="adb70-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="adb70-124">В этом примере выполняются два сценария, один toomount hello Azure файлов общей папки, а второй toorun этот скрипт на каждом узле кластера DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="adb70-125">Во-первых необходимы имя учетной записи хранилища Azure hello и ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="adb70-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="adb70-126">Выполните следующие команды tooget hello эти сведения.</span><span class="sxs-lookup"><span data-stu-id="adb70-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="adb70-127">Запомните или запишите эти значения — они будут использоваться в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="adb70-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="adb70-128">Имя учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="adb70-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="adb70-129">Ключ доступа к учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="adb70-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="adb70-130">Затем следует получите hello полное доменное имя hello DC/OS-шаблоны и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="adb70-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="adb70-131">Скопируйте на главном узле toohello закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="adb70-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="adb70-132">Этот ключ является необходимые toocreate ssh соединения с узлами в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="adb70-133">Обновите имя пользователя hello, если значение не по умолчанию использовался при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="adb70-134">Создайте SSH-подключения с hello master (или первый образец hello) кластера на базе контроллера домена/ОС.</span><span class="sxs-lookup"><span data-stu-id="adb70-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="adb70-135">Обновите имя пользователя hello, если значение не по умолчанию использовался при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="adb70-136">Создайте файл с именем **cifsMount.sh**, и hello копировать содержимое в него.</span><span class="sxs-lookup"><span data-stu-id="adb70-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="adb70-137">Этот скрипт является используется toomount hello Azure общей папки.</span><span class="sxs-lookup"><span data-stu-id="adb70-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="adb70-138">Обновление hello `STORAGE_ACCT_NAME` и `ACCESS_KEY` переменных с hello сведения, собранные ранее.</span><span class="sxs-lookup"><span data-stu-id="adb70-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="adb70-139">Создайте второй файл с именем **getNodesRunScript.sh** и hello копировать содержимое в файл hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="adb70-140">Этот сценарий обнаруживает все узлы кластера, а затем запускает hello **cifsMount.sh** сценарий toomount hello общую папку на каждом.</span><span class="sxs-lookup"><span data-stu-id="adb70-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="adb70-141">Hello выполнения сценария toomount hello Azure общей папки на всех узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="adb70-142">Hello общей папки теперь доступны в `/mnt/share/dcosshare` на каждом узле кластера hello.</span><span class="sxs-lookup"><span data-stu-id="adb70-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adb70-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="adb70-143">Next steps</span></span>

<span data-ttu-id="adb70-144">В этом учебнике Azure общей папки был сделан доступных tooa DC/OS кластер, использующий hello действия:</span><span class="sxs-lookup"><span data-stu-id="adb70-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="adb70-145">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="adb70-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="adb70-146">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="adb70-146">Create a file share</span></span>
> * <span data-ttu-id="adb70-147">Подключить hello общего ресурса в кластере DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="adb70-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="adb70-148">Переместить toohello Далее учебника toolearn об интеграции Azure контейнер реестра с контроллера домена или ОС в Azure.</span><span class="sxs-lookup"><span data-stu-id="adb70-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="adb70-149">Приложения балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="adb70-149">Load balance applications</span></span>](container-service-dcos-acr.md)