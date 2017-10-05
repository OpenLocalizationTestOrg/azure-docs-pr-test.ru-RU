---
title: "Непрерывное развертывание в службе приложений Azure | Документация Майкрософт"
description: "Узнайте, как включить непрерывное развертывание в службе приложений Azure."
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
ms.openlocfilehash: 7d978e623aaff25a9400090bd3ac18ed560d2ebf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="continuous-deployment-to-azure-app-service"></a><span data-ttu-id="df93e-103">Непрерывное развертывание в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="df93e-103">Continuous Deployment to Azure App Service</span></span>
<span data-ttu-id="df93e-104">В этом руководстве описано, как настроить рабочий процесс непрерывного развертывания для приложения [службы приложений Azure] .</span><span class="sxs-lookup"><span data-stu-id="df93e-104">This tutorial shows you how to configure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="df93e-105">Служба приложений Azure интегрируется с BitBucket, GitHub и [Visual Studio Team Services (VSTS](https://www.visualstudio.com/team-services/)), что обеспечивает непрерывное развертывание, когда Azure извлекает последние обновления из проекта, опубликованные в одной из этих служб.</span><span class="sxs-lookup"><span data-stu-id="df93e-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in the most recent updates from your project published to one of these services.</span></span> <span data-ttu-id="df93e-106">Непрерывное развертывание очень удобно для проектов, которые часто обновляются несколькими участниками.</span><span class="sxs-lookup"><span data-stu-id="df93e-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="df93e-107">Чтобы узнать, как вручную настроить непрерывное развертывание из облачного репозитория, которого нет списке на портале Azure (например, [GitLab](https://gitlab.com/)), см. раздел [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps) (Настройка непрерывного развертывания вручную).</span><span class="sxs-lookup"><span data-stu-id="df93e-107">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="df93e-108"><a name="overview"></a>Включение непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="df93e-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="df93e-109">Чтобы включить непрерывное развертывание, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="df93e-109">To enable continuous deployment,</span></span>

1. <span data-ttu-id="df93e-110">Опубликуйте содержимое приложения в репозиторий, который будет использоваться для непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="df93e-110">Publish your app content to the repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="df93e-111">Дополнительные сведения о публикации проекта в этих службах см. в статьях, посвященных [Create a repo (GitHub)], [Create a repo (BitBucket)] и [началу работы с VSTS].</span><span class="sxs-lookup"><span data-stu-id="df93e-111">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="df93e-112">В колонке меню приложения на [портале Azure] выберите пункт **Развертывание приложения > Параметры развертывания**.</span><span class="sxs-lookup"><span data-stu-id="df93e-112">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="df93e-113">Щелкните **Выбор источника** и укажите источник развертывания.</span><span class="sxs-lookup"><span data-stu-id="df93e-113">Click **Choose Source**, then select the deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="df93e-114">Настроить учетную запись VSTS для развертывания службы приложений можно с помощью этого [руководства](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="df93e-114">To configure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="df93e-115">Пройдите авторизацию.</span><span class="sxs-lookup"><span data-stu-id="df93e-115">Complete the authorization workflow.</span></span>
4. <span data-ttu-id="df93e-116">В колонке **Источник развертывания** выберите проект и ветвь.</span><span class="sxs-lookup"><span data-stu-id="df93e-116">In the **Deployment source** blade, choose the project and branch to deploy from.</span></span> <span data-ttu-id="df93e-117">Закончив, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="df93e-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="df93e-118">При включении непрерывного развертывания с использованием GitHub или BitBucket будут отображаться и открытые, и закрытые проекты.</span><span class="sxs-lookup"><span data-stu-id="df93e-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="df93e-119">Служба приложений создает связь с выбранным репозиторием, извлекает файлы из указанного филиала и поддерживает клон репозитория для приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="df93e-119">App Service creates an association with the selected repository, pulls in the files from the specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="df93e-120">При настройке непрерывного развертывания VSTS на портале Azure для интеграции используется [подсистема развертывания Kudu](https://github.com/projectkudu/kudu/wiki) службы приложений. Она автоматизирует задачи сборки и развертывания при каждом вызове `git push`.</span><span class="sxs-lookup"><span data-stu-id="df93e-120">When you configure VSTS continuous deployment from the Azure portal, the integration uses the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="df93e-121">Настраивать отдельно непрерывное развертывание в VSTS не нужно.</span><span class="sxs-lookup"><span data-stu-id="df93e-121">You do not need to separately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="df93e-122">Когда этот процесс завершится, в колонке **Параметры развертывания** для приложения отобразится активное развертывание.</span><span class="sxs-lookup"><span data-stu-id="df93e-122">After this process completes, the **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="df93e-123">Чтобы проверить развертывание приложения, щелкните **URL-адрес** в верхней части колонки приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="df93e-123">To verify the app is successfully deployed, click the **URL** at the top of the app's blade in the Azure portal.</span></span>
6. <span data-ttu-id="df93e-124">Чтобы убедиться, что непрерывное развертывание выполняется из выбранного репозитория, отправьте в этот репозиторий изменения.</span><span class="sxs-lookup"><span data-stu-id="df93e-124">To verify that continuous deployment is occurring from the repository of your choice, push a change to the repository.</span></span> <span data-ttu-id="df93e-125">Приложение должно обновиться в соответствии с этими изменениями вскоре после их отправки в репозиторий.</span><span class="sxs-lookup"><span data-stu-id="df93e-125">Your app should update to reflect the changes shortly after the push to the repository completes.</span></span> <span data-ttu-id="df93e-126">Проверить применение в приложении соответствующих изменений можно в колонке **Параметры развертывания** для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="df93e-126">You can verify that it has pulled in the update in the **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="df93e-127"><a name="VSsolution"></a>Непрерывное развертывание решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df93e-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="df93e-128">Передача решения Visual Studio в службу приложений Azure не сложнее передачи простого файла index.html.</span><span class="sxs-lookup"><span data-stu-id="df93e-128">Pushing a Visual Studio solution to Azure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="df93e-129">Процесс развертывания службы приложений упрощает выполнение всех операций, включая восстановление зависимостей NuGet и создание двоичных файлов приложения.</span><span class="sxs-lookup"><span data-stu-id="df93e-129">The App Service deployment process streamlines all the details, including restoring NuGet dependencies and building the application binaries.</span></span> <span data-ttu-id="df93e-130">Вы можете воспользоваться практическими рекомендациями по управлению версиями только в репозитории Git, а всем остальным займется процесс развертывания службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="df93e-130">You can follow the source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of the rest.</span></span>

<span data-ttu-id="df93e-131">Операции по передаче решения Visual Studio в службу приложений будут такими же, как в [предыдущем разделе](#overview), если вы настроите решение и репозиторий следующим образом.</span><span class="sxs-lookup"><span data-stu-id="df93e-131">The steps for pushing your Visual Studio solution to App Service are the same as in the [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="df93e-132">С помощью функции управления версиями в Visual Studio создайте файл `.gitignore`, как на рисунке ниже. Или вручную добавьте в корневую папку репозитория файл `.gitignore` с тем же содержимым, что и в [примере GITIGNORE-файла](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="df93e-132">Use the Visual Studio source control option to generate a `.gitignore` file such as the image below or manually add a `.gitignore` file in your repository root with content similar to this [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="df93e-133">Добавьте в репозиторий все дерево каталогов решения с файлом .sln в корневой папке репозитория.</span><span class="sxs-lookup"><span data-stu-id="df93e-133">Add the entire solution's directory tree to your repository, with the .sln file in the repository root.</span></span>

<span data-ttu-id="df93e-134">Настроив, как указано, репозиторий и задав непрерывную публикацию приложения Azure из одного из сетевых репозиториев Git, можно разрабатывать приложение ASP.NET локально в Visual Studio и непрерывно разворачивать свой код путем простой отправки изменений в сетевой репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="df93e-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of the online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes to your online Git repository.</span></span>

## <span data-ttu-id="df93e-135"><a name="disableCD"></a>Отключение непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="df93e-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="df93e-136">Чтобы отключить непрерывное развертывание, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="df93e-136">To disable continuous deployment,</span></span>

1. <span data-ttu-id="df93e-137">В колонке меню приложения на [портале Azure] выберите пункт **Развертывание приложения > Параметры развертывания**.</span><span class="sxs-lookup"><span data-stu-id="df93e-137">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="df93e-138">В колонке **Параметры развертывания** щелкните **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="df93e-138">Then click **Disconnect** in the **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="df93e-139">Ответив **Да** на запрос подтверждения, можно вернуться к колонке приложения, чтобы выбрать **Развертывание приложения > Параметры развертывания**, если вам нужно настроить публикацию из другого источника.</span><span class="sxs-lookup"><span data-stu-id="df93e-139">After answering **Yes** to the confirmation message, you can return to your app's blade and click **APP DEPLOYMENT > Deployment options** if you would like to set up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df93e-140">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="df93e-140">Additional Resources</span></span>
* [<span data-ttu-id="df93e-141">Изучение распространенных проблем с непрерывным развертыванием</span><span class="sxs-lookup"><span data-stu-id="df93e-141">How to investigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="df93e-142">[Использование PowerShell для Azure]</span><span class="sxs-lookup"><span data-stu-id="df93e-142">[How to use PowerShell for Azure]</span></span>
* <span data-ttu-id="df93e-143">[Средства командной строки Azure для Mac и Linux]</span><span class="sxs-lookup"><span data-stu-id="df93e-143">[How to use the Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="df93e-144">[Документация по Git]</span><span class="sxs-lookup"><span data-stu-id="df93e-144">[Git documentation]</span></span>
* [<span data-ttu-id="df93e-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="df93e-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="df93e-146">Использование Azure для автоматического создания конвейера CI/CD для развертывания приложения ASP.NET 4</span><span class="sxs-lookup"><span data-stu-id="df93e-146">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="df93e-147">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="df93e-147">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="df93e-148">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="df93e-148">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="df93e-149">[службы приложений Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="df93e-149">[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span></span>
<span data-ttu-id="df93e-150">[портале Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="df93e-150">[Azure portal]: https://portal.azure.com</span></span>
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="df93e-151">[Использование PowerShell для Azure]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="df93e-151">[How to use PowerShell for Azure]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="df93e-152">[Средства командной строки Azure для Mac и Linux]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="df93e-152">[How to use the Azure Command-Line Tools for Mac and Linux]:../cli-install-nodejs.md</span></span>
<span data-ttu-id="df93e-153">[Документация по Git]: http://git-scm.com/documentation</span><span class="sxs-lookup"><span data-stu-id="df93e-153">[Git Documentation]: http://git-scm.com/documentation</span></span>

<span data-ttu-id="df93e-154">[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo (Создание репозитория GitHub)</span><span class="sxs-lookup"><span data-stu-id="df93e-154">[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo</span></span>
<span data-ttu-id="df93e-155">[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo (Создание репозитория BitBucket)</span><span class="sxs-lookup"><span data-stu-id="df93e-155">[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span></span>
<span data-ttu-id="df93e-156">[началу работы с VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview (Приступая к работе с VSTS)</span><span class="sxs-lookup"><span data-stu-id="df93e-156">[Get started with VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview</span></span>
