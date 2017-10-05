---
title: "Настройка частных IP-адресов для виртуальных машин (Azure CLI 2.0) | Документация Майкрософт"
description: "Узнайте, как настроить частные IP-адреса для виртуальных машин с помощью интерфейса командной строки Azure (CLI) версии 2.0."
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
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="26c42-103">Настройка частных IP-адресов для виртуальной машины с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="26c42-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="26c42-104">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="26c42-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="26c42-105">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="26c42-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="26c42-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26c42-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="26c42-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager (описывается в этой статье).</span><span class="sxs-lookup"><span data-stu-id="26c42-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="26c42-108">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="26c42-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="26c42-109">Кроме того, вы можете [управлять статическим частным IP-адресом в классической модели развертывания](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="26c42-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="26c42-110">Для выполнения приведенных ниже примеров команд Azure CLI 2.0 требуется созданная простая среда.</span><span class="sxs-lookup"><span data-stu-id="26c42-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="26c42-111">Чтобы выполнять команды в соответствии с указаниями, представленными в этом документе, сначала постройте тестовую среду, как описано в статье [Создание виртуальной сети](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="26c42-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="26c42-112">Указание статического частного IP-адреса при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="26c42-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="26c42-113">Чтобы создать виртуальную машину с именем *DNS01* в подсети *FrontEnd* виртуальной сети *TestVNet* со статическим частным IP-адресом *192.168.1.101*, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="26c42-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="26c42-114">Установите и настройте последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) (если вы еще этого не сделали), а затем войдите с использованием учетной записи Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="26c42-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="26c42-115">Создайте общедоступный IP-адрес для виртуальной машины с помощью команды [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="26c42-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="26c42-116">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="26c42-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="26c42-117">Возможно, вам понадобится использовать разные значения для аргументов на этих и последующих шагах в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="26c42-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="26c42-118">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="26c42-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="26c42-119">`--resource-group` — имя группы ресурсов, в которой будет создан общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="26c42-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="26c42-120">`--name` —имя общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="26c42-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="26c42-121">`--location` — регион Azure, в котором будет создан общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="26c42-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="26c42-122">Выполните команду [az network nic create](/cli/azure/network/nic#create), чтобы создать сетевую карту со статическим частным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="26c42-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="26c42-123">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="26c42-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="26c42-124">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="26c42-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="26c42-125">Параметры</span><span class="sxs-lookup"><span data-stu-id="26c42-125">Parameters:</span></span>

    * <span data-ttu-id="26c42-126">`--private-ip-address`: статический частный IP-адрес для сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="26c42-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="26c42-127">`--vnet-name`: имя виртуальной сети для создания сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="26c42-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="26c42-128">`--subnet`: имя подсети для создания сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="26c42-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="26c42-129">Выполните команду [azure vm create](/cli/azure/vm/nic#create) , чтобы создать виртуальную машину с использованием общедоступного IP-адреса и сетевой карты, созданных ранее.</span><span class="sxs-lookup"><span data-stu-id="26c42-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="26c42-130">В списке, который откроется после выполнения команды, будут указаны используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="26c42-130">The list shown after the output explains the parameters used.</span></span>
   
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

    <span data-ttu-id="26c42-131">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="26c42-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="26c42-132">Параметры, отличные от базовых параметров [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="26c42-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="26c42-133">`--nics` — имя сетевой карты, к которой подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="26c42-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="26c42-134">Получение сведений о статическом частном IP-адресе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="26c42-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="26c42-135">Чтобы просмотреть сведения о созданном статическом частном IP-адресе, выполните следующую команду Azure CLI. Обратите внимание на значения *метода выделения частных IP-адресов* и *частного IP-адреса*:</span><span class="sxs-lookup"><span data-stu-id="26c42-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="26c42-136">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="26c42-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="26c42-137">Чтобы отобразить определенные сведения об IP-адресе сетевой карты для этой виртуальной машины, отправьте запрос к сетевой карте:</span><span class="sxs-lookup"><span data-stu-id="26c42-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="26c42-138">Результат будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="26c42-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="26c42-139">Удаление статического частного IP-адреса виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="26c42-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="26c42-140">Статический частный IP-адрес нельзя удалить из сетевой карты с использованием Azure CLI для развертываний Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26c42-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="26c42-141">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="26c42-141">You must:</span></span>
- <span data-ttu-id="26c42-142">Создайте сетевую карту, использующую динамический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="26c42-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="26c42-143">Настройте созданную сетевую карту на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="26c42-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="26c42-144">Чтобы изменить сетевую карту для виртуальной машины, которая использовалась в приведенных выше командах, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="26c42-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="26c42-145">Выполните команду **azure network nic create**, чтобы создать сетевую карту с новым IP-адресом путем выделения динамических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="26c42-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="26c42-146">Обратите внимание, что так как IP-адрес не указан, используется **динамический** способ выделения.</span><span class="sxs-lookup"><span data-stu-id="26c42-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="26c42-147">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="26c42-147">Expected output:</span></span>

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

2. <span data-ttu-id="26c42-148">Выполните команду **azure vm set** , чтобы изменить сетевую карту, используемую виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="26c42-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="26c42-149">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="26c42-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="26c42-150">Если размер виртуальной машины позволяет подключить несколько сетевых карт, выполните команду **azure network nic delete**, чтобы удалить старую сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="26c42-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="26c42-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26c42-151">Next steps</span></span>
* <span data-ttu-id="26c42-152">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="26c42-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="26c42-153">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="26c42-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="26c42-154">Ознакомьтесь с информацией о [REST API зарезервированных IP-адресов](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="26c42-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

