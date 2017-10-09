---
title: "aaaMonitoring функции Azure | Документы Microsoft"
description: "Узнайте, как toomonitor функций Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="5487d-104">Мониторинг функций Azure</span><span class="sxs-lookup"><span data-stu-id="5487d-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="5487d-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="5487d-105">Overview</span></span> 


<span data-ttu-id="5487d-106">Hello **монитор** вкладки для каждой функции позволяет tooreview каждого выполнения функции.</span><span class="sxs-lookup"><span data-stu-id="5487d-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Вкладка "Мониторинг" Функций Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="5487d-108">Щелкнув выполнение позволяет вам tooreview hello длительность, входные данные, ошибок и связанных файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="5487d-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="5487d-109">Это полезно для отладки и настройки производительности ваших функций.</span><span class="sxs-lookup"><span data-stu-id="5487d-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="5487d-110">При использовании hello [потребления план размещения](functions-overview.md#pricing) функции Azure hello **мониторинг** плитки в колонке обзор функции приложения hello не отобразятся никакие данные.</span><span class="sxs-lookup"><span data-stu-id="5487d-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="5487d-111">Это так, как платформа hello динамически масштабирует и управляет вычислительных операций, поэтому эти показатели не имеют смысла в плане использования.</span><span class="sxs-lookup"><span data-stu-id="5487d-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="5487d-112">Использование hello toomonitor приложений-функций, следует использовать hello рекомендации в данной статье.</span><span class="sxs-lookup"><span data-stu-id="5487d-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="5487d-113">Следующий снимок экрана приветствия показан пример.</span><span class="sxs-lookup"><span data-stu-id="5487d-113">hello following screen-shot shows an example:</span></span>
> 
> ![Мониторинг в колонке ресурсов основного hello](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="5487d-115">Мониторинг в реальном времени</span><span class="sxs-lookup"><span data-stu-id="5487d-115">Real-time monitoring</span></span>

<span data-ttu-id="5487d-116">Чтобы выполнить мониторинг в реальном времени, щелкните ссылку **прямой поток событий**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5487d-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Live параметр поток событий для вкладки монитора hello](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="5487d-118">поток динамической событий Hello будет отобразить на диаграмме в новой вкладке браузера как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5487d-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Пример прямого потока событий](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="5487d-120">Имеется известная проблема, которая может привести к заполняется toofail toobe вашей данных система.</span><span class="sxs-lookup"><span data-stu-id="5487d-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="5487d-121">Если возникают, может потребоваться tooclose hello браузера вкладку содержащего hello динамической поток событий, а затем нажмите кнопку **поток событий динамической** снова tooallow его tooproperly заполнения данными потока событий.</span><span class="sxs-lookup"><span data-stu-id="5487d-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="5487d-122">поток динамической событий Hello будет graph hello следующие статистические данные для функции:</span><span class="sxs-lookup"><span data-stu-id="5487d-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="5487d-123">количество начатых выполнений в секунду;</span><span class="sxs-lookup"><span data-stu-id="5487d-123">Executions started per second</span></span>
* <span data-ttu-id="5487d-124">количество завершенных выполнений в секунду;</span><span class="sxs-lookup"><span data-stu-id="5487d-124">Executions completed per second</span></span>
* <span data-ttu-id="5487d-125">количество выполнений, завершившихся сбоем, в секунду;</span><span class="sxs-lookup"><span data-stu-id="5487d-125">Executions failed per second</span></span>
* <span data-ttu-id="5487d-126">среднее время выполнения в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="5487d-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="5487d-127">Эти статистические данные в режиме реального времени, но фактический построения диаграмм данных выполнения hello hello могут иметься около 10 секунд задержки.</span><span class="sxs-lookup"><span data-stu-id="5487d-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="5487d-128">Мониторинг файлов журнала из командной строки</span><span class="sxs-lookup"><span data-stu-id="5487d-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="5487d-129">Можно осуществлять потоковую передачу сеанса командной строки tooa файлы журнала на локальной рабочей станции с помощью hello Azure интерфейс командной строки (CLI) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5487d-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="5487d-130">Мониторинг файлов журнала приложения функции с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5487d-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="5487d-131">запущена, tooget [установить hello Azure CLI](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="5487d-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="5487d-132">Войти в учетную запись Azure с помощью следующих hello команды или любой из hello другие параметры, описываемые в, [вход tooAzure из hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5487d-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="5487d-133">Используйте hello следующая команда режим управления службы Azure CLI (ASM) tooenable:.</span><span class="sxs-lookup"><span data-stu-id="5487d-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="5487d-134">Если у вас несколько подписок, используйте следующие команды toolist hello подписки и набор hello текущей подписки toohello подписку, которая содержит функции приложения.</span><span class="sxs-lookup"><span data-stu-id="5487d-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="5487d-135">Hello следующая команда использует потоковую передачу файлах журналов hello функции приложения toohello командную строку:</span><span class="sxs-lookup"><span data-stu-id="5487d-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="5487d-136">Мониторинг файлов журнала приложения-функции с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5487d-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="5487d-137">запущена, tooget [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5487d-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5487d-138">Добавьте учетную запись Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5487d-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="5487d-139">Если у вас несколько подписок, их список можно получить по имени с hello, следующие команды toosee Если hello правильные подписка является hello выбранного в данный момент на основе `IsCurrent` свойство:</span><span class="sxs-lookup"><span data-stu-id="5487d-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="5487d-140">Если вам требуется toohello tooset hello активной подписки, одна из которых содержит функции приложения, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5487d-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="5487d-141">Поток hello журналы tooyour сеанс PowerShell с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5487d-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="5487d-142">Дополнительные сведения см. в разделе слишком[как: потоковую передачу журналов для веб-приложений](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="5487d-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5487d-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5487d-143">Next steps</span></span>
<span data-ttu-id="5487d-144">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="5487d-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="5487d-145">Тестирование функции</span><span class="sxs-lookup"><span data-stu-id="5487d-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="5487d-146">Масштабирование функции</span><span class="sxs-lookup"><span data-stu-id="5487d-146">Scale a function</span></span>](functions-scale.md)

