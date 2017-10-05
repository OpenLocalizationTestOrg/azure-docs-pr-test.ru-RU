---
title: "Использование .NET Core в веб-приложении на платформе Linux | Документация Майкрософт"
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
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="5e0c2-104">Использование .NET Core в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="5e0c2-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="5e0c2-105">[Веб-приложение](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) в Linux предоставляет масштабируемую службу размещения с самостоятельной установкой исправлений на основе операционной системы Linux.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="5e0c2-106">Это руководство содержит пошаговые инструкции по созданию приложения [.NET Core](https://docs.microsoft.com/aspnet/core/) в виде веб-приложении Azure на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Веб-приложения на платформе Linux][10]

<span data-ttu-id="5e0c2-108">Выполните действия, приведенные ниже, с помощью компьютера Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e0c2-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5e0c2-109">Prerequisites</span></span> ##

<span data-ttu-id="5e0c2-110">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="5e0c2-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="5e0c2-111">Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="5e0c2-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="5e0c2-112">Установите [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="5e0c2-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="5e0c2-113">Создание локального приложения .NET Core</span><span class="sxs-lookup"><span data-stu-id="5e0c2-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="5e0c2-114">Запустите новый сеанс терминала.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-114">Start a new terminal session.</span></span> <span data-ttu-id="5e0c2-115">Создайте каталог `hellodotnetcore` и перейдите в него.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="5e0c2-116">Затем введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="5e0c2-117">Она создает в текущем каталоге три файла (*hellodotnetcore.csproj*, *Program.cs* и *Startup.cs*) и одну пустую папку (*wwwroot*).</span><span class="sxs-lookup"><span data-stu-id="5e0c2-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="5e0c2-118">Содержимое файла с расширением `.csproj` должно выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-118">The content of `.csproj` file should look like the following:</span></span> 

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

<span data-ttu-id="5e0c2-119">Так как это приложение является веб-приложением, ссылка на пакет ASP.NET Core была автоматически добавлена в файл *hellodotnetcore.csproj*.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="5e0c2-120">Номер версии пакета настроен в соответствии с выбранной платформой.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="5e0c2-121">В этом примере используется ссылка на ASP.NET Core версии 1.1.2, так как используется .NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="5e0c2-122">Сборка и тестирование приложения в локальной среде</span><span class="sxs-lookup"><span data-stu-id="5e0c2-122">Build and test the application locally</span></span> ##

<span data-ttu-id="5e0c2-123">Можно выполнить сборку приложения .NET Core, выполнив команду `dotnet restore`, а затем запустить его командой `dotnet run`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="5e0c2-124">При запуске приложения будет отображено сообщение о том, что приложение ожидает передачи входящих запросов через порт.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="5e0c2-125">Протестируйте его, перейдя по адресу `http://localhost:5000/` в браузере.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="5e0c2-126">Если все работает правильно, вы увидите сообщение "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="5e0c2-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="5e0c2-127">после перехода.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-127">as the result text.</span></span>

![Тестирование с помощью браузера][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="5e0c2-129">Создание приложения .NET Core на портале Azure</span><span class="sxs-lookup"><span data-stu-id="5e0c2-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="5e0c2-130">Сначала необходимо создать пустое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-130">First you need to create an empty web app.</span></span> <span data-ttu-id="5e0c2-131">Войдите на [портал Azure](https://portal.azure.com/) и создайте [веб-приложение на платформе Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="5e0c2-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Создание веб-приложения][1]

<span data-ttu-id="5e0c2-133">Когда откроется страница **Создание**, укажите данные веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-133">When the **Create** page opens, provide details about your web app:</span></span>

![Выбор стека времени выполнения .NET Core][2]

<span data-ttu-id="5e0c2-135">Используйте следующую таблицу в качестве руководства по заполнению страницы **Создание**, а затем нажмите кнопки **ОК** и **Создать**, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="5e0c2-136">Настройка</span><span class="sxs-lookup"><span data-stu-id="5e0c2-136">Setting</span></span>      | <span data-ttu-id="5e0c2-137">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="5e0c2-137">Suggested value</span></span>  | <span data-ttu-id="5e0c2-138">Описание</span><span class="sxs-lookup"><span data-stu-id="5e0c2-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="5e0c2-139">Имя приложения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-139">App name</span></span> | <span data-ttu-id="5e0c2-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="5e0c2-140">hellodotnetcore</span></span>  | <span data-ttu-id="5e0c2-141">Имя приложения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-141">The name of your app.</span></span> <span data-ttu-id="5e0c2-142">Это имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-142">This name must be unique.</span></span> |
| <span data-ttu-id="5e0c2-143">Подписки</span><span class="sxs-lookup"><span data-stu-id="5e0c2-143">Subscription</span></span> | <span data-ttu-id="5e0c2-144">Выберите существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-144">Choose an existing subscription</span></span> | <span data-ttu-id="5e0c2-145">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-145">The Azure subscription.</span></span> |
| <span data-ttu-id="5e0c2-146">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="5e0c2-146">Resource Group</span></span> | <span data-ttu-id="5e0c2-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e0c2-147">myResourceGroup</span></span> |  <span data-ttu-id="5e0c2-148">Группа ресурсов Azure, в которую будет помещено веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="5e0c2-149">План обслуживания приложения</span><span class="sxs-lookup"><span data-stu-id="5e0c2-149">App Service Plan</span></span> | <span data-ttu-id="5e0c2-150">Имя существующего плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="5e0c2-151">План службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-151">The App Service plan.</span></span>  |
| <span data-ttu-id="5e0c2-152">Настроить контейнер</span><span class="sxs-lookup"><span data-stu-id="5e0c2-152">Configure Container</span></span> | <span data-ttu-id="5e0c2-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="5e0c2-153">.NET Core 1.1</span></span> | <span data-ttu-id="5e0c2-154">Тип контейнера для этого веб-приложения: "Встроенный", "Docker" или "Частный реестр".</span><span class="sxs-lookup"><span data-stu-id="5e0c2-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="5e0c2-155">Источник образа</span><span class="sxs-lookup"><span data-stu-id="5e0c2-155">Image source</span></span>  | <span data-ttu-id="5e0c2-156">Встроены</span><span class="sxs-lookup"><span data-stu-id="5e0c2-156">Built-in</span></span>  |  <span data-ttu-id="5e0c2-157">Источник образа.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-157">The source of the image.</span></span> |
| <span data-ttu-id="5e0c2-158">Стек времени выполнения</span><span class="sxs-lookup"><span data-stu-id="5e0c2-158">Runtime Stack</span></span>  | <span data-ttu-id="5e0c2-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="5e0c2-159">.NET Core 1.1</span></span>  | <span data-ttu-id="5e0c2-160">Стек времени выполнения и версия.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="5e0c2-161">Развертывание приложения с помощью Git</span><span class="sxs-lookup"><span data-stu-id="5e0c2-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="5e0c2-162">Используете Git для развертывания приложения .NET Core в веб-приложение службы приложений Azure на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="5e0c2-163">Для нового веб-приложения Azure уже настроено развертывание Git.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="5e0c2-164">URL-адрес развертывания Git можно найти, перейдя по приведенному ниже URL-адресу после вставки имение своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="5e0c2-165">URL-адрес Git имеет следующий вид в соответствии с именем вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="5e0c2-166">Выполните следующие команды, чтобы развернуть локальное приложение в веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="5e0c2-167">Не нужно отправлять какие-либо файлы в каталогах *bin /* или *obj/*, так как при размещении исходных файлов приложения в Azure его сборка была выполнена в облаке.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="5e0c2-168">После завершения сборки двоичные файлы копируются в каталог приложения в */home/сайт/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="5e0c2-169">Убедитесь, что операции удаленного развертывания успешно выполнены.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="5e0c2-170">Операции отправки могут занимать некоторое, так как разрешение пакетов и процесс сборки выполняются в облаке.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="5e0c2-171">Вы увидите несколько сообщений о состоянии, включая сообщения о том, что файлы были скопированы.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="5e0c2-172">Результат должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-172">The output should look similar to the following:</span></span>

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
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="5e0c2-173">После завершения развертывания перезапустите веб-приложение, чтобы задействовать развернутую службу.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="5e0c2-174">Для этого войдите на портал Azure перейдите к колонке **Обзор** веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="5e0c2-175">Нажмите кнопку **Перезапустить** на странице.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="5e0c2-176">Когда появится всплывающее окно, щелкните **Да** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="5e0c2-177">Затем можно будет перейти к своему веб-приложению, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5e0c2-177">You can then browse your web app, as shown here:</span></span>

![Обзор приложения .NET Core, развернутого в службе приложений Azure на платформе Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="5e0c2-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e0c2-179">Next steps</span></span>
* [<span data-ttu-id="5e0c2-180">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="5e0c2-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
