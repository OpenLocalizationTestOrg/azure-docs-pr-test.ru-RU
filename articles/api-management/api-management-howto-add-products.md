---
title: "Создание и публикация продукта в службе управления API Azure"
description: "Сведения о создании и публикации продуктов в службе управления API Azure."
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="58cc4-103">Создание и публикация продукта в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="58cc4-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="58cc4-104">В службе управления API Azure продукт содержит один или несколько API вместе с квотой и условиями использования.</span><span class="sxs-lookup"><span data-stu-id="58cc4-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="58cc4-105">Как только продукт будет опубликован, разработчики могут подписаться на него и начать использовать его интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="58cc4-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="58cc4-106">В данном разделе рассматривается процесс создания продукта, добавления интерфейса API и публикации продукта для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="58cc4-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="58cc4-107"><a name="create-product"> </a>Создание продукта</span><span class="sxs-lookup"><span data-stu-id="58cc4-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="58cc4-108">Операции добавляются и настраиваются для API на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="58cc4-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="58cc4-109">Чтобы перейти на портал издателя, на портале Azure щелкните **Publisher portal** (Портал издателя) для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="58cc4-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="58cc4-111">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="58cc4-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="58cc4-112">Щелкните **Продукты** в меню слева для отображения страницы **Продукты**, а затем щелкните **Добавить продукт**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Продукты][api-management-products]

![Новый продукт][api-management-add-new-product]

<span data-ttu-id="58cc4-115">Введите описательное имя для продукта в поле **Имя** и описание продукта в поле **Описание**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="58cc4-116">Продукты в службе управления API могут быть **открытыми** или **защищенными**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="58cc4-117">Прежде чем можно будет использовать защищенные продукты, на них необходимо подписаться, а открытые продукты могут использоваться без подписки.</span><span class="sxs-lookup"><span data-stu-id="58cc4-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="58cc4-118">Установите флажок **Требуется подписка** , чтобы создать защищенный продукт, требующий подписки.</span><span class="sxs-lookup"><span data-stu-id="58cc4-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="58cc4-119">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="58cc4-119">This is the default setting.</span></span>

<span data-ttu-id="58cc4-120">Установите флажок **Require subscription approval** (Требуется утверждение администратора), если вы хотите, чтобы администратор рассматривал и принимал или отклонял попытки подписки на этот продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="58cc4-121">Если флажок не установлен, попытки подписки получат автоматическое утверждение.</span><span class="sxs-lookup"><span data-stu-id="58cc4-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="58cc4-122">Дополнительные сведения о подписках см. в разделе [Просмотр подписчиков продукта][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="58cc4-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="58cc4-123">Чтобы разрешить для учетных записей разработчика многократную подписку на продукт, установите флажок **Разрешить несколько подписок** .</span><span class="sxs-lookup"><span data-stu-id="58cc4-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="58cc4-124">Если этот флажок не установлен, каждую учетную запись разработчика можно подписать на продукт только один раз.</span><span class="sxs-lookup"><span data-stu-id="58cc4-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Неограниченное количество подписок][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="58cc4-126">Чтобы ограничить количество одновременных подписок, установите флажок **Ограничить количество одновременных подписок до** и введите ограничение количества подписок.</span><span class="sxs-lookup"><span data-stu-id="58cc4-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="58cc4-127">В следующем примере количество одновременных подписок ограничено до четырех на каждую учетную запись разработчика.</span><span class="sxs-lookup"><span data-stu-id="58cc4-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Четыре подписки][api-management-four-multiple-subscriptions]

<span data-ttu-id="58cc4-129">После настройки всех параметров нового продукта щелкните **Сохранить** , чтобы создать новый продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Продукты][api-management-products-page]

> <span data-ttu-id="58cc4-131">По умолчанию новые продукты не опубликованы и видны только группе **Администраторы**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="58cc4-132">Для настройки продукта щелкните имя продукта на вкладке **Продукты** .</span><span class="sxs-lookup"><span data-stu-id="58cc4-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="58cc4-133"><a name="add-apis"> </a>Добавление интерфейсов API в продукт</span><span class="sxs-lookup"><span data-stu-id="58cc4-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="58cc4-134">Страница **Продукты** содержит четыре ссылки для настройки: **Сводка**, **Параметры**, **Видимость** и **Подписчики**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="58cc4-135">На вкладке **Сводка** можно добавить интерфейсы API, а также опубликовать продукт или отменить его публикацию.</span><span class="sxs-lookup"><span data-stu-id="58cc4-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Сводка][api-management-new-product-summary]

<span data-ttu-id="58cc4-137">Прежде чем опубликовать продукт, необходимо добавить один или несколько интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="58cc4-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="58cc4-138">Для этого щелкните **Добавить API к продукту**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-138">To do this, click **Add API to product**.</span></span>

![Добавление интерфейсов API][api-management-add-apis-to-product]

<span data-ttu-id="58cc4-140">Выберите требуемые интерфейсы API и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="58cc4-141"><a name="add-description"> </a>Добавление описательной информации в продукт</span><span class="sxs-lookup"><span data-stu-id="58cc4-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="58cc4-142">На вкладке **Параметры** можно вводить подробные сведения о продукте, например его назначение, интерфейсы API, к которым он предоставляет доступ, и другую полезную информацию.</span><span class="sxs-lookup"><span data-stu-id="58cc4-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="58cc4-143">Данные сведения предназначены для разработчиков, которые будут вызывать API, и могут быть внесены в виде обычного текста или в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="58cc4-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Параметры продукта][api-management-product-settings]

<span data-ttu-id="58cc4-145">Установите флажок **Требуется подписка** , чтобы создать защищенный продукт, который требует подписку для использования, или снимите флажок, чтобы создать открытый продукт, который можно вызвать без подписки.</span><span class="sxs-lookup"><span data-stu-id="58cc4-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="58cc4-146">Установите флажок **Требуется утверждение администратором** , если вы хотите вручную утверждать все запросы подписки на продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="58cc4-147">По умолчанию все подписки на продукт предоставляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="58cc4-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="58cc4-148">Чтобы разрешить для учетных записей разработчика многократную подписку на продукт, установите флажок **Разрешить несколько подписок** и по желанию укажите ограничение.</span><span class="sxs-lookup"><span data-stu-id="58cc4-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="58cc4-149">Если этот флажок не установлен, каждую учетную запись разработчика можно подписать на продукт только один раз.</span><span class="sxs-lookup"><span data-stu-id="58cc4-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="58cc4-150">Дополнительно в поле **Условия использования** можно указать условия применения продукта, который должны принимать подписчики, если они хотят использовать продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="58cc4-151"><a name="publish-product"> </a>Публикация продукта</span><span class="sxs-lookup"><span data-stu-id="58cc4-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="58cc4-152">Прежде чем можно будет вызывать интерфейсы API в продукте, сам продукт должен быть опубликован.</span><span class="sxs-lookup"><span data-stu-id="58cc4-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="58cc4-153">На вкладке **Сводка** для продукта щелкните **Опубликовать**, а затем **Yes, publish it** (Да, опубликовать) для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="58cc4-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="58cc4-154">Для отмены публикации уже опубликованного продукта щелкните **Отменить публикацию**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-154">To make a previously published product private, click **Unpublish**.</span></span>

![Публикация продукта][api-management-publish-product]

## <span data-ttu-id="58cc4-156"><a name="make-visible"> </a>Обеспечение видимости продукта для разработчиков</span><span class="sxs-lookup"><span data-stu-id="58cc4-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="58cc4-157">На вкладке **Видимость** можно указать, какие роли смогут видеть продукт на портале разработчика и подписываться на продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Видимость продукта][api-management-product-visiblity]

<span data-ttu-id="58cc4-159">Чтобы включить или отключить видимость продукта для разработчиков в группе, установите или снимите флажок для группы, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="58cc4-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="58cc4-160">Дополнительные сведения см. в статье [Как создавать и использовать группы для управления учетными записями разработчика в службе управления Azure API][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="58cc4-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="58cc4-161"><a name="view-subscribers"> </a>Просмотр подписчиков продукта</span><span class="sxs-lookup"><span data-stu-id="58cc4-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="58cc4-162">На вкладке **Подписчики** содержится перечень разработчиков, которые подписались на продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="58cc4-163">Для просмотра сведений и параметров для каждого разработчика щелкните по имени разработчика.</span><span class="sxs-lookup"><span data-stu-id="58cc4-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="58cc4-164">В этом примере никакие разработчики еще не подписались на продукт.</span><span class="sxs-lookup"><span data-stu-id="58cc4-164">In this example no developers have yet subscribed to the product.</span></span>

![Разработчики][api-management-developer-list]

## <span data-ttu-id="58cc4-166"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58cc4-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="58cc4-167">Как только требуемые интерфейсы API добавлены, а продукт опубликован, разработчики могут подписаться на продукт и начать вызывать интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="58cc4-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="58cc4-168">Руководство, в котором рассматриваются эти операции, а также подробно описывается конфигурация продукта, см. в статье [Защита API путем ограничения скорости с помощью управления API Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="58cc4-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="58cc4-169">Дополнительную информацию о работе с продуктами см. в следующем видео.</span><span class="sxs-lookup"><span data-stu-id="58cc4-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
