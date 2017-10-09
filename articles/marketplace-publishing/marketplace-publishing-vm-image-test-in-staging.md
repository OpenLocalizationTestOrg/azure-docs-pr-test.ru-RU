---
title: "aaaTest предлагают ВМ для hello Marketplace | Документы Microsoft"
description: "Понимать, каким образом tootest виртуальной Машины из образа для hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="ddc35-103">Проверить ваше предложение виртуальной Машины для hello Azure Marketplace в промежуточной</span><span class="sxs-lookup"><span data-stu-id="ddc35-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="ddc35-104">Промежуточная означает развертыванию ваш SKU в закрытом «песочницы», где можно протестировать и проверить его функциональность перед его развертыванием toohello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ddc35-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="ddc35-105">Hello SKU появляется в промежуточном так же, как будто он имеет tooa клиента, к которому она развернута.</span><span class="sxs-lookup"><span data-stu-id="ddc35-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="ddc35-106">Образ виртуальной Машины должно быть toostaging сертифицированных toobe отправлена.</span><span class="sxs-lookup"><span data-stu-id="ddc35-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="ddc35-107">Шаг 1: Push toostaging вашего предложения</span><span class="sxs-lookup"><span data-stu-id="ddc35-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="ddc35-108">На hello **публикации** щелкните **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="ddc35-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![рисунок](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="ddc35-110">Если портал публикации hello сообщает об ошибках, исправьте их.</span><span class="sxs-lookup"><span data-stu-id="ddc35-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="ddc35-111">В hello **доступ промежуточные предложение?** диалогового окна введите hello список подписок Azure, который будет использоваться toopreview ваше предложение в hello [портал предварительной версии Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ddc35-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ddc35-112">В случае с виртуальными машинами и шаблонами решений **не** включайте в список разрешений подписки типа CSP, DreamSpark или Azure с открытой лицензией.</span><span class="sxs-lookup"><span data-stu-id="ddc35-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="ddc35-113">В случае виртуальные машины, после нажатия на кнопку hello **tooSTAGING ПРИНУДИТЕЛЬНОЙ**, hello указанные действия выполняются за hello сцены.</span><span class="sxs-lookup"><span data-stu-id="ddc35-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="ddc35-114">Можно будет tooview hello ход выполнения каждого шага на вкладке публикации hello в hello публикацию портала.</span><span class="sxs-lookup"><span data-stu-id="ddc35-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="ddc35-115">Необходимо проверить эту страницу определенные интервалы (до состояния hello показывает ПРОМЕЖУТОЧНОЕ) для любого сообщения об ошибках которых требует исправления из твоих.</span><span class="sxs-lookup"><span data-stu-id="ddc35-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="ddc35-116">На первом промежуточный запрос направляется сертификации toohello рабочей группы, которым проверка hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="ddc35-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="ddc35-117">Тем не менее, если запрос есть только маркетинговые изменений, затем hello сертификации шаг пропускается.</span><span class="sxs-lookup"><span data-stu-id="ddc35-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="ddc35-118">После завершения сертификации hello репликации hello начала предложения по всем hello центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc35-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="ddc35-119">Обычно имеет 24-48hours для hello toocomplete репликации, но может занять до tooa недели, в зависимости от размера hello hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="ddc35-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="ddc35-120">Однако если запрос есть только маркетинговые изменений, затем hello репликации выполняется быстрее.</span><span class="sxs-lookup"><span data-stu-id="ddc35-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="ddc35-121">По завершении репликации hello затем hello предложения будут доступны в hello [портал Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ddc35-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="ddc35-122">В этой hello времени состояние становятся ЗАНЕСЕНЫ в hello публикацию портала.</span><span class="sxs-lookup"><span data-stu-id="ddc35-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="ddc35-123">Промежуточные предложение является видимым в hello [портал Azure](http:/portal.azure.com) только с использованием идентификаторов hello электронной почты, связанный с подпиской hello, с которой hello на промежуточное хранение предложение.</span><span class="sxs-lookup"><span data-stu-id="ddc35-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="ddc35-124">Войдите в toohello [портал предварительной версии Azure](https://portal.azure.com) с помощью одного из hello подписок Azure, перечисленные в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="ddc35-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="ddc35-125">Найдите свое предложение и проверьте образ виртуальной машины на соответствие следующим условиям:</span><span class="sxs-lookup"><span data-stu-id="ddc35-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="ddc35-126">Убедитесь в том, маркетинговые содержимое отображается правильно в hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ddc35-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="ddc35-127">Развертывание образа виртуальной Машины hello начала до конца.</span><span class="sxs-lookup"><span data-stu-id="ddc35-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="ddc35-129">Ваше предложение будет оставаться в промежуточной, пока не будет уведомлять корпорацию Майкрософт через портал публикации hello [**публикации** вкладка > нажмите кнопку "hello" **» tooProduction tooPush утверждения запроса «**], которые готовы toopush tooproduction.</span><span class="sxs-lookup"><span data-stu-id="ddc35-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="ddc35-130">Это toohave идеальный времени проверять все члены вашей команды через все, что в процессе подготовки для вашего предложения, перейдя в списке.</span><span class="sxs-lookup"><span data-stu-id="ddc35-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="ddc35-131">Hello промежуточных платформы предназначен для тестирования предложение hello в режиме предварительного просмотра hello издателем.</span><span class="sxs-lookup"><span data-stu-id="ddc35-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="ddc35-132">Настоятельно рекомендуем не использовать эту платформу в коммерческих целях.</span><span class="sxs-lookup"><span data-stu-id="ddc35-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ddc35-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddc35-133">Next steps</span></span>
<span data-ttu-id="ddc35-134">Теперь, когда ваше предложение «промежуточные» и протестируйте его функциональность и маркетинга содержимого, можно перейти последней публикации toohello этапе **шаг 4**: [развертывание вашего предложения toohello Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="ddc35-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ddc35-135">См. также</span><span class="sxs-lookup"><span data-stu-id="ddc35-135">See also</span></span>
* [<span data-ttu-id="ddc35-136">Приступая к работе: как toopublish toohello предложение Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ddc35-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

