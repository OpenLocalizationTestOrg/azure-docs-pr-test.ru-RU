---
ms.assetid: 
title: "aaaAzure рекомендации регулирования хранилища ключей | Документы Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="efe9d-102">Руководство по регулированию хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="efe9d-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="efe9d-103">Регулирование — это процесс инициируется, ограничивает число одновременных вызовов службы Azure toohello tooprevent злоупотребление ресурсами hello.</span><span class="sxs-lookup"><span data-stu-id="efe9d-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="efe9d-104">Хранилище Azure ключ (AKV) — спроектированный toohandle большое количество запросов.</span><span class="sxs-lookup"><span data-stu-id="efe9d-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="efe9d-105">Если происходит огромное количество запросов, регулирование запросов клиента используется для поддержания оптимальной производительности и надежности hello службы хранилищем ключей AZURE.</span><span class="sxs-lookup"><span data-stu-id="efe9d-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="efe9d-106">Ограничения регулирования различаются в зависимости от сценария hello.</span><span class="sxs-lookup"><span data-stu-id="efe9d-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="efe9d-107">Например при выполнении большой объем операций записи hello возможность регулирования больше, чем если только выполняются операции чтения.</span><span class="sxs-lookup"><span data-stu-id="efe9d-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="efe9d-108">Как хранилище ключей обрабатывает свои ограничения?</span><span class="sxs-lookup"><span data-stu-id="efe9d-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="efe9d-109">Ограничения службы в хранилище ключей существуют tooprevent неправильное использование ресурсов и обеспечения качества обслуживания для всех клиентов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="efe9d-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="efe9d-110">При превышении порогового значения службы хранилище ключей ограничивает все последующие запросы от этого клиента на определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="efe9d-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="efe9d-111">В этом случае хранилище ключей возвращает код состояния HTTP 429 (слишком много запросов), и при сбое запросов hello.</span><span class="sxs-lookup"><span data-stu-id="efe9d-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="efe9d-112">Кроме того неудачных запросов, возвращающих 429 учитываются при определении ограничения регулирования hello отслеживается хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="efe9d-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="efe9d-113">Если у вас есть реальный пример использования с более высокими ограничениями регулирования, пожалуйста, расскажите нам о нем.</span><span class="sxs-lookup"><span data-stu-id="efe9d-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="efe9d-114">Как toothrottle приложения в ответ tooservice ограничивает</span><span class="sxs-lookup"><span data-stu-id="efe9d-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="efe9d-115">Hello ниже приведены **рекомендации** для регулирования приложения:</span><span class="sxs-lookup"><span data-stu-id="efe9d-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="efe9d-116">Сократите число hello операций на запрос.</span><span class="sxs-lookup"><span data-stu-id="efe9d-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="efe9d-117">Уменьшите частоту hello запросов.</span><span class="sxs-lookup"><span data-stu-id="efe9d-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="efe9d-118">Избегайте немедленных повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="efe9d-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="efe9d-119">Все запросы учитываются, и их количество сравнивается с ограничениями использования.</span><span class="sxs-lookup"><span data-stu-id="efe9d-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="efe9d-120">При реализации обработки ошибок приложения используйте hello HTTP ошибки кода 429 toodetect hello требуются для регулирования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="efe9d-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="efe9d-121">Если запрос hello снова происходит сбой с кодом ошибки HTTP 429, удастся устранить ограничения службы Azure.</span><span class="sxs-lookup"><span data-stu-id="efe9d-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="efe9d-122">Продолжайте toouse hello рекомендуется регулирования клиентский метод, повторная попытка запроса hello до ее успешного завершения.</span><span class="sxs-lookup"><span data-stu-id="efe9d-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="efe9d-123">Рекомендуемый метод регулирования на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="efe9d-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="efe9d-124">При возврате кода ошибки HTTP 429 начните регулирование клиента с помощью метода экспоненциального откладывания:</span><span class="sxs-lookup"><span data-stu-id="efe9d-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="efe9d-125">Подождите 1 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="efe9d-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="efe9d-126">Если запрос по-прежнему не выполнен, подождите 2 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="efe9d-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="efe9d-127">Если запрос по-прежнему не выполнен, подождите 4 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="efe9d-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="efe9d-128">Если запрос по-прежнему не выполнен, подождите 8 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="efe9d-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="efe9d-129">Если запрос по-прежнему не выполнен, подождите 16 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="efe9d-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="efe9d-130">На этом этапе вы не должны получать коды ответа HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="efe9d-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="efe9d-131">См. также</span><span class="sxs-lookup"><span data-stu-id="efe9d-131">See also</span></span>

<span data-ttu-id="efe9d-132">Более глубокого ориентацию регулирования для hello Microsoft Cloud см [регулирования шаблон](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="efe9d-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

