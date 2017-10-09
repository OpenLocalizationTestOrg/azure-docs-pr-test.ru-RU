---
title: "aaaCreate веб-приложение ASP.NET Core в коде Visual Studio"
description: "Этот учебник демонстрирует, как toocreate ASP.NET Core веб-приложения с помощью кода Visual Studio."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="a0d84-103">Создание веб-приложения ASP.NET Core в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a0d84-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="a0d84-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a0d84-104">Overview</span></span>
<span data-ttu-id="a0d84-105">В этом учебнике показано, как toocreate ASP.NET Core веб-приложения с использованием [кода Visual Studio (VS Code)](http://code.visualstudio.com//Docs/whyvscode) и развернуть ее слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="a0d84-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="a0d84-106">Хотя данная статья относится tooweb приложений, также применяется tooAPI приложений и мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="a0d84-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="a0d84-107">ASP.NET Core является существенно переработанной версией ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a0d84-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="a0d84-108">Это новая кроссплатформенная среда с открытым кодом, предназначенная для создания современных облачных веб-приложений с использованием .NET.</span><span class="sxs-lookup"><span data-stu-id="a0d84-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="a0d84-109">Дополнительные сведения см. в разделе [tooASP.NET введение Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="a0d84-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="a0d84-110">Дополнительную информацию о веб-приложениях службы приложений Azure см. в статье [Обзор веб-приложений](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0d84-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="a0d84-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0d84-111">Prerequisites</span></span>
* <span data-ttu-id="a0d84-112">Установка [VSCode](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="a0d84-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="a0d84-113">Установите Git. Можно установить систему с любого из этих сайтов: [Chocolatey](https://chocolatey.org/packages/git) или [git-scm.com](http://git-scm.com/downloads). Если новый tooGit, выберите [git scm.com](http://git-scm.com/downloads) и выберите вариант hello слишком**используйте Git из командной строки Windows hello**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="a0d84-114">После установки Git, вам потребуются имя пользователя Git tooset hello и адрес электронной почты как обязательный далее в учебнике hello (при выполнении фиксации из VS Code).</span><span class="sxs-lookup"><span data-stu-id="a0d84-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="a0d84-115">Установка ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a0d84-115">Install ASP.NET Core</span></span>
<span data-ttu-id="a0d84-116">ASP.NET 5 Core представляют собой простой стек .NET для сборки современных облачных и веб-приложений, работающих в OS X, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="a0d84-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="a0d84-117">Он был создан из hello основание, tooprovide платформу разработки, оптимизированный для приложений, либо облачные развернутой toohello или выполнения в локальной.</span><span class="sxs-lookup"><span data-stu-id="a0d84-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="a0d84-118">Он состоит из модульных компонентов с минимальными служебными данными, что позволяет сохранить гибкость при построении решений.</span><span class="sxs-lookup"><span data-stu-id="a0d84-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="a0d84-119">Этот учебник предназначен спроектированный tooget запущен построение приложений с помощью hello последние разработки версии ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a0d84-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="a0d84-120">Привет, следуя инструкциям, определенных tooWindows.</span><span class="sxs-lookup"><span data-stu-id="a0d84-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="a0d84-121">Инструкции по установке для OS X, Linux и Windows см. в статье [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started) (Начало работы с ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="a0d84-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="a0d84-122">Подробные указания по установке для OS X, Linux и Windows см. в статье об [установке ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="a0d84-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="a0d84-123">Создать веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="a0d84-123">Create hello web app</span></span>
<span data-ttu-id="a0d84-124">В этом разделе показано, как tooscaffold нового приложения ASP.NET, веб-приложения с помощью средства .NET CLI hello.</span><span class="sxs-lookup"><span data-stu-id="a0d84-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="a0d84-125">Введите следующий текст hello в командной строке toocreate hello проект папку и формирования шаблонов hello приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a0d84-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![Интерфейс командной строки .NET — генератор ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="a0d84-127">toorestore hello необходимые пакеты NuGet, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0d84-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="a0d84-128">Запустите веб-приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="a0d84-128">Run hello web app locally</span></span>
<span data-ttu-id="a0d84-129">Теперь, после создания веб-приложения hello и получения все пакеты NuGet hello, приложение hello, hello веб-приложения можно выполнять локально.</span><span class="sxs-lookup"><span data-stu-id="a0d84-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="a0d84-130">Выполните приложение hello (hello `dotnet run` команда выполняет построение приложения hello, когда он является устаревшим):</span><span class="sxs-lookup"><span data-stu-id="a0d84-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="a0d84-131">Откройте браузер и перейдите toohello URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="a0d84-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="a0d84-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="a0d84-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="a0d84-133">страница по умолчанию Hello hello веб-приложения будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a0d84-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Веб-приложение, запущенное локально в браузере](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="a0d84-135">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="a0d84-135">Close your browser.</span></span> <span data-ttu-id="a0d84-136">В hello **командное окно**, нажмите клавишу **Ctrl + C** tooshut работу приложения hello и закрыть hello **командное окно**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="a0d84-137">Создание веб-приложения в hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="a0d84-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="a0d84-138">Hello ниже поможет выполнить создание веб-приложения в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d84-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="a0d84-139">Войдите в toohello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0d84-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a0d84-140">Нажмите кнопку **NEW** на hello верхнего левого угла hello портала.</span><span class="sxs-lookup"><span data-stu-id="a0d84-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="a0d84-141">Щелкните **Веб-приложения > Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-141">Click **Web Apps > Web App**.</span></span>
   
    ![Новое веб-приложение Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="a0d84-143">Введите значение в поле **Имя**, например **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="a0d84-144">Обратите внимание, что это имя должно уникальным toobe портала hello потребует выполнения условия, при попытке имя tooenter hello.</span><span class="sxs-lookup"><span data-stu-id="a0d84-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="a0d84-145">Таким образом, при выборе введите другое значение, вам потребуется toosubstitute это значение для каждого вхождения **SampleWebAppDemo** , отображаемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a0d84-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="a0d84-146">Выберите существующий план службы приложений в поле **План службы приложений** или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="a0d84-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="a0d84-147">При создании нового плана, выберите hello Ценовая категория, расположение и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="a0d84-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="a0d84-148">Дополнительные сведения о планах службы приложений см. в статье hello, [исчерпывающий обзор планы службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0d84-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Колонка нового веб-приложения Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="a0d84-150">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-150">Click **Create**.</span></span>
   
    ![Колонка веб-приложения](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="a0d84-152">Включить публикацию Git для нового веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="a0d84-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="a0d84-153">Git — это система управления распределенных версии, можно использовать toodeploy веб-приложения службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d84-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="a0d84-154">Будут храниться hello код, предназначенный для веб-приложения в локальном репозитории Git и вы развернете tooAzure вашего кода с помощью принудительной отправки tooa удаленный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="a0d84-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="a0d84-155">Войти в hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0d84-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a0d84-156">Щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-156">Click **Browse**.</span></span>
3. <span data-ttu-id="a0d84-157">Нажмите кнопку **веб-приложений** tooview список hello веб-приложений, связанных с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d84-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="a0d84-158">Выберите веб-приложения hello, созданный в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a0d84-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="a0d84-159">В колонке приложения hello web щелкните **параметры** > **непрерывного развертывания**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Хост веб-приложений Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="a0d84-161">Щелкните **Выбор источника > Локальный репозиторий Git**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="a0d84-162">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-162">Click **OK**.</span></span>
   
    ![Локальный репозиторий Git для Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="a0d84-164">Если ранее вы не настроили учетные данные развертывания для публикации веб-приложения или другого приложения службы приложений, сделайте это сейчас, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a0d84-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="a0d84-165">Щелкните **Параметры** > **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="a0d84-166">Hello **задать учетные данные развертывания** отображается колонку.</span><span class="sxs-lookup"><span data-stu-id="a0d84-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="a0d84-167">Укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a0d84-167">Create a user name and password.</span></span>  <span data-ttu-id="a0d84-168">Этот пароль потребуется позднее при настройке Git.</span><span class="sxs-lookup"><span data-stu-id="a0d84-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="a0d84-169">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-169">Click **Save**.</span></span>
9. <span data-ttu-id="a0d84-170">В колонке веб-приложения щелкните **Параметры > Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="a0d84-171">URL-адрес Hello hello удаленный репозиторий Git, вы развернете toois, показанный в разделе **URL-адрес GIT**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="a0d84-172">Копировать hello **URL-адрес GIT** значение для последующего использования в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="a0d84-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![URL-адрес Git для Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="a0d84-174">Публикация вашего web app tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="a0d84-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="a0d84-175">В этом разделе вы создадите локального репозитория Git и push из этого репозитория tooAzure toodeploy вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="a0d84-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="a0d84-176">В VS Code выберите hello **Git** параметр hello левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="a0d84-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Значок Git в VSCode](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="a0d84-178">Выберите **Initialize репозитории** toomake убедиться, что рабочая область — в системе управления версиями git.</span><span class="sxs-lookup"><span data-stu-id="a0d84-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Инициализация Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="a0d84-180">Откройте окно командной строки hello и измените каталог toohello каталоги веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a0d84-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="a0d84-181">Затем введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0d84-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="a0d84-182">Эта команда предотвращает проблемы, связанные с символами конца строк CRLF и LF.</span><span class="sxs-lookup"><span data-stu-id="a0d84-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="a0d84-183">В VS Code, добавьте сообщение фиксации и нажмите кнопку hello **фиксации все** значок галочки.</span><span class="sxs-lookup"><span data-stu-id="a0d84-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![«Фиксировать все» в Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="a0d84-185">После завершения обработки Git, вы увидите, что нет файлов в окно приветствия Git под **изменения**.</span><span class="sxs-lookup"><span data-stu-id="a0d84-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git без изменений](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="a0d84-187">Измените задней toohello окно команд, где командную строку hello указывает каталог toohello где находится веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a0d84-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="a0d84-188">Создайте удаленную ссылку для принудительной отправки обновлений tooyour веб-приложения с помощью hello URL-адрес Git (окончание в «.git»), скопированное ранее.</span><span class="sxs-lookup"><span data-stu-id="a0d84-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="a0d84-189">Настройка Git toosave учетные данные локально, чтобы они будут автоматически добавленных tooyour принудительной команды, сформированные из кода VS.</span><span class="sxs-lookup"><span data-stu-id="a0d84-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="a0d84-190">Принудительно вашей tooAzure изменения, введя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="a0d84-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="a0d84-191">После этого tooAzure начальной принудительной можно будет toodo все принудительной hello команд VS Code.</span><span class="sxs-lookup"><span data-stu-id="a0d84-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="a0d84-192">Запрашивается пароль hello, созданный ранее в Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d84-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="a0d84-193">**Примечание. Ваш пароль не будет отображаться.**</span><span class="sxs-lookup"><span data-stu-id="a0d84-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="a0d84-194">Вывод Hello hello выше команда завершается с сообщением, что развертывание было выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="a0d84-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="a0d84-195">При внесении изменений tooyour приложение можно опубликовать непосредственно в коде VS, с помощью встроенных возможностей Git hello, выбрав hello **зафиксировать все** параметр следуют hello **Push** параметр.</span><span class="sxs-lookup"><span data-stu-id="a0d84-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="a0d84-196">Вы найдете hello **Push** параметр, доступный в toohello Далее раскрывающееся меню hello **зафиксировать все** и **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a0d84-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="a0d84-197">Если вам требуется toocollaborate над проектом, следует помещает tooGitHub между tooAzure принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="a0d84-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="a0d84-198">Выполните приложение hello в Azure</span><span class="sxs-lookup"><span data-stu-id="a0d84-198">Run hello app in Azure</span></span>
<span data-ttu-id="a0d84-199">Теперь, когда развертывания веб-приложения, запустим приложение hello в размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d84-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="a0d84-200">Это можно сделать двумя способами:</span><span class="sxs-lookup"><span data-stu-id="a0d84-200">This can be done in two ways:</span></span>

* <span data-ttu-id="a0d84-201">Откройте браузер и введите имя веб-приложения hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a0d84-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="a0d84-202">В hello портал Azure, найдите колонка приложения hello web для веб-приложения и нажмите кнопку **Обзор** tooview приложения</span><span class="sxs-lookup"><span data-stu-id="a0d84-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="a0d84-203">в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a0d84-203">in your default browser.</span></span>

![Веб-приложение Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="a0d84-205">Сводка</span><span class="sxs-lookup"><span data-stu-id="a0d84-205">Summary</span></span>
<span data-ttu-id="a0d84-206">В этом учебнике вы узнали, как toocreate веб-приложения в VS Code и развернуть ее tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a0d84-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="a0d84-207">Дополнительные сведения о VS Code см. в статье hello, [почему кода на Visual Studio?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="a0d84-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="a0d84-208">Дополнительную информацию о веб-приложениях службы приложений Azure см. в статье [Обзор веб-приложений](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0d84-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

