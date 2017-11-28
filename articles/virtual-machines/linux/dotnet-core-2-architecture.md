---
title: "aaaDeploying ресурсов вычислений Linux с помощью шаблонов диспетчера ресурсов Azure | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="6fb95-103">Архитектура приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="6fb95-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="6fb95-104">При разработке развертывания диспетчера ресурсов Azure, требования к вычислений должны toobe сопоставлен tooAzure ресурсы и службы.</span><span class="sxs-lookup"><span data-stu-id="6fb95-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="6fb95-105">Если приложение содержит несколько конечных точек http, базы данных и службу кэширования данных, hello ресурсы Azure, на которых размещены каждого из этих компонентов должен toobe процессов оптимизации.</span><span class="sxs-lookup"><span data-stu-id="6fb95-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="6fb95-106">Например приложение Music Store образец hello содержит веб-приложения, размещенного на виртуальной машине и базу данных SQL, которая размещается в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6fb95-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="6fb95-107">В этом документе описаны как hello Music Store вычислительные ресурсы настроены в шаблоне Azure Resource Manager образец hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="6fb95-108">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="6fb95-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="6fb95-109">Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb95-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="6fb95-110">Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="6fb95-110">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="6fb95-111">Виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="6fb95-111">Virtual Machine</span></span>
<span data-ttu-id="6fb95-112">Hello Music Store приложение включает веб-приложения, где можно просматривать и покупать музыка клиентов.</span><span class="sxs-lookup"><span data-stu-id="6fb95-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="6fb95-113">Для размещения веб-приложений можно использовать несколько служб Azure. В нашем примере используется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="6fb95-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="6fb95-114">С помощью шаблона Music Store образец hello, развернута виртуальная машина, установить веб-сервер и веб-сайт Music Store hello установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="6fb95-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="6fb95-115">Ради hello объекта в этой статье подробно только hello развертывания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6fb95-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="6fb95-116">конфигурации Hello hello веб-сервера и приложения hello подробно описана в статье более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6fb95-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="6fb95-117">Виртуальные машины можно добавить tooa шаблон, с помощью Visual Studio добавьте новый ресурс мастер, или путем вставки допустимых данных JSON в шаблон развертывания hello hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="6fb95-118">Для развертывания виртуальной машины также потребуются несколько связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6fb95-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="6fb95-119">Если используется шаблон hello toocreate Visual Studio, эти ресурсы создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="6fb95-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="6fb95-120">При ручном создании шаблона hello, эти ресурсы требуют toobe вставляется и настроен.</span><span class="sxs-lookup"><span data-stu-id="6fb95-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="6fb95-121">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [JSON виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="6fb95-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

<span data-ttu-id="6fb95-122">После развертывания hello свойства виртуальной машины можно увидеть в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb95-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Виртуальная машина](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="6fb95-124">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="6fb95-124">Storage Account</span></span>
<span data-ttu-id="6fb95-125">Учетные записи хранения имеют множество возможностей и параметров хранения.</span><span class="sxs-lookup"><span data-stu-id="6fb95-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="6fb95-126">Для контекста hello виртуальных машин Azure учетная запись хранения содержит hello виртуальных жестких дисков виртуальной машины hello и любых дополнительных дисков данных.</span><span class="sxs-lookup"><span data-stu-id="6fb95-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="6fb95-127">Образец Hello Music Store включает один хранилища учетной записи toohold hello виртуального жесткого диска для каждой виртуальной машины в развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="6fb95-128">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [учетной записи хранилища](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="6fb95-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="6fb95-129">Учетная запись хранения —, связанных с виртуальной машины в объявлении шаблона диспетчера ресурсов hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6fb95-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="6fb95-130">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [виртуальной машины и учетной записи хранилища ассоциации](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="6fb95-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="6fb95-131">После развертывания можно просмотреть hello учетной записи хранилища в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb95-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Учетная запись хранения](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="6fb95-133">Щелкните кнопкой мыши в контейнер BLOB-объектов учетной записи хранилища hello, можно увидеть hello файлу виртуального жесткого диска для всех виртуальных машин, развернутых с помощью шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Виртуальные жесткие диски](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="6fb95-135">Дополнительные сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="6fb95-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="6fb95-136">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="6fb95-136">Virtual Network</span></span>
<span data-ttu-id="6fb95-137">Если виртуальная машина требует внутренней сети, например toocommunicate возможность hello с другими виртуальными машинами и ресурсами Azure, виртуальная сеть Azure не требуется.</span><span class="sxs-lookup"><span data-stu-id="6fb95-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="6fb95-138">Виртуальная сеть не делает hello виртуальной машины доступно по Интернету hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="6fb95-139">Для открытого доступа нужен общедоступный IP-адрес, который описывается в следующих статьях этой серии.</span><span class="sxs-lookup"><span data-stu-id="6fb95-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="6fb95-140">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [виртуальную сеть и подсети](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="6fb95-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="6fb95-141">Из hello портал Azure виртуальная сеть hello выглядит как hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="6fb95-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="6fb95-142">Обратите внимание, что все виртуальные машины, развернутые с шаблоном hello вложенного toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6fb95-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Виртуальная сеть](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="6fb95-144">Сетевой интерфейс</span><span class="sxs-lookup"><span data-stu-id="6fb95-144">Network Interface</span></span>
 <span data-ttu-id="6fb95-145">Сетевой интерфейс подключается виртуальной сети виртуальной машины tooa, точнее tooa подсети, который был определен в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="6fb95-146">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [сетевой интерфейс](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="6fb95-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="6fb95-147">Каждый ресурс виртуальной машины включает в себя профиль сети.</span><span class="sxs-lookup"><span data-stu-id="6fb95-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="6fb95-148">сетевой интерфейс Hello не связанную с виртуальной машиной hello в этом профиле.</span><span class="sxs-lookup"><span data-stu-id="6fb95-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="6fb95-149">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [профиль сети виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="6fb95-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="6fb95-150">Из hello портал Azure hello сетевой интерфейс выглядит как hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="6fb95-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="6fb95-151">внутренний IP-адрес Hello и наборов ассоциаций hello виртуальной машины можно просмотреть на ресурс hello сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="6fb95-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Сетевой интерфейс](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="6fb95-153">Дополнительные сведения см. в [документации по виртуальным сетям Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="6fb95-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="6fb95-154">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6fb95-154">Azure SQL Database</span></span>
<span data-ttu-id="6fb95-155">В дополнение к этому tooa виртуальная машина, содержащая Music Store hello веб-сайта, базы данных SQL Azure — развернутой toohost hello Music Store, база данных.</span><span class="sxs-lookup"><span data-stu-id="6fb95-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="6fb95-156">Преимущество Hello здесь использования базы данных SQL Azure — что второй набор виртуальных машин не требуется и масштабируемость и доступность встроен в службы hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="6fb95-157">Базы данных Azure SQL можно добавить с помощью Visual Studio добавьте новый ресурс мастер, или путем вставки допустимых данных JSON в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="6fb95-158">Hello ресурсов SQL Server включает в себя имя пользователя и пароль, которые предоставляются права администратора на экземпляре SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="6fb95-159">Также добавляется ресурс брандмауэра SQL.</span><span class="sxs-lookup"><span data-stu-id="6fb95-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="6fb95-160">По умолчанию приложения, размещенные в Azure, может tooconnect с экземпляром SQL hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="6fb95-161">tooallow внешних таких SQL Server Management studio tooconnect toohello экземпляр SQL Server, брандмауэр hello приложению toobe настроен.</span><span class="sxs-lookup"><span data-stu-id="6fb95-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="6fb95-162">Конфигурация по умолчанию hello подойдет ради hello демонстрации Music Store hello.</span><span class="sxs-lookup"><span data-stu-id="6fb95-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="6fb95-163">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [базу данных SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="6fb95-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="6fb95-164">Представление hello SQL server и MusicStore базы данных, как показано в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb95-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="6fb95-166">Дополнительные сведения о развертывании базы данных SQL см. в [документации по базе данных SQL Azure](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="6fb95-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="6fb95-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6fb95-167">Next step</span></span>
<hr>

[<span data-ttu-id="6fb95-168">Шаг 2. Доступ и безопасность в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6fb95-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

