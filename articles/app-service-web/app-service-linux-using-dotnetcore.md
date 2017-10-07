---
title: "aaaUse .NET Core в веб-приложения на платформе Linux | Документы Microsoft"
description: "Использование .NET Core в веб-приложении на платформе Linux."
keywords: "служба приложений azure, веб-приложение, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="8fc71-104">Использование .NET Core в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="8fc71-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="8fc71-105">[Веб-приложение](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) в Linux предоставляет высокомасштабируемых, самостоятельно исправления веб-службы размещения, в операционной системе Linux на hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="8fc71-106">Этот учебник содержит пошаговые инструкции, которые отображаются как toocreate [.NET Core](https://docs.microsoft.com/aspnet/core/) приложения на веб-приложение Azure в Linux.</span><span class="sxs-lookup"><span data-stu-id="8fc71-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Веб-приложения на платформе Linux][10]

<span data-ttu-id="8fc71-108">Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="8fc71-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fc71-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8fc71-109">Prerequisites</span></span> ##

<span data-ttu-id="8fc71-110">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="8fc71-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="8fc71-111">Установка hello [пакета SDK для .NET Core](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="8fc71-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="8fc71-112">Установите [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="8fc71-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="8fc71-113">Создание локального приложения .NET Core</span><span class="sxs-lookup"><span data-stu-id="8fc71-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="8fc71-114">Запустите новый сеанс терминала.</span><span class="sxs-lookup"><span data-stu-id="8fc71-114">Start a new terminal session.</span></span> <span data-ttu-id="8fc71-115">Создайте каталог с именем `hellodotnetcore`и изменить текущий каталог tooit hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="8fc71-116">Затем введите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8fc71-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="8fc71-117">Эта команда создает три файла (*hellodotnetcore.csproj*, *Program.cs*, и *файла Startup.cs*) и одну пустую папку (*wwwroot /*) в текущем каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="8fc71-118">содержимое Hello `.csproj` файл должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8fc71-118">hello content of `.csproj` file should look like hello following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="8fc71-119">Так как это приложение является веб-приложение, tooan ссылку, ASP.NET Core пакет был автоматически добавлен toohello *hellodotnetcore.csproj* файла.</span><span class="sxs-lookup"><span data-stu-id="8fc71-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="8fc71-120">номер версии пакета hello Hello задается в соответствии с выбранной framework toohello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="8fc71-121">В этом примере используется ссылка на ASP.NET Core версии 1.1.2, так как используется .NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="8fc71-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="8fc71-122">Построение и тестирование приложения hello локально</span><span class="sxs-lookup"><span data-stu-id="8fc71-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="8fc71-123">Можно построить и запустить приложение .NET Core с hello `dotnet restore` команды следуют hello `dotnet run` команды, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8fc71-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="8fc71-124">При запуске приложения hello, будет выведено сообщение о том, что приложение hello прослушивает tooincoming запросы по порту.</span><span class="sxs-lookup"><span data-stu-id="8fc71-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="8fc71-125">Протестируйте его путем просмотра слишком`http://localhost:5000/` с браузером.</span><span class="sxs-lookup"><span data-stu-id="8fc71-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="8fc71-126">Если все работает правильно, вы увидите сообщение "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="8fc71-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="8fc71-127">текст hello результат.</span><span class="sxs-lookup"><span data-stu-id="8fc71-127">as hello result text.</span></span>

![Тестирование с помощью браузера][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="8fc71-129">Создать приложение .NET Core на портале Azure hello</span><span class="sxs-lookup"><span data-stu-id="8fc71-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="8fc71-130">Во-первых, требуется toocreate пустой веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="8fc71-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="8fc71-131">Войдите в toohello [портал Azure](https://portal.azure.com/) и создайте новый [веб-приложения на платформе Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="8fc71-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Создание веб-приложения][1]

<span data-ttu-id="8fc71-133">Здравствуйте, когда **создать** откроется страница, содержат сведения о веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="8fc71-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Выбор стека времени выполнения .NET Core][2]

<span data-ttu-id="8fc71-135">Используйте следующие hello таблицы как руководство toofill out hello **создать** , а затем выберите **ОК** и **создать** toocreate приложение hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="8fc71-136">Настройка</span><span class="sxs-lookup"><span data-stu-id="8fc71-136">Setting</span></span>      | <span data-ttu-id="8fc71-137">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="8fc71-137">Suggested value</span></span>  | <span data-ttu-id="8fc71-138">Описание</span><span class="sxs-lookup"><span data-stu-id="8fc71-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="8fc71-139">Имя приложения.</span><span class="sxs-lookup"><span data-stu-id="8fc71-139">App name</span></span> | <span data-ttu-id="8fc71-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="8fc71-140">hellodotnetcore</span></span>  | <span data-ttu-id="8fc71-141">Имя приложения Hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-141">hello name of your app.</span></span> <span data-ttu-id="8fc71-142">Это имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="8fc71-142">This name must be unique.</span></span> |
| <span data-ttu-id="8fc71-143">Подписки</span><span class="sxs-lookup"><span data-stu-id="8fc71-143">Subscription</span></span> | <span data-ttu-id="8fc71-144">Выберите существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="8fc71-144">Choose an existing subscription</span></span> | <span data-ttu-id="8fc71-145">Здравствуйте, подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="8fc71-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="8fc71-146">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="8fc71-146">Resource Group</span></span> | <span data-ttu-id="8fc71-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8fc71-147">myResourceGroup</span></span> |  <span data-ttu-id="8fc71-148">Hello Azure ресурсов группы toocontain hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8fc71-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="8fc71-149">План обслуживания приложения</span><span class="sxs-lookup"><span data-stu-id="8fc71-149">App Service Plan</span></span> | <span data-ttu-id="8fc71-150">Имя существующего плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="8fc71-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="8fc71-151">Здравствуйте, план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="8fc71-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="8fc71-152">Настроить контейнер</span><span class="sxs-lookup"><span data-stu-id="8fc71-152">Configure Container</span></span> | <span data-ttu-id="8fc71-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="8fc71-153">.NET Core 1.1</span></span> | <span data-ttu-id="8fc71-154">Здравствуйте, тип контейнера для этого веб-приложения: встроенные, Docker или частного реестра.</span><span class="sxs-lookup"><span data-stu-id="8fc71-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="8fc71-155">Источник образа</span><span class="sxs-lookup"><span data-stu-id="8fc71-155">Image source</span></span>  | <span data-ttu-id="8fc71-156">Встроены</span><span class="sxs-lookup"><span data-stu-id="8fc71-156">Built-in</span></span>  |  <span data-ttu-id="8fc71-157">Источник Hello hello изображения.</span><span class="sxs-lookup"><span data-stu-id="8fc71-157">hello source of hello image.</span></span> |
| <span data-ttu-id="8fc71-158">Стек времени выполнения</span><span class="sxs-lookup"><span data-stu-id="8fc71-158">Runtime Stack</span></span>  | <span data-ttu-id="8fc71-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="8fc71-159">.NET Core 1.1</span></span>  | <span data-ttu-id="8fc71-160">стек времени выполнения Hello и версии.</span><span class="sxs-lookup"><span data-stu-id="8fc71-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="8fc71-161">Развертывание приложения с помощью Git</span><span class="sxs-lookup"><span data-stu-id="8fc71-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="8fc71-162">Используйте Git toodeploy hello приложения .NET Core tooAzure приложения службы веб-приложения на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="8fc71-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="8fc71-163">Hello новый веб-приложение Azure уже настроена развертывания Git.</span><span class="sxs-lookup"><span data-stu-id="8fc71-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="8fc71-164">URL-адрес развертывания hello Git можно найти, перейдя по toohello следующий URL-адрес после вставки имя вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="8fc71-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="8fc71-165">Hello URL-адрес Git имеет следующие формы, основанной на имя вашего веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="8fc71-166">Выполните следующие команды toodeploy hello локальное приложение tooyour веб-приложение Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8fc71-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="8fc71-167">Не требуется toopush файлами внутри *bin /* или *obj или* каталоги, так как ваше приложение построено в облаке hello при hello приложения исходные файлы помещаются в стек tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8fc71-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="8fc71-168">После завершения процесса построения hello двоичные файлы копируются в каталог приложения hello в */home/сайт/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="8fc71-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="8fc71-169">Убедитесь, что операции удаленного развертывания hello сообщать об успехе.</span><span class="sxs-lookup"><span data-stu-id="8fc71-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="8fc71-170">Принудительной операции может занять некоторое время с момента разрешения пакет и выполняются в облаке hello процесса построения.</span><span class="sxs-lookup"><span data-stu-id="8fc71-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="8fc71-171">Вы увидите несколько сообщений о состоянии, включая сообщения о том, что файлы были скопированы.</span><span class="sxs-lookup"><span data-stu-id="8fc71-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="8fc71-172">Hello вывод должен выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="8fc71-172">hello output should look similar toohello following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="8fc71-173">После завершения развертывания hello, перезапустите веб-приложения для эффекта tootake hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="8fc71-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="8fc71-174">toodo это, перейдите на портал Azure toohello и перейдите toohello **Обзор** страницы веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8fc71-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="8fc71-175">Выберите hello **перезапустите** кнопки странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="8fc71-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="8fc71-176">Когда появится всплывающее окно отображается, выберите **Да** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="8fc71-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="8fc71-177">Затем можно будет перейти к своему веб-приложению, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8fc71-177">You can then browse your web app, as shown here:</span></span>

![Обзор .NET Core развернуто приложение tooAzure службы приложений на платформе Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="8fc71-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fc71-179">Next steps</span></span>
* [<span data-ttu-id="8fc71-180">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="8fc71-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
