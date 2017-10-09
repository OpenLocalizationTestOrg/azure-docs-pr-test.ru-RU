---
title: "aaaConfigure веб-приложений в службе приложений Azure"
description: "Как tooconfigure веб-приложения в службы приложений Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="82b56-103">Настройка веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="82b56-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="82b56-104">В этом разделе объясняется, как веб-приложения с использованием tooconfigure hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="82b56-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="82b56-105">Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="82b56-105">Application settings</span></span>
1. <span data-ttu-id="82b56-106">В hello [портала Azure]откройте колонку hello hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82b56-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="82b56-107">Щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="82b56-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="82b56-108">Щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="82b56-108">Click **Application Settings**.</span></span>

![Параметры приложения][configure01]

<span data-ttu-id="82b56-110">Hello **параметры приложения** колонке имеет параметры, сгруппированный в несколько категорий.</span><span class="sxs-lookup"><span data-stu-id="82b56-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="82b56-111">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="82b56-111">General settings</span></span>
<span data-ttu-id="82b56-112">**Версии Framework**.</span><span class="sxs-lookup"><span data-stu-id="82b56-112">**Framework versions**.</span></span> <span data-ttu-id="82b56-113">Укажите эти параметры, если приложение использует какие-либо из этих инфраструктур разработки:</span><span class="sxs-lookup"><span data-stu-id="82b56-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="82b56-114">**.NET framework**: набор hello платформу .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="82b56-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="82b56-115">**PHP**: версия PHP набор hello, или **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="82b56-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="82b56-116">**Java**: версия Java выберите hello или **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="82b56-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="82b56-117">Используйте hello **контейнера Web** toochoose параметр версий Tomcat и Jetty.</span><span class="sxs-lookup"><span data-stu-id="82b56-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="82b56-118">**Python**: версия Python выберите hello, или **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="82b56-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="82b56-119">По техническим причинам Включение Java для своего приложения отключает параметры .NET, PHP и Python hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="82b56-120"><a name="platform"></a>
**Платформа**.</span><span class="sxs-lookup"><span data-stu-id="82b56-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="82b56-121">Выберите разрядность среды выполнения приложения – 32 или 64 бита.</span><span class="sxs-lookup"><span data-stu-id="82b56-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="82b56-122">64-разрядной среде Hello требует простом и стандартном режимах.</span><span class="sxs-lookup"><span data-stu-id="82b56-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="82b56-123">В 32-разрядной среде режим свободного и общего доступа выполняются всегда.</span><span class="sxs-lookup"><span data-stu-id="82b56-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="82b56-124">**Веб-сокеты**.</span><span class="sxs-lookup"><span data-stu-id="82b56-124">**Web Sockets**.</span></span> <span data-ttu-id="82b56-125">Задать **ON** tooenable hello протокола WebSocket; например, если веб-приложение использует [ASP.NET SignalR] или [socket.io].</span><span class="sxs-lookup"><span data-stu-id="82b56-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="82b56-126"><a name="alwayson"></a>
**Всегда включено**.</span><span class="sxs-lookup"><span data-stu-id="82b56-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="82b56-127">По умолчанию в случае простоя в течение определенного периода времени веб-приложения будут выгружены.</span><span class="sxs-lookup"><span data-stu-id="82b56-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="82b56-128">Это позволяет сэкономить ресурсы системы hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="82b56-129">В простом и стандартном режимах можно включить **Always On** приложение hello tookeep загружены все hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="82b56-130">Если ваше приложение запускается непрерывные веб-задания или запускает веб-заданий запускается с помощью выражения CRON, следует включить **Always On**, или hello веб-задания может не работать надежно.</span><span class="sxs-lookup"><span data-stu-id="82b56-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="82b56-131">**Версия управляемого конвейера**.</span><span class="sxs-lookup"><span data-stu-id="82b56-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="82b56-132">Задает hello IIS [режим конвейера].</span><span class="sxs-lookup"><span data-stu-id="82b56-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="82b56-133">Оставьте это значение tooIntegrated (по умолчанию hello), если у вас есть устаревшие приложения, которое требуется более старая версия служб IIS.</span><span class="sxs-lookup"><span data-stu-id="82b56-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="82b56-134">**Автоматическое переключение**.</span><span class="sxs-lookup"><span data-stu-id="82b56-134">**Auto Swap**.</span></span> <span data-ttu-id="82b56-135">При включении автоматического переключения для слота развертывания службы приложений автоматически поменяет hello веб-приложения в рабочей среде при выполнении отправки разъем toothat обновления.</span><span class="sxs-lookup"><span data-stu-id="82b56-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="82b56-136">Дополнительные сведения см. в разделе [развертывание toostaging слотов для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="82b56-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="82b56-137">Отладка</span><span class="sxs-lookup"><span data-stu-id="82b56-137">Debugging</span></span>
<span data-ttu-id="82b56-138">**Удаленная отладка**.</span><span class="sxs-lookup"><span data-stu-id="82b56-138">**Remote Debugging**.</span></span> <span data-ttu-id="82b56-139">Включение удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="82b56-139">Enables remote debugging.</span></span> <span data-ttu-id="82b56-140">При включении можно использовать hello удаленный отладчик в Visual Studio tooconnect напрямую tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82b56-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="82b56-141">Удаленная отладка останется включенной на 48 часов.</span><span class="sxs-lookup"><span data-stu-id="82b56-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="82b56-142">Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="82b56-142">App settings</span></span>
<span data-ttu-id="82b56-143">Этот раздел содержит пары "имя и значение", которые веб-приложение будет загружать при запуске.</span><span class="sxs-lookup"><span data-stu-id="82b56-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="82b56-144">Для приложений .NET эти параметры вносятся в конфигурацию .NET `AppSettings` во время выполнения, переопределяя текущие настройки.</span><span class="sxs-lookup"><span data-stu-id="82b56-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="82b56-145">Во время выполнения приложения PHP, Python, Java и Node могут обращаться к этим параметрам как к переменным среды.</span><span class="sxs-lookup"><span data-stu-id="82b56-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="82b56-146">Для каждого параметра приложения создаются две переменные среды; одно с указанным путем записи параметров приложения hello, а другой с префиксом APPSETTING_ именем hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="82b56-147">Оба содержат hello одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="82b56-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="82b56-148">Строки подключения</span><span class="sxs-lookup"><span data-stu-id="82b56-148">Connection strings</span></span>
<span data-ttu-id="82b56-149">Строки подключения для связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82b56-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="82b56-150">Для приложений .NET, эти строки подключения будут вноситься в конфигурацию .NET `connectionStrings` параметры во время выполнения, переопределяя существующие записи, где ключ hello, равный hello имя связанной базы данных.</span><span class="sxs-lookup"><span data-stu-id="82b56-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="82b56-151">Для приложений PHP, Python, Java и узел эти параметры будут доступны в виде переменных во время выполнения, с типом соединения hello в качестве префикса.</span><span class="sxs-lookup"><span data-stu-id="82b56-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="82b56-152">префиксы переменных среды Hello выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="82b56-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="82b56-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="82b56-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="82b56-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="82b56-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="82b56-155">База данных SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="82b56-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="82b56-156">Пользовательская: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="82b56-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="82b56-157">Например, если строку подключения MySql были названы `connectionstring1`, оно будет доступно через переменную среды hello `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="82b56-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="82b56-158">Стандартные документы</span><span class="sxs-lookup"><span data-stu-id="82b56-158">Default documents</span></span>
<span data-ttu-id="82b56-159">документ по умолчанию Hello — hello веб-страницу, отображаемую в hello корневой URL-адрес для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="82b56-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="82b56-160">используется первый соответствующий файл Hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="82b56-161">Веб-приложения могут использовать модули, для которых выполняется маршрутизация на основе URL-адреса вместо выдачи статичного содержимого. В таком случае документ по умолчанию не используется.</span><span class="sxs-lookup"><span data-stu-id="82b56-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="82b56-162">Сопоставления обработчиков</span><span class="sxs-lookup"><span data-stu-id="82b56-162">Handler mappings</span></span>
<span data-ttu-id="82b56-163">Используйте этот области tooadd пользовательского скрипта процессоров toohandle запросов для определенных расширений файлов.</span><span class="sxs-lookup"><span data-stu-id="82b56-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="82b56-164">**Расширение**.</span><span class="sxs-lookup"><span data-stu-id="82b56-164">**Extension**.</span></span> <span data-ttu-id="82b56-165">обработать toobe расширение файла Hello, например, *.php или handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="82b56-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="82b56-166">**Путь к обработчику сценариев**.</span><span class="sxs-lookup"><span data-stu-id="82b56-166">**Script Processor Path**.</span></span> <span data-ttu-id="82b56-167">Hello абсолютный путь обработчика скриптов hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="82b56-168">Toofiles запросов, которая соответствует расширению файла hello будут обрабатываться обработчиком сценариев hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="82b56-169">Использование пути к hello `D:\home\site\wwwroot` корневого каталога приложения tooyour toorefer.</span><span class="sxs-lookup"><span data-stu-id="82b56-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="82b56-170">**Дополнительные аргументы**.</span><span class="sxs-lookup"><span data-stu-id="82b56-170">**Additional Arguments**.</span></span> <span data-ttu-id="82b56-171">Необязательные аргументы командной строки для обработчика скриптов hello</span><span class="sxs-lookup"><span data-stu-id="82b56-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="82b56-172">Виртуальные приложения и каталоги</span><span class="sxs-lookup"><span data-stu-id="82b56-172">Virtual applications and directories</span></span>
<span data-ttu-id="82b56-173">tooconfigure виртуальные приложения и каталоги, укажите каждого виртуального каталога и его соответствующий корневой веб-сайт относительный toohello физический путь.</span><span class="sxs-lookup"><span data-stu-id="82b56-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="82b56-174">При необходимости можно выбрать hello **приложения** toomark флажок виртуального каталога, как приложение.</span><span class="sxs-lookup"><span data-stu-id="82b56-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="82b56-175">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="82b56-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="82b56-176">журналы диагностики tooenable:</span><span class="sxs-lookup"><span data-stu-id="82b56-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="82b56-177">В колонке hello веб-приложения, нажмите кнопку **все параметры**.</span><span class="sxs-lookup"><span data-stu-id="82b56-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="82b56-178">Щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="82b56-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="82b56-179">Параметры записи журналов диагноcтики из веб-приложения, поддерживающего ведение журналов.</span><span class="sxs-lookup"><span data-stu-id="82b56-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="82b56-180">**Ведение журнала приложений**.</span><span class="sxs-lookup"><span data-stu-id="82b56-180">**Application Logging**.</span></span> <span data-ttu-id="82b56-181">Записывает журналы приложений toohello файловой системы.</span><span class="sxs-lookup"><span data-stu-id="82b56-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="82b56-182">Ведение журнала продолжается в течение 12 часов.</span><span class="sxs-lookup"><span data-stu-id="82b56-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="82b56-183">**Уровень**.</span><span class="sxs-lookup"><span data-stu-id="82b56-183">**Level**.</span></span> <span data-ttu-id="82b56-184">Если включено ведение журнала приложения, этот параметр указывает hello объем сведений, которые будут записанные (ошибка, предупреждение, сведения или Verbose).</span><span class="sxs-lookup"><span data-stu-id="82b56-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="82b56-185">**Ведение журнала веб-сервера**.</span><span class="sxs-lookup"><span data-stu-id="82b56-185">**Web server logging**.</span></span> <span data-ttu-id="82b56-186">Журналы сохраняются в расширенном формате файлов журналов W3C hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="82b56-187">**Подробные сообщения об ошибках**.</span><span class="sxs-lookup"><span data-stu-id="82b56-187">**Detailed error messages**.</span></span> <span data-ttu-id="82b56-188">Сохраняет HTM-файлы с подробными сведениями об ошибках.</span><span class="sxs-lookup"><span data-stu-id="82b56-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="82b56-189">в разделе /LogFiles/DetailedErrors сохраняются файлы Hello.</span><span class="sxs-lookup"><span data-stu-id="82b56-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="82b56-190">**Трассировка неудачно завершенных запросов**.</span><span class="sxs-lookup"><span data-stu-id="82b56-190">**Failed request tracing**.</span></span> <span data-ttu-id="82b56-191">Журналы сбой tooXML файлов запросов.</span><span class="sxs-lookup"><span data-stu-id="82b56-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="82b56-192">Hello файлы сохраняются в группе/LogFiles/W3SVC*xxx*, где xxx является уникальным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="82b56-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="82b56-193">Эта папка содержит XSL-файл и один или несколько XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="82b56-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="82b56-194">Убедитесь что toodownload hello XSL-файл, так как он предоставляет возможности для форматирования и фильтрации содержимого hello hello XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="82b56-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="82b56-195">файлы журнала tooview hello, необходимо создать учетные данные FTP, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="82b56-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="82b56-196">В колонке hello веб-приложения, нажмите кнопку **все параметры**.</span><span class="sxs-lookup"><span data-stu-id="82b56-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="82b56-197">Щелкните **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="82b56-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="82b56-198">Введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="82b56-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="82b56-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82b56-199">Click **Save**.</span></span>

![Сброс учетных данных развертывания][configure03]

<span data-ttu-id="82b56-201">Hello полное имя пользователя FTP — «app\username», где *приложения* — hello имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82b56-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="82b56-202">Hello имени пользователя в списке в колонке hello web app в разделе **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="82b56-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![Учетные данные развертывания FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="82b56-204">Другие задачи по настройке</span><span class="sxs-lookup"><span data-stu-id="82b56-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="82b56-205">SSL</span><span class="sxs-lookup"><span data-stu-id="82b56-205">SSL</span></span>
<span data-ttu-id="82b56-206">В стандартном и базовом режиме можно загрузить SSL-сертификаты для настраиваемого домена.</span><span class="sxs-lookup"><span data-stu-id="82b56-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="82b56-207">Дополнительные сведения см. в статье [Включение протокола HTTPS для веб-приложения].</span><span class="sxs-lookup"><span data-stu-id="82b56-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="82b56-208">tooview отправленного сертификаты, щелкните **все параметры** > **пользовательские домены и SSL**.</span><span class="sxs-lookup"><span data-stu-id="82b56-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="82b56-209">Имена доменов</span><span class="sxs-lookup"><span data-stu-id="82b56-209">Domain names</span></span>
<span data-ttu-id="82b56-210">Добавление имени личного домена для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82b56-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="82b56-211">Дополнительные сведения см. в статье [Настройка личного доменного имени для веб-приложения в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="82b56-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="82b56-212">Щелкните tooview ваши доменные имена **все параметры** > **пользовательские домены и SSL**.</span><span class="sxs-lookup"><span data-stu-id="82b56-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="82b56-213">Развернутые приложения</span><span class="sxs-lookup"><span data-stu-id="82b56-213">Deployments</span></span>
* <span data-ttu-id="82b56-214">Настройка непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="82b56-214">Set up continuous deployment.</span></span> <span data-ttu-id="82b56-215">В разделе [toodeploy Git с помощью веб-приложений в службе приложений Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="82b56-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="82b56-216">Слоты развертывания.</span><span class="sxs-lookup"><span data-stu-id="82b56-216">Deployment slots.</span></span> <span data-ttu-id="82b56-217">В разделе [развертывания tooStaging сред для веб-приложений в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="82b56-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="82b56-218">tooview вашей слоты развертывания щелкните **все параметры** > **слоты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="82b56-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="82b56-219">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="82b56-219">Monitoring</span></span>
<span data-ttu-id="82b56-220">В простом и стандартном режимах вы можете проверить hello доступности конечных точек HTTP или HTTPS, копирование toothree географически распределенных расположений.</span><span class="sxs-lookup"><span data-stu-id="82b56-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="82b56-221">Тест завершается с ошибкой, если hello код ответа HTTP об ошибке (4xx или 5xx) или hello ответ требуется более 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="82b56-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="82b56-222">Конечная точка считается доступной, если тесты мониторинга hello успешно из всех hello указаны местоположения.</span><span class="sxs-lookup"><span data-stu-id="82b56-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="82b56-223">Дополнительные сведения см. в статье [Практическое руководство: мониторинг состояния конечной веб-точки].</span><span class="sxs-lookup"><span data-stu-id="82b56-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="82b56-224">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений], в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="82b56-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="82b56-225">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="82b56-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="82b56-226">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82b56-226">Next steps</span></span>
* <span data-ttu-id="82b56-227">[Настройка личного доменного имени в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="82b56-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="82b56-228">[Включение протокола HTTPS для приложения в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="82b56-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="82b56-229">[Масштабирование веб-приложения в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="82b56-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="82b56-230">[Основы мониторинга для веб-приложений в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="82b56-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[портала Azure]: https://portal.azure.com/
[Настройка личного доменного имени в службе приложений Azure]: ./app-service-web-tutorial-custom-domain.md
[развертывания tooStaging сред для веб-приложений в службе приложений Azure]: ./web-sites-staged-publishing.md
[Включение протокола HTTPS для приложения в службе приложений Azure]: ./app-service-web-tutorial-custom-ssl.md
[Практическое руководство: мониторинг состояния конечной веб-точки]: http://go.microsoft.com/fwLink/?LinkID=279906
[Основы мониторинга для веб-приложений в службе приложений Azure]: ./web-sites-monitor.md
[режим конвейера]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Масштабирование веб-приложения в службе приложений Azure]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[повторите служб приложений]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
