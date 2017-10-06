---
title: "журналы aaaStreaming и консоли"
description: "Журналы потоковой передачи и общие сведения о консоли"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="b9f31-103">Журналы потоковой передачи и hello консоли</span><span class="sxs-lookup"><span data-stu-id="b9f31-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="b9f31-104">Журналы потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b9f31-104">Streaming Logs</span></span>
<span data-ttu-id="b9f31-105">Hello **портал Azure** предоставляет средство интеграции потоковой передачи просмотра журнала, позволяет просматривать события трассировки из вашего **службы приложений** приложения в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="b9f31-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="b9f31-106">Для настройки этой функции необходимо выполнить несколько простых действий:</span><span class="sxs-lookup"><span data-stu-id="b9f31-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="b9f31-107">Записать трассировки в код.</span><span class="sxs-lookup"><span data-stu-id="b9f31-107">Write traces in your code</span></span>
* <span data-ttu-id="b9f31-108">Включить **журналы диагностики** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="b9f31-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="b9f31-109">Представление потока hello через встроенные hello **журналы потоковой передачи** пользовательский Интерфейс в hello **портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="b9f31-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="b9f31-110">Способ отслеживания toowrite в коде</span><span class="sxs-lookup"><span data-stu-id="b9f31-110">How toowrite traces in your code</span></span>
<span data-ttu-id="b9f31-111">Запись трассировок в код не представляет никаких сложностей.</span><span class="sxs-lookup"><span data-stu-id="b9f31-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="b9f31-112">В C# является максимально упростить написание hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b9f31-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="b9f31-113">класс Trace Hello живет в пространстве имен System.Diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="b9f31-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="b9f31-114">Этот код можно написать в приложении node.js tooachieve hello одинаковый результат:</span><span class="sxs-lookup"><span data-stu-id="b9f31-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="b9f31-115">Здравствуйте как tooenable и Просмотр журналов потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b9f31-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="b9f31-116">![][BrowseSitesScreenshot] Диагностика включается отдельно для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="b9f31-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="b9f31-117">Начните с перехода toohello сайта хотелось бы tooenable эту возможность на.</span><span class="sxs-lookup"><span data-stu-id="b9f31-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="b9f31-118">![][DiagnosticsLogs]Из меню параметров, прокрутите вниз toohello **мониторинг** и нажмите кнопку на **(1) журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="b9f31-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="b9f31-119">Затем **(2) включить** **ведение журнала приложения (файловая система)** или **(blob), ведение журнала приложения** hello **уровень** позволяет изменить hello уровень серьезности toocapture трассировок.</span><span class="sxs-lookup"><span data-stu-id="b9f31-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="b9f31-120">Если вы просто tooget знакомы с функцией hello, установите уровень hello слишком**Verbose** tooensure все операторов трассировки собираются.</span><span class="sxs-lookup"><span data-stu-id="b9f31-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="b9f31-121">Нажмите кнопку **Сохранить** hello верхней части колонки hello и вы будете готовы tooview журналы.</span><span class="sxs-lookup"><span data-stu-id="b9f31-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="b9f31-122">выше hello Hello **уровень серьезности** hello дополнительные ресурсы, обрабатываемом toolog и hello, создаются дополнительные трассировки.</span><span class="sxs-lookup"><span data-stu-id="b9f31-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="b9f31-123">Убедитесь, что **уровень серьезности** является настроенным toohello правильный уровень детализации для производства или сайтов с высоким трафиком.</span><span class="sxs-lookup"><span data-stu-id="b9f31-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="b9f31-124">![][StreamingLogsScreenshot]tooview hello **журналы потоковой передачи** внутри hello портал Azure, выберите на **(1) потока журнала** также в hello **мониторинг** раздел hello параметры меню.</span><span class="sxs-lookup"><span data-stu-id="b9f31-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="b9f31-125">Если приложение активно записывает операторов трассировки, то они должны появляться в hello **(2) потоковой передачи журналов пользовательского интерфейса** почти в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="b9f31-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="b9f31-126">Консоль</span><span class="sxs-lookup"><span data-stu-id="b9f31-126">Console</span></span>
<span data-ttu-id="b9f31-127">Hello **портал Azure** предоставляет tooyour доступа консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="b9f31-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="b9f31-128">Вы можете просматривать файловую систему приложения и выполнять сценарии PowerShell или командной строки.</span><span class="sxs-lookup"><span data-stu-id="b9f31-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="b9f31-129">Ограничиваются hello одинаковые разрешения задан по выполнение кода приложения, при выполнении команд консоли.</span><span class="sxs-lookup"><span data-stu-id="b9f31-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="b9f31-130">Блокируется доступ tooprotected каталогов или выполнение скриптов, которые требуются повышенные разрешения.</span><span class="sxs-lookup"><span data-stu-id="b9f31-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="b9f31-131">![][ConsoleScreenshot]Из меню параметров, прокрутите вниз слишком**средства разработки** раздел и выберите команду **(1) консоли** и hello **(2) консоли** пользовательского интерфейса откроется toohello справа.</span><span class="sxs-lookup"><span data-stu-id="b9f31-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="b9f31-132">Знание hello tooget **консоли**, попробуйте основные команды, такие как:</span><span class="sxs-lookup"><span data-stu-id="b9f31-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
