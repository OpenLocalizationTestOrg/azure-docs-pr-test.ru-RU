---
title: "Создание групп безопасности сети с помощью шаблона Azure Resource Manager | Документация Майкрософт"
description: "Узнайте, как создавать и развертывать группы безопасности сети с помощью шаблона Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88f7e5b2144daee7bf1c8e7312ba98e6fa967899
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="0806e-103">Создание групп безопасности сети с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0806e-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="0806e-104">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0806e-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="0806e-105">Вы также можете [создавать группы безопасности сети с помощью классической модели развертывания](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0806e-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="0806e-106">Ресурсы сетевой группы безопасности в файле шаблона</span><span class="sxs-lookup"><span data-stu-id="0806e-106">NSG resources in a template file</span></span>
<span data-ttu-id="0806e-107">Вы можете просмотреть и скачать [образец шаблона](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="0806e-107">You can view and download the [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="0806e-108">В следующем разделе показано определение группы безопасности сети переднего плана на основе этого сценария.</span><span class="sxs-lookup"><span data-stu-id="0806e-108">The following section shows the definition of the front-end NSG, based on the scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="0806e-109">Чтобы связать группу безопасности сети с подсетью переднего плана, необходимо изменить определение подсети в шаблоне и использовать идентификатор ссылки для группы.</span><span class="sxs-lookup"><span data-stu-id="0806e-109">To associate the NSG to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="0806e-110">Обратите внимание, чтобы то же самое было сделано для серверной группы безопасности сети и серверной подсети в этом шаблоне.</span><span class="sxs-lookup"><span data-stu-id="0806e-110">Notice the same being done for the back-end NSG and the back-end subnet in the template.</span></span>

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="0806e-111">Развертывание шаблона ARM с помощью кнопки развертывания</span><span class="sxs-lookup"><span data-stu-id="0806e-111">Deploy the ARM template by using click to deploy</span></span>
<span data-ttu-id="0806e-112">Образец шаблона, который находится в общедоступном репозитории, использует файл параметров, содержащий значения по умолчанию для создания описанного выше сценария.</span><span class="sxs-lookup"><span data-stu-id="0806e-112">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="0806e-113">Чтобы развернуть этот шаблон, перейдите по [данной ссылке](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), нажмите **Deploy to Azure**(Развернуть в Azure), при необходимости замените значения параметров по умолчанию и следуйте указаниям на портале.</span><span class="sxs-lookup"><span data-stu-id="0806e-113">To deploy this template using click to deploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-arm-template-by-using-powershell"></a><span data-ttu-id="0806e-114">Развертывание шаблона ARM с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0806e-114">Deploy the ARM template by using PowerShell</span></span>
<span data-ttu-id="0806e-115">Чтобы развернуть шаблон ARM, загруженный с помощью PowerShell, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="0806e-115">To deploy the ARM template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="0806e-116">Если вы ранее не использовали Azure PowerShell, следуйте инструкциям по установке и настройке Azure PowerShell в [этой статье](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0806e-116">If you have never used Azure PowerShell, follow the instructions in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) to install and configure it.</span></span>
2. <span data-ttu-id="0806e-117">Запустите командлет **`New-AzureRmResourceGroup`** для создания группы ресурсов с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="0806e-117">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="0806e-118">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0806e-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-the-arm-template-by-using-the-azure-cli"></a><span data-ttu-id="0806e-119">Развертывание шаблона ARM с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="0806e-119">Deploy the ARM template by using the Azure CLI</span></span>
<span data-ttu-id="0806e-120">Чтобы развернуть шаблон ARM с помощью интерфейса командной строки Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0806e-120">To deploy the ARM template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="0806e-121">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="0806e-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0806e-122">Выполните команду **`azure config mode`** , чтобы переключиться в режим диспетчера ресурсов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0806e-122">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="0806e-123">Вот результат, ожидаемый для указанной выше команды:</span><span class="sxs-lookup"><span data-stu-id="0806e-123">The following is the expected output for the command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="0806e-124">Выполните командлет **`azure group deployment create`** , чтобы развернуть новую виртуальную сеть с помощью файлов шаблона и параметров, которые вы загрузили и изменили раньше.</span><span class="sxs-lookup"><span data-stu-id="0806e-124">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="0806e-125">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="0806e-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="0806e-126">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0806e-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="0806e-127">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="0806e-127">**-n (or --name)**.</span></span> <span data-ttu-id="0806e-128">Имя создаваемой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0806e-128">Name of the resource group to be created.</span></span>
   * <span data-ttu-id="0806e-129">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="0806e-129">**-l (or --location)**.</span></span> <span data-ttu-id="0806e-130">Регион Azure, в котором будет создана группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0806e-130">Azure region where the resource group will be created.</span></span>
   * <span data-ttu-id="0806e-131">**-f (или --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="0806e-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="0806e-132">Путь к файлу шаблона ARM.</span><span class="sxs-lookup"><span data-stu-id="0806e-132">Path to your ARM template file.</span></span>
   * <span data-ttu-id="0806e-133">**-e (или --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="0806e-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="0806e-134">Путь к файлу параметров ARM.</span><span class="sxs-lookup"><span data-stu-id="0806e-134">Path to your ARM parameters file.</span></span>

