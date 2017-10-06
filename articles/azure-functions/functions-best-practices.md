---
title: "aaaBest и рекомендации для функций Azure | Документы Microsoft"
description: "Ознакомьтесь с рекомендациями и шаблонами для Функций Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Функции Azure, шаблоны, рекомендация, функции, обработка событий, объекты webhook, динамические вычисления, бессерверная архитектура"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="58e90-104">Оптимизировать производительность hello и надежность функций Azure</span><span class="sxs-lookup"><span data-stu-id="58e90-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="58e90-105">Эта статья содержит рекомендации tooimprove hello производительности и надежности приложений-функций.</span><span class="sxs-lookup"><span data-stu-id="58e90-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="58e90-106">Избегайте длительных функций</span><span class="sxs-lookup"><span data-stu-id="58e90-106">Avoid long running functions</span></span>

<span data-ttu-id="58e90-107">Крупные длительные функции могут вызывать непредвиденные проблемы времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="58e90-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="58e90-108">Функция может оказаться большим из-за зависимости toomany Node.js.</span><span class="sxs-lookup"><span data-stu-id="58e90-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="58e90-109">Импорт зависимостей может также привести к замедлению загрузки, что, в свою очередь, приводит к непредвиденным проблемам времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="58e90-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="58e90-110">Зависимости можно загрузить явно и неявно.</span><span class="sxs-lookup"><span data-stu-id="58e90-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="58e90-111">Один модуль, загруженный в коде, может загрузить собственные дополнительные модули.</span><span class="sxs-lookup"><span data-stu-id="58e90-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="58e90-112">По возможности выполняйте рефакторинг крупных функций и перерабатывайте их на более мелкие совместимые наборы функций, которые работают сообща и быстро возвращают ответ.</span><span class="sxs-lookup"><span data-stu-id="58e90-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="58e90-113">Например веб-перехватчик или функция триггера HTTP может потребовать подтверждения ответ в течение некоторого ограниченного промежутка времени; Чаще всего для веб-перехватчиков toorequire ответ немедленно.</span><span class="sxs-lookup"><span data-stu-id="58e90-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="58e90-114">Полезные данные триггера hello HTTP можно передать в toobe очереди, обрабатываемых функция очереди триггера.</span><span class="sxs-lookup"><span data-stu-id="58e90-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="58e90-115">Такой подход позволяет toodefer hello фактическую работу и возвращает ответ немедленно.</span><span class="sxs-lookup"><span data-stu-id="58e90-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="58e90-116">Взаимодействие функций</span><span class="sxs-lookup"><span data-stu-id="58e90-116">Cross function communication</span></span>

<span data-ttu-id="58e90-117">При установке нескольких функций, обычно является наилучшим практике toouse очереди хранилища для функции обмена данными между.</span><span class="sxs-lookup"><span data-stu-id="58e90-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="58e90-118">Hello основной причиной является то очереди хранилища дешевле и гораздо проще tooprovision.</span><span class="sxs-lookup"><span data-stu-id="58e90-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="58e90-119">Отдельные сообщения в очередь хранилища, ограничены размером too64 КБ.</span><span class="sxs-lookup"><span data-stu-id="58e90-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="58e90-120">При необходимости toopass больших сообщений между функциями очереди шины обслуживания Azure может быть размером сообщений используется toosupport копирование too256 КБ.</span><span class="sxs-lookup"><span data-stu-id="58e90-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="58e90-121">Если перед обработкой сообщений их нужно отфильтровать, ознакомьтесь со статьями о служебной шине.</span><span class="sxs-lookup"><span data-stu-id="58e90-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="58e90-122">Концентраторы событий являются полезным toosupport связи большого объема.</span><span class="sxs-lookup"><span data-stu-id="58e90-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="58e90-123">Запись toobe функции без сохранения состояния</span><span class="sxs-lookup"><span data-stu-id="58e90-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="58e90-124">По возможности функции должны быть без отслеживания состояния и идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="58e90-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="58e90-125">Свяжите любые необходимые сведения о состоянии со своими данными.</span><span class="sxs-lookup"><span data-stu-id="58e90-125">Associate any required state information with your data.</span></span> <span data-ttu-id="58e90-126">Например, с обрабатываемым заказом скорее всего будет связан элемент `state`.</span><span class="sxs-lookup"><span data-stu-id="58e90-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="58e90-127">Функция может обработать заказ, основываясь на это состояние, а сама функция hello остается без сохранения состояния.</span><span class="sxs-lookup"><span data-stu-id="58e90-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="58e90-128">Идемпотентные функции рекомендуется использовать с триггерами таймера.</span><span class="sxs-lookup"><span data-stu-id="58e90-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="58e90-129">Например если вас что-то совершенно необходимо запустить один раз в день, напишите он мог выполняться любое время в течение дня hello с hello одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="58e90-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="58e90-130">Если нет заданий для конкретного дня выхода из функции Hello.</span><span class="sxs-lookup"><span data-stu-id="58e90-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="58e90-131">Также при предыдущем запуске сбой toocomplete, следующий запуск hello следует взять прерванную.</span><span class="sxs-lookup"><span data-stu-id="58e90-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="58e90-132">Создавайте защищенные функции</span><span class="sxs-lookup"><span data-stu-id="58e90-132">Write defensive functions</span></span>

<span data-ttu-id="58e90-133">Предположим, что в любое время в функции может возникнуть исключение.</span><span class="sxs-lookup"><span data-stu-id="58e90-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="58e90-134">Разрабатывать собственные функции с помощью toocontinue возможность hello из предыдущей точки сбоя во время следующего выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="58e90-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="58e90-135">Рассмотрим сценарий, требующий hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="58e90-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="58e90-136">Запросить 10 000 строк в базе данных.</span><span class="sxs-lookup"><span data-stu-id="58e90-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="58e90-137">Создание очереди сообщений для каждого из этих строк tooprocess дальнейшей строку hello вниз.</span><span class="sxs-lookup"><span data-stu-id="58e90-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="58e90-138">В зависимости от сложности системы, подчиненные службы могут работать неправильно, могут происходить сбои в работе сети или нарушения лимитов квоты и т. д. Все это может в любое время повлиять на функцию.</span><span class="sxs-lookup"><span data-stu-id="58e90-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="58e90-139">Необходимо toodesign вашей toobe функции, готовым к ней.</span><span class="sxs-lookup"><span data-stu-id="58e90-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="58e90-140">Как отреагирует ваш код при сбое после вставки 5000 элементов в очередь для обработки?</span><span class="sxs-lookup"><span data-stu-id="58e90-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="58e90-141">Отслеживайте элементы в наборе, работа с которым завершена.</span><span class="sxs-lookup"><span data-stu-id="58e90-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="58e90-142">В противном случае их можно вставить позже.</span><span class="sxs-lookup"><span data-stu-id="58e90-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="58e90-143">Это может серьезно повлиять на рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="58e90-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="58e90-144">Если элемент очереди уже был обработан, позволит вашей toobe функция холостой.</span><span class="sxs-lookup"><span data-stu-id="58e90-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="58e90-145">Воспользуйтесь преимуществами защитные меры, уже предоставлены для компонентов, используемых в платформе Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="58e90-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="58e90-146">Например, в разделе **обработка сообщений в очередь подозрительных сообщений** hello документации по [запускает очередь хранилища Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="58e90-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="58e90-147">Не рабочего и тестового набора программировать в hello так же функция приложения</span><span class="sxs-lookup"><span data-stu-id="58e90-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="58e90-148">Функции в приложении-функции совместно используют ресурсы.</span><span class="sxs-lookup"><span data-stu-id="58e90-148">Functions within a function app share resources.</span></span> <span data-ttu-id="58e90-149">Например, память.</span><span class="sxs-lookup"><span data-stu-id="58e90-149">For example, memory is shared.</span></span> <span data-ttu-id="58e90-150">Если вы используете приложение функции в рабочей среде, не добавлять функции, связанные с тестами и tooit ресурсов.</span><span class="sxs-lookup"><span data-stu-id="58e90-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="58e90-151">Это может вызвать непредвиденные затраты во время выполнения кода в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="58e90-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="58e90-152">Следите за тем, что вы загружаете в рабочие приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="58e90-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="58e90-153">Память усредняется с учетом каждой функции в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="58e90-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="58e90-154">При наличии общей сборки, указанной в нескольких функциях .Net, поместите ее в общую папку.</span><span class="sxs-lookup"><span data-stu-id="58e90-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="58e90-155">Ссылка сборки hello аналогичные toohello оператор, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="58e90-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="58e90-156">В противном случае это просто tooaccidentally развертывания нескольких версий теста же двоичного файла, которые ведут себя по-разному между функции hello.</span><span class="sxs-lookup"><span data-stu-id="58e90-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="58e90-157">Не используйте подробное ведение журнала в рабочем коде.</span><span class="sxs-lookup"><span data-stu-id="58e90-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="58e90-158">Это отрицательно сказывается на производительности.</span><span class="sxs-lookup"><span data-stu-id="58e90-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="58e90-159">Использование асинхронного кода без блокирующих вызовов</span><span class="sxs-lookup"><span data-stu-id="58e90-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="58e90-160">Рекомендуется применять метод асинхронного программирования.</span><span class="sxs-lookup"><span data-stu-id="58e90-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="58e90-161">Однако всегда избегать ссылок hello `Result` свойства или метода `Wait` метод `Task` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="58e90-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="58e90-162">Этот подход может привести нехватка toothread.</span><span class="sxs-lookup"><span data-stu-id="58e90-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="58e90-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58e90-163">Next steps</span></span>
<span data-ttu-id="58e90-164">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="58e90-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="58e90-165">Так как Функции Azure используют службу приложений Azure, необходимо также ознакомиться с рекомендациями для нее.</span><span class="sxs-lookup"><span data-stu-id="58e90-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="58e90-166">Шаблоны и методики оптимизации производительности HTTP</span><span class="sxs-lookup"><span data-stu-id="58e90-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

