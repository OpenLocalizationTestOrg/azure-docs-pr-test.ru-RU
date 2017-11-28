---
title: "шаблон решения обеспечивают для hello Marketplace aaaTesting | Документы Microsoft"
description: "Понимать, каким образом tootest шаблон решения предложение для hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: 9c195c465d2fc6aa349e4bbcc348e5325f32850d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="abf35-103">Тестирование предложения шаблона решения в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="abf35-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="abf35-104">Промежуточная означает ваше предложение в «песочницу», где можно проверить и проверьте его функциональность перед принудительной отправки tooproduction закрытого развертывания.</span><span class="sxs-lookup"><span data-stu-id="abf35-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="abf35-105">предложение Hello появляется в промежуточном так же, как будто он имеет tooa клиента, к которому она развернута.</span><span class="sxs-lookup"><span data-stu-id="abf35-105">hello offer appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="abf35-106">Ваше предложение должно быть toostaging сертифицированных toobe отправлена.</span><span class="sxs-lookup"><span data-stu-id="abf35-106">Your offer must be certified toobe pushed toostaging.</span></span>

<span data-ttu-id="abf35-107">После предложения hello на промежуточное хранение, можно просмотреть и проверить предложение hello в hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="abf35-107">After hello offer is staged, you can view and test hello offer in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="abf35-108">Выполните действия hello ниже toopush toostaging вашего предложения и тестирование в hello [портала Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="abf35-108">Follow hello steps below toopush your offer toostaging and test it in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="abf35-109">Go toohello [портал публикации](https://publish.windowsazure.com) > **шаблоны решений** вкладка > ваше предложение > **публикации** > **Push tooStaging** .</span><span class="sxs-lookup"><span data-stu-id="abf35-109">Go toohello [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push tooStaging**.</span></span>
2. <span data-ttu-id="abf35-110">Укажите список hello подписок Azure, будут использовать toopreview и протестировать ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="abf35-110">Provide hello list of Azure subscriptions that you will use toopreview and test your offer.</span></span>
3. <span data-ttu-id="abf35-111">Войдите в портал предварительной версии Azure toohello с помощью hello идентификатор подписки, который использовался в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="abf35-111">Sign in toohello Azure preview portal by using hello subscription ID that you used in hello previous step.</span></span>
4. <span data-ttu-id="abf35-112">Выполните по крайней мере одного цикла тестирования на портале Azure предварительной версии hello в точках hello упомянутых ниже:</span><span class="sxs-lookup"><span data-stu-id="abf35-112">Carry out at least one round of testing in hello Azure preview portal on hello points mentioned below:</span></span>
   * <span data-ttu-id="abf35-113">Убедитесь в том, маркетинговые содержимое отображается правильно в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="abf35-113">Make sure that marketing content shows up correctly in hello Azure Marketplace.</span></span>
   * <span data-ttu-id="abf35-114">Развертывание конца в конец hello топологии.</span><span class="sxs-lookup"><span data-stu-id="abf35-114">End-to-end deployment of hello topology.</span></span>
   * <span data-ttu-id="abf35-115">Выполните тестирование производительности и стрессовое тестирование.</span><span class="sxs-lookup"><span data-stu-id="abf35-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="abf35-116">Обеспечьте что топологии toohello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="abf35-116">Ensure that your topology adheres toohello best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abf35-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="abf35-117">Next steps</span></span>
<span data-ttu-id="abf35-118">Если вы удовлетворены результатами hello, то окончательный предложение toohello публикации этапа, можно перейти **шаг 4**: [развертывание вашего предложения toohello Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="abf35-118">If you are satisfied with hello results, then you can proceed toohello final offer publishing phase, **Step 4**:  [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="abf35-119">В противном случае внесите изменения в предложение и запросите повторную сертификацию.</span><span class="sxs-lookup"><span data-stu-id="abf35-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="abf35-120">Для изменения маркетингового содержимого сертификация не обязательна.</span><span class="sxs-lookup"><span data-stu-id="abf35-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="abf35-121">В разделе [Приступая к работе: как toopublish toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md) для задач руководства tooall издателя.</span><span class="sxs-lookup"><span data-stu-id="abf35-121">See [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md) for a guide tooall publisher tasks.</span></span>

