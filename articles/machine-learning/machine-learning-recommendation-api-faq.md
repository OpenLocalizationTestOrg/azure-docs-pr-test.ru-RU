---
title: "aaaSet копирование и использование hello машины обучения рекомендации API | Документы Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="d7422-103">Часто задаваемые вопросы о настройке и использовании API рекомендаций для машинного обучения</span><span class="sxs-lookup"><span data-stu-id="d7422-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="d7422-104">**Что представляет собой служба «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="d7422-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="d7422-105">Необходимо запустить с помощью службы Когнитивных рекомендации API hello вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="d7422-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="d7422-106">Эта служба будет заменена Hello службы Когнитивных рекомендации и всех hello новых функций, которые будут реализованы существует.</span><span class="sxs-lookup"><span data-stu-id="d7422-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="d7422-107">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="d7422-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="d7422-108">Дополнительные сведения о [toohello перенос новой Когнитивных службы](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="d7422-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="d7422-109">Для компании и организации, которые зависят от продаж toocross рекомендации и увеличения продаж продуктов и служб tootheir клиентов рекомендации, ПРИВЕДЕННЫЕ в машинного обучения Azure предоставляет механизм самообслуживания рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d7422-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="d7422-110">Это реализация функции совместной фильтрации, использующей факторизацию матрицы в качестве основного алгоритма.</span><span class="sxs-lookup"><span data-stu-id="d7422-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="d7422-111">Разработчики приложений могут получать доступ к службе «РЕКОМЕНДАЦИИ» с помощью интерфейсов REST API.</span><span class="sxs-lookup"><span data-stu-id="d7422-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d7422-112">**Для чего можно использовать службу «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="d7422-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="d7422-113">Служба "РЕКОМЕНДАЦИИ" принимает в качестве входных данных элемент или набор элементов и возвращает список соответствующих рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d7422-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="d7422-114">Пример — клиент интернет-магазина выбирает продукт.</span><span class="sxs-lookup"><span data-stu-id="d7422-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="d7422-115">Интернет-магазине Hello отправляет этого продукта в качестве входного tooRECOMMENDATIONS, взамен возвращает список продуктов и решает, какие из них будет отображаться toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="d7422-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="d7422-116">Возможно требуется toooptimize РЕКОМЕНДАЦИИ toouse Интернет-магазина или даже tooinform внутренних продаж отдела или вызов центра.</span><span class="sxs-lookup"><span data-stu-id="d7422-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="d7422-117">**Существуют ли какие-либо ограничения использования?**</span><span class="sxs-lookup"><span data-stu-id="d7422-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="d7422-118">Рекомендации имеет следующие ограничения использования hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="d7422-119">Максимальное число моделей на одну подписку — 10.</span><span class="sxs-lookup"><span data-stu-id="d7422-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="d7422-120">Максимальное количество элементов в каталоге: 100 000</span><span class="sxs-lookup"><span data-stu-id="d7422-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="d7422-121">Hello использования точек, которые хранятся не более 5 000 000 ~.</span><span class="sxs-lookup"><span data-stu-id="d7422-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="d7422-122">Если новые будут отправлены или отмечены Hello старые будут удалены.</span><span class="sxs-lookup"><span data-stu-id="d7422-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="d7422-123">Максимальный размер данных, которые можно отправить по электронной почте (например, при импорте данных каталога, импорте данных по использованию), составляет 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="d7422-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="d7422-124">Число транзакций в секунду (TPS) для неактивной сборки модели рекомендаций — около 2.</span><span class="sxs-lookup"><span data-stu-id="d7422-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="d7422-125">Построение модели рекомендации активным может быть установлено too20 транзакций в Секунду.</span><span class="sxs-lookup"><span data-stu-id="d7422-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="d7422-126">Покупка и выставление счетов</span><span class="sxs-lookup"><span data-stu-id="d7422-126">Purchase and Billing</span></span>
<span data-ttu-id="d7422-127">**Сколько стоит рекомендации период запуска hello**</span><span class="sxs-lookup"><span data-stu-id="d7422-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="d7422-128">"РЕКОМЕНДАЦИИ" — это служба на основе подписки.</span><span class="sxs-lookup"><span data-stu-id="d7422-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="d7422-129">Оплата осуществляется на основе количества транзакций в месяц.</span><span class="sxs-lookup"><span data-stu-id="d7422-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="d7422-130">Вы можете проверить hello [предлагают страницы](https://datamarket.azure.com/dataset/amla/recommendations) в Microsoft Azure Marketplace для получения сведений о ценах.</span><span class="sxs-lookup"><span data-stu-id="d7422-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="d7422-131">**Взимается ли какая-либо плата за отслеживание и/или сохранение информации о действиях пользователей службой «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="d7422-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="d7422-132">Не в момент hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-132">Not at hello moment.</span></span>

<span data-ttu-id="d7422-133">**Есть ли у службы «РЕКОМЕНДАЦИИ» бесплатная пробная версия?**</span><span class="sxs-lookup"><span data-stu-id="d7422-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="d7422-134">Нет бесплатную ознакомительную, который является ограниченным too10, 000 транзакций в месяц.</span><span class="sxs-lookup"><span data-stu-id="d7422-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="d7422-135">**Когда мне будет выставлен счет за использование службы «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="d7422-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="d7422-136">Платная подписка — это подписка, за которую взимается ежемесячная плата.</span><span class="sxs-lookup"><span data-stu-id="d7422-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="d7422-137">При приобретении платной подписки вы немедленно взимается плата для hello сначала месяц использования.</span><span class="sxs-lookup"><span data-stu-id="d7422-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="d7422-138">Взимается сумма hello, связанный с предложением hello на странице приветствия подписки (плюс применимые налоги).</span><span class="sxs-lookup"><span data-stu-id="d7422-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="d7422-139">Ежемесячная плата взимается ежемесячно на hello же календарь даты приобретения до отмены подписки hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="d7422-140">**Как обновить tooa выше уровня службы?**</span><span class="sxs-lookup"><span data-stu-id="d7422-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="d7422-141">Можно приобрести или обновить подписки hello [предлагают страницы](https://datamarket.azure.com/dataset/amla/recommendations) страницы в Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d7422-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="d7422-142">При обновлении подписки:</span><span class="sxs-lookup"><span data-stu-id="d7422-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="d7422-143">Транзакции, которые остаются в вашей старой подписки не добавляются tooyour новую подписку.</span><span class="sxs-lookup"><span data-stu-id="d7422-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="d7422-144">Вы оплачиваете полную стоимость новой подписки hello, несмотря на то, что у вас есть неиспользуемые транзакции на вашей старой подписки.</span><span class="sxs-lookup"><span data-stu-id="d7422-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="d7422-145">Процесс tooupgrade подписки:</span><span class="sxs-lookup"><span data-stu-id="d7422-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="d7422-146">Nevigate toohello [предлагают страницы](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="d7422-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="d7422-147">Если вы еще не выполнили вход toohello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d7422-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="d7422-148">Hello правой панели перечислены все доступные планы hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="d7422-149">Установите переключатель hello плана hello нужные tooupgrade для.</span><span class="sxs-lookup"><span data-stu-id="d7422-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="d7422-150">Если вы хотите tooupgrade, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d7422-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="d7422-151">Если вы не хотите tooupgrade, нажмите кнопку **отменить**.</span><span class="sxs-lookup"><span data-stu-id="d7422-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="d7422-152">**Важные** диалоговое окно hello тщательно чтения перед началом обновления, так как существуют последствия для выставления счетов и использования.</span><span class="sxs-lookup"><span data-stu-id="d7422-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="d7422-153">**Когда завершается tooRecommendations Мои подписки**</span><span class="sxs-lookup"><span data-stu-id="d7422-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="d7422-154">Подписка закончится, когда вы ее отмените.</span><span class="sxs-lookup"><span data-stu-id="d7422-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="d7422-155">Если вы хотите toocancel hello, следуя инструкциям в разделе ваших подписок.</span><span class="sxs-lookup"><span data-stu-id="d7422-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="d7422-156">**Как отменить подписку на службу "РЕКОМЕНДАЦИИ"?**</span><span class="sxs-lookup"><span data-stu-id="d7422-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="d7422-157">toocancel, подписки, hello используйте следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="d7422-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="d7422-158">Если текущая подписка является платной подписки, подписки продолжает действовать до конца hello hello текущего расчетный период.</span><span class="sxs-lookup"><span data-stu-id="d7422-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="d7422-159">Если требуется hello отмены toobe силу немедленно, свяжитесь с нами по [поддержки Майкрософт](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="d7422-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="d7422-160">**Примечание** не возмещение не предоставляется, если отменить до hello конце периода выставления счетов или неиспользуемые транзакций в расчетном периоде.</span><span class="sxs-lookup"><span data-stu-id="d7422-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="d7422-161">Перейдите toohello [предлагают страницы](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="d7422-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="d7422-162">Если вы еще не выполнили вход toohello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d7422-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="d7422-163">Нажмите кнопку **отменить** toohello справа от имени набора данных hello и состояние.</span><span class="sxs-lookup"><span data-stu-id="d7422-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="d7422-164">Можно использовать эту подписку до достижения конца hello hello текущего расчетный период или лимита транзакций (произойдет раньше).</span><span class="sxs-lookup"><span data-stu-id="d7422-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="d7422-165">Если вы хотите toocancel подписку немедленно, поэтому можно приобрести новую подписку, заполняют заявку на [поддержки Майкрософт](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="d7422-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="d7422-166">Приступая к работе со службой «РЕКОМЕНДАЦИИ»</span><span class="sxs-lookup"><span data-stu-id="d7422-166">Getting started with Recommendations</span></span>
<span data-ttu-id="d7422-167">**Могу ли я пользоваться службой «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="d7422-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="d7422-168">Рекомендации, приведенные в машинное обучение — для компании и организации, зависящие от рекомендаций toocross продаж и увеличения продаж продуктов или услуг tootheir клиентов.</span><span class="sxs-lookup"><span data-stu-id="d7422-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="d7422-169">Если у вас есть веб-сайт для клиентов, команда торговых агентов, команда дистанционных торговых агентов или колл-центр и вы предлагаете каталог, в котором более нескольких десятков товаров или услуг, служба «РЕКОМЕНДАЦИИ» может помочь увеличить вашу прибыль.</span><span class="sxs-lookup"><span data-stu-id="d7422-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="d7422-170">Эксперименты с рекомендации — спроектированный toobe довольно проста.</span><span class="sxs-lookup"><span data-stu-id="d7422-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="d7422-171">Hello текущей версии на основе API требует основные навыки программирования.</span><span class="sxs-lookup"><span data-stu-id="d7422-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="d7422-172">Если вам нужна помощь, обратитесь к поставщику hello, разработанных веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="d7422-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="d7422-173">Если у вас есть внутренний ИТ-отдела или внутренним разработчиком, они должны быть toowork может tooget рекомендации для вас.</span><span class="sxs-lookup"><span data-stu-id="d7422-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="d7422-174">**Что такое hello предварительных требований для настройки рекомендации**</span><span class="sxs-lookup"><span data-stu-id="d7422-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="d7422-175">Рекомендации по требует наличия журналов выбора пользователя относительно каталога tooyour.</span><span class="sxs-lookup"><span data-stu-id="d7422-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="d7422-176">Если у вас нет такого журнала, но есть веб-сайт для клиентов, служба рекомендаций может собирать для вас сведения о действиях пользователей.</span><span class="sxs-lookup"><span data-stu-id="d7422-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="d7422-177">Службе «РЕКОМЕНДАЦИИ» также требуется каталог ваших товаров или услуг.</span><span class="sxs-lookup"><span data-stu-id="d7422-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="d7422-178">Если у вас нет каталога hello, рекомендаций можно использовать данные об использовании клиента hello и уточнить каталога.</span><span class="sxs-lookup"><span data-stu-id="d7422-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="d7422-179">Такой каталог не будет содержать элементы, которые не участвовали в пользовательских транзакциях.</span><span class="sxs-lookup"><span data-stu-id="d7422-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="d7422-180">**Как установить рекомендуемые действия для hello первый раз?**</span><span class="sxs-lookup"><span data-stu-id="d7422-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="d7422-181">После [подписки](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, следует использовать hello API документации в hello [машины обучения Azure рекомендации — краткое руководство по](machine-learning-recommendation-api-quick-start-guide.md) tooset hello службы.</span><span class="sxs-lookup"><span data-stu-id="d7422-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="d7422-182">**Где найти документацию по API?**</span><span class="sxs-lookup"><span data-stu-id="d7422-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="d7422-183">Hello документации по API — [Azure Machine Learning рекомендации — краткое руководство по](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d7422-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="d7422-184">**Выполните параметров у меня tooRecommendations tooupload каталога и использования данных?**</span><span class="sxs-lookup"><span data-stu-id="d7422-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="d7422-185">Есть два способа для загрузки данных каталога и использование: можно экспортировать данные hello из системы CRM или другие журналы и отправьте его tooRecommendations или можно добавить теги tooyour веб-сайт, отслеживает действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="d7422-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="d7422-186">Если используется последний метод hello, hello данных будут храниться в Azure.</span><span class="sxs-lookup"><span data-stu-id="d7422-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="d7422-187">Обслуживание и поддержка</span><span class="sxs-lookup"><span data-stu-id="d7422-187">Maintenance and support</span></span>
<span data-ttu-id="d7422-188">**Насколько большим может быть набор данных?**</span><span class="sxs-lookup"><span data-stu-id="d7422-188">**How large can my data set be?**</span></span>

<span data-ttu-id="d7422-189">Каждый набор данных может содержать too100 000 элементов каталога и копирование too2048 МБ данных об использовании.</span><span class="sxs-lookup"><span data-stu-id="d7422-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="d7422-190">Кроме того подписки может содержать копию too10 наборов данных (модели).</span><span class="sxs-lookup"><span data-stu-id="d7422-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="d7422-191">**Где можно получить техническую поддержку для службы «РЕКОМЕНДАЦИИ»?**</span><span class="sxs-lookup"><span data-stu-id="d7422-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="d7422-192">Техническая поддержка доступна на hello [Microsoft Azure поддерживает](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) сайта.</span><span class="sxs-lookup"><span data-stu-id="d7422-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="d7422-193">**Где найти hello условия использования**</span><span class="sxs-lookup"><span data-stu-id="d7422-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="d7422-194">[Интерфейсы API рекомендаций по Машинному обучению Microsoft Azure. Условия предоставления услуг](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="d7422-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

