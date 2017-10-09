---
title: "aaaConfigure балансировки нагрузки для SQL всегда on | Документы Microsoft"
description: "Настроить toowork подсистемы балансировки нагрузки с помощью SQL всегда на и как tooleverage powershell toocreate Подсистема балансировки нагрузки для реализации SQL hello"
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
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="e4153-103">Настройка подсистемы балансировки нагрузки для AlwaysOn SQL</span><span class="sxs-lookup"><span data-stu-id="e4153-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="e4153-104">Группы доступности AlwaysOn SQL Server теперь можно использовать совместно с внутренней подсистемой балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e4153-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="e4153-105">Группа доступности — это флагманское решение SQL Server, обеспечивающее высокий уровень доступности и аварийное восстановление.</span><span class="sxs-lookup"><span data-stu-id="e4153-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="e4153-106">Hello прослушивателя группы доступности позволяет клиентским приложениям tooseamlessly подключения toohello первичной реплике, независимо от hello число реплик hello в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="e4153-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="e4153-107">Hello имя прослушивателя (DNS) — IP-адрес сопоставленных tooa балансировки нагрузки и балансировку нагрузки Azure направляет hello входящего трафика tooonly hello сервера-источника в наборе реплик hello.</span><span class="sxs-lookup"><span data-stu-id="e4153-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="e4153-108">Поддержку внутренней подсистемы балансировки нагрузки можно использовать для конечных точек (прослушивателя) AlwaysOn SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e4153-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="e4153-109">Теперь могут контролировать доступность hello hello прослушивателя и выберите hello балансировкой нагрузки IP-адрес из определенной подсети в виртуальной сети (VNet).</span><span class="sxs-lookup"><span data-stu-id="e4153-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="e4153-110">Используя ILB hello прослушивателя, hello конечной точки SQL server (например, Server = tcp:ListenerName, 1433, базы данных = имя базы данных), доступен только для:</span><span class="sxs-lookup"><span data-stu-id="e4153-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="e4153-111">Службы и виртуальные машины в hello одной виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="e4153-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="e4153-112">Службы и виртуальные машины из подключенной локальной сети</span><span class="sxs-lookup"><span data-stu-id="e4153-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="e4153-113">Службы и виртуальные машины из взаимосвязанных виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="e4153-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="e4153-115">Рис. 1. Группа SQL AlwaysOn, в которой настроена подсистема балансировки нагрузки с выходом в Интернет</span><span class="sxs-lookup"><span data-stu-id="e4153-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="e4153-116">Добавление службы toohello внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e4153-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="e4153-117">На следующий пример hello мы Настройка виртуальной сети, содержащей подсеть с именем «подсеть-1".</span><span class="sxs-lookup"><span data-stu-id="e4153-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="e4153-118">Добавление конечных точек с балансировкой нагрузки для внутренней подсистемы балансировки нагрузки на каждой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="e4153-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="e4153-119">В приведенном выше примере hello, у вас есть 2 ВМ вызываемой «sqlsvc1» и «sqlsvc2» работает в облаке hello службы «Sqlsvc».</span><span class="sxs-lookup"><span data-stu-id="e4153-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="e4153-120">После создания hello ILB с `DirectServerReturn` переключения, можно добавить конечные точки с балансировкой toohello ILB tooallow SQL tooconfigure hello прослушиватели группы доступности hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="e4153-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="e4153-121">Подробные указания см. в статье [Настройка внутреннего балансировщика нагрузки для группы доступности AlwaysOn в Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="e4153-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e4153-122">См. также</span><span class="sxs-lookup"><span data-stu-id="e4153-122">See Also</span></span>
[<span data-ttu-id="e4153-123">Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="e4153-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="e4153-124">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e4153-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="e4153-125">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e4153-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="e4153-126">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e4153-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
