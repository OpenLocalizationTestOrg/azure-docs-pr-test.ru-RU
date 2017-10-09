---
title: "Общие сведения о группах доступности сервера - виртуальных машинах Azure - aaaSQL | Документы Microsoft"
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
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="cc269-103">Введение в группы доступности AlwaysOn SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="cc269-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="cc269-104">В этой статье рассматриваются группы доступности SQL Server на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="cc269-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="cc269-105">Группы доступности AlwaysOn на виртуальных машинах Azure, аналогичные tooAlways групп доступности на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cc269-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="cc269-106">Дополнительные сведения см. в разделе [Группы доступности AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc269-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="cc269-107">Hello диаграмме показаны компоненты hello завершения доступности группы серверов SQL Server в виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="cc269-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="cc269-109">Hello ключевое различие для группы доступности на виртуальных машинах Azure, hello виртуальных машинах Azure, требуют [подсистемы балансировки нагрузки](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc269-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="cc269-110">Подсистема балансировки нагрузки Hello содержит hello IP-адресов для прослушивателя группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="cc269-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="cc269-111">Если используется несколько групп доступности, то каждой из них требуется прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="cc269-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="cc269-112">Одна подсистема балансировки нагрузки может обслуживать несколько прослушивателей.</span><span class="sxs-lookup"><span data-stu-id="cc269-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="cc269-113">Когда вы будете готовы toobuild aroup доступности SQL Server на виртуальных машинах Azure, см. в toothese учебники.</span><span class="sxs-lookup"><span data-stu-id="cc269-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="cc269-114">Автоматическое создание группы доступности из шаблона</span><span class="sxs-lookup"><span data-stu-id="cc269-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="cc269-115">Автоматическая настройка группы доступности AlwaysOn на виртуальной машине Azure в модели Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc269-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="cc269-116">Создание группы доступности на портале Azure вручную</span><span class="sxs-lookup"><span data-stu-id="cc269-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="cc269-117">Можно также создать виртуальные машины hello самостоятельно без шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="cc269-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="cc269-118">Во-первых выполните hello предварительные требования, а затем создайте группу доступности hello.</span><span class="sxs-lookup"><span data-stu-id="cc269-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="cc269-119">В разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="cc269-119">See hello following topics:</span></span> 

- [<span data-ttu-id="cc269-120">Настройка необходимых компонентов для создания групп доступности AlwaysOn в виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="cc269-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="cc269-121">Создание группы доступности AlwaysOn tooimprove доступности и аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="cc269-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="cc269-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc269-122">Next steps</span></span>

<span data-ttu-id="cc269-123">[Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="cc269-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
