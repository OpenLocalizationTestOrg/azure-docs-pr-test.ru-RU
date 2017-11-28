---
title: "aaaCreate сетевых групп безопасности - шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание сетевых групп безопасности с помощью шаблона диспетчера ресурсов Azure."
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
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="d1670-103">Создание групп безопасности сети с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1670-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d1670-104">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1670-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d1670-105">Вы также можете [создать Nsg в hello классической модели развертывания](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d1670-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="d1670-106">Ресурсы сетевой группы безопасности в файле шаблона</span><span class="sxs-lookup"><span data-stu-id="d1670-106">NSG resources in a template file</span></span>
<span data-ttu-id="d1670-107">Можно просматривать и загружать hello [образец шаблона](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="d1670-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="d1670-108">Hello ниже показано определение hello hello NSG переднего плана, в зависимости от варианта hello.</span><span class="sxs-lookup"><span data-stu-id="d1670-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

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
<span data-ttu-id="d1670-109">tooassociate hello NSG toohello интерфейса подсети получить определения подсети toochange hello в шаблоне hello и используйте идентификатор ссылки hello для hello NSG.</span><span class="sxs-lookup"><span data-stu-id="d1670-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

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

<span data-ttu-id="d1670-110">Обратите внимание на то же добиваются hello внутренней NSG и hello внутренней подсети в шаблоне hello hello.</span><span class="sxs-lookup"><span data-stu-id="d1670-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="d1670-111">Развертывание с помощью шаблона hello ARM щелкните toodeploy</span><span class="sxs-lookup"><span data-stu-id="d1670-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="d1670-112">шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="d1670-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="d1670-113">toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello при необходимости и следуйте инструкциям hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="d1670-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="d1670-114">Развертывание шаблона hello ARM с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1670-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="d1670-115">toodeploy hello ARM загруженный шаблон с помощью PowerShell, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d1670-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="d1670-116">Если ранее не пользовались Azure PowerShell, выполните инструкции hello hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) tooinstall и настройте его.</span><span class="sxs-lookup"><span data-stu-id="d1670-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="d1670-117">Запустите hello  **`New-AzureRmResourceGroup`**  toocreate командлет группы ресурсов с помощью hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="d1670-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="d1670-118">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d1670-118">Expected output:</span></span>

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

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="d1670-119">Развертывание шаблона hello ARM с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1670-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="d1670-120">toodeploy hello ARM шаблона с использованием hello Azure CLI, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d1670-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="d1670-121">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="d1670-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d1670-122">Запустите hello  **`azure config mode`**  tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d1670-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d1670-123">Hello Вот hello ожидается выходные данные команды hello:</span><span class="sxs-lookup"><span data-stu-id="d1670-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="d1670-124">Запустите hello  **`azure group deployment create`**  файлы новой виртуальной сети с помощью шаблонов hello и параметров командлета toodeploy hello вы загрузили и изменить выше.</span><span class="sxs-lookup"><span data-stu-id="d1670-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="d1670-125">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="d1670-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="d1670-126">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d1670-126">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="d1670-127">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="d1670-127">**-n (or --name)**.</span></span> <span data-ttu-id="d1670-128">Имя hello ресурсов группы toobe создан.</span><span class="sxs-lookup"><span data-stu-id="d1670-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="d1670-129">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="d1670-129">**-l (or --location)**.</span></span> <span data-ttu-id="d1670-130">Регион Azure, где будет создана группа ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="d1670-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="d1670-131">**-f (или --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="d1670-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="d1670-132">Путь к файлу шаблона tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="d1670-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="d1670-133">**-e (или --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="d1670-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="d1670-134">Путь к файлу параметров tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="d1670-134">Path tooyour ARM parameters file.</span></span>

