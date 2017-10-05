---
title: "Дополнительная информация о регулировании в службах BizTalk | Документация Майкрософт"
description: "Узнайте о пороговых значениях регулирования и соответствующем поведении среды выполнения для служб BizTalk. Регулирование основывается на использовании памяти и количестве сообщений. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="5b15a-105">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="5b15a-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="5b15a-106">Службы Azure BizTalk реализуют регулирование служб на основе двух условий: использования памяти и числа одновременно обрабатываемых сообщений.</span><span class="sxs-lookup"><span data-stu-id="5b15a-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="5b15a-107">В этом разделе содержатся сведения о пороговых значениях регулирования и описывается поведение среды выполнения при возникновении условия регулирования.</span><span class="sxs-lookup"><span data-stu-id="5b15a-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="5b15a-108">Пороги регулирования</span><span class="sxs-lookup"><span data-stu-id="5b15a-108">Throttling Thresholds</span></span>
<span data-ttu-id="5b15a-109">В следующей таблице перечислены источник и пороговые значения регулирования:</span><span class="sxs-lookup"><span data-stu-id="5b15a-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="5b15a-110">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="5b15a-110">Description</span></span> | <span data-ttu-id="5b15a-111">Нижнее пороговое значение</span><span class="sxs-lookup"><span data-stu-id="5b15a-111">Low Threshold</span></span> | <span data-ttu-id="5b15a-112">Верхнее пороговое значение</span><span class="sxs-lookup"><span data-stu-id="5b15a-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b15a-113">Память</span><span class="sxs-lookup"><span data-stu-id="5b15a-113">Memory</span></span> |<span data-ttu-id="5b15a-114">% всей доступной системной памяти/PageFileBytes (количество байтов файла подкачки).</span><span class="sxs-lookup"><span data-stu-id="5b15a-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="5b15a-115">Итоговое доступное количество байтов файла подкачки приблизительно в 2 раза превышает ОЗУ в системе.</span><span class="sxs-lookup"><span data-stu-id="5b15a-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="5b15a-116">60 %</span><span class="sxs-lookup"><span data-stu-id="5b15a-116">60%</span></span> |<span data-ttu-id="5b15a-117">70 %</span><span class="sxs-lookup"><span data-stu-id="5b15a-117">70%</span></span> |
| <span data-ttu-id="5b15a-118">Обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="5b15a-118">Message Processing</span></span> |<span data-ttu-id="5b15a-119">Число сообщений, обрабатываемых одновременно</span><span class="sxs-lookup"><span data-stu-id="5b15a-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="5b15a-120">40 * число ядер</span><span class="sxs-lookup"><span data-stu-id="5b15a-120">40 * number of cores</span></span> |<span data-ttu-id="5b15a-121">100 * число ядер</span><span class="sxs-lookup"><span data-stu-id="5b15a-121">100 * number of cores</span></span> |

<span data-ttu-id="5b15a-122">При достижении верхнего порогового значения в службах BizTalk для Azure запускается регулирование.</span><span class="sxs-lookup"><span data-stu-id="5b15a-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="5b15a-123">Регулирование прекращается при достижении нижнего порогового значения.</span><span class="sxs-lookup"><span data-stu-id="5b15a-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="5b15a-124">Например, служба использует 65 % системной памяти.</span><span class="sxs-lookup"><span data-stu-id="5b15a-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="5b15a-125">В этом случае служба не ведет регулирование.</span><span class="sxs-lookup"><span data-stu-id="5b15a-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="5b15a-126">Использование системной памяти повышается до 70 %.</span><span class="sxs-lookup"><span data-stu-id="5b15a-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="5b15a-127">В этом случае служба начинает регулирование, которое продолжается до того момента, пока загрузка системной памяти не снизится до 60 % (нижнее пороговое значение).</span><span class="sxs-lookup"><span data-stu-id="5b15a-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="5b15a-128">Службы BizTalk для Azure отслеживают состояние регулирования (обычный режим и регулируемый режим), а также продолжительность регулирования.</span><span class="sxs-lookup"><span data-stu-id="5b15a-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="5b15a-129">Поведение во время выполнения</span><span class="sxs-lookup"><span data-stu-id="5b15a-129">Runtime Behavior</span></span>
<span data-ttu-id="5b15a-130">Когда службы BizTalk для Azure переключаются в состояние регулирования, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="5b15a-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="5b15a-131">Регулирование осуществляется для отдельных экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="5b15a-131">Throttling is per role instance.</span></span> <span data-ttu-id="5b15a-132">Например:</span><span class="sxs-lookup"><span data-stu-id="5b15a-132">For example:</span></span><br/>
  <span data-ttu-id="5b15a-133">RoleInstanceA выполняет регулирование.</span><span class="sxs-lookup"><span data-stu-id="5b15a-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="5b15a-134">RoleInstanceB не ведет регулирование.</span><span class="sxs-lookup"><span data-stu-id="5b15a-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="5b15a-135">В этом случае сообщения в RoleInstanceB обрабатываются как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="5b15a-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="5b15a-136">Сообщения в RoleInstanceA отклоняются и завершаются со следующей ошибкой:</span><span class="sxs-lookup"><span data-stu-id="5b15a-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="5b15a-137">
  **Сервер занят. Повторите попытку позже.**</span><span class="sxs-lookup"><span data-stu-id="5b15a-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="5b15a-138">Ни один запрашивающий источник не ведет опрос и не загружает сообщение.</span><span class="sxs-lookup"><span data-stu-id="5b15a-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="5b15a-139">Например,</span><span class="sxs-lookup"><span data-stu-id="5b15a-139">For example:</span></span><br/>
  <span data-ttu-id="5b15a-140">конвейер извлекает сообщения из внешнего FTP-источника.</span><span class="sxs-lookup"><span data-stu-id="5b15a-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="5b15a-141">Экземпляр роли, посылающий запрос на извлечение, переходит в состояние регулирования.</span><span class="sxs-lookup"><span data-stu-id="5b15a-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="5b15a-142">В этом случае загрузка дополнительных сообщений в конвейере приостанавливается до прекращения регулирования для этого экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="5b15a-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="5b15a-143">Клиенту отправляется ответ, чтобы он мог повторно отправить это сообщение.</span><span class="sxs-lookup"><span data-stu-id="5b15a-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="5b15a-144">Необходимо дождаться, когда регулирование будет завершено.</span><span class="sxs-lookup"><span data-stu-id="5b15a-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="5b15a-145">В частности, следует дождаться момента достижения нижнего порогового значения.</span><span class="sxs-lookup"><span data-stu-id="5b15a-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="5b15a-146">Важные примечания</span><span class="sxs-lookup"><span data-stu-id="5b15a-146">Important notes</span></span>
* <span data-ttu-id="5b15a-147">Регулирование нельзя отключить.</span><span class="sxs-lookup"><span data-stu-id="5b15a-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="5b15a-148">Пороговые значения регулирования нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="5b15a-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="5b15a-149">Регулирование реализуется на уровне всей системы.</span><span class="sxs-lookup"><span data-stu-id="5b15a-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="5b15a-150">Сервер базы данных SQL Azure имеет также и встроенное регулирование.</span><span class="sxs-lookup"><span data-stu-id="5b15a-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="5b15a-151">Дополнительная информация о службах BizTalk в Azure</span><span class="sxs-lookup"><span data-stu-id="5b15a-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="5b15a-152">Установка пакета SDK для служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="5b15a-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="5b15a-153">Руководства по службам BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="5b15a-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="5b15a-154">Как приступить к работе с пакетом SDK для служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="5b15a-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="5b15a-155">Службы BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="5b15a-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="5b15a-156">См. также</span><span class="sxs-lookup"><span data-stu-id="5b15a-156">See Also</span></span>
* [<span data-ttu-id="5b15a-157">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="5b15a-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="5b15a-158">Службы BizTalk: подготовка с использованием классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="5b15a-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="5b15a-159">Службы BizTalk. Диаграмма состояния подготовки</span><span class="sxs-lookup"><span data-stu-id="5b15a-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="5b15a-160">Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»</span><span class="sxs-lookup"><span data-stu-id="5b15a-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="5b15a-161">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="5b15a-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="5b15a-162">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="5b15a-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

