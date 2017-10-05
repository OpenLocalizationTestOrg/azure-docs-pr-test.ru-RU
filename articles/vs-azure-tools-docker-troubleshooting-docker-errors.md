---
title: "Устранение неполадок клиента Docker в Windows с помощью Visual Studio | Документация Майкрософт"
description: "Устранение неполадок, которые возникают при использовании Visual Studio для создания и развертывания веб-приложений в Docker в Windows с помощью Visual Studio."
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
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="0becd-103">Устранение неполадок при разработке Docker в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0becd-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="0becd-104">При работе с инструментами Visual Studio для предварительной версии Docker могут возникать некоторые проблемы из-за особенностей предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="0becd-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="0becd-105">Далее приведены некоторые распространенные проблемы и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="0becd-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="0becd-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="0becd-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="0becd-107">**Контейнеры Linux**</span><span class="sxs-lookup"><span data-stu-id="0becd-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="0becd-108">При отладке веб-приложения или консольного приложения .NET Core возникают ошибки сборки.</span><span class="sxs-lookup"><span data-stu-id="0becd-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="0becd-109">Это может быть связано с отсутствием общего доступа к диску, на котором расположен проект с Docker для Windows.</span><span class="sxs-lookup"><span data-stu-id="0becd-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="0becd-110">Может появляться сообщение об ошибке следующего вида.</span><span class="sxs-lookup"><span data-stu-id="0becd-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="0becd-111">Действия для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="0becd-111">To resolve this issue:</span></span>

1. <span data-ttu-id="0becd-112">Щелкните правой кнопкой мыши **Docker for Windows** (Docker для Windows) в области уведомлений, а затем выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="0becd-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="0becd-113">Перейдите на вкладку **Shared Drives** (Общие диски) и предоставьте доступ к диску, на котором находится проект.</span><span class="sxs-lookup"><span data-stu-id="0becd-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="0becd-114">**Контейнеры Windows**</span><span class="sxs-lookup"><span data-stu-id="0becd-114">**Windows containers**</span></span>

<span data-ttu-id="0becd-115">Ниже описываются особенности отладки веб-приложений и консольных приложений .NET Framework в контейнерах Windows.</span><span class="sxs-lookup"><span data-stu-id="0becd-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="0becd-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0becd-116">Prerequisites</span></span>

1. <span data-ttu-id="0becd-117">Должна быть установлена Visual Studio 2017 RC (или более поздняя версия) с .NET Core и Docker (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="0becd-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="0becd-118">Юбилейное обновление Windows 10 с последними обновлениями и исправлениями для Windows.</span><span class="sxs-lookup"><span data-stu-id="0becd-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="0becd-119">В частности, должно быть установлено обновление [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016).</span><span class="sxs-lookup"><span data-stu-id="0becd-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="0becd-120">Должен быть установлен компонент [Docker для Windows](https://docs.docker.com/docker-for-windows/) (сборка 1.13.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="0becd-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="0becd-121">Должен быть выбран параметр **Switch to Windows containers** (Переключение на контейнеры Windows).</span><span class="sxs-lookup"><span data-stu-id="0becd-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="0becd-122">В области уведомлений щелкните **Docker for Windows** (Docker для Windows) и выберите **Switch to Windows containers** (Переключение на контейнеры Windows).</span><span class="sxs-lookup"><span data-stu-id="0becd-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="0becd-123">После перезагрузки виртуальной машины убедитесь, что этот параметр остался включенным.</span><span class="sxs-lookup"><span data-stu-id="0becd-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="0becd-124">Вывод консоли не отображается в окне вывода Visual Studio при отладке консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="0becd-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="0becd-125">Это известная проблема отладчика Visual Studio (msvsmon.exe), который сейчас не предназначен для такого использования.</span><span class="sxs-lookup"><span data-stu-id="0becd-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="0becd-126">Поддержка этого сценария, возможно, будет добавлена в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="0becd-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="0becd-127">Для просмотра выходных данных консольного приложения в Visual Studio используйте **Docker: Start Project** (Docker: запустить проект), что эквивалентно операции **Start without Debugging** (Запуск без отладки).</span><span class="sxs-lookup"><span data-stu-id="0becd-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="0becd-128">При отладке веб-приложений в конфигурации выпуска возникает ошибка "(403) Запрещено".</span><span class="sxs-lookup"><span data-stu-id="0becd-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="0becd-129">Чтобы решить эту проблему, откройте файл web.release.config в решении и закомментируйте или удалите приведенные ниже строки.</span><span class="sxs-lookup"><span data-stu-id="0becd-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="0becd-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0becd-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="0becd-131">**Контейнеры Linux**</span><span class="sxs-lookup"><span data-stu-id="0becd-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="0becd-132">Не удалось проверить сопоставление тома</span><span class="sxs-lookup"><span data-stu-id="0becd-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="0becd-133">Сопоставление тома требуется для доступа к исходному коду и двоичным файлам приложения из папки приложения в контейнере.</span><span class="sxs-lookup"><span data-stu-id="0becd-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="0becd-134">Определенные сопоставления томов содержатся в файлах docker-compose.dev.debug.yml и docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="0becd-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="0becd-135">Так как файлы изменяются на хост-компьютере, контейнеры отобразят эти изменения в той же структуре папок.</span><span class="sxs-lookup"><span data-stu-id="0becd-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="0becd-136">Вот как включить сопоставление тома.</span><span class="sxs-lookup"><span data-stu-id="0becd-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="0becd-137">Щелкните значок **кита** в области уведомлений и выберите **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="0becd-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="0becd-138">Выберите **Shared Drives** (Общие диски).</span><span class="sxs-lookup"><span data-stu-id="0becd-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="0becd-139">Выберите диск, на котором размещен ваш проект, и диск, на котором находится профиль пользователя (%USERPROFILE%).</span><span class="sxs-lookup"><span data-stu-id="0becd-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="0becd-140">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="0becd-140">Click **Apply**.</span></span>

<span data-ttu-id="0becd-141">Чтобы проверить, работает ли сопоставление тома, выполните повторную сборку или нажмите клавишу F5 в Visual Studio. Или же выполните следующие команды из командной строки.</span><span class="sxs-lookup"><span data-stu-id="0becd-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="0becd-142">В этом примере предполагается, что папка Users находится на диске C и что к этому диску предоставлен общий доступ.</span><span class="sxs-lookup"><span data-stu-id="0becd-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="0becd-143">Измените настройки, если общий доступ предоставлен к другому диску.</span><span class="sxs-lookup"><span data-stu-id="0becd-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="0becd-144">Выполните следующий код в контейнере Linux.</span><span class="sxs-lookup"><span data-stu-id="0becd-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="0becd-145">Вы должны увидеть список каталогов из папки Users/Public.</span><span class="sxs-lookup"><span data-stu-id="0becd-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="0becd-146">Если файлы не отображаются и папка /c/Users/Public не пустая, значит сопоставление тома настроено неправильно.</span><span class="sxs-lookup"><span data-stu-id="0becd-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="0becd-147">Перейдите в каталог wormhole, чтобы просмотреть содержимое каталога `/c/Users/Public`:</span><span class="sxs-lookup"><span data-stu-id="0becd-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="0becd-148">При работе с виртуальными машинами Linux в файловой системе контейнера учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="0becd-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="0becd-149">Сборка. Непредвиденная ошибка при выполнении задачи PrepareForBuild</span><span class="sxs-lookup"><span data-stu-id="0becd-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="0becd-150">Microsoft.DotNet.Docker.CommandLine.ClientException. Произошла ошибка при попытке подключения.</span><span class="sxs-lookup"><span data-stu-id="0becd-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="0becd-151">Убедитесь, что запущен узел Docker по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0becd-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="0becd-152">Откройте окно командой строки и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0becd-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="0becd-153">Если команда вернет ошибку, попытайтесь запустить классическое приложение **Docker для Windows** .</span><span class="sxs-lookup"><span data-stu-id="0becd-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="0becd-154">При запущенном приложении в области уведомлений должен отображаться значок **кита**.</span><span class="sxs-lookup"><span data-stu-id="0becd-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="0becd-155">Щелкните значок **кита** правой кнопкой мыши и откройте **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="0becd-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="0becd-156">Щелкните **Reset** (Сброс) и перезапустите Docker.</span><span class="sxs-lookup"><span data-stu-id="0becd-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="0becd-157">В контейнере отображается сообщение об ошибке при попытке добавить поддержку Docker или запустить отладку (F5) для приложения ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0becd-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="0becd-158">Иногда после удаления и установки расширений может повреждаться кэш Visual Studio MEF (Managed Extensibility Framework).</span><span class="sxs-lookup"><span data-stu-id="0becd-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="0becd-159">В таком случае могут возникать разные сообщения об ошибках при добавлении поддержки Docker и (или) попытке запустить или выполнить отладку (F5) для приложения ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0becd-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="0becd-160">В качестве временного решения удалите и повторно создайте кэш MEF, используя следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0becd-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="0becd-161">Закройте все экземпляры Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0becd-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="0becd-162">Откройте каталог %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="0becd-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="0becd-163">Удалите следующие папки:</span><span class="sxs-lookup"><span data-stu-id="0becd-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="0becd-164">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0becd-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="0becd-165">Запустите сценарий снова.</span><span class="sxs-lookup"><span data-stu-id="0becd-165">Attempt the scenario again.</span></span>
