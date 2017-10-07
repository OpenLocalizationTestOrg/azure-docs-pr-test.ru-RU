---
title: "aaaGuide toocreating службы данных для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развертывать службу данных для приобретения на hello Azure Marketplace."
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
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="3d545-103">Данные службы руководство по публикации для hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3d545-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3d545-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="3d545-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="3d545-105">Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="3d545-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="3d545-106">Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="3d545-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="3d545-107">После завершения hello шага 1, [создания учетной записи и регистрации](marketplace-publishing-accounts-creation-registration.md), мы предложены вы hello [общие нетехнических](marketplace-publishing-pre-requisites.md) и [технические требования](marketplace-publishing-data-service-creation-prerequisites.md) службы данных предложить в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3d545-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="3d545-108">Теперь мы поможет hello шаги для создания предложения службы данных на hello [портал публикации] [ link-pubportal] для hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3d545-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="3d545-109">1.    Toohello входа портал публикации.</span><span class="sxs-lookup"><span data-stu-id="3d545-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="3d545-110">Go слишком[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="3d545-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="3d545-111">**Для первого tooPublishing входа время портала используйте hello же учетную запись, с которым профиль компании продавца, зарегистрированные в центре разработчиков.**</span><span class="sxs-lookup"><span data-stu-id="3d545-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="3d545-112">(Позднее можно добавить любой сотрудник компании как соадминистратора в hello портал публикации).</span><span class="sxs-lookup"><span data-stu-id="3d545-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="3d545-113">Щелкните hello **публикации служб данных** плитке, если это hello при первом входе в портал публикации hello.</span><span class="sxs-lookup"><span data-stu-id="3d545-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="3d545-114">2.    Выберите **Data Services** выберите в меню навигации hello hello слева.</span><span class="sxs-lookup"><span data-stu-id="3d545-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![рисунок](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="3d545-116">3.    Создание новой службы данных</span><span class="sxs-lookup"><span data-stu-id="3d545-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="3d545-117">Введите название hello вашей новой службы данных, предложения и нажмите на «+» в правом hello.</span><span class="sxs-lookup"><span data-stu-id="3d545-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="3d545-119">4.    Службы данных новые hello подменю проверку под hello в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="3d545-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="3d545-120">Щелкните hello **Пошаговое руководство** и проверьте все необходимые действия, необходимые toopublish hello правильно службы данных на hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3d545-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="3d545-121">Всегда можно щелкнуть hello ссылки на странице «Пошаговое руководство» hello или используйте вкладки на предложение службы данных hello подменю в левой части hello.</span><span class="sxs-lookup"><span data-stu-id="3d545-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="3d545-122">5.    Создание нового плана</span><span class="sxs-lookup"><span data-stu-id="3d545-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="3d545-123">Предложения, планы, транзакции.</span><span class="sxs-lookup"><span data-stu-id="3d545-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="3d545-124">Каждое предложение может иметь несколько планов, но не менее одного (1).</span><span class="sxs-lookup"><span data-stu-id="3d545-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="3d545-125">Когда конечные пользователи подписка предложение tooyour они подписаны для одного плана hello предложения.</span><span class="sxs-lookup"><span data-stu-id="3d545-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="3d545-126">Каждый план определяет, как будет конечным пользователям быть toouse доступ к службе.</span><span class="sxs-lookup"><span data-stu-id="3d545-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="3d545-127">В настоящее время Azure Marketplace поддержка только ежемесячные подписки транзакции в соответствии с модели для служб данных, т. е. конечные пользователи будут уделять toohello цены hello конкретный план, они подписались tooand в соответствии с ежемесячная плата будет может tooconsume числом каждого месяца транзакции, определенной hello плана.</span><span class="sxs-lookup"><span data-stu-id="3d545-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="3d545-128">Каждая транзакция, обычно определяется как число записей, возвращаемых службы данных на основании hello запроса, отправленного toohello службы.</span><span class="sxs-lookup"><span data-stu-id="3d545-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="3d545-129">по умолчанию Hello равно 100.</span><span class="sxs-lookup"><span data-stu-id="3d545-129">hello default is 100.</span></span> <span data-ttu-id="3d545-130">Число транзакций, возвращаемых tooeach запрос будет число записей делится на 100 и округленное до ближайшего целого в toohello.</span><span class="sxs-lookup"><span data-stu-id="3d545-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="3d545-131">Это служба Azure Marketplace слоя ответственности toomonitor (метр) количество транзакций, потребляемых каждым запросом.</span><span class="sxs-lookup"><span data-stu-id="3d545-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d545-132">Конечные пользователи, которых достиг ограничения на операции hello hello месяц будет блокирована toouse hello службы до завершения их ежемесячного цикла подписки.</span><span class="sxs-lookup"><span data-stu-id="3d545-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="3d545-133">Hello плана или одной из схем hello можно (но не должен) содержать неограниченное количество транзакций.</span><span class="sxs-lookup"><span data-stu-id="3d545-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="3d545-134">Создание плана.</span><span class="sxs-lookup"><span data-stu-id="3d545-134">Create a plan.</span></span>
1. <span data-ttu-id="3d545-135">Щелкните **«+»** Далее toohello «добавить новый план».</span><span class="sxs-lookup"><span data-stu-id="3d545-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="3d545-136">Выберите один из вариантов hello: **неограниченное количество** или **ограниченный** использования для этого плана.</span><span class="sxs-lookup"><span data-stu-id="3d545-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="3d545-137">Если Limited, затем укажите номер hello транзакции hello плана позволит tooconsume в месяц.</span><span class="sxs-lookup"><span data-stu-id="3d545-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![рисунок](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="3d545-139">Публикацию портала также предложит «Идентификатор плана», которое будет toohello используется toocommunicate конечных пользователей hello имя плана hello в hello пользовательского интерфейса и также используются программой hello tooidentify hello рынок службы плана.</span><span class="sxs-lookup"><span data-stu-id="3d545-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="3d545-140">При желании можно изменить hello «Планирование идентификатор».</span><span class="sxs-lookup"><span data-stu-id="3d545-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3d545-141">Hello «Идентификатор плана» должно быть уникальным в пределах области hello каждого предложения.</span><span class="sxs-lookup"><span data-stu-id="3d545-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="3d545-142">При использовании других идентификаторов в hello публикации портала планирование идентификатор будет заблокирована после hello первой публикации tooproduction и вы не будет возможности toochange этот идентификатор.</span><span class="sxs-lookup"><span data-stu-id="3d545-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="3d545-143">Щелкните tooaccept вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="3d545-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="3d545-144">Затем вам будет предложено ответить на несколько дополнительных вопросов о новом плане.</span><span class="sxs-lookup"><span data-stu-id="3d545-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![рисунок](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="3d545-146">Вопрос</span><span class="sxs-lookup"><span data-stu-id="3d545-146">Question</span></span> | <span data-ttu-id="3d545-147">Значимость</span><span class="sxs-lookup"><span data-stu-id="3d545-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="3d545-148">**Этот план бесплатный и доступен во всем мире?**</span><span class="sxs-lookup"><span data-stu-id="3d545-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="3d545-149">Можно создать полностью бесплатный план.</span><span class="sxs-lookup"><span data-stu-id="3d545-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="3d545-150">Его hello только план на это предложение — означает, что вы публикуете «Свободного предлагаются» в hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3d545-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="3d545-151">Если это только для одного (из лишь немногие) плана hello позволяет конечным пользователям параметр toooffer, toolearn Дополнительные сведения о службе с помощью относительно небольшого числа транзакций в месяц.</span><span class="sxs-lookup"><span data-stu-id="3d545-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="3d545-152">Если hello ответ «Да», затем будет предложено без дополнительных вопросов.</span><span class="sxs-lookup"><span data-stu-id="3d545-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="3d545-153">Конечным пользователям всегда можно обновить toohello платная планов.</span><span class="sxs-lookup"><span data-stu-id="3d545-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="3d545-154">Вопрос</span><span class="sxs-lookup"><span data-stu-id="3d545-154">Question</span></span> | <span data-ttu-id="3d545-155">Значимость</span><span class="sxs-lookup"><span data-stu-id="3d545-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="3d545-156">**Предусмотрена ли бесплатная пробная версия?**</span><span class="sxs-lookup"><span data-stu-id="3d545-156">**Is free trial available?**</span></span> |<span data-ttu-id="3d545-157">Можно выбрать «Нет пробная версия» вообще или предоставить параметр toouse план «Месяц».</span><span class="sxs-lookup"><span data-stu-id="3d545-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="3d545-158">Издатели, например toouse, этот параметр tooprovide конечным пользователям hello вероятность toounderstand hello преимущества hello предлагают бесплатно в течение месяца.</span><span class="sxs-lookup"><span data-stu-id="3d545-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3d545-159">Конечным пользователям будет в toopurchase возможности использования бесплатной пробной версии, только если у них установлены платежного средства например кредитной карты, соглашение enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="3d545-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="3d545-160">Через месяц hello бесплатной пробной версии Azure Marketplace начнется заряжается клиентов hello цены на момент выхода hello hello подписки, если клиента hello инициировал hello отмены подписки.</span><span class="sxs-lookup"><span data-stu-id="3d545-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="3d545-161">Специальные уведомление не будет предоставляться toohello конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="3d545-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="3d545-162">Вопрос</span><span class="sxs-lookup"><span data-stu-id="3d545-162">Question</span></span> | <span data-ttu-id="3d545-163">Значимость</span><span class="sxs-lookup"><span data-stu-id="3d545-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="3d545-164">**Для этого тарифа необходим toopurchase код рекламной акции?**</span><span class="sxs-lookup"><span data-stu-id="3d545-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="3d545-165">Издатели имеют параметр toolimit доступа tootheir планы обслуживания, предоставляя специального кода, называется «Promocode» toospecific клиентов.</span><span class="sxs-lookup"><span data-stu-id="3d545-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="3d545-166">Только конечные пользователи, имеющие это Promocode будет может toosubscribe toohello плана.</span><span class="sxs-lookup"><span data-stu-id="3d545-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="3d545-167">Если выбрать «Нет», то вы согласны, каждый из которых приобрести hello региона hello доступен (см. [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) подробнее) будет может toosubscribe toothis плана.</span><span class="sxs-lookup"><span data-stu-id="3d545-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="3d545-168">Дополнительных вопросов больше не будет.</span><span class="sxs-lookup"><span data-stu-id="3d545-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="3d545-169">**Скрыть этот план от всех, у кого нет действующего промокода?**</span><span class="sxs-lookup"><span data-stu-id="3d545-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="3d545-170">Если hello ответов toohello предыдущий вопрос — «Yes» hello издатель имеет параметр toocompletely этот план удаляется из отображаются в Интерфейсе hello Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="3d545-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="3d545-171">Это означает, клиенты не будут видеть этот план на hello предложение «подробности».</span><span class="sxs-lookup"><span data-stu-id="3d545-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="3d545-172">Конечные пользователи, которые будут получать promocode toopurchase, будут tooit toosubscribe может с помощью этого promocode.</span><span class="sxs-lookup"><span data-stu-id="3d545-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="3d545-173">6.    Создание маркетинговых материалов Marketplace</span><span class="sxs-lookup"><span data-stu-id="3d545-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="3d545-174">Для как tooprovide сведения, необходимые в **отдела маркетинга, цены, поддержки и категории** вкладок перейдите на страницу [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) это общие tooall артефакты, публикуемые в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3d545-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="3d545-175">7.    Подключитесь к tooyour предложение службы (на основе SQL Azure или веб-службы).</span><span class="sxs-lookup"><span data-stu-id="3d545-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="3d545-176">Щелкните hello **Data Services** подменю.</span><span class="sxs-lookup"><span data-stu-id="3d545-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="3d545-177">В верхней части страницы приветствия hello запрашивается предложение hello tooprovide **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="3d545-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="3d545-179">Hello ниже вопрос будет определена как hello издатель будет вновь созданные tooexpose предложение tooAzure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3d545-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="3d545-180">(Дополнительные сведения см. в разделе hello [руководство технической готовности к установке служб данных](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="3d545-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="3d545-182">**Публикация hello служба на основе базы данных**</span><span class="sxs-lookup"><span data-stu-id="3d545-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="3d545-183">Щелкните **База данных**.</span><span class="sxs-lookup"><span data-stu-id="3d545-183">Click on **Database**.</span></span> <span data-ttu-id="3d545-184">Появится следующая страница приветствия.</span><span class="sxs-lookup"><span data-stu-id="3d545-184">hello following page will appear:</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="3d545-186">toocreate сопоставление языка CSDL для hello набора данных, основанный на hello базу данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="3d545-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="3d545-188">А затем для каждой таблицы</span><span class="sxs-lookup"><span data-stu-id="3d545-188">And then for each table</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="3d545-191">Для веб-службы укажите следующее.</span><span class="sxs-lookup"><span data-stu-id="3d545-191">If Web Service</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="3d545-193">Чтение [сопоставление существующего веб-службы tooOData через CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) подробные инструкции и примеры для создания веб-службе языка CSDL.</span><span class="sxs-lookup"><span data-stu-id="3d545-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3d545-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d545-194">Next Steps</span></span>
<span data-ttu-id="3d545-195">После создания службы данных предложение убедитесь, необходимо выполнить инструкции hello в hello [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) перед перемещением вперед слишком[тестирование службы данных в промежуточной](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="3d545-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3d545-196">См. также</span><span class="sxs-lookup"><span data-stu-id="3d545-196">See Also</span></span>
* [<span data-ttu-id="3d545-197">Приступая к работе: Как toopublish toohello предложение Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3d545-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="3d545-198">Если вы заинтересованы в общее представление о hello общий процесс сопоставления OData и цели, эта статья [данных службы OData сопоставления](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview определений, структуры и инструкции.</span><span class="sxs-lookup"><span data-stu-id="3d545-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="3d545-199">Если вы заинтересованы в обучении и основные сведения о hello конкретных узлов и их параметров, эта статья [узлы сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) для определения и объяснения, примеры и контекст вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="3d545-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="3d545-200">Если вы заинтересованы в просмотре примеров, эта статья [примеры сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee образцы кода и понимания синтаксиса кода и контекста.</span><span class="sxs-lookup"><span data-stu-id="3d545-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
