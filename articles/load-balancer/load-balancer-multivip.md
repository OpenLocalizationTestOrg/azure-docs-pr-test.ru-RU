---
title: "Несколько виртуальных IP-адресов для облачной службы"
description: "Обзор данных об использовании нескольких виртуальных IP-адресов и установке нескольких виртуальных IP-адресов для облачной службы"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="aad39-103">Настройка нескольких виртуальных IP-адресов для облачной службы</span><span class="sxs-lookup"><span data-stu-id="aad39-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="aad39-104">Доступ к облачным службам Azure через общедоступное подключение к Интернету можно получить с помощью IP-адреса, предоставляемого Azure.</span><span class="sxs-lookup"><span data-stu-id="aad39-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="aad39-105">Этот общедоступный IP-адрес называется виртуальным IP-адресом, так как он привязан к подсистеме балансировки нагрузки Azure, а не к экземплярам виртуальной машины в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="aad39-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="aad39-106">Доступ к любому экземпляру виртуальной машины в облачной службе можно получить с помощью одного виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="aad39-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="aad39-107">Однако существуют случаи, в которых может потребоваться несколько виртуальных IP-адресов в качестве точки входа для одной и той же облачной службы.</span><span class="sxs-lookup"><span data-stu-id="aad39-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="aad39-108">Например, в вашей облачной службе может размещаться несколько веб-сайтов, которые требуют подключения по протоколу SSL с помощью порта 443 по умолчанию, так как каждый из веб-сайтов должен быть размещен для отдельного пользователя или клиента.</span><span class="sxs-lookup"><span data-stu-id="aad39-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="aad39-109">В этом случае необходим отдельный общедоступный IP-адрес для каждого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="aad39-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="aad39-110">На схеме ниже показан типичный мультитенантный веб-хостинг, требующий несколько сертификатов SSL для одного и того же общедоступного порта.</span><span class="sxs-lookup"><span data-stu-id="aad39-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Сценарий SSL с несколькими виртуальными IP-адресами](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="aad39-112">В приведенном выше примере все виртуальные IP-адреса используют один и тот же общедоступный порт (443), а трафик перенаправляется на одну или несколько виртуальных машин с балансировкой нагрузки по уникальному частному порту для внутреннего IP-адреса облачной службы, в которой размещены все веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="aad39-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="aad39-113">Другой вариант использования нескольких виртуальных IP-адресов заключается в размещении нескольких прослушивателей группы доступности SQL AlwaysOn в одном и том же наборе виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="aad39-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="aad39-114">Виртуальные IP-адреса динамичны по умолчанию. Это означает, что фактический IP-адрес, назначенный облачной службе, может со временем измениться.</span><span class="sxs-lookup"><span data-stu-id="aad39-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="aad39-115">Чтобы избежать этого, можно зарезервировать виртуальный IP-адрес для службы.</span><span class="sxs-lookup"><span data-stu-id="aad39-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="aad39-116">Дополнительную информацию о зарезервированных виртуальных IP-адресах см. в статье [Обзор зарезервированных IP-адресов](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="aad39-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aad39-117">Информацию о ценах на виртуальные IP-адреса и зарезервированные IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="aad39-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="aad39-118">Вы можете использовать PowerShell для проверки виртуальных IP-адресов, используемых облачной службой, а также добавления и удаления виртуальных IP-адресов, привязки виртуального IP-адреса к конечной точке и настройки балансировки нагрузки для конкретного виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="aad39-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="aad39-119">Ограничения</span><span class="sxs-lookup"><span data-stu-id="aad39-119">Limitations</span></span>

<span data-ttu-id="aad39-120">В настоящее время функциональность нескольких виртуальных IP-адресов ограничена следующими сценариями.</span><span class="sxs-lookup"><span data-stu-id="aad39-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="aad39-121">**Только IaaS**.</span><span class="sxs-lookup"><span data-stu-id="aad39-121">**IaaS only**.</span></span> <span data-ttu-id="aad39-122">Вы можете включить несколько виртуальных IP-адресов для облачных служб, содержащих виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="aad39-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="aad39-123">Нельзя использовать несколько виртуальных IP-адресов в сценариях PaaS с экземплярами ролей.</span><span class="sxs-lookup"><span data-stu-id="aad39-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="aad39-124">**Только PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="aad39-124">**PowerShell only**.</span></span> <span data-ttu-id="aad39-125">Несколькими виртуальными IP-адресами можно управлять только с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aad39-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="aad39-126">Эти ограничения являются временными и могут измениться в любое время.</span><span class="sxs-lookup"><span data-stu-id="aad39-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="aad39-127">Обязательно вернитесь на эту страницу, чтобы проверить будущие изменения.</span><span class="sxs-lookup"><span data-stu-id="aad39-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="aad39-128">Как добавить виртуальный IP-адрес в облачную службу</span><span class="sxs-lookup"><span data-stu-id="aad39-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="aad39-129">Чтобы добавить виртуальный IP-адрес в службу, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aad39-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="aad39-130">Эта команда отображает примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="aad39-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="aad39-131">Как удалить виртуальный IP-адрес из облачной службы</span><span class="sxs-lookup"><span data-stu-id="aad39-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="aad39-132">Чтобы удалить виртуальный IP-адрес, добавленный в службу в примере выше, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aad39-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="aad39-133">Виртуальный IP-адрес можно удалить только в том случае, если с ним не связаны конечные точки.</span><span class="sxs-lookup"><span data-stu-id="aad39-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="aad39-134">Как получить данные о виртуальном IP-адресе из облачной службы</span><span class="sxs-lookup"><span data-stu-id="aad39-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="aad39-135">Чтобы получить виртуальный IP-адрес, связанный с облачной службой, выполните следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aad39-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="aad39-136">Сценарий отображает примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="aad39-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="aad39-137">В этом примере облачная служба имеет 3 виртуальных IP-адреса:</span><span class="sxs-lookup"><span data-stu-id="aad39-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="aad39-138">**Vip1** — виртуальный IP-адрес по умолчанию, так как для параметра IsDnsProgrammedName задано значение true;</span><span class="sxs-lookup"><span data-stu-id="aad39-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="aad39-139">**Vip2** и **Vip3** не используются, так как они не имеют IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="aad39-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="aad39-140">Они будут использоваться, только если связать конечную точку с виртуальным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="aad39-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="aad39-141">За использование дополнительных виртуальных IP-адресов в подписке начнет взиматься плата, когда они будут связаны с конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="aad39-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="aad39-142">Дополнительную информацию о ценах см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="aad39-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="aad39-143">Как привязать виртуальный IP-адрес к конечной точке</span><span class="sxs-lookup"><span data-stu-id="aad39-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="aad39-144">Чтобы связать виртуальный IP-адрес в облачной службе с конечной точкой, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aad39-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="aad39-145">Эта команда создает конечную точку, связанную с виртуальным IP-адресом, с именем *Vip2* на порте *80* и связывает ее с виртуальной машиной с именем *myVM1* в облачной службе с именем *myService* с помощью *TCP* на порте *8080*.</span><span class="sxs-lookup"><span data-stu-id="aad39-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="aad39-146">Чтобы проверить конфигурацию, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aad39-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="aad39-147">Результат должен быть аналогичным приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="aad39-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="aad39-148">Как включить балансировку нагрузки в конкретном виртуальном IP-адресе</span><span class="sxs-lookup"><span data-stu-id="aad39-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="aad39-149">Вы можете связать один виртуальный IP-адрес с несколькими виртуальными машинами для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="aad39-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="aad39-150">Например, у вас есть облачная служба с именем *myService* и две виртуальные машины с именами *myVM1* и *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="aad39-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="aad39-151">Облачная служба имеет несколько виртуальных IP-адресов, имя одного из которых — *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="aad39-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="aad39-152">Если вы хотите убедиться, что весь трафик порта *81* по адресу *Vip2* распределяется между *myVM1* и *myVM2* на порте *8181*, выполните следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aad39-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="aad39-153">Вы можете также обновить подсистему балансировки нагрузки, чтобы использовать другой виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="aad39-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="aad39-154">Например, если выполнить следующую команду PowerShell, набор балансировки нагрузки станет использовать виртуальный IP-адрес с именем Vip1:</span><span class="sxs-lookup"><span data-stu-id="aad39-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="aad39-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aad39-155">Next Steps</span></span>

[<span data-ttu-id="aad39-156">Служба анализа журналов для балансировщика нагрузки Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="aad39-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="aad39-157">Обзор подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="aad39-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="aad39-158">Приступая к работе с подсистемой балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="aad39-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="aad39-159">Обзор виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="aad39-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="aad39-160">API REST зарезервированных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="aad39-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
