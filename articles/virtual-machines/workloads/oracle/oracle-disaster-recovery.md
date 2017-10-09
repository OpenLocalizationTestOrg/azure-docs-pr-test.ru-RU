---
title: "aaaOverview сценария Oracle аварийного восстановления в среде Azure | Документы Microsoft"
description: "Сценарий аварийного восстановления базы данных Oracle Database 12c в среде Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="171fe-103">Аварийное восстановление базы данных Oracle Database 12c в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="171fe-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="171fe-104">Предположения</span><span class="sxs-lookup"><span data-stu-id="171fe-104">Assumptions</span></span>

- <span data-ttu-id="171fe-105">У вас есть представление о структуре Oracle Data Guard и средах Azure.</span><span class="sxs-lookup"><span data-stu-id="171fe-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="171fe-106">Цели</span><span class="sxs-lookup"><span data-stu-id="171fe-106">Goals</span></span>
- <span data-ttu-id="171fe-107">Проектирование топологии hello и конфигурации, соответствующие требованиям аварийного восстановления (DR).</span><span class="sxs-lookup"><span data-stu-id="171fe-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="171fe-108">Сценарий 1. Основные сайты и сайты аварийного восстановления в Azure</span><span class="sxs-lookup"><span data-stu-id="171fe-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="171fe-109">У клиента есть Oracle базы данных set на первичном сайте hello.</span><span class="sxs-lookup"><span data-stu-id="171fe-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="171fe-110">Сайт аварийного восстановления находится в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="171fe-110">A DR site is in a different region.</span></span> <span data-ttu-id="171fe-111">Hello клиент использует Oracle Data Guard для быстрого восстановления между этими сайтами.</span><span class="sxs-lookup"><span data-stu-id="171fe-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="171fe-112">Первичный сайт Hello оказывает баз данных-получателей для отчетности и других целей.</span><span class="sxs-lookup"><span data-stu-id="171fe-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="171fe-113">Топология</span><span class="sxs-lookup"><span data-stu-id="171fe-113">Topology</span></span>

<span data-ttu-id="171fe-114">Ниже приведена сводка hello Настройка Azure:</span><span class="sxs-lookup"><span data-stu-id="171fe-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="171fe-115">два сайта (первичный сайт и сайт для аварийного восстановления);</span><span class="sxs-lookup"><span data-stu-id="171fe-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="171fe-116">две виртуальные сети;</span><span class="sxs-lookup"><span data-stu-id="171fe-116">Two virtual networks</span></span>
- <span data-ttu-id="171fe-117">две базы данных Oracle с Data Guard (основная и резервная);</span><span class="sxs-lookup"><span data-stu-id="171fe-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="171fe-118">две базы данных Oracle с Golden Gate или Data Guard (только основной сайт);</span><span class="sxs-lookup"><span data-stu-id="171fe-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="171fe-119">Две службы приложения, основной и один на сайте hello аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="171fe-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="171fe-120">*Наборе доступности* которого используется для базы данных и приложения службы на первичном сайте hello</span><span class="sxs-lookup"><span data-stu-id="171fe-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="171fe-121">Один jumpbox на каждом сайте, который ограничивает доступ toohello частной сети и разрешает только вход администратора</span><span class="sxs-lookup"><span data-stu-id="171fe-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="171fe-122">среда Jumpbox, служба приложения, база данных и VPN-шлюз в отдельных подсетях;</span><span class="sxs-lookup"><span data-stu-id="171fe-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="171fe-123">группа безопасности сети, применяющаяся в подсетях приложения и базы данных;</span><span class="sxs-lookup"><span data-stu-id="171fe-123">NSG enforced on application and database subnets</span></span>

![Снимок экрана со страницей топологии hello аварийного восстановления](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="171fe-125">Сценарий 2. Основной локальный сайт и сайт аварийного восстановления в Azure</span><span class="sxs-lookup"><span data-stu-id="171fe-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="171fe-126">Клиент имеет локальную базу данных Oracle (основной сайт).</span><span class="sxs-lookup"><span data-stu-id="171fe-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="171fe-127">Сайт аварийного восстановления — в Azure.</span><span class="sxs-lookup"><span data-stu-id="171fe-127">A DR site is on Azure.</span></span> <span data-ttu-id="171fe-128">Oracle Data Guard используется для быстрого восстановления между этими сайтами.</span><span class="sxs-lookup"><span data-stu-id="171fe-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="171fe-129">Первичный сайт Hello оказывает баз данных-получателей для отчетности и других целей.</span><span class="sxs-lookup"><span data-stu-id="171fe-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="171fe-130">Существует два подхода для такой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="171fe-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="171fe-131">Способ 1: Прямые соединения между локальной и Azure, требуется открыть TCP-порты в брандмауэре hello</span><span class="sxs-lookup"><span data-stu-id="171fe-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="171fe-132">Мы не рекомендуем прямые подключения, так как они определяют toohello порты TCP hello за пределами world.</span><span class="sxs-lookup"><span data-stu-id="171fe-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="171fe-133">Топология</span><span class="sxs-lookup"><span data-stu-id="171fe-133">Topology</span></span>

<span data-ttu-id="171fe-134">Ниже приводится сводка hello Настройка Azure:</span><span class="sxs-lookup"><span data-stu-id="171fe-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="171fe-135">один сайт для аварийного восстановления;</span><span class="sxs-lookup"><span data-stu-id="171fe-135">One DR site</span></span> 
- <span data-ttu-id="171fe-136">Одна виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="171fe-136">One virtual network</span></span>
- <span data-ttu-id="171fe-137">одна база данных Oracle с Data Guard (активная);</span><span class="sxs-lookup"><span data-stu-id="171fe-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="171fe-138">Одно приложение службы на сайте hello аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="171fe-138">One application service on hello DR site</span></span>
- <span data-ttu-id="171fe-139">Один jumpbox, ограничивает доступ toohello частной сети, а только вход администратором</span><span class="sxs-lookup"><span data-stu-id="171fe-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="171fe-140">среда Jumpbox, служба приложения, база данных и VPN-шлюз в отдельных подсетях;</span><span class="sxs-lookup"><span data-stu-id="171fe-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="171fe-141">группа безопасности сети, применяющаяся в подсетях приложения и базы данных;</span><span class="sxs-lookup"><span data-stu-id="171fe-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="171fe-142">Политика и правила NSG tooallow входящего трафика TCP-порт 1521 (или порта, определяемые пользователем)</span><span class="sxs-lookup"><span data-stu-id="171fe-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="171fe-143">NSG правила и политики toorestrict только hello IP-адрес или адреса локальной (базы данных или приложения) tooaccess hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="171fe-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Снимок экрана со страницей топологии hello аварийного восстановления](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="171fe-145">Способ 2. VPN-подключение типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="171fe-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="171fe-146">Оптимальным способом является использование VPN-подключения типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="171fe-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="171fe-147">Дополнительные сведения о настройке VPN см. в статье [Создание виртуальной сети с VPN типа "сеть — сеть" с помощью интерфейса командной строки](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="171fe-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="171fe-148">Топология</span><span class="sxs-lookup"><span data-stu-id="171fe-148">Topology</span></span>

<span data-ttu-id="171fe-149">Ниже приводится сводка hello Настройка Azure:</span><span class="sxs-lookup"><span data-stu-id="171fe-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="171fe-150">один сайт для аварийного восстановления;</span><span class="sxs-lookup"><span data-stu-id="171fe-150">One DR site</span></span> 
- <span data-ttu-id="171fe-151">Одна виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="171fe-151">One virtual network</span></span> 
- <span data-ttu-id="171fe-152">одна база данных Oracle с Data Guard (активная);</span><span class="sxs-lookup"><span data-stu-id="171fe-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="171fe-153">Одно приложение службы на сайте hello аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="171fe-153">One application service on hello DR site</span></span>
- <span data-ttu-id="171fe-154">Один jumpbox, ограничивает доступ toohello частной сети, а только вход администратором</span><span class="sxs-lookup"><span data-stu-id="171fe-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="171fe-155">среда Jumpbox, служба приложения, база данных и VPN-шлюз находятся в отдельных подсетях;</span><span class="sxs-lookup"><span data-stu-id="171fe-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="171fe-156">группа безопасности сети, применяющаяся в подсетях приложения и базы данных;</span><span class="sxs-lookup"><span data-stu-id="171fe-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="171fe-157">VPN-подключение типа "сеть — сеть" между локальной средой и Azure.</span><span class="sxs-lookup"><span data-stu-id="171fe-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Снимок экрана со страницей топологии hello аварийного восстановления](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="171fe-159">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="171fe-159">Additional reading</span></span>

- <span data-ttu-id="171fe-160">[Design and implement an Oracle database in Azure](oracle-design.md) (Разработка базы данных Oracle и ее реализация в Azure)</span><span class="sxs-lookup"><span data-stu-id="171fe-160">[Design and implement an Oracle database on Azure](oracle-design.md)</span></span>
- [<span data-ttu-id="171fe-161">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="171fe-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="171fe-162">Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="171fe-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="171fe-163">Создание резервных копий и восстановление базы данных Oracle Database 12c на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="171fe-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="171fe-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="171fe-164">Next steps</span></span>

- <span data-ttu-id="171fe-165">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="171fe-165">[Tutorial: Create highly available VMs](../../linux/create-cli-complete.md)</span></span>
- <span data-ttu-id="171fe-166">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="171fe-166">[Explore VM deployment Azure CLI samples](../../linux/cli-samples.md)</span></span>
