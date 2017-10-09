---
title: "aaaMutiple виртуальные IP-адреса для облачной службы"
description: "Общие сведения о multiVIP и как tooset несколько виртуальных IP-адресов в облачной службе"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="4b27f-103">Настройка нескольких виртуальных IP-адресов для облачной службы</span><span class="sxs-lookup"><span data-stu-id="4b27f-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="4b27f-104">Облачные службы Azure для доступа к hello общедоступный Интернет с помощью IP-адрес, предоставленный службой Azure.</span><span class="sxs-lookup"><span data-stu-id="4b27f-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="4b27f-105">Этот общедоступный IP-адрес является ссылка tooas виртуального IP-адреса (виртуальный IP-адрес), так как он связан toohello Azure подсистемы балансировки нагрузки, а не hello в облачную службу hello экземпляров виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="4b27f-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="4b27f-106">Доступ к любому экземпляру виртуальной машины в облачной службе можно получить с помощью одного виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4b27f-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="4b27f-107">Однако существуют сценарии, в которых может потребоваться более одного виртуального IP-адреса в качестве точки входа toohello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="4b27f-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="4b27f-108">Например облачной службы может содержать несколько веб-сайтов, требующих подключения SSL, с использованием порта 443, по умолчанию hello, как каждый сайт размещается для другого клиента или клиента.</span><span class="sxs-lookup"><span data-stu-id="4b27f-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="4b27f-109">В этом случае необходимо toohave другой открытый IP-адреса для каждого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="4b27f-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="4b27f-110">Hello схеме ниже показан типичный несколькими клиентами размещения веб-сайтов с необходимостью несколько SSL-сертификатов на hello же открытый порт.</span><span class="sxs-lookup"><span data-stu-id="4b27f-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Сценарий SSL с несколькими виртуальными IP-адресами](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="4b27f-112">В примере hello выше, все виртуальные IP-адреса используйте hello же открытый порт (443) и трафик перенаправленный tooone или более нагрузки взаимосвязанных виртуальных машин на уникальный частный порт для hello внутренний IP-адрес облачной службы hello размещение всех hello веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="4b27f-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="4b27f-113">Другой используйте hello требующих hello ситуации несколько виртуальных IP-адресов размещается несколько прослушивателей группы доступности SQL AlwaysOn в hello же набор виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4b27f-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="4b27f-114">Виртуальные IP-адреса являются динамическими по умолчанию, это означает, что со временем может меняться hello фактических IP-адрес toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4b27f-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="4b27f-115">tooprevent, ситуации, вы можете зарезервировать VIP-адрес для службы.</span><span class="sxs-lookup"><span data-stu-id="4b27f-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="4b27f-116">toolearn Дополнительные сведения о зарезервированных виртуальных IP-адресов в разделе [зарезервированный общедоступный IP-адрес](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="4b27f-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4b27f-117">Информацию о ценах на виртуальные IP-адреса и зарезервированные IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="4b27f-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="4b27f-118">Можно использовать PowerShell tooverify hello виртуальные IP-адреса, используемые облачных служб, а также добавить и удалить виртуальные IP-адреса, связать конечную точку tooan виртуального IP-адреса и Настройка балансировки нагрузки в конкретных виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="4b27f-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="4b27f-119">Ограничения</span><span class="sxs-lookup"><span data-stu-id="4b27f-119">Limitations</span></span>

<span data-ttu-id="4b27f-120">В настоящее время функциональные возможности нескольких виртуальных IP-адресов является ограниченной toohello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="4b27f-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="4b27f-121">**Только IaaS**.</span><span class="sxs-lookup"><span data-stu-id="4b27f-121">**IaaS only**.</span></span> <span data-ttu-id="4b27f-122">Вы можете включить несколько виртуальных IP-адресов для облачных служб, содержащих виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="4b27f-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="4b27f-123">Нельзя использовать несколько виртуальных IP-адресов в сценариях PaaS с экземплярами ролей.</span><span class="sxs-lookup"><span data-stu-id="4b27f-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="4b27f-124">**Только PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4b27f-124">**PowerShell only**.</span></span> <span data-ttu-id="4b27f-125">Несколькими виртуальными IP-адресами можно управлять только с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b27f-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="4b27f-126">Эти ограничения являются временными и могут измениться в любое время.</span><span class="sxs-lookup"><span data-stu-id="4b27f-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="4b27f-127">Убедитесь, что toorevisit tooverify будущие изменения этой страницы.</span><span class="sxs-lookup"><span data-stu-id="4b27f-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="4b27f-128">Как tooa tooadd VIP облачной службы</span><span class="sxs-lookup"><span data-stu-id="4b27f-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="4b27f-129">tooyour службе tooadd VIP-адрес, выполните следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="4b27f-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="4b27f-130">Эта команда выводит примерно toohello результат, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="4b27f-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="4b27f-131">Как tooremove VIP-адрес из облачной службы</span><span class="sxs-lookup"><span data-stu-id="4b27f-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="4b27f-132">в примере hello выше выполнения hello следующую команду PowerShell hello tooremove виртуальных IP-адресов добавлены tooyour службы:</span><span class="sxs-lookup"><span data-stu-id="4b27f-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="4b27f-133">VIP-адрес можно удалить только в том случае, если у него есть не tooit конечных точек, связанных.</span><span class="sxs-lookup"><span data-stu-id="4b27f-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="4b27f-134">Каким образом сведения tooretrieve виртуальных IP-адресов из облачной службы</span><span class="sxs-lookup"><span data-stu-id="4b27f-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="4b27f-135">hello tooretrieve виртуальные IP-адреса связанный с облачной службой, запустите следующий сценарий PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="4b27f-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="4b27f-136">сценарий Hello отображает результат аналогичные toohello, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="4b27f-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="4b27f-137">В этом примере hello облачная служба имеет 3 виртуальные IP-адреса:</span><span class="sxs-lookup"><span data-stu-id="4b27f-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="4b27f-138">**Vip1** Здравствуйте виртуальных IP-адресов по умолчанию, вам известно, что поскольку hello для IsDnsProgrammedName значение tootrue.</span><span class="sxs-lookup"><span data-stu-id="4b27f-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="4b27f-139">**Vip2** и **Vip3** не используются, так как они не имеют IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="4b27f-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="4b27f-140">Они будут использоваться только в том случае, если вы связываете конечной точки toohello виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="4b27f-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="4b27f-141">За использование дополнительных виртуальных IP-адресов в подписке начнет взиматься плата, когда они будут связаны с конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="4b27f-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="4b27f-142">Дополнительную информацию о ценах см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="4b27f-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="4b27f-143">Как конечная точка tooan tooassociate VIP-адрес</span><span class="sxs-lookup"><span data-stu-id="4b27f-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="4b27f-144">tooassociate VIP-адрес в облаке tooan конечную точку службы, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="4b27f-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="4b27f-145">Hello команда создает конечная точка с именем виртуальный IP-адрес связанного toohello *Vip2* через порт *80*и связывает его toohello виртуальной Машины с именем *myVM1* в облачной службе с именем  *myService* с помощью *TCP* через порт *8080*.</span><span class="sxs-lookup"><span data-stu-id="4b27f-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="4b27f-146">tooverify конфигурация hello, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="4b27f-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="4b27f-147">Hello выходные данные выглядят аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4b27f-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="4b27f-148">Как tooenable балансировку нагрузки для определенного виртуального IP-адреса</span><span class="sxs-lookup"><span data-stu-id="4b27f-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="4b27f-149">Вы можете связать один виртуальный IP-адрес с несколькими виртуальными машинами для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4b27f-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="4b27f-150">Например, у вас есть облачная служба с именем *myService* и две виртуальные машины с именами *myVM1* и *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="4b27f-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="4b27f-151">Облачная служба имеет несколько виртуальных IP-адресов, имя одного из которых — *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="4b27f-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="4b27f-152">Если требуется, весь трафик tooport tooensure *81* на *Vip2* распределяются между *myVM1* и *myVM2* через порт *8181* , запустите hello следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4b27f-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="4b27f-153">Можно также обновить ваш toouse подсистемы балансировки нагрузки различных виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="4b27f-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="4b27f-154">Например при запуске hello следующую команду PowerShell, мы изменим hello балансировки toouse набора виртуальных IP-адресов, с именем Vip1:</span><span class="sxs-lookup"><span data-stu-id="4b27f-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="4b27f-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4b27f-155">Next Steps</span></span>

[<span data-ttu-id="4b27f-156">Служба анализа журналов для балансировщика нагрузки Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="4b27f-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="4b27f-157">Обзор подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="4b27f-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="4b27f-158">Приступая к работе с подсистемой балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="4b27f-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="4b27f-159">Обзор виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="4b27f-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="4b27f-160">API REST зарезервированных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="4b27f-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
