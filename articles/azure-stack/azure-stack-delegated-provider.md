---
title: "Стек Azure предлагает aaaDelegating | Документы Microsoft"
description: "Узнайте, как tooput другим пользователям, ответственный за создание предложений и регистрация пользователей."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: d539cac3ed56f342338c830d95fbec7e93175929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="1aa11-103">Делегирование предложения в стек Azure</span><span class="sxs-lookup"><span data-stu-id="1aa11-103">Delegating offers in Azure Stack</span></span>

<span data-ttu-id="1aa11-104">Как оператор облака Azure стека hello часто требуется tooput другим пользователям, ответственный за создание предложений и регистрация пользователей.</span><span class="sxs-lookup"><span data-stu-id="1aa11-104">As hello Azure Stack cloud operator, you often want tooput other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="1aa11-105">Например при наличии поставщиком услуг и вы хотите toosign торговые посредники клиентов и управлять ими от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="1aa11-105">For example, if you are a service provider and you want resellers toosign up customers and manage them on your behalf.</span></span> <span data-ttu-id="1aa11-106">Он может произойти на предприятии, если являются частью центральная ИТ-группа и подразделений или дочерних компаниях toosign пользователей без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="1aa11-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries toosign up users without your intervention.</span></span>

<span data-ttu-id="1aa11-107">Делегирование поможет вам с этими задачами, помогая tooreach пользователей и управление ими более чем toodo могли бы непосредственно.</span><span class="sxs-lookup"><span data-stu-id="1aa11-107">Delegation helps you with these tasks, helping you tooreach and manage more users than you would be able toodo directly.</span></span> <span data-ttu-id="1aa11-108">Hello ниже показан один уровень делегирования, но стек Azure поддерживает несколько уровней.</span><span class="sxs-lookup"><span data-stu-id="1aa11-108">hello following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="1aa11-109">Делегированные поставщиков в свою очередь может делегировать tooother поставщиков, toofive уровни.</span><span class="sxs-lookup"><span data-stu-id="1aa11-109">Delegated providers can in turn delegate tooother providers, up toofive levels.</span></span>

![](media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="1aa11-110">Операторы облака Azure стека можно делегировать создание hello tooother пользователей, предложений и клиентов с помощью функции делегирования hello.</span><span class="sxs-lookup"><span data-stu-id="1aa11-110">Azure Stack cloud operators can delegate hello creation of offers and tenants tooother users by using hello delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="1aa11-111">Роли и действия, описанные в делегирования</span><span class="sxs-lookup"><span data-stu-id="1aa11-111">Roles and steps in delegation</span></span>
<span data-ttu-id="1aa11-112">Делегирование toounderstand, имейте в виду, что существуют три роли участвующих:</span><span class="sxs-lookup"><span data-stu-id="1aa11-112">toounderstand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="1aa11-113">Hello **оператор облака** управляет инфраструктуры Azure стека hello, создает шаблон предложения и делегирует другим пользователям tootheir предоставлена.</span><span class="sxs-lookup"><span data-stu-id="1aa11-113">hello **cloud operator** manages hello Azure Stack infrastructure, creates an offer template, and delegates others to offer it tootheir users.</span></span>
* <span data-ttu-id="1aa11-114">Hello делегированного облака Администраторы называются **делегированы поставщики**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-114">hello delegated cloud administrators are called **delegated providers**.</span></span> <span data-ttu-id="1aa11-115">Они могут принадлежать tooother организации (например, других клиентов Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1aa11-115">They can belong tooother organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="1aa11-116">**Пользователи** подписываться на предложения hello и использовать их для управления их рабочих нагрузок, создании виртуальных машин, хранение данных и т. д.</span><span class="sxs-lookup"><span data-stu-id="1aa11-116">**Users** sign up for hello offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="1aa11-117">Как показано в следующих график hello, существует два действия по настройке делегирования.</span><span class="sxs-lookup"><span data-stu-id="1aa11-117">As shown in hello following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="1aa11-118">**Определить hello делегированы поставщиков** подписавшись их tooan предложения на основе план, который содержит только службу hello подписок.</span><span class="sxs-lookup"><span data-stu-id="1aa11-118">**Identify hello delegated providers** by subscribing them tooan offer based on a plan that contains only hello subscriptions service.</span></span>
   <span data-ttu-id="1aa11-119">Пользователи подписаться предложение toothis получить некоторые возможности администратора облака hello, включая предложения tooextend возможность hello и вход пользователей, для их использования.</span><span class="sxs-lookup"><span data-stu-id="1aa11-119">Users who subscribe toothis offer acquire some of hello cloud administrator’s capabilities, including hello ability tooextend offers and sign users up for them.</span></span>
2. <span data-ttu-id="1aa11-120">**Делегат toohello предложение делегировать поставщику**, это предложение работает в качестве шаблона для что hello делегированного поставщик может предложить.</span><span class="sxs-lookup"><span data-stu-id="1aa11-120">**Delegate an offer toohello delegated provider**, this offer functions as a template for what hello delegated provider can offer.</span></span> <span data-ttu-id="1aa11-121">Hello делегированного поставщика — теперь может tootake hello предложение, выберите ее имя (но не изменения ее служб и квоты) и предложить его toocustomers.</span><span class="sxs-lookup"><span data-stu-id="1aa11-121">hello delegated provider is now able tootake hello offer, choose a name for it (but not change its services and quotas), and offer it toocustomers.</span></span>

![](media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="1aa11-122">tooact как поставщики делегированные пользователи должны tooestablish связь с главной поставщика hello. Другими словами они должны toocreate подписки.</span><span class="sxs-lookup"><span data-stu-id="1aa11-122">tooact as delegated providers, users need tooestablish a relationship with hello main provider; in other words, they need toocreate a subscription.</span></span> <span data-ttu-id="1aa11-123">В этом сценарии эта подписка определяет делегированного поставщиков как имеющий hello правой toopresent предложений от имени основного поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="1aa11-123">In this scenario, this subscription identifies the delegated providers as having hello right toopresent offers on behalf of hello main provider.</span></span>

<span data-ttu-id="1aa11-124">После установления этой связи оператор hello облака можно делегировать делегированного поставщик toohello предложения.</span><span class="sxs-lookup"><span data-stu-id="1aa11-124">Once this relationship is established, hello cloud operator can delegate an offer toohello delegated provider.</span></span> <span data-ttu-id="1aa11-125">Hello делегированного поставщика — теперь может tootake hello предложение, переименуйте его (но не изменять их содержимое) и предоставлять его tooits.</span><span class="sxs-lookup"><span data-stu-id="1aa11-125">hello delegated provider is now able tootake hello offer, rename it (but not change its substance), and offer it tooits customers.</span></span>

<span data-ttu-id="1aa11-126">Hello в следующих разделах описано, как tooestablish поставщик делегированного делегировать предложение и убедитесь, что пользователи могут зарегистрироваться для него.</span><span class="sxs-lookup"><span data-stu-id="1aa11-126">hello following sections describe how tooestablish a delegated provider, delegate an offer, and verify that users can sign up for it.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="1aa11-127">Настройка ролей</span><span class="sxs-lookup"><span data-stu-id="1aa11-127">Set up roles</span></span>

<span data-ttu-id="1aa11-128">toosee делегированные поставщика на работе, вы должны дополнительные учетные записи Azure Active Directory в облако оператор сложения tooyour счета.</span><span class="sxs-lookup"><span data-stu-id="1aa11-128">toosee a delegated provider at work, you need additional Azure Active Directory accounts in addition tooyour cloud operator account.</span></span> <span data-ttu-id="1aa11-129">Если их нет, создайте две учетные записи hello.</span><span class="sxs-lookup"><span data-stu-id="1aa11-129">If you do not have them, create hello two accounts.</span></span> <span data-ttu-id="1aa11-130">Hello учетные записи могут принадлежать tooany клиента AAD.</span><span class="sxs-lookup"><span data-stu-id="1aa11-130">hello accounts can belong tooany AAD tenant.</span></span> <span data-ttu-id="1aa11-131">Мы называем toothem как hello делегированы поставщика (DP) и hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="1aa11-131">We refer toothem as hello delegated provider (DP) and hello user.</span></span>

| <span data-ttu-id="1aa11-132">**Роль**</span><span class="sxs-lookup"><span data-stu-id="1aa11-132">**Role**</span></span> | <span data-ttu-id="1aa11-133">**Прав в организации**</span><span class="sxs-lookup"><span data-stu-id="1aa11-133">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="1aa11-134">Делегированные поставщика</span><span class="sxs-lookup"><span data-stu-id="1aa11-134">Delegated Provider</span></span> |<span data-ttu-id="1aa11-135">Пользователь</span><span class="sxs-lookup"><span data-stu-id="1aa11-135">User</span></span> |
| <span data-ttu-id="1aa11-136">Пользователь</span><span class="sxs-lookup"><span data-stu-id="1aa11-136">User</span></span> |<span data-ttu-id="1aa11-137">Пользователь</span><span class="sxs-lookup"><span data-stu-id="1aa11-137">User</span></span> |

## <a name="identify-hello-delegated-providers"></a><span data-ttu-id="1aa11-138">Определите hello делегированы поставщиков</span><span class="sxs-lookup"><span data-stu-id="1aa11-138">Identify hello delegated providers</span></span>
1. <span data-ttu-id="1aa11-139">Войдите как оператор облака.</span><span class="sxs-lookup"><span data-stu-id="1aa11-139">Sign in as cloud operator.</span></span>
2. <span data-ttu-id="1aa11-140">Создание предложения hello, позволяющую поставщикам toobecome делегированы пользователей.</span><span class="sxs-lookup"><span data-stu-id="1aa11-140">Create hello offer that enables users toobecome delegated providers.</span></span> <span data-ttu-id="1aa11-141">Для этого необходимо создать план и на его основе предложение:</span><span class="sxs-lookup"><span data-stu-id="1aa11-141">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="1aa11-142">а.</span><span class="sxs-lookup"><span data-stu-id="1aa11-142">a.</span></span>  <span data-ttu-id="1aa11-143">[Создание плана](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="1aa11-143">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="1aa11-144">Этот план должен содержать только служба hello подписок.</span><span class="sxs-lookup"><span data-stu-id="1aa11-144">This plan should include only hello subscriptions service.</span></span> <span data-ttu-id="1aa11-145">В этой статье мы используем план с именем PlanForDelegation.</span><span class="sxs-lookup"><span data-stu-id="1aa11-145">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="1aa11-146">b.</span><span class="sxs-lookup"><span data-stu-id="1aa11-146">b.</span></span>  <span data-ttu-id="1aa11-147">[Создать предложение](azure-stack-create-offer.md) на основе этого плана.</span><span class="sxs-lookup"><span data-stu-id="1aa11-147">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="1aa11-148">В этой статье мы используем вызывается OfferToDP предложение.</span><span class="sxs-lookup"><span data-stu-id="1aa11-148">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="1aa11-149">c.</span><span class="sxs-lookup"><span data-stu-id="1aa11-149">c.</span></span>  <span data-ttu-id="1aa11-150">После завершения создания hello предложения hello добавляется hello делегированного поставщик предложение toothis подписчика, щелкнув **подписки** &gt; **добавить** &gt; **New Подписки для клиента**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-150">Once hello creation of hello offer is complete, add hello delegated provider as a subscriber toothis offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="1aa11-151">С все предложения стек Azure имеется возможность hello создания предложения hello public и т. е пользователи подписаться или хранение закрытого и имеют оператор облака hello управление hello регистрации.</span><span class="sxs-lookup"><span data-stu-id="1aa11-151">As with all Azure Stack offers, you have hello option of making hello offer public and letting users sign up for it, or keeping it private and have hello cloud operator manage hello sign-up.</span></span> <span data-ttu-id="1aa11-152">Делегированные поставщики обычно являются небольшой группе и хотите toocontrol, кто является допущенная tooit, поэтому хранение закрытого это предложение имеет смысл в большинстве случаев.</span><span class="sxs-lookup"><span data-stu-id="1aa11-152">Delegated providers are usually a small group and you want toocontrol who is admitted tooit, so keeping this offer private makes sense in most cases.</span></span>
> 
> 

## <a name="cloud-operator-creates-hello-delegated-offer"></a><span data-ttu-id="1aa11-153">Оператор облака создает предложение делегированного hello</span><span class="sxs-lookup"><span data-stu-id="1aa11-153">Cloud operator creates hello delegated offer</span></span>

<span data-ttu-id="1aa11-154">Теперь вы установили делегированного поставщика.</span><span class="sxs-lookup"><span data-stu-id="1aa11-154">You have now established your delegated provider.</span></span> <span data-ttu-id="1aa11-155">Hello следующим шагом является создание плана hello и предлагают, что будет toodelegate, а какие будут использовать клиенты.</span><span class="sxs-lookup"><span data-stu-id="1aa11-155">hello next step is to create hello plan and offer that you are going toodelegate, and which your customers will use.</span></span> <span data-ttu-id="1aa11-156">Это предложение следует определять так, как клиенты toosee, поскольку полномочный hello поставщика нельзя будет изменить планы hello и квоты, он содержит.</span><span class="sxs-lookup"><span data-stu-id="1aa11-156">You should define this offer exactly as you want the customers toosee it, because hello delegated provider will not be able to change hello plans and quotas it includes.</span></span>

1. <span data-ttu-id="1aa11-157">Как оператор облака [создать план](azure-stack-create-plan.md) и [предложение](azure-stack-create-offer.md) на его основе.</span><span class="sxs-lookup"><span data-stu-id="1aa11-157">As cloud operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="1aa11-158">В этой статье мы используем вызывается DelegatedOffer предложение.</span><span class="sxs-lookup"><span data-stu-id="1aa11-158">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1aa11-159">Это предложение не имеет открытого toobe.</span><span class="sxs-lookup"><span data-stu-id="1aa11-159">This offer does not have toobe public.</span></span> <span data-ttu-id="1aa11-160">Он может быть сделан открытым, если выбрано, но в большинстве случаев требуется только полномочные tooit доступа toohave поставщиков.</span><span class="sxs-lookup"><span data-stu-id="1aa11-160">It can be made public if you choose, but, in most cases, you only want delegated providers toohave access tooit.</span></span> <span data-ttu-id="1aa11-161">После закрытого предложение делегировать, как описано в hello, выполнив действия, hello делегированного поставщика есть tooit доступа.</span><span class="sxs-lookup"><span data-stu-id="1aa11-161">Once you delegate a private offer as described in hello following steps, hello delegated provider has access tooit.</span></span>
   > 
   > 
1. <span data-ttu-id="1aa11-162">Предложение hello делегата.</span><span class="sxs-lookup"><span data-stu-id="1aa11-162">Delegate hello offer.</span></span> <span data-ttu-id="1aa11-163">Откройте tooDelegatedOffer и в области параметров hello, щелкните **делегированы поставщики** &gt; **добавить**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-163">Go tooDelegatedOffer, and in hello Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
2. <span data-ttu-id="1aa11-164">Выберите подписку делегированного поставщика hello hello раскрывающемся списке и нажмите кнопку **делегат**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-164">Select hello delegated provider’s subscription from hello drop-down list box and click **Delegate**.</span></span>

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-hello-offer"></a><span data-ttu-id="1aa11-165">Делегированные поставщика настраивает предложение hello</span><span class="sxs-lookup"><span data-stu-id="1aa11-165">Delegated provider customizes hello offer</span></span>

<span data-ttu-id="1aa11-166">Войдите в toohello **портала клиента** как hello делегируются поставщику и создание нового предложения, используя предложение делегированного hello в качестве шаблона.</span><span class="sxs-lookup"><span data-stu-id="1aa11-166">Sign in toohello **tenant portal** as hello delegated provider and create a new offer using hello delegated offer as a template.</span></span>

1. <span data-ttu-id="1aa11-167">Нажмите кнопку **новый** &gt; **клиента предлагает + планы** &gt; **предлагают**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-167">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="1aa11-168">Назначьте предложение toohello имя.</span><span class="sxs-lookup"><span data-stu-id="1aa11-168">Assign a name toohello offer.</span></span> <span data-ttu-id="1aa11-169">Здесь мы выбираем ResellerOffer.</span><span class="sxs-lookup"><span data-stu-id="1aa11-169">Here we choose ResellerOffer.</span></span> <span data-ttu-id="1aa11-170">Выберите hello делегировать предложение toobase ее на и выберите команду **создать**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-170">Select hello delegated offer toobase it on and then click **Create**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="1aa11-171">Примечание hello значительно отличаются toooffer созданием как опытным оператором hello облака.</span><span class="sxs-lookup"><span data-stu-id="1aa11-171">Note hello difference compared toooffer creation as experienced by hello cloud operator.</span></span> <span data-ttu-id="1aa11-172">Поставщик делегированного Hello не создает предложение hello базовые планы и планы надстройка; они могут выбирать только из предложений, которые были делегированного toothem и вносить изменения toothose предложения.</span><span class="sxs-lookup"><span data-stu-id="1aa11-172">hello delegated provider does not construct hello offer from base plans and add-on plans; they can only choose from offers that have been delegated toothem, and can't make changes toothose offers.</span></span>

1. <span data-ttu-id="1aa11-173">Сделать hello предлагают общедоступным, щелкнув **Обзор** &gt; **предлагает**, при выборе предложения hello и щелкнув **изменению состояния**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-173">Make hello offer public by clicking **Browse** &gt; **Offers**, selecting hello offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="1aa11-174">Hello делегированного поставщик предоставляет эти предложения собственные портале URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1aa11-174">hello delegated provider exposes these offers through their own portal URL.</span></span> <span data-ttu-id="1aa11-175">Эти предложения, отображаются только через портал делегированы hello.</span><span class="sxs-lookup"><span data-stu-id="1aa11-175">These offers are visible only through hello delegated portal.</span></span> <span data-ttu-id="1aa11-176">toofind и изменить этот URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="1aa11-176">toofind and change this URL:</span></span>
   
    <span data-ttu-id="1aa11-177">а.</span><span class="sxs-lookup"><span data-stu-id="1aa11-177">a.</span></span>  <span data-ttu-id="1aa11-178">Нажмите кнопку **Обзор** &gt; **дополнительные службы** &gt; **подписки** &gt; выберите hello делегированы подписки поставщика в нашем случае его *DPSubscription* &gt; **свойства**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-178">Click **Browse**&gt; **More services**&gt; **Subscriptions**&gt; Select hello delegated provider subscription, in our case its *DPSubscription*&gt; **Properties**.</span></span>
   
    <span data-ttu-id="1aa11-179">b.</span><span class="sxs-lookup"><span data-stu-id="1aa11-179">b.</span></span>  <span data-ttu-id="1aa11-180">Скопируйте hello портала URL-адрес tooa отдельном расположении, таком как Блокнот.</span><span class="sxs-lookup"><span data-stu-id="1aa11-180">Copy hello portal URL tooa separate location, such as Notepad.</span></span>
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   <span data-ttu-id="1aa11-181">Создания hello делегированного предлагается как поставщик делегированного успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="1aa11-181">You have now completed hello creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="1aa11-182">Выйдите из системы как hello делегированного поставщика.</span><span class="sxs-lookup"><span data-stu-id="1aa11-182">Sign out as hello delegated provider.</span></span> <span data-ttu-id="1aa11-183">Закройте вкладку браузера hello, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="1aa11-183">Close hello browser tab you have been using.</span></span>

## <a name="sign-up-for-hello-offer"></a><span data-ttu-id="1aa11-184">Подписаться на предложение hello</span><span class="sxs-lookup"><span data-stu-id="1aa11-184">Sign up for hello offer</span></span>
1. <span data-ttu-id="1aa11-185">В новом окне браузера перейдите делегированного портала toohello URL-адрес, созданный на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="1aa11-185">In a new browser window, go toohello delegated portal URL you saved in hello previous step.</span></span> <span data-ttu-id="1aa11-186">Войдите в портал toohello имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="1aa11-186">Sign in toohello portal as user.</span></span> <span data-ttu-id="1aa11-187">Примечание: Используйте hello делегированных портал для этого шага.</span><span class="sxs-lookup"><span data-stu-id="1aa11-187">Note: Use hello delegated portal for this step.</span></span> <span data-ttu-id="1aa11-188">предложение делегированного Hello в противном случае не отображаются.</span><span class="sxs-lookup"><span data-stu-id="1aa11-188">hello delegated offer are not visible otherwise.</span></span>
2. <span data-ttu-id="1aa11-189">В панели мониторинга hello, щелкните **получить подписку**.</span><span class="sxs-lookup"><span data-stu-id="1aa11-189">In hello dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="1aa11-190">Вы увидите, что содержит только делегированы hello, созданные поставщиком hello делегированы доступны toohello пользователя:</span><span class="sxs-lookup"><span data-stu-id="1aa11-190">You will see that only hello delegated offers created by hello delegated provider are presented toohello user:</span></span>

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="1aa11-191">На этом завершается процесс hello предложение делегирования.</span><span class="sxs-lookup"><span data-stu-id="1aa11-191">This concludes hello process of offer delegation.</span></span> <span data-ttu-id="1aa11-192">Hello пользователь может теперь зарегистрироваться на это предложение, обратившись подписки для него.</span><span class="sxs-lookup"><span data-stu-id="1aa11-192">hello user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="1aa11-193">Делегирование многоуровневого</span><span class="sxs-lookup"><span data-stu-id="1aa11-193">Multiple-tier delegation</span></span>

<span data-ttu-id="1aa11-194">Делегирование многоуровневого позволяет hello делегировать поставщику toodelegate сущностей tooother предложения.</span><span class="sxs-lookup"><span data-stu-id="1aa11-194">Multiple-tier delegation allows hello delegated provider toodelegate the offer tooother entities.</span></span> <span data-ttu-id="1aa11-195">Это позволяет, например, создание hello глубже каналов торгового посредника, в которых hello поставщик управляющий стек Azure делегирует распространителя tooa предложения, который в свою очередь делегирует tooreseller.</span><span class="sxs-lookup"><span data-stu-id="1aa11-195">This allows, for example, hello creation of deeper reseller channels, in which hello provider managing Azure Stack delegates an offer tooa distributor, who in turn delegates tooreseller.</span></span>
<span data-ttu-id="1aa11-196">Стек Azure поддерживает до уровней toofive делегирования.</span><span class="sxs-lookup"><span data-stu-id="1aa11-196">Azure Stack supports up toofive levels of delegation.</span></span>

<span data-ttu-id="1aa11-197">toocreate делегирования предлагают на нескольких уровнях, поставщик делегированного hello в свою очередь делегирует поставщик Далее toohello предложения hello.</span><span class="sxs-lookup"><span data-stu-id="1aa11-197">toocreate multiple tiers of offer delegation, hello delegated provider in turn delegates hello offer toohello next provider.</span></span> <span data-ttu-id="1aa11-198">Hello процесса является hello же для делегированной поставщика hello как и оператор hello облака (в разделе [оператор облака создает предложение делегированного hello](#cloud-operator-creates-the-delegated-offer)).</span><span class="sxs-lookup"><span data-stu-id="1aa11-198">hello process is hello same for hello delegated provider as it was for hello cloud operator (see [Cloud operator creates hello delegated offer](#cloud-operator-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa11-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1aa11-199">Next steps</span></span>
[<span data-ttu-id="1aa11-200">Подготовка виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1aa11-200">Provision a VM</span></span>](azure-stack-provision-vm.md)

