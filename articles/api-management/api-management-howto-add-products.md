---
title: "aaaHow toocreate и публикация продукта в службе управления API Azure"
description: "Узнайте, как toocreate и публиковать продукты в Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="5d3ab-103">Как toocreate и публикация продукта в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="5d3ab-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="5d3ab-104">В службе управления API Azure продукт содержит один или несколько интерфейсов API, а также использование квот и hello условия использования.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="5d3ab-105">После публикации продукта разработчики могут подписаться toohello продукта и начать toouse hello его интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="5d3ab-106">раздел Hello содержит toocreating руководство по продукции, добавление API и публикации для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="5d3ab-107"><a name="create-product"> </a>Создание продукта</span><span class="sxs-lookup"><span data-stu-id="5d3ab-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="5d3ab-108">Операции являются добавляется и настраивается tooan API hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="5d3ab-109">tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="5d3ab-111">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="5d3ab-112">Щелкните **продуктов** выберите в меню слева toodisplay hello hello hello **продуктов** и нажмите кнопку **добавить продукт**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Продукты][api-management-products]

![Новый продукт][api-management-add-new-product]

<span data-ttu-id="5d3ab-115">Введите описательное имя для продукта hello в hello **имя** и описание продукта hello в hello **описание** поля.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="5d3ab-116">Продукты в службе управления API могут быть **открытыми** или **защищенными**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="5d3ab-117">Защищенные продуктов должен быть подписанным toobefore, они могут использоваться, во время открытия продуктов может быть использован без подписки.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="5d3ab-118">Проверьте **требует подписки** toocreate защищенных продукт, который требует наличия подписки.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="5d3ab-119">Это параметр по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-119">This is hello default setting.</span></span>

<span data-ttu-id="5d3ab-120">Проверьте **утверждение подписки** при необходимости tooreview администратора и принять или отклонить подписки пытается toothis продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="5d3ab-121">Если hello флажок не установлен, попыток подписка будет автоматически выполнено.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="5d3ab-122">Дополнительные сведения о подписках см. в разделе [tooa подписчиков просмотр продукта][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="5d3ab-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="5d3ab-123">toosubscribe учетных записей tooallow разработчиков продукта toohello несколько раз, проверьте hello **допускать несколько подписок** флажок.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="5d3ab-124">Если этот флажок не установлен, каждой учетной записи разработчика можно подписаться только один раз toohello продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Неограниченное количество подписок][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="5d3ab-126">число hello toolimit несколько одновременных подписок, проверьте hello **максимальное число одновременных подписок** флажок и введите лимит подписки hello.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="5d3ab-127">В следующем примере hello одновременных подписки, ограниченный toofour на учетную запись разработчика.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Четыре подписки][api-management-four-multiple-subscriptions]

<span data-ttu-id="5d3ab-129">После настройки все новые параметры продукта щелкните **Сохранить** toocreate hello нового продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Продукты][api-management-products-page]

> <span data-ttu-id="5d3ab-131">По умолчанию еще не опубликованы новые продукты и являются видимыми только toohello **Администраторы** группы.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="5d3ab-132">tooconfigure продукта, щелкните имя продукта hello в hello **продуктов** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="5d3ab-133"><a name="add-apis"></a>Добавить API-интерфейсы tooa продукта</span><span class="sxs-lookup"><span data-stu-id="5d3ab-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="5d3ab-134">Hello **продуктов** страница содержит четыре ссылки для конфигурации: **Сводка**, **параметры**, **видимость**, и  **Подписчики**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="5d3ab-135">Hello **Сводка** вкладка, где можно добавить API-интерфейсов и опубликовать или отменить публикацию продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Сводка][api-management-new-product-summary]

<span data-ttu-id="5d3ab-137">Перед публикацией продукта необходимо tooadd один или несколько интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="5d3ab-138">toodo, нажмите кнопку **tooproduct добавить API**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-138">toodo this, click **Add API tooproduct**.</span></span>

![Добавление интерфейсов API][api-management-add-apis-to-product]

<span data-ttu-id="5d3ab-140">Выберите hello требуемого API-интерфейсы и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="5d3ab-141"><a name="add-description"></a>Добавить описательную информацию tooa продукта</span><span class="sxs-lookup"><span data-stu-id="5d3ab-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="5d3ab-142">Hello **параметры** вкладке можно tooprovide подробные сведения о продукте hello, такие как его назначение, hello он обеспечивает доступ к API-интерфейсы и другие полезные сведения.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="5d3ab-143">содержимое Hello ориентирована на разработчиков hello, вызова hello API и могут записываться в обычный текст или HTML-разметка.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Параметры продукта][api-management-product-settings]

<span data-ttu-id="5d3ab-145">Проверьте **требует подписки** toocreate защищенных продукт, который требует toobe подписки используется или очистить hello toocreate флажок Открыть продукта, который может вызываться без подписки.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="5d3ab-146">Выберите **утверждение подписки** Если требуется toomanually утвердить все запросы подписки продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="5d3ab-147">По умолчанию все подписки на продукт предоставляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="5d3ab-148">toosubscribe учетных записей tooallow разработчиков продукта toohello несколько раз, проверьте hello **допускать несколько подписок** флажок и при необходимости укажите ограничение.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="5d3ab-149">Если этот флажок не установлен, каждой учетной записи разработчика можно подписаться только один раз toohello продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="5d3ab-150">При необходимости заполните hello **условия использования** поле, описывающее hello условия использования для hello продукта, который необходимо принять подписчиков в порядке toouse hello продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="5d3ab-151"><a name="publish-product"> </a>Публикация продукта</span><span class="sxs-lookup"><span data-stu-id="5d3ab-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="5d3ab-152">Перед вызовом hello интерфейсы API в продукте hello продукта должен быть опубликован.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="5d3ab-153">На hello **Сводка** hello продукта, нажмите кнопку **публикации**, а затем нажмите кнопку **Да, опубликуйте его** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="5d3ab-154">Щелкните toomake закрытый ранее опубликованные продукта, **отменить публикацию**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Публикация продукта][api-management-publish-product]

## <span data-ttu-id="5d3ab-156"><a name="make-visible"></a>Сделать видимым toodevelopers продукта</span><span class="sxs-lookup"><span data-stu-id="5d3ab-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="5d3ab-157">Hello **видимость** вкладке можно toochoose, какие роли могут toosee hello продукта на портал разработчиков hello и подписываться toohello продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Видимость продукта][api-management-product-visiblity]

<span data-ttu-id="5d3ab-159">tooenable или отключить видимость продукта для разработчиков hello в группе, установите или снимите флажок hello рядом с hello группы и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="5d3ab-160">Дополнительные сведения см. в разделе [как разработчик toomanage группы toocreate и использование учетных записей в Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5d3ab-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="5d3ab-161"><a name="view-subscribers"></a>Просмотр подписчиков tooa продукта</span><span class="sxs-lookup"><span data-stu-id="5d3ab-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="5d3ab-162">Hello **подписчиков** вкладке перечисляются hello разработчиков, которые подписаны toohello продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="5d3ab-163">Hello сведения и параметры на каждом компьютере разработчика можно просмотреть, щелкнув имя разработчика hello.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="5d3ab-164">В этом примере не разработчики еще подписаны toohello продукта.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-164">In this example no developers have yet subscribed toohello product.</span></span>

![Разработчики][api-management-developer-list]

## <span data-ttu-id="5d3ab-166"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d3ab-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="5d3ab-167">Один раз hello требуемого API-интерфейсы добавляются и опубликован продукт hello, разработчики могут подписаться toohello продукта и начать hello toocall API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="5d3ab-168">Руководство, в котором рассматриваются эти операции, а также подробно описывается конфигурация продукта, см. в статье [Защита API путем ограничения скорости с помощью управления API Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5d3ab-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="5d3ab-169">Дополнительные сведения о работе с продуктами см. следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="5d3ab-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
