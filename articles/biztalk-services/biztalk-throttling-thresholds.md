---
title: "aaaLearn о регулирование в службах BizTalk | Документы Microsoft"
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="13ee1-105">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="13ee1-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="13ee1-106">Службы BizTalk Azure реализует регулирование службы на основе двух условий: памяти использования и hello количество одновременных сообщений обработки.</span><span class="sxs-lookup"><span data-stu-id="13ee1-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="13ee1-107">В этом разделе перечислены hello регулирования пороговых значений и описывает hello поведения во время выполнения при возникновении условия регулирования.</span><span class="sxs-lookup"><span data-stu-id="13ee1-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="13ee1-108">Пороги регулирования</span><span class="sxs-lookup"><span data-stu-id="13ee1-108">Throttling Thresholds</span></span>
<span data-ttu-id="13ee1-109">Привет, в следующей таблице перечислены hello регулирования источника и пороговых значений:</span><span class="sxs-lookup"><span data-stu-id="13ee1-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="13ee1-110">Описание</span><span class="sxs-lookup"><span data-stu-id="13ee1-110">Description</span></span> | <span data-ttu-id="13ee1-111">Нижнее пороговое значение</span><span class="sxs-lookup"><span data-stu-id="13ee1-111">Low Threshold</span></span> | <span data-ttu-id="13ee1-112">Верхнее пороговое значение</span><span class="sxs-lookup"><span data-stu-id="13ee1-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13ee1-113">Память</span><span class="sxs-lookup"><span data-stu-id="13ee1-113">Memory</span></span> |<span data-ttu-id="13ee1-114">% всей доступной системной памяти/PageFileBytes (количество байтов файла подкачки).</span><span class="sxs-lookup"><span data-stu-id="13ee1-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="13ee1-115">Общее доступных PageFileBytes приблизительно — в два раза hello ОЗУ системы hello.</span><span class="sxs-lookup"><span data-stu-id="13ee1-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="13ee1-116">60 %</span><span class="sxs-lookup"><span data-stu-id="13ee1-116">60%</span></span> |<span data-ttu-id="13ee1-117">70 %</span><span class="sxs-lookup"><span data-stu-id="13ee1-117">70%</span></span> |
| <span data-ttu-id="13ee1-118">Обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="13ee1-118">Message Processing</span></span> |<span data-ttu-id="13ee1-119">Число сообщений, обрабатываемых одновременно</span><span class="sxs-lookup"><span data-stu-id="13ee1-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="13ee1-120">40 * число ядер</span><span class="sxs-lookup"><span data-stu-id="13ee1-120">40 * number of cores</span></span> |<span data-ttu-id="13ee1-121">100 * число ядер</span><span class="sxs-lookup"><span data-stu-id="13ee1-121">100 * number of cores</span></span> |

<span data-ttu-id="13ee1-122">При достижении верхнего порогового значения службы BizTalk Azure запускает toothrottle.</span><span class="sxs-lookup"><span data-stu-id="13ee1-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="13ee1-123">Регулирование останавливается при достижении hello нижнее пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="13ee1-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="13ee1-124">Например, служба использует 65 % системной памяти.</span><span class="sxs-lookup"><span data-stu-id="13ee1-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="13ee1-125">В этом случае служба hello не регулирование.</span><span class="sxs-lookup"><span data-stu-id="13ee1-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="13ee1-126">Использование системной памяти повышается до 70 %.</span><span class="sxs-lookup"><span data-stu-id="13ee1-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="13ee1-127">В этом случае служба hello регулирует и toothrottle продолжается, пока служба hello использует системную память 60% (нижнее пороговое значение).</span><span class="sxs-lookup"><span data-stu-id="13ee1-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="13ee1-128">Служб BizTalk Azure отслеживает hello регулирования состояния (нормальное состояние и состояние регулированию) и регулирования длительность hello.</span><span class="sxs-lookup"><span data-stu-id="13ee1-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="13ee1-129">Поведение во время выполнения</span><span class="sxs-lookup"><span data-stu-id="13ee1-129">Runtime Behavior</span></span>
<span data-ttu-id="13ee1-130">Когда службы BizTalk Azure переходит в состояние регулирования, происходит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="13ee1-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="13ee1-131">Регулирование осуществляется для отдельных экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="13ee1-131">Throttling is per role instance.</span></span> <span data-ttu-id="13ee1-132">Например:</span><span class="sxs-lookup"><span data-stu-id="13ee1-132">For example:</span></span><br/>
  <span data-ttu-id="13ee1-133">RoleInstanceA выполняет регулирование.</span><span class="sxs-lookup"><span data-stu-id="13ee1-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="13ee1-134">RoleInstanceB не ведет регулирование.</span><span class="sxs-lookup"><span data-stu-id="13ee1-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="13ee1-135">В этом случае сообщения в RoleInstanceB обрабатываются как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="13ee1-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="13ee1-136">Сообщения в RoleInstanceA отбрасываются и завершаться hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="13ee1-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="13ee1-137">
  **Сервер занят. Повторите попытку позже.**</span><span class="sxs-lookup"><span data-stu-id="13ee1-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="13ee1-138">Ни один запрашивающий источник не ведет опрос и не загружает сообщение.</span><span class="sxs-lookup"><span data-stu-id="13ee1-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="13ee1-139">Например,</span><span class="sxs-lookup"><span data-stu-id="13ee1-139">For example:</span></span><br/>
  <span data-ttu-id="13ee1-140">конвейер извлекает сообщения из внешнего FTP-источника.</span><span class="sxs-lookup"><span data-stu-id="13ee1-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="13ee1-141">экземпляр роли Hello выполнив hello запросу возвращает в состоянии регулирования.</span><span class="sxs-lookup"><span data-stu-id="13ee1-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="13ee1-142">В этом случае конвейера hello останавливает загрузка дополнительных сообщений, пока экземпляр роли hello перестанет регулирования.</span><span class="sxs-lookup"><span data-stu-id="13ee1-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="13ee1-143">Клиент toohello отправляется ответ, клиент hello можно повторно отправить сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="13ee1-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="13ee1-144">Дождитесь, пока не будет устранена регулирования hello.</span><span class="sxs-lookup"><span data-stu-id="13ee1-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="13ee1-145">В частности необходимо дождаться, пока достигается hello нижнее пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="13ee1-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="13ee1-146">Важные примечания</span><span class="sxs-lookup"><span data-stu-id="13ee1-146">Important notes</span></span>
* <span data-ttu-id="13ee1-147">Регулирование нельзя отключить.</span><span class="sxs-lookup"><span data-stu-id="13ee1-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="13ee1-148">Пороговые значения регулирования нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="13ee1-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="13ee1-149">Регулирование реализуется на уровне всей системы.</span><span class="sxs-lookup"><span data-stu-id="13ee1-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="13ee1-150">Hello сервера базы данных SQL Azure имеет встроенные регулирования.</span><span class="sxs-lookup"><span data-stu-id="13ee1-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="13ee1-151">Дополнительная информация о службах BizTalk в Azure</span><span class="sxs-lookup"><span data-stu-id="13ee1-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="13ee1-152">Установка пакета SDK служб BizTalk Azure hello</span><span class="sxs-lookup"><span data-stu-id="13ee1-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="13ee1-153">Руководства по службам BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="13ee1-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="13ee1-154">Как я запустить с помощью hello пакета SDK служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="13ee1-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="13ee1-155">Службы BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="13ee1-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="13ee1-156">См. также</span><span class="sxs-lookup"><span data-stu-id="13ee1-156">See Also</span></span>
* [<span data-ttu-id="13ee1-157">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="13ee1-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="13ee1-158">Службы BizTalk: подготовка с использованием классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="13ee1-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="13ee1-159">Службы BizTalk. Диаграмма состояния подготовки</span><span class="sxs-lookup"><span data-stu-id="13ee1-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="13ee1-160">Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»</span><span class="sxs-lookup"><span data-stu-id="13ee1-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="13ee1-161">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="13ee1-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="13ee1-162">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="13ee1-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

