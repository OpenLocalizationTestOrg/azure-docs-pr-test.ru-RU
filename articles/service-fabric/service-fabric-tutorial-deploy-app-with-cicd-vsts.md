---
title: "Развертывание приложения Azure Service Fabric с непрерывной интеграцией (Team Services) | Документы Майкрософт"
description: "Общие сведения о том, как настроить непрерывную интеграцию и развертывание для приложения Service Fabric с помощью Visual Studio Team Services.  Разверните приложение в кластере Service Fabric в Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: 631f9794994530092d05a33b06ebf8c07f331649
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-with-cicd-to-a-service-fabric-cluster"></a><span data-ttu-id="a7a89-104">Развертывание приложения с непрерывной интеграцией и развертыванием в кластере Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a7a89-104">Deploy an application with CI/CD to a Service Fabric cluster</span></span>
<span data-ttu-id="a7a89-105">Это руководство из цикла. В нем описано, как настроить непрерывные интеграцию и развертывание для приложения Azure Service Fabric с помощью Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a7a89-105">This tutorial is part three of a series and describes how to set up continuous integration and deployment for an Azure Service Fabric application using Visual Studio Team Services.</span></span>  <span data-ttu-id="a7a89-106">Вам потребуется приложение Service Fabric. В качестве примера используется приложение, созданное в разделе [Создание приложения .NET](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="a7a89-106">An existing Service Fabric application is needed, the application created in [Build a .NET application](service-fabric-tutorial-create-dotnet-app.md) is used as an example.</span></span>

<span data-ttu-id="a7a89-107">В третьей части цикла вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a7a89-107">In part three of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7a89-108">Добавление проекта в систему управления версиями</span><span class="sxs-lookup"><span data-stu-id="a7a89-108">Add source control to your project</span></span>
> * <span data-ttu-id="a7a89-109">Создание определения сборки в Team Services</span><span class="sxs-lookup"><span data-stu-id="a7a89-109">Create a build definition in Team Services</span></span>
> * <span data-ttu-id="a7a89-110">Создание определения выпуска в Team Services</span><span class="sxs-lookup"><span data-stu-id="a7a89-110">Create a release definition in Team Services</span></span>
> * <span data-ttu-id="a7a89-111">Автоматическое развертывание и обновление приложения</span><span class="sxs-lookup"><span data-stu-id="a7a89-111">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="a7a89-112">Из этого цикла руководств вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a7a89-112">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a7a89-113">[Создание приложения .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="a7a89-113">[Build a .NET Service Fabric application](service-fabric-tutorial-create-dotnet-app.md)</span></span>
> * <span data-ttu-id="a7a89-114">[Развертывание приложения в удаленном кластере](service-fabric-tutorial-deploy-app-to-party-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a7a89-114">[Deploy the application to a remote cluster](service-fabric-tutorial-deploy-app-to-party-cluster.md)</span></span>
> * <span data-ttu-id="a7a89-115">Настройка непрерывной интеграции и непрерывного развертывания с помощью Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a7a89-115">Configure CI/CD using Visual Studio Team Services</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7a89-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7a89-116">Prerequisites</span></span>
<span data-ttu-id="a7a89-117">Перед началом работы с этим руководством выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a7a89-117">Before you begin this tutorial:</span></span>
- <span data-ttu-id="a7a89-118">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a7a89-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="a7a89-119">[Установите Visual Studio 2017](https://www.visualstudio.com/), а также рабочие нагрузки **разработка Azure** и **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-119">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="a7a89-120">Установка пакета SDK для Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a7a89-120">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)
- <span data-ttu-id="a7a89-121">Создайте приложение Service Fabric, например с помощью [этого руководства](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="a7a89-121">Create a Service Fabric application, for example by [following this tutorial](service-fabric-tutorial-create-dotnet-app.md).</span></span> 
- <span data-ttu-id="a7a89-122">Создайте кластер Service Fabric с Windows, например с помощью [этого руководства](service-fabric-tutorial-create-cluster-azure-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a7a89-122">Create a Windows Service Fabric cluster on Azure, for example by [following this tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)</span></span>
- <span data-ttu-id="a7a89-123">Создайте [учетную запись Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="a7a89-123">Create a [Team Services account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>

## <a name="download-the-voting-sample-application"></a><span data-ttu-id="a7a89-124">Скачивание примера приложения для голосования</span><span class="sxs-lookup"><span data-stu-id="a7a89-124">Download the Voting sample application</span></span>
<span data-ttu-id="a7a89-125">Если вы не создавали пример приложения для голосования [в первой части этой серии руководств](service-fabric-tutorial-create-dotnet-app.md), вы можете скачать его.</span><span class="sxs-lookup"><span data-stu-id="a7a89-125">If you did not build the Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="a7a89-126">В окне терминала выполните следующую команду, чтобы клонировать репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a7a89-126">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a><span data-ttu-id="a7a89-127">Подготовка профиля публикации</span><span class="sxs-lookup"><span data-stu-id="a7a89-127">Prepare a publish profile</span></span>
<span data-ttu-id="a7a89-128">После [создания приложения](service-fabric-tutorial-create-dotnet-app.md) и [развертывания приложения в Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md) вы можете настроить непрерывную интеграцию.</span><span class="sxs-lookup"><span data-stu-id="a7a89-128">Now that you've [created an application](service-fabric-tutorial-create-dotnet-app.md) and have [deployed the application to Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md), you're ready to set up continuous integration.</span></span>  <span data-ttu-id="a7a89-129">Сначала подготовьте профиль публикации для развертывания приложения в Team Services.</span><span class="sxs-lookup"><span data-stu-id="a7a89-129">First, prepare a publish profile within your application for use by the deployment process that executes within Team Services.</span></span>  <span data-ttu-id="a7a89-130">Профиль публикации следует настроить для целевого кластера, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="a7a89-130">The publish profile should be configured to target the cluster that you've previously created.</span></span>  <span data-ttu-id="a7a89-131">Запустите Visual Studio и откройте существующий проект приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a7a89-131">Start Visual Studio and open an existing Service Fabric application project.</span></span>  <span data-ttu-id="a7a89-132">Щелкните правой кнопкой мыши приложение в **обозревателе решений** и выберите **Опубликовать...**</span><span class="sxs-lookup"><span data-stu-id="a7a89-132">In **Solution Explorer**, right-click the application and select **Publish...**.</span></span>

<span data-ttu-id="a7a89-133">Выберите в проекте приложения целевой профиль, который будет использоваться для рабочего процесса непрерывной интеграции, например "Облако".</span><span class="sxs-lookup"><span data-stu-id="a7a89-133">Choose a target profile within your application project to use for your continuous integration workflow, for example Cloud.</span></span>  <span data-ttu-id="a7a89-134">Укажите конечную точку подключения кластера.</span><span class="sxs-lookup"><span data-stu-id="a7a89-134">Specify the cluster connection endpoint.</span></span>  <span data-ttu-id="a7a89-135">Установите флажок **Обновлять приложение**, чтобы ваше приложение обновлялось при каждом развертывании в Team Services.</span><span class="sxs-lookup"><span data-stu-id="a7a89-135">Check the **Upgrade the Application** checkbox so that your application upgrades for each deployment in Team Services.</span></span>  <span data-ttu-id="a7a89-136">Нажмите ссылку **Сохранить**, чтобы сохранить параметры профиля публикации, а затем нажмите кнопку **Отменить**, чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a7a89-136">Click the **Save** hyperlink to save the settings to the publish profile and then click **Cancel** to close the dialog box.</span></span>  

![Принудительная отправка профиля][publish-app-profile]

## <a name="share-your-visual-studio-solution-to-a-new-team-services-git-repo"></a><span data-ttu-id="a7a89-138">Поделитесь своим решением Visual Studio в новом репозитории Git Team Services</span><span class="sxs-lookup"><span data-stu-id="a7a89-138">Share your Visual Studio solution to a new Team Services Git repo</span></span>
<span data-ttu-id="a7a89-139">Поделитесь исходными файлами приложения в проекте команды в Team Services, чтобы создавать сборки.</span><span class="sxs-lookup"><span data-stu-id="a7a89-139">Share your application source files to a team project in Team Services so you can generate builds.</span></span>  

<span data-ttu-id="a7a89-140">Создайте новый локальный репозиторий Git, выбрав **Добавить в систему управления версиями** -> **Git** в строке состояния в правом нижнем углу Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7a89-140">Create a new local Git repo for your project by selecting **Add to Source Control** -> **Git** on the status bar in the lower right-hand corner of Visual Studio.</span></span> 

<span data-ttu-id="a7a89-141">В представлении **Принудительная отправка** в **Team Explorer** выберите **Опубликовать репозиторий Git** в разделе **Принудительная отправка в Visual Studio Team Services**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-141">In the **Push** view in **Team Explorer**, select the **Publish Git Repo** button under **Push to Visual Studio Team Services**.</span></span>

![Принудительная отправка репозитория Git][push-git-repo]

<span data-ttu-id="a7a89-143">Проверьте почту и выберите свою учетную запись в раскрывающемся списке **Домен Team Services**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-143">Verify your email and select your account in the **Team Services Domain** drop-down.</span></span> <span data-ttu-id="a7a89-144">Введите имя репозитория и выберите **Опубликовать репозиторий**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-144">Enter your repository name and select **Publish repository**.</span></span>

![Принудительная отправка репозитория Git][publish-code]

<span data-ttu-id="a7a89-146">При публикации репозитория в вашей учетной записи создается новый командный проект с тем же именем, что и у локального репозитория.</span><span class="sxs-lookup"><span data-stu-id="a7a89-146">Publishing the repo creates a new team project in your account with the same name as the local repo.</span></span> <span data-ttu-id="a7a89-147">Чтобы создать репозиторий в существующем командном проекте, нажмите кнопку **Дополнительно** рядом с именем **репозитория** и выберите командный проект.</span><span class="sxs-lookup"><span data-stu-id="a7a89-147">To create the repo in an existing team project, click **Advanced** next to **Repository** name and select a team project.</span></span> <span data-ttu-id="a7a89-148">Код можно просматривать в Интернете, выбрав **Просмотреть на веб-сайте**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-148">You can view your code on the web by selecting **See it on the web**.</span></span>

## <a name="configure-continuous-delivery-with-vsts"></a><span data-ttu-id="a7a89-149">Настройка непрерывной поставки с помощью VSTS</span><span class="sxs-lookup"><span data-stu-id="a7a89-149">Configure Continuous Delivery with VSTS</span></span>
<span data-ttu-id="a7a89-150">Определение сборки Team Services описывает рабочий процесс, состоящий из набора шагов сборки, которые выполняются последовательно.</span><span class="sxs-lookup"><span data-stu-id="a7a89-150">A Team Services build definition describes a workflow that is composed of a set of build steps that are executed sequentially.</span></span> <span data-ttu-id="a7a89-151">Создайте определение сборки, который создает пакет приложения Service Fabric и другие артефакты, которые будут развернуты в кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a7a89-151">Create a build definition that that produces a Service Fabric application package, and other artifacts, to deploy to a Service Fabric cluster.</span></span> <span data-ttu-id="a7a89-152">Дополнительные сведения об [определениях сборок Team Services](https://www.visualstudio.com/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="a7a89-152">Learn more about [Team Services build definitions](https://www.visualstudio.com/docs/build/define/create).</span></span> 

<span data-ttu-id="a7a89-153">Определение выпуска Team Services описывает рабочий процесс развертывания пакета приложения в кластере.</span><span class="sxs-lookup"><span data-stu-id="a7a89-153">A Team Services release definition describes a workflow that deploys an application package to a cluster.</span></span> <span data-ttu-id="a7a89-154">При совместном использовании определение сборки и определение выпуска выполняют весь рабочий процесс начиная с исходных файлов и заканчивая запуском приложения в кластере.</span><span class="sxs-lookup"><span data-stu-id="a7a89-154">When used together, the build definition and release definition execute the entire workflow starting with source files to ending with a running application in your cluster.</span></span> <span data-ttu-id="a7a89-155">Узнайте больше об [определениях выпуска](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)Team Services.</span><span class="sxs-lookup"><span data-stu-id="a7a89-155">Learn more about Team Services [release definitions](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span></span>

### <a name="create-a-build-definition"></a><span data-ttu-id="a7a89-156">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="a7a89-156">Create a build definition</span></span>
<span data-ttu-id="a7a89-157">Откройте веб-браузер и перейдите к новому командному проекту по адресу: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting.</span><span class="sxs-lookup"><span data-stu-id="a7a89-157">Open a web browser and navigate to your new team project at: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting .</span></span> 

<span data-ttu-id="a7a89-158">Перейдите на вкладку **Сборка и выпуск**, выберите **Сборки** и щелкните **+Новое определение**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-158">Select the **Build & Release** tab, then **Builds**, then **+ New definition**.</span></span>  <span data-ttu-id="a7a89-159">В области **Выбор шаблона** выберите шаблон **Приложение Azure Service Fabric** и нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-159">In **Select a template**, select the **Azure Service Fabric Application** template and click **Apply**.</span></span> 

![Выбор шаблона сборки][select-build-template] 

<span data-ttu-id="a7a89-161">Приложение для голосования содержит проект .NET Core, поэтому необходимо добавить задачу для восстановления зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a7a89-161">The voting application contains a .NET Core project, so add a task that restores the dependencies.</span></span> <span data-ttu-id="a7a89-162">В представлении **Задачи** нажмите кнопку **+Добавить задачу** в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="a7a89-162">In the **Tasks** view, select **+ Add Task** in the bottom left.</span></span> <span data-ttu-id="a7a89-163">Выполните поиск по фразе "Командная строка", чтобы найти задачу командной строки, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-163">Search on "Command Line" to find the command-line task, then click **Add**.</span></span> 

![Добавление задачи][add-task] 

<span data-ttu-id="a7a89-165">В поле **Отображаемое имя** новой задачи введите "Run dotnet.exe", в поле **Средство** введите "dotnet.exe", а в поле **Аргументы** — "restore".</span><span class="sxs-lookup"><span data-stu-id="a7a89-165">In the new task, enter "Run dotnet.exe" in **Display name**, "dotnet.exe" in **Tool**, and "restore" in **Arguments**.</span></span> 

![Создание задачи][new-task] 

<span data-ttu-id="a7a89-167">В представлении **Триггеры** щелкните переключатель **Включить этот триггер** в разделе **Непрерывная интеграция**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-167">In the **Triggers** view, click the **Enable this trigger** switch under **Continuous Integration**.</span></span> 

<span data-ttu-id="a7a89-168">Щелкните **Сохранить и поместить в очередь** и введите "Hosted VS2017" в качестве значения параметра **Очередь агента**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-168">Select **Save & queue** and enter "Hosted VS2017" as the **Agent queue**.</span></span> <span data-ttu-id="a7a89-169">Щелкните **Поставить в очередь**, чтобы выполнить сборку вручную.</span><span class="sxs-lookup"><span data-stu-id="a7a89-169">Select **Queue** to manually start a build.</span></span>  <span data-ttu-id="a7a89-170">Сборки также активируются после принудительного запуска или возврата.</span><span class="sxs-lookup"><span data-stu-id="a7a89-170">Builds also triggers upon push or check-in.</span></span>

<span data-ttu-id="a7a89-171">Чтобы проверить ход сборки, перейдите на вкладку **Сборки**.  Проверив, что сборка запускается успешно, создайте определение выпуска, которое развертывает приложение в кластер.</span><span class="sxs-lookup"><span data-stu-id="a7a89-171">To check your build progress, switch to the **Builds** tab.  Once you verify that the build executes successfully, define a release definition that deploys your application to a cluster.</span></span> 

### <a name="create-a-release-definition"></a><span data-ttu-id="a7a89-172">Создание определения выпуска</span><span class="sxs-lookup"><span data-stu-id="a7a89-172">Create a release definition</span></span>  

<span data-ttu-id="a7a89-173">Перейдите на вкладку **Сборка и выпуск**, выберите **Выпуски** и щелкните **+Новое определение**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-173">Select the **Build & Release** tab, then **Releases**, then **+ New definition**.</span></span>  <span data-ttu-id="a7a89-174">В области **Создание определения выпуска** выберите шаблон **Развертывание Azure Service Fabric** в списке и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-174">In **Create release definition**, select the **Azure Service Fabric Deployment** template from the list and click **Next**.</span></span>  <span data-ttu-id="a7a89-175">Выберите источник **Сборка**, установите флажок **Непрерывное развертывание** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-175">Select the **Build** source, check the **Continuous deployment** box, and click **Create**.</span></span> 

<span data-ttu-id="a7a89-176">В представлении **Среды** щелкните **Добавить** справа от поля **Подключение кластера**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-176">In the **Environments** view, click **Add** to the right of **Cluster Connection**.</span></span>  <span data-ttu-id="a7a89-177">Укажите mysftestcluster в качестве имени подключения, адрес tcp://mysftestcluster.westus.cloudapp.azure.com:19000 для конечной точки кластера и учетные данные сертификата или Azure Active Directory для кластера.</span><span class="sxs-lookup"><span data-stu-id="a7a89-177">Specify a connection name of "mysftestcluster", a cluster endpoint of "tcp://mysftestcluster.westus.cloudapp.azure.com:19000", and the Azure Active Directory or certificate credentials for the cluster.</span></span> <span data-ttu-id="a7a89-178">В полях **Имя пользователя** и **Пароль** укажите учетные данные Azure Active Directory для подключения к кластеру.</span><span class="sxs-lookup"><span data-stu-id="a7a89-178">For Azure Active Directory credentials, define the credentials you want to use to connect to the cluster in the **Username** and **Password** fields.</span></span> <span data-ttu-id="a7a89-179">В поле **Сертификат клиента** укажите кодировку Base64 для файла сертификата клиента, который используется для проверки подлинности на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="a7a89-179">For certificate-based authentication, define the Base64 encoding of the client certificate file in the **Client Certificate** field.</span></span>  <span data-ttu-id="a7a89-180">Сведения о том, как получить это значение, получите во всплывающем окне справки для этого поля.</span><span class="sxs-lookup"><span data-stu-id="a7a89-180">See the help pop-up on that field for info on how to get that value.</span></span>  <span data-ttu-id="a7a89-181">Если ваш сертификат защищен паролем, укажите его в поле **Пароль** .</span><span class="sxs-lookup"><span data-stu-id="a7a89-181">If your certificate is password-protected, define the password in the **Password** field.</span></span>  <span data-ttu-id="a7a89-182">Нажмите кнопку **Сохранить**, чтобы сохранить определение выпуска.</span><span class="sxs-lookup"><span data-stu-id="a7a89-182">Click **Save** to save the release definition.</span></span>

![Добавление подключения к кластеру][add-cluster-connection] 

<span data-ttu-id="a7a89-184">Щелкните **Запуск в агенте** и в поле **Очередь развертывания** выберите **Hosted VS2017**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-184">Click **Run on agent**, then select **Hosted VS2017** for **Deployment queue**.</span></span> <span data-ttu-id="a7a89-185">Нажмите кнопку **Сохранить**, чтобы сохранить определение выпуска.</span><span class="sxs-lookup"><span data-stu-id="a7a89-185">Click **Save** to save the release definition.</span></span>

![Запуск в агенте][run-on-agent]

<span data-ttu-id="a7a89-187">Чтобы создать выпуск вручную, последовательно выберите **+Выпуск** -> **Создать выпуск** -> **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7a89-187">Select **+Release** -> **Create Release** -> **Create** to manually create a release.</span></span>  <span data-ttu-id="a7a89-188">Убедитесь, что развертывание выполнено успешно и приложение выполняется в кластере.</span><span class="sxs-lookup"><span data-stu-id="a7a89-188">Verify that the deployment succeeded and the application is running in the cluster.</span></span>  <span data-ttu-id="a7a89-189">Откройте браузер и перейдите по ссылке [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="a7a89-189">Open a web browser and navigate to [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="a7a89-190">Обратите внимание на версию приложения, в данном случае "1.0.0.20170616.3".</span><span class="sxs-lookup"><span data-stu-id="a7a89-190">Note the application version, in this example it is "1.0.0.20170616.3".</span></span> 

## <a name="commit-and-push-changes-trigger-a-release"></a><span data-ttu-id="a7a89-191">Фиксация и отправка изменений, создание выпуска</span><span class="sxs-lookup"><span data-stu-id="a7a89-191">Commit and push changes, trigger a release</span></span>
<span data-ttu-id="a7a89-192">Чтобы проверить работу конвейера непрерывной интеграции, отправьте некоторые изменения кода в Team Services.</span><span class="sxs-lookup"><span data-stu-id="a7a89-192">To verify that the continuous integration pipeline is functioning by checking in some code changes to Team Services.</span></span>    

<span data-ttu-id="a7a89-193">При написании кода в Visual Studio изменения отслеживаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="a7a89-193">As you write your code, your changes are automatically tracked by Visual Studio.</span></span> <span data-ttu-id="a7a89-194">Зафиксировать изменения в локальном репозитории Git можно, щелкнув значок ожидающих изменений (</span><span class="sxs-lookup"><span data-stu-id="a7a89-194">Commit changes to your local Git repository by selecting the pending changes icon (</span></span>![Ожидает][pending]<span data-ttu-id="a7a89-196">) в строке состояния в нижнем правом углу.</span><span class="sxs-lookup"><span data-stu-id="a7a89-196">) from the status bar in the bottom right.</span></span>

<span data-ttu-id="a7a89-197">В представлении **Изменения** в Team Explorer добавьте сообщение с описанием обновления и зафиксируйте изменения.</span><span class="sxs-lookup"><span data-stu-id="a7a89-197">On the **Changes** view in Team Explorer, add a message describing your update and commit your changes.</span></span>

![Фиксация всех изменений][changes]

<span data-ttu-id="a7a89-199">Щелкните значок неопубликованных изменений в строке состояния (![Неопубликованные изменения][unpublished-changes]) или в представлении "Синхронизация" в Team Explorer.</span><span class="sxs-lookup"><span data-stu-id="a7a89-199">Select the unpublished changes status bar icon (![Unpublished changes][unpublished-changes]) or the Sync view in Team Explorer.</span></span> <span data-ttu-id="a7a89-200">Выберите **Отправить изменения**, чтобы обновить код в Team Services/TFS.</span><span class="sxs-lookup"><span data-stu-id="a7a89-200">Select **Push** to update your code in Team Services/TFS.</span></span>

![Отправка изменений][push]

<span data-ttu-id="a7a89-202">При отправке изменений в Team Services автоматически запускается сборка.</span><span class="sxs-lookup"><span data-stu-id="a7a89-202">Pushing the changes to Team Services automatically triggers a build.</span></span>  <span data-ttu-id="a7a89-203">После создания определения сборки автоматически создается выпуск и начинается обновление приложения в кластере.</span><span class="sxs-lookup"><span data-stu-id="a7a89-203">When the build definition successfully completes, a release is automatically created and starts upgrading the application on the cluster.</span></span>

<span data-ttu-id="a7a89-204">Чтобы проверить ход сборки, перейдите на вкладку **Сборки** в **Team Explorer** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7a89-204">To check your build progress, switch to the **Builds** tab in **Team Explorer** in Visual Studio.</span></span>  <span data-ttu-id="a7a89-205">Проверив, что сборка запускается успешно, создайте определение выпуска, которое развертывает приложение в кластер.</span><span class="sxs-lookup"><span data-stu-id="a7a89-205">Once you verify that the build executes successfully, define a release definition that deploys your application to a cluster.</span></span>

<span data-ttu-id="a7a89-206">Убедитесь, что развертывание выполнено успешно и приложение выполняется в кластере.</span><span class="sxs-lookup"><span data-stu-id="a7a89-206">Verify that the deployment succeeded and the application is running in the cluster.</span></span>  <span data-ttu-id="a7a89-207">Откройте браузер и перейдите по ссылке [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="a7a89-207">Open a web browser and navigate to [http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="a7a89-208">Обратите внимание на версию приложения, в этом случае — 1.0.0.20170815.3.</span><span class="sxs-lookup"><span data-stu-id="a7a89-208">Note the application version, in this example it is "1.0.0.20170815.3".</span></span>

![Service Fabric Explorer][sfx1]

## <a name="update-the-application"></a><span data-ttu-id="a7a89-210">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="a7a89-210">Update the application</span></span>
<span data-ttu-id="a7a89-211">Измените код в приложении.</span><span class="sxs-lookup"><span data-stu-id="a7a89-211">Make code changes in the application.</span></span>  <span data-ttu-id="a7a89-212">Сохраните и зафиксируйте изменения, выполнив указанные выше действия.</span><span class="sxs-lookup"><span data-stu-id="a7a89-212">Save and commit the changes, following the previous steps.</span></span>

<span data-ttu-id="a7a89-213">После начала обновления вы сможете отслеживать ход обновления в Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="a7a89-213">Once the upgrade of the application begins, you can watch the upgrade progress in Service Fabric Explorer:</span></span>

![Service Fabric Explorer][sfx2]

<span data-ttu-id="a7a89-215">Обновление приложения может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a7a89-215">The application upgrade may take several minutes.</span></span> <span data-ttu-id="a7a89-216">После завершения обновления будет запущена новая версия приложения.</span><span class="sxs-lookup"><span data-stu-id="a7a89-216">When the upgrade is complete, the application will be running the next version.</span></span>  <span data-ttu-id="a7a89-217">В этом примере — 1.0.0.20170815.4.</span><span class="sxs-lookup"><span data-stu-id="a7a89-217">In this example "1.0.0.20170815.4".</span></span>

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a><span data-ttu-id="a7a89-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7a89-219">Next steps</span></span>
<span data-ttu-id="a7a89-220">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a7a89-220">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7a89-221">Добавление проекта в систему управления версиями</span><span class="sxs-lookup"><span data-stu-id="a7a89-221">Add source control to your project</span></span>
> * <span data-ttu-id="a7a89-222">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="a7a89-222">Create a build definition</span></span>
> * <span data-ttu-id="a7a89-223">Создание определения выпуска</span><span class="sxs-lookup"><span data-stu-id="a7a89-223">Create a release definition</span></span>
> * <span data-ttu-id="a7a89-224">Автоматическое развертывание и обновление приложения</span><span class="sxs-lookup"><span data-stu-id="a7a89-224">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="a7a89-225">Теперь, когда вы развернули приложение и настроили непрерывную интеграцию, попробуйте сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="a7a89-225">Now that you have deployed an application and configured continuous integration, try the following:</span></span>
- [<span data-ttu-id="a7a89-226">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="a7a89-226">Upgrade an app</span></span>](service-fabric-application-upgrade.md)
- [<span data-ttu-id="a7a89-227">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="a7a89-227">Test an app</span></span>](service-fabric-testability-overview.md) 
- [<span data-ttu-id="a7a89-228">Мониторинг и диагностика</span><span class="sxs-lookup"><span data-stu-id="a7a89-228">Monitor and diagnose</span></span>](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png