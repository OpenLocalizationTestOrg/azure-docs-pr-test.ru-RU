---
title: "Настройка балансировщика нагрузки для SQL AlwaysOn | Документация Майкрософт"
description: "Информация о настройке подсистемы балансировки нагрузки для работы с AlwaysOn SQL и использовании Powershell для создания подсистемы балансировки нагрузки для реализации SQL"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="c20eb-103">Настройка подсистемы балансировки нагрузки для AlwaysOn SQL</span><span class="sxs-lookup"><span data-stu-id="c20eb-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="c20eb-104">Группы доступности AlwaysOn SQL Server теперь можно использовать совместно с внутренней подсистемой балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="c20eb-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="c20eb-105">Группа доступности — это флагманское решение SQL Server, обеспечивающее высокий уровень доступности и аварийное восстановление.</span><span class="sxs-lookup"><span data-stu-id="c20eb-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="c20eb-106">Прослушиватель групп доступности позволяет клиентским приложениям с легкостью подключаться к первичной реплике, независимо от числа реплик в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c20eb-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="c20eb-107">Имя прослушивателя (DNS) сопоставляется с IP-адресом с балансировкой нагрузки, и балансировщик нагрузки Azure направляет входящий трафик только на сервер-источник в наборе реплик.</span><span class="sxs-lookup"><span data-stu-id="c20eb-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="c20eb-108">Поддержку внутренней подсистемы балансировки нагрузки можно использовать для конечных точек (прослушивателя) AlwaysOn SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c20eb-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="c20eb-109">Теперь вы можете контролировать доступность прослушивателя и выбирать IP-адрес с балансировкой нагрузки конкретной подсети в вашей виртуальной сети (VNet).</span><span class="sxs-lookup"><span data-stu-id="c20eb-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="c20eb-110">При использовании внутренней подсистемы балансировки нагрузки для прослушивателя к конечной точке сервера SQL Server (например, Server=tcp:ListenerName,1433;Database=DatabaseName) могут получать доступ только:</span><span class="sxs-lookup"><span data-stu-id="c20eb-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="c20eb-111">Службы и виртуальные машины в одной виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c20eb-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="c20eb-112">Службы и виртуальные машины из подключенной локальной сети</span><span class="sxs-lookup"><span data-stu-id="c20eb-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="c20eb-113">Службы и виртуальные машины из взаимосвязанных виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="c20eb-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="c20eb-115">Рис. 1. Группа SQL AlwaysOn, в которой настроена подсистема балансировки нагрузки с выходом в Интернет</span><span class="sxs-lookup"><span data-stu-id="c20eb-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="c20eb-116">Добавление внутренней подсистемы балансировки нагрузки в службу</span><span class="sxs-lookup"><span data-stu-id="c20eb-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="c20eb-117">В следующем примере мы настроим виртуальную сеть, содержащую подсеть с именем Subnet-1.</span><span class="sxs-lookup"><span data-stu-id="c20eb-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="c20eb-118">Добавление конечных точек с балансировкой нагрузки для внутренней подсистемы балансировки нагрузки на каждой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c20eb-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="c20eb-119">В приведенном выше примере две виртуальные машины с именами sqlsvc1 и sqlsvc2 работают в облачной службе Sqlsvc.</span><span class="sxs-lookup"><span data-stu-id="c20eb-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="c20eb-120">Создав внутренний балансировщик нагрузки с параметром `DirectServerReturn`, вы добавите в него конечные точки с балансировкой нагрузки, чтобы разрешить SQL настраивать прослушиватели для групп доступности.</span><span class="sxs-lookup"><span data-stu-id="c20eb-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="c20eb-121">Подробные указания см. в статье [Настройка внутреннего балансировщика нагрузки для группы доступности AlwaysOn в Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="c20eb-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c20eb-122">См. также</span><span class="sxs-lookup"><span data-stu-id="c20eb-122">See Also</span></span>
[<span data-ttu-id="c20eb-123">Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="c20eb-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="c20eb-124">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="c20eb-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c20eb-125">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="c20eb-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c20eb-126">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="c20eb-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
