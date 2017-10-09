---
title: "aaaContinuous tooAzure развертывания службы приложений | Документы Microsoft"
description: "Узнайте, как tooAzure tooenable непрерывного развертывания служб приложений."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="fcc4e-103">TooAzure непрерывного развертывания служб приложений</span><span class="sxs-lookup"><span data-stu-id="fcc4e-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="fcc4e-104">В этом учебнике показано как tooconfigure рабочего процесса непрерывного развертывания для вашего [службе приложений Azure] приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="fcc4e-105">Интеграция служб приложений с BitBucket, GitHub, и [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) позволяет непрерывной рабочий процесс развертывания, где Azure извлекает hello самые последние обновления из проекта опубликованных tooone из этих служб.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="fcc4e-106">Непрерывное развертывание очень удобно для проектов, которые часто обновляются несколькими участниками.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="fcc4e-107">toofind out как tooconfigure непрерывного развертывания вручную из репозитория облака, не перечислен в hello портал Azure (такие как [GitLab](https://gitlab.com/)), в разделе [Настройка непрерывного развертывания, с помощью действий вручную](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="fcc4e-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="fcc4e-108"><a name="overview"></a>Включение непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="fcc4e-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="fcc4e-109">tooenable непрерывного развертывания,</span><span class="sxs-lookup"><span data-stu-id="fcc4e-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="fcc4e-110">Опубликуйте репозиторий содержимого toohello приложения, который будет использоваться для непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="fcc4e-111">Дополнительные сведения о публикации служб toothese проекта см. в разделе [создания репозитория (GitHub)], [создания репозитория (BitBucket)], и [Приступая к работе с VSTS].</span><span class="sxs-lookup"><span data-stu-id="fcc4e-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="fcc4e-112">В колонке меню приложения в hello [портал Azure], нажмите кнопку **развертывание Приложений > варианты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="fcc4e-113">Нажмите кнопку **Выбор источника**, а затем выберите источник развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="fcc4e-114">tooconfigure учетную запись VSTS для развертывания службы приложений см. в разделе это [учебника](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="fcc4e-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="fcc4e-115">Полный рабочий процесс авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="fcc4e-116">В hello **источник развертывания** колонке выберите проект hello и ветвление toodeploy из.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="fcc4e-117">Закончив, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="fcc4e-118">При включении непрерывного развертывания с использованием GitHub или BitBucket будут отображаться и открытые, и закрытые проекты.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="fcc4e-119">Службы приложений создает связь с выбранном репозитории hello, запрашивающий hello файлы из указанной ветви hello и сохраняет копию репозиторий для своего приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="fcc4e-120">При настройке VSTS непрерывного развертывания из hello портал Azure, интеграция hello использует службы приложения hello [подсистема развертывания Kudu](https://github.com/projectkudu/kudu/wiki), который уже автоматизирует задачи построения и развертывания с каждой `git push`.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="fcc4e-121">Нет необходимости tooseparately непрерывное развертывание в VSTS.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="fcc4e-122">После завершения этого процесса hello **варианты развертывания** колонка приложения будет отображаться активное развертывание, указывающее развертывания завершилась успешно.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="fcc4e-123">приложение hello tooverify успешно развернут, нажмите кнопку hello **URL-адрес** hello верхней части колонки приложение hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="fcc4e-124">tooverify, возникающей непрерывного развертывания из репозитория hello по своему усмотрению push репозиторий toohello изменений.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="fcc4e-125">Приложение следует обновить изменения hello tooreflect вскоре после завершения hello принудительной toohello репозитория.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="fcc4e-126">Убедитесь, что он извлечены обновления hello в hello **варианты развертывания** колонке приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="fcc4e-127"><a name="VSsolution"></a>Непрерывное развертывание решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fcc4e-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="fcc4e-128">Помещает tooAzure решения Visual Studio приложения службы — так же просто, как отправить файл index.html простой.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="fcc4e-129">процесс развертывания службы приложения Hello упрощает все сведения о hello, включая восстановление NuGet зависимостей и построения двоичные файлы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="fcc4e-130">Рекомендации по hello источника управления поддержания кода только в репозиторий Git и позволить позаботиться о hello rest развертывания службы приложений.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="fcc4e-131">Hello шаги для принудительной отправки вашего tooApp решения Visual Studio, службы, hello же, как и hello [предыдущего раздела](#overview), предоставленном настройке решения и репозитория следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fcc4e-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="fcc4e-132">Используйте hello Visual Studio исходный элемент управления параметр toogenerate `.gitignore` файла, например hello образ ниже или добавьте вручную `.gitignore` файл в корневом каталоге репозитория с содержимым аналогичные toothis [.gitignore пример](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="fcc4e-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="fcc4e-133">Добавьте репозиторий tooyour дерева каталогов hello всего решения, с hello SLN-файл в корневом хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="fcc4e-134">После настройки вашего хранилища, как описано и настроить приложение в Azure для непрерывной публикации из одного hello online репозиториев Git, можно разрабатывать приложения ASP.NET локально в Visual Studio и постоянно путем простого развертывания вашего кода нажать online репозиторий Git изменения tooyour.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="fcc4e-135"><a name="disableCD"></a>Отключение непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="fcc4e-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="fcc4e-136">toodisable непрерывного развертывания,</span><span class="sxs-lookup"><span data-stu-id="fcc4e-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="fcc4e-137">В колонке меню приложения в hello [портал Azure], нажмите кнопку **развертывание Приложений > варианты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="fcc4e-138">Нажмите кнопку **Disconnect** в hello **варианты развертывания** колонку.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="fcc4e-139">После ответа на **Да** toohello сообщение с подтверждением, можно возвращать колонка tooyour приложения и нажмите кнопку **развертывание Приложений > варианты развертывания** при желании tooset вверх публикации из другого источника.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcc4e-140">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fcc4e-140">Additional Resources</span></span>
* [<span data-ttu-id="fcc4e-141">Как tooinvestigate распространенные проблемы с непрерывным развертыванием</span><span class="sxs-lookup"><span data-stu-id="fcc4e-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="fcc4e-142">[Как toouse PowerShell для Azure]</span><span class="sxs-lookup"><span data-stu-id="fcc4e-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="fcc4e-143">[Как toouse hello средства командной строки Azure для Mac и Linux]</span><span class="sxs-lookup"><span data-stu-id="fcc4e-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="fcc4e-144">[Документация по Git]</span><span class="sxs-lookup"><span data-stu-id="fcc4e-144">[Git documentation]</span></span>
* [<span data-ttu-id="fcc4e-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="fcc4e-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="fcc4e-146">Использовать Azure tooautomatically создания приложении CI/CD конвейера toodeploy ASP.NET 4</span><span class="sxs-lookup"><span data-stu-id="fcc4e-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="fcc4e-147">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fcc4e-148">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="fcc4e-148">No credit cards required; no commitments.</span></span>
> 
> 

[службе приложений Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[портал Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Как toouse PowerShell для Azure]: /powershell/azureps-cmdlets-docs
[Как toouse hello средства командной строки Azure для Mac и Linux]:../cli-install-nodejs.md
[Документация по Git]: http://git-scm.com/documentation

[создания репозитория (GitHub)]: https://help.github.com/articles/create-a-repo (Создание репозитория GitHub)
[создания репозитория (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo (Создание репозитория BitBucket)
[Приступая к работе с VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview (Приступая к работе с VSTS)
