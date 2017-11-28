---
title: "aaaContinuous развертывания для функций Azure | Документы Microsoft"
description: "Используйте средства службы приложений Azure toopublish непрерывного развертывания Azure функций."
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
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="e9aa4-103">Непрерывное развертывание для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="e9aa4-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="e9aa4-104">Функции Azure позволяет легко toodeploy функции приложения с помощью непрерывной интеграции служб приложений.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="e9aa4-105">Компонент функции интегрируется с BitBucket, Dropbox, GitHub и Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="e9aa4-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="e9aa4-106">Это обеспечивает рабочий процесс, где кода функции обновления, выполненные с помощью одного из этих tooAzure интегрированные службы триггера развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="e9aa4-107">Если новые функции tooAzure, начните с [Общие сведения о функциях Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9aa4-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="e9aa4-108">Непрерывное развертывание очень удобно для проектов, которые часто обновляются несколькими участниками.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="e9aa4-109">Этот процесс также обеспечивает поддержку системы управления версиями в коде функций.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="e9aa4-110">в настоящее время поддерживаются следующие источники развертывания Hello:</span><span class="sxs-lookup"><span data-stu-id="e9aa4-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="e9aa4-111">Bitbucket;</span><span class="sxs-lookup"><span data-stu-id="e9aa4-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="e9aa4-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="e9aa4-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="e9aa4-113">Внешний репозиторий (Git или Mercurial)</span><span class="sxs-lookup"><span data-stu-id="e9aa4-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="e9aa4-114">Локальный репозиторий Git</span><span class="sxs-lookup"><span data-stu-id="e9aa4-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="e9aa4-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="e9aa4-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="e9aa4-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="e9aa4-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="e9aa4-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="e9aa4-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="e9aa4-118">Развертывания настраиваются на основе приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="e9aa4-119">После включения непрерывного развертывания toofunction код доступа на портале hello задано слишком*только для чтения*.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="e9aa4-120">Требования к непрерывному развертыванию</span><span class="sxs-lookup"><span data-stu-id="e9aa4-120">Continuous deployment requirements</span></span>

<span data-ttu-id="e9aa4-121">Необходимо иметь вашего настроенного источника развертывания и код функции в источнике развертывания hello, прежде чем настраивать непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="e9aa4-122">При развертывании приложения нужной функции в каждой функции живет в именованный подкаталог, где имя каталога hello hello имя функции hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="e9aa4-123">Непрерывное развертывание с использованием GIT в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e9aa4-123">Set up continuous deployment</span></span>
<span data-ttu-id="e9aa4-124">Использование этой процедуры tooconfigure непрерывного развертывания для существующего приложения функции.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="e9aa4-125">Здесь показана интеграция с репозиторием GitHub, однако аналогичные действия применяются и для Visual Studio Team Services и других служб развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="e9aa4-126">В приложении функции в hello [портал Azure](https://portal.azure.com), нажмите кнопку **возможности платформы** и **варианты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="e9aa4-128">Затем в hello **развертываний** колонки щелкните **установки**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="e9aa4-130">В hello **источник развертывания** колонка, щелкните **выбрать источник**, затем заполните hello сведения для выбранного развертывания источника и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Выбор источника развертывания](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="e9aa4-132">После настройки непрерывного развертывания, все изменения файла в источнике развертывания, скопированный toohello функции приложения и развертывания весь сайт запускается.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="e9aa4-133">Hello сайта развертывается при обновлении файлов в исходном hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="e9aa4-134">Варианты развертывания</span><span class="sxs-lookup"><span data-stu-id="e9aa4-134">Deployment options</span></span>

<span data-ttu-id="e9aa4-135">Hello ниже приведены некоторые типичные сценарии развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="e9aa4-136">Создание промежуточного развертывания</span><span class="sxs-lookup"><span data-stu-id="e9aa4-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="e9aa4-137">Перемещение существующего развертывания toocontinuous функции</span><span class="sxs-lookup"><span data-stu-id="e9aa4-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="e9aa4-138">Создание промежуточного развертывания</span><span class="sxs-lookup"><span data-stu-id="e9aa4-138">Create a staging deployment</span></span>

<span data-ttu-id="e9aa4-139">В настоящее время приложения-функции не поддерживают слоты развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="e9aa4-140">Однако промежуточными и рабочими развертываниями можно отдельно управлять с помощью непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="e9aa4-141">Здравствуйте, процесс tooconfigure и работа с промежуточного развертывания обычно выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9aa4-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="e9aa4-142">Создайте два приложения функции в вашей подписки: для рабочего кода hello и для промежуточного хранения.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="e9aa4-143">Создайте источник развертывания, если он еще не создан.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="e9aa4-144">В этом примере используется [GitHub].</span><span class="sxs-lookup"><span data-stu-id="e9aa4-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="e9aa4-145">Для функции на рабочее приложение завершения hello выше шагов **непрерывное развертывание** и набор hello развертывания ветви toohello главную ветвь репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Выбор ветви развертывания](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="e9aa4-147">Повторите этот шаг для промежуточных функции приложения hello, но выбрать hello вместо промежуточной ветвь в репозиторию GitHub.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="e9aa4-148">Если источник развертывания не поддерживает ветвление, используйте другую папку.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="e9aa4-149">Внести в код tooyour обновлений в hello промежуточных ветви или папки, а затем убедитесь, что эти изменения отражаются в промежуточном развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="e9aa4-150">После тестирования, слияние изменений из промежуточной ветви в главную ветвь hello hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="e9aa4-151">Слияние триггеры развертывания toohello рабочей функции приложения.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="e9aa4-152">Если ваш источник развертывания не поддерживает ветвей, перезаписывайте файлы hello в hello рабочей папки с файлами hello в промежуточную папку hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="e9aa4-153">Перемещение существующего развертывания toocontinuous функции</span><span class="sxs-lookup"><span data-stu-id="e9aa4-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="e9aa4-154">При наличии существующих функций, которые созданы и обслуживаются в портал hello необходимо toodownload существующие функции файлы кода, с помощью FTP или hello локального репозитория Git, прежде чем можно настроить непрерывное развертывание, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="e9aa4-155">Это можно сделать в hello параметров приложения службы для функции приложения.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="e9aa4-156">После загрузки файлов, их можно загрузить tooyour выбранного источника непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="e9aa4-157">После настройки непрерывная интеграция не будет возможности tooedit файлов источника на портале функции hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="e9aa4-158">Практическое руководство. Настройка учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="e9aa4-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="e9aa4-159">Практическое руководство. Скачивание файлов с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="e9aa4-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="e9aa4-160">Как: загрузка файлов с помощью hello локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="e9aa4-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="e9aa4-161">Практическое руководство. Настройка учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="e9aa4-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="e9aa4-162">Перед загрузкой файлов из приложения функция через FTP или локальный репозиторий Git, необходимо настроить сайт hello tooaccess учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="e9aa4-163">Учетные данные задаются на уровне приложения функции hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="e9aa4-164">Используйте следующие шаги tooset учетные данные развертывания hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="e9aa4-165">В приложении функции в hello [портал Azure](https://portal.azure.com), нажмите кнопку **возможности платформы** и **учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Настройка учетных данных локального развертывания](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="e9aa4-167">Введите имя пользователя и пароль, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="e9aa4-168">Теперь можно использовать эти учетные данные tooaccess функции приложения из FTP или hello встроенного репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="e9aa4-169">Практическое руководство. Скачивание файлов с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="e9aa4-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="e9aa4-170">В приложении функции в hello [портал Azure](https://portal.azure.com), нажмите кнопку **возможности платформы** и **свойства**, скопируйте значения hello для **пользователя FTP или развертывание**, **Имя узла FTP**, и **имя узла FTPS**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="e9aa4-171">**Пользователь FTP или развертывание** должны вводиться, показанной в портал hello, включая имя приложения hello, tooprovide правильный контекст для hello FTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Получение сведений о развертывании](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="e9aa4-173">В клиентском приложении FTP используйте hello приложения tooyour tooconnect собранные сведения о подключении и загрузки hello исходных файлов для функций.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="e9aa4-174">Практическое руководство. Скачивание файлов с помощью локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="e9aa4-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="e9aa4-175">В приложении функции в hello [портал Azure](https://portal.azure.com), нажмите кнопку **возможности платформы** и **варианты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="e9aa4-177">Затем в hello **развертываний** колонки щелкните **установки**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="e9aa4-179">В hello **источник развертывания** колонка, щелкните **локального репозитория Git** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="e9aa4-180">В **возможности платформы**, нажмите кнопку **свойства** и запишите значение hello URL-адрес Git.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Настройка непрерывного развертывания](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="e9aa4-182">Клонирование репозитория hello на локальном компьютере, используя командную строку Git виду или избранный инструмент Git.</span><span class="sxs-lookup"><span data-stu-id="e9aa4-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="e9aa4-183">Hello Git клон команды выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9aa4-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="e9aa4-184">Получения файлов из клона toohello функции приложения на локальном компьютере, как и hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e9aa4-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="e9aa4-185">При появлении запроса укажите свои [настроенные учетные данные развертывания](#credentials).</span><span class="sxs-lookup"><span data-stu-id="e9aa4-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
