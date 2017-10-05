---
title: "Проверка работоспособности и оповещение о проблемах в Azure Service Fabric | Документация Майкрософт"
description: "Узнайте, как отправлять отчеты о работоспособности из кода службы и проверять работоспособность службы с использованием средств наблюдения Azure Service Fabric."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="c6b70-103">Проверка работоспособности службы и оповещение о проблемах</span><span class="sxs-lookup"><span data-stu-id="c6b70-103">Report and check service health</span></span>
<span data-ttu-id="c6b70-104">Если при работе служб возникают проблемы, то возможность ответить на все возникшие инциденты и устранить их зависит от того, насколько быстро вы сможете обнаружить проблему.</span><span class="sxs-lookup"><span data-stu-id="c6b70-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="c6b70-105">Сообщив о проблемах и сбоях диспетчеру работоспособности Azure Service Fabric из кода службы, вы сможете использовать стандартные средства мониторинга работоспособности, которые предоставляет Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c6b70-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="c6b70-106">Существует три способа, с помощью которых служба может сообщить о своей работоспособности:</span><span class="sxs-lookup"><span data-stu-id="c6b70-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="c6b70-107">С помощью объектов [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) или [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="c6b70-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="c6b70-108">Используйте объекты `Partition` и `CodePackageActivationContext`, чтобы сообщить сведения о работоспособности элементов, которые являются частью текущего контекста.</span><span class="sxs-lookup"><span data-stu-id="c6b70-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="c6b70-109">Например, код, выполняемый в рамках реплики, может передать сведения о работоспособности только для этой реплики, раздела, к которому она принадлежит, и приложения, частью которого она является.</span><span class="sxs-lookup"><span data-stu-id="c6b70-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="c6b70-110">C помощью `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="c6b70-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="c6b70-111">`FabricClient` можно использовать для передачи сведений о работоспособности из кода службы в том случае, если кластер не является [безопасным](service-fabric-cluster-security.md) или если служба запущена с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c6b70-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="c6b70-112">В большинстве реальных сценариев не используются незащищенные кластеры и не предоставляются права администратора.</span><span class="sxs-lookup"><span data-stu-id="c6b70-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="c6b70-113">С помощью `FabricClient`можно отправлять сведения о работоспособности для любой сущности, которая является частью кластера.</span><span class="sxs-lookup"><span data-stu-id="c6b70-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="c6b70-114">Но в идеале код службы должен сообщать только о работоспособности самой службы.</span><span class="sxs-lookup"><span data-stu-id="c6b70-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="c6b70-115">Используйте интерфейсы REST API на уровне кластера, приложения, развернутого приложения, службы, пакета службы, секции, реплики или узла.</span><span class="sxs-lookup"><span data-stu-id="c6b70-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="c6b70-116">Так можно сообщить о работоспособности из контейнера.</span><span class="sxs-lookup"><span data-stu-id="c6b70-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="c6b70-117">В этой статье описан пример того, как отправлять отчеты о работоспособности из кода службы.</span><span class="sxs-lookup"><span data-stu-id="c6b70-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="c6b70-118">В примере также показано, как можно использовать инструменты, предоставляемые Service Fabric, для проверки состояния работоспособности.</span><span class="sxs-lookup"><span data-stu-id="c6b70-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="c6b70-119">Эта статья представляет собой краткое изложение возможностей Service Fabric по отслеживанию работоспособности.</span><span class="sxs-lookup"><span data-stu-id="c6b70-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="c6b70-120">Для получения дополнительных сведений вы можете прочесть серию подробных статей о работоспособности, начиная со статьи, ссылка на которую приведена в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c6b70-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6b70-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c6b70-121">Prerequisites</span></span>
<span data-ttu-id="c6b70-122">Должны быть установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="c6b70-122">You must have the following installed:</span></span>

* <span data-ttu-id="c6b70-123">Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6b70-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="c6b70-124">Пакет SDK для Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c6b70-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="c6b70-125">Создание безопасного локального кластера для разработки</span><span class="sxs-lookup"><span data-stu-id="c6b70-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="c6b70-126">Запустите PowerShell с правами администратора и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c6b70-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Команды для создания безопасного кластера для разработки](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="c6b70-128">Развертывание приложения и проверка его работоспособности</span><span class="sxs-lookup"><span data-stu-id="c6b70-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="c6b70-129">Откройте Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c6b70-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="c6b70-130">Создайте проект с помощью шаблона **службы с отслеживанием состояния** .</span><span class="sxs-lookup"><span data-stu-id="c6b70-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Создание приложения Service Fabric со службами с отслеживанием состояния](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="c6b70-132">Нажмите **F5** , чтобы запустить приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="c6b70-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="c6b70-133">Приложение будет развернуто на локальный кластер.</span><span class="sxs-lookup"><span data-stu-id="c6b70-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="c6b70-134">После запуска приложения в области уведомлений щелкните правой кнопкой мыши значок локального диспетчера кластера и выберите в контекстном меню пункт **Управление локальным кластером** , чтобы открыть обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c6b70-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Открытие обозревателя Service Fabric из области уведомлений](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="c6b70-136">Состояние работоспособности приложения должно отображаться, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="c6b70-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="c6b70-137">Приложение должно работать исправно и без ошибок.</span><span class="sxs-lookup"><span data-stu-id="c6b70-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Работоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="c6b70-139">Кроме того, вы можете проверить работоспособность с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6b70-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="c6b70-140">Вы можете использовать команду ```Get-ServiceFabricApplicationHealth``` для проверки работоспособности приложения, а ```Get-ServiceFabricServiceHealth``` — для проверки работоспособности службы.</span><span class="sxs-lookup"><span data-stu-id="c6b70-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="c6b70-141">Отчет о работоспособности для этого же приложения в PowerShell выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6b70-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Работоспособное приложение в PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="c6b70-143">Добавление пользовательских событий работоспособности в код службы</span><span class="sxs-lookup"><span data-stu-id="c6b70-143">To add custom health events to your service code</span></span>
<span data-ttu-id="c6b70-144">В шаблонах проекта Service Fabric в Visual Studio приведен пример кода.</span><span class="sxs-lookup"><span data-stu-id="c6b70-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="c6b70-145">Ниже показано, как сообщить о пользовательских событиях работоспособности из кода службы.</span><span class="sxs-lookup"><span data-stu-id="c6b70-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="c6b70-146">Такие отчеты автоматически появятся в стандартных инструментах для наблюдения за работоспособностью, предоставляемых Service Fabric, таких как Service Fabric Explorer, представление работоспособности на портале Azure и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6b70-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="c6b70-147">Повторно откройте приложение, созданное ранее в Visual Studio, или создайте новое приложение с использованием шаблона **службы с отслеживанием состояния** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6b70-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="c6b70-148">Откройте файл Stateful1.cs и найдите вызов `myDictionary.TryGetValueAsync` в методе `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="c6b70-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="c6b70-149">Как видите, этот метод возвращает `result` , который содержит текущее значение счетчика, так как основная логика этого приложения — поддерживать работу счетчика.</span><span class="sxs-lookup"><span data-stu-id="c6b70-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="c6b70-150">В настоящем приложении, если отсутствие результата означает сбой, необходимо сообщить о нарушении работоспособности.</span><span class="sxs-lookup"><span data-stu-id="c6b70-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="c6b70-151">Чтобы сообщить о событии отсутствия результата, что представляет собой сбой, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c6b70-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="c6b70-152">а.</span><span class="sxs-lookup"><span data-stu-id="c6b70-152">a.</span></span> <span data-ttu-id="c6b70-153">Добавьте в файл Stateful1.cs пространство имен `System.Fabric.Health` .</span><span class="sxs-lookup"><span data-stu-id="c6b70-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="c6b70-154">b.</span><span class="sxs-lookup"><span data-stu-id="c6b70-154">b.</span></span> <span data-ttu-id="c6b70-155">Добавьте приведенный ниже код после вызова `myDictionary.TryGetValueAsync` .</span><span class="sxs-lookup"><span data-stu-id="c6b70-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="c6b70-156">Мы сообщаем о работоспособности реплики, так как сообщение приходит от службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="c6b70-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="c6b70-157">Параметр `HealthInformation` содержит сведения о сообщенной в отчете проблеме с работоспособностью.</span><span class="sxs-lookup"><span data-stu-id="c6b70-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="c6b70-158">Если была создана служба без отслеживания состояния, используйте следующий код.</span><span class="sxs-lookup"><span data-stu-id="c6b70-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="c6b70-159">Если служба запущена с правами администратора или кластер не является [безопасным](service-fabric-cluster-security.md), для отправки сведений о работоспособности также можно использовать `FabricClient`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c6b70-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="c6b70-160">а.</span><span class="sxs-lookup"><span data-stu-id="c6b70-160">a.</span></span> <span data-ttu-id="c6b70-161">Создайте экземпляр `FabricClient` после объявления `var myDictionary`.</span><span class="sxs-lookup"><span data-stu-id="c6b70-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="c6b70-162">b.</span><span class="sxs-lookup"><span data-stu-id="c6b70-162">b.</span></span> <span data-ttu-id="c6b70-163">Добавьте приведенный ниже код после вызова `myDictionary.TryGetValueAsync` .</span><span class="sxs-lookup"><span data-stu-id="c6b70-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="c6b70-164">Давайте сымитируем этот сбой и посмотрим, как он будет отображаться в средствах наблюдения за работоспособностью.</span><span class="sxs-lookup"><span data-stu-id="c6b70-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="c6b70-165">Чтобы сымитировать сбой, закомментируйте первую строку в коде проверки работоспособности, который был добавлен ранее.</span><span class="sxs-lookup"><span data-stu-id="c6b70-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="c6b70-166">После этого код будет выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c6b70-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="c6b70-167">Этот код отправляет отчет о работоспособности при каждом выполнении `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="c6b70-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="c6b70-168">После внесения изменений нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="c6b70-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="c6b70-169">Запустив приложение, откройте обозреватель Service Fabric для проверки работоспособности приложения.</span><span class="sxs-lookup"><span data-stu-id="c6b70-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="c6b70-170">На этот раз Service Fabric Explorer показывает, что работоспособность приложения нарушена.</span><span class="sxs-lookup"><span data-stu-id="c6b70-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="c6b70-171">Это вызвано ошибкой в коде, который мы добавили раньше.</span><span class="sxs-lookup"><span data-stu-id="c6b70-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Неработоспособное приложение в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="c6b70-173">При выборе основной реплики в древовидном представлении обозревателя Service Fabric вы увидите, что в ней также отображается **нарушение работоспособности** .</span><span class="sxs-lookup"><span data-stu-id="c6b70-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="c6b70-174">Кроме того, в обозревателе Service Fabric отображаются подробные сведения о работоспособности, добавленные в параметр `HealthInformation` в коде.</span><span class="sxs-lookup"><span data-stu-id="c6b70-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="c6b70-175">Эти же отчеты о работоспособности можно просмотреть с помощью PowerShell и на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b70-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Работоспособность реплики в обозревателе Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="c6b70-177">Этот отчет останется в диспетчере работоспособности до тех пор, пока не будет заменен другим отчетом или пока эта реплика не будет удалена.</span><span class="sxs-lookup"><span data-stu-id="c6b70-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="c6b70-178">Так как мы не задали параметр `TimeToLive` для этого отчета о работоспособности в объекте `HealthInformation`, срок действия отчета не истечет.</span><span class="sxs-lookup"><span data-stu-id="c6b70-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="c6b70-179">Сведения о работоспособности рекомендуется сообщать на самом детальном уровне. В приведенном выше случае это уровень реплики.</span><span class="sxs-lookup"><span data-stu-id="c6b70-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="c6b70-180">Вы также можете создавать отчеты о работоспособности о `Partition`.</span><span class="sxs-lookup"><span data-stu-id="c6b70-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="c6b70-181">Чтобы создавать отчеты о работоспособности о `Application`, `DeployedApplication` и `DeployedServicePackage`, используйте `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="c6b70-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="c6b70-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6b70-182">Next steps</span></span>
* [<span data-ttu-id="c6b70-183">Подробный обзор работоспособности в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c6b70-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* <span data-ttu-id="c6b70-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service) (REST API для формирования отчетов о работоспособности службы)</span><span class="sxs-lookup"><span data-stu-id="c6b70-184">[REST API for reporting service health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)</span></span>
* <span data-ttu-id="c6b70-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application) (REST API для формирования отчетов о работоспособности приложения)</span><span class="sxs-lookup"><span data-stu-id="c6b70-185">[REST API for reporting application health](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)</span></span>

