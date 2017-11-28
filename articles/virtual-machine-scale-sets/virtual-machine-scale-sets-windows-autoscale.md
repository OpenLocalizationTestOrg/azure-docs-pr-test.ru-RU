---
title: "Наборы масштабирования виртуальных машин Windows aaaAutoscale | Документы Microsoft"
description: "Настройка автоматического масштабирования набора масштабирования виртуальных машин Windows с помощью Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="b9a80-103">Автоматическое масштабирование ВМ в наборе масштабирования ВМ</span><span class="sxs-lookup"><span data-stu-id="b9a80-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="b9a80-104">Наборы масштабирования виртуальных машин упростить для вас toodeploy идентичные виртуальных машин и управление как набор.</span><span class="sxs-lookup"><span data-stu-id="b9a80-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="b9a80-105">Масштабируемые наборы обеспечивают высокую степень масштабируемости и персонализацию уровня вычислений для гипермасштабируемых приложений. Кроме того, они поддерживают образы платформ Windows и Linux, а также пользовательские образы и расширения.</span><span class="sxs-lookup"><span data-stu-id="b9a80-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="b9a80-106">Дополнительные сведения о наборах масштабирования см. в разделе [Наборы масштабирования виртуальных машин](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="b9a80-107">Этом учебнике показано, как задать toocreate набор масштабирования виртуальных машин Windows и автоматически машины hello масштабирования в hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="b9a80-108">Можно создать hello шкалу установить и настроить масштабирование, создание шаблона диспетчера ресурсов Azure и развертывая его с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9a80-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="b9a80-109">Дополнительную информацию о шаблонах см. в статье [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="b9a80-110">toolearn Дополнительные сведения о автоматического масштабирования наборы масштабирования в разделе [автоматического масштабирования и виртуальной машины задает масштаб](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="b9a80-111">В этой статье развертывание hello следующих ресурсов и расширения:</span><span class="sxs-lookup"><span data-stu-id="b9a80-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="b9a80-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="b9a80-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="b9a80-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="b9a80-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="b9a80-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="b9a80-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="b9a80-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="b9a80-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="b9a80-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="b9a80-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="b9a80-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="b9a80-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="b9a80-118">Microsoft.Compute/virtualMachineScaleSets;</span><span class="sxs-lookup"><span data-stu-id="b9a80-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="b9a80-119">Microsoft.Insights.VMDiagnosticsSettings;</span><span class="sxs-lookup"><span data-stu-id="b9a80-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="b9a80-120">Microsoft.Insights/autoscaleSettings.</span><span class="sxs-lookup"><span data-stu-id="b9a80-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="b9a80-121">Дополнительные сведения о ресурсах Resource Manager см. в статье [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) (Развертывание с помощью Azure Resource Manager и классическое развертывание).</span><span class="sxs-lookup"><span data-stu-id="b9a80-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="b9a80-122">Шаг 1. Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a80-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="b9a80-123">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b9a80-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="b9a80-124">Шаг 2. Создание группы ресурсов и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b9a80-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="b9a80-125">**Создание группы ресурсов** — все ресурсы должны быть tooa развернутой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b9a80-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="b9a80-126">Используйте [New AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate группу ресурсов с именем **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="b9a80-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="b9a80-127">**Создать учетную запись хранилища** — эта учетная запись хранения —, где хранится шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="b9a80-128">Используйте [New AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate учетной записи хранилища с именем **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="b9a80-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="b9a80-129">Шаг 3: Создание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="b9a80-129">Step 3: Create hello template</span></span>
<span data-ttu-id="b9a80-130">Шаблон диспетчера ресурсов Azure позволяет вам toodeploy и управлять ресурсами Azure совместно с помощью описания JSON ресурсов hello и связанных параметров развертывания.</span><span class="sxs-lookup"><span data-stu-id="b9a80-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="b9a80-131">В любом редакторе создайте файл hello C:\VMSSTemplate.json и добавьте hello исходного JSON структуры toosupport hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="b9a80-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="b9a80-132">Параметры обычно не требуется, но они обеспечивают tooinput способом значения при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="b9a80-133">Добавление этих параметров hello параметров родительского элемента, что вы добавили шаблон toohello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="b9a80-134">Имя для hello отдельной виртуальной машине, используемых tooaccess hello машины в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="b9a80-135">Имя учетной записи хранения hello, где хранится шаблон hello Hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="b9a80-136">Hello количество виртуальных машин tooinitially создать в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="b9a80-137">Hello имя и пароль учетной записи администратора hello на виртуальных машинах hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="b9a80-138">Задайте префикс имени hello ресурсов, которые создаются toosupport hello шкалы.</span><span class="sxs-lookup"><span data-stu-id="b9a80-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="b9a80-139">Переменные могут использоваться в значениях toospecify шаблона, которые могут часто изменяться или значения, которые необходимо toobe, созданные на основе сочетания значений параметров.</span><span class="sxs-lookup"><span data-stu-id="b9a80-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="b9a80-140">Добавьте эти переменные hello переменные родительского элемента, что вы добавили шаблон toohello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="b9a80-141">DNS-имена, которые используются в hello сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="b9a80-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="b9a80-142">Hello IP адрес имена и префиксы для hello виртуальную сеть и подсети.</span><span class="sxs-lookup"><span data-stu-id="b9a80-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="b9a80-143">Hello имена и идентификаторы hello виртуальной сети, подсистема балансировки нагрузки и сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="b9a80-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="b9a80-144">Имена учетной записи хранения для hello учетных записей, связанных с машинами hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="b9a80-145">Параметры для расширения диагностики, которая устанавливается на виртуальных машинах hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="b9a80-146">Дополнительные сведения о hello расширения диагностики см. в разделе [создать Windows виртуальной машины с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9a80-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="b9a80-147">Добавьте ресурс учетной записи хранения hello hello ресурсы родительского элемента, что вы добавили шаблон toohello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="b9a80-148">Этот шаблон использует hello toocreate цикла, рекомендуется использовать пять учетных записей хранилища, место хранения hello дисков операционной системы и диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="b9a80-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="b9a80-149">Этот набор учетных записей может поддерживать до too100 виртуальных машин в наборе масштабирования, — текущий максимум hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="b9a80-150">Каждая учетная запись хранения называется с буквенный код, которое было определено в переменных hello вместе с префиксом hello, укажите в параметрах hello для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="b9a80-151">Добавьте ресурс hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9a80-151">Add hello virtual network resource.</span></span> <span data-ttu-id="b9a80-152">Дополнительную информацию см. в статье [Поставщик сетевых ресурсов](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="b9a80-153">Добавьте hello открытые ресурсы IP-адресов, используемых hello Подсистема балансировки нагрузки и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b9a80-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="b9a80-154">Добавьте ресурс балансировки нагрузки hello, который используется набором масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="b9a80-155">Дополнительные сведения см. в статье, посвященной [поддержке Azure Resource Manager для подсистемы балансировки нагрузки](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="b9a80-156">Добавьте hello ресурс сетевого интерфейса, используемый hello отдельной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b9a80-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="b9a80-157">Поскольку машины в наборе масштабирования не доступны через общедоступный IP-адрес, отдельная виртуальная машина создается в hello же виртуальных машин hello tooremotely доступа к сети.</span><span class="sxs-lookup"><span data-stu-id="b9a80-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="b9a80-158">Добавьте hello отдельной виртуальной машины в сетевых как набор масштабирования hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="b9a80-159">Добавление ресурса набора масштабирования виртуальных машин hello и укажите расширение диагностики hello, установленного на всех виртуальных машин в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="b9a80-160">Многие из параметров hello для этого ресурса похожи hello ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b9a80-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="b9a80-161">Ниже перечислены основные различия Hello hello емкости элемент, который задает hello количество виртуальных машин в наборе масштабирования hello и upgradePolicy, указывающее, каким образом производятся изменения toovirtual машины.</span><span class="sxs-lookup"><span data-stu-id="b9a80-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="b9a80-162">Hello масштабный набор не создается, пока все учетные записи хранения hello создаются в соответствии с элементом dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="b9a80-163">Добавьте ресурс autoscaleSettings hello, который определяет, как набор масштабирования hello корректирует зависимости от использования процессора hello на машинах hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="b9a80-164">Для целей этого руководства важны значения следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="b9a80-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="b9a80-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="b9a80-165">**metricName**</span></span>  
    <span data-ttu-id="b9a80-166">Это значение является hello то же, что счетчик производительности hello, которое было определено в переменной wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="b9a80-167">С помощью этой переменной, hello расширения диагностики собирает hello **процессор(_всего)\% загруженности** счетчика.</span><span class="sxs-lookup"><span data-stu-id="b9a80-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="b9a80-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="b9a80-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="b9a80-169">Это значение является идентификатором ресурса hello hello набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b9a80-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="b9a80-170">**timegrain**</span><span class="sxs-lookup"><span data-stu-id="b9a80-170">**timeGrain**</span></span>  
    <span data-ttu-id="b9a80-171">Это значение является гранулярности hello hello метрик, которые собираются.</span><span class="sxs-lookup"><span data-stu-id="b9a80-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="b9a80-172">В этом шаблоне задается tooone минуты.</span><span class="sxs-lookup"><span data-stu-id="b9a80-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="b9a80-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="b9a80-173">**statistic**</span></span>  
    <span data-ttu-id="b9a80-174">Это значение определяет, как метрики hello hello объединенный tooaccommodate автоматического масштабирования действия.</span><span class="sxs-lookup"><span data-stu-id="b9a80-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="b9a80-175">Возможные значения Hello: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="b9a80-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="b9a80-176">В этом шаблоне собираются hello среднее общее использование ЦП hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b9a80-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="b9a80-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="b9a80-177">**timeWindow**</span></span>  
    <span data-ttu-id="b9a80-178">Это значение является hello диапазон времени, в котором собираются данные экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b9a80-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="b9a80-179">Значение должно составлять от 5 минут до 12 часов.</span><span class="sxs-lookup"><span data-stu-id="b9a80-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="b9a80-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="b9a80-180">**timeAggregation**</span></span>  
    <span data-ttu-id="b9a80-181">его значение определяет способ объединения собираемых данных hello со временем.</span><span class="sxs-lookup"><span data-stu-id="b9a80-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="b9a80-182">значение по умолчанию Hello — среднее значение.</span><span class="sxs-lookup"><span data-stu-id="b9a80-182">hello default value is Average.</span></span> <span data-ttu-id="b9a80-183">Возможные значения Hello: среднее, минимальное, максимальное, конец, общее, число.</span><span class="sxs-lookup"><span data-stu-id="b9a80-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="b9a80-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="b9a80-184">**operator**</span></span>  
    <span data-ttu-id="b9a80-185">Это значение является hello оператор, который используется toocompare hello метрики данных и hello порогового значения.</span><span class="sxs-lookup"><span data-stu-id="b9a80-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="b9a80-186">Hello возможными значениями являются: равно NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="b9a80-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="b9a80-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="b9a80-187">**threshold**</span></span>  
    <span data-ttu-id="b9a80-188">Это значение является hello значение, которое запускает действие масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="b9a80-189">В этом шаблоне машины добавляются в набор при hello средняя загрузка ЦП между машинами в наборе hello более чем на 50% toohello масштабирования.</span><span class="sxs-lookup"><span data-stu-id="b9a80-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="b9a80-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="b9a80-190">**direction**</span></span>  
    <span data-ttu-id="b9a80-191">Это значение определяет hello действие, которое предпринимается, когда достигается пороговое значение hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="b9a80-192">Возможные значения Hello: увеличиваются или уменьшаются.</span><span class="sxs-lookup"><span data-stu-id="b9a80-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="b9a80-193">В этом шаблоне hello количество виртуальных машин в наборе масштабирования hello увеличивается, если пороговое значение hello более чем на 50% hello в определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="b9a80-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="b9a80-194">**type**</span><span class="sxs-lookup"><span data-stu-id="b9a80-194">**type**</span></span>  
    <span data-ttu-id="b9a80-195">Это значение является hello тип действия, которое должно выполняться и значением tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="b9a80-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="b9a80-196">**значение**</span><span class="sxs-lookup"><span data-stu-id="b9a80-196">**value**</span></span>  
    <span data-ttu-id="b9a80-197">Это значение является hello число виртуальных машин, которые добавляются или удаляются из набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="b9a80-198">Для этого параметра должно быть указано значение не меньше 1.</span><span class="sxs-lookup"><span data-stu-id="b9a80-198">This value must be 1 or greater.</span></span> <span data-ttu-id="b9a80-199">значение по умолчанию Hello-1.</span><span class="sxs-lookup"><span data-stu-id="b9a80-199">hello default value is 1.</span></span> <span data-ttu-id="b9a80-200">В этом шаблоне hello количество машин в шкале hello набора увеличивается на 1 при достижении порога hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="b9a80-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="b9a80-201">**cooldown**</span></span>  
    <span data-ttu-id="b9a80-202">Это значение является hello объем toowait времени с момента последнего действия масштабирования hello, прежде чем произойдет следующее действие hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="b9a80-203">Допустимые значения: от одной минуты до одной недели.</span><span class="sxs-lookup"><span data-stu-id="b9a80-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="b9a80-204">Сохраните файл шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="b9a80-205">Шаг 4: Отправка шаблона toostorage hello</span><span class="sxs-lookup"><span data-stu-id="b9a80-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="b9a80-206">можно загрузить шаблон Hello, при условии, что известно имя hello и первичный ключ учетной записи хранения hello, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="b9a80-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="b9a80-207">В Microsoft Azure PowerShell hello задайте переменную, указывающую имя hello hello учетной записи хранения, созданной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="b9a80-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="b9a80-208">Задайте переменную, указывающую hello первичного ключа учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="b9a80-209">Этот ключ можно получить, щелкнув значок ключа hello при просмотре hello ресурс учетной записи хранения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9a80-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="b9a80-210">Создайте объект контекста учетной записи хранилища hello, используемые toovalidate операций с учетной записью хранения hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="b9a80-211">Создание контейнера hello для хранения шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="b9a80-212">Отправьте новый контейнер файла шаблона toohello hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="b9a80-213">Шаг 5: Применение шаблона hello</span><span class="sxs-lookup"><span data-stu-id="b9a80-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="b9a80-214">Теперь, когда вы создали шаблон hello, можно начать развертывание ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="b9a80-215">Используйте этот процесс hello toostart команды:</span><span class="sxs-lookup"><span data-stu-id="b9a80-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="b9a80-216">При нажатии клавиши ВВОД, запрашиваемые tooprovide значения переменных hello, назначенные вами.</span><span class="sxs-lookup"><span data-stu-id="b9a80-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="b9a80-217">Укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b9a80-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="b9a80-218">Для развертывания всех toosuccessfully ресурсы hello он займет около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="b9a80-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a80-219">Также можно использовать портал hello возможность toodeploy hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b9a80-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="b9a80-220">Используйте эту ссылку: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="b9a80-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="b9a80-221">Шаг 6. Мониторинг ресурсов</span><span class="sxs-lookup"><span data-stu-id="b9a80-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="b9a80-222">Сведения о масштабируемых наборах виртуальных машин можно получать, используя следующие методы:</span><span class="sxs-lookup"><span data-stu-id="b9a80-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="b9a80-223">Здравствуйте, портал Azure — в настоящее время можно получить ограниченный объем информации с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="b9a80-224">Hello [обозревателя ресурсов Azure](https://resources.azure.com/) -это средство — hello, наилучшим образом подходит для изучения hello текущее состояние набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="b9a80-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="b9a80-225">Выполните этот путь, и вы увидите набор, созданный представление экземпляра hello hello шкалы:</span><span class="sxs-lookup"><span data-stu-id="b9a80-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="b9a80-226">subscriptions > {ваша подписка} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="b9a80-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="b9a80-227">Azure PowerShell, используйте tooget этой команды некоторые сведения:</span><span class="sxs-lookup"><span data-stu-id="b9a80-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="b9a80-228">Или</span><span class="sxs-lookup"><span data-stu-id="b9a80-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="b9a80-229">Подключение toohello отдельной виртуальной машине, так же, как и любой другой компьютер и затем позволяет осуществлять удаленный доступ hello виртуальных машин в отдельных процессах набор масштабирования toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a80-230">Полный REST API для получения информации о масштабируемых наборах можно найти на странице [Масштабируемые наборы виртуальных машин](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="b9a80-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="b9a80-231">Шаг 7: Удаление ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="b9a80-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="b9a80-232">Поскольку вы оплачивать ресурсы, используемые в Azure, это всегда ресурсов toodelete рекомендаций, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="b9a80-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="b9a80-233">Не нужно toodelete каждого ресурса, отдельно от группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b9a80-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="b9a80-234">Можно удалить группу ресурсов hello и автоматически удаляются все ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b9a80-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="b9a80-235">Если требуется tookeep группы ресурсов, можно удалить только набор масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="b9a80-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="b9a80-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9a80-236">Next steps</span></span>
* <span data-ttu-id="b9a80-237">Управление hello масштабного набора только что создан с использованием информации hello в [управление виртуальными машинами в наборе масштабирования виртуальных машин](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="b9a80-238">Дополнительные сведения о вертикальном масштабировании см. в статье [Вертикальное автомасштабирование наборов масштабирования виртуальных машин](virtual-machine-scale-sets-vertical-scale-reprovision.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="b9a80-239">Просмотрите примеры функций мониторинга Azure Monitor в статье [Примеры для быстрого запуска Azure Insights с помощью PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b9a80-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="b9a80-240">Дополнительные сведения о функции уведомлений в [используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="b9a80-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="b9a80-241">Узнайте, каким образом слишком[журналы аудита используйте toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="b9a80-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

