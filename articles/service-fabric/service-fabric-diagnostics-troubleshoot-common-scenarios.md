---
title: "aaaTroubleshooting с трассировкой событий | Документы Microsoft"
description: "Hello наиболее распространенных неполадок, возникающих при развертывании службы в Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="02ec5-103">Устранение распространенных проблем при развертывании служб в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="02ec5-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="02ec5-104">При запуске службы на компьютере разработчика, это просто toouse [средств отладки Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="02ec5-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="02ec5-105">Для удаленных кластеров [отчеты о работоспособности](service-fabric-view-entities-aggregated-health.md) всегда являются toostart лучше всего.</span><span class="sxs-lookup"><span data-stu-id="02ec5-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="02ec5-106">Здравствуйте, простой tooaccess способами, эти отчеты, с помощью PowerShell или [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="02ec5-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="02ec5-107">В этой статье предполагается, что выполняется отладка удаленного кластера и иметь базовое понимание того, как toouse любой из этих средств.</span><span class="sxs-lookup"><span data-stu-id="02ec5-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="02ec5-108">Сбой приложения</span><span class="sxs-lookup"><span data-stu-id="02ec5-108">Application crash</span></span>
<span data-ttu-id="02ec5-109">Hello» секция меньше целевой реплики или числа экземпляров» отчет — это означает, что произошло аварийное завершение службы.</span><span class="sxs-lookup"><span data-stu-id="02ec5-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="02ec5-110">toofind, где произошло аварийное завершение службы занимает немного дополнительного изучения.</span><span class="sxs-lookup"><span data-stu-id="02ec5-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="02ec5-111">Если служба масштабируется, незаменимыми будут тщательно продуманные трассировки.</span><span class="sxs-lookup"><span data-stu-id="02ec5-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="02ec5-112">Мы рекомендуем попробовать [диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md) для сбора этих трассировок и с помощью решения, такие как [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) для просмотра и поиска hello трассировок.</span><span class="sxs-lookup"><span data-stu-id="02ec5-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![Работоспособность секции SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="02ec5-114">Во время инициализации службы или субъекта</span><span class="sxs-lookup"><span data-stu-id="02ec5-114">During service or actor initialization</span></span>
<span data-ttu-id="02ec5-115">Все исключения до инициализации типа hello службы приведет к toocrash процесса hello.</span><span class="sxs-lookup"><span data-stu-id="02ec5-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="02ec5-116">Эти типы сбоев журнал событий приложения hello будут показаны ошибки hello из службы.</span><span class="sxs-lookup"><span data-stu-id="02ec5-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="02ec5-117">Это наиболее распространенных исключения toosee hello до инициализации службы hello.</span><span class="sxs-lookup"><span data-stu-id="02ec5-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="02ec5-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="02ec5-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="02ec5-119">Эта ошибка часто является из-за зависимости между сборками toomissing.</span><span class="sxs-lookup"><span data-stu-id="02ec5-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="02ec5-120">Проверьте свойство CopyLocal hello в Visual Studio или hello глобальный кэш сборок для узла hello.</span><span class="sxs-lookup"><span data-stu-id="02ec5-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="02ec5-121">***System.Runtime.InteropServices.COMException*** *в System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="02ec5-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="02ec5-122">Это означает, что это имя типа зарегистрированную службу hello не соответствует hello манифест службы.</span><span class="sxs-lookup"><span data-stu-id="02ec5-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="02ec5-123">[Диагностика Azure](service-fabric-diagnostics-how-to-setup-wad.md) может быть автоматически настроенного tooupload hello журнал событий приложений для всех узлов.</span><span class="sxs-lookup"><span data-stu-id="02ec5-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="02ec5-124">RunAsync() или OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="02ec5-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="02ec5-125">Если происходит сбой hello во время инициализации hello или запущен зарегистрированную службу типа или субъект, hello исключение будет перехвачено Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="02ec5-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="02ec5-126">Можно просмотреть эти от поставщиков EventSource hello, описанные в hello раздел «Дальнейшие действия».</span><span class="sxs-lookup"><span data-stu-id="02ec5-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02ec5-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02ec5-127">Next steps</span></span>
<span data-ttu-id="02ec5-128">Узнайте больше о существующих видах диагностики, предоставляемых Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="02ec5-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="02ec5-129">Диагностика Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="02ec5-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="02ec5-130">Диагностика Reliable Services</span><span class="sxs-lookup"><span data-stu-id="02ec5-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

