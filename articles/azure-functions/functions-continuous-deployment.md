---
title: "Непрерывное развертывание для Функций Azure | Документация Майкрософт"
description: "Публикация Функций Azure с помощью средств непрерывного развертывания службы приложений Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="4f9bf-103">Непрерывное развертывание для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="4f9bf-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="4f9bf-104">Функции Azure упрощают развертывание приложения-функции за счет непрерывной интеграции службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="4f9bf-105">Компонент функции интегрируется с BitBucket, Dropbox, GitHub и Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="4f9bf-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="4f9bf-106">Это позволяет организовать работу так, чтобы изменения кода функций, вносимые одной из интегрированных служб, активировали развертывание в Azure.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="4f9bf-107">Если вы еще не работали с Функциями Azure, начните с [обзора](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f9bf-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="4f9bf-108">Непрерывное развертывание очень удобно для проектов, которые часто обновляются несколькими участниками.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="4f9bf-109">Этот процесс также обеспечивает поддержку системы управления версиями в коде функций.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="4f9bf-110">В настоящее время поддерживаются следующие источники развертывания:</span><span class="sxs-lookup"><span data-stu-id="4f9bf-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="4f9bf-111">Bitbucket;</span><span class="sxs-lookup"><span data-stu-id="4f9bf-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="4f9bf-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="4f9bf-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="4f9bf-113">Внешний репозиторий (Git или Mercurial)</span><span class="sxs-lookup"><span data-stu-id="4f9bf-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="4f9bf-114">Локальный репозиторий Git</span><span class="sxs-lookup"><span data-stu-id="4f9bf-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="4f9bf-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f9bf-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="4f9bf-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="4f9bf-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="4f9bf-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4f9bf-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="4f9bf-118">Развертывания настраиваются на основе приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="4f9bf-119">После включения непрерывного развертывания доступ к коду функции на портале предоставляется *только для чтения*.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="4f9bf-120">Требования к непрерывному развертыванию</span><span class="sxs-lookup"><span data-stu-id="4f9bf-120">Continuous deployment requirements</span></span>

<span data-ttu-id="4f9bf-121">Перед настройкой непрерывного развертывания нужно настроить источник развертывания и код функций в этом источнике.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="4f9bf-122">В заданном развертывании приложения-функции каждая функция расположена в именованном подкаталоге, где имя каталога соответствует имени функции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="4f9bf-123">Непрерывное развертывание с использованием GIT в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4f9bf-123">Set up continuous deployment</span></span>
<span data-ttu-id="4f9bf-124">Используйте эту процедуру, чтобы настроить непрерывное развертывание для имеющегося приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="4f9bf-125">Здесь показана интеграция с репозиторием GitHub, однако аналогичные действия применяются и для Visual Studio Team Services и других служб развертывания.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="4f9bf-126">В приложении-функции на [портале Azure](https://portal.azure.com) щелкните **Функции платформы** и **Параметры развертывания**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="4f9bf-128">В колонке **Развертывания** щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="4f9bf-130">В колонке **Источник развертывания** щелкните **Выбор источника**, а затем введите сведения о выбранном источнике развертывания и нажмите кнопку **OК**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Выбор источника развертывания](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="4f9bf-132">После настройки непрерывного развертывания все изменения файлов в источнике развертывания копируются в приложение-функцию, и активируется полное развертывание сайта.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="4f9bf-133">После обновления файлов в источнике выполняется повторное развертывание сайта.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="4f9bf-134">Варианты развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-134">Deployment options</span></span>

<span data-ttu-id="4f9bf-135">Ниже приведены некоторые стандартные сценарии развертывания.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="4f9bf-136">Создание промежуточного развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="4f9bf-137">Перемещение имеющихся функций в среду непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="4f9bf-138">Создание промежуточного развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-138">Create a staging deployment</span></span>

<span data-ttu-id="4f9bf-139">В настоящее время приложения-функции не поддерживают слоты развертывания.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="4f9bf-140">Однако промежуточными и рабочими развертываниями можно отдельно управлять с помощью непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="4f9bf-141">Обычно процедура настройки и работа с промежуточным развертыванием выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="4f9bf-142">Создайте в своей подписке два приложения-функции: одно для рабочего кода, а второе для промежуточного.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="4f9bf-143">Создайте источник развертывания, если он еще не создан.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="4f9bf-144">В этом примере используется [GitHub].</span><span class="sxs-lookup"><span data-stu-id="4f9bf-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="4f9bf-145">Для рабочего приложения-функции выполните действия, описанные в разделе **Настройка непрерывного развертывания**, и выберите в качестве ветви развертывания главную ветвь репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Выбор ветви развертывания](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="4f9bf-147">Повторите это действие для промежуточного приложения-функции, но вместо главной ветви выберите промежуточную в своем репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="4f9bf-148">Если источник развертывания не поддерживает ветвление, используйте другую папку.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="4f9bf-149">Обновите код в промежуточной ветви или папке и убедитесь, что эти изменения отражаются в промежуточном развертывании.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="4f9bf-150">После проверки внесите изменения из промежуточной ветви в главную.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="4f9bf-151">Это позволит активировать развертывание в рабочем приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="4f9bf-152">Если источник развертывания не поддерживает ветвление, замените файлы в рабочей папке файлами из промежуточной папки.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="4f9bf-153">Перемещение имеющихся функций в среду непрерывного развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="4f9bf-154">Если вы создали функции и разместили их на портале, прежде чем настроить непрерывное развертывание, как описано выше, необходимо скачать имеющиеся файлы кода функции с помощью FTP или локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="4f9bf-155">Это можно сделать в параметрах службы приложений для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="4f9bf-156">Скачанные файлы можно отправить в выбранный источник непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="4f9bf-157">После настройки непрерывной интеграции исходные файлы больше нельзя изменять на портале функций.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="4f9bf-158">Практическое руководство. Настройка учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="4f9bf-159">Практическое руководство. Скачивание файлов с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="4f9bf-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="4f9bf-160">Практическое руководство. Скачивание файлов с помощью локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="4f9bf-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="4f9bf-161">Практическое руководство. Настройка учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="4f9bf-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="4f9bf-162">Чтобы скачать файлы из приложения-функции с помощью FTP или локального репозитория Git, нужно настроить учетные данные для доступа к сайту.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="4f9bf-163">Учетные данные задаются на уровне приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="4f9bf-164">Чтобы задать учетные данные развертывания на портале Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4f9bf-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="4f9bf-165">В приложении-функции на [портале Azure](https://portal.azure.com) щелкните **Функции платформы** и **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Настройка учетных данных локального развертывания](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="4f9bf-167">Введите имя пользователя и пароль, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="4f9bf-168">Теперь эти учетные данные можно использовать для доступа к приложению-функции из FTP или встроенного репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="4f9bf-169">Практическое руководство. Скачивание файлов с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="4f9bf-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="4f9bf-170">В приложении-функции на [портале функций Azure](https://portal.azure.com) щелкните **Функции платформы** и **Свойства**, а затем скопируйте значения параметров **Пользователь FTP или развертывания**, **Имя узла FTP** и **Имя узла FTPS**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="4f9bf-171">Параметр **Пользователь FTP или развертывания** нужно ввести так, как он отображается на портале, включая имя приложения, чтобы обеспечить правильный контекст для FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Получение сведений о развертывании](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="4f9bf-173">Подключитесь к приложению из клиента FTP, используя полученные сведения, и скачайте исходные файлы функций.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="4f9bf-174">Практическое руководство. Скачивание файлов с помощью локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="4f9bf-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="4f9bf-175">В приложении-функции на [портале Azure](https://portal.azure.com) щелкните **Функции платформы** и **Параметры развертывания**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="4f9bf-177">В колонке **Развертывания** щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="4f9bf-179">В колонке **Источник развертывания** щелкните **Локальный репозиторий Git** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="4f9bf-180">В разделе **Функции платформы**  щелкните **Свойства** и запишите значение URL-адреса репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="4f9bf-182">Клонируйте репозиторий на локальном компьютере с помощью программы командной строки, поддерживающей Git, или одного из средств Git.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="4f9bf-183">Команда git clone выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4f9bf-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="4f9bf-184">Получите удаленный доступ к файлам из приложения-функции в клонированном репозитории файлов на локальном компьютере, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="4f9bf-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="4f9bf-185">При появлении запроса укажите свои [настроенные учетные данные развертывания](#credentials).</span><span class="sxs-lookup"><span data-stu-id="4f9bf-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="4f9bf-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="4f9bf-186">[GitHub]: https://github.com/</span></span>
