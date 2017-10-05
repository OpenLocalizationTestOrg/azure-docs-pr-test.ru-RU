---
title: "Вопросы и ответы по доступности приложений и служб для облачных служб Microsoft Azure | Документы Майкрософт"
description: "В этой статье приведены часто задаваемые вопросы по доступности приложений и служб для облачных служб Microsoft Azure."
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
ms.openlocfilehash: a893a6d009dd018ad440964419e0a5a1963084b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="2a8b0-103">Проблемы доступности приложений и служб для облачных служб Azure. Вопросы и ответы (FAQ)</span><span class="sxs-lookup"><span data-stu-id="2a8b0-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="2a8b0-104">В этой статье приведены часто задаваемые вопросы по доступности приложений и служб для [облачных служб Microsoft Azure](https://azure.microsoft.com/services/cloud-services).</span><span class="sxs-lookup"><span data-stu-id="2a8b0-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="2a8b0-105">Сведения о размерах приводятся в статье [Размеры для облачных служб](cloud-services-sizes-specs.md) .</span><span class="sxs-lookup"><span data-stu-id="2a8b0-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="2a8b0-106">Моя роль была возобновлена.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-106">My role got recycled.</span></span> <span data-ttu-id="2a8b0-107">Было ли развернуто какое-либо обновление для моей облачной службы?</span><span class="sxs-lookup"><span data-stu-id="2a8b0-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="2a8b0-108">Примерно раз в месяц корпорация Майкрософт выпускает новую версию гостевой ОС для виртуальных машин PaaS Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="2a8b0-109"> Гостевая ОС — только одно из таких обновлений в конвейере.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-109"> The Guest OS is only one such update in the pipeline.</span></span> <span data-ttu-id="2a8b0-110">На выпуск может влиять множество факторов.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="2a8b0-111">Кроме того, Azure работает на сотнях тысяч компьютеров.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="2a8b0-112">Это означает, что невозможно предсказать точную дату и время перезапуска ваших ролей.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-112">Therefore, it's impossible to predict the exact date and time when your roles will reboot.</span></span> <span data-ttu-id="2a8b0-113">Корпорация Майкрософт будет размещать на RSS-канале обновлений гостевой ОС последние сведения, которыми мы располагаем, но указанные временные рамки следует воспринимать только в качестве приблизительных.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-113">We update the Guest OS Update RSS Feed with the latest information that we have, but you should consider that reported time to be an approximate value.</span></span> <span data-ttu-id="2a8b0-114">Мы осознаем, что это вызывает неудобства для клиентов, и работаем над планом по ограничению перезапусков или уточнению их времени.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-114">We are aware that this is problematic for customers and are working on a plan to limit or precisely time reboots.</span></span>

<span data-ttu-id="2a8b0-115">Полные сведения о последних обновлениях гостевой ОС см. в статье [Выпуски гостевой ОС Azure и таблица совместимости пакетов SDK](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="2a8b0-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="2a8b0-116">Полезные сведения о перезапусках и ссылки на дополнительную техническую информацию по обновлениям гостевой и базовой ОС см. в записи блога MSDN [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx) (Перезапуски экземпляров ролей из-за обновлений ОС).</span><span class="sxs-lookup"><span data-stu-id="2a8b0-116">For helpful information on restarts and pointers to technical details of Guest and Host OS updates, see the MSDN blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-the-first-request-to-my-cloud-service-after-the-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="2a8b0-117">Почему первый запрос в облачную службу после простоя службы в течение некоторого времени занимает больше времени, чем обычно?</span><span class="sxs-lookup"><span data-stu-id="2a8b0-117">Why does the first request to my cloud service after the service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="2a8b0-118">Когда веб-сервер получает первый запрос, он сначала перекомпилирует код, а затем обрабатывает запрос.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-118">When the Web Server receives the first request, it first recompiles the code and then processes the request.</span></span> <span data-ttu-id="2a8b0-119">Вот почему первый запрос занимает больше времени, чем другие.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-119">That's why the first request takes longer than the others.</span></span> <span data-ttu-id="2a8b0-120">По умолчанию пул приложений завершает работу в случае бездействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-120">By default, the app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="2a8b0-121">Пул приложений также будет перезапускаться по умолчанию каждые 1,740 минут (29 часов).</span><span class="sxs-lookup"><span data-stu-id="2a8b0-121">The app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="2a8b0-122">Пулы приложений служб IIS могут периодически перезапускаться во избежание нестабильных состояний, которые могут привести к аварийному завершению приложений, зависаниям или утечкам памяти.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-122">Internet Information Services (IIS) application pools can be periodically recycled to avoid unstable states that can lead to application crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="2a8b0-123">Следующие документы помогут вам понять и решить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-123">The following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="2a8b0-124">Исправление медленной начальной загрузки для служб IIS</span><span class="sxs-lookup"><span data-stu-id="2a8b0-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="2a8b0-125">Очень медленный первый запрос веб-приложения IIS 7.5 после перезапуска пула приложений</span><span class="sxs-lookup"><span data-stu-id="2a8b0-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="2a8b0-126">Если вы хотите изменить поведение по умолчанию служб IIS, необходимо будет использовать задачи при запуске, так как если вручную применить изменения к экземплярам веб-роли, в итоге изменения будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="2a8b0-126">If you want to change the default behavior of IIS, you will need to use startup tasks, because if you manually apply changes to the Web Role instances, the changes will eventually be lost.</span></span>

<span data-ttu-id="2a8b0-127">Дополнительные сведения см. в статье [Как настроить и выполнить задачи при запуске для облачной службы](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="2a8b0-127">For more information, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
