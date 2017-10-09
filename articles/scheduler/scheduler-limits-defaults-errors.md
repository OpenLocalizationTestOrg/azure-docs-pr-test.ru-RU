---
title: "Ограничения aaaScheduler и значения по умолчанию"
description: "Ограничения и значения по умолчанию планировщика"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="dd6c2-103">Ограничения и значения по умолчанию планировщика</span><span class="sxs-lookup"><span data-stu-id="dd6c2-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="dd6c2-104">Квоты планировщика, ограничения, значения по умолчанию и регулирования</span><span class="sxs-lookup"><span data-stu-id="dd6c2-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="dd6c2-105">Здравствуйте x-ms-request-id заголовка</span><span class="sxs-lookup"><span data-stu-id="dd6c2-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="dd6c2-106">Каждый запрос к hello служба планировщика возвращает заголовок ответа с именем**x-ms-request-id**. Этот заголовок содержит Непрозрачное значение, которое однозначно идентифицирует запрос hello.</span><span class="sxs-lookup"><span data-stu-id="dd6c2-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="dd6c2-107">Если запрос постоянно неудачей и вы проверили hello Запрос сформулирован должным, может использовать это значение tooreport hello ошибки tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="dd6c2-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="dd6c2-108">В отчете, включить hello значение x-ms-request-id hello приблизительное время, hello запрос был сделан, hello идентификатор подписки hello, коллекции заданий и/или задания и hello тип операции, hello попытки запроса.</span><span class="sxs-lookup"><span data-stu-id="dd6c2-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="dd6c2-109">См. также</span><span class="sxs-lookup"><span data-stu-id="dd6c2-109">See Also</span></span>
 [<span data-ttu-id="dd6c2-110">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="dd6c2-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="dd6c2-111">Основные понятия, терминология и иерархия сущностей планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="dd6c2-112">Начало работы с планировщиком в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="dd6c2-113">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="dd6c2-114">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="dd6c2-115">Справочник по командлетам PowerShell планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="dd6c2-116">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="dd6c2-117">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="dd6c2-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

