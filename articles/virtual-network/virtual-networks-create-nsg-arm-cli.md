---
title: "aaaCreate сетевых групп безопасности - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate и развертывание сетевых групп безопасности с помощью Azure CLI 2.0 hello."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="a9bf3-103">Создание группы безопасности с помощью Azure CLI 2.0 hello сети</span><span class="sxs-lookup"><span data-stu-id="a9bf3-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a9bf3-104">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="a9bf3-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="a9bf3-105">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="a9bf3-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления</span><span class="sxs-lookup"><span data-stu-id="a9bf3-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="a9bf3-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="a9bf3-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="a9bf3-108">Образец Hello Azure CLI 2.0 команды ниже ожидать простой среде уже создан на основании предыдущего сценария hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="a9bf3-109">Создать hello NSG для hello `FrontEnd` подсети</span><span class="sxs-lookup"><span data-stu-id="a9bf3-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="a9bf3-110">toocreate NSG с именем *NSG-FrontEnd* в зависимости от предыдущего сценария hello, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="a9bf3-111">Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a9bf3-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="a9bf3-112">Создание с помощью hello NSG [создать az сети nsg](/cli/azure/network/nsg#create) команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="a9bf3-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9bf3-113">Parameters:</span></span>
   
   * <span data-ttu-id="a9bf3-114">`--resource-group`: Имя группы ресурсов hello, где создается hello NSG.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="a9bf3-115">В данном сценарии это *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="a9bf3-116">`--location`: Azure регион, где hello новой NSG создается.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="a9bf3-117">В нашем случае это *westus*.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="a9bf3-118">`--name`: Имя hello новая NSG.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="a9bf3-119">В данном сценарии это *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="a9bf3-120">Hello тесты на ожидаемые выходные данные выглядят бит сведения, включая список всех правил по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="a9bf3-121">Hello пример hello правила по умолчанию, с помощью фильтра запроса JMESPATH с hello `table` формат вывода:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="a9bf3-122">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="a9bf3-123">Создать правило, разрешающее доступ tooport 3389 (RDP) из hello Интернета с hello [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a9bf3-124">В зависимости от hello оболочки используется, может потребоваться toomodify hello `*` знаку в hello аргументы после так как не tooexpand hello аргумент перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="a9bf3-125">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="a9bf3-126">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9bf3-126">Parameters:</span></span>

    * <span data-ttu-id="a9bf3-127">`--resource-group testrg`: hello toouse группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="a9bf3-128">Обратите внимание, что в ней не учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="a9bf3-129">`--nsg-name NSG-FrontEnd`: Имя hello NSG, в которой hello создается правило.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="a9bf3-130">`--name rdp-rule`: Имя для нового правила hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="a9bf3-131">`--access Allow`: Уровень доступа hello правила (запретить или разрешить).</span><span class="sxs-lookup"><span data-stu-id="a9bf3-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="a9bf3-132">`--protocol Tcp` — протокол (TCP, UDP или "*").</span><span class="sxs-lookup"><span data-stu-id="a9bf3-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="a9bf3-133">`--direction Inbound`: Направление соединения hello (входящий или исходящий).</span><span class="sxs-lookup"><span data-stu-id="a9bf3-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="a9bf3-134">`--priority 100`: Приоритет для правила hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="a9bf3-135">`--source-address-prefix Internet` — префикс адреса источника в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="a9bf3-136">`--source-port-range "*"` — исходный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="a9bf3-137">Порт, который подключился hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="a9bf3-138">`--destination-address-prefix "*"` — префикс адреса назначения в CIDR или использование тегов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="a9bf3-139">`--destination-port-range 3389` — конечный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="a9bf3-140">Порт, который получает запрос на подключение hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="a9bf3-141">Создать правило, разрешающее доступ tooport 80 (HTTP) из Интернета hello **создать правило nsg сети az** команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="a9bf3-142">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="a9bf3-143">Привязать hello NSG toohello **переднего плана** подсети с hello [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update) команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="a9bf3-144">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="a9bf3-145">Создать hello NSG для hello `BackEnd` подсети</span><span class="sxs-lookup"><span data-stu-id="a9bf3-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="a9bf3-146">toocreate NSG с именем *NSG серверной* в зависимости от предыдущего сценария hello, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="a9bf3-147">Создать hello `NSG-BackEnd` NSG с **создать az сети nsg**.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="a9bf3-148">Как на шаге 2 выше hello тесты на ожидаемые выходные данные довольно велик, включая правила по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="a9bf3-149">Создать правило, разрешающее доступ tooport 1433 (SQL) из hello `FrontEnd` подсети с hello **создать правило nsg сети az** команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="a9bf3-150">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="a9bf3-151">Создать правило, запрещающее доступ toohello в Интернет с помощью hello **создать правило nsg сети az** команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="a9bf3-152">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="a9bf3-153">Привязать hello NSG toohello `BackEnd` подсеть, используя hello **набор подсети виртуальной сети сети az** команды.</span><span class="sxs-lookup"><span data-stu-id="a9bf3-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="a9bf3-154">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a9bf3-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
