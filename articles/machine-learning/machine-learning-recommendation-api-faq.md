---
title: "Настройка и использование API рекомендаций для машинного обучения | Документация Майкрософт"
description: "Microsoft RECOMMENDATIONS API, созданный с помощью часто задаваемых вопросов и ответов по Машинному обучению Azure"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="e0912-103">Часто задаваемые вопросы о настройке и использовании API рекомендаций для машинного обучения</span><span class="sxs-lookup"><span data-stu-id="e0912-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="e0912-104">**Что представляет собой служба «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="e0912-105">Начните использовать когнитивную службу API рекомендаций вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="e0912-105">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="e0912-106">Когнитивная служба рекомендаций заменит эту службу, и все новые функции будут разрабатываться в ней.</span><span class="sxs-lookup"><span data-stu-id="e0912-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="e0912-107">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="e0912-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="e0912-108">Узнайте больше о [переходе на новую когнитивную службу](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="e0912-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="e0912-109">Для организаций и компаний, которые полагаются на рекомендации для перекрестных продаж товаров и услуг, а также увеличения их продаж, служба «РЕКОМЕНДАЦИИ», являющаяся частью Машинного обучения Azure, представляет собой механизм самообслуживания для получения рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="e0912-109">For organizations and businesses that rely on recommendations to cross-sell and up-sell products and services to their customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="e0912-110">Это реализация функции совместной фильтрации, использующей факторизацию матрицы в качестве основного алгоритма.</span><span class="sxs-lookup"><span data-stu-id="e0912-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="e0912-111">Разработчики приложений могут получать доступ к службе «РЕКОМЕНДАЦИИ» с помощью интерфейсов REST API.</span><span class="sxs-lookup"><span data-stu-id="e0912-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e0912-112">**Для чего можно использовать службу «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="e0912-113">Служба "РЕКОМЕНДАЦИИ" принимает в качестве входных данных элемент или набор элементов и возвращает список соответствующих рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="e0912-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="e0912-114">Пример — клиент интернет-магазина выбирает продукт.</span><span class="sxs-lookup"><span data-stu-id="e0912-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="e0912-115">Интернет-магазин отправляет данные продукта в качестве входных данных в службу «РЕКОМЕНДАЦИИ», получает в ответ список продуктов и решает, какие из них будут показаны клиенту.</span><span class="sxs-lookup"><span data-stu-id="e0912-115">The online retailer sends that product as input to RECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown to the customer.</span></span> <span data-ttu-id="e0912-116">Вы можете использовать службу "РЕКОМЕНДАЦИИ" для оптимизации работы интернет-магазина или даже для информирования отдела продаж или колл-центра.</span><span class="sxs-lookup"><span data-stu-id="e0912-116">You may want to use RECOMMENDATIONS to optimize your online store or even to inform your inside sales department or call center.</span></span>

<span data-ttu-id="e0912-117">**Существуют ли какие-либо ограничения использования?**</span><span class="sxs-lookup"><span data-stu-id="e0912-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="e0912-118">Рекомендации имеют следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="e0912-118">Recommendations has the following usage limitations:</span></span>

* <span data-ttu-id="e0912-119">Максимальное число моделей на одну подписку — 10.</span><span class="sxs-lookup"><span data-stu-id="e0912-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="e0912-120">Максимальное количество элементов в каталоге: 100 000</span><span class="sxs-lookup"><span data-stu-id="e0912-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="e0912-121">Максимальное количество поддерживаемых точек использования — около 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="e0912-121">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="e0912-122">По мере поступления новых точек будут удаляться самые старые.</span><span class="sxs-lookup"><span data-stu-id="e0912-122">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="e0912-123">Максимальный размер данных, которые можно отправить по электронной почте (например, при импорте данных каталога, импорте данных по использованию), составляет 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="e0912-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="e0912-124">Число транзакций в секунду (TPS) для неактивной сборки модели рекомендаций — около 2.</span><span class="sxs-lookup"><span data-stu-id="e0912-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="e0912-125">Для активной сборки модели рекомендаций это значение может достигать 20 транзакций в секунду.</span><span class="sxs-lookup"><span data-stu-id="e0912-125">A Recommendations model build that is active can hold up to 20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="e0912-126">Покупка и выставление счетов</span><span class="sxs-lookup"><span data-stu-id="e0912-126">Purchase and Billing</span></span>
<span data-ttu-id="e0912-127">**Сколько стоит использование службы «РЕКОМЕНДАЦИИ» в стартовый период?**</span><span class="sxs-lookup"><span data-stu-id="e0912-127">**How much does Recommendations cost during the launch period?**</span></span>

<span data-ttu-id="e0912-128">"РЕКОМЕНДАЦИИ" — это служба на основе подписки.</span><span class="sxs-lookup"><span data-stu-id="e0912-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="e0912-129">Оплата осуществляется на основе количества транзакций в месяц.</span><span class="sxs-lookup"><span data-stu-id="e0912-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="e0912-130">Сведения о ценах см. на [странице предложений](https://datamarket.azure.com/dataset/amla/recommendations) в Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e0912-130">You can check the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="e0912-131">**Взимается ли какая-либо плата за отслеживание и/или сохранение информации о действиях пользователей службой «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="e0912-132">В данный момент нет.</span><span class="sxs-lookup"><span data-stu-id="e0912-132">Not at the moment.</span></span>

<span data-ttu-id="e0912-133">**Есть ли у службы «РЕКОМЕНДАЦИИ» бесплатная пробная версия?**</span><span class="sxs-lookup"><span data-stu-id="e0912-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="e0912-134">Во время бесплатного пробного периода служба ограничена 10 000 транзакций в месяц.</span><span class="sxs-lookup"><span data-stu-id="e0912-134">There is a free trail which is restricted to 10,000 transactions per month.</span></span>

<span data-ttu-id="e0912-135">**Когда мне будет выставлен счет за использование службы «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="e0912-136">Платная подписка — это подписка, за которую взимается ежемесячная плата.</span><span class="sxs-lookup"><span data-stu-id="e0912-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="e0912-137">При приобретении платной подписки с вас немедленно взимается плата за первый месяц.</span><span class="sxs-lookup"><span data-stu-id="e0912-137">When you purchase a paid subscription, you are immediately charged for the first month's use.</span></span> <span data-ttu-id="e0912-138">Взимается сумма, связанная с предложением на странице подписки (плюс применимые налоги).</span><span class="sxs-lookup"><span data-stu-id="e0912-138">You are charged the amount that is associated with the offer on the subscription page (plus applicable taxes).</span></span> <span data-ttu-id="e0912-139">Эта ежемесячная плата взимается каждый месяц в ту же календарную дату, в которую была осуществлена исходная покупка, пока подписка не будет отменена.</span><span class="sxs-lookup"><span data-stu-id="e0912-139">This monthly charge is made each month on the same calendar date as your original purchase until you cancel the subscription.</span></span> 

<span data-ttu-id="e0912-140">**Как обновить службу до более высокого уровня?**</span><span class="sxs-lookup"><span data-stu-id="e0912-140">**How do I upgrade to a higher tier service?**</span></span>

<span data-ttu-id="e0912-141">Вы можете приобрести или обновить подписку на [странице предложений](https://datamarket.azure.com/dataset/amla/recommendations) в Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e0912-141">You can buy or update your subscription from the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="e0912-142">При обновлении подписки:</span><span class="sxs-lookup"><span data-stu-id="e0912-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="e0912-143">Транзакции, остающиеся в старой подписке, не добавляются в новую.</span><span class="sxs-lookup"><span data-stu-id="e0912-143">Transactions that are remaining on your old subscription are not added to your new subscription.</span></span> 
* <span data-ttu-id="e0912-144">Вы оплачиваете полную стоимость новой подписки, даже если в вашей старой подписке есть неиспользованные транзакции.</span><span class="sxs-lookup"><span data-stu-id="e0912-144">You pay full price for the new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="e0912-145">Как обновить подписку:</span><span class="sxs-lookup"><span data-stu-id="e0912-145">Process to upgrade a subscription:</span></span>

* <span data-ttu-id="e0912-146">Перейдите на [страницу предложений](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="e0912-146">Nevigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="e0912-147">Войдите в Marketplace, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="e0912-147">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="e0912-148">На панели справа перечислены все доступные планы.</span><span class="sxs-lookup"><span data-stu-id="e0912-148">In the right pane, all the available plans are listed.</span></span> <span data-ttu-id="e0912-149">Щелкните переключатель для плана, который необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="e0912-149">Click the radio button for the plan you want to upgrade to.</span></span>
* <span data-ttu-id="e0912-150">Чтобы выполнить обновление, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0912-150">If you want to upgrade, click **OK**.</span></span> <span data-ttu-id="e0912-151">Если обновление не требуется, нажмите кнопку **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="e0912-151">If you do not want to upgrade, click **Cancel**.</span></span>

<span data-ttu-id="e0912-152">**Важно!** Внимательно прочитайте информацию в диалоговом окне перед обновлением, чтобы быть в курсе условий выставления счетов и использования.</span><span class="sxs-lookup"><span data-stu-id="e0912-152">**Important** Carefully read the dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="e0912-153">**Когда закончится срок действия подписки на службу "РЕКОМЕНДАЦИИ"?**</span><span class="sxs-lookup"><span data-stu-id="e0912-153">**When will my subscription to Recommendations end?**</span></span>

<span data-ttu-id="e0912-154">Подписка закончится, когда вы ее отмените.</span><span class="sxs-lookup"><span data-stu-id="e0912-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="e0912-155">Если вы хотите отменить подписку, см. указания ниже.</span><span class="sxs-lookup"><span data-stu-id="e0912-155">If you would like to cancel your subscriptions, see the following instructions.</span></span>

<span data-ttu-id="e0912-156">**Как отменить подписку на службу "РЕКОМЕНДАЦИИ"?**</span><span class="sxs-lookup"><span data-stu-id="e0912-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="e0912-157">Чтобы отменить подписку, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0912-157">To cancel your subscription, use the following steps.</span></span> <span data-ttu-id="e0912-158">Если у вас платная подписка, она будет действовать до конца текущего расчетного периода.</span><span class="sxs-lookup"><span data-stu-id="e0912-158">If your current subscription is a paid subscription, your subscription continues in effect until the end of the current billing period.</span></span> <span data-ttu-id="e0912-159">Если необходимо немедленно отменить подписку, обратитесь в [службу поддержки Майкрософт](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="e0912-159">If you need the cancellation to be effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="e0912-160">**Примечание.** Возмещение в случае отмены подписки до окончания расчетного периода и за транзакции, не использованные во время расчетного периода, не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="e0912-160">**Note** No refund is given if you cancel before the end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="e0912-161">Перейдите на [страницу предложений](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="e0912-161">Navigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="e0912-162">Войдите в Marketplace, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="e0912-162">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="e0912-163">Нажмите кнопку **Отмена** справа от имени набора данных и состояния.</span><span class="sxs-lookup"><span data-stu-id="e0912-163">Click **Cancel** to the right of the dataset name and status.</span></span> <span data-ttu-id="e0912-164">Вы можете использовать эту подписку до окончания текущего расчетного периода или до достижения лимита транзакций (в зависимости от того, что произойдет раньше).</span><span class="sxs-lookup"><span data-stu-id="e0912-164">You can use this subscription until the end of the current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="e0912-165">Если вы хотите немедленно отменить подписку, чтобы приобрести новую, то отправьте запрос в [службу поддержки Майкрософт](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="e0912-165">If you would like to cancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="e0912-166">Приступая к работе со службой «РЕКОМЕНДАЦИИ»</span><span class="sxs-lookup"><span data-stu-id="e0912-166">Getting started with Recommendations</span></span>
<span data-ttu-id="e0912-167">**Могу ли я пользоваться службой «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="e0912-168">Служба машинного обучения «РЕКОМЕНДАЦИИ» предназначена для организаций и компаний, которые полагаются на рекомендации для перекрестных продаж товаров и услуг, а также увеличения их продаж.</span><span class="sxs-lookup"><span data-stu-id="e0912-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations to cross-sell and up-sell products or services to their customers.</span></span> <span data-ttu-id="e0912-169">Если у вас есть веб-сайт для клиентов, команда торговых агентов, команда дистанционных торговых агентов или колл-центр и вы предлагаете каталог, в котором более нескольких десятков товаров или услуг, служба «РЕКОМЕНДАЦИИ» может помочь увеличить вашу прибыль.</span><span class="sxs-lookup"><span data-stu-id="e0912-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="e0912-170">Работать со службой «РЕКОМЕНДАЦИИ» довольно просто.</span><span class="sxs-lookup"><span data-stu-id="e0912-170">Experimenting with Recommendations is designed to be fairly simple.</span></span> <span data-ttu-id="e0912-171">Текущая версия на основе API требует знания основных операций программирования.</span><span class="sxs-lookup"><span data-stu-id="e0912-171">The current API-based version requires basic programming skills.</span></span> <span data-ttu-id="e0912-172">Если вам требуется помощь, обратитесь к разработчику вашего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e0912-172">If you need assistance, contact the vendor who developed your website.</span></span> <span data-ttu-id="e0912-173">Если у вас есть ИТ-отдел или штатный разработчик, они смогут настроить службу «РЕКОМЕНДАЦИИ» для вас.</span><span class="sxs-lookup"><span data-stu-id="e0912-173">If you have an internal IT department or an in-house developer, they should be able to get Recommendations to work for you.</span></span> 

<span data-ttu-id="e0912-174">**Что необходимо для использования службы «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-174">**What are the prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="e0912-175">Для использования службы «РЕКОМЕНДАЦИИ» требуется журнал с информацией о выборе пользователей, связанном с вашим каталогом.</span><span class="sxs-lookup"><span data-stu-id="e0912-175">Recommendations requires that you have a log of user choices as it relates to your catalog.</span></span> <span data-ttu-id="e0912-176">Если у вас нет такого журнала, но есть веб-сайт для клиентов, служба рекомендаций может собирать для вас сведения о действиях пользователей.</span><span class="sxs-lookup"><span data-stu-id="e0912-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="e0912-177">Службе «РЕКОМЕНДАЦИИ» также требуется каталог ваших товаров или услуг.</span><span class="sxs-lookup"><span data-stu-id="e0912-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="e0912-178">Если у вас нет каталога, служба рекомендаций может создать каталог на основе данных об использовании клиентами товаров или услуг.</span><span class="sxs-lookup"><span data-stu-id="e0912-178">If you don't have the catalog, Recommendations can use the actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="e0912-179">Такой каталог не будет содержать элементы, которые не участвовали в пользовательских транзакциях.</span><span class="sxs-lookup"><span data-stu-id="e0912-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="e0912-180">**Как настроить службу «РЕКОМЕНДАЦИИ» при первом использовании?**</span><span class="sxs-lookup"><span data-stu-id="e0912-180">**How do I set up Recommendations for the first time?**</span></span>

<span data-ttu-id="e0912-181">После оформления [подписки](https://datamarket.azure.com/dataset/amla/recommendations) на службу рекомендаций используйте [краткое руководство по API рекомендаций для машинного обучения](machine-learning-recommendation-api-quick-start-guide.md), чтобы настроить ее.</span><span class="sxs-lookup"><span data-stu-id="e0912-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) to Recommendations, you should use the API documentation in the [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) to set up the service.</span></span>

<span data-ttu-id="e0912-182">**Где найти документацию по API?**</span><span class="sxs-lookup"><span data-stu-id="e0912-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="e0912-183">Сведения об API см. в статье [Краткое руководство по API рекомендаций для машинного обучения](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e0912-183">The API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="e0912-184">**Какие есть варианты загрузки данных каталога и данных об использовании в службу «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-184">**What options do I have to upload catalog and usage data to Recommendations?**</span></span>

<span data-ttu-id="e0912-185">Есть два варианта загрузки данных каталога и данных об использовании: экспортировать эти данные из системы CRM или других журналов и загрузить их в службу «РЕКОМЕНДАЦИИ» или добавить на веб-сайт теги, которые будут отслеживать действия пользователей.</span><span class="sxs-lookup"><span data-stu-id="e0912-185">You have two options for uploading your catalog and usage data: You can export the data from your CRM system or other logs and upload it to Recommendations, or you can add tags to your website that will track user activities.</span></span> <span data-ttu-id="e0912-186">В случае выбора второго способа данные будут храниться в Azure.</span><span class="sxs-lookup"><span data-stu-id="e0912-186">If you use the latter method, the data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="e0912-187">Обслуживание и поддержка</span><span class="sxs-lookup"><span data-stu-id="e0912-187">Maintenance and support</span></span>
<span data-ttu-id="e0912-188">**Насколько большим может быть набор данных?**</span><span class="sxs-lookup"><span data-stu-id="e0912-188">**How large can my data set be?**</span></span>

<span data-ttu-id="e0912-189">Каждый набор данных может содержать до 100 000 элементов каталога и до 2048 МБ данных об использовании.</span><span class="sxs-lookup"><span data-stu-id="e0912-189">Each data set can contain up to 100,000 catalog items and up to 2048 MB of usage data.</span></span>
<span data-ttu-id="e0912-190">Кроме того, подписка может содержать до 10 наборов данных (моделей).</span><span class="sxs-lookup"><span data-stu-id="e0912-190">In addition, a subscription can contain up to 10 data sets (models).</span></span>

<span data-ttu-id="e0912-191">**Где можно получить техническую поддержку для службы «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="e0912-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="e0912-192">Техническая поддержка доступна на сайте [поддержки Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) .</span><span class="sxs-lookup"><span data-stu-id="e0912-192">Technical support is available on the [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="e0912-193">**Где можно найти условия использования?**</span><span class="sxs-lookup"><span data-stu-id="e0912-193">**Where can I find the terms of use?**</span></span>

<span data-ttu-id="e0912-194">[Интерфейсы API рекомендаций по Машинному обучению Microsoft Azure. Условия предоставления услуг](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="e0912-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

