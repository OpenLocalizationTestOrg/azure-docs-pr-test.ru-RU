---
title: "aaaDebugging приложений в локальном контейнере Docker | Документы Microsoft"
description: "Узнайте, как toomodify приложения, запущенного в локальном контейнере Docker, обновите hello контейнере с помощью изменения и обновления и установите отладочные точки останова"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="f45a7-103">Отладка приложений в локальном контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="f45a7-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="f45a7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f45a7-104">Overview</span></span>
<span data-ttu-id="f45a7-105">Hello Visual Studio Tools для Docker предоставляет согласованный способ toodevelop в и проверка приложения на локальном компьютере в контейнер Linux Docker.</span><span class="sxs-lookup"><span data-stu-id="f45a7-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="f45a7-106">У вас нет контейнера hello toorestart каждый раз при внесении изменений в код.</span><span class="sxs-lookup"><span data-stu-id="f45a7-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="f45a7-107">В этой статье показано, как toouse hello «Изменить и обновить» функция toostart основных компонентов веб-приложение ASP.NET в локальном контейнере Docker, внесите необходимые изменения, а затем обновить браузер toosee hello эти изменения.</span><span class="sxs-lookup"><span data-stu-id="f45a7-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="f45a7-108">В этой статье также показано, как tooset точки останова для отладки.</span><span class="sxs-lookup"><span data-stu-id="f45a7-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="f45a7-109">Поддержка контейнера Windows будет реализована в следующем выпуске.</span><span class="sxs-lookup"><span data-stu-id="f45a7-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f45a7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f45a7-110">Prerequisites</span></span>
<span data-ttu-id="f45a7-111">должны быть установлены следующие средства Hello.</span><span class="sxs-lookup"><span data-stu-id="f45a7-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="f45a7-112">Последняя версия Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f45a7-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="f45a7-113">Установить [пакет SDK для Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122).</span><span class="sxs-lookup"><span data-stu-id="f45a7-113">[Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>

<span data-ttu-id="f45a7-114">toorun контейнеры Docker локально, вам потребуется клиент локальной docker.</span><span class="sxs-lookup"><span data-stu-id="f45a7-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="f45a7-115">Можно использовать hello [элементов Docker](https://www.docker.com/products/docker-toolbox), которого требуется отключить toobe Hyper-V, или можно использовать [Docker для Windows](https://www.docker.com/get-docker), когда используется Hyper-V и требуется Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f45a7-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="f45a7-116">Если с помощью элементов Docker, вам потребуется слишком[настройки клиента Docker hello](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="f45a7-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="f45a7-117">1. Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f45a7-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="f45a7-118">2. Добавление поддержки Docker</span><span class="sxs-lookup"><span data-stu-id="f45a7-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="f45a7-119">3. Изменение и обновление кода</span><span class="sxs-lookup"><span data-stu-id="f45a7-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="f45a7-120">tooquickly перечисления изменений, можно запустить приложение в контейнере и продолжить toomake изменения, их просмотра, как и с IIS Express.</span><span class="sxs-lookup"><span data-stu-id="f45a7-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="f45a7-121">Задать конфигурацию решения hello слишком`Debug` и нажмите клавишу  **&lt;сочетание клавиш CTRL + F5 >** toobuild вашей docker образа и его локального запуска.</span><span class="sxs-lookup"><span data-stu-id="f45a7-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="f45a7-122">Когда образ контейнера hello построен и запущен в контейнер Docker, Visual Studio запустит hello веб-приложение в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f45a7-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="f45a7-123">Если вы используете браузер Microsoft Edge hello или нет ошибок, см. раздел [Устранение неполадок](vs-azure-tools-docker-troubleshooting-docker-errors.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="f45a7-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="f45a7-124">Go toohello о страница, которая является здесь мы увидим toomake изменения.</span><span class="sxs-lookup"><span data-stu-id="f45a7-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="f45a7-125">Возвращает tooVisual Studio и откройте `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f45a7-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="f45a7-126">Добавить hello следующему HTML содержимого toohello конца файла hello и сохранить изменения hello.</span><span class="sxs-lookup"><span data-stu-id="f45a7-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="f45a7-127">Просмотр hello окно вывода, после завершения сборки .NET hello и просмотреть эти строки, перейдите назад tooyour браузера и обновите hello о странице.</span><span class="sxs-lookup"><span data-stu-id="f45a7-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="f45a7-128">Изменения применены!</span><span class="sxs-lookup"><span data-stu-id="f45a7-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="f45a7-129">4. Отладка с использованием точек останова</span><span class="sxs-lookup"><span data-stu-id="f45a7-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="f45a7-130">Часто изменения потребуется дальнейшей проверки, используя hello отладки Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f45a7-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="f45a7-131">Возвращает tooVisual Studio и откройте`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="f45a7-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="f45a7-132">Замените содержимое метода About() hello hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f45a7-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="f45a7-133">Набор toohello останова слева от hello `string message`... строки.</span><span class="sxs-lookup"><span data-stu-id="f45a7-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="f45a7-134">Попаданий  **&lt;F5 >** toostart отладки.</span><span class="sxs-lookup"><span data-stu-id="f45a7-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="f45a7-135">Перейдите в toohello о toohit страницы точка останова.</span><span class="sxs-lookup"><span data-stu-id="f45a7-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="f45a7-136">Переключение точки останова для hello tooview Studio tooVisual и проверьте значение сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="f45a7-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="f45a7-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="f45a7-137">Summary</span></span>
<span data-ttu-id="f45a7-138">С [инструменты Visual Studio 2015 для Docker](https://aka.ms/DockerToolsForVS), вы можете получить hello производительность работы локально, с hello реалистичности рабочей среде разработки в контейнере Docker.</span><span class="sxs-lookup"><span data-stu-id="f45a7-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f45a7-139">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f45a7-139">Troubleshooting</span></span>
[<span data-ttu-id="f45a7-140">Устранение неполадок при разработке в Visual Studio Docker</span><span class="sxs-lookup"><span data-stu-id="f45a7-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="f45a7-141">Дополнительные сведения об использовании Docker с Visual Studio, Windows и Azure</span><span class="sxs-lookup"><span data-stu-id="f45a7-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="f45a7-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) (Инструменты Docker для Visual Studio) — разработка кода .NET Core в контейнере.</span><span class="sxs-lookup"><span data-stu-id="f45a7-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="f45a7-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) (Инструменты Docker для Visual Studio Team Services) — сборка и развертывание контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="f45a7-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="f45a7-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) (Инструменты Docker для Visual Studio Code) — языковые службы для редактирования файлов Docker с дополнительными сценариями E2E (ожидаются в ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="f45a7-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="f45a7-145">[Windows Container Information](http://aka.ms/containers)(Сведения о контейнерах Windows) — сведения о Windows Server и Nano Server.</span><span class="sxs-lookup"><span data-stu-id="f45a7-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="f45a7-146">[Служба контейнеров Azure](https://azure.microsoft.com/services/container-service/)  -  [общие сведения о службе контейнеров Azure](http://aka.ms/AzureContainerService).</span><span class="sxs-lookup"><span data-stu-id="f45a7-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="f45a7-147">Дополнительные примеры работы с Docker см. в разделе [работы с Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) из hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [Демонстрация](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="f45a7-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="f45a7-148">Дополнительные примеры использования из образца hello HealthClinic.biz, в разделе [примеры использования средств разработчика Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="f45a7-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="f45a7-149">Различные инструменты Docker</span><span class="sxs-lookup"><span data-stu-id="f45a7-149">Various Docker tools</span></span>
[<span data-ttu-id="f45a7-150">Some great docker tools (Steve Lasker's blog) (Несколько отличных инструментов Docker — блог Стива Ласкера (Steve Lasker))</span><span class="sxs-lookup"><span data-stu-id="f45a7-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="f45a7-151">Рекомендуемые статьи</span><span class="sxs-lookup"><span data-stu-id="f45a7-151">Good articles</span></span>
[<span data-ttu-id="f45a7-152">Введение tooMicroservices из NGINX</span><span class="sxs-lookup"><span data-stu-id="f45a7-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="f45a7-153">Презентации</span><span class="sxs-lookup"><span data-stu-id="f45a7-153">Presentations</span></span>
* [<span data-ttu-id="f45a7-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Стив Ласкер: презентация по Visual Studio и Docker E2E — Лас-Вегас, 2016 г.)</span><span class="sxs-lookup"><span data-stu-id="f45a7-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="f45a7-155">Введение tooASP.NET Core @ 2016 — когда вы в демонстрационной построения</span><span class="sxs-lookup"><span data-stu-id="f45a7-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="f45a7-156">Developing .NET apps in containers, Channel 9 (Разработка приложений .NET в контейнерах, Channel 9)</span><span class="sxs-lookup"><span data-stu-id="f45a7-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
