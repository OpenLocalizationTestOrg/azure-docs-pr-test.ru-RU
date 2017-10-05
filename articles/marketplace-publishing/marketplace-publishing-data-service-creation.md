---
title: "Руководство по созданию службы данных для Marketplace | Документация Майкрософт"
description: "Подробные инструкции по созданию, сертификации и развертыванию службы данных для продажи в Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="2505a-103">Руководство по публикации службы данных для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2505a-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2505a-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="2505a-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="2505a-105">Дополнительные сведения о публикации бизнес-приложения SaaS на AppSource см. [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="2505a-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="2505a-106">Дополнительные сведения о публикации приложений IaaS или службы разработчика в Azure Marketplace см. [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="2505a-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="2505a-107">После выполнения шага 1 ([создание и регистрация учетной записи](marketplace-publishing-accounts-creation-registration.md)) мы рассказали об [общих нетехнических](marketplace-publishing-pre-requisites.md) и [технических требованиях](marketplace-publishing-data-service-creation-prerequisites.md) для службы данных в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="2505a-108">Рассмотрим процедуру создания предложения службы данных на [портале публикации][link-pubportal] для Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="2505a-109">1.    Войдите на портал публикации.</span><span class="sxs-lookup"><span data-stu-id="2505a-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="2505a-110">Откройте страницу [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="2505a-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="2505a-111">**При первом входе в портал публикации укажите учетную запись, под которой профиль продавца для вашей компании зарегистрирован в центре разработчиков.**</span><span class="sxs-lookup"><span data-stu-id="2505a-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="2505a-112">(Впоследствии вы сможете добавить в качестве соадминистратора на портале публикации любого сотрудника своей компании.)</span><span class="sxs-lookup"><span data-stu-id="2505a-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="2505a-113">Щелкните плитку **Публикация служб данных** , если это первый вход на портал публикации.</span><span class="sxs-lookup"><span data-stu-id="2505a-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="2505a-114">2.    Выберите **Службы данных** в меню навигации с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="2505a-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![рисунок](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="2505a-116">3.    Создание новой службы данных</span><span class="sxs-lookup"><span data-stu-id="2505a-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="2505a-117">Введите название нового предложения службы данных и щелкните на знак плюса ("+") справа.</span><span class="sxs-lookup"><span data-stu-id="2505a-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="2505a-119">4.    Просмотрите подменю только что созданной службы данных в меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2505a-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="2505a-120">Откройте вкладку **Пошаговое руководство** и ознакомьтесь с действиями, необходимыми для правильной публикации службы данных в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="2505a-121">В любое время можно перейти по ссылкам на странице "Пошаговое руководство" или воспользоваться вкладками в подменю предложения службы данных слева.</span><span class="sxs-lookup"><span data-stu-id="2505a-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="2505a-122">5.    Создание нового плана</span><span class="sxs-lookup"><span data-stu-id="2505a-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="2505a-123">Предложения, планы, транзакции.</span><span class="sxs-lookup"><span data-stu-id="2505a-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="2505a-124">Каждое предложение может иметь несколько планов, но не менее одного (1).</span><span class="sxs-lookup"><span data-stu-id="2505a-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="2505a-125">Когда конечные пользователи подписываются на ваше предложение, они подписываются на один из планов предложения.</span><span class="sxs-lookup"><span data-stu-id="2505a-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="2505a-126">Каждый план определяет порядок применения службы конечными пользователями.</span><span class="sxs-lookup"><span data-stu-id="2505a-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="2505a-127">В настоящее время Azure Marketplace поддерживает для служб данных только ежемесячную подписку на основе транзакций, то есть конечные пользователи вносят ежемесячную плату за выбранный план и каждый месяц могут использовать транзакции в количестве, определенном этим планом.</span><span class="sxs-lookup"><span data-stu-id="2505a-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="2505a-128">Транзакция обычно определяется как ряд записей, возвращаемых службой данных по запросу.</span><span class="sxs-lookup"><span data-stu-id="2505a-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="2505a-129">Количество по умолчанию — 100.</span><span class="sxs-lookup"><span data-stu-id="2505a-129">The default is 100.</span></span> <span data-ttu-id="2505a-130">Число транзакций, выполняемых по запросу, равно числу записей, деленному на 100 и округленному до ближайшего целого числа.</span><span class="sxs-lookup"><span data-stu-id="2505a-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="2505a-131">Отслеживанием (измерением) числа транзакций по каждому запросу занимается уровень службы Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2505a-132">Пользователи, которые достигли максимального числа транзакций за месяц, блокируются и не смогут работать со службой до окончания месячного цикла подписки.</span><span class="sxs-lookup"><span data-stu-id="2505a-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="2505a-133">План или один из планов может (но не обязательно) включать неограниченное количество транзакций.</span><span class="sxs-lookup"><span data-stu-id="2505a-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="2505a-134">Создание плана.</span><span class="sxs-lookup"><span data-stu-id="2505a-134">Create a plan.</span></span>
1. <span data-ttu-id="2505a-135">Щелкните **"+"** рядом с командой "Добавить план".</span><span class="sxs-lookup"><span data-stu-id="2505a-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="2505a-136">Выберите один из вариантов использования плана: **Не ограничено** или **Ограничено**.</span><span class="sxs-lookup"><span data-stu-id="2505a-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="2505a-137">Если выбран вариант "Ограниченный", укажите число транзакций, доступных по плану в месяц.</span><span class="sxs-lookup"><span data-stu-id="2505a-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![рисунок](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="2505a-139">Портал публикации также предложит "Идентификатор плана", который будет использоваться в интерфейсе, а также в службе Marketplace для идентификации плана.</span><span class="sxs-lookup"><span data-stu-id="2505a-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="2505a-140">При желании "Идентификатор плана" можно изменить.</span><span class="sxs-lookup"><span data-stu-id="2505a-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2505a-141">"Идентификатор плана" должен быть уникальным в рамках каждого предложения.</span><span class="sxs-lookup"><span data-stu-id="2505a-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="2505a-142">Как и многие другие идентификаторы, используемые на портале публикации, "Идентификатор плана" будет заблокирован после первой публикации в рабочей среде, и вы больше не сможете изменить его.</span><span class="sxs-lookup"><span data-stu-id="2505a-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="2505a-143">Щелкните, чтобы подтвердить выбор.</span><span class="sxs-lookup"><span data-stu-id="2505a-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="2505a-144">Затем вам будет предложено ответить на несколько дополнительных вопросов о новом плане.</span><span class="sxs-lookup"><span data-stu-id="2505a-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![рисунок](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="2505a-146">Вопрос</span><span class="sxs-lookup"><span data-stu-id="2505a-146">Question</span></span> | <span data-ttu-id="2505a-147">Значимость</span><span class="sxs-lookup"><span data-stu-id="2505a-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="2505a-148">**Этот план бесплатный и доступен во всем мире?**</span><span class="sxs-lookup"><span data-stu-id="2505a-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="2505a-149">Можно создать полностью бесплатный план.</span><span class="sxs-lookup"><span data-stu-id="2505a-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="2505a-150">Если это единственный план для данного предложения, значит, вы публикуете в Marketplace "Бесплатное предложение".</span><span class="sxs-lookup"><span data-stu-id="2505a-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="2505a-151">Если плата не взимается только в одном (из нескольких) плане, вы можете дать своим конечным пользователям возможность познакомиться со своей службой, предоставив бесплатно относительно небольшой объем транзакций в месяц.</span><span class="sxs-lookup"><span data-stu-id="2505a-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="2505a-152">Если вы ответите "Да", дополнительных вопросов не будет.</span><span class="sxs-lookup"><span data-stu-id="2505a-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="2505a-153">Конечные пользователи всегда могут перейти на платные планы.</span><span class="sxs-lookup"><span data-stu-id="2505a-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="2505a-154">Вопрос</span><span class="sxs-lookup"><span data-stu-id="2505a-154">Question</span></span> | <span data-ttu-id="2505a-155">Значимость</span><span class="sxs-lookup"><span data-stu-id="2505a-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="2505a-156">**Предусмотрена ли бесплатная пробная версия?**</span><span class="sxs-lookup"><span data-stu-id="2505a-156">**Is free trial available?**</span></span> |<span data-ttu-id="2505a-157">Можно выбрать ответ "Без пробной версии" или указать возможность пробного использования плана в течение "Одного месяца".</span><span class="sxs-lookup"><span data-stu-id="2505a-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="2505a-158">Издатели часто используют этот вариант, чтобы предоставить конечным пользователям возможность узнать о преимуществах их предложений в течение месяца бесплатной подписки.</span><span class="sxs-lookup"><span data-stu-id="2505a-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="2505a-159">Конечные пользователи могут воспользоваться бесплатной пробной версией, только если они задали платежный инструмент, например, кредитную карту, соглашению Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2505a-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="2505a-160">Через месяц пробного использования Azure Marketplace начнет выставлять счета с даты оформления подписки, если только клиент не начал процедуру отмены подписки.</span><span class="sxs-lookup"><span data-stu-id="2505a-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="2505a-161">Никаких специальных уведомлений конечным пользователям не отправляется.</span><span class="sxs-lookup"><span data-stu-id="2505a-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="2505a-162">Вопрос</span><span class="sxs-lookup"><span data-stu-id="2505a-162">Question</span></span> | <span data-ttu-id="2505a-163">Значимость</span><span class="sxs-lookup"><span data-stu-id="2505a-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="2505a-164">**Требуется ли промокод для приобретения этого плана?**</span><span class="sxs-lookup"><span data-stu-id="2505a-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="2505a-165">Издатель может ограничить доступ к своим планам обслуживания, предоставляя специальный код ("промокод") некоторым клиентам.</span><span class="sxs-lookup"><span data-stu-id="2505a-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="2505a-166">В этом случае подписаться на план смогут только пользователи, имеющие этот промокод.</span><span class="sxs-lookup"><span data-stu-id="2505a-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="2505a-167">Если вы выберете "Нет", то вы подтверждаете, что любой человек из региона, где доступно предложение (дополнительные сведения см. в [руководстве по маркетинговому содержимому Marketplace](marketplace-publishing-push-to-staging.md)), сможет подписаться на этот план.</span><span class="sxs-lookup"><span data-stu-id="2505a-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="2505a-168">Дополнительных вопросов больше не будет.</span><span class="sxs-lookup"><span data-stu-id="2505a-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="2505a-169">**Скрыть этот план от всех, у кого нет действующего промокода?**</span><span class="sxs-lookup"><span data-stu-id="2505a-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="2505a-170">Если на предыдущий вопрос был дан ответ "Да", издатель может полностью удалить этот план из интерфейса Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="2505a-171">Это означает, что клиенты не будут видеть этот план на странице сведений о предложении.</span><span class="sxs-lookup"><span data-stu-id="2505a-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="2505a-172">Конечные пользователи, получившие промокод для покупки этого плана, смогут подписаться на него с помощью этого промокода.</span><span class="sxs-lookup"><span data-stu-id="2505a-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="2505a-173">6.    Создание маркетинговых материалов Marketplace</span><span class="sxs-lookup"><span data-stu-id="2505a-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="2505a-174">Сведения об указании данных на вкладках **Маркетинг, Цены, Поддержка и Категории** см. в [руководстве по маркетинговому содержимому Marketplace](marketplace-publishing-push-to-staging.md), которое применяется ко всем артефактам, опубликованным в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="2505a-175">7.    Подключение вашего предложения к службе (на основе SQL Azure или веб-службы)</span><span class="sxs-lookup"><span data-stu-id="2505a-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="2505a-176">Откройте подменю **Службы данных** .</span><span class="sxs-lookup"><span data-stu-id="2505a-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="2505a-177">В верхней половине страницы вам будет предложено указать **Пространство имен**предложения.</span><span class="sxs-lookup"><span data-stu-id="2505a-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="2505a-179">Ответ на вопрос ниже определяет, как издатель будет выставлять новое предложение в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2505a-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="2505a-180">(Дополнительные сведения см. в [руководстве по техническим условиям для служб данных](marketplace-publishing-data-service-creation-prerequisites.md).)</span><span class="sxs-lookup"><span data-stu-id="2505a-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="2505a-182">**Публикация службы на основе базы данных**</span><span class="sxs-lookup"><span data-stu-id="2505a-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="2505a-183">Щелкните **База данных**.</span><span class="sxs-lookup"><span data-stu-id="2505a-183">Click on **Database**.</span></span> <span data-ttu-id="2505a-184">Откроется следующая страница.</span><span class="sxs-lookup"><span data-stu-id="2505a-184">The following page will appear:</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="2505a-186">Чтобы создать сопоставление CSDL для набора данных, основанного на базе данных SQL Azure, укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="2505a-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="2505a-188">А затем для каждой таблицы</span><span class="sxs-lookup"><span data-stu-id="2505a-188">And then for each table</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="2505a-191">Для веб-службы укажите следующее.</span><span class="sxs-lookup"><span data-stu-id="2505a-191">If Web Service</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="2505a-193">Подробные инструкции и примеры для создания веб-службы CSDL см. в статье [Сопоставление существующей веб-службы и OData с помощью CSDL](marketplace-publishing-data-service-creation-odata-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="2505a-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2505a-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2505a-194">Next Steps</span></span>
<span data-ttu-id="2505a-195">После создания предложения службы данных выполните инструкции в [руководстве по маркетинговому содержимому Marketplace](marketplace-publishing-push-to-staging.md) перед тем, как перейти к [тестированию службы данных в промежуточной среде](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="2505a-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2505a-196">См. также</span><span class="sxs-lookup"><span data-stu-id="2505a-196">See Also</span></span>
* [<span data-ttu-id="2505a-197">Приступая к работе: как опубликовать предложение в Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2505a-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="2505a-198">Если вы хотите понять процесс и смысл сопоставления OData, см. статью [Сопоставление существующей веб-службы и OData с помощью CSDL](marketplace-publishing-data-service-creation-odata-mapping.md), где приводятся определения, структуры и инструкции.</span><span class="sxs-lookup"><span data-stu-id="2505a-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="2505a-199">Если вы заинтересованы в изучении и понимании конкретных узлов и их параметров, в статье [Узлы сопоставления службы данных OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) вы найдете определения и объяснения, примеры и контекст вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="2505a-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="2505a-200">Если вы хотите поработать с примерами, см. статью [Примеры сопоставления существующей веб-службы OData через CSDL](marketplace-publishing-data-service-creation-odata-mapping-examples.md), где приводятся примеры кода вместе с объяснением синтаксиса и контекста.</span><span class="sxs-lookup"><span data-stu-id="2505a-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
