---
title: "Создание веб-приложения ASP.NET Core в Visual Studio Code"
description: "В этом руководстве показано, как создать приложение ASP.NET Core, используя Visual Studio Code."
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="03dc4-103">Создание веб-приложения ASP.NET Core в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="03dc4-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="03dc4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="03dc4-104">Overview</span></span>
<span data-ttu-id="03dc4-105">В этом руководстве показано, как создать веб-приложение ASP.NET Core, используя [Visual Studio Code (VSCode)](http://code.visualstudio.com//Docs/whyvscode), и развернуть его в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="03dc4-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="03dc4-106">Хотя эта статья относится к веб-приложениям, она также применима к приложениям API и мобильным приложениям.</span><span class="sxs-lookup"><span data-stu-id="03dc4-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="03dc4-107">ASP.NET Core является существенно переработанной версией ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03dc4-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="03dc4-108">Это новая кроссплатформенная среда с открытым кодом, предназначенная для создания современных облачных веб-приложений с использованием .NET.</span><span class="sxs-lookup"><span data-stu-id="03dc4-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="03dc4-109">Дополнительные сведения см. в статье [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html) (Введение в ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="03dc4-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="03dc4-110">Дополнительную информацию о веб-приложениях службы приложений Azure см. в статье [Обзор веб-приложений](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03dc4-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="03dc4-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="03dc4-111">Prerequisites</span></span>
* <span data-ttu-id="03dc4-112">Установка [VSCode](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="03dc4-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="03dc4-113">Установите Git. Можно установить систему с любого из этих сайтов: [Chocolatey](https://chocolatey.org/packages/git) или [git-scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="03dc4-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="03dc4-114">Если вы еще не работали с Git, выберите [git-scm.com](http://git-scm.com/downloads), а затем параметр **Use Git from the Windows Command Prompt** (Использовать Git из командной строки Windows).</span><span class="sxs-lookup"><span data-stu-id="03dc4-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="03dc4-115">После установки Git также необходимо задать имя пользователя Git и его адрес электронной почты, так как это потребуется далее в этом учебнике (при выполнении фиксации из VSCode).</span><span class="sxs-lookup"><span data-stu-id="03dc4-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="03dc4-116">Установка ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="03dc4-116">Install ASP.NET Core</span></span>
<span data-ttu-id="03dc4-117">ASP.NET 5 Core представляют собой простой стек .NET для сборки современных облачных и веб-приложений, работающих в OS X, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="03dc4-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="03dc4-118">Он был создан с нуля, чтобы предоставить платформу для разработки, оптимизированную для приложений, которые можно разворачивать в облачной или локальной среде.</span><span class="sxs-lookup"><span data-stu-id="03dc4-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="03dc4-119">Он состоит из модульных компонентов с минимальными служебными данными, что позволяет сохранить гибкость при построении решений.</span><span class="sxs-lookup"><span data-stu-id="03dc4-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="03dc4-120">Это руководство позволяет приступить к созданию приложений с помощью последних версий ASP.NET Core для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="03dc4-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="03dc4-121">Приведенные ниже указания относятся только к Windows.</span><span class="sxs-lookup"><span data-stu-id="03dc4-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="03dc4-122">Инструкции по установке для OS X, Linux и Windows см. в статье [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started) (Начало работы с ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="03dc4-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="03dc4-123">Подробные указания по установке для OS X, Linux и Windows см. в статье об [установке ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="03dc4-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="03dc4-124">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="03dc4-124">Create the web app</span></span>
<span data-ttu-id="03dc4-125">В этом разделе показано, как сформировать шаблон нового веб-приложения ASP.NET с помощью инструмента интерфейса командной строки .NET.</span><span class="sxs-lookup"><span data-stu-id="03dc4-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="03dc4-126">Введите следующую команду в командной строке, чтобы создать папку проекта и сформировать шаблон приложения:</span><span class="sxs-lookup"><span data-stu-id="03dc4-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![Интерфейс командной строки .NET — генератор ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="03dc4-128">Чтобы восстановить требуемые пакеты NuGet для запуска следующей команды, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="03dc4-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="03dc4-129">Локальный запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="03dc4-129">Run the web app locally</span></span>
<span data-ttu-id="03dc4-130">Теперь, когда веб-приложение создано и для него получены все пакеты NuGet, можно запустить его локально.</span><span class="sxs-lookup"><span data-stu-id="03dc4-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="03dc4-131">Запустите приложение (команда `dotnet run` выполняет сборку приложения, если оно устарело):</span><span class="sxs-lookup"><span data-stu-id="03dc4-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="03dc4-132">Откройте браузер и перейдите по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="03dc4-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="03dc4-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="03dc4-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="03dc4-134">Страница веб-приложения по умолчанию будет выглядеть так.</span><span class="sxs-lookup"><span data-stu-id="03dc4-134">The default page of the web app will appear as follows.</span></span>
   
    ![Веб-приложение, запущенное локально в браузере](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="03dc4-136">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="03dc4-136">Close your browser.</span></span> <span data-ttu-id="03dc4-137">Нажмите клавиши **CTRL+C** в **командном окне**, чтобы завершить работу приложения и закрыть **командное окно**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="03dc4-138">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="03dc4-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="03dc4-139">Ниже описаны шаги, которые помогут вам создать веб-приложение на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="03dc4-140">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03dc4-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03dc4-141">Щелкните команду **СОЗДАТЬ** в верхнем левом углу портала.</span><span class="sxs-lookup"><span data-stu-id="03dc4-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="03dc4-142">Щелкните **Веб-приложения > Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-142">Click **Web Apps > Web App**.</span></span>
   
    ![Новое веб-приложение Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="03dc4-144">Введите значение в поле **Имя**, например **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="03dc4-145">Обратите внимание, что имя должно быть уникальным. Это обязательное требование, которое будет проверено при вводе.</span><span class="sxs-lookup"><span data-stu-id="03dc4-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="03dc4-146">Если вы введете другое значение, вам необходимо будет заменить им все вхождения **SampleWebAppDemo**, приведенные в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="03dc4-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="03dc4-147">Выберите существующий план службы приложений в поле **План службы приложений** или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="03dc4-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="03dc4-148">При создании нового плана выберите ценовую категорию, расположение и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="03dc4-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="03dc4-149">Дополнительную информацию о планах службы приложений см. в статье [Подробный обзор планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03dc4-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Колонка нового веб-приложения Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="03dc4-151">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-151">Click **Create**.</span></span>
   
    ![Колонка веб-приложения](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="03dc4-153">Включение публикации Git для нового веб-приложения</span><span class="sxs-lookup"><span data-stu-id="03dc4-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="03dc4-154">Git — это распределенная система управления версиями, которую можно использовать для развертывания веб-приложения службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="03dc4-155">Код, созданный для веб-приложения, будет храниться в локальном репозитории Git, а для развертывания кода в Azure он будет передаваться в удаленный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="03dc4-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="03dc4-156">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03dc4-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03dc4-157">Щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-157">Click **Browse**.</span></span>
3. <span data-ttu-id="03dc4-158">Щелкните **Веб-приложения** , чтобы просмотреть список веб-приложений, связанных с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="03dc4-159">Выберите веб-приложение, созданное в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="03dc4-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="03dc4-160">В колонке веб-приложения щелкните **Параметры** > **Непрерывное развертывание**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Хост веб-приложений Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="03dc4-162">Щелкните **Выбор источника > Локальный репозиторий Git**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="03dc4-163">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-163">Click **OK**.</span></span>
   
    ![Локальный репозиторий Git для Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="03dc4-165">Если ранее вы не настроили учетные данные развертывания для публикации веб-приложения или другого приложения службы приложений, сделайте это сейчас, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="03dc4-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="03dc4-166">Щелкните **Параметры** > **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="03dc4-167">Отображается колонка **Установка учетных данных развертывания** .</span><span class="sxs-lookup"><span data-stu-id="03dc4-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="03dc4-168">Укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="03dc4-168">Create a user name and password.</span></span>  <span data-ttu-id="03dc4-169">Этот пароль потребуется позднее при настройке Git.</span><span class="sxs-lookup"><span data-stu-id="03dc4-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="03dc4-170">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-170">Click **Save**.</span></span>
9. <span data-ttu-id="03dc4-171">В колонке веб-приложения щелкните **Параметры > Свойства**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="03dc4-172">В разделе **URL-адрес GIT**отображается URL-адрес удаленного репозитория Git, в который выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="03dc4-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="03dc4-173">Скопируйте значение из поля **URL-АДРЕС GIT** для последующего использования в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="03dc4-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![URL-адрес Git для Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="03dc4-175">Публикация веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="03dc4-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="03dc4-176">В этом разделе вы создадите локальный репозиторий Git и выполните принудительную отправку содержимого из него в Azure, чтобы развернуть веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="03dc4-177">В VSCode выберите параметр **Git** на панели навигации слева.</span><span class="sxs-lookup"><span data-stu-id="03dc4-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Значок Git в VSCode](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="03dc4-179">В VSCode выберите **Инициализировать репозиторий Git** , чтобы задействовать управление версиями Git в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="03dc4-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Инициализация Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="03dc4-181">Откройте командную строку и перейдите в каталог, в котором размещено веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="03dc4-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="03dc4-182">Затем введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="03dc4-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="03dc4-183">Эта команда предотвращает проблемы, связанные с символами конца строк CRLF и LF.</span><span class="sxs-lookup"><span data-stu-id="03dc4-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="03dc4-184">В VSCode добавьте сообщение о фиксации и щелкните значок с галочкой **Фиксировать все** .</span><span class="sxs-lookup"><span data-stu-id="03dc4-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![«Фиксировать все» в Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="03dc4-186">После завершения обработки Git вы увидите, что в окне Git в разделе **Изменения**отсутствуют файлы.</span><span class="sxs-lookup"><span data-stu-id="03dc4-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Git без изменений](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="03dc4-188">Вернитесь обратно в окно командной строки, в котором открыт каталог веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="03dc4-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="03dc4-189">Создайте внешнюю ссылку для отправки обновлений в веб-приложение, используя URL-адрес Git (заканчивающийся на «.git»), скопированный ранее.</span><span class="sxs-lookup"><span data-stu-id="03dc4-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="03dc4-190">Выберите в настройках Git вариант локального хранения учетных данных. Благодаря этому эти данные будут автоматически добавляться в ваши команды отправки, созданные с помощью VS Code.</span><span class="sxs-lookup"><span data-stu-id="03dc4-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="03dc4-191">Отправьте обновления в Azure с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="03dc4-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="03dc4-192">После этой начальной отправки в Azure вы сможете выполнить все команды отправки из VS Code.</span><span class="sxs-lookup"><span data-stu-id="03dc4-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="03dc4-193">Появится запрос на ввод пароля, который вы создали ранее в Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="03dc4-194">**Примечание. Ваш пароль не будет отображаться.**</span><span class="sxs-lookup"><span data-stu-id="03dc4-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="03dc4-195">Вывод этой команды завершается сообщением об успешном развертывании.</span><span class="sxs-lookup"><span data-stu-id="03dc4-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="03dc4-196">При внесении изменений в приложение можно выполнить повторную публикацию непосредственно в VSCode с помощью встроенных функций Git. Для этого выберите **Зафиксировать все**, а затем — **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="03dc4-197">Пункт **Отправить** находится в раскрывающемся меню рядом с кнопками **Зафиксировать все** и **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="03dc4-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="03dc4-198">При совместной работе над проектом рассмотрите возможность отправки изменений в GitHub до отправки в Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="03dc4-199">Запуск приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="03dc4-199">Run the app in Azure</span></span>
<span data-ttu-id="03dc4-200">Теперь, когда веб-приложение развернуто, запустим его в Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="03dc4-201">Это можно сделать двумя способами:</span><span class="sxs-lookup"><span data-stu-id="03dc4-201">This can be done in two ways:</span></span>

* <span data-ttu-id="03dc4-202">Откройте браузер и введите имя веб-приложения в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="03dc4-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="03dc4-203">На портале Azure перейдите к колонке веб-приложения и щелкните **Обзор** для просмотра своего приложения</span><span class="sxs-lookup"><span data-stu-id="03dc4-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="03dc4-204">в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="03dc4-204">in your default browser.</span></span>

![Веб-приложение Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="03dc4-206">Сводка</span><span class="sxs-lookup"><span data-stu-id="03dc4-206">Summary</span></span>
<span data-ttu-id="03dc4-207">В этом учебнике вы узнали, как создавать веб-приложение в VSCode и развертывать его в Azure.</span><span class="sxs-lookup"><span data-stu-id="03dc4-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="03dc4-208">Дополнительную информацию о VS Code см. в разделе [Зачем использовать Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="03dc4-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="03dc4-209">Дополнительную информацию о веб-приложениях службы приложений Azure см. в статье [Обзор веб-приложений](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03dc4-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

