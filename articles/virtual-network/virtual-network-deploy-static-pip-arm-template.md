---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toocreate виртуальную Машину с статический общедоступный IP-адрес решения с помощью шаблона диспетчера ресурсов Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="fd664-103">Создание виртуальной машины со статическим общедоступным IP-адресом с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd664-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd664-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="fd664-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="fd664-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd664-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="fd664-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="fd664-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="fd664-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="fd664-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="fd664-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="fd664-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fd664-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fd664-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fd664-110">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd664-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="fd664-111">Ресурсы общедоступного IP-адреса в файле шаблона</span><span class="sxs-lookup"><span data-stu-id="fd664-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="fd664-112">Можно просматривать и загружать hello [образец шаблона](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fd664-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="fd664-113">Hello ниже показано определение hello hello открытый IP ресурсу на основе hello сценарии выше:</span><span class="sxs-lookup"><span data-stu-id="fd664-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="fd664-114">Обратите внимание hello **publicIPAllocationMethod** свойство, которое задано слишком*статических*.</span><span class="sxs-lookup"><span data-stu-id="fd664-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="fd664-115">Это свойство может иметь значение либо *Dynamic* (значение по умолчанию), либо *Static*.</span><span class="sxs-lookup"><span data-stu-id="fd664-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="fd664-116">Настройка toostatic гарантии, которые никогда не изменяют общий IP-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="fd664-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="fd664-117">Hello следующем разделе показано сопоставление hello hello общедоступного IP-адреса с сетевым интерфейсом:</span><span class="sxs-lookup"><span data-stu-id="fd664-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="fd664-118">Обратите внимание hello **publicIPAddress** свойство, указывающее toohello **идентификатор** ресурс с именем **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="fd664-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="fd664-119">Это имя hello открытый IP-ресурс hello показано выше.</span><span class="sxs-lookup"><span data-stu-id="fd664-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="fd664-120">Наконец, выше hello сетевой интерфейс указан в hello **параметров масштабирования виртуальных** свойство hello создаваемой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fd664-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="fd664-121">Развертывание с помощью шаблона hello щелкните toodeploy</span><span class="sxs-lookup"><span data-stu-id="fd664-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="fd664-122">шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="fd664-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="fd664-123">toodeploy это с помощью шаблона щелкните toodeploy, нажмите кнопку **развертывание tooAzure** в файле Readme.md hello для hello [виртуальной Машины с помощью статических PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) шаблона.</span><span class="sxs-lookup"><span data-stu-id="fd664-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="fd664-124">При необходимости замените значения параметров по умолчанию hello и введите значения для параметров пустой hello.</span><span class="sxs-lookup"><span data-stu-id="fd664-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="fd664-125">Следуйте инструкциям hello hello портала toocreate виртуальную машину с статический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="fd664-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="fd664-126">Развертывание hello шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd664-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="fd664-127">toodeploy hello шаблона, загруженного с помощью PowerShell, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="fd664-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="fd664-128">Если ранее не пользовались Azure PowerShell, hello завершения шагов в hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="fd664-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="fd664-129">В консоли PowerShell запустите hello `New-AzureRmResourceGroup` toocreate командлета новую группу ресурсов, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="fd664-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="fd664-130">Если уже созданы группы ресурсов, воспользуйтесь toostep 3.</span><span class="sxs-lookup"><span data-stu-id="fd664-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="fd664-131">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fd664-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="fd664-132">В консоли PowerShell запустите hello `New-AzureRmResourceGroupDeployment` шаблон hello toodeploy командлета.</span><span class="sxs-lookup"><span data-stu-id="fd664-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="fd664-133">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fd664-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="fd664-134">Развертывание hello шаблона с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fd664-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="fd664-135">toodeploy hello шаблона с использованием hello Azure CLI, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fd664-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="fd664-136">Если ранее не пользовались Azure CLI, выполните действия hello в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) статью tooinstall и настройте его.</span><span class="sxs-lookup"><span data-stu-id="fd664-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="fd664-137">Запустите hello `azure config mode` tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fd664-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="fd664-138">Hello ожидаемый результат для приведенных выше команд hello:</span><span class="sxs-lookup"><span data-stu-id="fd664-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="fd664-139">Откройте hello [файл параметров](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), выберите его содержимое и сохраните файл tooa на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="fd664-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="fd664-140">В этом примере hello параметры сохраняются в файл tooa с именем *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="fd664-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="fd664-141">Изменить значения параметров hello в файле hello, при необходимости, но как минимум, рекомендуется установить значение hello для hello adminPassword параметр tooa уникальный сложный пароль.</span><span class="sxs-lookup"><span data-stu-id="fd664-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="fd664-142">Запустите hello `azure group deployment create` файлов новой виртуальной сети с помощью шаблона hello и параметр cmd toodeploy hello вы загрузили и изменить выше.</span><span class="sxs-lookup"><span data-stu-id="fd664-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="fd664-143">В следующей команде hello, замените <path> hello путь был сохранен файл hello для.</span><span class="sxs-lookup"><span data-stu-id="fd664-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="fd664-144">Ожидаемый результат (перечисляются используемые значения параметров):</span><span class="sxs-lookup"><span data-stu-id="fd664-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

