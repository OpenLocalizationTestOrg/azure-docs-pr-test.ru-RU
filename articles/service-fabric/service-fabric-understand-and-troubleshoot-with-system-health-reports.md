---
title: "aaaTroubleshoot с отчеты о работоспособности системы | Документы Microsoft"
description: "Описание отчетов о работоспособности hello, отправленных компонентами Azure Service Fabric и их использования для устранения неполадок кластера или проблемы с приложением."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="09e49-103">Использовать tootroubleshoot отчеты о работоспособности системы</span><span class="sxs-lookup"><span data-stu-id="09e49-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="09e49-104">Azure Service Fabric компоненты отчет стандартной hello все сущности в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="09e49-105">Hello [базе данных health store](service-fabric-health-introduction.md#health-store) создает и удаляет сущности на основании отчетов системы hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="09e49-106">Кроме того, эти сущности упорядочиваются в иерархию с учетом взаимодействия между ними.</span><span class="sxs-lookup"><span data-stu-id="09e49-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="09e49-107">Основные понятия здоровья toounderstand, ознакомьтесь с дополнительными на [модель работоспособности Service Fabric](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="09e49-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="09e49-108">В отчетах о работоспособности системы отражаются показатели функциональности кластеров и приложений, а также отмечаются проблемы с работоспособностью.</span><span class="sxs-lookup"><span data-stu-id="09e49-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="09e49-109">Для приложений и служб отчеты о работоспособности системы убедитесь, что сущности, реализуются и правильно работает с hello перспективы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="09e49-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="09e49-110">Hello отчеты не имеют любой наблюдение за работоспособностью hello бизнес-логику службы hello или обнаружения зависших процессов.</span><span class="sxs-lookup"><span data-stu-id="09e49-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="09e49-111">Пользователь службы можно обогатить данные работоспособности hello с логикой конкретных tootheir сведения.</span><span class="sxs-lookup"><span data-stu-id="09e49-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="09e49-112">Отчеты о работоспособности watchdogs видны только *после* компоненты системы hello создание сущности.</span><span class="sxs-lookup"><span data-stu-id="09e49-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="09e49-113">При удалении сущности, базе данных health store hello автоматически удаляет все связанные с ним отчеты о работоспособности.</span><span class="sxs-lookup"><span data-stu-id="09e49-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="09e49-114">Hello это справедливо при создании нового экземпляра сущности hello (например, создается новый экземпляр службы с отслеживанием состояния сохраненного реплики).</span><span class="sxs-lookup"><span data-stu-id="09e49-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="09e49-115">Все отчеты, связанные с hello старого экземпляра удаляются и удаляются из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="09e49-116">Hello отчетов компонента системы идентифицируются hello источника, который начинается с hello»**системы.**»</span><span class="sxs-lookup"><span data-stu-id="09e49-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="09e49-117">.</span><span class="sxs-lookup"><span data-stu-id="09e49-117">prefix.</span></span> <span data-ttu-id="09e49-118">Watchdogs не следует использовать одинаковые префиксы для своих источников hello как отчеты с недопустимыми параметрами отклоняются.</span><span class="sxs-lookup"><span data-stu-id="09e49-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="09e49-119">Давайте рассмотрим некоторые системы сообщает toounderstand их триггеры и о том, как toocorrect hello возможные причины неполадок они представляют.</span><span class="sxs-lookup"><span data-stu-id="09e49-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="09e49-120">Service Fabric продолжается отчеты tooadd условиями интерес, повысить видимость выполняемых в кластере hello и приложения.</span><span class="sxs-lookup"><span data-stu-id="09e49-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="09e49-121">Также можно улучшить существующие отчеты более подробные данные, toohelp устранить проблему hello, быстрее.</span><span class="sxs-lookup"><span data-stu-id="09e49-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="09e49-122">Системные отчеты о работоспособности кластеров</span><span class="sxs-lookup"><span data-stu-id="09e49-122">Cluster system health reports</span></span>
<span data-ttu-id="09e49-123">сущности работоспособности кластера Hello автоматически создается в базе данных health store hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="09e49-124">Если все работает надлежащим образом, в этом хранилище нет системного отчета.</span><span class="sxs-lookup"><span data-stu-id="09e49-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="09e49-125">Потеря окружения</span><span class="sxs-lookup"><span data-stu-id="09e49-125">Neighborhood loss</span></span>
<span data-ttu-id="09e49-126">**System.Federation** сообщает об ошибке при обнаружении потери окружения.</span><span class="sxs-lookup"><span data-stu-id="09e49-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="09e49-127">Hello отчет получен из отдельных узлов, и идентификатор узла hello включается в имени свойства hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="09e49-128">В случае утраты одно окружение в hello всего обмена Service Fabric обычно можно ожидать два события (обе стороны hello разрыв отчета).</span><span class="sxs-lookup"><span data-stu-id="09e49-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="09e49-129">Если теряется несколько окружений, происходит больше событий.</span><span class="sxs-lookup"><span data-stu-id="09e49-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="09e49-130">Hello отчета указывает время ожидания аренды глобального hello как toolive время hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="09e49-131">отчет Hello повторен каждые половине длительность TTL hello при условии, что условие hello остается активным.</span><span class="sxs-lookup"><span data-stu-id="09e49-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="09e49-132">событие Hello автоматически удаляется после истечения срока его действия.</span><span class="sxs-lookup"><span data-stu-id="09e49-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="09e49-133">Удалите при истекшим сроком действия поведение гарантирует, что отчет hello очистки из хранилища работоспособности hello правильно, даже если hello узел «отчеты» не работает.</span><span class="sxs-lookup"><span data-stu-id="09e49-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="09e49-134">**SourceId**: System.Federation.</span><span class="sxs-lookup"><span data-stu-id="09e49-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="09e49-135">**Свойство**: начинается с **Neighborhood** и включает сведения об узле.</span><span class="sxs-lookup"><span data-stu-id="09e49-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="09e49-136">**Дальнейшие действия**: изучить, почему окружение hello теряется (например, проверка hello связи между узлами кластера).</span><span class="sxs-lookup"><span data-stu-id="09e49-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="09e49-137">Системные отчеты о работоспособности узлов</span><span class="sxs-lookup"><span data-stu-id="09e49-137">Node system health reports</span></span>
<span data-ttu-id="09e49-138">**System.FM**, который представляет службу диспетчера отказоустойчивости hello, hello центром сертификации, который управляет сведения об узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="09e49-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="09e49-139">Каждый узел должен содержать один отчет системы System.FM о его состоянии.</span><span class="sxs-lookup"><span data-stu-id="09e49-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="09e49-140">Hello узла сущностей удаляются при удалении состояния узла hello (см. [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="09e49-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="09e49-141">Включение и отключение узла</span><span class="sxs-lookup"><span data-stu-id="09e49-141">Node up/down</span></span>
<span data-ttu-id="09e49-142">System.FM отчеты в виде ОК при присоединении узла hello кольцо hello (это работает).</span><span class="sxs-lookup"><span data-stu-id="09e49-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="09e49-143">Сообщение об ошибке при hello узла не соответствует кольцо hello (для обновления или просто не работает, либо из-за непрохождения).</span><span class="sxs-lookup"><span data-stu-id="09e49-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="09e49-144">иерархии работоспособности Hello, построенных по базе данных health store hello предпринимает действия развернутой сущностей в связи с System.FM отчеты узлов.</span><span class="sxs-lookup"><span data-stu-id="09e49-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="09e49-145">Он считает узел hello виртуальный родительский всех развернутых сущностей.</span><span class="sxs-lookup"><span data-stu-id="09e49-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="09e49-146">сущности Hello развернуты на этом узле, предоставляются через запросы, если узел hello вверх по System.FM, с hello же экземпляр как экземпляр hello, связанный с сущностями hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="09e49-147">Если System.FM сообщение hello узла не работает или перезапуска (экземпляра), базе данных health store hello автоматически очищает hello развертывания сущностей, которые могут существовать только hello работу узла или hello предыдущий экземпляр узла hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="09e49-148">**SourceId**: System.FM.</span><span class="sxs-lookup"><span data-stu-id="09e49-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="09e49-149">**Свойство**: State.</span><span class="sxs-lookup"><span data-stu-id="09e49-149">**Property**: State</span></span>
* <span data-ttu-id="09e49-150">**Дальнейшие действия**: Если hello узел не работает для обновления, он должен возвращаться к работе после его обновления.</span><span class="sxs-lookup"><span data-stu-id="09e49-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="09e49-151">В этом случае состояние работоспособности hello следует перейти назад tooOK.</span><span class="sxs-lookup"><span data-stu-id="09e49-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="09e49-152">Если узел hello не возвращаться или завершается с ошибкой, hello проблема, требующая дополнительного изучения.</span><span class="sxs-lookup"><span data-stu-id="09e49-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="09e49-153">Hello ниже приведен пример hello System.FM событий с состоянием работоспособности ОК для узла.</span><span class="sxs-lookup"><span data-stu-id="09e49-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="09e49-154">Истечение срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="09e49-154">Certificate expiration</span></span>
<span data-ttu-id="09e49-155">**System.FabricNode** отображает предупреждение, когда сертификаты, используемые узлом hello, истекающим сроком действия.</span><span class="sxs-lookup"><span data-stu-id="09e49-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="09e49-156">У каждого узла есть три сертификата: **Certificate_cluster**, **Certificate_server** и **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="09e49-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="09e49-157">При по крайней мере две недели до истечения срока действия hello состояние работоспособности hello отчетов — ОК.</span><span class="sxs-lookup"><span data-stu-id="09e49-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="09e49-158">Когда hello истечение срока действия в течение двух недель, тип отчета hello является предупреждением.</span><span class="sxs-lookup"><span data-stu-id="09e49-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="09e49-159">Бесконечный срок ЖИЗНИ этих событий, и они будут удалены после выхода узла из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="09e49-160">**SourceId**: System.FabricNode.</span><span class="sxs-lookup"><span data-stu-id="09e49-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="09e49-161">**Свойство**: начинается с **сертификат** и содержит дополнительные сведения о типе hello сертификата</span><span class="sxs-lookup"><span data-stu-id="09e49-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="09e49-162">**Дальнейшие действия**: обновление сертификатов hello, если они имеют истекающим сроком действия.</span><span class="sxs-lookup"><span data-stu-id="09e49-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="09e49-163">Нарушение емкости для загрузки</span><span class="sxs-lookup"><span data-stu-id="09e49-163">Load capacity violation</span></span>
<span data-ttu-id="09e49-164">Hello балансировки нагрузки Service Fabric отображает предупреждение, когда он обнаруживает нарушение емкости узла.</span><span class="sxs-lookup"><span data-stu-id="09e49-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="09e49-165">**SourceId**: System.PLB.</span><span class="sxs-lookup"><span data-stu-id="09e49-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="09e49-166">**Свойство**: начинается с **Capacity**.</span><span class="sxs-lookup"><span data-stu-id="09e49-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="09e49-167">**Дальнейшие действия**: проверка предоставленных метрики и представление текущей емкости hello на узле hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="09e49-168">Системные отчеты о работоспособности приложений</span><span class="sxs-lookup"><span data-stu-id="09e49-168">Application system health reports</span></span>
<span data-ttu-id="09e49-169">**System.CM**, который представляет службу диспетчера кластеров hello, hello центром сертификации, который управляет сведений о приложении.</span><span class="sxs-lookup"><span data-stu-id="09e49-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="09e49-170">Состояние</span><span class="sxs-lookup"><span data-stu-id="09e49-170">State</span></span>
<span data-ttu-id="09e49-171">System.CM отчеты в виде ОК после создания или обновления приложения hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="09e49-172">Информирует hello работоспособности хранилища при удалении приложения hello, чтобы его можно удалить из хранилища.</span><span class="sxs-lookup"><span data-stu-id="09e49-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="09e49-173">**SourceId**: System.CM.</span><span class="sxs-lookup"><span data-stu-id="09e49-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="09e49-174">**Свойство**: State.</span><span class="sxs-lookup"><span data-stu-id="09e49-174">**Property**: State</span></span>
* <span data-ttu-id="09e49-175">**Дальнейшие действия**: Если для создания или обновления приложения hello, он должен включать отчет о работоспособности hello диспетчер кластеров.</span><span class="sxs-lookup"><span data-stu-id="09e49-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="09e49-176">В противном случае проверьте состояние hello приложения hello запрос (например, hello командлета PowerShell **Get ServiceFabricApplication - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="09e49-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="09e49-177">Hello приведенном ниже примере показаны события состояния hello hello **fabric: / WordCount** приложения:</span><span class="sxs-lookup"><span data-stu-id="09e49-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="09e49-178">Системные отчеты о работоспособности служб</span><span class="sxs-lookup"><span data-stu-id="09e49-178">Service system health reports</span></span>
<span data-ttu-id="09e49-179">**System.FM**, который представляет службу диспетчера отказоустойчивости hello, hello центром сертификации, который управляет сведениями о службах.</span><span class="sxs-lookup"><span data-stu-id="09e49-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="09e49-180">Состояние</span><span class="sxs-lookup"><span data-stu-id="09e49-180">State</span></span>
<span data-ttu-id="09e49-181">System.FM отчеты в виде ОК, когда была создана служба hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="09e49-182">Удаляет из хранилища работоспособности hello hello сущности при hello службы был удален.</span><span class="sxs-lookup"><span data-stu-id="09e49-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="09e49-183">**SourceId**: System.FM.</span><span class="sxs-lookup"><span data-stu-id="09e49-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="09e49-184">**Свойство**: State.</span><span class="sxs-lookup"><span data-stu-id="09e49-184">**Property**: State</span></span>

<span data-ttu-id="09e49-185">Hello пример hello события состояния службы hello **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="09e49-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="09e49-186">Ошибка сопоставления службы</span><span class="sxs-lookup"><span data-stu-id="09e49-186">Service correlation error</span></span>
<span data-ttu-id="09e49-187">**System.PLB** сообщает об ошибке, когда обнаруживает, что обновление toobe службы, связанной с другой службой создает цепочку сходства.</span><span class="sxs-lookup"><span data-stu-id="09e49-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="09e49-188">Hello отчетов очищается, когда происходит успешное обновление.</span><span class="sxs-lookup"><span data-stu-id="09e49-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="09e49-189">**SourceId**: System.PLB.</span><span class="sxs-lookup"><span data-stu-id="09e49-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="09e49-190">**Свойство**: ServiceDescription.</span><span class="sxs-lookup"><span data-stu-id="09e49-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="09e49-191">**Дальнейшие действия**: hello проверка коррелированных описания службы.</span><span class="sxs-lookup"><span data-stu-id="09e49-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="09e49-192">Системные отчеты о работоспособности разделов</span><span class="sxs-lookup"><span data-stu-id="09e49-192">Partition system health reports</span></span>
<span data-ttu-id="09e49-193">**System.FM**, который представляет службу диспетчера отказоустойчивости hello, hello центром сертификации, который управляет сведениями о секциях службы.</span><span class="sxs-lookup"><span data-stu-id="09e49-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="09e49-194">Состояние</span><span class="sxs-lookup"><span data-stu-id="09e49-194">State</span></span>
<span data-ttu-id="09e49-195">System.FM отчеты в виде ОК, если секция hello будет создана и находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="09e49-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="09e49-196">Удаляет из хранилища работоспособности hello hello сущности при hello секция, удаляется.</span><span class="sxs-lookup"><span data-stu-id="09e49-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="09e49-197">Если раздел hello ниже счетчик минимальное реплики hello, он сообщает об ошибке.</span><span class="sxs-lookup"><span data-stu-id="09e49-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="09e49-198">Если секция hello не меньше минимального реплики счетчика hello, но находится ниже числа реплик целевых hello, он выводит предупреждение.</span><span class="sxs-lookup"><span data-stu-id="09e49-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="09e49-199">Если раздел hello потери кворума, System.FM сообщает об ошибке.</span><span class="sxs-lookup"><span data-stu-id="09e49-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="09e49-200">Другие важные события включать предупреждение, когда перенастройки hello занимает больше времени, чем ожидалось, и если сборки hello занимает больше времени, чем ожидалось.</span><span class="sxs-lookup"><span data-stu-id="09e49-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="09e49-201">Hello ожидаемого времени для построения hello и изменения конфигурации можно настроить на основе сценариев службы.</span><span class="sxs-lookup"><span data-stu-id="09e49-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="09e49-202">Например если служба имеет терабайт данных состояния, таких как база данных SQL, требуется больше времени, чем для службы с помощью небольшого количества состояние сборки hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="09e49-203">**SourceId**: System.FM.</span><span class="sxs-lookup"><span data-stu-id="09e49-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="09e49-204">**Свойство**: State.</span><span class="sxs-lookup"><span data-stu-id="09e49-204">**Property**: State</span></span>
* <span data-ttu-id="09e49-205">**Дальнейшие действия**: Если состояние работоспособности hello не ОК, все равно возможно, что некоторые реплики не были созданный opened и повышенным уровнем tooprimary или дополнительных правильно.</span><span class="sxs-lookup"><span data-stu-id="09e49-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="09e49-206">Во многих случаях hello корневой причиной является ошибка в Привет открыть или изменить роль реализации службы.</span><span class="sxs-lookup"><span data-stu-id="09e49-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="09e49-207">Следующий пример Hello показано работоспособное секции:</span><span class="sxs-lookup"><span data-stu-id="09e49-207">hello following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="09e49-208">Hello пример hello состояние работоспособности раздела под счетчик целевой реплики.</span><span class="sxs-lookup"><span data-stu-id="09e49-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="09e49-209">Hello следующим шагом является описание раздела tooget hello, которое показано, как настроить: **MinReplicaSetSize** , равно 3 и **TargetReplicaSetSize** — семь.</span><span class="sxs-lookup"><span data-stu-id="09e49-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="09e49-210">Затем получите hello количество узлов в кластере hello: 5.</span><span class="sxs-lookup"><span data-stu-id="09e49-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="09e49-211">Поэтому в этом случае две реплики нельзя разместить, поскольку hello целевое количество реплик больше, чем число узлов, доступных в hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="09e49-212">Нарушение ограничений в отношении реплик</span><span class="sxs-lookup"><span data-stu-id="09e49-212">Replica constraint violation</span></span>
<span data-ttu-id="09e49-213">**System.PLB** выдает предупреждение, если обнаруживает нарушение ограничений реплик и не может разместить все реплики секции.</span><span class="sxs-lookup"><span data-stu-id="09e49-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="09e49-214">сведения об отчете Hello показывают, какие ограничения и свойства заблокируйте размещение реплики hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="09e49-215">**SourceId**: System.PLB.</span><span class="sxs-lookup"><span data-stu-id="09e49-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="09e49-216">**Свойство**: начинается с **ReplicaConstraintViolation**.</span><span class="sxs-lookup"><span data-stu-id="09e49-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="09e49-217">Системные отчеты о работоспособности реплик</span><span class="sxs-lookup"><span data-stu-id="09e49-217">Replica system health reports</span></span>
<span data-ttu-id="09e49-218">**System.RA**, который представляет компонента агента перенастройки hello, получает права hello состояние реплики hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="09e49-219">Состояние</span><span class="sxs-lookup"><span data-stu-id="09e49-219">State</span></span>
<span data-ttu-id="09e49-220">**System.RA** сообщает ОК после создания реплики hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="09e49-221">**SourceId**: System.RA.</span><span class="sxs-lookup"><span data-stu-id="09e49-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="09e49-222">**Свойство**: State.</span><span class="sxs-lookup"><span data-stu-id="09e49-222">**Property**: State</span></span>

<span data-ttu-id="09e49-223">Следующий пример Hello показано работоспособности реплики.</span><span class="sxs-lookup"><span data-stu-id="09e49-223">hello following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="09e49-224">Состояние открытия реплики</span><span class="sxs-lookup"><span data-stu-id="09e49-224">Replica open status</span></span>
<span data-ttu-id="09e49-225">Описание этого отчета о работоспособности Hello содержит время начала hello (время по Гринвичу), когда вызов hello API.</span><span class="sxs-lookup"><span data-stu-id="09e49-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="09e49-226">**System.RA** отображает предупреждение, если реплика Привет открыть выполняется дольше период hello настроен (по умолчанию: 30 минут).</span><span class="sxs-lookup"><span data-stu-id="09e49-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="09e49-227">Если hello API влияет на доступность службы, hello отчета выдается гораздо быстрее (с заданным интервалом, значение по умолчанию 30 секунд).</span><span class="sxs-lookup"><span data-stu-id="09e49-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="09e49-228">измеряется время Hello включает hello времени для репликации Привет открыть и откройте службу hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="09e49-229">Завершает изменения tooOK Hello свойство, если открыть hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="09e49-230">**SourceId**: System.RA.</span><span class="sxs-lookup"><span data-stu-id="09e49-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="09e49-231">**Свойство**. **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="09e49-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="09e49-232">**Дальнейшие действия**: Если состояние работоспособности hello не ОК, изучить, почему реплики Привет открыть занимает длительное время.</span><span class="sxs-lookup"><span data-stu-id="09e49-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="09e49-233">Медленный вызов API службы</span><span class="sxs-lookup"><span data-stu-id="09e49-233">Slow service API call</span></span>
<span data-ttu-id="09e49-234">**System.RAP** и **System.Replicator** выдать предупреждение, если код вызова пользовательского toohello службы занимает больше времени настройки hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="09e49-235">Предупреждение Hello очищается при завершении вызова hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="09e49-236">**SourceId**: System.RAP или System.Replicator.</span><span class="sxs-lookup"><span data-stu-id="09e49-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="09e49-237">**Свойство**: hello имя hello медленно API.</span><span class="sxs-lookup"><span data-stu-id="09e49-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="09e49-238">Описание Hello предоставляет дополнительные сведения о времени hello hello API был ожидание.</span><span class="sxs-lookup"><span data-stu-id="09e49-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="09e49-239">**Дальнейшие действия**: изучить, почему вызов hello занимает длительное время.</span><span class="sxs-lookup"><span data-stu-id="09e49-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="09e49-240">Следующий пример Hello показывает секции в потери кворума, а toofigure действия выполнено исследование hello почему.</span><span class="sxs-lookup"><span data-stu-id="09e49-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="09e49-241">Одна из реплик hello имеет состояние работоспособности предупреждения, чтобы получить его работоспособности.</span><span class="sxs-lookup"><span data-stu-id="09e49-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="09e49-242">Он показывает, что операция службы hello занимает длительное время, при возникновении события, о которых сообщили System.RAP.</span><span class="sxs-lookup"><span data-stu-id="09e49-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="09e49-243">После получения этих сведений hello следующим шагом является toolook в код службы hello и исследовать существует.</span><span class="sxs-lookup"><span data-stu-id="09e49-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="09e49-244">В этом случае hello **RunAsync** реализации службы с отслеживанием состояния hello вызывает необработанное исключение.</span><span class="sxs-lookup"><span data-stu-id="09e49-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="09e49-245">Hello реплик перезапуск, поэтому может не отображаться ни одной реплики в состояние предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="09e49-246">Можно повторить попытку получения состояния работоспособности hello и искать любые различия в идентификаторе hello реплики.</span><span class="sxs-lookup"><span data-stu-id="09e49-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="09e49-247">В некоторых случаях hello повторные попытки могут предоставить подсказки.</span><span class="sxs-lookup"><span data-stu-id="09e49-247">In certain cases, hello retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="09e49-248">При запуске приложения неисправный hello отладчике hello события диагностики windows hello Показать hello исключение из RunAsync:</span><span class="sxs-lookup"><span data-stu-id="09e49-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![События диагностики Visual Studio 2015: сбой RunAsync в fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="09e49-250">События диагностики Visual Studio 2015: сбой RunAsync в **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="09e49-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="09e49-251">Переполнение очереди репликации</span><span class="sxs-lookup"><span data-stu-id="09e49-251">Replication queue full</span></span>
<span data-ttu-id="09e49-252">**System.Replicator** отображает предупреждение, когда hello очередь репликации заполнена.</span><span class="sxs-lookup"><span data-stu-id="09e49-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="09e49-253">На hello первичной репликации обычно заполнения очереди из-за одной или нескольких вторичных реплик tooacknowledge медленных операций.</span><span class="sxs-lookup"><span data-stu-id="09e49-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="09e49-254">На вторичных hello обычно это происходит при медленных tooapply hello операций службы hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="09e49-255">Hello предупреждение будет удалено при hello очереди больше не заполнен.</span><span class="sxs-lookup"><span data-stu-id="09e49-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="09e49-256">**SourceId**: System.Replicator.</span><span class="sxs-lookup"><span data-stu-id="09e49-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="09e49-257">**Свойство**: **PrimaryReplicationQueueStatus** или **SecondaryReplicationQueueStatus**, в зависимости от роли реплики hello</span><span class="sxs-lookup"><span data-stu-id="09e49-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="09e49-258">Медленные операции именования</span><span class="sxs-lookup"><span data-stu-id="09e49-258">Slow Naming operations</span></span>
<span data-ttu-id="09e49-259">**System.NamingService** сообщает о состоянии работоспособности первичной реплики, когда операция именования длится больше допустимого.</span><span class="sxs-lookup"><span data-stu-id="09e49-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="09e49-260">Примеры операций именования — [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) и [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="09e49-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="09e49-261">Дополнительные методы можно найти в статьях, посвященных FabricClient, например в статье о [методах управления службами](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) или [методах управления свойствами](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="09e49-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="09e49-262">Hello службы именования разрешает расположение tooa имена службы в кластере hello и позволяет пользователям toomanage службы имена и свойства.</span><span class="sxs-lookup"><span data-stu-id="09e49-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="09e49-263">Это секционированная материализованная служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="09e49-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="09e49-264">Один из разделов hello представляет hello Authority Owner, который содержит метаданные о все имена структуры службы и службы.</span><span class="sxs-lookup"><span data-stu-id="09e49-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="09e49-265">Hello Service Fabric, называются сопоставленных toodifferent, вызывается секций имя владельца, поэтому служба hello является расширяемым.</span><span class="sxs-lookup"><span data-stu-id="09e49-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="09e49-266">Узнайте больше о [службе именования](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="09e49-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="09e49-267">При операции именование занимает больше времени, чем ожидалось, операция hello помечается отчет предупреждение на hello *первичная реплика hello упоминания служебного раздела служит hello операции*.</span><span class="sxs-lookup"><span data-stu-id="09e49-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="09e49-268">После успешного выполнения операции hello hello предупреждение очищается.</span><span class="sxs-lookup"><span data-stu-id="09e49-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="09e49-269">Если операция hello завершается с ошибкой, hello работоспособности отчет содержит подробные сведения об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="09e49-270">**SourceId**: System.NamingService.</span><span class="sxs-lookup"><span data-stu-id="09e49-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="09e49-271">**Свойство**: начинается с префикса **Duration_** и определяет медленной операцией hello и имя Service Fabric hello, на какие hello применяется операция.</span><span class="sxs-lookup"><span data-stu-id="09e49-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="09e49-272">Например если создать службу на имя структуры: / MyApp/MyService занимает слишком много времени, свойство hello является Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="09e49-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="09e49-273">AO роль toohello точек hello именование разделов для этого имени и операции.</span><span class="sxs-lookup"><span data-stu-id="09e49-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="09e49-274">**Дальнейшие действия**: Проверьте причину сбоя hello именование операции.</span><span class="sxs-lookup"><span data-stu-id="09e49-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="09e49-275">Каждая операция может завершаться сбоем по различным причинам.</span><span class="sxs-lookup"><span data-stu-id="09e49-275">Each operation can have different root causes.</span></span> <span data-ttu-id="09e49-276">Например, удаление службы может зависнуть на узле, поскольку ведущее приложение hello отслеживает аварийное завершение работы на узле из-за ошибки пользователя tooa в коде службы hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="09e49-277">Следующий пример Hello показывает операции создания службы.</span><span class="sxs-lookup"><span data-stu-id="09e49-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="09e49-278">Hello занимает дольше времени настройки hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="09e49-279">AO повторных попыток и отправляет tooNO работы.</span><span class="sxs-lookup"><span data-stu-id="09e49-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="09e49-280">Нет завершенных hello последней операции с временем ожидания.</span><span class="sxs-lookup"><span data-stu-id="09e49-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="09e49-281">В этом случае hello же реплики является основной для hello AO и ни одна роль.</span><span class="sxs-lookup"><span data-stu-id="09e49-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="09e49-282">Системные отчеты о работоспособности DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="09e49-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="09e49-283">**System.Hosting** hello центром сертификации для развернутых сущностей.</span><span class="sxs-lookup"><span data-stu-id="09e49-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="09e49-284">Активация</span><span class="sxs-lookup"><span data-stu-id="09e49-284">Activation</span></span>
<span data-ttu-id="09e49-285">System.Hosting отчеты в виде ОК, если приложение успешно активирована на узле hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="09e49-286">В противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="09e49-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="09e49-287">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-288">**Свойство**: активации, включая версию выпуска hello</span><span class="sxs-lookup"><span data-stu-id="09e49-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="09e49-289">**Дальнейшие действия**: Если именно отмечается неработоспособность приложения hello, изучить, почему не удалось активировать hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="09e49-290">Hello ниже приведен пример успешной активации.</span><span class="sxs-lookup"><span data-stu-id="09e49-290">hello following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="09e49-291">Загрузить</span><span class="sxs-lookup"><span data-stu-id="09e49-291">Download</span></span>
<span data-ttu-id="09e49-292">**System.Hosting** сообщает об ошибке в случае сбоя скачивания пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="09e49-293">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-294">**Property**: **Download:*версия_развертывания***</span><span class="sxs-lookup"><span data-stu-id="09e49-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="09e49-295">**Дальнейшие действия**: изучить, почему не удалось загрузить hello на узле hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="09e49-296">Системные отчеты о работоспособности DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="09e49-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="09e49-297">**System.Hosting** hello центром сертификации для развернутых сущностей.</span><span class="sxs-lookup"><span data-stu-id="09e49-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="09e49-298">Активация пакета службы</span><span class="sxs-lookup"><span data-stu-id="09e49-298">Service package activation</span></span>
<span data-ttu-id="09e49-299">System.Hosting отчеты в виде ОК ли hello активации пакета службы на узле hello выполнена.</span><span class="sxs-lookup"><span data-stu-id="09e49-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="09e49-300">В противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="09e49-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="09e49-301">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-302">**Property**: Activation.</span><span class="sxs-lookup"><span data-stu-id="09e49-302">**Property**: Activation</span></span>
* <span data-ttu-id="09e49-303">**Дальнейшие действия**: исследовании причин сбоя активации hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="09e49-304">Активация пакета кода</span><span class="sxs-lookup"><span data-stu-id="09e49-304">Code package activation</span></span>
<span data-ttu-id="09e49-305">**System.Hosting** сообщает как "ОК" для каждого пакета кода при успешной активации hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="09e49-306">В случае сбоя активации hello отображает предупреждение, согласно настройкам.</span><span class="sxs-lookup"><span data-stu-id="09e49-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="09e49-307">Если **CodePackage** сбоя tooactivate или завершается с ошибкой, больше, чем hello настроен **CodePackageHealthErrorThreshold**, размещение сообщает об ошибке.</span><span class="sxs-lookup"><span data-stu-id="09e49-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="09e49-308">Если пакет службы содержит несколько пакетов кода, для каждого из них создается отчет об активации.</span><span class="sxs-lookup"><span data-stu-id="09e49-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="09e49-309">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-310">**Свойство**: префикс hello использует **CodePackageActivation** и содержит имя пакета кода hello и точка входа hello как hello  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (например, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="09e49-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="09e49-311">Регистрация типа службы</span><span class="sxs-lookup"><span data-stu-id="09e49-311">Service type registration</span></span>
<span data-ttu-id="09e49-312">**System.Hosting** сообщает как "ОК", если тип службы hello Регистрация успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="09e49-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="09e49-313">Сообщение об ошибке, если регистрация hello не была выполнена вовремя (согласно настройке с помощью **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="09e49-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="09e49-314">Если среда выполнения hello закрыт, тип службы hello отменяется из узла "hello" и отображает предупреждение, размещения.</span><span class="sxs-lookup"><span data-stu-id="09e49-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="09e49-315">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-316">**Свойство**: префикс hello использует **ServiceTypeRegistration** и содержит имя типа службы hello (например, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="09e49-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="09e49-317">Привет, в следующем примере показан пакет работоспособности развернутой службы:</span><span class="sxs-lookup"><span data-stu-id="09e49-317">hello following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="09e49-318">Загрузить</span><span class="sxs-lookup"><span data-stu-id="09e49-318">Download</span></span>
<span data-ttu-id="09e49-319">**System.Hosting** сообщает об ошибке при сбое загрузки пакета службы hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="09e49-320">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-321">**Property**: **Download:*версия_развертывания***</span><span class="sxs-lookup"><span data-stu-id="09e49-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="09e49-322">**Дальнейшие действия**: изучить, почему не удалось загрузить hello на узле hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="09e49-323">Проверка обновления</span><span class="sxs-lookup"><span data-stu-id="09e49-323">Upgrade validation</span></span>
<span data-ttu-id="09e49-324">**System.Hosting** сообщает об ошибке при сбое проверки во время обновления hello или hello обновление выполняется на узле hello.</span><span class="sxs-lookup"><span data-stu-id="09e49-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="09e49-325">**SourceId**: System.Hosting.</span><span class="sxs-lookup"><span data-stu-id="09e49-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="09e49-326">**Свойство**: префикс hello использует **FabricUpgradeValidation** и содержит версию обновления hello</span><span class="sxs-lookup"><span data-stu-id="09e49-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="09e49-327">**Описание**: произошла ошибка toohello точек</span><span class="sxs-lookup"><span data-stu-id="09e49-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="09e49-328">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09e49-328">Next steps</span></span>
[<span data-ttu-id="09e49-329">Просмотр отчетов о работоспособности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="09e49-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="09e49-330">Как tooreport и проверки службы работоспособности</span><span class="sxs-lookup"><span data-stu-id="09e49-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="09e49-331">Мониторинг и диагностика состояния служб в локальной среде разработки</span><span class="sxs-lookup"><span data-stu-id="09e49-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="09e49-332">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="09e49-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

