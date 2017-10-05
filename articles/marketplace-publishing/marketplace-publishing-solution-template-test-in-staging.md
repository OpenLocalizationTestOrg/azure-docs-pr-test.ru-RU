---
title: "Тестирование предложения шаблона решения для Marketplace | Документация Майкрософт"
description: "Узнайте, как протестировать предложение шаблона решения для Azure Marketplace."
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
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="d11ee-103">Тестирование предложения шаблона решения в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="d11ee-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="d11ee-104">Промежуточное развертывание подразумевает развертывание предложения в частной песочнице, в которой вы можете проверить все его функциональные возможности и убедиться в их работе перед публикацией в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d11ee-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="d11ee-105">Предложение отображается в промежуточной среде точно так же, как на компьютере выполнившего развертывание клиента.</span><span class="sxs-lookup"><span data-stu-id="d11ee-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="d11ee-106">Для промежуточного развертывания предложение должно пройти сертификацию.</span><span class="sxs-lookup"><span data-stu-id="d11ee-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="d11ee-107">После промежуточного развертывания предложения его можно просмотреть и проверить на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d11ee-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="d11ee-108">Выполните следующие шаги, чтобы отправить предложение в промежуточную среду и провести его тестирование на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d11ee-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="d11ee-109">Выберите [Портал публикации](https://publish.windowsazure.com) >  вкладка **Шаблоны решений** > ваше предложение > **Публикация** > **Push to Staging** (Переместить в промежуточную среду).</span><span class="sxs-lookup"><span data-stu-id="d11ee-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="d11ee-110">Укажите список подписок Azure, которые будут использоваться для предварительного просмотра и тестирования предложения.</span><span class="sxs-lookup"><span data-stu-id="d11ee-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="d11ee-111">Войдите на портал предварительной версии Azure, применяя идентификатор подписки, указанной на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="d11ee-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="d11ee-112">На портале предварительной версии Azure выполните по крайней мере один цикл тестирования по пунктам, указанным ниже.</span><span class="sxs-lookup"><span data-stu-id="d11ee-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="d11ee-113">Убедитесь, что маркетинговое содержимое правильно отображается в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d11ee-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="d11ee-114">Топология развернута полностью.</span><span class="sxs-lookup"><span data-stu-id="d11ee-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="d11ee-115">Выполните тестирование производительности и стрессовое тестирование.</span><span class="sxs-lookup"><span data-stu-id="d11ee-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="d11ee-116">Убедитесь, что топология соответствует рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="d11ee-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d11ee-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d11ee-117">Next steps</span></span>
<span data-ttu-id="d11ee-118">Если вы довольны результатами, то можете перейти к завершающему этапу публикации предложения, **Шаг 4.**[Развертывание предложения в Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="d11ee-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="d11ee-119">В противном случае внесите изменения в предложение и запросите повторную сертификацию.</span><span class="sxs-lookup"><span data-stu-id="d11ee-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="d11ee-120">Для изменения маркетингового содержимого сертификация не обязательна.</span><span class="sxs-lookup"><span data-stu-id="d11ee-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="d11ee-121">Руководство по всем задачам издателя см. в статье [Как опубликовать предложение и управлять им в Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d11ee-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

