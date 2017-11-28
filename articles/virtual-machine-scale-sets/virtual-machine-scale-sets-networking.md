---
title: "Сеть для масштабируемых наборов виртуальных машин Azure | Документация Майкрософт"
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
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="470b5-103">Сеть для масштабируемых наборов виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="470b5-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="470b5-104">При развертывании масштабируемого набора виртуальных машин Azure с помощью портала определенные свойства сети заданы по умолчанию, например Azure Load Balancer с правилами преобразования сетевых адресов для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="470b5-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="470b5-105">В этой статье описывается, как использовать некоторые расширенные сетевые функции, которые можно настроить с помощью наборов масштабирования.</span><span class="sxs-lookup"><span data-stu-id="470b5-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="470b5-106">Вы можете настроить все функции, описанные в этой статье, с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="470b5-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="470b5-107">Кроме того, будут добавлены примеры Azure CLI и PowerShell для выбранных компонентов.</span><span class="sxs-lookup"><span data-stu-id="470b5-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="470b5-108">Используйте интерфейс командной строки версии 2.10 и PowerShell 4.2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="470b5-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="470b5-109">Ускорение работы в сети</span><span class="sxs-lookup"><span data-stu-id="470b5-109">Accelerated Networking</span></span>
<span data-ttu-id="470b5-110">[Ускорение работы в сети](../virtual-network/virtual-network-create-vm-accelerated-networking.md) Azure повышает производительность сети с помощью использования виртуализации ввода-вывода с единым корнем (SR-IOV) для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="470b5-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="470b5-111">Чтобы использовать ускоренную сеть с масштабируемыми наборами, в настройках networkInterfaceConfigurations масштабируемого набора задайте для параметра enableAcceleratedNetworking значение **true**.</span><span class="sxs-lookup"><span data-stu-id="470b5-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="470b5-112">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="470b5-113">Создание набора масштабирования, который ссылается на существующую службу Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="470b5-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="470b5-114">Если набор масштабирования создается с помощью портала Azure, для большинства параметров конфигурации создается новая подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="470b5-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="470b5-115">Если вы создаете набор масштабирования, которому необходимо ссылаться на существующую подсистему балансировки нагрузки, вы можете создать его с помощью интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="470b5-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="470b5-116">Следующий пример сценария создает подсистему балансировки нагрузки, а затем набор масштабирования, который ссылается на нее:</span><span class="sxs-lookup"><span data-stu-id="470b5-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="470b5-117">Настраиваемые параметры DNS</span><span class="sxs-lookup"><span data-stu-id="470b5-117">Configurable DNS Settings</span></span>
<span data-ttu-id="470b5-118">По умолчанию наборы масштабирования принимают определенные параметры DNS виртуальной сети и подсети, в которых они были созданы.</span><span class="sxs-lookup"><span data-stu-id="470b5-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="470b5-119">Однако вы можете настроить параметры DNS непосредственно для набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="470b5-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="470b5-120">Создание масштабируемого набора с настраиваемыми DNS-серверами</span><span class="sxs-lookup"><span data-stu-id="470b5-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="470b5-121">Чтобы создать масштабируемый набор с настраиваемой конфигурацией DNS с помощью интерфейса командной строки 2.0, добавьте аргумент **--dns-servers** в команду **vmss create**, за которой следуют разделенные пробелами IP-адреса сервера.</span><span class="sxs-lookup"><span data-stu-id="470b5-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="470b5-122">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="470b5-123">Чтобы настроить пользовательские DNS-серверы в шаблоне Azure, добавьте свойство dnsSettings в раздел networkInterfaceConfigurations набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="470b5-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="470b5-124">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="470b5-125">Создание масштабируемого набора с настраиваемыми именами доменов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="470b5-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="470b5-126">Чтобы создать масштабируемый набор с настраиваемым DNS-именем для виртуальных машин с помощью CLI 2.0, добавьте аргумент **--vm-domain-name** в команду **vmss create**, за которой следует строка, представляющая доменное имя.</span><span class="sxs-lookup"><span data-stu-id="470b5-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="470b5-127">Чтобы настроить доменное имя в шаблоне Azure, добавьте свойство **dnsSettings** в раздел масштабируемого набора **networkInterfaceConfigurations**.</span><span class="sxs-lookup"><span data-stu-id="470b5-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="470b5-128">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-128">For example:</span></span>

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

<span data-ttu-id="470b5-129">Выходные данные для DNS-имени отдельной виртуальной машины будут представлены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="470b5-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="470b5-130">Общедоступный IPv4 на каждую виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="470b5-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="470b5-131">Как правило, виртуальным машинам в масштабируемом наборе Azure не требуются собственные общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="470b5-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="470b5-132">Для большинства сценариев наиболее безопасно, а также экономически целесообразно связать общедоступный IP-адрес с подсистемой балансировки нагрузки или отдельной виртуальной машиной (также называемой jumpbox), которая затем (при необходимости) направит входящие подключения на виртуальные машины в масштабируемом наборе (например, через правила преобразования сетевых адресов для входящих подключений).</span><span class="sxs-lookup"><span data-stu-id="470b5-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="470b5-133">Тем не менее, в некоторых сценариях виртуальным машинам в масштабируемом наборе обязательно нужны собственные общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="470b5-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="470b5-134">В качестве примера можно привести игры, в которых консоли необходимо установить прямое подключение к облачной виртуальной машине, выполняющей физическую обработку игр.</span><span class="sxs-lookup"><span data-stu-id="470b5-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="470b5-135">Другим примером можно назвать случай, когда виртуальным машинам необходимо установить внешние подключения между собой в регионах в распределенной базе данных.</span><span class="sxs-lookup"><span data-stu-id="470b5-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="470b5-136">Создание масштабируемого набора с общедоступным IP-адресом на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="470b5-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="470b5-137">Чтобы создать масштабируемый набор, который назначает общедоступный IP-адрес каждой виртуальной машине с помощью CLI 2.0, добавьте параметр **--public-ip-per-vm** в команду **vmss create**.</span><span class="sxs-lookup"><span data-stu-id="470b5-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="470b5-138">Чтобы создать масштабируемый набор с помощью шаблона Azure версии API ресурса Microsoft.Compute/virtualMachineScaleSets должна быть по крайней мере **30-03-2017**. Добавьте свойство JSON **publicIpAddressConfiguration** в раздел ipConfigurations масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="470b5-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="470b5-139">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="470b5-140">Пример шаблона: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="470b5-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="470b5-141">Запрос общедоступных IP-адресов виртуальных машин в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="470b5-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="470b5-142">Чтобы получить список общедоступных IP-адресов, назначенных виртуальным машинам в масштабируемом наборе, с помощью CLI 2.0, используйте команду **az vmss list-instance-public-ips**.</span><span class="sxs-lookup"><span data-stu-id="470b5-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="470b5-143">Используйте команду _Get-AzureRmPublicIpAddress_, чтобы вывести список общедоступных IP-адресов масштабируемого набора, используя PowerShell.</span><span class="sxs-lookup"><span data-stu-id="470b5-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="470b5-144">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="470b5-145">Вы также можете запрашивать общедоступные IP-адреса, напрямую ссылаясь на идентификатор ресурса конфигурации общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="470b5-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="470b5-146">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="470b5-147">Чтобы запросить общедоступные IP-адреса, назначенные виртуальным машинам в масштабируемом наборе, используйте [обозреватель ресурсов Azure](https://resources.azure.com) или Azure REST API версии **30-03-2017** или более поздней.</span><span class="sxs-lookup"><span data-stu-id="470b5-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="470b5-148">Чтобы просмотреть общедоступные IP-адреса для масштабируемого набора с помощью обозревателя ресурсов, ознакомьтесь с разделом **publicipaddresses** в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="470b5-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="470b5-149">Например, https://resources.azure.com/subscriptions/_ИД_подсистемы_/resourceGroups/_ваша_группа_ресурсов_/providers/Microsoft.Compute/virtualMachineScaleSets/_ваша_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="470b5-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="470b5-150">Выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="470b5-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="470b5-151">Несколько IP-адресов на сетевой адаптер</span><span class="sxs-lookup"><span data-stu-id="470b5-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="470b5-152">У каждого сетевого адаптера, подключенного к виртуальной машине в масштабируемом наборе, может быть одна или несколько конфигураций IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="470b5-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="470b5-153">Каждая конфигурация получает один частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="470b5-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="470b5-154">Кроме того, каждой конфигурации также может быть присвоен один ресурс общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="470b5-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="470b5-155">Чтобы узнать, сколько IP-адресов можно назначить сетевому адаптеру, а также сколько общедоступных IP-адресов можно использовать в подписке Azure, ознакомьтесь с [ограничениями Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="470b5-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="470b5-156">Несколько сетевых адаптеров на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="470b5-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="470b5-157">У вам может быть до 8 сетевых адаптеров на виртуальную машину в зависимости от размера машины.</span><span class="sxs-lookup"><span data-stu-id="470b5-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="470b5-158">Узнать о максимальном количестве сетевых адаптеров на машину вы можете в статье [Размеры виртуальных машин Windows в Azure](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="470b5-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="470b5-159">Пример ниже представляет сетевой профиль в масштабируемом наборе, отображающий несколько записей сетевых адаптеров, а также несколько общедоступных IP-адресов на виртуальную машину:</span><span class="sxs-lookup"><span data-stu-id="470b5-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="470b5-160">Группа безопасности сети на масштабируемый набор</span><span class="sxs-lookup"><span data-stu-id="470b5-160">NSG per scale set</span></span>
<span data-ttu-id="470b5-161">Группы безопасности сети можно применить непосредственно к масштабируемому набору, добавив ссылку в раздел конфигурации сетевого интерфейса свойств виртуальной машины в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="470b5-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="470b5-162">Например:</span><span class="sxs-lookup"><span data-stu-id="470b5-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="470b5-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="470b5-163">Next steps</span></span>
<span data-ttu-id="470b5-164">Дополнительные сведения см. в статье [Виртуальная сеть Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="470b5-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
