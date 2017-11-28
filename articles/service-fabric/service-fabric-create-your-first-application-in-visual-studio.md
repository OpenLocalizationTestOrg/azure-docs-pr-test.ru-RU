---
title: "aaaCreate надежной службы Azure Service Fabric с помощью C#"
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
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="51d39-103">Создание первого приложения надежных служб Service Fabric с отслеживанием состояния на C#</span><span class="sxs-lookup"><span data-stu-id="51d39-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="51d39-104">Узнайте, как toodeploy первого приложения Service Fabric для .NET в Windows через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="51d39-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="51d39-105">По завершении у вас будет локальный кластер, выполняющийся с приложением надежной службы.</span><span class="sxs-lookup"><span data-stu-id="51d39-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51d39-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="51d39-106">Prerequisites</span></span>

<span data-ttu-id="51d39-107">Перед началом работы [настройте среду разработки](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="51d39-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="51d39-108">Сюда входит установка hello Service Fabric SDK и Visual Studio 2017 г. или 2015.</span><span class="sxs-lookup"><span data-stu-id="51d39-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="51d39-109">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="51d39-109">Create hello application</span></span>

<span data-ttu-id="51d39-110">Запустите Visual Studio от имени **администратора**.</span><span class="sxs-lookup"><span data-stu-id="51d39-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="51d39-111">Создайте проект, нажав клавиши `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="51d39-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="51d39-112">В hello **новый проект** диалоговое окно, выберите **облака > приложение Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="51d39-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="51d39-113">Имя приложения hello **MyApplication** и нажмите клавишу **ОК**.</span><span class="sxs-lookup"><span data-stu-id="51d39-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Диалоговое окно "Новый проект" в Visual Studio][1]

<span data-ttu-id="51d39-115">В следующем диалоговом окне приветствия, можно создать любой тип приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="51d39-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="51d39-116">В рамках этого краткого руководства выберите **Служба с отслеживанием состояния**.</span><span class="sxs-lookup"><span data-stu-id="51d39-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="51d39-117">Имя службы hello **MyStatefulService** и нажмите клавишу **ОК**.</span><span class="sxs-lookup"><span data-stu-id="51d39-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Диалоговое окно "Новая служба" в Visual Studio][2]


<span data-ttu-id="51d39-119">Visual Studio создает проект приложения hello и проект службы с отслеживанием состояния hello и отображает их в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="51d39-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Обозреватель решений после создания приложения и службы с отслеживанием состояния][3]

<span data-ttu-id="51d39-121">проект приложения Hello (**MyApplication**) содержит код напрямую.</span><span class="sxs-lookup"><span data-stu-id="51d39-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="51d39-122">Он только ссылается на набор проектов служб.</span><span class="sxs-lookup"><span data-stu-id="51d39-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="51d39-123">Также он содержит данные еще трех типов.</span><span class="sxs-lookup"><span data-stu-id="51d39-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="51d39-124">**Профили публикации**</span><span class="sxs-lookup"><span data-stu-id="51d39-124">**Publish profiles**</span></span>  
<span data-ttu-id="51d39-125">Развертывание сред toodifferent профилей.</span><span class="sxs-lookup"><span data-stu-id="51d39-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="51d39-126">**Сценарии**</span><span class="sxs-lookup"><span data-stu-id="51d39-126">**Scripts**</span></span>  
<span data-ttu-id="51d39-127">Сценарий PowerShell для развертывания и обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="51d39-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="51d39-128">**Определение приложения**</span><span class="sxs-lookup"><span data-stu-id="51d39-128">**Application definition**</span></span>  
<span data-ttu-id="51d39-129">Включает файл ApplicationManifest.xml hello под *ApplicationPackageRoot* описывающей композиции вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="51d39-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="51d39-130">Файлы параметров связанного приложения находятся в *ApplicationParameters*, который может быть toospecify используемые параметры, относящиеся к среде.</span><span class="sxs-lookup"><span data-stu-id="51d39-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="51d39-131">Профиль публикации Visual Studio выбирает, связанный файл параметров приложения, который указан в hello во время развертывания tooa конкретной среды.</span><span class="sxs-lookup"><span data-stu-id="51d39-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="51d39-132">Общие сведения о hello содержимое проекта службы hello. в разделе [Приступая к работе с надежного обмена](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="51d39-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="51d39-133">Развернуть и отладить приложение hello</span><span class="sxs-lookup"><span data-stu-id="51d39-133">Deploy and debug hello application</span></span>

<span data-ttu-id="51d39-134">Теперь, когда вы создали приложение, запустите его.</span><span class="sxs-lookup"><span data-stu-id="51d39-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="51d39-135">В Visual Studio нажмите клавишу `F5` toodeploy hello приложения для отладки.</span><span class="sxs-lookup"><span data-stu-id="51d39-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="51d39-136">Hello в первый раз запустить и развернуть hello приложения локально, Visual Studio создает локального кластера для отладки.</span><span class="sxs-lookup"><span data-stu-id="51d39-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="51d39-137">Это может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="51d39-137">This may take some time.</span></span> <span data-ttu-id="51d39-138">Состояние создания кластера Hello отображается в окне вывода Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="51d39-139">При hello кластера будет готово, вы получите уведомление из hello локального кластера приложения области уведомлений диспетчера входящий в состав пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Уведомление в области уведомлений локального кластера][4]

<span data-ttu-id="51d39-141">После запуска приложения hello, Visual Studio автоматически выбирает hello **средство просмотра событий диагностики**, где можно просмотреть выходные данные трассировки из служб.</span><span class="sxs-lookup"><span data-stu-id="51d39-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Средство просмотра диагностических событий][5]

<span data-ttu-id="51d39-143">Hello шаблона службы с отслеживанием состояния, мы использовали просто показывает, увеличение значения счетчика в hello `RunAsync` метод **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="51d39-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="51d39-144">Разверните одну из события toosee hello сведения, включая узел hello, где выполняется код hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="51d39-145">В данном случае это \_Узел 2\_, хотя на вашем компьютере это может быть другой узел.</span><span class="sxs-lookup"><span data-stu-id="51d39-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Подробная информация в средстве просмотра диагностических событий][6]

<span data-ttu-id="51d39-147">локальный кластер Hello содержит пять узлов, размещенных на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="51d39-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="51d39-148">В рабочей среде каждый узел размещается на различных физических или виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="51d39-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="51d39-149">отладчик потери hello toosimulate машины во время выполнения hello Visual Studio в hello же время, давайте вниз по одному из узлов hello hello локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="51d39-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="51d39-150">В hello **обозревателе решений** откройте **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="51d39-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="51d39-151">Найти hello `RunAsync` метод и задайте точки останова на первой строке метода hello hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Точка останова в методе RunAsync службы с отслеживанием состояния][7]

<span data-ttu-id="51d39-153">Запустите hello **Service Fabric Explorer** инструмент, щелкнув hello **локального кластера диспетчера** приложения области уведомлений и выберите **управление локального кластера**.</span><span class="sxs-lookup"><span data-stu-id="51d39-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Запустите обозреватель Service Fabric из локального кластера диспетчера hello][systray-launch-sfx]

<span data-ttu-id="51d39-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) обеспечивает визуальное представление кластера.</span><span class="sxs-lookup"><span data-stu-id="51d39-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="51d39-156">Содержит набор приложений, развернутых tooit hello и физические узлы, входящие в состав набора hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="51d39-157">В левой области hello, разверните **кластера > узлы** и найти hello узел, где выполняется ваш код.</span><span class="sxs-lookup"><span data-stu-id="51d39-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="51d39-158">Нажмите кнопку **действия > деактивировать (перезапустите)** toosimulate перезапуска компьютера.</span><span class="sxs-lookup"><span data-stu-id="51d39-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Остановка узла в обозревателе Service Fabric][sfx-stop-node]

<span data-ttu-id="51d39-160">Сразу же увидите точка останова попадать в Visual Studio, как вы делали на одном узле, легко вычисление hello при сбое tooanother.</span><span class="sxs-lookup"><span data-stu-id="51d39-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="51d39-161">Затем возвращают toohello диагностические средства просмотра событий и просмотрите сообщения приветствия.</span><span class="sxs-lookup"><span data-stu-id="51d39-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="51d39-162">Счетчик Hello возобновлена увеличения, несмотря на то, что фактически поступления событий hello с другого узла.</span><span class="sxs-lookup"><span data-stu-id="51d39-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Информация в средстве просмотра диагностических событий после аварийного переключения][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="51d39-164">Очистка hello локального кластера (необязательно)</span><span class="sxs-lookup"><span data-stu-id="51d39-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="51d39-165">Помните, что этот локальный кластер работает по-настоящему.</span><span class="sxs-lookup"><span data-stu-id="51d39-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="51d39-166">Остановка отладчика hello удаляет экземпляр приложения и Отмена регистрации типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="51d39-167">Однако hello кластер продолжает toorun в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="51d39-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="51d39-168">Когда вы будете готовы toostop hello локального кластера, существует несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="51d39-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="51d39-169">Хранение приложения и трассировка данных</span><span class="sxs-lookup"><span data-stu-id="51d39-169">Keep application and trace data</span></span>

<span data-ttu-id="51d39-170">Завершите работу кластера, hello, щелкнув hello **локального кластера диспетчера** приложения области уведомлений и выберите **остановить локальный кластер**.</span><span class="sxs-lookup"><span data-stu-id="51d39-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="51d39-171">Удаление кластера hello и все данные</span><span class="sxs-lookup"><span data-stu-id="51d39-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="51d39-172">Удаление кластера hello, щелкнув hello **локального кластера диспетчера** приложения области уведомлений и выберите **удалить локальный кластер**.</span><span class="sxs-lookup"><span data-stu-id="51d39-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="51d39-173">Если этот параметр выбран, Visual Studio будет повторное развертывание кластера hello hello очередном запуске hello приложения.</span><span class="sxs-lookup"><span data-stu-id="51d39-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="51d39-174">Выберите этот параметр, если не планируется, локального кластера hello toouse некоторое время или при необходимости tooreclaim ресурсов.</span><span class="sxs-lookup"><span data-stu-id="51d39-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51d39-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51d39-175">Next steps</span></span>
<span data-ttu-id="51d39-176">Дополнительные сведения о [надежных службах](service-fabric-reliable-services-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="51d39-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
