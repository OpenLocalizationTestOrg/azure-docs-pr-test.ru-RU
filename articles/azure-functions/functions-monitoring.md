---
title: "Мониторинг Функций Azure | Документация Майкрософт"
description: "Сведения о мониторинге Функций Azure."
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
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="16298-104">Мониторинг функций Azure</span><span class="sxs-lookup"><span data-stu-id="16298-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="16298-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="16298-105">Overview</span></span> 


<span data-ttu-id="16298-106">На вкладке **Мониторинг** для каждой функции можно просматривать каждое ее выполнение.</span><span class="sxs-lookup"><span data-stu-id="16298-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Вкладка "Мониторинг" Функций Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="16298-108">Если щелкнуть выполнение, можно просмотреть длительность, входные данные, ошибки и связанные файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="16298-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="16298-109">Это полезно для отладки и настройки производительности ваших функций.</span><span class="sxs-lookup"><span data-stu-id="16298-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="16298-110">При использовании [плана потребления](functions-overview.md#pricing) для Функций Azure в колонке обзора приложения-функции на плитке **Мониторинг** не будут отображаться какие-либо данные.</span><span class="sxs-lookup"><span data-stu-id="16298-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="16298-111">Это объясняется тем, что платформа динамически масштабирует вычислительные операции и управляет ими, поэтому эти показатели не являются информативными при использовании плана потребления.</span><span class="sxs-lookup"><span data-stu-id="16298-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="16298-112">Для мониторинга использования приложений-функций следуйте инструкциям, приведенным в этой статье.</span><span class="sxs-lookup"><span data-stu-id="16298-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="16298-113">На следующем снимке экрана показан пример.</span><span class="sxs-lookup"><span data-stu-id="16298-113">The following screen-shot shows an example:</span></span>
> 
> ![Мониторинг в основной колонке ресурсов](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="16298-115">Мониторинг в реальном времени</span><span class="sxs-lookup"><span data-stu-id="16298-115">Real-time monitoring</span></span>

<span data-ttu-id="16298-116">Чтобы выполнить мониторинг в реальном времени, щелкните ссылку **прямой поток событий**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="16298-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Параметр "Прямой поток событий" на вкладке "Мониторинг"](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="16298-118">Прямой поток событий появится в виде диаграммы в новой вкладке браузера, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="16298-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Пример прямого потока событий](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="16298-120">Есть известная проблема, из-за которой может произойти сбой заполнения данных.</span><span class="sxs-lookup"><span data-stu-id="16298-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="16298-121">Если она возникнет, может потребоваться закрыть вкладку браузера с прямым потоком событий, а затем щелкнуть ссылку **прямой поток событий** еще раз, чтобы приложение правильно заполнило данные потока событий.</span><span class="sxs-lookup"><span data-stu-id="16298-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="16298-122">На диаграмме потока событий будут представлены следующие статистические данные для функции:</span><span class="sxs-lookup"><span data-stu-id="16298-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="16298-123">количество начатых выполнений в секунду;</span><span class="sxs-lookup"><span data-stu-id="16298-123">Executions started per second</span></span>
* <span data-ttu-id="16298-124">количество завершенных выполнений в секунду;</span><span class="sxs-lookup"><span data-stu-id="16298-124">Executions completed per second</span></span>
* <span data-ttu-id="16298-125">количество выполнений, завершившихся сбоем, в секунду;</span><span class="sxs-lookup"><span data-stu-id="16298-125">Executions failed per second</span></span>
* <span data-ttu-id="16298-126">среднее время выполнения в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="16298-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="16298-127">Эти статистические данные отображаются в режиме реального времени, но фактическое построение диаграммы данных выполнения может происходить с задержкой приблизительно в 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="16298-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="16298-128">Мониторинг файлов журнала из командной строки</span><span class="sxs-lookup"><span data-stu-id="16298-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="16298-129">Потоковую передачу файлов журнала в сеанс командной строки на локальной рабочей станции можно осуществлять с помощью интерфейса командной строки Azure (CLI) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16298-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="16298-130">Мониторинг файлов журнала приложения-функции с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="16298-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="16298-131">Чтобы начать работу, [установите Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="16298-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="16298-132">Войдите в учетную запись Azure, используя следующую команду или другие варианты, описанные в статье [Войдите в Azure из командной строки Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="16298-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="16298-133">При необходимости используйте следующую команду для включения режима управления службами для интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="16298-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="16298-134">Если у вас несколько подписок, используйте следующие команды, чтобы вывести их список и настроить текущую подписку в качестве подписки, содержащую приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="16298-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="16298-135">Следующая команда выполняет потоковую передачу файлов журналов приложения-функции в командную строку:</span><span class="sxs-lookup"><span data-stu-id="16298-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="16298-136">Мониторинг файлов журнала приложения-функции с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="16298-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="16298-137">Чтобы начать работу, [установите и настройте Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16298-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="16298-138">Добавьте свою учетную запись Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="16298-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="16298-139">Если у вас несколько подписок, с помощью следующей команды можно вывести их список, отсортированный по имени, чтобы убедиться, что в данный момент выбрана правильная подписка, по свойству `IsCurrent`:</span><span class="sxs-lookup"><span data-stu-id="16298-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="16298-140">Если необходимо настроить активную подписку в качестве подписки, содержащей приложение-функцию, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16298-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="16298-141">Передайте журналы в сеанс PowerShell с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="16298-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="16298-142">Дополнительные сведения см. в разделе [Практическое руководство. Потоковая передача журналов](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="16298-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="16298-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16298-143">Next steps</span></span>
<span data-ttu-id="16298-144">Для получения дополнительных сведений см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="16298-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="16298-145">Тестирование функции</span><span class="sxs-lookup"><span data-stu-id="16298-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="16298-146">Масштабирование функции</span><span class="sxs-lookup"><span data-stu-id="16298-146">Scale a function</span></span>](functions-scale.md)

