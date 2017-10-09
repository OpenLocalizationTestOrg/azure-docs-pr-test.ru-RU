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
# <a name="troubleshoot-visual-studio-docker-development"></a>Устранение неполадок при разработке Docker в Visual Studio

При работе с Visual Studio Tools для предварительной версии Docker, могут возникнуть некоторые проблемы из-за характера hello hello предварительного просмотра.
Далее приведены некоторые распространенные проблемы и способы их устранения.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Контейнеры Linux**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>При отладке веб-приложения или консольного приложения .NET Core возникают ошибки сборки.  

Это может быть связанные toonot на диске hello, где находится проект hello Docker для Windows.  Может появиться ошибка hello следующим образом:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve этой проблемы:

1. Щелкните правой кнопкой мыши **Docker для Windows** в hello области уведомлений, а затем выберите **параметры**.  
2. Выберите **общих дисков** и общий доступ к диску hello, где находится проект hello.

### <a name="windows-containers"></a>**Контейнеры Windows**

Hello следующие вопросы, toodebugging конкретных приложений .NET Framework и веб-консоли в контейнерах Windows.

#### <a name="prerequisites"></a>Предварительные требования

1. Версия-Кандидат Visual Studio 2017 г. (или более поздней версии) с hello .NET Core и должен быть установлен Docker Предварительный просмотр рабочей нагрузки.
2. Юбилейное обновление Windows 10 с последними обновлениями и исправлениями для Windows. В частности, должно быть установлено обновление [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016). 
3. Должен быть установлен компонент [Docker для Windows](https://docs.docker.com/docker-for-windows/) (сборка 1.13.0 или более поздней версии).
4. **Переключение контейнеры tooWindows** должен быть выбран. В области уведомлений hello, нажмите кнопку **Docker для Windows**, а затем выберите **переключаться контейнеры tooWindows**. После перезапуска машины hello убедитесь, что данная настройка сохраняется.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>Вывод консоли не отображается в окне вывода Visual Studio при отладке консольного приложения.

Это известная проблема с отладчиком Visual Studio hello (msvsmon.exe), которая в настоящее время не предназначена для этого сценария. Поддержка этого сценария, возможно, будет добавлена в будущем выпуске. Вывод toosee hello консольное приложение в Visual Studio, используйте **Docker: запуск проекта**, что равносильно слишком**Запуск без отладки**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Отладка веб-приложений с hello выпуска конфигурации происходит сбой с ошибкой (403) запрещено

toowork решения этой проблемы откройте web.release.config в решении hello и закомментируйте или удалите hello следующие строки:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Контейнеры Linux**

#### <a name="unable-toovalidate-volume-mapping"></a>Не удается toovalidate тома сопоставления
Сопоставление том является обязательным tooshare hello исходного кода и двоичные файлы приложения в папке приложения hello в контейнере hello.  Определенные сопоставления томов содержатся в файлах docker-compose.dev.debug.yml и docker-compose.dev.release.yml. Как файлы изменяются на хост-компьютере, контейнеры hello отразить эти изменения в аналогичную структуру папок.

сопоставление tooenable тома:

1. Нажмите кнопку **Moby** в области уведомлений hello и выберите **параметры**.
2. Выберите **Shared Drives** (Общие диски).
3. Выберите hello диск, на котором находится где находится % USERPROFILE % проекта и hello диска.
4. Нажмите кнопку **Применить**.

tootest исправности тома сопоставленного перестроить и выберите F5 из среды Visual Studio после одного или нескольких дисков были совместно, или запустите hello после кода из командной строки.

> [!NOTE]
> В этом примере предполагается, что папка Users находится на диске C и что к этому диску предоставлен общий доступ.
> Измените настройки, если общий доступ предоставлен к другому диску.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Запустите следующий код в контейнере Linux hello hello.

```
/ # ls
```

Вы увидите список из hello пользователей и общих папок каталогов. Если файлы не отображаются и папка /c/Users/Public не пустая, значит сопоставление тома настроено неправильно.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Изменить содержимое toohello норки каталога toosee hello объекта hello `/c/Users/Public` каталога:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> При работе с виртуальными машинами Linux hello контейнера файловая система учитывает регистр.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Сборка. Непредвиденная ошибка при выполнении задачи PrepareForBuild

Microsoft.DotNet.Docker.CommandLine.ClientException: Произошла ошибка при попытке tooconnect.

Убедитесь, что этот узел Docker по умолчанию hello работает. Откройте окно командой строки и выполните следующую команду:

```
docker info
```

Если возвращается ошибка, будет пытаться toostart hello **Docker для Windows** классического приложения. Если выполняется классического приложения hello, затем **Moby** должны быть видимыми в области уведомлений hello. Щелкните значок **кита** правой кнопкой мыши и откройте **Settings** (Параметры). Щелкните **Reset** (Сброс) и перезапустите Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Окно сообщения об ошибке возникает при попытке tooadd поддержки Docker или отладки приложения ASP.NET Core в контейнере (F5)

После удаления и установки расширений, могут быть повреждены hello кэша Managed Extensibility Framework (MEF) в Visual Studio. В этом случае можно вызвать различные сообщения об ошибках при добавление поддержки Docker или попытка toorun или отладки приложения ASP.NET Core (F5). Для временного решения проблемы используйте следующие шаги toodelete и повторное создание hello кэш MEF hello.

1. Закройте все экземпляры Visual Studio.
1. Откройте каталог %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Удалите hello следующие папки:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Откройте Visual Studio.
1. Сценарий hello повторите попытку.
