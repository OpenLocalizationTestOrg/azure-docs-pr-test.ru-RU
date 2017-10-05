---
title: "Создание надежной службы Azure Service Fabric с помощью C#"
description: "Создание, развертывание и отладка приложения надежной службы, созданного в Service Fabric с помощью Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="d5b9b-103">Создание первого приложения надежных служб Service Fabric с отслеживанием состояния на C#</span><span class="sxs-lookup"><span data-stu-id="d5b9b-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="d5b9b-104">Узнайте, как развертывать приложение Service Fabric для .NET в Windows за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="d5b9b-105">По завершении у вас будет локальный кластер, выполняющийся с приложением надежной службы.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5b9b-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d5b9b-106">Prerequisites</span></span>

<span data-ttu-id="d5b9b-107">Перед началом работы [настройте среду разработки](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5b9b-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="d5b9b-108">Это включает установку пакета SDK для Service Fabric и Visual Studio 2017 или 2015.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="d5b9b-109">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="d5b9b-109">Create the application</span></span>

<span data-ttu-id="d5b9b-110">Запустите Visual Studio от имени **администратора**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="d5b9b-111">Создайте проект, нажав клавиши `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="d5b9b-112">В диалоговом окне **Создать проект** выберите **Облако > Приложение Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="d5b9b-113">Укажите имя приложения **MyApplication** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Диалоговое окно "Новый проект" в Visual Studio][1]

<span data-ttu-id="d5b9b-115">Вы можете создать любой тип приложения Service Fabric из следующего диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="d5b9b-116">В рамках этого краткого руководства выберите **Служба с отслеживанием состояния**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="d5b9b-117">Присвойте службе имя **MyStatefulService** и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Диалоговое окно "Новая служба" в Visual Studio][2]


<span data-ttu-id="d5b9b-119">Visual Studio создаст проект приложения и проект службы с отслеживанием состояния, затем отобразит их в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![Обозреватель решений после создания приложения и службы с отслеживанием состояния][3]

<span data-ttu-id="d5b9b-121">Проект приложения (**MyApplication**) не содержит никакой код.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="d5b9b-122">Он только ссылается на набор проектов служб.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="d5b9b-123">Также он содержит данные еще трех типов.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="d5b9b-124">**Профили публикации**</span><span class="sxs-lookup"><span data-stu-id="d5b9b-124">**Publish profiles**</span></span>  
<span data-ttu-id="d5b9b-125">Профили для развертывания в различных средах.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="d5b9b-126">**Сценарии**</span><span class="sxs-lookup"><span data-stu-id="d5b9b-126">**Scripts**</span></span>  
<span data-ttu-id="d5b9b-127">Сценарий PowerShell для развертывания и обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="d5b9b-128">**Определение приложения**</span><span class="sxs-lookup"><span data-stu-id="d5b9b-128">**Application definition**</span></span>  
<span data-ttu-id="d5b9b-129">Включает файл ApplicationManifest.xml в *ApplicationPackageRoot*, описывающей композицию приложения.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="d5b9b-130">Связанные файлы параметров приложения расположены в разделе *ApplicationParameters*, которые можно использовать для указания параметров среды.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="d5b9b-131">Visual Studio выбирает файл параметров приложения, который указан в связанном профиле публикации во время развертывания в определенную среду.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="d5b9b-132">Обзор содержимого проекта службы вы найдете в статье [Начало работы со службами Reliable Services в Service Fabric](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="d5b9b-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="d5b9b-133">Развертывание и отладка приложения</span><span class="sxs-lookup"><span data-stu-id="d5b9b-133">Deploy and debug the application</span></span>

<span data-ttu-id="d5b9b-134">Теперь, когда вы создали приложение, запустите его.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="d5b9b-135">Чтобы начать отладку, разверните приложение, нажав в Visual Studio клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="d5b9b-136">Во время первого запуска и развертывания приложения локально Visual Studio создает локальный кластер для отладки.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="d5b9b-137">Это может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-137">This may take some time.</span></span> <span data-ttu-id="d5b9b-138">Процесс создания кластера можно наблюдать в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="d5b9b-139">Когда кластер будет готов, вы получите уведомление от приложения диспетчера области уведомлений локального кластера, которое входит в состав пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![Уведомление в области уведомлений локального кластера][4]

<span data-ttu-id="d5b9b-141">Когда приложение будет запущено, Visual Studio автоматически откроет **средство просмотра событий диагностики**, в котором отображаются данные трассировки службы.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Средство просмотра диагностических событий][5]

<span data-ttu-id="d5b9b-143">Шаблон службы с отслеживанием состояния, который мы использовали, содержит только значение счетчика, которое увеличивается в методе `RunAsync` файла **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="d5b9b-144">Разверните одно из событий для получения дополнительных сведений, в том числе об узле, где выполняется код.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="d5b9b-145">В данном случае это \_Узел 2\_, хотя на вашем компьютере это может быть другой узел.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Подробная информация в средстве просмотра диагностических событий][6]

<span data-ttu-id="d5b9b-147">Локальный кластер содержит пять узлов, размещенных на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="d5b9b-148">В рабочей среде каждый узел размещается на различных физических или виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="d5b9b-149">Чтобы потренироваться использовать отладчик Visual Studio, имитировав потерю связи с машиной, можно отключить один из узлов локального кластера.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="d5b9b-150">В окне **Обозреватель решений** откройте **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="d5b9b-151">Найдите метод `RunAsync` и установите точку остановки в первой строке метода.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![Точка останова в методе RunAsync службы с отслеживанием состояния][7]

<span data-ttu-id="d5b9b-153">Запустите средство **Service Fabric Explorer**, щелкнув правой кнопкой мыши область уведомлений **диспетчера локального кластера** и выберите пункт **Manage Local Cluster** (Управление локальным кластером).</span><span class="sxs-lookup"><span data-stu-id="d5b9b-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Запуск обозревателя Service Fabric из диспетчера локального кластера][systray-launch-sfx]

<span data-ttu-id="d5b9b-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) обеспечивает визуальное представление кластера.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="d5b9b-156">Он включает в себя набор приложений, развернутых в нем, а также набор физических узлов, обеспечивающих их работу.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="d5b9b-157">В области слева разверните **Кластер > Узлы** и найдите узел, в котором выполняется код приложения.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="d5b9b-158">Щелкните **Действия > Отключить (перезапустить)** для имитации перезапуска компьютера.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![Остановка узла в обозревателе Service Fabric][sfx-stop-node]

<span data-ttu-id="d5b9b-160">Вы сразу же увидите срабатывание точки останова в Visual Studio. Это означает, что процесс вычислений с отключенного узла передан на другой узел как единое целое.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="d5b9b-161">Затем вернитесь к средству просмотра диагностических событий и изучите сообщения.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="d5b9b-162">Показания счетчика продолжают расти, хотя события теперь поступают с другого узла.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![Информация в средстве просмотра диагностических событий после аварийного переключения][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="d5b9b-164">Очистка локального кластера (необязательно)</span><span class="sxs-lookup"><span data-stu-id="d5b9b-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="d5b9b-165">Помните, что этот локальный кластер работает по-настоящему.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="d5b9b-166">Если остановить работу отладчика, будет удален экземпляр приложения и отменена регистрация типа приложения.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="d5b9b-167">Однако кластер при этом будет работать в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="d5b9b-168">Когда вы захотите остановить локальный кластер, имеется несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="d5b9b-169">Хранение приложения и трассировка данных</span><span class="sxs-lookup"><span data-stu-id="d5b9b-169">Keep application and trace data</span></span>

<span data-ttu-id="d5b9b-170">Завершите работу кластера, щелкнув правой кнопкой мыши область уведомлений **диспетчера локального кластера** и выберите пункт **Stop Local Cluster** (Остановить локальный кластер).</span><span class="sxs-lookup"><span data-stu-id="d5b9b-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="d5b9b-171">Удаление кластера и всех данных</span><span class="sxs-lookup"><span data-stu-id="d5b9b-171">Delete the cluster and all data</span></span>

<span data-ttu-id="d5b9b-172">Удалите кластер, щелкнув правой кнопкой мыши область уведомлений **диспетчера локального кластера** и выберите пункт **Remove Local Cluster** (Удалить локальный кластер).</span><span class="sxs-lookup"><span data-stu-id="d5b9b-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="d5b9b-173">Если этот параметр выбран, Visual Studio повторно развернет кластер во время следующего запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="d5b9b-174">Выбирайте этот вариант, только если вы не собираетесь использовать его в течение некоторого времени или вам нужно освободить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d5b9b-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5b9b-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5b9b-175">Next steps</span></span>
<span data-ttu-id="d5b9b-176">Дополнительные сведения о [надежных службах](service-fabric-reliable-services-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d5b9b-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
