---
title: "Быстрый запуск - aaaAzure создать CLI ВМ Windows | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машинах с hello Azure CLI."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="1ed8c-103">Создание виртуальной машины Windows с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1ed8c-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="1ed8c-104">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="1ed8c-105">В этом руководстве рассматривается использование виртуальной машины с ОС Windows Server 2016 toodeploy hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="1ed8c-106">После завершения развертывания мы подключения toohello сервера и установить службы IIS.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="1ed8c-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1ed8c-108">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1ed8c-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1ed8c-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1ed8c-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="1ed8c-111">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1ed8c-111">Create a resource group</span></span>

<span data-ttu-id="1ed8c-112">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1ed8c-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1ed8c-113">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="1ed8c-114">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="1ed8c-115">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1ed8c-115">Create virtual machine</span></span>

<span data-ttu-id="1ed8c-116">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1ed8c-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="1ed8c-117">Hello следующий пример создает Виртуальную машину с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="1ed8c-118">В этом примере используется *azureuser* имени пользователя с правами администратора и *myPassword12* hello паролем.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="1ed8c-119">Обновите эти значения toosomething соответствующие tooyour среду.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="1ed8c-120">Эти значения необходимы при создании соединения с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="1ed8c-121">При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="1ed8c-122">Запишите hello `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="1ed8c-123">Этот адрес будет hello используется tooaccess виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-123">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="1ed8c-124">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="1ed8c-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="1ed8c-125">По умолчанию в tooWindows виртуальных машин, развернутых в Azure допускаются только подключений по протоколу RDP.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="1ed8c-126">Если эта виртуальная машина будет toobe веб-сервере, необходимо tooopen порту 80 из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="1ed8c-127">Используйте hello [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) команда tooopen hello требуемого порта.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="1ed8c-128">Подключиться к компьютеру toovirtual</span><span class="sxs-lookup"><span data-stu-id="1ed8c-128">Connect toovirtual machine</span></span>

<span data-ttu-id="1ed8c-129">Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="1ed8c-130">Замените hello IP-адрес hello общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="1ed8c-131">При появлении запроса введите hello учетные данные, используемые при создании виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="1ed8c-132">Установка IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ed8c-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="1ed8c-133">Теперь, когда вы вошли в toohello виртуальной Машине Azure, можно использовать одну строку PowerShell tooinstall IIS и включить hello локальном брандмауэре правило tooallow веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="1ed8c-134">Откройте командную строку PowerShell и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1ed8c-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="1ed8c-135">Представление hello страницу приветствия IIS</span><span class="sxs-lookup"><span data-stu-id="1ed8c-135">View hello IIS welcome page</span></span>

<span data-ttu-id="1ed8c-136">С установленными службами IIS и порт 80, теперь открыт на ВМ из hello Интернета можно использовать веб-браузере choice tooview hello по умолчанию службы IIS страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="1ed8c-137">Быть убедиться, что toouse hello общедоступный IP-адрес, описанных выше toovisit страница по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="1ed8c-139">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="1ed8c-139">Clean up resources</span></span>

<span data-ttu-id="1ed8c-140">Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1ed8c-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ed8c-141">Next steps</span></span>

<span data-ttu-id="1ed8c-142">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="1ed8c-143">toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Windows.</span><span class="sxs-lookup"><span data-stu-id="1ed8c-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ed8c-144">Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ed8c-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
