---
title: "проблемы доступности aaaApplication и службы для облачных служб Microsoft Azure часто задаваемые вопросы о | Документы Microsoft"
description: "В этой статье перечислены hello часто задаваемые вопросы о приложении и доступность службы для облачных служб Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="2b9f9-103">Проблемы доступности приложений и служб для облачных служб Azure. Вопросы и ответы (FAQ)</span><span class="sxs-lookup"><span data-stu-id="2b9f9-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="2b9f9-104">В этой статье приведены часто задаваемые вопросы по доступности приложений и служб для [облачных служб Microsoft Azure](https://azure.microsoft.com/services/cloud-services).</span><span class="sxs-lookup"><span data-stu-id="2b9f9-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="2b9f9-105">Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="2b9f9-106">Моя роль была возобновлена.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-106">My role got recycled.</span></span> <span data-ttu-id="2b9f9-107">Было ли развернуто какое-либо обновление для моей облачной службы?</span><span class="sxs-lookup"><span data-stu-id="2b9f9-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="2b9f9-108">Примерно раз в месяц корпорация Майкрософт выпускает новую версию гостевой ОС для виртуальных машин PaaS Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="2b9f9-109"> Гостевая ОС — только одно из таких обновлений в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-109"> The Guest OS is only one such update in hello pipeline.</span></span> <span data-ttu-id="2b9f9-110">На выпуск может влиять множество факторов.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="2b9f9-111">Кроме того, Azure работает на сотнях тысяч компьютеров.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="2b9f9-112">Таким образом это невозможно toopredict hello точную дату и время, когда будут перезапущены ваши роли.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-112">Therefore, it's impossible toopredict hello exact date and time when your roles will reboot.</span></span> <span data-ttu-id="2b9f9-113">Мы обновления гостевой ОС RSS-канал обновления hello с последними сведениями hello, у нас есть, но рекомендуется, сообщения о времени toobe приблизительное значение.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-113">We update hello Guest OS Update RSS Feed with hello latest information that we have, but you should consider that reported time toobe an approximate value.</span></span> <span data-ttu-id="2b9f9-114">Мы знали, что это создает проблему для клиентов и работе toolimit плана или точного времени после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-114">We are aware that this is problematic for customers and are working on a plan toolimit or precisely time reboots.</span></span>

<span data-ttu-id="2b9f9-115">Полные сведения о последних обновлениях гостевой ОС см. в статье [Выпуски гостевой ОС Azure и таблица совместимости пакетов SDK](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="2b9f9-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="2b9f9-116">Полезные сведения о перезапусках и указатели tootechnical обновлений гостевой и базовой ОС см. в разделе блога MSDN hello [роли экземпляра перезапускается из-за обновления tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b9f9-116">For helpful information on restarts and pointers tootechnical details of Guest and Host OS updates, see hello MSDN blog post [Role Instance Restarts Due tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="2b9f9-117">Почему hello первый запрос toomy облачной службы после простоя службы hello в течение некоторого времени требуется больше времени?</span><span class="sxs-lookup"><span data-stu-id="2b9f9-117">Why does hello first request toomy cloud service after hello service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="2b9f9-118">Когда hello веб-сервер получает первый запрос hello, он сначала повторных компиляций кода hello и затем обрабатывает запрос hello.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-118">When hello Web Server receives hello first request, it first recompiles hello code and then processes hello request.</span></span> <span data-ttu-id="2b9f9-119">Почему hello первый запрос занимает больше времени, чем hello другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-119">That's why hello first request takes longer than hello others.</span></span> <span data-ttu-id="2b9f9-120">По умолчанию пула приложения hello возвращает завершена в случаях отсутствия активности пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-120">By default, hello app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="2b9f9-121">Hello приложения также перезапуск пула по умолчанию каждые 1,740 минут (29 часов).</span><span class="sxs-lookup"><span data-stu-id="2b9f9-121">hello app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="2b9f9-122">Пулы приложений Internet Information Services (IIS) может быть нестабильным периодически перезапущен tooavoid состояний, которые может вызвать сбои tooapplication, зависает или утечки памяти.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-122">Internet Information Services (IIS) application pools can be periodically recycled tooavoid unstable states that can lead tooapplication crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="2b9f9-123">следующие документы Hello помогут понять и решить эту проблему:</span><span class="sxs-lookup"><span data-stu-id="2b9f9-123">hello following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="2b9f9-124">Исправление медленной начальной загрузки для служб IIS</span><span class="sxs-lookup"><span data-stu-id="2b9f9-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="2b9f9-125">Очень медленный первый запрос веб-приложения IIS 7.5 после перезапуска пула приложений</span><span class="sxs-lookup"><span data-stu-id="2b9f9-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="2b9f9-126">Если требуется поведение по умолчанию hello toochange служб IIS, необходимо будет toouse задачи запуска, так как при установке вручную экземпляров веб-роли toohello изменения hello изменения в конечном счете будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="2b9f9-126">If you want toochange hello default behavior of IIS, you will need toouse startup tasks, because if you manually apply changes toohello Web Role instances, hello changes will eventually be lost.</span></span>

<span data-ttu-id="2b9f9-127">Дополнительные сведения см. в разделе [как tooconfigure и выполнения запуска задачи для облачной службы](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="2b9f9-127">For more information, see [How tooconfigure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
