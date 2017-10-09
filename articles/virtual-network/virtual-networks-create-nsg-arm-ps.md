---
title: "aaaCreate сетевых групп безопасности - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание сетевых групп безопасности с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="97822-103">Создание групп безопасности сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="97822-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="97822-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="97822-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="97822-105">Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="97822-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="97822-106">Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="97822-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="97822-107">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="97822-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="97822-108">Вы также можете [создать Nsg в hello классической модели развертывания](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="97822-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="97822-109">Образец Hello PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="97822-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="97822-110">Toorun hello команд, отображаемых в этом документе, сначала построения необходимо hello тестовой среды, развернув [этот шаблон](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello При необходимости и выполнения инструкции hello в hello портала.</span><span class="sxs-lookup"><span data-stu-id="97822-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="97822-111">Как toocreate hello NSG для подсети hello переднего плана</span><span class="sxs-lookup"><span data-stu-id="97822-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="97822-112">toocreate NSG с именем *NSG-FrontEnd* в зависимости от сценария hello завершения hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="97822-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="97822-113">Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="97822-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="97822-114">Создаете правило безопасности, разрешающее доступ из Интернета hello tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="97822-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="97822-115">Создаете правило безопасности, разрешающее доступ из Интернета hello tooport 80.</span><span class="sxs-lookup"><span data-stu-id="97822-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="97822-116">Добавить правила hello, созданной ранее с именем новой NSG tooa **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="97822-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="97822-117">Проверка hello правила, созданные в hello NSG, введя hello следующее:</span><span class="sxs-lookup"><span data-stu-id="97822-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="97822-118">Выходные данные правил безопасности просто hello отображение:</span><span class="sxs-lookup"><span data-stu-id="97822-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="97822-119">Свяжите hello NSG созданной выше toohello *переднего плана* подсети.</span><span class="sxs-lookup"><span data-stu-id="97822-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="97822-120">Выходные данные отображение только hello *переднего плана* настройки подсети, значение hello уведомления для hello **NetworkSecurityGroup** свойства:</span><span class="sxs-lookup"><span data-stu-id="97822-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="97822-121">Hello для приведенных выше команд hello видно содержимое hello hello объекта конфигурации виртуальной сети, который существует только на компьютере hello, где запускается PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97822-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="97822-122">Требуется toorun hello `Set-AzureRmVirtualNetwork` toosave командлет tooAzure эти параметры.</span><span class="sxs-lookup"><span data-stu-id="97822-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="97822-123">Сохраните hello новой виртуальной сети параметры tooAzure.</span><span class="sxs-lookup"><span data-stu-id="97822-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="97822-124">Выходные данные отображаются только часть NSG hello:</span><span class="sxs-lookup"><span data-stu-id="97822-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="97822-125">Как toocreate hello NSG для hello конечной подсети</span><span class="sxs-lookup"><span data-stu-id="97822-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="97822-126">toocreate NSG с именем *NSG серверной* на основании выше сценарий hello, завершения hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="97822-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="97822-127">Создаете правило безопасности, разрешающее доступ из интерфейса подсети hello tooport 1433 (по умолчанию порт, используемый сервером SQL Server).</span><span class="sxs-lookup"><span data-stu-id="97822-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="97822-128">Создаете правило безопасности блокирует toohello доступа к Интернету.</span><span class="sxs-lookup"><span data-stu-id="97822-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="97822-129">Добавить правила hello, созданной ранее с именем новой NSG tooa **NSG серверной**.</span><span class="sxs-lookup"><span data-stu-id="97822-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="97822-130">Свяжите hello NSG созданной выше toohello *серверной* подсети.</span><span class="sxs-lookup"><span data-stu-id="97822-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="97822-131">Hello только Отображение выходных данных *серверной* настройки подсети, значение hello уведомления для hello **NetworkSecurityGroup** свойства:</span><span class="sxs-lookup"><span data-stu-id="97822-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="97822-132">Сохраните hello новой виртуальной сети параметры tooAzure.</span><span class="sxs-lookup"><span data-stu-id="97822-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="97822-133">Как tooremove NSG</span><span class="sxs-lookup"><span data-stu-id="97822-133">How tooremove an NSG</span></span>
<span data-ttu-id="97822-134">toodelete существующей NSG, вызывается *NSG-Frontend* в этом случае выполните шаг hello ниже:</span><span class="sxs-lookup"><span data-stu-id="97822-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="97822-135">Запустите hello **AzureRmNetworkSecurityGroup удаление** показано ниже и быть NSG находится в hello ресурсов группы, что tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="97822-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

