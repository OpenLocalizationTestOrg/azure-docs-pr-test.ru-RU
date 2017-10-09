---
title: "aaaReplicate развертывания многоуровневого Dynamics AX, с помощью Azure Site Recovery | Документы Microsoft"
description: "В этой статье описывается как tooreplicate и защитить с помощью Azure Site Recovery Dynamics AX"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="437f5-103">Репликация многоуровневого приложения Dynamics AX с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="437f5-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="437f5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="437f5-104">Overview</span></span>


<span data-ttu-id="437f5-105">Microsoft Dynamics AX является одним из наиболее популярных решений ERP hello среди предприятий toostandardized процесса в расположениях, управления ресурсами и упрощая соответствие.</span><span class="sxs-lookup"><span data-stu-id="437f5-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="437f5-106">Учитывая приложение hello — критический tooan организации является очень важным toobe убедиться, что, если любой аварии, приложение должно быть запущен и работает в кратчайшие сроки.</span><span class="sxs-lookup"><span data-stu-id="437f5-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="437f5-107">На данный момент Microsoft Dynamics AX не предоставляет какие-либо готовые функции аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="437f5-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="437f5-108">Microsoft Dynamics AX состоит из многих компонентов сервера как базы данных объекта сервера приложений, Active Directory (AD), SQL Server, SharePoint Server, и т.д. сервер отчетов toomanage hello аварийного восстановления для каждого из этих компонентов вручную, не только ресурсоемким, но также вероятность ошибок.</span><span class="sxs-lookup"><span data-stu-id="437f5-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="437f5-109">В этой статье подробно рассматривается создание решения аварийного восстановления для приложения Dynamics AX с помощью [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="437f5-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="437f5-110">Кроме того, рассматривается плановая, незапланированная и тестовая отработка отказа с помощью плана восстановления одним щелчком, поддерживаемых конфигураций и необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="437f5-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="437f5-111">Решение аварийного восстановления на основе Azure Site Recovery полностью протестировано, сертифицировано и рекомендовано рабочей группой Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="437f5-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="437f5-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="437f5-112">Prerequisites</span></span>

<span data-ttu-id="437f5-113">Реализация аварийного восстановления для приложения Dynamics AX, с помощью Azure Site Recovery требует hello следующих предварительных требований завершена.</span><span class="sxs-lookup"><span data-stu-id="437f5-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="437f5-114">•   Локальное развертывание Dynamics AX настроено.</span><span class="sxs-lookup"><span data-stu-id="437f5-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="437f5-115">•   Хранилище служб Azure Site Recovery создано в подписке Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="437f5-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="437f5-116">• Если Azure является сайта аварийного восстановления, запустите hello Оценка готовности виртуальной машины Azure на виртуальные машины tooensure, они были совместимы с виртуальными машинами Azure и служб Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="437f5-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="437f5-117">Поддержка Site Recovery</span><span class="sxs-lookup"><span data-stu-id="437f5-117">Site Recovery support</span></span>

<span data-ttu-id="437f5-118">Hello целью написания данной статьи использовались виртуальные машины VMware с Dynamics AX 2012R3 на Windows Server 2012 R2 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="437f5-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="437f5-119">Как репликация восстановления сайтов не зависит от приложения, рекомендации hello приведены здесь ожидаемый toohold также в следующих сценариях.</span><span class="sxs-lookup"><span data-stu-id="437f5-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="437f5-120">Исходный и целевой объект</span><span class="sxs-lookup"><span data-stu-id="437f5-120">Source and target</span></span>

<span data-ttu-id="437f5-121">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="437f5-121">**Scenario**</span></span> | <span data-ttu-id="437f5-122">**tooa вторичного сайта**</span><span class="sxs-lookup"><span data-stu-id="437f5-122">**tooa secondary site**</span></span> | <span data-ttu-id="437f5-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="437f5-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="437f5-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="437f5-124">**Hyper-V**</span></span> | <span data-ttu-id="437f5-125">Да</span><span class="sxs-lookup"><span data-stu-id="437f5-125">Yes</span></span> | <span data-ttu-id="437f5-126">Да</span><span class="sxs-lookup"><span data-stu-id="437f5-126">Yes</span></span>
<span data-ttu-id="437f5-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="437f5-127">**VMware**</span></span> | <span data-ttu-id="437f5-128">Да</span><span class="sxs-lookup"><span data-stu-id="437f5-128">Yes</span></span> | <span data-ttu-id="437f5-129">Да</span><span class="sxs-lookup"><span data-stu-id="437f5-129">Yes</span></span>
<span data-ttu-id="437f5-130">**Физический сервер**</span><span class="sxs-lookup"><span data-stu-id="437f5-130">**Physical server**</span></span> | <span data-ttu-id="437f5-131">Да</span><span class="sxs-lookup"><span data-stu-id="437f5-131">Yes</span></span> | <span data-ttu-id="437f5-132">Да</span><span class="sxs-lookup"><span data-stu-id="437f5-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="437f5-133">Реализация аварийного восстановления для приложений Dynamics AX с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="437f5-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="437f5-134">Защита приложения Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="437f5-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="437f5-135">Каждый компонент toobe потребностей Dynamics AX hello защищенных репликации полное приложение hello tooenable и восстановления.</span><span class="sxs-lookup"><span data-stu-id="437f5-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="437f5-136">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="437f5-136">This section covers:</span></span>

<span data-ttu-id="437f5-137">**1. Защита Active Directory**</span><span class="sxs-lookup"><span data-stu-id="437f5-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="437f5-138">**2. Защита уровня SQL**</span><span class="sxs-lookup"><span data-stu-id="437f5-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="437f5-139">**3. Защита уровня приложений и веб-уровня**</span><span class="sxs-lookup"><span data-stu-id="437f5-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="437f5-140">**4. Конфигурация сети**</span><span class="sxs-lookup"><span data-stu-id="437f5-140">**4. Networking configuration**</span></span>

<span data-ttu-id="437f5-141">**5. План восстановления**</span><span class="sxs-lookup"><span data-stu-id="437f5-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="437f5-142">1. Настройка AD и репликация DNS</span><span class="sxs-lookup"><span data-stu-id="437f5-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="437f5-143">На сайте аварийного восстановления hello toofunction приложение Dynamics AX требуется Active Directory.</span><span class="sxs-lookup"><span data-stu-id="437f5-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="437f5-144">Существует две рекомендуемые варианты в зависимости от сложности hello hello клиента в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="437f5-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="437f5-145">**Вариант 1**</span><span class="sxs-lookup"><span data-stu-id="437f5-145">**Option 1**</span></span>

<span data-ttu-id="437f5-146">Если у клиента hello небольшое количество приложений и один контроллер домена для всей своей локального сайта и будет завершаться hello всего узла вместе, то мы рекомендуем использовать ASR репликации tooreplicate hello контроллера домена компьютере toosecondary сайта ( применимо для сайта tooSite и tooAzure сайта).</span><span class="sxs-lookup"><span data-stu-id="437f5-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="437f5-147">**Вариант 2**</span><span class="sxs-lookup"><span data-stu-id="437f5-147">**Option 2**</span></span>

<span data-ttu-id="437f5-148">Если hello клиента имеет большое количество приложений и выполняется в лесу Active Directory и переключается несколько приложений одновременно, то рекомендуется настроить дополнительный контроллер домена на сайте hello аварийного восстановления (вторичного сайта или в Azure).</span><span class="sxs-lookup"><span data-stu-id="437f5-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="437f5-149">См. слишком[дополнительное руководство по на доступность контроллера домена на сайте аварийного восстановления](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="437f5-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="437f5-150">Далее в этом документе подразумевается, что контроллер домена доступен на сайте аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="437f5-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="437f5-151">2) Настройка репликации SQL Server</span><span class="sxs-lookup"><span data-stu-id="437f5-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="437f5-152">Подробное техническое руководство по hello, рекомендуется использовать параметр для защиты см. руководство по toocompanion [уровня SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="437f5-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="437f5-153">3. Включение защиты для клиента Dynamics AX и виртуальных машин AOS</span><span class="sxs-lookup"><span data-stu-id="437f5-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="437f5-154">Выполнить на ли hello виртуальных машин, развернутых на основе конфигурации Azure Site Recovery [Hyper-V](site-recovery-hyper-v-site-to-azure.md) или [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="437f5-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="437f5-155">Рекомендуемые tooconfigure частота для согласованности аварийного завершения составляет 15 минут.</span><span class="sxs-lookup"><span data-stu-id="437f5-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="437f5-156">Hello ниже моментального снимка состояние hello защиты виртуальных машин Dynamics компонента в сценарий защиты «TooAzure сайт VMware».</span><span class="sxs-lookup"><span data-stu-id="437f5-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="437f5-157">![Защищенные элементы](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="437f5-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="437f5-158">4. Настройка сети</span><span class="sxs-lookup"><span data-stu-id="437f5-158">4. Configure Networking</span></span>
<span data-ttu-id="437f5-159">Настройка параметров вычислений и сети для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="437f5-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="437f5-160">Для клиента AX hello и виртуальных машин AOS конфигурации сети в Azure Site Recovery, чтобы сети виртуальных Машин hello получить вложенные toohello правильной сети аварийного восстановления после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="437f5-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="437f5-161">Убедитесь, что сетевой hello аварийного восстановления для этих уровней является маршрутизируемым toohello уровня SQL.</span><span class="sxs-lookup"><span data-stu-id="437f5-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="437f5-162">Можно выбрать hello виртуальной Машины в hello реплицируются параметры сети hello tooconfigure элементов как показано ниже снимка hello.</span><span class="sxs-lookup"><span data-stu-id="437f5-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="437f5-163">Для серверов AOS выберите набор правильное значение доступности hello.</span><span class="sxs-lookup"><span data-stu-id="437f5-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="437f5-164">Если используется статический IP-адрес, а затем укажите IP-адрес hello требуется hello tootake виртуальной машины в hello **целевой IP-адрес** поле ![параметры сети](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="437f5-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="437f5-165">5. Создание плана восстановления</span><span class="sxs-lookup"><span data-stu-id="437f5-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="437f5-166">В процессе отработки отказа hello tooautomate Azure Site Recovery, можно создать план восстановления.</span><span class="sxs-lookup"><span data-stu-id="437f5-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="437f5-167">Добавьте в план восстановления hello уровень приложения и веб-уровня.</span><span class="sxs-lookup"><span data-stu-id="437f5-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="437f5-168">Расположите их в разные группы так, hello переднего плана завершения работы до уровня приложения.</span><span class="sxs-lookup"><span data-stu-id="437f5-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="437f5-169">Выберите хранилище Azure Site Recovery hello в вашей подписке и щелкните плитку «Планы восстановления».</span><span class="sxs-lookup"><span data-stu-id="437f5-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="437f5-170">Нажмите кнопку "Добавить план восстановления" и укажите имя.</span><span class="sxs-lookup"><span data-stu-id="437f5-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="437f5-171">Выберите hello «Источник» и «Целевой объект».</span><span class="sxs-lookup"><span data-stu-id="437f5-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="437f5-172">Hello цель может быть Azure или вторичного сайта.</span><span class="sxs-lookup"><span data-stu-id="437f5-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="437f5-173">В случае, если выбран Azure, необходимо указать модель развертывания hello</span><span class="sxs-lookup"><span data-stu-id="437f5-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Создание плана восстановления](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="437f5-175">Выберите hello AOS и план восстановления toohello виртуальные машины клиента и нажмите кнопку ✓.</span><span class="sxs-lookup"><span data-stu-id="437f5-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="437f5-176">![Создание плана восстановления](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="437f5-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![План восстановления](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="437f5-178">Hello план восстановления для приложения Dynamics AX можно настроить, добавив различные действия, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="437f5-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="437f5-179">Hello выше моментального снимка показывает hello всего плана восстановления после добавления всех шагов hello.</span><span class="sxs-lookup"><span data-stu-id="437f5-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="437f5-180">*Действия:*</span><span class="sxs-lookup"><span data-stu-id="437f5-180">*Steps:*</span></span>

<span data-ttu-id="437f5-181">*1. Действия по отработке отказа для SQL Server.*</span><span class="sxs-lookup"><span data-stu-id="437f5-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="437f5-182">См. слишком[«Решения аварийного восстановления SQL Server»](site-recovery-sql.md) дополнительное руководство по подробные сведения о сервере tooSQL определенные шаги восстановления.</span><span class="sxs-lookup"><span data-stu-id="437f5-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="437f5-183">*2. Переход на другой ресурс группа 1: Отработки отказа виртуальных машин AOS hello*</span><span class="sxs-lookup"><span data-stu-id="437f5-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="437f5-184">Убедитесь, что выбранная точка восстановления hello максимально близко базы данных возможно toohello PIT, но не вперед.</span><span class="sxs-lookup"><span data-stu-id="437f5-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="437f5-185">*3. Скрипт: Подсистема балансировки нагрузки добавить (только E-A)* добавления сценария (с помощью службы автоматизации Azure) после группы ВМ AOS появится tooadd tooit подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="437f5-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="437f5-186">Эту задачу можно использовать toodo сценария.</span><span class="sxs-lookup"><span data-stu-id="437f5-186">You can use a script toodo this task.</span></span> <span data-ttu-id="437f5-187">См. в статье [как tooadd Подсистема балансировки нагрузки для многоуровневого приложения аварийного восстановления](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="437f5-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="437f5-188">*4. Переход на другой ресурс группа 2: Переход на клиенте AX hello виртуальных машин.*</span><span class="sxs-lookup"><span data-stu-id="437f5-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="437f5-189">При сбое hello веб-уровень виртуальных машин в рамках плана восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="437f5-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="437f5-190">Тестовая отработка отказа</span><span class="sxs-lookup"><span data-stu-id="437f5-190">Doing a test failover</span></span>

<span data-ttu-id="437f5-191">Too'AD решение аварийного восстановления см. "и «Решения аварийного восстановления SQL Server» Дополнительные руководства для конкретных tooAD вопросы и SQL server, соответственно, при тесте отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="437f5-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="437f5-192">Портал tooAzure перейти и выбрать хранилище Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="437f5-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="437f5-193">Щелкните hello плана восстановления, созданных для Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="437f5-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="437f5-194">Щелкните "Тестовая отработка отказа".</span><span class="sxs-lookup"><span data-stu-id="437f5-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="437f5-195">Выберите hello виртуальной сети toostart hello сбое процесс тестирования.</span><span class="sxs-lookup"><span data-stu-id="437f5-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="437f5-196">После hello получателей среде можно выполнять вашей проверки.</span><span class="sxs-lookup"><span data-stu-id="437f5-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="437f5-197">После завершения проверки hello, «Выполнить проверку» можно выбрать и hello тестовой среды отработки отказа будет очищен.</span><span class="sxs-lookup"><span data-stu-id="437f5-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="437f5-198">Выполните [в этом руководстве](site-recovery-test-failover-to-azure.md) toodo тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="437f5-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="437f5-199">Отработка отказа</span><span class="sxs-lookup"><span data-stu-id="437f5-199">Doing a failover</span></span>

1.  <span data-ttu-id="437f5-200">Портал tooAzure перейти и выбрать хранилище Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="437f5-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="437f5-201">Щелкните hello плана восстановления, созданных для Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="437f5-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="437f5-202">Щелкните "Отработка отказа" и выберите "Отработка отказа".</span><span class="sxs-lookup"><span data-stu-id="437f5-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="437f5-203">Выберите целевой сети hello и щелкните процесс ✓ toostart hello отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="437f5-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="437f5-204">При выполнении отработки отказа используйте [это руководство](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="437f5-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="437f5-205">Восстановление размещения</span><span class="sxs-lookup"><span data-stu-id="437f5-205">Perform a Failback</span></span>

<span data-ttu-id="437f5-206">Ссылки too'SQL решение аварийного восстановления сервера "дополнительное руководство по для сервера tooSQL определенные вопросы при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="437f5-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="437f5-207">Портал tooAzure перейти и выбрать хранилище Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="437f5-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="437f5-208">Щелкните hello плана восстановления, созданных для Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="437f5-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="437f5-209">Щелкните "Отработка отказа" и выберите "Отработка отказа".</span><span class="sxs-lookup"><span data-stu-id="437f5-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="437f5-210">Щелкните "Изменить направление".</span><span class="sxs-lookup"><span data-stu-id="437f5-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="437f5-211">Выберите соответствующие параметры hello - синхронизации данных и параметры создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="437f5-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="437f5-212">Щелкните ✓ toostart hello «процесс восстановления размещения».</span><span class="sxs-lookup"><span data-stu-id="437f5-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="437f5-213">При восстановлении размещения используйте [это руководство](site-recovery-failback-azure-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="437f5-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="437f5-214">Сводка</span><span class="sxs-lookup"><span data-stu-id="437f5-214">Summary</span></span>
<span data-ttu-id="437f5-215">С помощью Azure Site Recovery можно создать полностью автоматизированный план аварийного восстановления для приложения Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="437f5-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="437f5-216">Вы может инициировать отработку отказа hello в течение секунды из любого места в hello событий перебои и получить приложение hello работающий в минутах.</span><span class="sxs-lookup"><span data-stu-id="437f5-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="437f5-217">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="437f5-217">Next steps</span></span>
<span data-ttu-id="437f5-218">Чтение [какие рабочие нагрузки защитить?](site-recovery-workload.md) toolearn Дополнительные сведения о защите рабочих нагрузок предприятия с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="437f5-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
