---
title: "Журналы и консоль потоковой передачи"
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="8bbeb-103">Журналы потоковой передачи и консоль</span><span class="sxs-lookup"><span data-stu-id="8bbeb-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="8bbeb-104">Журналы потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="8bbeb-104">Streaming Logs</span></span>
<span data-ttu-id="8bbeb-105">**Портал Azure** обеспечивает интегрированный просмотр журналов потоковой передачи, что позволяет просматривать события трассировки из приложений **службы приложений** в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="8bbeb-106">Для настройки этой функции необходимо выполнить несколько простых действий:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="8bbeb-107">Записать трассировки в код.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-107">Write traces in your code</span></span>
* <span data-ttu-id="8bbeb-108">Включить **журналы диагностики** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="8bbeb-109">Просмотреть потоковые данные с помощью встроенного пользовательского интерфейса **журналов передачи** на **портале Azure**.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="8bbeb-110">Порядок записи трассировок в код</span><span class="sxs-lookup"><span data-stu-id="8bbeb-110">How to write traces in your code</span></span>
<span data-ttu-id="8bbeb-111">Запись трассировок в код не представляет никаких сложностей.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="8bbeb-112">В C# это так же просто, как написание следующего кода:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="8bbeb-113">Класс Trace находится в пространстве имен System.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="8bbeb-114">В приложении node.js для достижения того же результата можно написать следующий код:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="8bbeb-115">Порядок включения и просмотра журналов потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="8bbeb-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="8bbeb-116">![][BrowseSitesScreenshot] Диагностика включается отдельно для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="8bbeb-117">Для начала просмотрите сайт, для которого вы хотите включить эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="8bbeb-118">![][DiagnosticsLogs] Прокрутите вниз меню "Параметры" до раздела **Мониторинг** и щелкните **Журналы диагностики** (1).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="8bbeb-119">Затем щелкните **Включить** (2) в разделе **Ведение журнала приложения (файловая система)** или **Ведение журнала приложения (большой двоичный объект)**. Параметр **Уровень** позволяет выбрать уровень серьезности для записи трассировок.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="8bbeb-120">Если вы только знакомитесь с функцией, следует задать значение **Подробно**, так как это обеспечит сбор всех инструкций трассировки.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="8bbeb-121">Нажмите кнопку **СОХРАНИТЬ** в верхней части выноски, теперь все готово для просмотра журналов.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="8bbeb-122">Чем выше **уровень серьезности**, тем больше ресурсов потребляется для ведения журнала и тем больше трассировок записывается в журнал.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="8bbeb-123">Для рабочего сайта или сайта с интенсивным трафиком следует настроить соответствующий **уровень серьезности**.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="8bbeb-124">![][StreamingLogsScreenshot] Для просмотра **журналов передачи** на портале Azure выберите **Поток журналов** (1) в разделе **Мониторинг** меню "Параметры".</span><span class="sxs-lookup"><span data-stu-id="8bbeb-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="8bbeb-125">Если приложение активно записывает инструкции трассировки, то они будут отображаться в **пользовательском интерфейсе журналов передачи** (2) практически в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="8bbeb-126">Консоль</span><span class="sxs-lookup"><span data-stu-id="8bbeb-126">Console</span></span>
<span data-ttu-id="8bbeb-127">**Портал Azure** предоставляет доступ к приложению из консоли.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="8bbeb-128">Вы можете просматривать файловую систему приложения и выполнять сценарии PowerShell или командной строки.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="8bbeb-129">Вам доступен тот же набор разрешений, что и для запуска кода приложения при выполнении команд консоли.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="8bbeb-130">Вы не можете получить доступ к защищенным каталогам или запускать сценарии, требующие повышенного уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="8bbeb-131">![][ConsoleScreenshot] Прокрутите вниз меню "Параметры" до раздела **Средства разработки** и щелкните **Консоль** (1). Справа откроется пользовательский интерфейс **консоли** (2).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="8bbeb-132">Для ознакомления с **консолью** попробуйте выполнить следующие базовые команды:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-132">To get familiar with the **console**, try basic commands like:</span></span>

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
