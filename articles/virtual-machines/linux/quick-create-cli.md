---
title: "Быстрый запуск - aaaAzure CLI создания виртуальной Машины | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машин с hello Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="ca5ee-103">Создание виртуальной машины Linux с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ca5ee-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="ca5ee-104">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="ca5ee-105">В этом руководстве рассматривается использование виртуальной машины, работающей Ubuntu server toodeploy hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="ca5ee-106">После развертывания сервера hello SSH-подключения создается и устанавливается веб-сервер NGINX.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="ca5ee-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ca5ee-108">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ca5ee-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ca5ee-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ca5ee-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="ca5ee-111">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ca5ee-111">Create a resource group</span></span>

<span data-ttu-id="ca5ee-112">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ca5ee-113">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ca5ee-114">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="ca5ee-115">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ca5ee-115">Create virtual machine</span></span>

<span data-ttu-id="ca5ee-116">Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="ca5ee-117">Hello следующий пример создает Виртуальную машину с именем *myVM* и создает ключи SSH, если они еще не существуют в ключевое расположение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="ca5ee-118">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="ca5ee-119">При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="ca5ee-120">Запишите hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="ca5ee-121">Этот адрес будет hello используется tooaccess виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="ca5ee-122">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="ca5ee-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="ca5ee-123">По умолчанию виртуальные машины Linux, развернутые в Azure, поддерживают только SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="ca5ee-124">Если эта виртуальная машина будет toobe веб-сервере, необходимо tooopen порту 80 из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="ca5ee-125">Используйте hello [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) команда tooopen hello требуемого порта.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="ca5ee-126">SSH-подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ca5ee-126">SSH into your VM</span></span>

<span data-ttu-id="ca5ee-127">Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="ca5ee-128">Убедитесь, что tooreplace  *<publicIpAddress>*  с hello корректировать общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="ca5ee-129">В примере выше виртуальная машина имела следующий IP-адрес: *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="ca5ee-130">Установка nginx</span><span class="sxs-lookup"><span data-stu-id="ca5ee-130">Install NGINX</span></span>

<span data-ttu-id="ca5ee-131">Используйте hello ниже bash источники пакетов tooupdate сценария и установить последнюю версию пакета NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="ca5ee-132">Просмотр hello NGINX начальной страницы</span><span class="sxs-lookup"><span data-stu-id="ca5ee-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="ca5ee-133">NGINX установлен и порт 80, теперь открыт на ВМ из hello Интернет - можно использовать веб-браузер на выбор tooview hello по умолчанию NGINX начальной страницы.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="ca5ee-134">Быть убедиться, что hello toouse *publicIpAddress* приведенной выше toovisit страница по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="ca5ee-136">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="ca5ee-136">Clean up resources</span></span>

<span data-ttu-id="ca5ee-137">Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ca5ee-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca5ee-138">Next steps</span></span>

<span data-ttu-id="ca5ee-139">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="ca5ee-140">toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="ca5ee-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="ca5ee-141">Создание виртуальных машин Linux и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ca5ee-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
