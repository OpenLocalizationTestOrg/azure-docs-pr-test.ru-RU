---
title: "aaaCI/CD из Jenkins tooAzure виртуальных машин с Team Services | Документы Microsoft"
description: "Настройка непрерывной интеграции (CI) и непрерывного развертывания (CD) с помощью виртуальных машин tooAzure Jenkins из управления выпусками в Visual Studio Team Services (VSTS) или Microsoft Team Foundation Server (TFS) приложение Node.js"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="5a98d-103">Развертывание вашего приложения tooLinux виртуальных машин с помощью Jenkins и Team Services</span><span class="sxs-lookup"><span data-stu-id="5a98d-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="5a98d-104">Непрерывная интеграция (CI) и непрерывное развертывание (CD) представляют собой конвейер, с помощью которого можно выполнить сборку, выпустить и развернуть свой код.</span><span class="sxs-lookup"><span data-stu-id="5a98d-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="5a98d-105">Team Services предоставляет полный, полнофункциональный набор средств автоматизации CI или компакт-диска для развертывания tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5a98d-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="5a98d-106">Jenkins — это популярный серверный инструмент CI и CD стороннего поставщика, который также обеспечивает автоматизацию этих процессов.</span><span class="sxs-lookup"><span data-stu-id="5a98d-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="5a98d-107">Можно использовать оба вместе toocustomize способ доставки облачного приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="5a98d-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="5a98d-108">В этом учебнике используется Jenkins toobuild **веб-приложение Node.js**и Visual Studio Team Services toodeploy его tooa [Группа развертывания](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) содержащий виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="5a98d-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="5a98d-109">Вы сможете выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5a98d-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a98d-110">Выполнение сборки приложения в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="5a98d-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="5a98d-111">Настройка Jenkins для интеграции с Team Services.</span><span class="sxs-lookup"><span data-stu-id="5a98d-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="5a98d-112">Создание группы развертывания для hello виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="5a98d-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="5a98d-113">Создание определения выпуска, который настраивает hello виртуальных машин и развертывает приложение hello</span><span class="sxs-lookup"><span data-stu-id="5a98d-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5a98d-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5a98d-114">Before you begin</span></span>

* <span data-ttu-id="5a98d-115">Требуется учетная запись доступа к tooa Jenkins.</span><span class="sxs-lookup"><span data-stu-id="5a98d-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="5a98d-116">Если вы еще не создали сервер Jenkins, ознакомьтесь с [документацией по Jenkins](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="5a98d-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="5a98d-117">Войдите в учетную запись Team Services tooyour (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="5a98d-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="5a98d-118">Вы можете получить [бесплатную учетную запись Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="5a98d-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="5a98d-119">Дополнительные сведения см. в разделе [подключения служб tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="5a98d-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="5a98d-120">Создайте личный маркер доступа (PAT) в своей учетной записи Team Services, если у вас его еще нет.</span><span class="sxs-lookup"><span data-stu-id="5a98d-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="5a98d-121">Jenkins требуется этот tooaccess сведения учетной записи Team Services.</span><span class="sxs-lookup"><span data-stu-id="5a98d-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="5a98d-122">Чтение [как создать личный маркер доступа для Team Services и TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn как toogenerate один.</span><span class="sxs-lookup"><span data-stu-id="5a98d-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="5a98d-123">Получите пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="5a98d-123">Get hello sample app</span></span>

<span data-ttu-id="5a98d-124">Вы должны toodeploy приложения, хранятся в репозитории.</span><span class="sxs-lookup"><span data-stu-id="5a98d-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="5a98d-125">В данном руководстве мы рекомендуем использовать [этот пример приложения с сайта GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="5a98d-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="5a98d-126">Создайте вилку это приложение и запишите расположение hello (URL) для использования в последующих шагах данного учебника.</span><span class="sxs-lookup"><span data-stu-id="5a98d-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="5a98d-127">Сделать вилки hello **открытый** toosimplify подключения tooGitHub позднее.</span><span class="sxs-lookup"><span data-stu-id="5a98d-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="5a98d-128">Дополнительные сведения см. в разделах [Fork A Repo](https://help.github.com/articles/fork-a-repo/) (Создание вилки репозитория) и [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Как сделать частный репозиторий общедоступным).</span><span class="sxs-lookup"><span data-stu-id="5a98d-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="5a98d-129">приложение Hello был создан с помощью [Yeoman](http://yeoman.io/learning/index.html); он использует **Express**, **bower**, и **grunt**; и он обладает некоторыми **npm**пакетов в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="5a98d-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="5a98d-130">Пример приложения Hello содержит набор [шаблоны Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) , используемые toodynamically создаются hello виртуальных машин для развертывания в Azure.</span><span class="sxs-lookup"><span data-stu-id="5a98d-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="5a98d-131">Эти шаблоны используются в задачах hello [определение выпуска Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="5a98d-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="5a98d-132">основной шаблон Hello создает группу безопасности сети, виртуальной машины и виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5a98d-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="5a98d-133">Он назначает общедоступный IP-адрес и открывает входящий порт 80.</span><span class="sxs-lookup"><span data-stu-id="5a98d-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="5a98d-134">Он также добавляет тег, который используется hello развертывания группы слишком выберите hello машины tooreceive hello развертыванием.</span><span class="sxs-lookup"><span data-stu-id="5a98d-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="5a98d-135">Образец Hello также содержит скрипт, который настраивает Nginx и развертывает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="5a98d-136">Он выполняется на всех виртуальных машинах hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="5a98d-137">В частности hello скрипт устанавливает узла, Nginx и PM2; Настраивает Nginx и PM2; затем запускает приложение hello узла.</span><span class="sxs-lookup"><span data-stu-id="5a98d-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="5a98d-138">Настройка подключаемых модулей Jenkins</span><span class="sxs-lookup"><span data-stu-id="5a98d-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="5a98d-139">Сначала необходимо настроить два подключаемых модуля Jenkins для **NodeJS** и **интеграции с Team Services**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="5a98d-140">Откройте учетную запись Jenkins и выберите **Manage Jenkins** (Управление Jenkins).</span><span class="sxs-lookup"><span data-stu-id="5a98d-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="5a98d-141">В hello **управления Jenkins** выберите **управление подключаемыми модулями**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="5a98d-142">Список toolocate фильтра hello hello **NodeJS** подключаемого модуля и установить его без перезапуска.</span><span class="sxs-lookup"><span data-stu-id="5a98d-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Добавление подключаемого модуля tooJenkins hello NodeJS](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="5a98d-144">Список toofind фильтра hello hello **Team Foundation Server** подключаемого модуля и установить его.</span><span class="sxs-lookup"><span data-stu-id="5a98d-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="5a98d-145">(Этот подключаемый модуль подходит и для Team Services, и для Team Foundation Server.) Перезапускать Jenkins не обязательно.</span><span class="sxs-lookup"><span data-stu-id="5a98d-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="5a98d-146">Настройка сборки Jenkins для Node.js</span><span class="sxs-lookup"><span data-stu-id="5a98d-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="5a98d-147">Создайте в Jenkins проект сборки и настройте его следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5a98d-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="5a98d-148">В hello **Общие** введите имя для сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="5a98d-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="5a98d-149">В hello **управление исходным кодом** выберите **Git** и введите сведения о hello репозитория hello и hello ветвь, содержащая код приложения.</span><span class="sxs-lookup"><span data-stu-id="5a98d-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Добавление сборки tooyour репозитория](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="5a98d-151">Если репозиторий не является открытым, выберите **добавить** и предоставить tooit tooconnect учетные данные.</span><span class="sxs-lookup"><span data-stu-id="5a98d-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="5a98d-152">В hello **сборки триггеров** выберите **SCM опроса** и введите hello расписания `H/03 * * * *` toopoll hello репозитории для изменения каждые три минуты.</span><span class="sxs-lookup"><span data-stu-id="5a98d-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="5a98d-153">В hello **среду сборки среды** выберите **предоставляют узел &amp; npm bin / путь к папке** и введите `NodeJS` для hello значение узла JS установки.</span><span class="sxs-lookup"><span data-stu-id="5a98d-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="5a98d-154">Для параметра **npmrc file** (NPMRC-файл) оставьте значение "use system default" (Использовать системное значение по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="5a98d-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="5a98d-155">В hello **построения** , введите команду hello `npm install` tooensure, обновляются все зависимости.</span><span class="sxs-lookup"><span data-stu-id="5a98d-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="5a98d-156">Настройка Jenkins для интеграции с Team Services.</span><span class="sxs-lookup"><span data-stu-id="5a98d-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="5a98d-157">В hello **действия после построения** вкладке для **tooarchive файлы**, введите `**/*` tooinclude все файлы.</span><span class="sxs-lookup"><span data-stu-id="5a98d-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="5a98d-158">Для **выпуска в TFS и Team Services**, введите полный URL-адрес hello, учетной записи (например, `https://your-account-name.visualstudio.com`), hello имя проекта, для определения выпуска hello (создано в более поздней версии), имя и hello учетной записи tooyour tooconnect учетные данные.</span><span class="sxs-lookup"><span data-stu-id="5a98d-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="5a98d-159">Требуется имя пользователя и hello МАРИЯ, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="5a98d-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Настройка действий после сборки Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="5a98d-161">Сохраните проект сборки hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="5a98d-162">Создание конечной точки службы Jenkins</span><span class="sxs-lookup"><span data-stu-id="5a98d-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="5a98d-163">Конечная точка службы позволяет tooJenkins tooconnect Team Services.</span><span class="sxs-lookup"><span data-stu-id="5a98d-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="5a98d-164">Откройте hello **службы** страницы в Team Services, откройте hello **новую конечную точку службы** , а затем выберите **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Добавление конечной точки Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="5a98d-166">Введите имя, будет использовать toorefer toothis соединения.</span><span class="sxs-lookup"><span data-stu-id="5a98d-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="5a98d-167">Введите адрес URL сервера Jenkins hello и деления hello **принимать недоверенные сертификаты SSL** параметр.</span><span class="sxs-lookup"><span data-stu-id="5a98d-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="5a98d-168">Введите hello имя пользователя и пароль для учетной записи Jenkins.</span><span class="sxs-lookup"><span data-stu-id="5a98d-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="5a98d-169">Выберите **Проверка подключения** toocheck, hello сведения верны.</span><span class="sxs-lookup"><span data-stu-id="5a98d-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="5a98d-170">Выберите **ОК** конечной точки службы toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="5a98d-171">Создание группы развертывания</span><span class="sxs-lookup"><span data-stu-id="5a98d-171">Create a deployment group</span></span>

<span data-ttu-id="5a98d-172">Требуется [Группа развертывания](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) слишком содержат hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a98d-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="5a98d-173">Привет открыть **выпуски** вкладка hello **построения &amp; выпуска** концентратора, а затем откройте hello **группы развертывания** и кнопку **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="5a98d-174">Введите имя для группы развертывания hello и необязательное описание.</span><span class="sxs-lookup"><span data-stu-id="5a98d-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="5a98d-175">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-175">Then choose **Create**.</span></span>

<span data-ttu-id="5a98d-176">Задача развертывания группы ресурсов Azure Hello создает и регистрирует hello виртуальных машин, когда оно выполняется с помощью шаблона Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="5a98d-177">Не нужны toocreate и зарегистрироваться в hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a98d-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="5a98d-178">Создание определения выпуска</span><span class="sxs-lookup"><span data-stu-id="5a98d-178">Create a release definition</span></span>

<span data-ttu-id="5a98d-179">Определение выпуска указывает, что процесс hello Team Services будет выполняться приложение hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5a98d-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="5a98d-180">Определение выпуска toocreate hello в Team Services:</span><span class="sxs-lookup"><span data-stu-id="5a98d-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="5a98d-181">Откройте hello **выпуски** вкладка hello **построения &amp; выпуска** концентратора, откройте hello  **+**  раскрывающегося списка в список hello определения выпуска, а затем выберите Hello **создать определение выпуска**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="5a98d-182">Выберите hello **пустой** шаблона и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="5a98d-183">В hello **артефакты** щелкните **ссылку артефакта** и выберите **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="5a98d-184">Выберите подключение к конечной точке службы Jenkins.</span><span class="sxs-lookup"><span data-stu-id="5a98d-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="5a98d-185">Затем выберите задание источника Jenkins hello и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="5a98d-186">В новых hello определение выпуска, выберите **+ добавить задачи** и добавьте **развертывания группы ресурсов Azure** среды по умолчанию toohello задач.</span><span class="sxs-lookup"><span data-stu-id="5a98d-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="5a98d-187">Выберите hello раскрывающийся список стрелку Далее toohello **+ добавить задачи** ссылку и добавьте определение toohello этап развертывания группы.</span><span class="sxs-lookup"><span data-stu-id="5a98d-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Добавление этапа группы развертывания](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="5a98d-189">В каталоге hello задач, откройте hello **программы** раздел и добавить экземпляр hello **сценарий** задачи.</span><span class="sxs-lookup"><span data-stu-id="5a98d-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="5a98d-190">шаблон параметров Hello, используемый в задачу развертывания группы ресурсов Azure hello задает hello администратора пароль, используемый tooconnect toohello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a98d-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="5a98d-191">Укажите этот пароль с переменной hello **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="5a98d-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="5a98d-192">Откройте hello **переменных** вкладке и в hello **переменных** введите имя hello `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="5a98d-193">Введите пароль администратора hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="5a98d-194">Выберите hello «замка» значок Далее toohello значение текстового поля tooprotect hello пароль.</span><span class="sxs-lookup"><span data-stu-id="5a98d-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="5a98d-195">Настроить задачу hello развертывания группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="5a98d-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="5a98d-196">Hello **развертывания группы ресурсов Azure** задача — Группа развертывания используется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="5a98d-197">Настройте его следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5a98d-197">Configure it as follows:</span></span>

* <span data-ttu-id="5a98d-198">**Подписка Azure:** выберите соединение из списка hello **доступных подключений службы Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="5a98d-199">Если подключения не отображается, выберите **управление**выберите **новую конечную точку службы** затем **диспетчера ресурсов Azure**и следуйте появляющимся на hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="5a98d-200">Возвращает определение tooyour выпуска, обновления hello **AzureRM подписки** список и выберите hello подключения, вы создали.</span><span class="sxs-lookup"><span data-stu-id="5a98d-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="5a98d-201">**Группа ресурсов**: Введите имя группы ресурсов hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="5a98d-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="5a98d-202">**Расположение**: Выберите регион для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-202">**Location**: Select a region for hello deployment.</span></span>

  ![Создание новой группы ресурсов](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="5a98d-204">**Расположение шаблона**: `URL of hello file`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="5a98d-205">**Ссылка на шаблон**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="5a98d-206">**Ссылка на параметры шаблона**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="5a98d-207">**Переопределение параметров шаблона**: список hello переопределения значений, например: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="5a98d-208">Вставьте особые значения для hello {заполнители}.</span><span class="sxs-lookup"><span data-stu-id="5a98d-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="5a98d-209">**Включить необходимые компоненты**: `Configure with Deployment Group agent`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="5a98d-210">**Конечная точка TFS и VSTS**: выберите **добавить** и в диалоговом окне «Добавить новое подключение службы Team Foundation Server и Team» hello, выберите **токена проверки подлинности на основе**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="5a98d-211">Введите имя соединения, hello и hello URL-адрес командного проекта.</span><span class="sxs-lookup"><span data-stu-id="5a98d-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="5a98d-212">Создает и введите [маркера личных доступа (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello подключения tooyour командного проекта.</span><span class="sxs-lookup"><span data-stu-id="5a98d-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Создание личного маркера доступа](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="5a98d-214">**Командный проект**: выберите свой текущий проект.</span><span class="sxs-lookup"><span data-stu-id="5a98d-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="5a98d-215">**Группа развертывания**: Введите hello одинаковые имена групп развертывания, используемого для hello **группы ресурсов** параметра.</span><span class="sxs-lookup"><span data-stu-id="5a98d-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="5a98d-216">параметры по умолчанию Hello для развертывания группы ресурсов Azure задачу hello toocreate или поэтому добавочное обновление ресурсов и toodo.</span><span class="sxs-lookup"><span data-stu-id="5a98d-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="5a98d-217">Задача Hello создает hello виртуальных машин hello первый раз, он выполняется и впоследствии изменить их.</span><span class="sxs-lookup"><span data-stu-id="5a98d-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="5a98d-218">Настройка задачи «Сценарий» hello</span><span class="sxs-lookup"><span data-stu-id="5a98d-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="5a98d-219">Hello **сценарий** задач является конфигурацией hello используется tooprovide toorun скрипт на каждый сервер tooinstall Node.js и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="5a98d-220">Настройте его следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5a98d-220">Configure it as follows:</span></span>

* <span data-ttu-id="5a98d-221">**Путь к скрипту**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="5a98d-222">**Указать рабочий каталог**: `Checked`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="5a98d-223">**Рабочий каталог**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="5a98d-224">Переименовать и сохранить определение выпуска hello</span><span class="sxs-lookup"><span data-stu-id="5a98d-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="5a98d-225">Измените имя hello hello определения выпуска toohello имя, указанное в **действия после построения** вкладке сборки hello в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="5a98d-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="5a98d-226">При обновлении источника артефактов hello, Jenkins требует может tootrigger каталога toobe это имя нового выпуска.</span><span class="sxs-lookup"><span data-stu-id="5a98d-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="5a98d-227">При необходимости измените имя hello среды hello, щелкнув имя hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="5a98d-228">Щелкните **Сохранить** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="5a98d-229">Запуск развертывания вручную</span><span class="sxs-lookup"><span data-stu-id="5a98d-229">Start a manual deployment</span></span>

1. <span data-ttu-id="5a98d-230">Щелкните **+ Release** (+ Выпуск) и выберите **Создать выпуск**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="5a98d-231">Щелкните завершения построения hello в hello выделенного раскрывающегося списка и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="5a98d-232">Выберите ссылку выпуска hello в всплывающее сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="5a98d-233">Пример: Создан выпуск **Release-1**.</span><span class="sxs-lookup"><span data-stu-id="5a98d-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="5a98d-234">Откройте hello **журналы** вкладке вывод на консоль выпуска toowatch hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="5a98d-235">В браузере, откройте hello URL-адрес одного из серверов hello добавлена группа tooyour развертывания.</span><span class="sxs-lookup"><span data-stu-id="5a98d-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="5a98d-236">Например, введите `http://{your-server-ip-address}`.</span><span class="sxs-lookup"><span data-stu-id="5a98d-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="5a98d-237">Запуск непрерывной интеграции или непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="5a98d-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="5a98d-238">Определение выпуска hello, снимите флажок hello **включено** флажок в hello **параметры управления** hello параметров для развертывания группы ресурсов Azure задачу hello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="5a98d-239">Для будущих развертываний toohello существующего развертывания группы не требуется toore-выполнения этой задачи.</span><span class="sxs-lookup"><span data-stu-id="5a98d-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="5a98d-240">Репозиторий Git источника toohello вернуться и изменить содержимое hello hello **h1** заголовок в файле hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="5a98d-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="5a98d-241">Зафиксируйте изменения.</span><span class="sxs-lookup"><span data-stu-id="5a98d-241">Commit your change.</span></span>

1. <span data-ttu-id="5a98d-242">Через несколько минут вы увидите новый выпуск, созданный в hello **выпуски** страница Team Services или TFS.</span><span class="sxs-lookup"><span data-stu-id="5a98d-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="5a98d-243">Откройте hello выпуска toosee hello развертывания происходит.</span><span class="sxs-lookup"><span data-stu-id="5a98d-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="5a98d-244">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="5a98d-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a98d-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a98d-245">Next Steps</span></span>

<span data-ttu-id="5a98d-246">В этом учебнике автоматизировать развертывание hello tooAzure приложения с помощью сборки Jenkins и Team Services для выпуска.</span><span class="sxs-lookup"><span data-stu-id="5a98d-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="5a98d-247">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5a98d-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a98d-248">Выполнение сборки приложения в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="5a98d-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="5a98d-249">Настройка Jenkins для интеграции с Team Services.</span><span class="sxs-lookup"><span data-stu-id="5a98d-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="5a98d-250">Создание группы развертывания для hello виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="5a98d-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="5a98d-251">Создание определения выпуска, который настраивает hello виртуальных машин и развертывает приложение hello</span><span class="sxs-lookup"><span data-stu-id="5a98d-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="5a98d-252">Дополнительные сведения о как стек LAMP (Linux, Apache, MySQL и PHP) toodeploy приращения Далее учебника toolearn toohello.</span><span class="sxs-lookup"><span data-stu-id="5a98d-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a98d-253">Развертывание стека LAMP</span><span class="sxs-lookup"><span data-stu-id="5a98d-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)