---
title: "Отслеживание приложений в службе приложений Azure | Документация Майкрософт"
description: "Узнайте, как осуществлять мониторинг приложений в службе приложений Azure с помощью портала Azure."
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
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="91596-103">Мониторинг приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="91596-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="91596-104">[Служба приложений](http://go.microsoft.com/fwlink/?LinkId=529714) предоставляет встроенные средства мониторинга на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91596-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="91596-105">Они позволяют просматривать **квоты**, **метрики** приложения и план службы приложений, а также настраивать получение **оповещений** и автоматическое **масштабирование** приложения на основе метрик.</span><span class="sxs-lookup"><span data-stu-id="91596-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="91596-106">Общие сведения о квотах и метриках</span><span class="sxs-lookup"><span data-stu-id="91596-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="91596-107">Квоты</span><span class="sxs-lookup"><span data-stu-id="91596-107">Quotas</span></span>
<span data-ttu-id="91596-108">На приложения, размещенные в службе приложений, распространяются *ограничения* на использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="91596-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="91596-109">Эти ограничения определены в рамках **плана службы приложений** , связанного с приложением.</span><span class="sxs-lookup"><span data-stu-id="91596-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="91596-110">Если приложение используется в режиме плана **Бесплатный** или **Общий**, ограничения на использование ресурсов выражены в виде **квот**.</span><span class="sxs-lookup"><span data-stu-id="91596-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="91596-111">Если приложение используется в режиме плана **Базовый**, **Стандартный** или **Премиум**, ограничения выражаются в виде **размера** выделенных ресурсов ("Малый", "Средний" или "Большой") и **числа экземпляров** (1, 2, 3 и т. д.) **плана службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="91596-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="91596-112">Для приложений, работающих в режиме плана **Бесплатный** или **Общий**, предоставляются следующие **квоты**.</span><span class="sxs-lookup"><span data-stu-id="91596-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="91596-113">**CPU (Short)**</span><span class="sxs-lookup"><span data-stu-id="91596-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="91596-114">Объем ресурсов ЦП, которые может потребить приложение в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="91596-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="91596-115">Эта квота повторно назначается каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="91596-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="91596-116">**CPU (Day)**</span><span class="sxs-lookup"><span data-stu-id="91596-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="91596-117">объем ресурсов ЦП, которые может потребить приложение в течение одного дня.</span><span class="sxs-lookup"><span data-stu-id="91596-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="91596-118">Эта квота повторно назначается каждые 24 часа в полночь (в формате UTC);</span><span class="sxs-lookup"><span data-stu-id="91596-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="91596-119">**Память**</span><span class="sxs-lookup"><span data-stu-id="91596-119">**Memory**</span></span>
  * <span data-ttu-id="91596-120">объем ресурсов ЦП, которые может потребить приложение;</span><span class="sxs-lookup"><span data-stu-id="91596-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="91596-121">**Пропускная способность**</span><span class="sxs-lookup"><span data-stu-id="91596-121">**Bandwidth**</span></span>
  * <span data-ttu-id="91596-122">объем исходящей пропускной способности, который может использовать приложение в течение одного дня.</span><span class="sxs-lookup"><span data-stu-id="91596-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="91596-123">Эта квота повторно назначается каждые 24 часа в полночь (в формате UTC);</span><span class="sxs-lookup"><span data-stu-id="91596-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="91596-124">**Filesystem**</span><span class="sxs-lookup"><span data-stu-id="91596-124">**Filesystem**</span></span>
  * <span data-ttu-id="91596-125">общий объем доступного пространства для хранения.</span><span class="sxs-lookup"><span data-stu-id="91596-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="91596-126">Для приложений, настроенных для работы в режиме плана **Базовый**, **Стандартный** и **Премиум**, доступна только квота **Filesystem**.</span><span class="sxs-lookup"><span data-stu-id="91596-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="91596-127">Дополнительные сведения об определенных квотах, ограничениях и функциях, доступных для разных номеров SKU службы приложений, см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#app-service-limits).</span><span class="sxs-lookup"><span data-stu-id="91596-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="91596-128">Принудительное применение квот</span><span class="sxs-lookup"><span data-stu-id="91596-128">Quota Enforcement</span></span>
<span data-ttu-id="91596-129">Если квоты на использование ЦП (**непродолжительное** и **посуточное**), а также квота на **пропускную способность** будут превышены, работа приложения будет остановлена до повторного назначения квоты.</span><span class="sxs-lookup"><span data-stu-id="91596-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="91596-130">В течение этого времени все входящие запросы будут завершаться с ошибкой **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="91596-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="91596-131">В случае превышения квоты на **память** приложение будет перезапущено.</span><span class="sxs-lookup"><span data-stu-id="91596-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="91596-132">Если будет превышена квота на **файловую систему** , все операции записи, в том числе и записи в журналы, будут завершаться сбоем.</span><span class="sxs-lookup"><span data-stu-id="91596-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="91596-133">Квоту на использование можно увеличить или удалить из приложения путем изменения плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="91596-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="91596-134">Метрики</span><span class="sxs-lookup"><span data-stu-id="91596-134">Metrics</span></span>
<span data-ttu-id="91596-135">**Метрики** предоставляют сведения о приложении или поведении плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="91596-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="91596-136">Для **приложения**доступны следующие метрики:</span><span class="sxs-lookup"><span data-stu-id="91596-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="91596-137">**Среднее время ответа**</span><span class="sxs-lookup"><span data-stu-id="91596-137">**Average Response Time**</span></span>
  * <span data-ttu-id="91596-138">среднее время обработки запроса приложением (в миллисекундах);</span><span class="sxs-lookup"><span data-stu-id="91596-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="91596-139">**средний размер рабочего набора памяти;**</span><span class="sxs-lookup"><span data-stu-id="91596-139">**Average memory working set**</span></span>
  * <span data-ttu-id="91596-140">средний объем памяти (в МиБ/с), используемый приложением;</span><span class="sxs-lookup"><span data-stu-id="91596-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="91596-141">**Время ЦП**</span><span class="sxs-lookup"><span data-stu-id="91596-141">**CPU Time**</span></span>
  * <span data-ttu-id="91596-142">количество времени ЦП (в секундах), используемого приложением.</span><span class="sxs-lookup"><span data-stu-id="91596-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="91596-143">Дополнительные сведения об этих метриках см. в документации по [времени и проценте использования ЦП](#cpu-time-vs-cpu-percentage);</span><span class="sxs-lookup"><span data-stu-id="91596-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="91596-144">**Входящие данные**</span><span class="sxs-lookup"><span data-stu-id="91596-144">**Data In**</span></span>
  * <span data-ttu-id="91596-145">объем входящей пропускной способности, используемый приложением (в МиБ/с);</span><span class="sxs-lookup"><span data-stu-id="91596-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="91596-146">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="91596-146">**Data Out**</span></span>
  * <span data-ttu-id="91596-147">объем исходящей пропускной способности, используемый приложением (в МиБ/с);</span><span class="sxs-lookup"><span data-stu-id="91596-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="91596-148">**HTTP 2xx**</span><span class="sxs-lookup"><span data-stu-id="91596-148">**Http 2xx**</span></span>
  * <span data-ttu-id="91596-149">Количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 200, но меньше 300.</span><span class="sxs-lookup"><span data-stu-id="91596-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="91596-150">**HTTP 3xx**</span><span class="sxs-lookup"><span data-stu-id="91596-150">**Http 3xx**</span></span>
  * <span data-ttu-id="91596-151">количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 300, но меньше 400;</span><span class="sxs-lookup"><span data-stu-id="91596-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="91596-152">**HTTP 401**</span><span class="sxs-lookup"><span data-stu-id="91596-152">**Http 401**</span></span>
  * <span data-ttu-id="91596-153">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 401;</span><span class="sxs-lookup"><span data-stu-id="91596-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="91596-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="91596-154">**Http 403**</span></span>
  * <span data-ttu-id="91596-155">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 403;</span><span class="sxs-lookup"><span data-stu-id="91596-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="91596-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="91596-156">**Http 404**</span></span>
  * <span data-ttu-id="91596-157">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 404;</span><span class="sxs-lookup"><span data-stu-id="91596-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="91596-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="91596-158">**Http 406**</span></span>
  * <span data-ttu-id="91596-159">количество запросов, для которых возвращается ошибка HTTP с кодом состояния 406;</span><span class="sxs-lookup"><span data-stu-id="91596-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="91596-160">**HTTP 4xx**</span><span class="sxs-lookup"><span data-stu-id="91596-160">**Http 4xx**</span></span>
  * <span data-ttu-id="91596-161">количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 400, но меньше 500;</span><span class="sxs-lookup"><span data-stu-id="91596-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="91596-162">**Ошибки HTTP-сервера**</span><span class="sxs-lookup"><span data-stu-id="91596-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="91596-163">количество запросов, для которых возвращается ошибка HTTP с кодом состояния больше (равно) 500, но меньше 600;</span><span class="sxs-lookup"><span data-stu-id="91596-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="91596-164">**рабочий набор памяти;**</span><span class="sxs-lookup"><span data-stu-id="91596-164">**Memory working set**</span></span>
  * <span data-ttu-id="91596-165">текущий объем используемой приложением памяти (в МиБ/с);</span><span class="sxs-lookup"><span data-stu-id="91596-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="91596-166">**Requests (Запросы)**</span><span class="sxs-lookup"><span data-stu-id="91596-166">**Requests**</span></span>
  * <span data-ttu-id="91596-167">общее количество запросов, для которых возвращается ошибка HTTP (независимо от кода состояния).</span><span class="sxs-lookup"><span data-stu-id="91596-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="91596-168">Для **плана службы приложений**доступны следующие метрики.</span><span class="sxs-lookup"><span data-stu-id="91596-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="91596-169">Метрики плана службы приложений поддерживаются только для планов **Базовый**, **Стандартный** и **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="91596-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="91596-170">**Процент использования ЦП**</span><span class="sxs-lookup"><span data-stu-id="91596-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="91596-171">средний процент использования ЦП всеми экземплярами плана;</span><span class="sxs-lookup"><span data-stu-id="91596-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="91596-172">**Процент использования памяти**</span><span class="sxs-lookup"><span data-stu-id="91596-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="91596-173">средний процент использование памяти всеми экземплярами плана;</span><span class="sxs-lookup"><span data-stu-id="91596-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="91596-174">**Входящие данные**</span><span class="sxs-lookup"><span data-stu-id="91596-174">**Data In**</span></span>
  * <span data-ttu-id="91596-175">средний показатель использования входящей пропускной способности всеми экземплярами плана;</span><span class="sxs-lookup"><span data-stu-id="91596-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="91596-176">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="91596-176">**Data Out**</span></span>
  * <span data-ttu-id="91596-177">средний показатель использования исходящей пропускной способности всеми экземплярами плана;</span><span class="sxs-lookup"><span data-stu-id="91596-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="91596-178">**Длина дисковой очереди**</span><span class="sxs-lookup"><span data-stu-id="91596-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="91596-179">среднее число запросов на чтение и запись, поставленных в очередь в хранилище.</span><span class="sxs-lookup"><span data-stu-id="91596-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="91596-180">Большая длина очереди на диске замедляет производительность приложения из-за избыточных дисковых операции ввода-вывода;</span><span class="sxs-lookup"><span data-stu-id="91596-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="91596-181">**Длина очереди HTTP**</span><span class="sxs-lookup"><span data-stu-id="91596-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="91596-182">среднее число запросов HTTP, которые ставятся в очередь перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="91596-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="91596-183">Большая или увеличивающая длина очереди HTTP является признаком интенсивной нагрузки плана.</span><span class="sxs-lookup"><span data-stu-id="91596-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="91596-184">Время и процент использования ЦП</span><span class="sxs-lookup"><span data-stu-id="91596-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="91596-185">Существуют 2 метрики, которые отражают использование ЦП:</span><span class="sxs-lookup"><span data-stu-id="91596-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="91596-186">**Время ЦП** и **Процент ЦП**.</span><span class="sxs-lookup"><span data-stu-id="91596-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="91596-187">Метрику **Время ЦП** рекомендуется использовать для приложений, настроенных для работы в режиме плана **Бесплатный** или **Общий**. Это связанно с тем, что квота на использование ЦП приложением, предоставленная в этих планах, определяется в минутах.</span><span class="sxs-lookup"><span data-stu-id="91596-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="91596-188">В свою очередь, метрику **Процент ЦП** рекомендуется использовать для приложений, настроенных для работы в режиме плана **Базовый**, **Стандартный** и **Премиум**, так как эти приложения можно масштабировать. Кроме того, эта метрика позволяет оценить общее потребление ресурсов ЦП всеми экземплярами.</span><span class="sxs-lookup"><span data-stu-id="91596-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="91596-189">Степень детализации метрик и политика их хранения</span><span class="sxs-lookup"><span data-stu-id="91596-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="91596-190">Метрики для приложения и плана службы приложений записываются и обрабатываются в службе в соответствии со следующей степенью детализации и политиками хранения.</span><span class="sxs-lookup"><span data-stu-id="91596-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="91596-191">Метрики со степенью детализации до **минут** хранятся **48 часов**.</span><span class="sxs-lookup"><span data-stu-id="91596-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="91596-192">Метрики со степенью детализации до **часов** хранятся **30 дней**.</span><span class="sxs-lookup"><span data-stu-id="91596-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="91596-193">Метрики со степенью детализации до **дней** хранятся **90 дней**.</span><span class="sxs-lookup"><span data-stu-id="91596-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="91596-194">Мониторинг квот и метрик на портале Azure</span><span class="sxs-lookup"><span data-stu-id="91596-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="91596-195">Состояние **квот** и **метрик**, влияющих на приложение, можно просмотреть на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91596-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="91596-196">Чтобы просмотреть сведения о ![][quotas]
**квотах**, выберите "Параметры" > **Квоты**.</span><span class="sxs-lookup"><span data-stu-id="91596-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="91596-197">В UX отображаются следующие сведения о квотах: имя, интервал повторного назначения, текущие ограничение и значение.</span><span class="sxs-lookup"><span data-stu-id="91596-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="91596-198">Доступ к сведениям о ![][metrics]
**метриках** можно получить прямо в колонке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="91596-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="91596-199">Здесь также можно настроить отображение диаграммы. Для этого необходимо **щелкнуть** диаграмму и выбрать **Изменить диаграмму**.</span><span class="sxs-lookup"><span data-stu-id="91596-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="91596-200">Этот параметр позволяет задать **диапазон времени**, **тип диаграммы** и отображаемые **метрики**.</span><span class="sxs-lookup"><span data-stu-id="91596-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="91596-201">Дополнительные сведения о метриках см. в статье [Обзор метрик в Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="91596-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="91596-202">Оповещения и автомасштабирование</span><span class="sxs-lookup"><span data-stu-id="91596-202">Alerts and Autoscale</span></span>
<span data-ttu-id="91596-203">Приложение и план службы приложений поддерживают получение оповещений на основе метрик. Дополнительные сведения о настройках этой возможности см. в статье [Создание оповещений для служб Azure с помощью портала Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="91596-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="91596-204">Приложения службы приложений, настроенные для работы в режиме плана "Базовый", "Стандартный" и "Премиум", поддерживают возможность **автомасштабирования**.</span><span class="sxs-lookup"><span data-stu-id="91596-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="91596-205">Это позволяет настроить правила мониторинга метрик плана службы приложений и изменить число экземпляров, благодаря чему можно получить дополнительные ресурсы или же сэкономить средства в случае избыточной подготовки.</span><span class="sxs-lookup"><span data-stu-id="91596-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="91596-206">Дополнительные сведения об автомасштабировании см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md) и [Рекомендации по автомасштабированию Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="91596-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="91596-207">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="91596-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="91596-208">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="91596-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="91596-209">Изменения</span><span class="sxs-lookup"><span data-stu-id="91596-209">What's changed</span></span>
* <span data-ttu-id="91596-210">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="91596-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
