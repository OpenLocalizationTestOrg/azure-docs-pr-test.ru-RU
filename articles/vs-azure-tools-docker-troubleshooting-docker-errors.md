---
title: "ошибки клиента aaaTroubleshooting Docker в Windows с помощью Visual Studio | Документы Microsoft"
description: "Устранение неполадок, возникающих при использовании Visual Studio toocreate и развертывание web tooDocker приложений для Windows с помощью Visual Studio."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="5d7c3-103">Устранение неполадок при разработке Docker в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d7c3-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="5d7c3-104">При работе с Visual Studio Tools для предварительной версии Docker, могут возникнуть некоторые проблемы из-за характера hello hello предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="5d7c3-105">Далее приведены некоторые распространенные проблемы и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="5d7c3-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="5d7c3-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="5d7c3-107">**Контейнеры Linux**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="5d7c3-108">При отладке веб-приложения или консольного приложения .NET Core возникают ошибки сборки.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="5d7c3-109">Это может быть связанные toonot на диске hello, где находится проект hello Docker для Windows.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="5d7c3-110">Может появиться ошибка hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="5d7c3-111">tooresolve этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="5d7c3-112">Щелкните правой кнопкой мыши **Docker для Windows** в hello области уведомлений, а затем выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="5d7c3-113">Выберите **общих дисков** и общий доступ к диску hello, где находится проект hello.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="5d7c3-114">**Контейнеры Windows**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-114">**Windows containers**</span></span>

<span data-ttu-id="5d7c3-115">Hello следующие вопросы, toodebugging конкретных приложений .NET Framework и веб-консоли в контейнерах Windows.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="5d7c3-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5d7c3-116">Prerequisites</span></span>

1. <span data-ttu-id="5d7c3-117">Версия-Кандидат Visual Studio 2017 г. (или более поздней версии) с hello .NET Core и должен быть установлен Docker Предварительный просмотр рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="5d7c3-118">Юбилейное обновление Windows 10 с последними обновлениями и исправлениями для Windows.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="5d7c3-119">В частности, должно быть установлено обновление [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="5d7c3-120">Должен быть установлен компонент [Docker для Windows](https://docs.docker.com/docker-for-windows/) (сборка 1.13.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="5d7c3-121">**Переключение контейнеры tooWindows** должен быть выбран.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="5d7c3-122">В области уведомлений hello, нажмите кнопку **Docker для Windows**, а затем выберите **переключаться контейнеры tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="5d7c3-123">После перезапуска машины hello убедитесь, что данная настройка сохраняется.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="5d7c3-124">Вывод консоли не отображается в окне вывода Visual Studio при отладке консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="5d7c3-125">Это известная проблема с отладчиком Visual Studio hello (msvsmon.exe), которая в настоящее время не предназначена для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="5d7c3-126">Поддержка этого сценария, возможно, будет добавлена в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="5d7c3-127">Вывод toosee hello консольное приложение в Visual Studio, используйте **Docker: запуск проекта**, что равносильно слишком**Запуск без отладки**.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="5d7c3-128">Отладка веб-приложений с hello выпуска конфигурации происходит сбой с ошибкой (403) запрещено</span><span class="sxs-lookup"><span data-stu-id="5d7c3-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="5d7c3-129">toowork решения этой проблемы откройте web.release.config в решении hello и закомментируйте или удалите hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="5d7c3-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="5d7c3-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="5d7c3-131">**Контейнеры Linux**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="5d7c3-132">Не удается toovalidate тома сопоставления</span><span class="sxs-lookup"><span data-stu-id="5d7c3-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="5d7c3-133">Сопоставление том является обязательным tooshare hello исходного кода и двоичные файлы приложения в папке приложения hello в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="5d7c3-134">Определенные сопоставления томов содержатся в файлах docker-compose.dev.debug.yml и docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="5d7c3-135">Как файлы изменяются на хост-компьютере, контейнеры hello отразить эти изменения в аналогичную структуру папок.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="5d7c3-136">сопоставление tooenable тома:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="5d7c3-137">Нажмите кнопку **Moby** в области уведомлений hello и выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="5d7c3-138">Выберите **Shared Drives** (Общие диски).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="5d7c3-139">Выберите hello диск, на котором находится где находится % USERPROFILE % проекта и hello диска.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="5d7c3-140">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-140">Click **Apply**.</span></span>

<span data-ttu-id="5d7c3-141">tootest исправности тома сопоставленного перестроить и выберите F5 из среды Visual Studio после одного или нескольких дисков были совместно, или запустите hello после кода из командной строки.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="5d7c3-142">В этом примере предполагается, что папка Users находится на диске C и что к этому диску предоставлен общий доступ.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="5d7c3-143">Измените настройки, если общий доступ предоставлен к другому диску.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="5d7c3-144">Запустите следующий код в контейнере Linux hello hello.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="5d7c3-145">Вы увидите список из hello пользователей и общих папок каталогов.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="5d7c3-146">Если файлы не отображаются и папка /c/Users/Public не пустая, значит сопоставление тома настроено неправильно.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="5d7c3-147">Изменить содержимое toohello норки каталога toosee hello объекта hello `/c/Users/Public` каталога:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="5d7c3-148">При работе с виртуальными машинами Linux hello контейнера файловая система учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="5d7c3-149">Сборка. Непредвиденная ошибка при выполнении задачи PrepareForBuild</span><span class="sxs-lookup"><span data-stu-id="5d7c3-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="5d7c3-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Произошла ошибка при попытке tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="5d7c3-151">Убедитесь, что этот узел Docker по умолчанию hello работает.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="5d7c3-152">Откройте окно командой строки и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="5d7c3-153">Если возвращается ошибка, будет пытаться toostart hello **Docker для Windows** классического приложения.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="5d7c3-154">Если выполняется классического приложения hello, затем **Moby** должны быть видимыми в области уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="5d7c3-155">Щелкните значок **кита** правой кнопкой мыши и откройте **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="5d7c3-156">Щелкните **Reset** (Сброс) и перезапустите Docker.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="5d7c3-157">Окно сообщения об ошибке возникает при попытке tooadd поддержки Docker или отладки приложения ASP.NET Core в контейнере (F5)</span><span class="sxs-lookup"><span data-stu-id="5d7c3-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="5d7c3-158">После удаления и установки расширений, могут быть повреждены hello кэша Managed Extensibility Framework (MEF) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="5d7c3-159">В этом случае можно вызвать различные сообщения об ошибках при добавление поддержки Docker или попытка toorun или отладки приложения ASP.NET Core (F5).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="5d7c3-160">Для временного решения проблемы используйте следующие шаги toodelete и повторное создание hello кэш MEF hello.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="5d7c3-161">Закройте все экземпляры Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="5d7c3-162">Откройте каталог %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="5d7c3-163">Удалите hello следующие папки:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="5d7c3-164">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="5d7c3-165">Сценарий hello повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-165">Attempt hello scenario again.</span></span>
