---
title: "aaaCI/CD с модуль службы контейнера Azure и скапливаются режимом | Документы Microsoft"
description: "Использовать модуль службы Azure контейнера с toodeliver режим скапливаются Docker, реестр контейнера Azure и Visual Studio Team Services постоянно приложении .NET Core несколькими контейнера"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, контейнеры, микрослужбы, Swarm, Azure, Visual Studio Team Services, DevOps, обработчик ACS"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="c5ae4-104">Полный toodeploy конвейера CI/CD приложении несколькими контейнера в контейнер службы Azure с обработчиком ACS и режиме скапливаются Docker, с помощью Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c5ae4-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="c5ae4-105">*Эта статья основана на [полный CI/CD конвейера toodeploy приложении несколькими контейнера в контейнер службы Azure с помощью Docker Swarm с помощью Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) документации*</span><span class="sxs-lookup"><span data-stu-id="c5ae4-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="c5ae4-106">В настоящее время один из hello крупнейших проблем Разработка современных приложений для облака hello, который может toodeliver этим приложениям непрерывно.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="c5ae4-107">В этой статье вы узнаете, как tooimplement полной непрерывной интеграции и развертывания (CI/CD) конвейера с помощью:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="c5ae4-108">обработчик Службы контейнеров Azure с Docker Swarm Mode;</span><span class="sxs-lookup"><span data-stu-id="c5ae4-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="c5ae4-109">реестр контейнеров Azure;</span><span class="sxs-lookup"><span data-stu-id="c5ae4-109">Azure Container Registry</span></span>
* <span data-ttu-id="c5ae4-110">Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-110">Visual Studio Team Services</span></span>

<span data-ttu-id="c5ae4-111">В этой статье используется простое приложение, доступное в [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) и разработанное с помощью ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="c5ae4-112">приложение Hello состоит из четырех различных служб: три веб-API и один веб-интерфейса:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Пример приложения MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="c5ae4-114">Цель Hello является toodeliver это приложение постоянно в кластере режим скапливаются Docker, с помощью Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="c5ae4-115">Hello следующем рисунке сведения в этом конвейере непрерывной поставки:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-115">hello following figure details this continuous delivery pipeline:</span></span>

![Пример приложения MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="c5ae4-117">Вот краткое описание шагов hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="c5ae4-118">Изменения кода будут зафиксированы toohello репозиторий исходного кода (в данном случае GitHub)</span><span class="sxs-lookup"><span data-stu-id="c5ae4-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="c5ae4-119">GitHub активирует сборку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="c5ae4-120">Visual Studio Team Services получает последнюю версию hello hello источников и создает все образы hello, составляющих приложение hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="c5ae4-121">Visual Studio Team Services помещает каждого реестра Docker tooa образов, созданных с помощью службы Azure контейнер реестра hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="c5ae4-122">Visual Studio Team Services активирует новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="c5ae4-123">выпуск Hello выполняет некоторые команды, с помощью SSH на главном узле кластера службы hello контейнер Azure</span><span class="sxs-lookup"><span data-stu-id="c5ae4-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="c5ae4-124">Режим скапливаются docker на кластере hello извлекает последнюю версию hello hello изображений</span><span class="sxs-lookup"><span data-stu-id="c5ae4-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="c5ae4-125">новую версию приложения hello Hello развертывается с помощью Docker стека</span><span class="sxs-lookup"><span data-stu-id="c5ae4-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c5ae4-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c5ae4-126">Prerequisites</span></span>

<span data-ttu-id="c5ae4-127">Перед запуском этого учебника, необходимо toocomplete hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="c5ae4-128">Создать кластер Swarm Mode в Службе контейнеров Azure с обработчиком ACS.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="c5ae4-129">Подключение с кластером hello группу мелких объектов в контейнере службы Azure</span><span class="sxs-lookup"><span data-stu-id="c5ae4-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="c5ae4-130">Создать реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="c5ae4-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="c5ae4-131">Создать учетную запись и командный проект Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c5ae4-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="c5ae4-132">Разветвление tooyour репозитория GitHub hello учетная запись GitHub</span><span class="sxs-lookup"><span data-stu-id="c5ae4-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="c5ae4-133">orchestrator помощью Docker Swarm Hello в службе контейнера Azure использует устаревший автономный группу мелких объектов.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="c5ae4-134">В настоящее время интегрирован hello [режим группу мелких объектов](https://docs.docker.com/engine/swarm/) (в Docker 1.12 и более поздние версии) не является поддерживаемой orchestrator в службе контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="c5ae4-135">По этой причине мы используем [модуль ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), предоставленного сообществом [шаблоном краткого руководства](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), или Docker решения в hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="c5ae4-136">Шаг 1. Настройка учетной записи Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c5ae4-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="c5ae4-137">В этом разделе настраивается учетная запись Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="c5ae4-138">tooconfigure VSTS служб конечных точек, в проекте Visual Studio Team Services щелкните hello **параметры** значок в панели инструментов hello и выберите **службы**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Откройте конечную точку служб](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="c5ae4-140">Подключение Visual Studio Team Services к учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="c5ae4-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="c5ae4-141">Настройте подключение между проектом VSTS и учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="c5ae4-142">В левой части экрана приветствия щелкните **новую конечную точку службы** > **диспетчера ресурсов Azure**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="c5ae4-143">tooauthorize toowork VSTS с учетной записью Azure, выберите ваш **подписки** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services — авторизация в Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="c5ae4-145">Подключение между Visual Studio Team Services и GitHub</span><span class="sxs-lookup"><span data-stu-id="c5ae4-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="c5ae4-146">Настройте подключение между проектом VSTS и учетной записью GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="c5ae4-147">В левой части экрана приветствия щелкните **новую конечную точку службы** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="c5ae4-148">Щелкните tooauthorize toowork VSTS с вашей учетной записи GitHub **авторизовать** и выполните процедуру hello в открывшемся окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services — авторизация GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="c5ae4-150">Подключите кластер контейнера службы Azure tooyour VSTS</span><span class="sxs-lookup"><span data-stu-id="c5ae4-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="c5ae4-151">Hello последнего действия перед тем как попасть в конвейер CI/CD hello, tooconfigure внешних соединений tooyour помощью Docker Swarm кластера в Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="c5ae4-152">Hello помощью Docker Swarm кластер, добавьте конечную точку типа **SSH**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="c5ae4-153">Введите сведения о соединении SSH hello группу мелких объектов кластера (главный узел).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="c5ae4-155">Все настройки hello сейчас выполняются.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-155">All hello configuration is done now.</span></span> <span data-ttu-id="c5ae4-156">В следующих шагах hello создайте hello CI/CD конвейера, который строит и развертывает hello приложения toohello помощью Docker Swarm кластера.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="c5ae4-157">Шаг 2: Создание определения построения hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="c5ae4-158">На этом этапе Настройка определения построения для проекта VSTS и определение рабочего процесса сборки hello для контейнера изображений</span><span class="sxs-lookup"><span data-stu-id="c5ae4-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="c5ae4-159">Начальная настройка определения</span><span class="sxs-lookup"><span data-stu-id="c5ae4-159">Initial definition setup</span></span>

1. <span data-ttu-id="c5ae4-160">Определение сборки toocreate подключения tooyour проект Visual Studio Team Services и нажмите кнопку **построения и выпуска**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="c5ae4-161">В hello **определений сборки** щелкните **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services — новое определение сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="c5ae4-163">Выберите hello **пустые процесса**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services — новое пустое определение сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="c5ae4-165">Нажмите кнопку hello **переменных** и создайте две переменные: **RegistryURL** и **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="c5ae4-166">Вставьте hello значения реестра и агенты DNS кластера.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services — конфигурация переменных сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="c5ae4-168">На hello **определений сборки** страницу, откройте hello **триггеры** и настройте hello построения toouse непрерывной интеграции с hello ветвления hello MyShop проект, созданный в предварительных требованиях для hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="c5ae4-169">Затем выберите **Пакетные изменения**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="c5ae4-170">Убедитесь, что выбрана *docker linux* как hello **ветвление спецификации**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services — конфигурация репозитория сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="c5ae4-172">Наконец, нажмите кнопку hello **параметры** и настройте очереди агента по умолчанию hello слишком**размещенных предварительной версии Linux**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services — конфигурация агента узла](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="c5ae4-174">Определение рабочего процесса сборки hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-174">Define hello build workflow</span></span>
<span data-ttu-id="c5ae4-175">рабочий процесс построения hello определяется Hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="c5ae4-176">Во-первых необходимо tooconfigure hello исходного кода hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="c5ae4-177">toodo его, выберите **GitHub** и **репозитория** и **ветви** (docker linux).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services — настройка источника кода](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="c5ae4-179">Существует пять toobuild образов контейнера для hello *MyShop* приложения.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="c5ae4-180">Каждый образ создается с помощью Dockerfile, расположенный в папках проекта hello hello:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="c5ae4-181">ProductsApi;</span><span class="sxs-lookup"><span data-stu-id="c5ae4-181">ProductsApi</span></span>
* <span data-ttu-id="c5ae4-182">Прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="c5ae4-182">Proxy</span></span>
* <span data-ttu-id="c5ae4-183">RatingsApi;</span><span class="sxs-lookup"><span data-stu-id="c5ae4-183">RatingsApi</span></span>
* <span data-ttu-id="c5ae4-184">RecommandationsApi;</span><span class="sxs-lookup"><span data-stu-id="c5ae4-184">RecommandationsApi</span></span>
* <span data-ttu-id="c5ae4-185">ShopFront.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-185">ShopFront</span></span>

<span data-ttu-id="c5ae4-186">Требуются два шага Docker для каждого изображения, одно изображение toobuild hello и одно изображение toopush hello в реестре hello контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="c5ae4-187">Нажмите кнопку tooadd шаг в процессе построения hello, **+ добавить шаг сборки** и выберите **Docker**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services — добавление шагов сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="c5ae4-189">Для каждого изображения, настройте один шаг, который использует hello `docker build` команды.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services — сборка Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="c5ae4-191">Hello операции сборки, выберите реестр контейнера Azure, hello **сборки образа** действие и hello Dockerfile, определяющий каждого изображения.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="c5ae4-192">Набор hello **рабочий каталог** hello Dockerfile корневого каталога, определение hello **имя образа**и выберите **включают последние тег**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="c5ae4-193">Имя образа Hello имеет toobe в следующем формате: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="c5ae4-194">Замените **[NAME]** с именем hello образа:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="c5ae4-195">Для каждого изображения, настроить второй этап, который использует hello `docker push` команды.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services — принудительная отправка Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="c5ae4-197">Операция отправки hello, выберите контейнер Azure реестр, hello **Push изображения** действие, введите hello **имя образа** , созданного в предыдущем шаге hello и выберите **включают последние тега** .</span><span class="sxs-lookup"><span data-stu-id="c5ae4-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="c5ae4-198">После настройки построения hello и принудительные действия для каждого из пяти образов hello, добавьте три дополнительные шаги в hello сборки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services — добавление задачи командной строки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="c5ae4-200">Задачу командной строки, которая использует hello bash сценарий tooreplace *RegistryURL* вхождение в файле hello docker compose.yml с переменной RegistryURL hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services — обновление файла Compose с URL-адресом реестра](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="c5ae4-202">Задачу командной строки, которая использует hello bash сценарий tooreplace *AgentURL* вхождение в файле hello docker compose.yml с переменной AgentURL hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="c5ae4-203">Задачу, которая удаляет hello обновления файла Создание сообщения в качестве артефакта построения, чтобы можно было использовать в выпуске hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="c5ae4-204">См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services — публикация артефакта](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services — публикация файла Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="c5ae4-207">Нажмите кнопку **сохранить & очередь** tootest определение сборки.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services — сохранение и помещение в очередь](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services — новая очередь](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="c5ae4-210">Если hello **построения** правильный, у вас toosee этот экран:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services — сборка выполнена успешно](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="c5ae4-212">Шаг 3: Создание определения выпуска hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="c5ae4-213">Visual Studio Team Services позволяет слишком[управления выпусками во всех средах](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="c5ae4-214">Вы можете включить развертывание приложения в различных средах (например, разработки, тестирования, подготовительной и рабочей среде) в виде smooth toomake непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="c5ae4-215">Вы также можете создать среду, которая представляет кластер Docker Swarm Mode Службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - tooACS выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="c5ae4-217">Начальная настройка выпуска</span><span class="sxs-lookup"><span data-stu-id="c5ae4-217">Initial release setup</span></span>

1. <span data-ttu-id="c5ae4-218">Щелкните определение выпуска toocreate **выпуски** > **+ выпуска**</span><span class="sxs-lookup"><span data-stu-id="c5ae4-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="c5ae4-219">Источник артефакта hello tooconfigure, щелкните **артефакты** > **ссылка на источник артефакта**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="c5ae4-220">Здесь свяжите этот новый сборки toohello определения выпуска, определенные в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="c5ae4-221">После этого файл docker compose.yml hello доступен в процесс выпуска hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services — артефакты выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="c5ae4-223">триггер выпуска tooconfigure hello, нажмите кнопку **триггеры** и выберите **непрерывного развертывания**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="c5ae4-224">Задать триггер hello для hello одного источника артефакта.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="c5ae4-225">Этот параметр гарантирует, что новый выпуск начинается при успешном построении hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services — триггеры выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="c5ae4-227">переменные выпуска tooconfigure hello, нажмите кнопку **переменных** и выберите **+ переменной** toocreate три новые переменные с информацией о hello реестра hello: **docker.username**, **docker.password**, и **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="c5ae4-228">Вставьте hello значения реестра и агенты DNS кластера.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services — конфигурация репозитория сборки](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="c5ae4-230">Как показано на предыдущем экране приветствия щелкните hello **блокировки** флажок в docker.password.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="c5ae4-231">Этот параметр является важным toorestrict hello пароль.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="c5ae4-232">Определение рабочего процесса выпуска hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-232">Define hello release workflow</span></span>

<span data-ttu-id="c5ae4-233">рабочий процесс выпуска Hello состоит из двух задач, которые вы добавляете.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="c5ae4-234">Настройка типа hello копирования toosecurely задач составления tooa файл *развертывания* папку hello помощью Docker Swarm главного узла, с помощью подключения SSH hello, настроенные ранее.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="c5ae4-235">См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="c5ae4-236">Исходная папка: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="c5ae4-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services — SCP выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="c5ae4-238">Настройте второй tooexecute задачи toorun команда bash `docker` и `docker stack deploy` команд на главном узле hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="c5ae4-239">См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services — bash-команда выпуска](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="c5ae4-241">Hello команда, выполняемая в образце hello использует hello Docker CLI и hello Docker Compose CLI toodo hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c5ae4-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="c5ae4-242">Войдите в реестре toohello контейнер Azure (в нем используются три переменные сборки, определенные в hello **переменных** вкладка)</span><span class="sxs-lookup"><span data-stu-id="c5ae4-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="c5ae4-243">Определение hello **DOCKER_HOST** переменных toowork с конечной точкой группу мелких объектов hello (: 2375)</span><span class="sxs-lookup"><span data-stu-id="c5ae4-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="c5ae4-244">Перейдите toohello *развертывание* папки, который был создан hello предшествующей задаче безопасного копирования, которая содержит файл docker compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="c5ae4-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="c5ae4-245">Выполнение `docker stack deploy` команды, которые запрашивает новые образы hello и создавать контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="c5ae4-246">Как показано на предыдущем экране приветствия, оставьте hello **сбой STDERR** флажок.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="c5ae4-247">Этот параметр позволяет нам процесс выпуска hello toocomplete из-за слишком`docker-compose` выводит несколько диагностические сообщения, такие как контейнеры, остановки или удаления, на hello стандартный вывод ошибок.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="c5ae4-248">Если флажок hello Visual Studio Team Services сообщает об ошибках при выпуске hello, даже если все пойдет хорошо.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="c5ae4-249">Сохраните это новое определение выпуска.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="c5ae4-250">Шаг 4: Тестирование hello CI/CD конвейера</span><span class="sxs-lookup"><span data-stu-id="c5ae4-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="c5ae4-251">Теперь, когда вы закончите настройку hello, это время tootest этот новый конвейер CI или компакт-диска.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="c5ae4-252">наиболее простым способом tootest Hello это tooupdate hello исходного кода, чтобы зафиксировать hello изменения в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="c5ae4-253">Через несколько секунд после принудительной кода hello, вы увидите новую сборку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="c5ae4-254">После успешного завершения новый выпуск активируется и развернуты hello новую версию приложения hello в кластере hello контейнера службы Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ae4-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5ae4-255">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5ae4-255">Next steps</span></span>

* <span data-ttu-id="c5ae4-256">Дополнительные сведения о конфигурации или компакт-ДИСК с Visual Studio Team Services см. в разделе hello [Обзор сборки VSTS](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="c5ae4-257">Дополнительные сведения о ACS см. в разделе hello [в репозитории GitHub модуль ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="c5ae4-258">Дополнительные сведения о режиме с помощью Docker Swarm см. в разделе hello [Общие сведения о режиме с помощью Docker Swarm](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="c5ae4-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
