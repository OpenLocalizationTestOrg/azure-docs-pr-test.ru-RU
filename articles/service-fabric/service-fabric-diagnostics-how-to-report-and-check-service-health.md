---
title: "aaaReport и проверьте состояние работоспособности с помощью Azure Service Fabric | Документы Microsoft"
description: "Узнайте, как отчеты о работоспособности toosend в коде службы и как предоставляет toocheck hello работоспособности службы с помощью средств наблюдения за работоспособностью hello, Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="11c62-103">Проверка работоспособности службы и оповещение о проблемах</span><span class="sxs-lookup"><span data-stu-id="11c62-103">Report and check service health</span></span>
<span data-ttu-id="11c62-104">При служб возникли проблемы, возможность toorespond tooand исправление инцидентов и простоям зависит от ваших проблем hello toodetect возможность быстро.</span><span class="sxs-lookup"><span data-stu-id="11c62-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="11c62-105">Если проблем и ошибок диспетчера работоспособности Azure Service Fabric toohello отчет из кода службы, можно использовать стандартный работоспособности, Service Fabric предоставляет состояние работоспособности hello toocheck средства мониторинга.</span><span class="sxs-lookup"><span data-stu-id="11c62-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="11c62-106">Можно сообщить работоспособности из службы hello тремя способами:</span><span class="sxs-lookup"><span data-stu-id="11c62-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="11c62-107">С помощью объектов [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) или [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="11c62-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="11c62-108">Можно использовать hello `Partition` и `CodePackageActivationContext` объектов работоспособности hello tooreport элементов, которые являются частью hello текущего контекста.</span><span class="sxs-lookup"><span data-stu-id="11c62-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="11c62-109">Например код, выполняемый в рамках реплики может включать в отчет работоспособности только этой реплики, hello секции, к которому принадлежит и приложения hello, он является частью.</span><span class="sxs-lookup"><span data-stu-id="11c62-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="11c62-110">C помощью `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="11c62-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="11c62-111">Можно использовать `FabricClient` tooreport работоспособности из кода службы hello, если кластер hello не [безопасного](service-fabric-cluster-security.md) или если hello служба запущена с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="11c62-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="11c62-112">В большинстве реальных сценариев не используются незащищенные кластеры и не предоставляются права администратора.</span><span class="sxs-lookup"><span data-stu-id="11c62-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="11c62-113">С `FabricClient`, можно создать отчет по любой сущности, который является частью кластера hello работоспособности.</span><span class="sxs-lookup"><span data-stu-id="11c62-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="11c62-114">В идеале тем не менее, код службы следует отправлять только отчеты, связанные tooits собственные работоспособности.</span><span class="sxs-lookup"><span data-stu-id="11c62-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="11c62-115">Используйте hello API-интерфейс REST в кластер hello, приложения, развернутого приложения, службы, пакет службы, секции, реплики или уровней узлов.</span><span class="sxs-lookup"><span data-stu-id="11c62-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="11c62-116">Это может быть работоспособности используется tooreport из контейнера.</span><span class="sxs-lookup"><span data-stu-id="11c62-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="11c62-117">В этой статье описывается пример, в котором сообщает о работоспособности из кода службы hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="11c62-118">Hello примере также показано, как можно hello средств, предоставляемых Service Fabric состояние работоспособности используется toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="11c62-119">В этой статье является предполагаемым toobe состояния toohello Краткое введение возможности Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="11c62-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="11c62-120">Для получения дополнительных сведений можно считывать hello наборы подробные статьи о работоспособности, начинающиеся со ссылкой hello в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="11c62-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11c62-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="11c62-121">Prerequisites</span></span>
<span data-ttu-id="11c62-122">Необходимо иметь hello установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="11c62-122">You must have hello following installed:</span></span>

* <span data-ttu-id="11c62-123">Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="11c62-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="11c62-124">Пакет SDK для Service Fabric</span><span class="sxs-lookup"><span data-stu-id="11c62-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="11c62-125">toocreate локальной разработки безопасного кластера</span><span class="sxs-lookup"><span data-stu-id="11c62-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="11c62-126">Откройте PowerShell с правами администратора и выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="11c62-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Команды где показано, как toocreate кластера безопасной разработки.](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="11c62-128">toodeploy приложение и проверить его работоспособность.</span><span class="sxs-lookup"><span data-stu-id="11c62-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="11c62-129">Откройте Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="11c62-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="11c62-130">Создание проекта с помощью hello **службы с отслеживанием состояния** шаблона.</span><span class="sxs-lookup"><span data-stu-id="11c62-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Создание приложения Service Fabric со службами с отслеживанием состояния](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="11c62-132">Нажмите клавишу **F5** toorun приложения hello в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="11c62-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="11c62-133">приложение Hello — развернутой toohello локального кластера.</span><span class="sxs-lookup"><span data-stu-id="11c62-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="11c62-134">После запуска приложения hello, щелкните правой кнопкой мыши значок локального кластера диспетчера hello в области уведомлений hello и выберите **управление локального кластера** из hello контекстное меню tooopen Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="11c62-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Открытие обозревателя Service Fabric из области уведомлений](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="11c62-136">работоспособность приложения Hello должен отображаться как в этот образ.</span><span class="sxs-lookup"><span data-stu-id="11c62-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="11c62-137">В настоящее время должно быть приложение hello работоспособное без ошибок.</span><span class="sxs-lookup"><span data-stu-id="11c62-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Работоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="11c62-139">Вы также можете проверить исправность hello с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11c62-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="11c62-140">Можно использовать ```Get-ServiceFabricApplicationHealth``` toocheck работоспособности приложения и могут использовать ```Get-ServiceFabricServiceHealth``` toocheck работоспособности службы.</span><span class="sxs-lookup"><span data-stu-id="11c62-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="11c62-141">Здравствуйте, отчет о работоспособности для hello наличие одного приложения в PowerShell в этот образ.</span><span class="sxs-lookup"><span data-stu-id="11c62-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Работоспособное приложение в PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="11c62-143">код службы tooyour события работоспособности пользовательские tooadd</span><span class="sxs-lookup"><span data-stu-id="11c62-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="11c62-144">шаблоны проектов Service Fabric Hello в Visual Studio содержится пример кода.</span><span class="sxs-lookup"><span data-stu-id="11c62-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="11c62-145">Hello следующие шаги показывают, как сообщать работоспособности пользовательские события из кода службы.</span><span class="sxs-lookup"><span data-stu-id="11c62-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="11c62-146">Такие отчеты отображаются автоматически в hello стандартные средства для мониторинга, Service Fabric предоставляет, такие как обозреватель Service Fabric, представление работоспособности Azure портала и PowerShell состояния.</span><span class="sxs-lookup"><span data-stu-id="11c62-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="11c62-147">Снова откройте приложение hello, созданную ранее в Visual Studio или создайте новое приложение с помощью hello **службы с отслеживанием состояния** шаблона Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11c62-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="11c62-148">Откройте файл Stateful1.cs hello и найти hello `myDictionary.TryGetValueAsync` вызов в hello `RunAsync` метод.</span><span class="sxs-lookup"><span data-stu-id="11c62-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="11c62-149">Вы увидите, что этот метод возвращает `result` , содержит hello текущее значение счетчика "hello", так как логика ключа hello в этом приложении tookeep текущее число.</span><span class="sxs-lookup"><span data-stu-id="11c62-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="11c62-150">Если бы это было реальном приложении и отсутствие hello результат представлен сбоя, необходимо tooflag этого события.</span><span class="sxs-lookup"><span data-stu-id="11c62-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="11c62-151">tooreport событие работоспособности при hello отсутствие результат представляет сбой, добавить hello, следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="11c62-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="11c62-152">а.</span><span class="sxs-lookup"><span data-stu-id="11c62-152">a.</span></span> <span data-ttu-id="11c62-153">Добавить hello `System.Fabric.Health` Stateful1.cs toohello имен файла.</span><span class="sxs-lookup"><span data-stu-id="11c62-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="11c62-154">b.</span><span class="sxs-lookup"><span data-stu-id="11c62-154">b.</span></span> <span data-ttu-id="11c62-155">Добавьте следующий код после hello hello `myDictionary.TryGetValueAsync` вызова</span><span class="sxs-lookup"><span data-stu-id="11c62-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="11c62-156">Мы сообщаем о работоспособности реплики, так как сообщение приходит от службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="11c62-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="11c62-157">Hello `HealthInformation` параметр сохраняет сведения о hello неполадку, которая сообщается.</span><span class="sxs-lookup"><span data-stu-id="11c62-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="11c62-158">Если вы создавали службы без отслеживания состояния, используйте после кода hello</span><span class="sxs-lookup"><span data-stu-id="11c62-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="11c62-159">Если служба запущена с правами администратора или если hello кластера не [безопасного](service-fabric-cluster-security.md), можно также использовать `FabricClient` tooreport работоспособности, как показано в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="11c62-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="11c62-160">а.</span><span class="sxs-lookup"><span data-stu-id="11c62-160">a.</span></span> <span data-ttu-id="11c62-161">Создать hello `FabricClient` экземпляра после hello `var myDictionary` объявления.</span><span class="sxs-lookup"><span data-stu-id="11c62-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="11c62-162">b.</span><span class="sxs-lookup"><span data-stu-id="11c62-162">b.</span></span> <span data-ttu-id="11c62-163">Добавьте следующий код после hello hello `myDictionary.TryGetValueAsync` вызова.</span><span class="sxs-lookup"><span data-stu-id="11c62-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="11c62-164">Давайте имитировать этот сбой и отобразится в средств мониторинга работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="11c62-165">Сбой toosimulate hello, закомментируйте hello первой строки в код, добавленный ранее отчетности работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="11c62-166">После закомментируйте первую строку hello, hello код будет выглядеть как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="11c62-167">Этот код запускается каждый раз при отчет о работоспособности hello `RunAsync` выполняет.</span><span class="sxs-lookup"><span data-stu-id="11c62-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="11c62-168">После внесения изменения hello, нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="11c62-169">После запуска приложения hello, откройте обозреватель Service Fabric toocheck hello работоспособности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="11c62-170">На этот раз обозреватель Service Fabric показывает, что приложение hello неработоспособен.</span><span class="sxs-lookup"><span data-stu-id="11c62-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="11c62-171">Это из-за ошибки hello, произошедшая из кода hello, добавленный ранее.</span><span class="sxs-lookup"><span data-stu-id="11c62-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Неработоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="11c62-173">При выборе в представлении дерева hello Service Fabric Explorer hello первичной реплики, вы увидите, что **состояние работоспособности** слишком указывает на ошибку.</span><span class="sxs-lookup"><span data-stu-id="11c62-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="11c62-174">Обозреватель Service Fabric также отображает сведения, которые были добавлены toohello отчет о работоспособности hello `HealthInformation` параметра в коде hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="11c62-175">Вы увидите hello же отчеты о работоспособности в PowerShell и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="11c62-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Работоспособность реплики в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="11c62-177">В этом отчете остается в диспетчере работоспособности hello, пока не будет заменена другой отчет или пока не будет удалена эта реплика.</span><span class="sxs-lookup"><span data-stu-id="11c62-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="11c62-178">Так как мы не задали `TimeToLive` отчета о работоспособности в hello `HealthInformation` объекта hello отчетов никогда не истекает.</span><span class="sxs-lookup"><span data-stu-id="11c62-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="11c62-179">Корпорация Майкрософт рекомендует работоспособности, должна быть представлена на самом детальном уровне hello, который в данном случае является репликой hello.</span><span class="sxs-lookup"><span data-stu-id="11c62-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="11c62-180">Вы также можете создавать отчеты о работоспособности о `Partition`.</span><span class="sxs-lookup"><span data-stu-id="11c62-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="11c62-181">состояние tooreport на `Application`, `DeployedApplication`, и `DeployedServicePackage`, используйте `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="11c62-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="11c62-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11c62-182">Next steps</span></span>
* [<span data-ttu-id="11c62-183">Подробный обзор работоспособности в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="11c62-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* <span data-ttu-id="11c62-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (REST API для формирования отчетов о работоспособности службы)</span><span class="sxs-lookup"><span data-stu-id="11c62-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)</span></span>
* <span data-ttu-id="11c62-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (REST API для формирования отчетов о работоспособности приложения)</span><span class="sxs-lookup"><span data-stu-id="11c62-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)</span></span>

