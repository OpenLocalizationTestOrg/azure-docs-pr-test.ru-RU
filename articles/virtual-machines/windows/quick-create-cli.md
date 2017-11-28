---
title: "Краткое руководство по Azure. Создание виртуальной машины Windows с помощью интерфейса командной строки | Документация Майкрософт"
description: "Быстро научитесь создавать виртуальные машины Windows с помощью Azure CLI."
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
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="8a41c-103">Создание виртуальной машины Windows с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8a41c-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="8a41c-104">Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="8a41c-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="8a41c-105">В этом руководстве описывается, как с помощью Azure CLI развернуть виртуальную машину под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a41c-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="8a41c-106">После завершения развертывания мы подключимся к серверу и установим IIS.</span><span class="sxs-lookup"><span data-stu-id="8a41c-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="8a41c-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="8a41c-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8a41c-108">Если вы решили установить и использовать CLI локально, для выполнения инструкций в этом руководстве вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8a41c-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8a41c-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="8a41c-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="8a41c-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8a41c-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="8a41c-111">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="8a41c-111">Create a resource group</span></span>

<span data-ttu-id="8a41c-112">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8a41c-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8a41c-113">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="8a41c-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8a41c-114">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="8a41c-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="8a41c-115">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8a41c-115">Create virtual machine</span></span>

<span data-ttu-id="8a41c-116">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8a41c-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="8a41c-117">В следующем примере создается виртуальная машина с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8a41c-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="8a41c-118">В этом примере используются имя администратора *azureuser* и его пароль *myPassword12*.</span><span class="sxs-lookup"><span data-stu-id="8a41c-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="8a41c-119">Измените эти значения в соответствии со своей средой.</span><span class="sxs-lookup"><span data-stu-id="8a41c-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="8a41c-120">Эти значения нужны для создания подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8a41c-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="8a41c-121">После создания виртуальной машины в Azure CLI отображается информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="8a41c-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="8a41c-122">Запишите значение `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="8a41c-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="8a41c-123">Этот адрес используется для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8a41c-123">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="8a41c-124">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="8a41c-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="8a41c-125">По умолчанию виртуальные машины Windows, развернутые в Azure, поддерживают только RDP-подключения.</span><span class="sxs-lookup"><span data-stu-id="8a41c-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="8a41c-126">Если эта виртуальная машина будет использоваться в качестве веб-сервера, необходимо открыть порт 80 через Интернет.</span><span class="sxs-lookup"><span data-stu-id="8a41c-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="8a41c-127">Выполните команду [az vm open-port](/cli/azure/vm#open-port), чтобы открыть нужный порт.</span><span class="sxs-lookup"><span data-stu-id="8a41c-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="8a41c-128">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="8a41c-128">Connect to virtual machine</span></span>

<span data-ttu-id="8a41c-129">Используйте следующую команду для создания сеанса удаленного рабочего стола с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="8a41c-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="8a41c-130">Замените IP-адрес общедоступным IP-адресом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8a41c-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="8a41c-131">При появлении запроса введите учетные данные, использованные при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8a41c-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="8a41c-132">Установка IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a41c-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="8a41c-133">После входа на виртуальную машину Azure вы можете установить IIS и включить локальное правило брандмауэра, разрешающее веб-трафик, с помощью одной строки кода PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a41c-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="8a41c-134">Откройте командную строку PowerShell и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a41c-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="8a41c-135">Просмотр страницы приветствия IIS</span><span class="sxs-lookup"><span data-stu-id="8a41c-135">View the IIS welcome page</span></span>

<span data-ttu-id="8a41c-136">Установив IIS и открыв через Интернет порт 80 на виртуальной машине, вы можете просмотреть страницу приветствия IIS по умолчанию в любом браузере.</span><span class="sxs-lookup"><span data-stu-id="8a41c-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="8a41c-137">Чтобы перейти на страницу по умолчанию, используйте общедоступный IP-адрес, записанный ранее.</span><span class="sxs-lookup"><span data-stu-id="8a41c-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="8a41c-139">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="8a41c-139">Clean up resources</span></span>

<span data-ttu-id="8a41c-140">Вы можете удалить ставшие ненужными группу ресурсов, виртуальную машину и все связанные с ней ресурсы, выполнив команду [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="8a41c-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8a41c-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a41c-141">Next steps</span></span>

<span data-ttu-id="8a41c-142">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="8a41c-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="8a41c-143">Дополнительные сведения о виртуальных машинах Azure см. в руководстве по работе с виртуальными машинами Windows.</span><span class="sxs-lookup"><span data-stu-id="8a41c-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a41c-144">Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a41c-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
