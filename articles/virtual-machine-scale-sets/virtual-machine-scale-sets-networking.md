---
title: "aaaNetworking для набора масштабирования виртуальной машины Azure | Документы Microsoft"
description: "Конфигурация свойств сети для масштабируемых наборов виртуальных машин Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="c3949-103">Сеть для масштабируемых наборов виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="c3949-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="c3949-104">При развертывании Azure масштабирования виртуальной машины через портал hello задать определенные свойства сети, используемое по умолчанию, например правил NAT для входящего трафика подсистемы балансировки нагрузки Azure с.</span><span class="sxs-lookup"><span data-stu-id="c3949-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="c3949-105">В этой статье описывается, каким образом задает toouse некоторые hello дополнительные сетевые возможности, которые можно настроить с масштабом.</span><span class="sxs-lookup"><span data-stu-id="c3949-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="c3949-106">Можно настроить все функции hello, описанные в этой статье, используя шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c3949-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="c3949-107">Кроме того, будут добавлены примеры Azure CLI и PowerShell для выбранных компонентов.</span><span class="sxs-lookup"><span data-stu-id="c3949-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="c3949-108">Используйте интерфейс командной строки версии 2.10 и PowerShell 4.2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c3949-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="c3949-109">Ускорение работы в сети</span><span class="sxs-lookup"><span data-stu-id="c3949-109">Accelerated Networking</span></span>
<span data-ttu-id="c3949-110">Azure [Accelerated сети](../virtual-network/virtual-network-create-vm-accelerated-networking.md) позволяет повысить производительность сети путем включения SR-iov виртуализацию SR-IOV tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c3949-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="c3949-111">toouse accelerated сетью с помощью набора масштабирования, задайте enableAcceleratedNetworking слишком**true** в параметрах набора масштабирования конфигураций сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c3949-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="c3949-112">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="c3949-113">Создание набора масштабирования, который ссылается на существующую службу Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c3949-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="c3949-114">При создании набора масштабирования с помощью портала Azure hello новую подсистему балансировки загрузки создается для большинства параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c3949-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="c3949-115">При создании набора масштабирования, которая должна tooreference существующей подсистемы балансировки нагрузки, это можно сделать с помощью CLI.</span><span class="sxs-lookup"><span data-stu-id="c3949-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="c3949-116">Следующий пример скрипта Hello создается подсистемы балансировки нагрузки, а затем создается набора масштабирования, который ссылается на нее:</span><span class="sxs-lookup"><span data-stu-id="c3949-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="c3949-117">Настраиваемые параметры DNS</span><span class="sxs-lookup"><span data-stu-id="c3949-117">Configurable DNS Settings</span></span>
<span data-ttu-id="c3949-118">По умолчанию наборы масштабирования отключить на определенные параметры DNS hello hello виртуальной сети и подсети, в котором они были созданы.</span><span class="sxs-lookup"><span data-stu-id="c3949-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="c3949-119">Однако вы можете настроить параметры DNS hello шкалы, задавать напрямую.</span><span class="sxs-lookup"><span data-stu-id="c3949-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="c3949-120">Создание масштабируемого набора с настраиваемыми DNS-серверами</span><span class="sxs-lookup"><span data-stu-id="c3949-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="c3949-121">в наборе с пользовательской конфигурацией DNS с помощью CLI 2.0 toocreate добавить hello **--dns-серверы** toohello аргумент **vmss создания** команды, за которыми следует пробел запятыми IP-адреса сервера.</span><span class="sxs-lookup"><span data-stu-id="c3949-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="c3949-122">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="c3949-123">tooconfigure пользовательские DNS-серверы в шаблоне Azure, добавить шкалу dnsSettings свойства toohello задать раздел конфигураций сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c3949-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="c3949-124">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="c3949-125">Создание масштабируемого набора с настраиваемыми именами доменов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c3949-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="c3949-126">toocreate в наборе с пользовательским именем DNS для виртуальных машин с помощью CLI версии 2.0, добавить hello **виртуальной машины — доменное имя** toohello аргумент **vmss создания** команды, за которым следует строка, представляющая hello доменное имя.</span><span class="sxs-lookup"><span data-stu-id="c3949-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="c3949-127">добавить имя домена tooset hello в шаблон Azure **dnsSettings** набор масштабирования toohello свойство **конфигураций сетевого интерфейса** раздела.</span><span class="sxs-lookup"><span data-stu-id="c3949-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="c3949-128">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="c3949-129">выходные данные Hello, для отдельных виртуальных машин DNS-имя может быть в hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="c3949-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="c3949-130">Общедоступный IPv4 на каждую виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="c3949-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="c3949-131">Как правило, виртуальным машинам в масштабируемом наборе Azure не требуются собственные общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c3949-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="c3949-132">В большинстве случаев это безопасное и экономичное tooassociate открытый IP адрес tooa нагрузки балансировки или tooan отдельных виртуальной машины (также называемого jumpbox), который затем направляет входящие соединения tooscale набор виртуальных машин, при необходимости (например, с помощью Входящие правила NAT).</span><span class="sxs-lookup"><span data-stu-id="c3949-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="c3949-133">Однако в некоторых сценариях требуется набор масштабирования виртуальных машин toohave собственные общедоступный IP-адрес адреса.</span><span class="sxs-lookup"><span data-stu-id="c3949-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="c3949-134">Игры пример, где консоли требуется наличие toomake прямое подключение tooa облака виртуальной машины, которой выполняется обработка игры физических.</span><span class="sxs-lookup"><span data-stu-id="c3949-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="c3949-135">Еще один пример — где виртуальные машины должны tooone внешних соединений toomake другой по регионам в распределенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="c3949-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="c3949-136">Создание масштабируемого набора с общедоступным IP-адресом на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="c3949-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="c3949-137">toocreate набор масштабирования, которая назначает открытый IP адрес tooeach виртуальную машину с CLI 2.0, добавить hello **--public-ip каждой виртуальной машине** toohello параметр **vmss создания** команды.</span><span class="sxs-lookup"><span data-stu-id="c3949-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="c3949-138">toocreate масштабирования, заданные с помощью шаблона Azure, убедитесь, что версия hello API hello Microsoft.Compute/virtualMachineScaleSets ресурсов по крайней мере **2017 г-03-30**и добавьте **publicIpAddressConfiguration**JSON свойство toohello в наборе раздел IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c3949-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="c3949-139">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="c3949-140">Пример шаблона: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="c3949-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="c3949-141">Выполнение запроса hello общедоступный IP-адрес набора адресов hello виртуальных машин на шкале</span><span class="sxs-lookup"><span data-stu-id="c3949-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="c3949-142">общедоступные IP-адреса toolist hello назначенный tooscale набор виртуальных машин с помощью CLI 2.0, используйте hello **az vmss списка экземпляр public-IP-адреса** команды.</span><span class="sxs-lookup"><span data-stu-id="c3949-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="c3949-143">задать масштаб toolist общих IP-адресов с помощью PowerShell, используйте hello _Get AzureRmPublicIpAddress_ команды.</span><span class="sxs-lookup"><span data-stu-id="c3949-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="c3949-144">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="c3949-145">Вы также можете запроса hello общих IP-адресов с помощью ссылки на идентификатор ресурса hello hello открытый IP-адрес конфигурации напрямую.</span><span class="sxs-lookup"><span data-stu-id="c3949-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="c3949-146">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="c3949-147">общедоступные IP-адреса tooquery hello назначенный tooscale набор виртуальных машин с помощью hello [обозревателя ресурсов Azure](https://resources.azure.com), или hello Azure REST API с версией **2017 г-03-30** или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c3949-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="c3949-148">tooview общих IP-адресов для масштабирования, заданные с помощью обозревателя ресурсов hello просмотрите hello **общедоступных** раздел находится в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="c3949-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="c3949-149">Например, https://resources.azure.com/subscriptions/_ИД_подсистемы_/resourceGroups/_ваша_группа_ресурсов_/providers/Microsoft.Compute/virtualMachineScaleSets/_ваша_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="c3949-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="c3949-150">Выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="c3949-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="c3949-151">Несколько IP-адресов на сетевой адаптер</span><span class="sxs-lookup"><span data-stu-id="c3949-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="c3949-152">Каждый сетевой Адаптер подключен tooa виртуальной Машины в наборе масштабирования может иметь один или несколько IP-конфигурации, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="c3949-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="c3949-153">Каждая конфигурация получает один частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c3949-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="c3949-154">Кроме того, каждой конфигурации также может быть присвоен один ресурс общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c3949-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="c3949-155">toounderstand, сколько IP-адреса могут назначаться tooa сетевого Адаптера, и сколько общедоступных IP-адресов, можно использовать в подписку Azure, см. слишком[ограничения Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="c3949-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="c3949-156">Несколько сетевых адаптеров на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="c3949-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="c3949-157">Можно создать до too8 сетевые адаптеры на каждую виртуальную машину, в зависимости от размера машины.</span><span class="sxs-lookup"><span data-stu-id="c3949-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="c3949-158">Hello максимальное количество сетевых адаптеров на один компьютер доступен в hello [статье размер виртуальной Машины](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c3949-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="c3949-159">Hello следующий пример — сетевой профиль, показывающий несколько записей сетевого Адаптера и несколько общих IP-адресов на каждую виртуальную машину в наборе масштабирования:</span><span class="sxs-lookup"><span data-stu-id="c3949-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="c3949-160">Группа безопасности сети на масштабируемый набор</span><span class="sxs-lookup"><span data-stu-id="c3949-160">NSG per scale set</span></span>
<span data-ttu-id="c3949-161">Сетевые группы безопасности можно применить непосредственно tooa набор масштабирования, добавив toohello сетевой интерфейс конфигурации Справочник шкалы hello задать свойства виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c3949-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="c3949-162">Например:</span><span class="sxs-lookup"><span data-stu-id="c3949-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="c3949-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3949-163">Next steps</span></span>
<span data-ttu-id="c3949-164">Дополнительные сведения о виртуальных сетях Azure см. в разделе слишком[этой документации](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3949-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
