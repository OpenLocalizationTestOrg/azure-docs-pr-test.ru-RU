---
title: "Наборы масштабирования виртуальных машин Linux aaaAutoscale | Документы Microsoft"
description: "Настройка масштабирования для набора масштабирования виртуальных машин Linux с помощью интерфейса командной строки Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="a078a-103">Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a078a-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="a078a-104">Наборы масштабирования виртуальных машин упростить для вас toodeploy идентичные виртуальных машин и управление как набор.</span><span class="sxs-lookup"><span data-stu-id="a078a-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="a078a-105">Масштабируемые наборы обеспечивают высокую степень масштабируемости и персонализацию уровня вычислений для гипермасштабируемых приложений. Кроме того, они поддерживают образы платформ Windows и Linux, а также пользовательские образы и расширения.</span><span class="sxs-lookup"><span data-stu-id="a078a-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="a078a-106">toolearn более, в разделе [обзор наборов масштабирования виртуальных машин](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="a078a-107">Этом учебнике показано, как задать toocreate масштабирования виртуальных машин Linux с помощью последней версии hello Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="a078a-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="a078a-108">Hello учебнике также показано, как задать tooautomatically машины hello масштабирования в hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="a078a-109">Можно создать шкалу hello установить и настроить масштабирование, создание шаблона диспетчера ресурсов Azure и развертывая его с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a078a-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="a078a-110">Дополнительную информацию о шаблонах см. в статье [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a078a-111">toolearn Дополнительные сведения о автоматического масштабирования наборы масштабирования в разделе [автоматического масштабирования и виртуальной машины задает масштаб](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="a078a-112">В этом учебнике развертывание hello следующих ресурсов и расширения:</span><span class="sxs-lookup"><span data-stu-id="a078a-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="a078a-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="a078a-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="a078a-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="a078a-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="a078a-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="a078a-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="a078a-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="a078a-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="a078a-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="a078a-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="a078a-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="a078a-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="a078a-119">Microsoft.Compute/virtualMachineScaleSets;</span><span class="sxs-lookup"><span data-stu-id="a078a-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="a078a-120">Microsoft.Insights.VMDiagnosticsSettings;</span><span class="sxs-lookup"><span data-stu-id="a078a-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="a078a-121">Microsoft.Insights/autoscaleSettings.</span><span class="sxs-lookup"><span data-stu-id="a078a-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="a078a-122">Дополнительные сведения о ресурсах Resource Manager см. в статье [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) (Развертывание с помощью Azure Resource Manager и классическое развертывание).</span><span class="sxs-lookup"><span data-stu-id="a078a-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="a078a-123">Перед началом работы с hello шаги в этом учебнике [установить hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="a078a-124">Шаг 1. Создание группы ресурсов и учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="a078a-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="a078a-125">**Войдите в tooMicrosoft Azure**</span><span class="sxs-lookup"><span data-stu-id="a078a-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="a078a-126">В интерфейсе командной строки (Bash, терминалов, командной строке) режима tooResource Manager, а затем [вход с идентификатором рабочей или учебной](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Следуйте инструкциям hello для интерактивного входа в систему качества tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a078a-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="a078a-127">Если вас есть рабочая идентификатор и не двухфакторная проверка подлинности включена, то следует использовать `azure login -u` с Идентификатором toolog hello в без интерактивного сеанса.</span><span class="sxs-lookup"><span data-stu-id="a078a-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="a078a-128">Если у вас нет рабочего или учебного идентификатора, его можно [создать в личной учетной записи Майкрософт](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="a078a-129">**Создайте группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="a078a-129">**Create a resource group**</span></span>  
<span data-ttu-id="a078a-130">Все ресурсы должны быть tooa развернутой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a078a-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="a078a-131">В этом учебнике, имя группы ресурсов hello **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="a078a-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="a078a-132">**Развертывание учетной записи хранения в новую группу ресурсов hello**</span><span class="sxs-lookup"><span data-stu-id="a078a-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="a078a-133">Эта учетная запись хранения —, где хранится шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="a078a-134">Создайте учетную запись хранения с именем **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="a078a-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="a078a-135">Шаг 2: Создание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="a078a-135">Step 2: Create hello template</span></span>
<span data-ttu-id="a078a-136">Шаблон диспетчера ресурсов Azure позволяет вам toodeploy и управлять ресурсами Azure совместно с помощью описания JSON ресурсов hello и связанных параметров развертывания.</span><span class="sxs-lookup"><span data-stu-id="a078a-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="a078a-137">В любом редакторе создайте файл hello VMSSTemplate.json и добавьте hello исходного JSON структуры toosupport hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="a078a-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="a078a-138">Параметры обычно не требуется, но они обеспечивают tooinput способом значения при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="a078a-139">Добавление этих параметров hello параметров родительского элемента, что вы добавили шаблон toohello.</span><span class="sxs-lookup"><span data-stu-id="a078a-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="a078a-140">Имя для hello отдельной виртуальной машине, используемых tooaccess hello машины в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="a078a-141">Имя для учетной записи хранения hello, где хранится шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="a078a-142">Hello число экземпляров виртуальных машин tooinitially создать в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="a078a-143">Имя и пароль учетной записи администратора hello на виртуальных машинах hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="a078a-144">Задайте префикс имени hello ресурсов, которые создаются toosupport hello шкалы.</span><span class="sxs-lookup"><span data-stu-id="a078a-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="a078a-145">Переменные могут использоваться в значениях toospecify шаблона, которые могут часто изменяться или значения, которые необходимо toobe, созданные на основе сочетания значений параметров.</span><span class="sxs-lookup"><span data-stu-id="a078a-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="a078a-146">Добавьте эти переменные hello переменные родительского элемента, что вы добавили шаблон toohello.</span><span class="sxs-lookup"><span data-stu-id="a078a-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="a078a-147">DNS-имена, которые используются в hello сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="a078a-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="a078a-148">Hello IP адрес имена и префиксы для hello виртуальную сеть и подсети.</span><span class="sxs-lookup"><span data-stu-id="a078a-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="a078a-149">Hello имена и идентификаторы hello виртуальной сети, подсистема балансировки нагрузки и сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="a078a-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="a078a-150">Имена учетной записи хранения для hello учетных записей, связанных с машинами hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="a078a-151">Параметры для расширения диагностики, которая устанавливается на виртуальных машинах hello hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="a078a-152">Дополнительные сведения о hello расширения диагностики см. в разделе [создать Windows виртуальной машины с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a078a-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="a078a-153">Добавьте ресурс учетной записи хранения hello hello ресурсы родительского элемента, что вы добавили шаблон toohello.</span><span class="sxs-lookup"><span data-stu-id="a078a-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="a078a-154">Этот шаблон использует hello toocreate цикла, рекомендуется использовать пять учетных записей хранилища, место хранения hello дисков операционной системы и диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="a078a-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="a078a-155">Этот набор учетных записей может поддерживать до too100 виртуальных машин в наборе масштабирования, — текущий максимум hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="a078a-156">Каждая учетная запись хранения называется с буквенный код, которое было определено в переменных hello, суффикс "hello", укажите в параметрах hello для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="a078a-157">Добавьте ресурс hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a078a-157">Add hello virtual network resource.</span></span> <span data-ttu-id="a078a-158">Дополнительную информацию см. в статье [Поставщик сетевых ресурсов](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="a078a-159">Добавьте hello открытые ресурсы IP-адресов, используемых hello Подсистема балансировки нагрузки и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a078a-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="a078a-160">Добавьте ресурс балансировки нагрузки hello, который используется набором масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="a078a-161">Дополнительные сведения см. в статье, посвященной [поддержке Azure Resource Manager для подсистемы балансировки нагрузки](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="a078a-162">Добавьте hello ресурс сетевого интерфейса, используемый hello отдельной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a078a-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="a078a-163">Поскольку машины в наборе масштабирования не доступны через общедоступный IP-адрес, отдельная виртуальная машина создается в hello же виртуальных машин hello tooremotely доступа к сети.</span><span class="sxs-lookup"><span data-stu-id="a078a-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="a078a-164">Добавьте hello отдельной виртуальной машины в сетевых как набор масштабирования hello hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. <span data-ttu-id="a078a-165">Добавление ресурса набора масштабирования виртуальных машин hello и укажите расширение диагностики hello, установленного на всех виртуальных машин в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="a078a-166">Многие из параметров hello для этого ресурса похожи hello ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a078a-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="a078a-167">Ниже перечислены основные различия Hello hello емкости элемент, который задает hello количество виртуальных машин в наборе масштабирования hello и upgradePolicy, указывающее, каким образом производятся изменения toovirtual машины.</span><span class="sxs-lookup"><span data-stu-id="a078a-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="a078a-168">Hello масштабный набор не создается, пока все учетные записи хранения hello создаются в соответствии с элементом dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="a078a-169">Добавьте ресурс autoscaleSettings hello, который определяет, как набор масштабирования hello корректирует зависимости от использования процессора на машинах hello в наборе hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    
    <span data-ttu-id="a078a-170">Для целей этого руководства важны значения следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="a078a-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="a078a-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="a078a-171">**metricName**</span></span>  
    <span data-ttu-id="a078a-172">Это значение является hello то же, что счетчик производительности hello, которое было определено в переменной wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="a078a-173">С помощью этой переменной, hello расширения диагностики собирает hello **Processor\PercentProcessorTime** счетчика.</span><span class="sxs-lookup"><span data-stu-id="a078a-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="a078a-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="a078a-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="a078a-175">Это значение является идентификатором ресурса hello hello набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a078a-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="a078a-176">**timegrain**</span><span class="sxs-lookup"><span data-stu-id="a078a-176">**timeGrain**</span></span>  
    <span data-ttu-id="a078a-177">Это значение является гранулярности hello hello метрик, которые собираются.</span><span class="sxs-lookup"><span data-stu-id="a078a-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="a078a-178">В этом шаблоне задается tooone минуты.</span><span class="sxs-lookup"><span data-stu-id="a078a-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="a078a-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="a078a-179">**statistic**</span></span>  
    <span data-ttu-id="a078a-180">Это значение определяет, как метрики hello hello объединенный tooaccommodate автоматического масштабирования действия.</span><span class="sxs-lookup"><span data-stu-id="a078a-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="a078a-181">Возможные значения Hello: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="a078a-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="a078a-182">В этом шаблоне собираются hello среднее общее использование ЦП hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a078a-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="a078a-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="a078a-183">**timeWindow**</span></span>  
    <span data-ttu-id="a078a-184">Это значение является hello диапазон времени, в котором собираются данные экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a078a-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="a078a-185">Значение должно составлять от 5 минут до 12 часов.</span><span class="sxs-lookup"><span data-stu-id="a078a-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="a078a-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="a078a-186">**timeAggregation**</span></span>  
    <span data-ttu-id="a078a-187">его значение определяет способ объединения собираемых данных hello со временем.</span><span class="sxs-lookup"><span data-stu-id="a078a-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="a078a-188">значение по умолчанию Hello — среднее значение.</span><span class="sxs-lookup"><span data-stu-id="a078a-188">hello default value is Average.</span></span> <span data-ttu-id="a078a-189">Возможные значения Hello: среднее, минимальное, максимальное, конец, общее, число.</span><span class="sxs-lookup"><span data-stu-id="a078a-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="a078a-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="a078a-190">**operator**</span></span>  
    <span data-ttu-id="a078a-191">Это значение является hello оператор, который используется toocompare hello метрики данных и hello порогового значения.</span><span class="sxs-lookup"><span data-stu-id="a078a-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="a078a-192">Hello возможными значениями являются: равно NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="a078a-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="a078a-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="a078a-193">**threshold**</span></span>  
    <span data-ttu-id="a078a-194">Это значение запускает действие масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-194">This value triggers hello scale action.</span></span> <span data-ttu-id="a078a-195">В этом шаблоне машины добавляются в набор при hello средняя загрузка ЦП между машинами в наборе hello более чем на 50% toohello масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a078a-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="a078a-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="a078a-196">**direction**</span></span>  
    <span data-ttu-id="a078a-197">Это значение определяет hello действие, которое предпринимается, когда достигается пороговое значение hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="a078a-198">Возможные значения Hello: увеличиваются или уменьшаются.</span><span class="sxs-lookup"><span data-stu-id="a078a-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="a078a-199">В этом шаблоне hello количество виртуальных машин в наборе масштабирования hello увеличивается, если пороговое значение hello более чем на 50% hello в определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="a078a-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="a078a-200">**type**</span><span class="sxs-lookup"><span data-stu-id="a078a-200">**type**</span></span>  
    <span data-ttu-id="a078a-201">Это значение является hello тип действия, которое должно выполняться и значением tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="a078a-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="a078a-202">**значение**</span><span class="sxs-lookup"><span data-stu-id="a078a-202">**value**</span></span>  
    <span data-ttu-id="a078a-203">Это значение является hello число виртуальных машин, которые добавляются или удаляются из набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="a078a-204">Для этого параметра должно быть указано значение не меньше 1.</span><span class="sxs-lookup"><span data-stu-id="a078a-204">This value must be 1 or greater.</span></span> <span data-ttu-id="a078a-205">значение по умолчанию Hello-1.</span><span class="sxs-lookup"><span data-stu-id="a078a-205">hello default value is 1.</span></span> <span data-ttu-id="a078a-206">В этом шаблоне hello количество машин в шкале hello набора увеличивается на 1 при достижении порога hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="a078a-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="a078a-207">**cooldown**</span></span>  
    <span data-ttu-id="a078a-208">Это значение является hello объем toowait времени с момента последнего действия масштабирования hello, прежде чем произойдет следующее действие hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="a078a-209">Допустимые значения: от одной минуты до одной недели.</span><span class="sxs-lookup"><span data-stu-id="a078a-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="a078a-210">Сохраните файл шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="a078a-211">Шаг 3: Отправка шаблона toostorage hello</span><span class="sxs-lookup"><span data-stu-id="a078a-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="a078a-212">можно загрузить шаблон Hello, при условии, что известно имя hello и первичный ключ учетной записи хранения hello, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="a078a-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="a078a-213">В интерфейсе командной строки (Bash, терминалов, командной строке) выполните следующие команды переменные среды hello tooset необходимости tooaccess hello учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="a078a-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="a078a-214">Hello ключ можно получить, щелкнув значок ключа hello при просмотре hello ресурс учетной записи хранения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a078a-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="a078a-215">Если вы используете командную строку Windows, введите **set** вместо export.</span><span class="sxs-lookup"><span data-stu-id="a078a-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="a078a-216">Создание контейнера hello для хранения шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="a078a-217">Отправьте новый контейнер файла шаблона toohello hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="a078a-218">Шаг 4: Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="a078a-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="a078a-219">Теперь, когда вы создали шаблон hello, можно начать развертывание ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="a078a-220">Используйте этот процесс hello toostart команды:</span><span class="sxs-lookup"><span data-stu-id="a078a-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="a078a-221">При нажатии клавиши ВВОД, запрашиваемые tooprovide значения переменных hello, назначенные вами.</span><span class="sxs-lookup"><span data-stu-id="a078a-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="a078a-222">Укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a078a-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="a078a-223">Для развертывания всех toosuccessfully ресурсы hello он займет около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="a078a-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="a078a-224">Также можно использовать портал hello возможность toodeploy hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a078a-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="a078a-225">Используйте эту ссылку: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>.</span><span class="sxs-lookup"><span data-stu-id="a078a-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="a078a-226">Шаг 5. Мониторинг ресурсов</span><span class="sxs-lookup"><span data-stu-id="a078a-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="a078a-227">Сведения о масштабируемых наборах виртуальных машин можно получать, используя следующие методы:</span><span class="sxs-lookup"><span data-stu-id="a078a-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="a078a-228">Здравствуйте, портал Azure — в настоящее время можно получить ограниченный объем информации с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="a078a-229">Hello [обозревателя ресурсов Azure](https://resources.azure.com/) -это средство — hello, наилучшим образом подходит для изучения hello текущее состояние набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a078a-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="a078a-230">Выполните этот путь, и вы увидите набор, созданный представление экземпляра hello hello шкалы:</span><span class="sxs-lookup"><span data-stu-id="a078a-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="a078a-231">Azure CLI - используйте этот tooget команда некоторые сведения:</span><span class="sxs-lookup"><span data-stu-id="a078a-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="a078a-232">Подключение toohello jumpbox виртуальной машины, так же, как и любой другой компьютер и затем позволяет осуществлять удаленный доступ hello виртуальных машин в отдельных процессах набор масштабирования toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a078a-233">Полный REST API для получения информации о масштабируемых наборах можно найти на странице [Масштабируемые наборы виртуальных машин](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="a078a-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="a078a-234">Шаг 6: Удаление ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="a078a-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="a078a-235">Поскольку вы оплачивать ресурсы, используемые в Azure, это всегда ресурсов toodelete рекомендаций, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="a078a-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="a078a-236">Не нужно toodelete каждого ресурса, отдельно от группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a078a-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="a078a-237">Можно удалить группу ресурсов hello и автоматически удаляются все ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a078a-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="a078a-238">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a078a-238">Next steps</span></span>
* <span data-ttu-id="a078a-239">Просмотрите примеры функций мониторинга Azure Monitor в статье [Шаблоны для быстрого начала работы с межплатформенным интерфейсом командной строки Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="a078a-240">Дополнительные сведения о функции уведомлений в [используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a078a-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="a078a-241">Узнайте, каким образом слишком[журналы аудита используйте toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a078a-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="a078a-242">Извлечение hello [автомасштабирования нашего примера приложения на Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) шаблон, который настраивает hello tooexercise приложения Python и Фляга для автоматического масштабирования функциональность наборы масштабирования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a078a-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

