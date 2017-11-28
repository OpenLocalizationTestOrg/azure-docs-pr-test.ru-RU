---
ms.assetid: 
title: "Руководство по регулированию хранилища ключей Azure | Документы Майкрософт"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="2cd39-102">Руководство по регулированию хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="2cd39-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="2cd39-103">Регулирование — это процесс, позволяющий ограничить число одновременных вызовов к службе Azure для предотвращения чрезмерного использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2cd39-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="2cd39-104">Хранилище ключей Azure (AKV) может обрабатывать большое число запросов.</span><span class="sxs-lookup"><span data-stu-id="2cd39-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="2cd39-105">Если это число превышает приемлемое, для обеспечения оптимальной производительности и надежности службы AKV используется регулирование клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="2cd39-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="2cd39-106">Ограничения регулирования зависят от сценария.</span><span class="sxs-lookup"><span data-stu-id="2cd39-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="2cd39-107">Например, при выполнении большого объема операций записи возможность регулирования будет более высокой по сравнению с ситуацией, когда выполняются только операции чтения.</span><span class="sxs-lookup"><span data-stu-id="2cd39-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="2cd39-108">Как хранилище ключей обрабатывает свои ограничения?</span><span class="sxs-lookup"><span data-stu-id="2cd39-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="2cd39-109">Для предотвращения некорректного использования ресурсов и обеспечения качества обслуживания для всех клиентов хранилища ключей в самом хранилище существуют ограничения служб.</span><span class="sxs-lookup"><span data-stu-id="2cd39-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="2cd39-110">При превышении порогового значения службы хранилище ключей ограничивает все последующие запросы от этого клиента на определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="2cd39-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="2cd39-111">В этом случае хранилище ключей возвращает код состояния HTTP 429 (слишком много запросов), и запросы завершаются сбоем.</span><span class="sxs-lookup"><span data-stu-id="2cd39-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="2cd39-112">Кроме того, хранилище ключей подсчитывает невыполненные запросы, возвращающих код состояния 429, и сравнивает их с ограничениями регулирования.</span><span class="sxs-lookup"><span data-stu-id="2cd39-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="2cd39-113">Если у вас есть реальный пример использования с более высокими ограничениями регулирования, пожалуйста, расскажите нам о нем.</span><span class="sxs-lookup"><span data-stu-id="2cd39-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="2cd39-114">Регулирование приложения в ответ на ограничения служб</span><span class="sxs-lookup"><span data-stu-id="2cd39-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="2cd39-115">Ниже приведены **рекомендации** по регулированию приложения.</span><span class="sxs-lookup"><span data-stu-id="2cd39-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="2cd39-116">Сократите число операций на один запрос.</span><span class="sxs-lookup"><span data-stu-id="2cd39-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="2cd39-117">Уменьшите частоту запросов.</span><span class="sxs-lookup"><span data-stu-id="2cd39-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="2cd39-118">Избегайте немедленных повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="2cd39-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="2cd39-119">Все запросы учитываются, и их количество сравнивается с ограничениями использования.</span><span class="sxs-lookup"><span data-stu-id="2cd39-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="2cd39-120">При реализации обработки ошибок для приложения используйте код ошибки HTTP 429, чтобы определить необходимость регулирования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="2cd39-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="2cd39-121">Если запрос снова завершается сбоем с кодом ошибки HTTP 429, это означает, что вы по-прежнему не соблюдаете ограничения службы Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd39-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="2cd39-122">Продолжайте использовать рекомендуемый метод регулирования на стороне клиента и повторяйте выполнять запрос, пока он не будет успешно выполнен.</span><span class="sxs-lookup"><span data-stu-id="2cd39-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="2cd39-123">Рекомендуемый метод регулирования на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="2cd39-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="2cd39-124">При возврате кода ошибки HTTP 429 начните регулирование клиента с помощью метода экспоненциального откладывания:</span><span class="sxs-lookup"><span data-stu-id="2cd39-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="2cd39-125">Подождите 1 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="2cd39-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="2cd39-126">Если запрос по-прежнему не выполнен, подождите 2 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="2cd39-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="2cd39-127">Если запрос по-прежнему не выполнен, подождите 4 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="2cd39-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="2cd39-128">Если запрос по-прежнему не выполнен, подождите 8 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="2cd39-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="2cd39-129">Если запрос по-прежнему не выполнен, подождите 16 с и повторите запрос</span><span class="sxs-lookup"><span data-stu-id="2cd39-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="2cd39-130">На этом этапе вы не должны получать коды ответа HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="2cd39-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="2cd39-131">См. также</span><span class="sxs-lookup"><span data-stu-id="2cd39-131">See also</span></span>

<span data-ttu-id="2cd39-132">Более подробные сведения о регулировании для Microsoft Cloud см. в разделе [Шаблон регулирования](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="2cd39-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

