---
title: "aaaConfigure частных IP-адресов для виртуальных машин - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин с помощью hello Azure командной строки (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="e06aa-103">Настройка частного IP-адреса для виртуальной машины с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="e06aa-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e06aa-104">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="e06aa-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="e06aa-105">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="e06aa-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="e06aa-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления</span><span class="sxs-lookup"><span data-stu-id="e06aa-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="e06aa-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="e06aa-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="e06aa-108">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e06aa-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="e06aa-109">Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e06aa-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="e06aa-110">приведенную ниже команду CLI Azure 2.0 Образец Hello ожидать простой среде уже создан.</span><span class="sxs-lookup"><span data-stu-id="e06aa-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="e06aa-111">Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e06aa-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="e06aa-112">Указание статического частного IP-адреса при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e06aa-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="e06aa-113">toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="e06aa-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="e06aa-114">Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e06aa-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="e06aa-115">Создать общедоступный IP-адрес для hello виртуальной Машины с hello [создать az сетевого public-IP-адреса](/cli/azure/network/public-ip#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e06aa-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="e06aa-116">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="e06aa-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e06aa-117">Возможно или toouse различные значения для аргументов, в этом и последующих шагов в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="e06aa-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="e06aa-118">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e06aa-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="e06aa-119">`--resource-group`: Имя группы ресурсов hello в какие toocreate hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e06aa-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="e06aa-120">`--name`: Имя hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e06aa-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="e06aa-121">`--location`: Azure область какие toocreate hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e06aa-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="e06aa-122">Запустите hello [сетевого адаптера сети az создать](/cli/azure/network/nic#create) команда toocreate сетевой Адаптер с статический частных IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e06aa-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="e06aa-123">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="e06aa-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="e06aa-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e06aa-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="e06aa-125">Параметры</span><span class="sxs-lookup"><span data-stu-id="e06aa-125">Parameters:</span></span>

    * <span data-ttu-id="e06aa-126">`--private-ip-address`: Статический частный IP-адрес для hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="e06aa-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="e06aa-127">`--vnet-name`: Имя hello виртуальной сети, в которой toocreate hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="e06aa-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="e06aa-128">`--subnet`: Имя hello подсети, в которой toocreate hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="e06aa-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="e06aa-129">Запустите hello [создания виртуальной машины azure](/cli/azure/vm/nic#create) команда toocreate hello созданную виртуальную Машину с помощью hello общедоступного IP-адреса и сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="e06aa-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="e06aa-130">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="e06aa-130">hello list shown after hello output explains hello parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="e06aa-131">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e06aa-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="e06aa-132">Параметры, кроме hello basic [создания виртуальной машины az](/cli/azure/vm#create) параметров.</span><span class="sxs-lookup"><span data-stu-id="e06aa-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="e06aa-133">`--nics`: Имя hello toowhich hello сетевого Адаптера виртуальной Машины она будет присоединена.</span><span class="sxs-lookup"><span data-stu-id="e06aa-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="e06aa-134">Получение сведений о статическом частном IP-адресе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e06aa-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="e06aa-135">tooview hello статический частный IP-адрес, созданный, запустите следующую команду Azure CLI hello и просмотрите значения hello *метод alloc частный IP-адрес* и *частный IP-адрес*:</span><span class="sxs-lookup"><span data-stu-id="e06aa-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="e06aa-136">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e06aa-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="e06aa-137">toodisplay специально hello IP подробности hello сетевой Адаптер для этой виртуальной Машины, запрос hello сетевого Адаптера:</span><span class="sxs-lookup"><span data-stu-id="e06aa-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="e06aa-138">выходные данные Hello выглядят примерно так:</span><span class="sxs-lookup"><span data-stu-id="e06aa-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="e06aa-139">Удаление статического частного IP-адреса виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e06aa-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="e06aa-140">Статический частный IP-адрес нельзя удалить из сетевой карты с использованием Azure CLI для развертываний Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e06aa-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="e06aa-141">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="e06aa-141">You must:</span></span>
- <span data-ttu-id="e06aa-142">Создайте сетевую карту, использующую динамический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e06aa-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="e06aa-143">Задать hello сетевого Адаптера виртуальной Машины hello hello вновь созданные сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="e06aa-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="e06aa-144">hello toochange сетевого Адаптера для hello виртуальной Машины, используемой в командах hello выше, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="e06aa-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="e06aa-145">Запустите hello **сетевого адаптера сети azure создать** команды toocreate новый сетевой Адаптер, с помощью динамического выделения IP-адресов с помощью нового IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e06aa-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="e06aa-146">Обратите внимание, что поскольку IP-адрес не указан, способ распределения hello **динамическое**.</span><span class="sxs-lookup"><span data-stu-id="e06aa-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="e06aa-147">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e06aa-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="e06aa-148">Запустите hello **набор виртуальных машин azure** команда toochange hello сетевой Адаптер, используемый hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e06aa-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="e06aa-149">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e06aa-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="e06aa-150">Если hello виртуальной Машины достаточно большой toohave более одного сетевого Адаптера, запустите hello **удалить сетевого адаптера сети azure** команды toodelete, старый hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="e06aa-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="e06aa-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e06aa-151">Next steps</span></span>
* <span data-ttu-id="e06aa-152">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="e06aa-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="e06aa-153">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="e06aa-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="e06aa-154">Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="e06aa-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

