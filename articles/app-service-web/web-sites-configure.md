---
title: "Настройка веб-приложений в службе приложений Azure"
description: "Настройка веб-приложения в службе приложений Azure"
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
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="424ae-103">Настройка веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="424ae-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="424ae-104">В этом разделе рассматривается настройка веб-приложения с помощью [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="424ae-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="424ae-105">Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="424ae-105">Application settings</span></span>
1. <span data-ttu-id="424ae-106">На [портале Azure]откройте колонку для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="424ae-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="424ae-107">Щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="424ae-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="424ae-108">Щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="424ae-108">Click **Application Settings**.</span></span>

![Параметры приложения][configure01]

<span data-ttu-id="424ae-110">В колонке **Параметры приложения** параметры сгруппированы по нескольким категориям.</span><span class="sxs-lookup"><span data-stu-id="424ae-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="424ae-111">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="424ae-111">General settings</span></span>
<span data-ttu-id="424ae-112">**Версии Framework**.</span><span class="sxs-lookup"><span data-stu-id="424ae-112">**Framework versions**.</span></span> <span data-ttu-id="424ae-113">Укажите эти параметры, если приложение использует какие-либо из этих инфраструктур разработки:</span><span class="sxs-lookup"><span data-stu-id="424ae-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="424ae-114">**.NET Framework**: укажите версию .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="424ae-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="424ae-115">**PHP**: укажите версию PHP или установите значение **Выключено**, чтобы отключить PHP.</span><span class="sxs-lookup"><span data-stu-id="424ae-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="424ae-116">**Java**: выберите версию Java или задайте **Выключено**, чтобы отключить Java.</span><span class="sxs-lookup"><span data-stu-id="424ae-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="424ae-117">Используйте параметр **Веб-контейнер** , чтобы выбрать версию Tomcat или Jetty.</span><span class="sxs-lookup"><span data-stu-id="424ae-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="424ae-118">**Python**: выберите версию Python или задайте **Выключено**, чтобы отключить Python.</span><span class="sxs-lookup"><span data-stu-id="424ae-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="424ae-119">По техническим причинам включение Java для веб-приложения отключает использование .NET, PHP и Python.</span><span class="sxs-lookup"><span data-stu-id="424ae-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="424ae-120"><a name="platform"></a>
**Платформа**.</span><span class="sxs-lookup"><span data-stu-id="424ae-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="424ae-121">Выберите разрядность среды выполнения приложения – 32 или 64 бита.</span><span class="sxs-lookup"><span data-stu-id="424ae-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="424ae-122">Для 64-битной среды требуется режим "Базовый" или "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="424ae-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="424ae-123">В 32-разрядной среде режим свободного и общего доступа выполняются всегда.</span><span class="sxs-lookup"><span data-stu-id="424ae-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="424ae-124">**Веб-сокеты**.</span><span class="sxs-lookup"><span data-stu-id="424ae-124">**Web Sockets**.</span></span> <span data-ttu-id="424ae-125">Установите значение **Включено**, чтобы разрешить использование протокола WebSocket (например, если ваше веб-приложение использует [ASP.NET SignalR] или [socket.io]).</span><span class="sxs-lookup"><span data-stu-id="424ae-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="424ae-126"><a name="alwayson"></a>
**Всегда включено**.</span><span class="sxs-lookup"><span data-stu-id="424ae-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="424ae-127">По умолчанию в случае простоя в течение определенного периода времени веб-приложения будут выгружены.</span><span class="sxs-lookup"><span data-stu-id="424ae-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="424ae-128">Это позволяет сэкономить системные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="424ae-128">This lets the system conserve resources.</span></span> <span data-ttu-id="424ae-129">В режиме Basic и Standard вы можете включить функцию **Всегда включено** , чтобы приложение постоянно оставалось загруженным.</span><span class="sxs-lookup"><span data-stu-id="424ae-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="424ae-130">Если приложение выполняет непрерывные веб-задания или веб-задания, активированные с помощью выражения CRON, следует включить функцию **Всегда включено**, иначе веб-задания не будут выполняться правильно.</span><span class="sxs-lookup"><span data-stu-id="424ae-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="424ae-131">**Версия управляемого конвейера**.</span><span class="sxs-lookup"><span data-stu-id="424ae-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="424ae-132">Задает [режим конвейера]IIS.</span><span class="sxs-lookup"><span data-stu-id="424ae-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="424ae-133">Оставьте здесь значение "Интегрированный" (по умолчанию), кроме тех случаев, когда имеется устаревшее веб-приложение, для которого требуется предыдущая версия IIS.</span><span class="sxs-lookup"><span data-stu-id="424ae-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="424ae-134">**Автоматическое переключение**.</span><span class="sxs-lookup"><span data-stu-id="424ae-134">**Auto Swap**.</span></span> <span data-ttu-id="424ae-135">При включении автоматического переключения для слота развертывания служба приложений будет автоматически переводить веб-приложение в рабочий режим после каждого обновления в этом слоте.</span><span class="sxs-lookup"><span data-stu-id="424ae-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="424ae-136">Дополнительную информацию см. в статье [Развертывание промежуточных слотов для веб-приложений в службе приложения Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="424ae-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="424ae-137">Отладка</span><span class="sxs-lookup"><span data-stu-id="424ae-137">Debugging</span></span>
<span data-ttu-id="424ae-138">**Удаленная отладка**.</span><span class="sxs-lookup"><span data-stu-id="424ae-138">**Remote Debugging**.</span></span> <span data-ttu-id="424ae-139">Включение удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="424ae-139">Enables remote debugging.</span></span> <span data-ttu-id="424ae-140">Если этот параметр включен, вы можете использовать удаленный отладчик Visual Studio для прямого подключения к веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="424ae-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="424ae-141">Удаленная отладка останется включенной на 48 часов.</span><span class="sxs-lookup"><span data-stu-id="424ae-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="424ae-142">Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="424ae-142">App settings</span></span>
<span data-ttu-id="424ae-143">Этот раздел содержит пары "имя и значение", которые веб-приложение будет загружать при запуске.</span><span class="sxs-lookup"><span data-stu-id="424ae-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="424ae-144">Для приложений .NET эти параметры вносятся в конфигурацию .NET `AppSettings` во время выполнения, переопределяя текущие настройки.</span><span class="sxs-lookup"><span data-stu-id="424ae-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="424ae-145">Во время выполнения приложения PHP, Python, Java и Node могут обращаться к этим параметрам как к переменным среды.</span><span class="sxs-lookup"><span data-stu-id="424ae-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="424ae-146">Для каждого параметра приложения создаются две переменные среды: одна с именем, указанным в параметре приложения, и другая с префиксом APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="424ae-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="424ae-147">Обе содержат одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="424ae-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="424ae-148">Строки подключения</span><span class="sxs-lookup"><span data-stu-id="424ae-148">Connection strings</span></span>
<span data-ttu-id="424ae-149">Строки подключения для связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="424ae-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="424ae-150">Для приложений .NET эти строки подключения будут внесены в параметры конфигурации .NET `connectionStrings` во время выполнения, переопределяя имеющиеся записи, для которых значение ключа равно имени связанной базы данных.</span><span class="sxs-lookup"><span data-stu-id="424ae-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="424ae-151">Для приложений PHP, Python, Java и Node эти параметры будут доступны во время выполнения в виде переменных среды. В качестве префикса будет использоваться тип подключения.</span><span class="sxs-lookup"><span data-stu-id="424ae-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="424ae-152">Префиксы переменных среды:</span><span class="sxs-lookup"><span data-stu-id="424ae-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="424ae-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="424ae-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="424ae-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="424ae-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="424ae-155">База данных SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="424ae-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="424ae-156">Пользовательская: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="424ae-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="424ae-157">Например, если строка подключения MySql будет иметь имя `connectionstring1`, доступ к ней будет выполняться через переменную среды `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="424ae-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="424ae-158">Стандартные документы</span><span class="sxs-lookup"><span data-stu-id="424ae-158">Default documents</span></span>
<span data-ttu-id="424ae-159">Документ по умолчанию — это веб-страница, которая отображается при открытии корневого URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="424ae-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="424ae-160">Используется первый найденный файл в списке.</span><span class="sxs-lookup"><span data-stu-id="424ae-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="424ae-161">Веб-приложения могут использовать модули, для которых выполняется маршрутизация на основе URL-адреса вместо выдачи статичного содержимого. В таком случае документ по умолчанию не используется.</span><span class="sxs-lookup"><span data-stu-id="424ae-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="424ae-162">Сопоставления обработчиков</span><span class="sxs-lookup"><span data-stu-id="424ae-162">Handler mappings</span></span>
<span data-ttu-id="424ae-163">Добавьте пользовательские обработчики скриптов, которые будут обрабатывать запросы для файлов с определенными расширениями.</span><span class="sxs-lookup"><span data-stu-id="424ae-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="424ae-164">**Расширение**.</span><span class="sxs-lookup"><span data-stu-id="424ae-164">**Extension**.</span></span> <span data-ttu-id="424ae-165">Расширение обрабатываемого файла, например *.php или handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="424ae-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="424ae-166">**Путь к обработчику сценариев**.</span><span class="sxs-lookup"><span data-stu-id="424ae-166">**Script Processor Path**.</span></span> <span data-ttu-id="424ae-167">Абсолютный путь к обработчику сценариев.</span><span class="sxs-lookup"><span data-stu-id="424ae-167">The absolute path of the script processor.</span></span> <span data-ttu-id="424ae-168">Запросы к файлам, совпадающим с расширением, будут обрабатываться обработчиком сценариев.</span><span class="sxs-lookup"><span data-stu-id="424ae-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="424ae-169">Используйте путь `D:\home\site\wwwroot` для указания корневого каталога веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="424ae-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="424ae-170">**Дополнительные аргументы**.</span><span class="sxs-lookup"><span data-stu-id="424ae-170">**Additional Arguments**.</span></span> <span data-ttu-id="424ae-171">Необязательные аргументы для командной строки обработчика сценариев.</span><span class="sxs-lookup"><span data-stu-id="424ae-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="424ae-172">Виртуальные приложения и каталоги</span><span class="sxs-lookup"><span data-stu-id="424ae-172">Virtual applications and directories</span></span>
<span data-ttu-id="424ae-173">Чтобы настроить виртуальные приложения и каталоги, укажите каждый виртуальный каталог и его соответствующий физический путь относительно корневого каталога веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="424ae-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="424ae-174">Или установите флажок **Приложение** , чтобы отметить виртуальный каталог как приложение.</span><span class="sxs-lookup"><span data-stu-id="424ae-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="424ae-175">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="424ae-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="424ae-176">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="424ae-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="424ae-177">В столбце веб-приложений щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="424ae-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="424ae-178">Щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="424ae-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="424ae-179">Параметры записи журналов диагноcтики из веб-приложения, поддерживающего ведение журналов.</span><span class="sxs-lookup"><span data-stu-id="424ae-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="424ae-180">**Ведение журнала приложений**.</span><span class="sxs-lookup"><span data-stu-id="424ae-180">**Application Logging**.</span></span> <span data-ttu-id="424ae-181">Эта функция записывает журналы приложений в файловую систему.</span><span class="sxs-lookup"><span data-stu-id="424ae-181">Writes application logs to the file system.</span></span> <span data-ttu-id="424ae-182">Ведение журнала продолжается в течение 12 часов.</span><span class="sxs-lookup"><span data-stu-id="424ae-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="424ae-183">**Уровень**.</span><span class="sxs-lookup"><span data-stu-id="424ae-183">**Level**.</span></span> <span data-ttu-id="424ae-184">Если включено ведение журналов приложений, этот параметр задает объем данных, который будет записан (ошибка, предупреждение, сведения или подробные сведения).</span><span class="sxs-lookup"><span data-stu-id="424ae-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="424ae-185">**Ведение журнала веб-сервера**.</span><span class="sxs-lookup"><span data-stu-id="424ae-185">**Web server logging**.</span></span> <span data-ttu-id="424ae-186">Журналы сохраняются в расширенном формате журнала W3C.</span><span class="sxs-lookup"><span data-stu-id="424ae-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="424ae-187">**Подробные сообщения об ошибках**.</span><span class="sxs-lookup"><span data-stu-id="424ae-187">**Detailed error messages**.</span></span> <span data-ttu-id="424ae-188">Сохраняет HTM-файлы с подробными сведениями об ошибках.</span><span class="sxs-lookup"><span data-stu-id="424ae-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="424ae-189">Файлы сохраняются в папке /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="424ae-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="424ae-190">**Трассировка неудачно завершенных запросов**.</span><span class="sxs-lookup"><span data-stu-id="424ae-190">**Failed request tracing**.</span></span> <span data-ttu-id="424ae-191">Журналы неудачных запросов к XML-файлам.</span><span class="sxs-lookup"><span data-stu-id="424ae-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="424ae-192">Файлы сохраняются в каталоге "/LogFiles/W3SVC*xxx*", где xxx — это уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="424ae-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="424ae-193">Эта папка содержит XSL-файл и один или несколько XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="424ae-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="424ae-194">Обязательно загрузите XSL-файл, т. к. предоставляет средства форматирования и фильтрации содержимого XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="424ae-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="424ae-195">Для просмотра файлов журнала необходимо создать учетные данные FTP, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="424ae-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="424ae-196">В столбце веб-приложений щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="424ae-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="424ae-197">Щелкните **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="424ae-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="424ae-198">Введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="424ae-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="424ae-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="424ae-199">Click **Save**.</span></span>

![Сброс учетных данных развертывания][configure03]

<span data-ttu-id="424ae-201">Полным именем пользователя FTP будет "app\username", где *app* — название вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="424ae-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="424ae-202">Имя пользователя указано в колонке веб-приложения в разделе **Основные сведения**.</span><span class="sxs-lookup"><span data-stu-id="424ae-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![Учетные данные развертывания FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="424ae-204">Другие задачи по настройке</span><span class="sxs-lookup"><span data-stu-id="424ae-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="424ae-205">SSL</span><span class="sxs-lookup"><span data-stu-id="424ae-205">SSL</span></span>
<span data-ttu-id="424ae-206">В стандартном и базовом режиме можно загрузить SSL-сертификаты для настраиваемого домена.</span><span class="sxs-lookup"><span data-stu-id="424ae-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="424ae-207">Дополнительные сведения см. в статье [Включение протокола HTTPS для веб-приложения].</span><span class="sxs-lookup"><span data-stu-id="424ae-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="424ae-208">Чтобы просмотреть загруженные сертификаты, щелкните **Все параметры** > **Личные домены и SSL**.</span><span class="sxs-lookup"><span data-stu-id="424ae-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="424ae-209">Имена доменов</span><span class="sxs-lookup"><span data-stu-id="424ae-209">Domain names</span></span>
<span data-ttu-id="424ae-210">Добавление имени личного домена для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="424ae-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="424ae-211">Дополнительные сведения см. в статье [Настройка личного доменного имени для веб-приложения в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="424ae-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="424ae-212">Чтобы просмотреть доменные имена, щелкните **Все параметры** > **Личные домены и SSL**.</span><span class="sxs-lookup"><span data-stu-id="424ae-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="424ae-213">Развернутые приложения</span><span class="sxs-lookup"><span data-stu-id="424ae-213">Deployments</span></span>
* <span data-ttu-id="424ae-214">Настройка непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="424ae-214">Set up continuous deployment.</span></span> <span data-ttu-id="424ae-215">Ознакомьтесь со статьей [Использование Git для развертывания веб-приложений в службе приложений Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="424ae-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="424ae-216">Слоты развертывания.</span><span class="sxs-lookup"><span data-stu-id="424ae-216">Deployment slots.</span></span> <span data-ttu-id="424ae-217">См. статью [Настройка промежуточных сред для веб-приложений в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="424ae-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="424ae-218">Чтобы просмотреть слоты развертывания, щелкните **Все параметры** > **Слоты развертывания**.</span><span class="sxs-lookup"><span data-stu-id="424ae-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="424ae-219">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="424ae-219">Monitoring</span></span>
<span data-ttu-id="424ae-220">В режимах "Базовый" и "Стандартный" можно проверить доступность конечных точек HTTP и HTTPS из трех географических распределенных расположений.</span><span class="sxs-lookup"><span data-stu-id="424ae-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="424ae-221">Тест мониторинга завершается с ошибкой, если код ответа HTTP говорит об ошибке (4xx или 5xx) или на ответ требуется более 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="424ae-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="424ae-222">Конечная точка считается доступной, если тесты мониторинга завершились для нее успешно для всех указанных расположений.</span><span class="sxs-lookup"><span data-stu-id="424ae-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="424ae-223">Дополнительные сведения см. в статье [Практическое руководство: мониторинг состояния конечной веб-точки].</span><span class="sxs-lookup"><span data-stu-id="424ae-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="424ae-224">Если вы хотите приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений], где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="424ae-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="424ae-225">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="424ae-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="424ae-226">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="424ae-226">Next steps</span></span>
* <span data-ttu-id="424ae-227">[Настройка личного доменного имени в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="424ae-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="424ae-228">[Включение протокола HTTPS для приложения в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="424ae-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="424ae-229">[Масштабирование веб-приложения в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="424ae-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="424ae-230">[Основы мониторинга для веб-приложений в службе приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="424ae-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="424ae-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="424ae-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="424ae-232">[портале Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="424ae-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="424ae-233">[Настройка личного доменного имени в службе приложений Azure]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="424ae-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="424ae-234">[Настройка промежуточных сред для веб-приложений в службе приложений Azure]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="424ae-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="424ae-235">[Включение протокола HTTPS для приложения в службе приложений Azure]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="424ae-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="424ae-236">[Практическое руководство: мониторинг состояния конечной веб-точки]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="424ae-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="424ae-237">[Основы мониторинга для веб-приложений в службе приложений Azure]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="424ae-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="424ae-238">[режим конвейера]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="424ae-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="424ae-239">[Масштабирование веб-приложения в службе приложений Azure]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="424ae-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="424ae-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="424ae-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="424ae-241">[Пробное использование службы приложений]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="424ae-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
