---
title: "aaaCI/CD с контейнера службы Azure и группу мелких объектов | Документы Microsoft"
description: "Использование контейнера службы Azure с помощью Docker Swarm реестра контейнера Azure и Visual Studio Team Services toodeliver постоянно приложении .NET Core несколькими контейнера"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Swarm, Azure, Visual Studio Team Services, DevOps"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="fcfdc-104">Полный toodeploy конвейера CI/CD приложении несколькими контейнера в контейнер службы Azure с помощью Docker Swarm с помощью Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fcfdc-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="fcfdc-105">Одно из hello крупнейших проблем Разработка современных приложений для облака hello, который может toodeliver этим приложениям непрерывно.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="fcfdc-106">В этой статье Узнайте, как создавать tooimplement полной непрерывной интеграции и развертывания (CI/CD) конвейера, с помощью контейнера службы Azure с помощью Docker Swarm реестра контейнера Azure и Visual Studio Team Services и управления выпуском.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="fcfdc-107">В этой статье используется простое приложение, доступное в [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) и разработанное с помощью ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="fcfdc-108">приложение Hello состоит из четырех различных служб: три веб-API и один веб-интерфейса:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Пример приложения MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="fcfdc-110">Цель Hello является toodeliver это приложение постоянно в кластере помощью Docker Swarm, с помощью Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="fcfdc-111">Hello следующем рисунке сведения в этом конвейере непрерывной поставки:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-111">hello following figure details this continuous delivery pipeline:</span></span>

![Пример приложения MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="fcfdc-113">Вот краткое описание шагов hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="fcfdc-114">Изменения кода будут зафиксированы toohello репозиторий исходного кода (в данном случае GitHub)</span><span class="sxs-lookup"><span data-stu-id="fcfdc-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="fcfdc-115">GitHub активирует сборку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="fcfdc-116">Visual Studio Team Services получает последнюю версию hello hello источников и создает все образы hello, составляющих приложение hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="fcfdc-117">Visual Studio Team Services помещает каждого реестра Docker tooa образов, созданных с помощью службы Azure контейнер реестра hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="fcfdc-118">Visual Studio Team Services активирует новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="fcfdc-119">выпуск Hello выполняет некоторые команды, с помощью SSH на главном узле кластера службы hello контейнер Azure</span><span class="sxs-lookup"><span data-stu-id="fcfdc-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="fcfdc-120">Docker группу мелких объектов hello кластера переносит hello последнюю версию hello изображений</span><span class="sxs-lookup"><span data-stu-id="fcfdc-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="fcfdc-121">новую версию приложения hello Hello развертывается с помощью Docker Compose</span><span class="sxs-lookup"><span data-stu-id="fcfdc-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fcfdc-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fcfdc-122">Prerequisites</span></span>

<span data-ttu-id="fcfdc-123">Перед запуском этого учебника, необходимо toocomplete hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="fcfdc-124">Создайте кластер Swarm в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="fcfdc-125">Подключение с кластером hello группу мелких объектов в контейнере службы Azure</span><span class="sxs-lookup"><span data-stu-id="fcfdc-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="fcfdc-126">Создать реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="fcfdc-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="fcfdc-127">Создать учетную запись и командный проект Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fcfdc-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="fcfdc-128">Разветвление tooyour репозитория GitHub hello учетная запись GitHub</span><span class="sxs-lookup"><span data-stu-id="fcfdc-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="fcfdc-129">Вам также понадобится компьютер Ubuntu (14.04 или 16.04) с установленным программным обеспечением Docker.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="fcfdc-130">Использовать этот компьютер с Visual Studio Team Services во время hello сборок и выпусков процессов.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="fcfdc-131">Одним из способов toocreate эта машина находится в hello изображения hello toouse [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="fcfdc-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="fcfdc-132">Шаг 1. Настройка учетной записи Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fcfdc-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="fcfdc-133">В этом разделе настраивается учетная запись Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="fcfdc-134">Настройка агента сборки Linux Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fcfdc-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="fcfdc-135">образы Docker toocreate и push-построения эти образы в реестр контейнер Azure из Visual Studio Team Services, необходимо tooregister агент Linux.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="fcfdc-136">Доступны следующие варианты установки:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-136">You have these installation options:</span></span>

* [<span data-ttu-id="fcfdc-137">Развертывание агента на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="fcfdc-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="fcfdc-138">Использовать агент VSTS hello toorun Docker</span><span class="sxs-lookup"><span data-stu-id="fcfdc-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="fcfdc-139">Установка расширения Docker интеграции VSTS hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="fcfdc-140">Корпорация Майкрософт предоставляет toowork расширения VSTS с помощью Docker в построении и освободить процессов.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="fcfdc-141">Этот модуль доступен в hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="fcfdc-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="fcfdc-142">Нажмите кнопку **установить** tooadd эту учетную запись VSTS tooyour расширения:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Установка hello интеграция Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="fcfdc-144">Будет предложено tooconnect tooyour VSTS учетную запись, используя свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="fcfdc-145">Подключение между Visual Studio Team Services и GitHub</span><span class="sxs-lookup"><span data-stu-id="fcfdc-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="fcfdc-146">Настройте подключение между проектом VSTS и учетной записью GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="fcfdc-147">В проекте Visual Studio Team Services щелкните hello **параметры** значок в панели инструментов hello и выберите **службы**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services — внешнее подключение](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="fcfdc-149">В левой части экрана приветствия щелкните **новую конечную точку службы** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services — GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="fcfdc-151">Щелкните tooauthorize toowork VSTS с вашей учетной записи GitHub **авторизовать** и выполните процедуру hello в открывшемся окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services — авторизация GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="fcfdc-153">Подключения VSTS tooyour контейнер Azure реестра и кластер контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="fcfdc-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="fcfdc-154">Hello последнего действия перед тем как попасть в конвейер CI/CD hello, tooconfigure внешних соединений tooyour контейнер реестра и помощью Docker Swarm кластера в Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="fcfdc-155">В hello **службы** параметры проекта Visual Studio Team Services добавить конечную точку службы типа **реестра Docker**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="fcfdc-156">В открывшемся всплывающем hello введите URL-адрес hello и hello учетные данные реестра контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services — реестр Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="fcfdc-158">Hello помощью Docker Swarm кластер, добавьте конечную точку типа **SSH**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="fcfdc-159">Введите сведения о соединении SSH hello кластера группу мелких объектов.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services — SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="fcfdc-161">Все настройки hello сейчас выполняются.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-161">All hello configuration is done now.</span></span> <span data-ttu-id="fcfdc-162">В следующих шагах hello создайте hello CI/CD конвейера, который строит и развертывает hello приложения toohello помощью Docker Swarm кластера.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="fcfdc-163">Шаг 2: Создание определения построения hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="fcfdc-164">На этом шаге вы установите definitionfor построения проекта VSTS и определите hello рабочего процесса сборки для образов контейнера</span><span class="sxs-lookup"><span data-stu-id="fcfdc-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="fcfdc-165">Начальная настройка определения</span><span class="sxs-lookup"><span data-stu-id="fcfdc-165">Initial definition setup</span></span>

1. <span data-ttu-id="fcfdc-166">Определение сборки toocreate подключения tooyour проект Visual Studio Team Services и нажмите кнопку **построения и выпуска**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="fcfdc-167">В hello **определений сборки** щелкните **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="fcfdc-168">Выберите hello **пустой** шаблона.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services — новое определение сборки](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="fcfdc-170">Настройте новую сборку hello с источником репозитория GitHub, проверка **непрерывной интеграции**и выберите hello очереди агента, где зарегистрирован агент Linux.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="fcfdc-171">Нажмите кнопку **создать** toocreate hello определение сборки.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services — создание определения сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="fcfdc-173">На hello **определений сборки** страницы, сначала откройте hello **репозитория** и настройте вилки hello toouse hello построения проекта MyShop hello, созданный в предварительных требованиях для hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="fcfdc-174">Убедитесь, что выбрана *acs docs* как hello **ветвь по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services — конфигурация репозитория сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="fcfdc-176">На hello **триггеры** настройте toobe сборки hello запускается после выполнения каждой фиксации.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="fcfdc-177">Выберите **Непрерывная интеграция** и **Пакетные изменения**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services — конфигурация триггера сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="fcfdc-179">Определение рабочего процесса сборки hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-179">Define hello build workflow</span></span>
<span data-ttu-id="fcfdc-180">рабочий процесс построения hello определяется Hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="fcfdc-181">Существует пять toobuild образов контейнера для hello *MyShop* приложения.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="fcfdc-182">Каждый образ создается с помощью Dockerfile, расположенный в папках проекта hello hello:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="fcfdc-183">ProductsApi;</span><span class="sxs-lookup"><span data-stu-id="fcfdc-183">ProductsApi</span></span>
* <span data-ttu-id="fcfdc-184">Прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="fcfdc-184">Proxy</span></span>
* <span data-ttu-id="fcfdc-185">RatingsApi;</span><span class="sxs-lookup"><span data-stu-id="fcfdc-185">RatingsApi</span></span>
* <span data-ttu-id="fcfdc-186">RecommandationsApi;</span><span class="sxs-lookup"><span data-stu-id="fcfdc-186">RecommandationsApi</span></span>
* <span data-ttu-id="fcfdc-187">ShopFront.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-187">ShopFront</span></span>

<span data-ttu-id="fcfdc-188">Требуются два шага Docker tooadd для каждого изображения, одно изображение toobuild hello и одно изображение toopush hello в реестре hello контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="fcfdc-189">Нажмите кнопку tooadd шаг в процессе построения hello, **+ добавить шаг сборки** и выберите **Docker**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services — добавление шагов сборки](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="fcfdc-191">Для каждого изображения, настройте один шаг, который использует hello `docker build` команды.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services — сборка Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="fcfdc-193">Hello операции сборки, выберите контейнер Azure реестр, hello **сборки образа** действие и hello Dockerfile, определяющий каждого изображения.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="fcfdc-194">Набор hello **контекст построения** как hello Dockerfile корневого каталога, а также определить hello **имя образа**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="fcfdc-195">Как показано на предыдущих экран приветствия, начните имя образа hello с hello URI реестра контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="fcfdc-196">(Также можно использовать тег hello переменной tooparameterize сборки hello изображения, например идентификатор сборки hello в этом примере.)</span><span class="sxs-lookup"><span data-stu-id="fcfdc-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="fcfdc-197">Для каждого изображения, настроить второй этап, который использует hello `docker push` команды.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services — принудительная отправка Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="fcfdc-199">Операция отправки hello, выберите контейнер Azure реестр, hello **Push изображения** действия и введите hello **имя образа** , созданного на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="fcfdc-200">После настройки построения hello и принудительные действия для каждого из пяти образов hello, добавьте два действия в hello сборки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="fcfdc-201">а.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-201">a.</span></span> <span data-ttu-id="fcfdc-202">Задачу командной строки, которая использует hello bash сценарий tooreplace *BuildNumber* вхождение в файле hello docker compose.yml с hello текущей сборки идентификатор. См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services — обновление файла Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="fcfdc-204">b.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-204">b.</span></span> <span data-ttu-id="fcfdc-205">Задачу, которая удаляет hello обновления файла Создание сообщения в качестве артефакта построения, чтобы можно было использовать в выпуске hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="fcfdc-206">См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services — публикация файла Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="fcfdc-208">Щелкните **Сохранить** и присвойте имя определению сборки.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="fcfdc-209">Шаг 3: Создание определения выпуска hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="fcfdc-210">Visual Studio Team Services позволяет слишком[управления выпусками во всех средах](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="fcfdc-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="fcfdc-211">Вы можете включить развертывание приложения в различных средах (например, разработки, тестирования, подготовительной и рабочей среде) в виде smooth toomake непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="fcfdc-212">Вы также можете создать среду, которая представляет кластер Docker Swarm Службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - tooACS выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="fcfdc-214">Начальная настройка выпуска</span><span class="sxs-lookup"><span data-stu-id="fcfdc-214">Initial release setup</span></span>

1. <span data-ttu-id="fcfdc-215">Щелкните определение выпуска toocreate **выпуски** > **+ выпуска**</span><span class="sxs-lookup"><span data-stu-id="fcfdc-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="fcfdc-216">Источник артефакта hello tooconfigure, щелкните **артефакты** > **ссылка на источник артефакта**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="fcfdc-217">Здесь свяжите этот новый сборки toohello определения выпуска, определенные в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="fcfdc-218">Таким образом, hello docker compose.yml файл находится в процессе выпуска hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services — артефакты выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="fcfdc-220">триггер выпуска tooconfigure hello, нажмите кнопку **триггеры** и выберите **непрерывного развертывания**.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="fcfdc-221">Задать триггер hello для hello одного источника артефакта.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="fcfdc-222">Этот параметр гарантирует, что новый выпуск начинается сразу после успешного построения hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services — триггеры выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="fcfdc-224">Определение рабочего процесса выпуска hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-224">Define hello release workflow</span></span>

<span data-ttu-id="fcfdc-225">рабочий процесс выпуска Hello состоит из двух задач, которые вы добавляете.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="fcfdc-226">Настройка типа hello копирования toosecurely задач составления tooa файл *развертывания* папку hello помощью Docker Swarm главного узла, с помощью подключения SSH hello, настроенные ранее.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="fcfdc-227">См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services — SCP выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="fcfdc-229">Настройте второй tooexecute задачи toorun команда bash `docker` и `docker-compose` команд на главном узле hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="fcfdc-230">См. следующий экран подробности hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services — bash-команда выпуска](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="fcfdc-232">Hello команда, выполняемая на hello hello используйте master Docker CLI и hello Docker Compose CLI toodo hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fcfdc-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="fcfdc-233">Реестр контейнер Azure toohello входа (он использует три variab'les сборки, определенные в hello **переменных** вкладка)</span><span class="sxs-lookup"><span data-stu-id="fcfdc-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="fcfdc-234">Определение hello **DOCKER_HOST** переменных toowork с конечной точкой группу мелких объектов hello (: 2375)</span><span class="sxs-lookup"><span data-stu-id="fcfdc-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="fcfdc-235">Перейдите toohello *развертывание* папки, который был создан hello предшествующей задаче безопасного копирования, которая содержит файл docker compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="fcfdc-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="fcfdc-236">Выполнение `docker-compose` команд, которые по запросу hello новых образов, остановите службы hello, удалите hello службы, а также создавать контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="fcfdc-237">Как показано на предыдущих экран приветствия, оставьте hello **сбой STDERR** флажок.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="fcfdc-238">Это важно установить, так как `docker-compose` выводит несколько диагностические сообщения, такие как контейнеры, остановки или удаления, на hello стандартный вывод ошибок.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="fcfdc-239">Если флажок hello Visual Studio Team Services сообщает об ошибках при выпуске hello, даже если все пойдет хорошо.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="fcfdc-240">Сохраните это новое определение выпуска.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="fcfdc-241">Это развертывание включает некоторое время простоя, поскольку мы остановка служб старого hello и запущен новый hello.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="fcfdc-242">Он является возможные tooavoid это, выполнив развертывание сине зеленый.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="fcfdc-243">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-243">Step 4.</span></span> <span data-ttu-id="fcfdc-244">Тестирование hello CI/CD конвейера</span><span class="sxs-lookup"><span data-stu-id="fcfdc-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="fcfdc-245">Теперь, когда вы закончите настройку hello, это время tootest этот новый конвейер CI или компакт-диска.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="fcfdc-246">наиболее простым способом tootest Hello это tooupdate hello исходного кода, чтобы зафиксировать hello изменения в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="fcfdc-247">Через несколько секунд после принудительной кода hello, вы увидите новую сборку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="fcfdc-248">После успешного завершения нового выпуска будет запущено и развернет hello новую версию приложения hello в кластере hello контейнера службы Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfdc-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcfdc-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcfdc-249">Next Steps</span></span>

* <span data-ttu-id="fcfdc-250">Дополнительные сведения о конфигурации или компакт-ДИСК с Visual Studio Team Services см. в разделе hello [Обзор сборки VSTS](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="fcfdc-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
