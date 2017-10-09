---
title: "обновление приложения aaaTroubleshooting | Документы Microsoft"
description: "В этой статье рассматриваются некоторых распространенных проблем при обновлении приложения Service Fabric и каким образом tooresolve их."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="9773e-103">Устранение неполадок при обновлениях приложений</span><span class="sxs-lookup"><span data-stu-id="9773e-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="9773e-104">В этой статье рассматриваются некоторые hello распространенных проблем при обновлении приложения Azure Service Fabric и каким образом tooresolve их.</span><span class="sxs-lookup"><span data-stu-id="9773e-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="9773e-105">Устранение неполадок при неудачном обновлении приложения</span><span class="sxs-lookup"><span data-stu-id="9773e-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="9773e-106">При сбое обновления выходные данные hello hello **Get-ServiceFabricApplicationUpgrade** команда содержит дополнительные сведения для отладки сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="9773e-107">Hello следующем списке указаны как можно использовать hello дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="9773e-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="9773e-108">Определите тип сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="9773e-109">Определите причину ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="9773e-110">Изоляция одного или нескольких отказавших компонентов для дальнейшего исследования.</span><span class="sxs-lookup"><span data-stu-id="9773e-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="9773e-111">Эта информация доступна, когда Service Fabric обнаруживает сбой hello независимо от того, является ли hello **FailureAction** tooroll возвращаю или приостановить обновление hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="9773e-112">Определите тип сбоя hello</span><span class="sxs-lookup"><span data-stu-id="9773e-112">Identify hello failure type</span></span>
<span data-ttu-id="9773e-113">В выходных данных hello **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** идентифицирует hello timestamp (в формате UTC), с которой была обнаружена ошибка обновления Service Fabric и  **FailureAction** было запущено.</span><span class="sxs-lookup"><span data-stu-id="9773e-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="9773e-114">**Причина ошибки** определяет одну из трех высокоуровневые причины сбоя hello:</span><span class="sxs-lookup"><span data-stu-id="9773e-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="9773e-115">UpgradeDomainTimeout - указывает, что определенного домена обновления заняло слишком много времени toocomplete и **UpgradeDomainTimeout** срок действия истек.</span><span class="sxs-lookup"><span data-stu-id="9773e-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="9773e-116">OverallUpgradeTimeout - указывает, что hello в целом обновления заняло слишком длинный toocomplete и **UpgradeTimeout** срок действия истек.</span><span class="sxs-lookup"><span data-stu-id="9773e-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="9773e-117">Технологий - указывает, что после обновления домен обновления, приложение hello оставались неработоспособное в соответствии с toohello указан политики работоспособности и **HealthCheckRetryTimeout** срок действия истек.</span><span class="sxs-lookup"><span data-stu-id="9773e-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="9773e-118">Эти записи отображаются только в выходных данных hello при сбое обновления hello и запускается откат.</span><span class="sxs-lookup"><span data-stu-id="9773e-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="9773e-119">Дополнительные сведения отображаются в зависимости от типа hello hello сбоя.</span><span class="sxs-lookup"><span data-stu-id="9773e-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="9773e-120">Исследование времени ожидания обновления</span><span class="sxs-lookup"><span data-stu-id="9773e-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="9773e-121">Сбои, связанные с истечением времени ожидания, чаще всего вызваны проблемами с доступностью служб.</span><span class="sxs-lookup"><span data-stu-id="9773e-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="9773e-122">Hello выходных данных ниже типичен для обновления, где реплик службы или экземпляры ошибкой toostart в новой версии кода hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="9773e-123">Hello **UpgradeDomainProgressAtFailure** поле создает снимок все ожидающие обновления работы во время hello сбоя.</span><span class="sxs-lookup"><span data-stu-id="9773e-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="9773e-124">В этом примере не удалось обновить hello в домене обновления *MYUD1* и двух секций (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* и *4b43f4d8-b26b-424e-9307-7a7a62e79750*) были затруднения.</span><span class="sxs-lookup"><span data-stu-id="9773e-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="9773e-125">Hello секции были затруднения из-за выполнения hello невозможно tooplace основной реплики (*WaitForPrimaryPlacement*) на целевых узлах *Node1* и *Node4*.</span><span class="sxs-lookup"><span data-stu-id="9773e-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="9773e-126">Hello **Get ServiceFabricNode** команду можно использовать tooverify, эти два узла в домене обновления *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="9773e-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="9773e-127">Hello *UpgradePhase* говорит *PostUpgradeSafetyCheck*, что означает, что эти проверки безопасности выполняются после завершения обновления всех узлов в домене обновления hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="9773e-128">Эта информация указывает tooa потенциальная проблема с новой версии кода приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="9773e-129">Hello наиболее распространенных проблем, ошибки службы Привет открыть или пути кода tooprimary повышения роли.</span><span class="sxs-lookup"><span data-stu-id="9773e-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="9773e-130">*UpgradePhase* из *PreUpgradeSafetyCheck* означает возникли проблемы, подготовка домена обновления hello, прежде чем она была проведена.</span><span class="sxs-lookup"><span data-stu-id="9773e-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="9773e-131">в этом случае Hello наиболее распространенных проблем являются ошибки службы закройте hello или понижения роли из путей основного кода.</span><span class="sxs-lookup"><span data-stu-id="9773e-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="9773e-132">Hello текущей **UpgradeState** — *RollingBackCompleted*, поэтому hello исходное обновление должно быть выполнено с помощью отката **FailureAction**, который автоматически откат обновления hello после сбоя.</span><span class="sxs-lookup"><span data-stu-id="9773e-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="9773e-133">Если было выполнено обновление исходного hello с ручной **FailureAction**, то обновление hello вместо этого будет в приостановленном состоянии tooallow динамической отладки приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="9773e-134">Исследование ошибок проверки работоспособности</span><span class="sxs-lookup"><span data-stu-id="9773e-134">Investigate health check failures</span></span>
<span data-ttu-id="9773e-135">Сбои проверки работоспособности могут быть вызваны различными ошибками, которые могут возникать после того, как обновление будет завершено во всех узлах в домене обновления при успешном выполнении всех проверок безопасности.</span><span class="sxs-lookup"><span data-stu-id="9773e-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="9773e-136">выходные данные Hello ниже типичен для сбоя обновления из-за проверок работоспособности toofailed.</span><span class="sxs-lookup"><span data-stu-id="9773e-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="9773e-137">Hello **UnhealthyEvaluations** поле создает снимок проверку работоспособности, не прошедшие во время hello hello обновления в соответствии с toohello указан [политики работоспособности](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9773e-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="9773e-138">Сначала исследование ошибок проверки работоспособности требует понимания модель работоспособности Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="9773e-139">Но даже без таких глубокое понимание, мы видим, что две службы находятся в неработоспособном состоянии: *fabric: / DemoApp/Svc3* и *fabric: / DemoApp/Svc2*, вместе с отчеты о работоспособности ошибки hello («InjectedFault «в данном случае).</span><span class="sxs-lookup"><span data-stu-id="9773e-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="9773e-140">В этом примере два из четырех служб находятся в неработоспособном состоянии, это меньше целевой объект по умолчанию hello 0% неработоспособное (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="9773e-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="9773e-141">Hello обновление было приостановлено после сбоя, указав **FailureAction** Если ручной запуск hello обновления.</span><span class="sxs-lookup"><span data-stu-id="9773e-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="9773e-142">Этот режим позволяет нам tooinvestigate hello динамической системы в состоянии hello не удалось выполнить перед переводом никаких дальнейших действий.</span><span class="sxs-lookup"><span data-stu-id="9773e-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="9773e-143">Восстановление при приостановке обновления</span><span class="sxs-lookup"><span data-stu-id="9773e-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="9773e-144">С помощью отката **FailureAction**, нет, восстановление не требуется, так как обновление hello автоматический откат после сбоя.</span><span class="sxs-lookup"><span data-stu-id="9773e-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="9773e-145">При установке действия **FailureAction**, выполняемого вручную, существует несколько вариантов восстановления.</span><span class="sxs-lookup"><span data-stu-id="9773e-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="9773e-146">Запуск отката.</span><span class="sxs-lookup"><span data-stu-id="9773e-146">trigger a rollback</span></span>
2. <span data-ttu-id="9773e-147">Пройдите оставшуюся hello hello обновления вручную</span><span class="sxs-lookup"><span data-stu-id="9773e-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="9773e-148">Возобновить hello отслеживать обновления</span><span class="sxs-lookup"><span data-stu-id="9773e-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="9773e-149">Hello **ServiceFabricApplicationRollback начала** команда может применяться в любое время toostart откат приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="9773e-150">После hello команда возвращает успешно, запрос отката hello был зарегистрирован в системе hello и вскоре после этого запускает.</span><span class="sxs-lookup"><span data-stu-id="9773e-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="9773e-151">Hello **командлет Resume-ServiceFabricApplicationUpgrade** можно использовать команду tooproceed через hello оставшуюся часть hello обновление вручную, один домен обновления одновременно.</span><span class="sxs-lookup"><span data-stu-id="9773e-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="9773e-152">В этом режиме проверки безопасности только выполняемых системой hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="9773e-153">Никаких дополнительных проверок работоспособности выполняться не будет.</span><span class="sxs-lookup"><span data-stu-id="9773e-153">No more health checks are performed.</span></span> <span data-ttu-id="9773e-154">Эта команда может использоваться, только когда hello *UpgradeState* показывает *RollingForwardPending*, что означает, что текущий домен обновления hello закончила обновление, но hello Далее она не запущена (ожидание).</span><span class="sxs-lookup"><span data-stu-id="9773e-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="9773e-155">Hello **ServiceFabricApplicationUpgrade обновление** команда может быть используется tooresume hello отслеживаемых проверок безопасности и работоспособности выполнить обновление.</span><span class="sxs-lookup"><span data-stu-id="9773e-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="9773e-156">Обновление Hello продолжается с домен обновления hello, где оно было приостановлено и используйте hello же обновления параметры и политики работоспособности как перед.</span><span class="sxs-lookup"><span data-stu-id="9773e-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="9773e-157">При необходимости, все обновления параметров hello и политики работоспособности, показано в предшествующих выходных данных hello может изменяться в hello же команды при возобновлении hello обновления.</span><span class="sxs-lookup"><span data-stu-id="9773e-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="9773e-158">В этом примере обновление hello возобновлен в режиме отслеживаемое с параметрами hello и политики работоспособности hello без изменений.</span><span class="sxs-lookup"><span data-stu-id="9773e-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="9773e-159">Дальнейшее устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9773e-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="9773e-160">Service Fabric не подписан hello указан политики работоспособности</span><span class="sxs-lookup"><span data-stu-id="9773e-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="9773e-161">Возможная причина 1.</span><span class="sxs-lookup"><span data-stu-id="9773e-161">Possible Cause 1:</span></span>

<span data-ttu-id="9773e-162">Service Fabric преобразует все проценты в фактическое число сущностей (например, реплики, секций и службы) для оценки работоспособности и всегда округляет toowhole сущностей.</span><span class="sxs-lookup"><span data-stu-id="9773e-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="9773e-163">Например, если hello максимальное *MaxPercentUnhealthyReplicasPerPartition* % 21 и есть пяти реплик, то Service Fabric позволяет вверх tootwo неработоспособных реплик (то есть,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="9773e-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="9773e-164">Поэтому политики работоспособности должны быть настроены с учетом этого.</span><span class="sxs-lookup"><span data-stu-id="9773e-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="9773e-165">Возможная причина 2.</span><span class="sxs-lookup"><span data-stu-id="9773e-165">Possible Cause 2:</span></span>

<span data-ttu-id="9773e-166">Политики работоспособности указываются в процентах от общего числа служб, а не в конкретных экземплярах служб.</span><span class="sxs-lookup"><span data-stu-id="9773e-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="9773e-167">Например, перед обновлением, если приложение имеет четыре экземпляров A, B, C и D, службы, где службы D находится в неработоспособном состоянии, но с прямым toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="9773e-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="9773e-168">Мы хотим известные неработоспособности службы D hello обновления и установите параметр hello tooignore *MaxPercentUnhealthyServices* toobe 25%, при условии, что только A, B и C должны toobe работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="9773e-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="9773e-169">Тем не менее во время обновления hello D могут стать работоспособное при C переходит в неработоспособное.</span><span class="sxs-lookup"><span data-stu-id="9773e-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="9773e-170">Обновление Hello по-прежнему пройдет успешно, так как только 25% hello службы находятся в неработоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="9773e-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="9773e-171">Тем не менее это может привести в непредвиденных ошибок из-за которой tooC неожиданно неработоспособное вместо г. В этом случае D должен моделироваться типом другую службу из A, B и C. Так как политики работоспособности указаны каждого типа службы, другой неработоспособное процент пороговые значения можно примененных toodifferent служб.</span><span class="sxs-lookup"><span data-stu-id="9773e-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="9773e-172">Я не указан в политике работоспособности для обновления приложения, но hello по-прежнему произошел сбой при обновлении некоторые значения времени ожидания, которые никогда не указаны</span><span class="sxs-lookup"><span data-stu-id="9773e-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="9773e-173">Если политики работоспособности не предоставлен запрос на обновление toohello, они берутся из hello *ApplicationManifest.xml* hello текущей версии приложения.</span><span class="sxs-lookup"><span data-stu-id="9773e-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="9773e-174">Например при обновлении приложения X из версии 1.0 tooversion 2.0 используются политики работоспособности приложения, указанное для версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="9773e-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="9773e-175">Если политика работоспособности различных должен использоваться для обновления hello, политики hello должен toobe, заданный как часть вызова API обновления приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="9773e-176">политики Hello, заданный как часть вызова hello API применяются только во время обновления hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="9773e-177">После завершения обновления hello hello политики, указанный в hello *ApplicationManifest.xml* используются.</span><span class="sxs-lookup"><span data-stu-id="9773e-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="9773e-178">Указаны неверные значения времени ожидания</span><span class="sxs-lookup"><span data-stu-id="9773e-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="9773e-179">Полагаю, вам интересно, что произойдет, если задать несогласованные значения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="9773e-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="9773e-180">Например, возможно, *UpgradeTimeout* , меньше, чем hello *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="9773e-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="9773e-181">Hello ответов — возвращает ошибку.</span><span class="sxs-lookup"><span data-stu-id="9773e-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="9773e-182">Ошибки возвращаются в том случае, если hello *UpgradeDomainTimeout* меньше, чем сумма hello *HealthCheckWaitDuration* и *HealthCheckRetryTimeout*, или если  *UpgradeDomainTimeout* меньше, чем сумма hello *HealthCheckWaitDuration* и *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="9773e-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="9773e-183">Мои обновления выполняются слишком долго</span><span class="sxs-lookup"><span data-stu-id="9773e-183">My upgrades are taking too long</span></span>
<span data-ttu-id="9773e-184">время Hello toocomplete обновления зависит от того, проверки работоспособности hello и указанного значения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="9773e-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="9773e-185">Проверки работоспособности и значения времени ожидания зависят от того, как долго toocopy, развертывание и стабилизация приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9773e-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="9773e-186">Слишком жесткое назначение времени ожидания может привести к большему числу сбоев при обновлении, поэтому при назначении значений времени ожидания рекомендуется консервативный подход.</span><span class="sxs-lookup"><span data-stu-id="9773e-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="9773e-187">Вот на взаимодействие с времени обновления hello тайм-ауты hello быстрое обновление.</span><span class="sxs-lookup"><span data-stu-id="9773e-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="9773e-188">Обновления для домена обновления не могут завершиться быстрее, чем сумма значений параметров *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="9773e-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="9773e-189">Сбой обновления не может произойти быстрее, чем сумма значений *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="9773e-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="9773e-190">Hello время обновления для обновления домена ограничивается *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="9773e-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="9773e-191">Если *HealthCheckRetryTimeout* и *HealthCheckStableDuration* оба не равны нулю и hello работоспособности приложения hello отслеживает переключение вперед и назад, то обновление hello произойдет тайм-аут на  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="9773e-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="9773e-192">*UpgradeDomainTimeout* начинается отсчет один раз hello обновления для текущего домена обновления hello начинается.</span><span class="sxs-lookup"><span data-stu-id="9773e-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9773e-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9773e-193">Next steps</span></span>
<span data-ttu-id="9773e-194">[Руководство по обновлению приложений Service Fabric с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md) поможет вам выполнить поэтапное обновление приложения с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9773e-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="9773e-195">[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9773e-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="9773e-196">Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="9773e-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="9773e-197">Обеспечить совместимость на обновление приложения путем изучения как toouse [сериализации данных](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="9773e-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="9773e-198">Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="9773e-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
