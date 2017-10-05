---
title: "Балансировка нагрузки в конфигурациях с несколькими IP-адресами с помощью интерфейса командной строки Azure | Документация Майкрософт"
description: "Узнайте, как назначить виртуальной машине несколько IP-адресов с использованием интерфейса командной строки Azure."
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
ms.openlocfilehash: bd15713752ea01ad403d8e3dcfed0c9a7adcc7fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="555a9-103">Балансировка нагрузки в конфигурациях с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="555a9-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="555a9-104">Портал</span><span class="sxs-lookup"><span data-stu-id="555a9-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="555a9-105">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="555a9-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="555a9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="555a9-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="555a9-107">В этой статье описывается, как использовать Azure Load Balancer в конфигурации, когда каждому дополнительному сетевому интерфейсу (сетевой карты) назначено несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="555a9-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="555a9-108">В этом сценарии у нас есть две виртуальные машины под управлением Windows, оснащенные основной и дополнительной сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="555a9-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="555a9-109">У каждой из дополнительных сетевых карт есть по две IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="555a9-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="555a9-110">На каждой виртуальной машине размещены веб-сайты contoso.com и fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="555a9-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="555a9-111">Каждый веб-сайт привязан к одной из IP-конфигураций дополнительной сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="555a9-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="555a9-112">Мы используем Azure Load Balancer, чтобы предоставить два интерфейсных IP-адреса, по одному для каждого веб-сайта. Это позволит направлять трафик в соответствующую IP-конфигурацию для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="555a9-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="555a9-113">В данном сценарии используется одинаковый номер порта для обоих внешних интерфейсов, как и для обоих IP-адресов внутренних пулов.</span><span class="sxs-lookup"><span data-stu-id="555a9-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Схема балансировки нагрузки для сценария](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="555a9-115">Инструкции по балансировке нагрузки в конфигурациях с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="555a9-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="555a9-116">Выполните следующие действия, чтобы реализовать сценарий, описанный в этой статье.</span><span class="sxs-lookup"><span data-stu-id="555a9-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="555a9-117">[Установите и настройте интерфейс командной строки Azure](../cli-install-nodejs.md), следуя инструкциям в соответствующей статье, а затем войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="555a9-117">[Install and Configure the Azure CLI](../cli-install-nodejs.md) the Azure CLI by following the steps in the linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="555a9-118">[Создайте группу ресурсов](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) *contosofabrikam*, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="555a9-118">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="555a9-119">[Создайте группу доступности](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) для двух виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="555a9-119">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) to for the two VMs.</span></span> <span data-ttu-id="555a9-120">В рамках данного сценария воспользуйтесь следующей командой.</span><span class="sxs-lookup"><span data-stu-id="555a9-120">For this scenario, use the following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="555a9-121">[Создайте виртуальную сеть](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) *myVNet* и подсеть *mySubnet*.</span><span class="sxs-lookup"><span data-stu-id="555a9-121">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="555a9-122">[Создайте подсистему балансировки нагрузки](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) *mylb*.</span><span class="sxs-lookup"><span data-stu-id="555a9-122">[Create the load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="555a9-123">Создайте два динамических общедоступных IP-адреса для интерфейсных IP-конфигураций подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="555a9-123">Create two dynamic public IP addresses for the frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="555a9-124">Создайте две интерфейсные IP-конфигурации, *contosofe* и *fabrikamfe*.</span><span class="sxs-lookup"><span data-stu-id="555a9-124">Create the two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="555a9-125">Создайте внутренние пулы адресов, *contosopool* и *fabrikampool*, [пробу](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json)  - *HTTP* и правила балансировки нагрузки, *HTTPc* и *HTTPf*.</span><span class="sxs-lookup"><span data-stu-id="555a9-125">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="555a9-126">Выполните приведенную ниже команду и проверьте выходные данные, чтобы убедиться, что [подсистема балансировки нагрузки](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) создана правильно.</span><span class="sxs-lookup"><span data-stu-id="555a9-126">Run the following command below and then check the output to [verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="555a9-127">[Создайте общедоступный IP-адрес](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address) *myPublicIp* и [учетную запись хранения](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) *mystorageaccont1* для первой виртуальной машины VM1, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="555a9-127">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="555a9-128">[Создайте сетевой интерфейс](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) для VM1 и добавьте вторую IP-конфигурацию — *VM1-ipconfig2*. Затем [создайте виртуальную машину](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="555a9-128">[Create the network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create the VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="555a9-129">Повторите шаги 10–11 для второй виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="555a9-129">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="555a9-130">Наконец, необходимо настроить записи ресурсов DNS, чтобы они указывали на соответствующие интерфейсные IP-адреса подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="555a9-130">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="555a9-131">Домены можно разместить в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="555a9-131">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="555a9-132">Дополнительные сведения об использовании Azure DNS с подсистемой балансировки нагрузки см. в разделе [Использование Azure DNS с другими службами Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="555a9-132">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="555a9-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="555a9-133">Next steps</span></span>
- <span data-ttu-id="555a9-134">Узнайте больше о том, как объединять службы балансировки нагрузки, в статье [Использование служб балансировки нагрузки в Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="555a9-134">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="555a9-135">Узнайте, как в Azure можно использовать журналы разных типов для управления подсистемой балансировки нагрузки и устранения неполадок в ее работе, ознакомившись со статьей [Служба анализа журналов для балансировщика нагрузки Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="555a9-135">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
