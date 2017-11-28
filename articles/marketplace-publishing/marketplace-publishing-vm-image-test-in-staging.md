---
title: "Тестирование предложения виртуальной машины для Marketplace | Документация Майкрософт"
description: "Узнайте, как протестировать образ виртуальной машины для Azure Marketplace."
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
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="196f4-103">Тестирование виртуальной машины для Azure Marketplace в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="196f4-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="196f4-104">Промежуточная среда подразумевает развертывание номера SKU в частной "песочнице", где можно проверить все функциональные возможности вашего решения и убедиться в его работоспособности перед развертыванием в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="196f4-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="196f4-105">SKU отображается в промежуточной среде точно так же, как на компьютере выполнившего развертывание клиента.</span><span class="sxs-lookup"><span data-stu-id="196f4-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="196f4-106">Для промежуточного развертывания образ виртуальной машины должен пройти сертификацию.</span><span class="sxs-lookup"><span data-stu-id="196f4-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="196f4-107">Шаг 1. Промежуточное развертывание предложения</span><span class="sxs-lookup"><span data-stu-id="196f4-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="196f4-108">Щелкните **Push to Staging** (Переместить в промежуточную среду) на вкладке **Публикация**.</span><span class="sxs-lookup"><span data-stu-id="196f4-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![рисунок](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="196f4-110">Если портал публикации сообщит об ошибках, исправьте их.</span><span class="sxs-lookup"><span data-stu-id="196f4-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="196f4-111">В диалоговом окне **Кому доступно предложение на промежуточном хранении?** введите список подписок Azure, которые будут использоваться для предварительного просмотра вашего предложения на [портале предварительной версии Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="196f4-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="196f4-112">В случае с виртуальными машинами и шаблонами решений **не** включайте в список разрешений подписки типа CSP, DreamSpark или Azure с открытой лицензией.</span><span class="sxs-lookup"><span data-stu-id="196f4-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="196f4-113">В случае с виртуальными машинами при нажатии кнопки **PUSH TO STAGING**(Переместить в промежуточную среду) в фоновом режиме выполняются следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="196f4-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="196f4-114">Вы можете просмотреть ход выполнения каждого шага на портале публикации на вкладке "ПУБЛИКАЦИЯ".</span><span class="sxs-lookup"><span data-stu-id="196f4-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="196f4-115">Эту страницу необходимо проверять регулярно (пока не отобразится состояние "ПРОМЕЖУТОЧНАЯ ВЕРСИЯ"), чтобы в случае сбоя выполнить действия по исправлению со своей стороны.</span><span class="sxs-lookup"><span data-stu-id="196f4-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="196f4-116">Сначала ваш запрос на перемещение в промежуточную среду поступает команде сертификации для проверки VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="196f4-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="196f4-117">Однако, если запрос содержит только маркетинговые изменения, то данный шаг сертификации пропускается.</span><span class="sxs-lookup"><span data-stu-id="196f4-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="196f4-118">По завершении сертификации по всем центрам обработки данных Azure начинается репликация предложения.</span><span class="sxs-lookup"><span data-stu-id="196f4-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="196f4-119">Обычно выполнение репликации занимает от 24 до 48 часов, но в зависимости от размера VHD-файла может длиться до одной недели.</span><span class="sxs-lookup"><span data-stu-id="196f4-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="196f4-120">Однако, если запрос содержит только маркетинговые изменения, то репликация выполняется быстрее.</span><span class="sxs-lookup"><span data-stu-id="196f4-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="196f4-121">По завершении репликации предложение становится доступным на [портале Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="196f4-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="196f4-122">В этот момент состояние на портале публикации меняется на "ПРОМЕЖУТОЧНАЯ ВЕРСИЯ".</span><span class="sxs-lookup"><span data-stu-id="196f4-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="196f4-123">Промежуточная версия предложения отображается на [портале Azure](http:/portal.azure.com) только при использовании идентификаторов электронной почты, связанных с подпиской, с помощью которой предложение было развернуто в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="196f4-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="196f4-124">Войдите на [портал предварительной версии Azure](https://portal.azure.com) , используя одну из подписок, указанных на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="196f4-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="196f4-125">Найдите свое предложение и проверьте образ виртуальной машины на соответствие следующим условиям:</span><span class="sxs-lookup"><span data-stu-id="196f4-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="196f4-126">Убедитесь, что маркетинговое содержимое правильно отображается в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="196f4-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="196f4-127">Образ виртуальной машины развернут полностью.</span><span class="sxs-lookup"><span data-stu-id="196f4-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="196f4-129">Ваше предложение будет находиться в промежуточной среде, пока вы не уведомите Майкрософт о том, что готовы переместить его в рабочую среду, используя портал публикации [вкладка **Публикация** > нажмите кнопку **Request Approval to Push to Production** (Запросить утверждение для перемещения в рабочую среду)].</span><span class="sxs-lookup"><span data-stu-id="196f4-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="196f4-130">Это время идеально для выполнения всех проверок вашими специалистами, чтобы подготовиться к внесению предложения в список.</span><span class="sxs-lookup"><span data-stu-id="196f4-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="196f4-131">Платформа промежуточного развертывания разработана для того, чтобы издатель мог протестировать предложение в режиме предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="196f4-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="196f4-132">Настоятельно рекомендуем не использовать эту платформу в коммерческих целях.</span><span class="sxs-lookup"><span data-stu-id="196f4-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="196f4-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="196f4-133">Next steps</span></span>
<span data-ttu-id="196f4-134">Теперь, когда вы развернули предложение в промежуточной среде и проверили его функциональность и маркетинговое содержимое, переходите к этапу окончательной публикации предложения: **Шаг 4.**[Развертывание предложения в Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="196f4-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="196f4-135">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="196f4-135">See also</span></span>
* [<span data-ttu-id="196f4-136">Приступая к работе: как опубликовать предложение в Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="196f4-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

