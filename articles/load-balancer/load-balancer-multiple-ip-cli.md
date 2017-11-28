---
title: "aaaLoad балансировки на несколько IP-конфигурации с помощью Azure CLI | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальной машины с помощью Azure CLI | Диспетчер ресурсов."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="ac5b1-103">Балансировка нагрузки в конфигурациях с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="ac5b1-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac5b1-104">Портал</span><span class="sxs-lookup"><span data-stu-id="ac5b1-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="ac5b1-105">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="ac5b1-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="ac5b1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac5b1-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="ac5b1-107">В этой статье описывается, как toouse подсистемы балансировки нагрузки Azure с несколькими IP-адресов для дополнительного сетевого интерфейса (NIC).</span><span class="sxs-lookup"><span data-stu-id="ac5b1-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="ac5b1-108">В этом сценарии у нас есть две виртуальные машины под управлением Windows, оснащенные основной и дополнительной сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="ac5b1-109">Каждый дополнительный hello сетевые адаптеры имеют два IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="ac5b1-110">На каждой виртуальной машине размещены веб-сайты contoso.com и fabrikam.com. Каждый веб-сайт имеет связанный tooone hello IP-конфигурации сетевого адаптера hello получателей.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="ac5b1-111">Мы используем подсистемы балансировки нагрузки Azure tooexpose два интерфейсных IP-адреса, один для каждого веб-сайта, toodistribute трафик toohello соответствующие IP-конфигурацию для веб-сайта hello.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="ac5b1-112">Этот сценарий использует hello одинаковый номер порта на серверах переднего плана, как, так и обоих внутренний пул IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Схема балансировки нагрузки для сценария](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="ac5b1-114">Баланс tooload действия на нескольких IP-конфигурации</span><span class="sxs-lookup"><span data-stu-id="ac5b1-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="ac5b1-115">Выполните действия hello ниже tooachieve hello сценарий, описанный в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="ac5b1-116">[Установка и настройка hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI, выполнив указанные ниже действия hello в связанной статье hello и войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="ac5b1-117">[Создайте группу ресурсов](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) *contosofabrikam*, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="ac5b1-118">[Создать группу доступности](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello две виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="ac5b1-119">В этом случае используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ac5b1-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="ac5b1-120">[Создайте виртуальную сеть](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) *myVNet* и подсеть *mySubnet*.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="ac5b1-121">[Создание балансировки нагрузки hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) вызывается *mylb*:</span><span class="sxs-lookup"><span data-stu-id="ac5b1-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="ac5b1-122">Создайте два динамических общедоступных IP-адресов для IP-конфигурации переднего плана hello балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="ac5b1-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="ac5b1-123">Создание IP-конфигурации переднего плана hello двух *contosofe* и *fabrikamfe* соответственно:</span><span class="sxs-lookup"><span data-stu-id="ac5b1-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="ac5b1-124">Создайте внутренние пулы адресов, *contosopool* и *fabrikampool*, [пробу](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json)  - *HTTP* и правила балансировки нагрузки, *HTTPc* и *HTTPf*.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="ac5b1-125">Выполнения hello следующую ниже команду и проверьте выходные данные hello слишком[проверьте балансировки нагрузки](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) создана правильно:</span><span class="sxs-lookup"><span data-stu-id="ac5b1-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="ac5b1-126">[Создайте общедоступный IP-адрес](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address) *myPublicIp* и [учетную запись хранения](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) *mystorageaccont1* для первой виртуальной машины VM1, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="ac5b1-127">[Создать hello сетевых интерфейсов](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) для VM1 и добавьте второй IP-конфигурация *VM1 ipconfig2*, и [создать hello ВМ](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ac5b1-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="ac5b1-128">Повторите шаги 10–11 для второй виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="ac5b1-129">Наконец необходимо настроить DNS ресурса записи toopoint toohello соответствующих интерфейсный IP-адрес hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="ac5b1-130">Домены можно разместить в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ac5b1-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="ac5b1-131">Дополнительные сведения об использовании Azure DNS с подсистемой балансировки нагрузки см. в разделе [Использование Azure DNS с другими службами Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="ac5b1-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac5b1-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac5b1-132">Next steps</span></span>
- <span data-ttu-id="ac5b1-133">Дополнительные сведения о как Балансировка нагрузки toocombine службами в Azure в [с помощью службы балансировки нагрузки в Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ac5b1-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="ac5b1-134">Узнайте, как использовать различные типы журналов в Azure toomanage и устранение неполадок подсистемы балансировки нагрузки в [аналитика журналов для балансировки нагрузки Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="ac5b1-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
