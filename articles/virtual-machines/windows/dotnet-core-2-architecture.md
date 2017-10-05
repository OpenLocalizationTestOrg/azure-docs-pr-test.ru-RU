---
title: "Развертывание вычислительных ресурсов Windows с помощью шаблонов Azure Resource Manager | Документация Майкрософт"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="fd862-103">Архитектура приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="fd862-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="fd862-104">При разработке развертывания Azure Resource Manager необходимую вычислительную мощность нужно сопоставлять с ресурсами и службами Azure.</span><span class="sxs-lookup"><span data-stu-id="fd862-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="fd862-105">Если приложение содержит несколько конечных точек http, базы данных и службы кэша, следует рационально распределить ресурсы Azure между всеми этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="fd862-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="fd862-106">Например, приложение "Магазин музыки" содержит веб-приложение, размещенное на виртуальной машине, и базу данных SQL на основе базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="fd862-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="fd862-107">В этом документе описана конфигурация вычислительных ресурсов для такого приложения, представленная в шаблоне Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fd862-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="fd862-108">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="fd862-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="fd862-109">Чтобы оптимизировать процесс, заранее разверните экземпляр решения в подписке Azure, а затем установите шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fd862-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="fd862-110">Полный шаблон можно найти [здесь](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="fd862-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="fd862-111">Виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="fd862-111">Virtual Machine</span></span>
<span data-ttu-id="fd862-112">Приложение "Магазин музыки" — это веб-приложение, где пользователи могут искать и приобретать доступные композиции.</span><span class="sxs-lookup"><span data-stu-id="fd862-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="fd862-113">Для размещения веб-приложений можно использовать несколько служб Azure. В нашем примере используется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="fd862-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="fd862-114">Используя предложенный шаблон магазина музыки, мы развернем виртуальную машину, установим веб-сервер, а затем установим и настроим веб-сайт самого магазина.</span><span class="sxs-lookup"><span data-stu-id="fd862-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="fd862-115">В этой статье подробно описывается только развертывание виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fd862-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="fd862-116">Настройка веб-сервера и приложения подробно описана в следующей статье.</span><span class="sxs-lookup"><span data-stu-id="fd862-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="fd862-117">Чтобы добавить в шаблон виртуальную машину, можно использовать мастер добавления нового ресурса в Visual Studio или вставить в шаблон развертывания допустимый объект JSON.</span><span class="sxs-lookup"><span data-stu-id="fd862-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="fd862-118">Для развертывания виртуальной машины также потребуются несколько связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fd862-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="fd862-119">Если для создания шаблона вы используете Visual Studio, эти ресурсы создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="fd862-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="fd862-120">При создании шаблона вручную вам нужно самостоятельно добавить и настроить эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fd862-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="fd862-121">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager — [JSON для виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="fd862-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
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

<span data-ttu-id="fd862-122">После развертывания свойства виртуальной машины можно увидеть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fd862-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Виртуальная машина](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="fd862-124">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="fd862-124">Storage Account</span></span>
<span data-ttu-id="fd862-125">Учетные записи хранения имеют множество возможностей и параметров хранения.</span><span class="sxs-lookup"><span data-stu-id="fd862-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="fd862-126">В контексте виртуальных машин Azure учетная запись хранения содержит виртуальные жесткие диски виртуальной машины и любые дополнительные диски данных.</span><span class="sxs-lookup"><span data-stu-id="fd862-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="fd862-127">В нашем примере для магазина музыки используется по одной учетной записи для хранения виртуального жесткого диска каждой виртуальной машины в развертывании.</span><span class="sxs-lookup"><span data-stu-id="fd862-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="fd862-128">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager для настройки [учетной записи хранения](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="fd862-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

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

<span data-ttu-id="fd862-129">Учетная запись хранения сопоставляется с виртуальной машиной в объявлении шаблона Resource Manager для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fd862-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="fd862-130">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager для настройки [сопоставления виртуальной машины и учетной записи хранения](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="fd862-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

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

<span data-ttu-id="fd862-131">После развертывания учетная запись хранения появится на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fd862-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Учетная запись хранения](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="fd862-133">Щелкните контейнер BLOB-объектов учетной записи хранения, чтобы просмотреть файл виртуального жесткого диска для каждой виртуальной машины, развернутой с использованием этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="fd862-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Виртуальные жесткие диски](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="fd862-135">Дополнительные сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="fd862-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="fd862-136">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="fd862-136">Virtual Network</span></span>
<span data-ttu-id="fd862-137">Если для виртуальной машины требуется обмен данными по внутренней сети (например, с другими виртуальными машинами и ресурсами Azure), нужно использовать виртуальную сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="fd862-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="fd862-138">Виртуальная сеть не предоставляет доступ к виртуальной машине из Интернета.</span><span class="sxs-lookup"><span data-stu-id="fd862-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="fd862-139">Для открытого доступа нужен общедоступный IP-адрес, который описывается в следующих статьях этой серии.</span><span class="sxs-lookup"><span data-stu-id="fd862-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="fd862-140">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager с настройками [виртуальной сети и подсети](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="fd862-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

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

<span data-ttu-id="fd862-141">На портале Azure виртуальная сеть будет выглядеть примерно так, как на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="fd862-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="fd862-142">Обратите внимание, что все виртуальные машины, развернутые с использованием этого шаблона, присоединяются к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fd862-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Виртуальная сеть](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="fd862-144">Сетевой интерфейс</span><span class="sxs-lookup"><span data-stu-id="fd862-144">Network Interface</span></span>
 <span data-ttu-id="fd862-145">Сетевой интерфейс соединяет виртуальную машину с виртуальной сетью, а именно с той подсетью, которая определена в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fd862-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="fd862-146">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager с настройками [сетевого интерфейса](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="fd862-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
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
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
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
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="fd862-147">Каждый ресурс виртуальной машины включает в себя профиль сети.</span><span class="sxs-lookup"><span data-stu-id="fd862-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="fd862-148">В этом профиле сетевой интерфейс сопоставляется с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="fd862-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="fd862-149">Щелкните эту ссылку, чтобы увидеть пример JSON в шаблоне Resource Manager с настройками [профиля виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="fd862-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="fd862-150">На портале Azure сетевой интерфейс будет выглядеть примерно так, как на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="fd862-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="fd862-151">Внутренний IP-адрес и сопоставления виртуальной машины можно просмотреть с помощью ресурса сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="fd862-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Сетевой интерфейс](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="fd862-153">Дополнительные сведения см. в [документации по виртуальным сетям Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="fd862-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="fd862-154">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fd862-154">Azure SQL Database</span></span>
<span data-ttu-id="fd862-155">Помимо виртуальной машины для размещения веб-сайта "Магазин музыки" вам также нужно развернуть базу данных SQL Azure для размещения базы данных этого магазина.</span><span class="sxs-lookup"><span data-stu-id="fd862-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="fd862-156">Использование базы данных SQL Azure позволяет нам обойтись без дополнительного набора виртуальных машин, а также обеспечивает встроенную поддержку масштабируемости и доступности.</span><span class="sxs-lookup"><span data-stu-id="fd862-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="fd862-157">Чтобы добавить в шаблон базу данных SQL Azure, можно использовать мастер добавления нового ресурса в Visual Studio или вставить в шаблон развертывания допустимый объект JSON.</span><span class="sxs-lookup"><span data-stu-id="fd862-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="fd862-158">Ресурс SQL Server включает имя пользователя и пароль, которые предоставляют права администратора на экземпляре SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fd862-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="fd862-159">Также добавляется ресурс брандмауэра SQL.</span><span class="sxs-lookup"><span data-stu-id="fd862-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="fd862-160">По умолчанию к экземпляру SQL Server могут подключаться только приложения, размещенные в Azure.</span><span class="sxs-lookup"><span data-stu-id="fd862-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="fd862-161">Чтобы разрешить подключение к экземпляру SQL Server для внешних приложений, например SQL Server Management Studio, следует настроить брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="fd862-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="fd862-162">В нашем примере с магазином можно использовать конфигурацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fd862-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="fd862-163">Щелкните эту ссылку, чтобы просмотреть пример JSON в шаблоне Resource Manager для [базы данных Azure SQL](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="fd862-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="fd862-164">Представление SQL Server и базы данных MusicStore в соответствии с отображением на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fd862-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="fd862-166">Дополнительные сведения о развертывании базы данных SQL см. в [документации по базе данных SQL Azure](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="fd862-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="fd862-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd862-167">Next step</span></span>
<hr>

[<span data-ttu-id="fd862-168">Шаг 2. Доступ и безопасность в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd862-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

