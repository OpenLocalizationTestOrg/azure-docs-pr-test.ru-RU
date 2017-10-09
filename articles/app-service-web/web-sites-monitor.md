---
title: "aaaMonitor приложений в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как в службе приложений Azure с помощью приложения toomonitor hello портала Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="4db4b-103">Мониторинг приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4db4b-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="4db4b-104">[Службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) предоставляет встроенные функциональные возможности наблюдения в hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4db4b-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="4db4b-105">Сюда входит возможность tooreview hello **квоты** и **метрики** для приложения, а также hello план служб приложений, Настройка **оповещения** и даже **масштабирование** автоматически на основании этих показателей.</span><span class="sxs-lookup"><span data-stu-id="4db4b-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="4db4b-106">Общие сведения о квотах и метриках</span><span class="sxs-lookup"><span data-stu-id="4db4b-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="4db4b-107">Квоты</span><span class="sxs-lookup"><span data-stu-id="4db4b-107">Quotas</span></span>
<span data-ttu-id="4db4b-108">Приложения, размещенные в службе приложений являются toocertain субъекта *ограничения* с ресурсами, они могут использовать.</span><span class="sxs-lookup"><span data-stu-id="4db4b-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="4db4b-109">Hello ограничения определяются hello **план служб приложений** связанные с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="4db4b-110">Если приложение hello находится в **Free** или **Shared** плана, а затем определяются hello ограничения на ресурсы hello, можно использовать приложение hello **квоты**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="4db4b-111">Приложение hello размещается в **основные**, **Стандартная** или **Premium** планирования, hello ограничения на ресурсы hello, они могут использовать задаются по hello **размер** (Небольшой, средний, большой) и **число экземпляров** (1, 2, 3,...) из hello **план служб приложений**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="4db4b-112">Для приложений, работающих в режиме плана **Бесплатный** или **Общий**, предоставляются следующие **квоты**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="4db4b-113">**CPU (Short)**</span><span class="sxs-lookup"><span data-stu-id="4db4b-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="4db4b-114">Объем ресурсов ЦП, которые может потребить приложение в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="4db4b-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="4db4b-115">Эта квота повторно назначается каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="4db4b-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="4db4b-116">**CPU (Day)**</span><span class="sxs-lookup"><span data-stu-id="4db4b-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="4db4b-117">объем ресурсов ЦП, которые может потребить приложение в течение одного дня.</span><span class="sxs-lookup"><span data-stu-id="4db4b-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="4db4b-118">Эта квота повторно назначается каждые 24 часа в полночь (в формате UTC);</span><span class="sxs-lookup"><span data-stu-id="4db4b-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="4db4b-119">**Память**</span><span class="sxs-lookup"><span data-stu-id="4db4b-119">**Memory**</span></span>
  * <span data-ttu-id="4db4b-120">объем ресурсов ЦП, которые может потребить приложение;</span><span class="sxs-lookup"><span data-stu-id="4db4b-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="4db4b-121">**Пропускная способность**</span><span class="sxs-lookup"><span data-stu-id="4db4b-121">**Bandwidth**</span></span>
  * <span data-ttu-id="4db4b-122">объем исходящей пропускной способности, который может использовать приложение в течение одного дня.</span><span class="sxs-lookup"><span data-stu-id="4db4b-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="4db4b-123">Эта квота повторно назначается каждые 24 часа в полночь (в формате UTC);</span><span class="sxs-lookup"><span data-stu-id="4db4b-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="4db4b-124">**Filesystem**</span><span class="sxs-lookup"><span data-stu-id="4db4b-124">**Filesystem**</span></span>
  * <span data-ttu-id="4db4b-125">общий объем доступного пространства для хранения.</span><span class="sxs-lookup"><span data-stu-id="4db4b-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="4db4b-126">Здравствуйте только квоту применимо tooapps размещенных на **основные**, **Стандартная** и **Premium** планы — **файловой системы**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="4db4b-127">Дополнительные сведения об особых квот hello, ограничения и возможности, доступные для различных конфигураций службы приложения hello можно найти здесь: [ограничения служб подписки Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="4db4b-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="4db4b-128">Принудительное применение квот</span><span class="sxs-lookup"><span data-stu-id="4db4b-128">Quota Enforcement</span></span>
<span data-ttu-id="4db4b-129">Если приложение в их использование превышает hello **ЦП (short)**, **ЦП (день)**, или **пропускной способности** квоты, а затем hello приложения будет остановлена, пока не будет повторно задает квоты hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="4db4b-130">В течение этого времени все входящие запросы будут завершаться с ошибкой **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="4db4b-131">Если приложение hello **памяти** превышена квота, то приложение hello будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="4db4b-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="4db4b-132">Если hello **Filesystem** превышении квоты, а затем любые записи, операция завершится ошибкой, это относится и к записи toologs.</span><span class="sxs-lookup"><span data-stu-id="4db4b-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="4db4b-133">Квоту на использование можно увеличить или удалить из приложения путем изменения плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4db4b-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="4db4b-134">Метрики</span><span class="sxs-lookup"><span data-stu-id="4db4b-134">Metrics</span></span>
<span data-ttu-id="4db4b-135">**Метрики** предоставляют сведения о приложение hello или поведение план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="4db4b-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="4db4b-136">Для **приложения**, доступные метрики hello:</span><span class="sxs-lookup"><span data-stu-id="4db4b-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="4db4b-137">**Среднее время ответа**</span><span class="sxs-lookup"><span data-stu-id="4db4b-137">**Average Response Time**</span></span>
  * <span data-ttu-id="4db4b-138">Hello среднее время, затраченное для запросов tooserve приложения hello в мс.</span><span class="sxs-lookup"><span data-stu-id="4db4b-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="4db4b-139">**средний размер рабочего набора памяти;**</span><span class="sxs-lookup"><span data-stu-id="4db4b-139">**Average memory working set**</span></span>
  * <span data-ttu-id="4db4b-140">Средний объем памяти в используемых приложение hello базы MIB Hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="4db4b-141">**Время ЦП**</span><span class="sxs-lookup"><span data-stu-id="4db4b-141">**CPU Time**</span></span>
  * <span data-ttu-id="4db4b-142">Hello объем ресурсов ЦП в секундах, затраченное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="4db4b-143">Дополнительные сведения об этих метриках см. в документации по [времени и проценте использования ЦП](#cpu-time-vs-cpu-percentage);</span><span class="sxs-lookup"><span data-stu-id="4db4b-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="4db4b-144">**Входящие данные**</span><span class="sxs-lookup"><span data-stu-id="4db4b-144">**Data In**</span></span>
  * <span data-ttu-id="4db4b-145">Hello объем входящей пропускной способности, используемой приложением hello в базы MIB.</span><span class="sxs-lookup"><span data-stu-id="4db4b-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="4db4b-146">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="4db4b-146">**Data Out**</span></span>
  * <span data-ttu-id="4db4b-147">объем исходящих пропускной способностью, используемой приложение hello в базы MIB Hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="4db4b-148">**HTTP 2xx**</span><span class="sxs-lookup"><span data-stu-id="4db4b-148">**Http 2xx**</span></span>
  * <span data-ttu-id="4db4b-149">Количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 200, но меньше 300.</span><span class="sxs-lookup"><span data-stu-id="4db4b-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="4db4b-150">**HTTP 3xx**</span><span class="sxs-lookup"><span data-stu-id="4db4b-150">**Http 3xx**</span></span>
  * <span data-ttu-id="4db4b-151">количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 300, но меньше 400;</span><span class="sxs-lookup"><span data-stu-id="4db4b-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="4db4b-152">**HTTP 401**</span><span class="sxs-lookup"><span data-stu-id="4db4b-152">**Http 401**</span></span>
  * <span data-ttu-id="4db4b-153">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 401;</span><span class="sxs-lookup"><span data-stu-id="4db4b-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="4db4b-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="4db4b-154">**Http 403**</span></span>
  * <span data-ttu-id="4db4b-155">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 403;</span><span class="sxs-lookup"><span data-stu-id="4db4b-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="4db4b-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="4db4b-156">**Http 404**</span></span>
  * <span data-ttu-id="4db4b-157">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 404;</span><span class="sxs-lookup"><span data-stu-id="4db4b-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="4db4b-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="4db4b-158">**Http 406**</span></span>
  * <span data-ttu-id="4db4b-159">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 406;</span><span class="sxs-lookup"><span data-stu-id="4db4b-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="4db4b-160">**HTTP 4xx**</span><span class="sxs-lookup"><span data-stu-id="4db4b-160">**Http 4xx**</span></span>
  * <span data-ttu-id="4db4b-161">количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 400, но меньше 500;</span><span class="sxs-lookup"><span data-stu-id="4db4b-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="4db4b-162">**Ошибки HTTP-сервера**</span><span class="sxs-lookup"><span data-stu-id="4db4b-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="4db4b-163">количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 500, но меньше 600;</span><span class="sxs-lookup"><span data-stu-id="4db4b-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="4db4b-164">**рабочий набор памяти;**</span><span class="sxs-lookup"><span data-stu-id="4db4b-164">**Memory working set**</span></span>
  * <span data-ttu-id="4db4b-165">Текущий объем памяти, используемой приложением hello в базы MIB.</span><span class="sxs-lookup"><span data-stu-id="4db4b-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="4db4b-166">**Requests (Запросы)**</span><span class="sxs-lookup"><span data-stu-id="4db4b-166">**Requests**</span></span>
  * <span data-ttu-id="4db4b-167">общее количество запросов, для которых возвращается ошибка HTTP (независимо от кода состояния).</span><span class="sxs-lookup"><span data-stu-id="4db4b-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="4db4b-168">Для **план служб приложений**, доступные метрики hello:</span><span class="sxs-lookup"><span data-stu-id="4db4b-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="4db4b-169">Метрики плана службы приложений поддерживаются только для планов **Базовый**, **Стандартный** и **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="4db4b-170">**Процент использования ЦП**</span><span class="sxs-lookup"><span data-stu-id="4db4b-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="4db4b-171">Hello средняя загрузка ЦП для всех экземпляров плана hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="4db4b-172">**Процент использования памяти**</span><span class="sxs-lookup"><span data-stu-id="4db4b-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="4db4b-173">Hello средний объем использованной памяти для всех экземпляров плана hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="4db4b-174">**Входящие данные**</span><span class="sxs-lookup"><span data-stu-id="4db4b-174">**Data In**</span></span>
  * <span data-ttu-id="4db4b-175">Hello среднее входящей пропускной способности, используемой для всех экземпляров плана hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="4db4b-176">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="4db4b-176">**Data Out**</span></span>
  * <span data-ttu-id="4db4b-177">Среднее Hello исходящей пропускной способности, используемой для всех экземпляров плана hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="4db4b-178">**Длина дисковой очереди**</span><span class="sxs-lookup"><span data-stu-id="4db4b-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="4db4b-179">Hello среднее время чтения и записи в хранилище запросов, которые были поставлены в очередь.</span><span class="sxs-lookup"><span data-stu-id="4db4b-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="4db4b-180">Длина очереди диска высокого уровня, это свидетельствует приложение, которое может снижения производительности из-за tooexcessive дискового ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="4db4b-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="4db4b-181">**Длина очереди HTTP**</span><span class="sxs-lookup"><span data-stu-id="4db4b-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="4db4b-182">Среднее количество HTTP-запросов, в которых использовался toosit очередь hello, прежде чем будет выполнен Hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="4db4b-183">Большая или увеличивающая длина очереди HTTP является признаком интенсивной нагрузки плана.</span><span class="sxs-lookup"><span data-stu-id="4db4b-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="4db4b-184">Время и процент использования ЦП</span><span class="sxs-lookup"><span data-stu-id="4db4b-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="4db4b-185">Существуют 2 метрики, которые отражают использование ЦП:</span><span class="sxs-lookup"><span data-stu-id="4db4b-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="4db4b-186">**Время ЦП** и **Процент ЦП**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="4db4b-187">**Время ЦП** полезна для приложений, размещенных в **Free** или **Shared** планов, так как один из их квоты указывается в минутах ЦП, используемых приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="4db4b-188">**Процент использования ЦП** на hello другой стороны полезна для приложений, размещенных в **основные**, **Стандартная** и **premium** планов, так как они могут быть масштабированы и эта метрика является хорошее представление о hello общее использование для всех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="4db4b-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="4db4b-189">Степень детализации метрик и политика их хранения</span><span class="sxs-lookup"><span data-stu-id="4db4b-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="4db4b-190">Метрики для плана службы приложений и приложений в журнал и статистически обрабатываются службой hello с hello детализации и политики хранения:</span><span class="sxs-lookup"><span data-stu-id="4db4b-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="4db4b-191">Метрики со степенью детализации до **минут** хранятся **48 часов**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="4db4b-192">Метрики со степенью детализации до **часов** хранятся **30 дней**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="4db4b-193">Метрики со степенью детализации до **дней** хранятся **90 дней**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="4db4b-194">Мониторинг квоты и параметры в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4db4b-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="4db4b-195">Можно просмотреть состояние различных hello hello **квоты** и **метрики** влияет на приложения в hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4db4b-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4db4b-196">Чтобы просмотреть сведения о ![][quotas]
**квотах**, выберите "Параметры" > **Квоты**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="4db4b-197">Hello UX позволяет просмотреть: имя квоты hello (1), (2) его интервал сброса, (3) его текущее ограничение и (4) текущее значение.</span><span class="sxs-lookup"><span data-stu-id="4db4b-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="4db4b-198">![][metrics]
**Метрики** может получать доступ непосредственно из колонки ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4db4b-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="4db4b-199">Можно также настроить hello диаграмма по: (1) **щелкните** на его, а затем выберите (2) **изменение диаграммы**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="4db4b-200">Здесь можно изменить hello (3) **временной диапазон**, (4) **тип диаграммы**и (5) **метрики** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="4db4b-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="4db4b-201">Дополнительные сведения о метриках см. в статье [Обзор метрик в Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="4db4b-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="4db4b-202">Оповещения и автомасштабирование</span><span class="sxs-lookup"><span data-stu-id="4db4b-202">Alerts and Autoscale</span></span>
<span data-ttu-id="4db4b-203">Метрики плана приложения или службы, приложения могут вызываться tooalerts toolearn Подробнее об этом, в разделе [получать уведомления об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="4db4b-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="4db4b-204">Приложения службы приложений, настроенные для работы в режиме плана "Базовый", "Стандартный" и "Премиум", поддерживают возможность **автомасштабирования**.</span><span class="sxs-lookup"><span data-stu-id="4db4b-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="4db4b-205">Это позволяет вам tooconfigure правила, отслеживать метрики плана служб приложений и можно увеличить или уменьшить число экземпляров hello, предоставляя дополнительные ресурсы при необходимости или сохранение money когда приложение hello избыточной подготовки.</span><span class="sxs-lookup"><span data-stu-id="4db4b-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="4db4b-206">Дополнительные сведения о Автомасштабирование здесь: [как tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) и здесь [советы и рекомендации для автоматического масштабирования Azure монитора](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="4db4b-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="4db4b-207">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="4db4b-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4db4b-208">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="4db4b-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="4db4b-209">Изменения</span><span class="sxs-lookup"><span data-stu-id="4db4b-209">What's changed</span></span>
* <span data-ttu-id="4db4b-210">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4db4b-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
