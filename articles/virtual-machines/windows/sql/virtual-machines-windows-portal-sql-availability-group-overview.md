---
title: "Обзор групп доступности SQL Server и виртуальных машин Azure | Документация Майкрософт"
description: "В этой статье рассматриваются группы доступности SQL Server на виртуальных машинах Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="fc409-103">Введение в группы доступности AlwaysOn SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="fc409-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="fc409-104">В этой статье рассматриваются группы доступности SQL Server на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="fc409-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="fc409-105">Группы доступности AlwaysOn на виртуальных машинах Azure аналогичны группам доступности AlwaysOn в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="fc409-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="fc409-106">Дополнительные сведения см. в разделе [Группы доступности AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc409-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="fc409-107">На схеме показаны компоненты полной группы доступности SQL Server на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="fc409-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="fc409-109">Основное отличие группы доступности на виртуальных машинах Azure состоит в том, что для виртуальных машин Azure требуется [подсистема балансировки нагрузки](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc409-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="fc409-110">Подсистема балансировки нагрузки хранит IP-адреса для прослушивателя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="fc409-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="fc409-111">Если используется несколько групп доступности, то каждой из них требуется прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="fc409-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="fc409-112">Одна подсистема балансировки нагрузки может обслуживать несколько прослушивателей.</span><span class="sxs-lookup"><span data-stu-id="fc409-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="fc409-113">Когда все будет готово к созданию группы доступности SQL Server на виртуальных машинах Azure, обратитесь к этим руководствам.</span><span class="sxs-lookup"><span data-stu-id="fc409-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="fc409-114">Автоматическое создание группы доступности из шаблона</span><span class="sxs-lookup"><span data-stu-id="fc409-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="fc409-115">Автоматическая настройка группы доступности AlwaysOn на виртуальной машине Azure в модели Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc409-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="fc409-116">Создание группы доступности на портале Azure вручную</span><span class="sxs-lookup"><span data-stu-id="fc409-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="fc409-117">Имеется возможность создать виртуальные машины самостоятельно, без шаблона.</span><span class="sxs-lookup"><span data-stu-id="fc409-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="fc409-118">Сначала выполните необходимые условия, после чего создайте группу доступности.</span><span class="sxs-lookup"><span data-stu-id="fc409-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="fc409-119">Ознакомьтесь со следующими разделами.</span><span class="sxs-lookup"><span data-stu-id="fc409-119">See the following topics:</span></span> 

- [<span data-ttu-id="fc409-120">Настройка необходимых компонентов для создания групп доступности AlwaysOn в виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="fc409-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="fc409-121">Создание группы доступности AlwaysOn для улучшения доступности и аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="fc409-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="fc409-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc409-122">Next steps</span></span>

<span data-ttu-id="fc409-123">[Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="fc409-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
