---
title: "aaaDeploy и обновления Azure микрослужбами локально | Документы Microsoft"
description: "Узнайте, как tooset локального кластера Service Fabric, развернуть существующий tooit приложения, а затем обновите приложение."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="e2159-103">Начало развертывания и обновления приложений в локальном кластере</span><span class="sxs-lookup"><span data-stu-id="e2159-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="e2159-104">Hello Azure Service Fabric SDK включает полной локальной среде разработки, можно использовать tooquickly Приступая к работе с развертывания и управления приложениями на локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="e2159-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="e2159-105">В этой статье создания локального кластера, развернуть существующий tooit приложения, а затем обновите данной приложения tooa новой версии, все из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2159-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e2159-106">В этой статье предполагается, что вы уже [настроили среду разработки](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2159-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="e2159-107">Создание локального кластера</span><span class="sxs-lookup"><span data-stu-id="e2159-107">Create a local cluster</span></span>
<span data-ttu-id="e2159-108">Кластер Service Fabric представляет собой набор аппаратных ресурсов, на которых можно развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="e2159-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="e2159-109">Как правило кластер состоит из в любом из пяти toomany тысяч машин.</span><span class="sxs-lookup"><span data-stu-id="e2159-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="e2159-110">Однако hello Service Fabric SDK включает конфигурации кластера, который может выполняться на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e2159-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="e2159-111">Очень важно, что toounderstand, hello локального кластера Service Fabric не эмуляторе или симуляторе.</span><span class="sxs-lookup"><span data-stu-id="e2159-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="e2159-112">Он запускает hello того же кода платформы, который находится на кластеры с несколькими компьютерами.</span><span class="sxs-lookup"><span data-stu-id="e2159-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="e2159-113">Hello единственное отличие заключается в том, что он выполняется hello платформы процессы, которые обычно распределены по пяти машин на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e2159-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="e2159-114">Hello SDK предоставляет два способа tooset локального кластера: Windows PowerShell скрипт и hello локального кластера диспетчера системы значок приложения.</span><span class="sxs-lookup"><span data-stu-id="e2159-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="e2159-115">В этом учебнике мы используем скрипт PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="e2159-116">Если вы уже создали локальный кластер путем развертывания приложения из Visual Studio, можете пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="e2159-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="e2159-117">Откройте новое окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e2159-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="e2159-118">Запустите сценарий установки кластера hello из папки hello SDK:</span><span class="sxs-lookup"><span data-stu-id="e2159-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="e2159-119">Настройка кластера занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e2159-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="e2159-120">После завершения установки вы увидите примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="e2159-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Результат установки кластера][cluster-setup-success]
   
    <span data-ttu-id="e2159-122">Теперь вы находитесь готов tootry развертывание кластера tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="e2159-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="e2159-123">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="e2159-123">Deploy an application</span></span>
<span data-ttu-id="e2159-124">Hello Service Fabric SDK включает широкий набор платформ и средства для создания приложений разработки.</span><span class="sxs-lookup"><span data-stu-id="e2159-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="e2159-125">Если вы заинтересованы в обучении toocreate приложений в Visual Studio. в статье [создание первого приложения Service Fabric в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e2159-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="e2159-126">В этом учебнике, что можно сосредоточиться на аспекты управления hello hello платформы, использование существующего приложения образец для (называемые WordCount): развертывания, наблюдения и обновления.</span><span class="sxs-lookup"><span data-stu-id="e2159-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="e2159-127">Откройте новое окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e2159-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="e2159-128">Импортируйте модуль Service Fabric SDK PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="e2159-129">Создание приложения hello toostore каталога, загрузить и развернуть, например C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="e2159-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="e2159-130">[Загрузка приложения WordCount hello](http://aka.ms/servicefabric-wordcountapp) расположение toohello был создан.</span><span class="sxs-lookup"><span data-stu-id="e2159-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="e2159-131">Примечание: hello браузера Microsoft Edge сохраняет файл hello с *.zip* расширения.</span><span class="sxs-lookup"><span data-stu-id="e2159-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="e2159-132">Измените расширение файла hello слишком*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="e2159-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="e2159-133">Подключение локального кластера toohello:</span><span class="sxs-lookup"><span data-stu-id="e2159-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="e2159-134">Создайте новое приложение с помощью команды развертывания hello SDK с имя и путь пакета приложения toohello.</span><span class="sxs-lookup"><span data-stu-id="e2159-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="e2159-135">Если все пойдет хорошо, вы увидите hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e2159-135">If all goes well, you should see hello following output:</span></span>
   
    ![Развернуть локальный кластер toohello приложения][deploy-app-to-local-cluster]
7. <span data-ttu-id="e2159-137">приложение hello toosee в действии, запустить браузер hello и перехода слишком[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="e2159-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="e2159-138">Вы должны увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="e2159-138">You should see:</span></span>
   
    ![Пользовательский интерфейс развернутого приложения][deployed-app-ui]
   
    <span data-ttu-id="e2159-140">Hello приложения WordCount проста.</span><span class="sxs-lookup"><span data-stu-id="e2159-140">hello WordCount application is simple.</span></span> <span data-ttu-id="e2159-141">Он включает клиентские JavaScript кода toogenerate случайных пяти символов «слов», который затем передаются приложению toohello через веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e2159-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="e2159-142">Службы с отслеживанием состояния отслеживает количество hello подсчетом слов.</span><span class="sxs-lookup"><span data-stu-id="e2159-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="e2159-143">Они разбиваются зависимости hello первый символ слова hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="e2159-144">Можно найти hello исходного кода для приложения WordCount hello в hello [классический Приступая к работе образцы](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="e2159-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="e2159-145">приложение Hello, которое мы развернуто содержит четыре секции.</span><span class="sxs-lookup"><span data-stu-id="e2159-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="e2159-146">Поэтому слова, начинающиеся с буквы A – G хранятся в первом разделе hello, слова, начинающиеся с H до N, хранятся в второй раздел hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="e2159-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="e2159-147">Просмотр сведений о приложении и его состояния</span><span class="sxs-lookup"><span data-stu-id="e2159-147">View application details and status</span></span>
<span data-ttu-id="e2159-148">Теперь, когда мы развернуто приложение hello, давайте взглянем на некоторые сведения о приложении hello в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2159-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="e2159-149">Запрос всех развернутых приложений в кластере hello:</span><span class="sxs-lookup"><span data-stu-id="e2159-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="e2159-150">Предположим, что только вы развернули приложение hello WordCount, появится примерно:</span><span class="sxs-lookup"><span data-stu-id="e2159-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Запрос всех развернутых приложений в PowerShell][ps-getsfapp]
2. <span data-ttu-id="e2159-152">Go toohello следующий уровень, запрашивая hello набор служб, которые включены в приложения WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Список служб для приложения hello в PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="e2159-154">приложение Hello состоит из двух служб, hello фронтальный веб-сервер и службы с отслеживанием состояния hello, управляющего слова hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="e2159-155">Наконец проверьте список секций hello WordCountService:</span><span class="sxs-lookup"><span data-stu-id="e2159-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Просмотр разделов службы hello в PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="e2159-157">Здравствуйте, набор команд, которые вы использовали, как и все команды PowerShell структуры службы, доступные для кластера, вы можете подключиться к локальным или удаленным.</span><span class="sxs-lookup"><span data-stu-id="e2159-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="e2159-158">Для более наглядный способ toointeract с кластером hello, средство hello веб-обозреватель Service Fabric, перейдя по слишком[http://localhost:19080/обозреватель](http://localhost:19080/Explorer) в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Просмотр сведений о приложении в обозревателе Service Fabric][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="e2159-160">toolearn Дополнительные сведения о Service Fabric Explorer. в разделе [визуализация кластера с Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e2159-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="e2159-161">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="e2159-161">Upgrade an application</span></span>
<span data-ttu-id="e2159-162">Service Fabric обеспечивает обновления нет простоев, мониторинг работоспособности hello приложения hello, как происходит откат кластеру hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="e2159-163">Выполните обновление приложения WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="e2159-164">Новая версия приложения hello, теперь Hello подсчитывает только слова, начинающиеся с гласные.</span><span class="sxs-lookup"><span data-stu-id="e2159-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="e2159-165">Как обновление hello разворачивает, мы видим два изменения в поведении приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="e2159-166">Во-первых скорость hello увеличения размера hello count должно медленно, так как подсчитываются меньшее количество слов.</span><span class="sxs-lookup"><span data-stu-id="e2159-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="e2159-167">Во-вторых поскольку hello первая секция содержит два гласные ("A" и "E"), а все остальные разделы содержат только один каждого, число ее со временем запустить toooutpace hello другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="e2159-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="e2159-168">[Загрузить пакет версии 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello местоположения, куда вы загрузили hello версии 1 пакета.</span><span class="sxs-lookup"><span data-stu-id="e2159-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="e2159-169">Вернуть tooyour окно PowerShell и команда hello SDK обновления tooregister hello новой версии в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="e2159-170">Затем перейдите к обновлению hello fabric: / приложения WordCount.</span><span class="sxs-lookup"><span data-stu-id="e2159-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="e2159-171">Вы увидите, что hello следующие выходные данные в PowerShell, что hello обновления начинается.</span><span class="sxs-lookup"><span data-stu-id="e2159-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Ход обновления в PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="e2159-173">Во время обновления hello будет продолжена, может оказаться проще toomonitor его состояние с Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e2159-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="e2159-174">Откройте окно браузера и перейдите слишком[http://localhost:19080/обозреватель](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="e2159-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="e2159-175">Разверните **приложений** в дереве hello hello слева, затем выберите **WordCount**и, наконец, **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="e2159-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="e2159-176">На вкладке essentials hello появится hello состояния обновления hello как проходит доменов обновления кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Ход обновления в обозревателе Service Fabric][sfx-upgradeprogress]
   
    <span data-ttu-id="e2159-178">Как происходит обновление hello через каждый домен, проверки работоспособности, выполненной tooensure правильно написанное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="e2159-179">При повторном запуске hello ранее запрос для набора служб в фабрике hello hello: / приложения WordCount Обратите внимание, что hello WordCountService версии изменены, но hello WordCountWebService версии не:</span><span class="sxs-lookup"><span data-stu-id="e2159-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Запрос служб приложений после обновления][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="e2159-181">Этот пример демонстрирует, как платформа Service Fabric управляет обновлениями: они применяются только к набору служб (либо к пакетам кода или конфигурации в этих службах), которые были изменены.</span><span class="sxs-lookup"><span data-stu-id="e2159-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="e2159-182">Оно касается только hello набор служб (или кода и конфигурации пакетов в пределах этих служб), были ли изменены, что делает hello процесс обновления быстрее и надежнее.</span><span class="sxs-lookup"><span data-stu-id="e2159-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="e2159-183">Наконец возвращают toohello tooobserve браузера hello поведение hello новой версии приложения.</span><span class="sxs-lookup"><span data-stu-id="e2159-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="e2159-184">Как и ожидалось, медленнее hello число по мере того и первая секция hello составляло немного более hello тома.</span><span class="sxs-lookup"><span data-stu-id="e2159-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Представление hello новую версию приложения hello в браузере hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="e2159-186">Очистка.</span><span class="sxs-lookup"><span data-stu-id="e2159-186">Cleaning up</span></span>
<span data-ttu-id="e2159-187">Перед упаковкой, очень важно, tooremember, hello локального кластера является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="e2159-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="e2159-188">Приложения продолжают toorun в фоновом режиме hello, пока вы не удалите их.</span><span class="sxs-lookup"><span data-stu-id="e2159-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="e2159-189">В зависимости от характера приложения hello выполняемого приложения могут занимать значительных ресурсов на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e2159-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="e2159-190">У вас есть несколько вариантов toomanage приложений и hello кластера:</span><span class="sxs-lookup"><span data-stu-id="e2159-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="e2159-191">tooremove отдельного приложения и все его с данными, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2159-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="e2159-192">Или удаление приложения hello из hello Service Fabric Explorer **действия** hello контекстном меню в виде списка в левой части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Удаление приложения в обозревателе Service Fabric][sfe-delete-application]
2. <span data-ttu-id="e2159-194">После удаления приложения hello из кластера hello, отмените регистрацию версии 1.0.0 и 2.0.0 из типа приложения WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="e2159-195">При удалении пакетов приложения hello, включая кода hello и конфигурации из хранилища образов hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e2159-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="e2159-196">Или в обозреватель Service Fabric, выберите **наполнение типа** для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="e2159-197">tooshut вниз hello кластера, но сохранить данные приложения hello и трассировки щелкните **остановить локальный кластер** в значок приложения hello системы.</span><span class="sxs-lookup"><span data-stu-id="e2159-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="e2159-198">кластер hello toodelete целиком, щелкните **удалить локального кластера** в значок приложения hello системы.</span><span class="sxs-lookup"><span data-stu-id="e2159-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="e2159-199">Этот параметр приведет к другой медленной развертывания hello следующий раз при нажатии клавиши F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2159-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="e2159-200">Удаление локального кластера hello только в том случае, если не предполагается toouse некоторое время или если необходимо tooreclaim ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e2159-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="e2159-201">Режимы кластера с одним и с пятью узлами</span><span class="sxs-lookup"><span data-stu-id="e2159-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="e2159-202">При разработке приложений часто бывает необходимо быстро написать, изменить код или выполнить его отладку.</span><span class="sxs-lookup"><span data-stu-id="e2159-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="e2159-203">toohelp оптимизировать этот процесс, hello локального кластера может работать в двух режимах: один узел или узел пяти.</span><span class="sxs-lookup"><span data-stu-id="e2159-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="e2159-204">Каждый из этих режимов имеет свои преимущества.</span><span class="sxs-lookup"><span data-stu-id="e2159-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="e2159-205">Режим пяти узел кластера позволяет toowork с реальными кластера.</span><span class="sxs-lookup"><span data-stu-id="e2159-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="e2159-206">Вы можете тестировать сценарии отработки отказа и работать с несколькими экземплярами и репликами служб.</span><span class="sxs-lookup"><span data-stu-id="e2159-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="e2159-207">Кластер с одним узлом режим — оптимизированный toodo быстрого развертывания и регистрации служб, toohelp быстро проверить код с помощью среды выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e2159-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="e2159-208">Режимы кластера с одним узлом и с пятью узлами не являются эмуляторами или имитаторами.</span><span class="sxs-lookup"><span data-stu-id="e2159-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="e2159-209">Hello локальному кластеру разработки запусков hello того же кода платформы, который находится на кластеры с несколькими компьютерами.</span><span class="sxs-lookup"><span data-stu-id="e2159-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="e2159-210">При изменении режима кластера hello hello текущего кластера удаляется из системы и создается новый кластер.</span><span class="sxs-lookup"><span data-stu-id="e2159-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="e2159-211">Hello данные, хранящиеся в кластере hello удаляется при изменении режима кластера.</span><span class="sxs-lookup"><span data-stu-id="e2159-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="e2159-212">toochange hello режим tooone узел кластера, выберите **Переключите режим кластера** в hello локального кластера Service Fabric диспетчера.</span><span class="sxs-lookup"><span data-stu-id="e2159-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Переключение режима кластера][switch-cluster-mode]

<span data-ttu-id="e2159-214">Или измените режим hello кластера, с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e2159-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="e2159-215">Откройте новое окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e2159-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="e2159-216">Запустите сценарий установки кластера hello из папки hello SDK:</span><span class="sxs-lookup"><span data-stu-id="e2159-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="e2159-217">Настройка кластера занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e2159-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="e2159-218">После завершения установки вы увидите примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="e2159-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Результат установки кластера][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="e2159-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2159-220">Next steps</span></span>
* <span data-ttu-id="e2159-221">Теперь, когда вы развернули и обновили предварительно собранные приложения, вы можете [выполнить сборку своего приложения в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e2159-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="e2159-222">Все hello действия, выполняемые в локальном кластере hello в этой статье может выполняться на [кластера Azure](service-fabric-cluster-creation-via-portal.md) также.</span><span class="sxs-lookup"><span data-stu-id="e2159-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="e2159-223">Обновление Hello, мы выполнили в этой статье был basic.</span><span class="sxs-lookup"><span data-stu-id="e2159-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="e2159-224">В разделе hello [документации по обновлению](service-fabric-application-upgrade.md) toolearn Дополнительные сведения о hello мощность и гибкость обновления Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e2159-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
