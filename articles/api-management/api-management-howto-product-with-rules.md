---
title: "Защита API с помощью службы управления API Azure | Документация Майкрософт"
description: "Узнайте, как защитить API с помощью политик квот и регулирования (ограничения скорости)."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 5553bcb8f9fd38630f694151dc644a684266387c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="254c6-103">Защита API путем ограничения скорости с помощью управления API Azure</span><span class="sxs-lookup"><span data-stu-id="254c6-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="254c6-104">В этом руководстве показано, как просто защитить серверный API, настроив политики ограничения скорости и политики квот с помощью управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="254c6-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="254c6-105">В ходе работы с этим руководством вы создадите продукт "Бесплатная пробная версия", в котором есть API. Разработчики смогут вызывать этот API до 10 раз в минуту и до 200 раз в неделю, используя политики [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) (Ограничение скорости вызова по подписке) и [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) (Установка квоты использования по подписке).</span><span class="sxs-lookup"><span data-stu-id="254c6-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="254c6-106">Затем вы опубликуете API и протестируете политику ограничения скорости.</span><span class="sxs-lookup"><span data-stu-id="254c6-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="254c6-107">Более сложные сценарии регулирования, в которых используются политики [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey), описаны в статье [Расширенное регулирование запросов с помощью управления API](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="254c6-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="254c6-108"><a name="create-product"> </a>Создание продукта</span><span class="sxs-lookup"><span data-stu-id="254c6-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="254c6-109">На этом шаге создается бесплатная пробная версия продукта, которая не требует утверждения подписки.</span><span class="sxs-lookup"><span data-stu-id="254c6-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="254c6-110">Если вы уже настроили продукт и хотите использовать его в этом руководстве, можно сразу перейти к разделу [Настройка ограничений скорости вызова и политик квот][Configure call rate limit and quota policies] и выполнить указания руководства с этого места, используя вместо бесплатной пробной версии продукта свой продукт.</span><span class="sxs-lookup"><span data-stu-id="254c6-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="254c6-111">Чтобы начать работу, щелкните **Publisher portal** (Портал издателя) на портале Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="254c6-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="254c6-113">Если экземпляр службы управления API еще не создан, выполните инструкции из раздела [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="254c6-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="254c6-114">В меню **Управление API** слева щелкните **Продукты**, чтобы открыть страницу **Продукты**.</span><span class="sxs-lookup"><span data-stu-id="254c6-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![Добавление продукта][api-management-add-product]

<span data-ttu-id="254c6-116">Щелкните **Добавить продукт**, чтобы открыть диалоговое окно **Add new product** (Добавление нового продукта).</span><span class="sxs-lookup"><span data-stu-id="254c6-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![Добавление нового продукта][api-management-new-product-window]

<span data-ttu-id="254c6-118">В поле **Заголовок** введите **Бесплатная пробная версия**.</span><span class="sxs-lookup"><span data-stu-id="254c6-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="254c6-119">В текстовом поле **Описание** введите: **Подписчики смогут выполнять до 10 вызовов в минуту и до 200 вызовов в неделю, после чего доступ будет запрещен.**</span><span class="sxs-lookup"><span data-stu-id="254c6-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="254c6-120">Продукты в службе управления API могут быть защищенными или открытыми.</span><span class="sxs-lookup"><span data-stu-id="254c6-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="254c6-121">Доступ к защищенным продуктам предоставляется по подписке.</span><span class="sxs-lookup"><span data-stu-id="254c6-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="254c6-122">Открытые продукты могут использоваться без подписки.</span><span class="sxs-lookup"><span data-stu-id="254c6-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="254c6-123">Обязательно установите флажок **Require subscription** (Требуется подписка), чтобы создать защищенный продукт, требующий подписки.</span><span class="sxs-lookup"><span data-stu-id="254c6-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="254c6-124">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="254c6-124">This is the default setting.</span></span>

<span data-ttu-id="254c6-125">Установите флажок **Require subscription approval**(Требуется утверждение администратора), чтобы администратор просматривал и утверждал попытки подписки на продукт.</span><span class="sxs-lookup"><span data-stu-id="254c6-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="254c6-126">Если не установить этот флажок, попытки подписки будут утверждаться автоматически.</span><span class="sxs-lookup"><span data-stu-id="254c6-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="254c6-127">В этом примере подписки утверждаются автоматически, поэтому не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="254c6-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="254c6-128">Чтобы разрешить для учетных записей разработчика многократную подписку на новый продукт, установите флажок **Allow multiple simultaneous subscriptions** (Разрешить несколько одновременных подписок).</span><span class="sxs-lookup"><span data-stu-id="254c6-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="254c6-129">В этом руководстве не используются несколько одновременных подписок, поэтому не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="254c6-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="254c6-130">После ввода значений щелкните **Сохранить** для создания продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-130">After all values are entered, click **Save** to create the product.</span></span>

![Продукт создан][api-management-product-added]

<span data-ttu-id="254c6-132">По умолчанию новые продукты могут видеть пользователи группы **Администраторы** .</span><span class="sxs-lookup"><span data-stu-id="254c6-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="254c6-133">Мы добавим группу **Разработчики** .</span><span class="sxs-lookup"><span data-stu-id="254c6-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="254c6-134">Щелкните **Бесплатная пробная версия** и выберите вкладку **Видимость**.</span><span class="sxs-lookup"><span data-stu-id="254c6-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="254c6-135">В службе управления API группы используются для управления видимостью продуктов для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="254c6-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="254c6-136">Продукты предоставляют видимость группам, и разработчики могут просматривать и подписываться на продукты, видимые для групп, к которым они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="254c6-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="254c6-137">Дополнительные сведения см. в статье [Как создавать и использовать группы для управления учетными записями разработчика в службе управления Azure API][How to create and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="254c6-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![Добавление группы разработчиков][api-management-add-developers-group]

<span data-ttu-id="254c6-139">Установите флажок **Разработчики** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="254c6-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="254c6-140"><a name="add-api"> </a>Добавление API к продукту</span><span class="sxs-lookup"><span data-stu-id="254c6-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="254c6-141">На этом шаге руководства Echo API добавится для нового продукта Free Trial.</span><span class="sxs-lookup"><span data-stu-id="254c6-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="254c6-142">Каждый экземпляр службы API Management поставляется предварительно настроенным с Echo API, с которым можно экспериментировать при изучении API Management.</span><span class="sxs-lookup"><span data-stu-id="254c6-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="254c6-143">Дополнительные сведения см. в статье [Начало работы со службой управления Azure API][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="254c6-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="254c6-144">В меню **Управление API** слева щелкните **Продукты** и выберите **Бесплатная пробная версия** для настройки продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Настройка продукта][api-management-configure-product]

<span data-ttu-id="254c6-146">Щелкните **Добавить API к продукту**.</span><span class="sxs-lookup"><span data-stu-id="254c6-146">Click **Add API to product**.</span></span>

![Добавить API к продукту][api-management-add-api]

<span data-ttu-id="254c6-148">Выберите **Echo API**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="254c6-148">Select **Echo API**, and then click **Save**.</span></span>

![Добавление Echo API][api-management-add-echo-api]

## <span data-ttu-id="254c6-150"><a name="policies"> </a>Настройка ограничений скорости вызова и политик квот</span><span class="sxs-lookup"><span data-stu-id="254c6-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="254c6-151">Ограничения скорости и квоты настраиваются в редакторе политик.</span><span class="sxs-lookup"><span data-stu-id="254c6-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="254c6-152">В этом руководстве добавляются две политики: [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) (Ограничение скорости вызова по подписке) и [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) (Установка квоты использования по подписке).</span><span class="sxs-lookup"><span data-stu-id="254c6-152">The two policies we will be adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="254c6-153">Эти политики должны применяться в области продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-153">These policies must be applied at the product scope.</span></span>

<span data-ttu-id="254c6-154">В меню **Управление API** слева щелкните **Политики**.</span><span class="sxs-lookup"><span data-stu-id="254c6-154">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="254c6-155">В списке **Продукт** выберите **Бесплатная пробная версия**.</span><span class="sxs-lookup"><span data-stu-id="254c6-155">In the **Product** list, click **Free Trial**.</span></span>

![Политика продукта][api-management-product-policy]

<span data-ttu-id="254c6-157">Нажмите кнопку **Добавить политику**, чтобы импортировать шаблон политики и начать создание ограничения скорости и политики квот.</span><span class="sxs-lookup"><span data-stu-id="254c6-157">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![Добавить политику][api-management-add-policy]

<span data-ttu-id="254c6-159">Ограничение скорости и политики квот – это входящие политики, поэтому поместите курсор в раздел входящих.</span><span class="sxs-lookup"><span data-stu-id="254c6-159">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![Редактор политики][api-management-policy-editor-inbound]

<span data-ttu-id="254c6-161">Прокрутите список политик и найдите запись политики **Limit call rate per subscription** (Ограничение скорости вызова по подписке).</span><span class="sxs-lookup"><span data-stu-id="254c6-161">Scroll through the list of policies and locate the **Limit call rate per subscription** policy entry.</span></span>

![Правила политики][api-management-limit-policies]

<span data-ttu-id="254c6-163">Поместив курсор в элемент политики **inbound**, щелкните стрелку рядом с политикой **Limit call rate per subscription** (Ограничение скорости вызова по подписке), чтобы вставить шаблон политики.</span><span class="sxs-lookup"><span data-stu-id="254c6-163">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="254c6-164">Как видно во фрагменте, политика позволяет ограничивать число операций и API продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-164">As you can see from the snippet, the policy allows setting limits for the product's APIs and operations.</span></span> <span data-ttu-id="254c6-165">В этом руководстве мы не будем использовать эту возможность, поэтому удалите элементы **api** и **operation** из элемента **rate-limit**, чтобы остался только внешний элемент **rate-limit**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="254c6-165">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **rate-limit** element, such that only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="254c6-166">В бесплатной версии продукта "Бесплатная пробная версия" максимальная разрешенная скорость вызова — 10 вызовов в минуту, поэтому введите **10** в качестве значения атрибута **calls** и **60** в качестве значения атрибута **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="254c6-166">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="254c6-167">Чтобы настроить политику **Set usage quota per subscription** (Установка квоты использования по подписке), поместите курсор под только что добавленным элементом **rate-limit** в элементе **inbound**, а затем найдите и щелкните стрелку слева от политики **Set usage quota per subscription** (Установка квоты использования по подписке).</span><span class="sxs-lookup"><span data-stu-id="254c6-167">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then locate and click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="254c6-168">Аналогично политике **Set usage quota per subscription** (Установка квоты использования по подписке), политика **Limit call rate per subscription** (Ограничение скорости вызова по подписке) позволяет настраивать ограничения для операций и API продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-168">Similarly to the **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on the product's APIs and operations.</span></span> <span data-ttu-id="254c6-169">В этом руководстве мы не будем использовать эту возможность, поэтому удалите элементы **api** и **operation** из элемента **quota**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="254c6-169">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **quota** element, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="254c6-170">Квоты могут основываться на количестве вызовов за интервал, пропускной способности или обоих факторах.</span><span class="sxs-lookup"><span data-stu-id="254c6-170">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="254c6-171">В этом руководстве нет регулировки по пропускной способности, поэтому удалите атрибут **bandwidth** .</span><span class="sxs-lookup"><span data-stu-id="254c6-171">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="254c6-172">Для продукта Free Trial квота составит 200 вызовов в неделю.</span><span class="sxs-lookup"><span data-stu-id="254c6-172">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="254c6-173">Укажите **200** в качестве значения атрибута **calls** и **604800** в качестве значения атрибута **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="254c6-173">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="254c6-174">Интервалы политики указываются в секундах.</span><span class="sxs-lookup"><span data-stu-id="254c6-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="254c6-175">Для вычисления интервала в неделю можно умножить число дней (7) на число часов в дне (24), на число минут в часе (60) и на число секунд в минуте (60): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="254c6-175">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="254c6-176">После окончания настройки политика должна соответствовать следующему примеру.</span><span class="sxs-lookup"><span data-stu-id="254c6-176">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="254c6-177">После настройки желаемой политики нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="254c6-177">After the desired policies are configured, click **Save**.</span></span>

![Сохранение политики][api-management-policy-save]

## <span data-ttu-id="254c6-179"><a name="publish-product"> </a> Публикация продукта</span><span class="sxs-lookup"><span data-stu-id="254c6-179"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="254c6-180">Теперь, когда API добавлены и политики настроены, продукт можно опубликовать, чтобы его могли использовать разработчики.</span><span class="sxs-lookup"><span data-stu-id="254c6-180">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="254c6-181">В меню **Управление API** слева щелкните **Продукты** и выберите **Бесплатная пробная версия** для настройки продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-181">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Настройка продукта][api-management-configure-product]

<span data-ttu-id="254c6-183">Щелкните **Опубликовать**, а затем — **Yes, publish it** (Да, опубликовать) для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="254c6-183">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![Публикация продукта][api-management-publish-product]

## <span data-ttu-id="254c6-185"><a name="subscribe-account"> </a>Подписка учетной записи разработчика на продукт</span><span class="sxs-lookup"><span data-stu-id="254c6-185"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="254c6-186">Теперь продукт опубликован и доступен для подписки и использования разработчиками.</span><span class="sxs-lookup"><span data-stu-id="254c6-186">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="254c6-187">Администраторы экземпляра API Management автоматически подписываются на каждый продукт.</span><span class="sxs-lookup"><span data-stu-id="254c6-187">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="254c6-188">На этом шаге руководства будет проведена подписка одной из учетных записей, не принадлежащей администратору, на бесплатную пробную версию продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-188">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="254c6-189">Если учетная запись разработчика является частью роли "Администраторы", можно выполнить этот шаг, даже если подписка уже оформлена.</span><span class="sxs-lookup"><span data-stu-id="254c6-189">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="254c6-190">В меню **Управление API** слева щелкните **Пользователи** и выберите имя учетной записи разработчика.</span><span class="sxs-lookup"><span data-stu-id="254c6-190">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="254c6-191">В этом примере используется учетная запись **Clayton Gragg** .</span><span class="sxs-lookup"><span data-stu-id="254c6-191">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![Настройка разработчика][api-management-configure-developer]

<span data-ttu-id="254c6-193">Нажмите кнопку **Добавить подписку**.</span><span class="sxs-lookup"><span data-stu-id="254c6-193">Click **Add Subscription**.</span></span>

![Добавить подписку][api-management-add-subscription-menu]

<span data-ttu-id="254c6-195">Выберите **Бесплатная пробная версия**, а затем нажмите кнопку **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="254c6-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Добавить подписку][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="254c6-197">В этом руководстве для бесплатной пробной версии продукта не включаются несколько одновременных подписок.</span><span class="sxs-lookup"><span data-stu-id="254c6-197">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="254c6-198">Если бы они включались, вам было бы предложено назвать подписку, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="254c6-198">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![Добавить подписку][api-management-add-subscription-multiple]

<span data-ttu-id="254c6-200">После нажатия кнопки **Подписаться** продукт появится в списке **Подписки**.</span><span class="sxs-lookup"><span data-stu-id="254c6-200">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![Подписка добавлена][api-management-subscription-added]

## <span data-ttu-id="254c6-202"><a name="test-rate-limit"> </a>Вызов операции и тестирование ограничения скорости</span><span class="sxs-lookup"><span data-stu-id="254c6-202"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="254c6-203">Теперь, когда продукт Free Trial настроен и опубликован, можно вызвать некоторые операции и протестировать политику ограничения скорости.</span><span class="sxs-lookup"><span data-stu-id="254c6-203">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="254c6-204">Перейдите на портал разработчика, щелкнув **Портал разработчика** в меню вверху справа.</span><span class="sxs-lookup"><span data-stu-id="254c6-204">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="254c6-206">Щелкните **API** в верхнем меню, а затем выберите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="254c6-206">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![Портал разработчика][api-management-developer-portal-api-menu]

<span data-ttu-id="254c6-208">Щелкните **GET Resource** (Ресурс GET), а затем нажмите кнопку **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="254c6-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Открытие консоли][api-management-open-console]

<span data-ttu-id="254c6-210">Сохраните значения по умолчанию и выберите ключ подписки для бесплатной пробной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="254c6-210">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![Ключ подписки][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="254c6-212">Если у вас несколько подписок, убедитесь, что выбран ключ для **бесплатной пробной версии**, иначе политики, настроенные на предыдущем шаге, не смогут вступить в силу.</span><span class="sxs-lookup"><span data-stu-id="254c6-212">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="254c6-213">Щелкните **Отправить**, а затем просмотрите ответ.</span><span class="sxs-lookup"><span data-stu-id="254c6-213">Click **Send**, and then view the response.</span></span> <span data-ttu-id="254c6-214">Обратите внимание, что для **состояния ответа** отображается значение **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="254c6-214">Note the **Response status** of **200 OK**.</span></span>

![Результаты операции][api-management-http-get-results]

<span data-ttu-id="254c6-216">Щелкайте **Отправить** со скоростью, превышающей ограничение скорости политики в 10 вызовов в минуту.</span><span class="sxs-lookup"><span data-stu-id="254c6-216">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="254c6-217">Как только ограничение скорости политики будет превышено, возвращается ответ **429 – Слишком много запросов** .</span><span class="sxs-lookup"><span data-stu-id="254c6-217">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Результаты операции][api-management-http-get-429]

<span data-ttu-id="254c6-219">**Содержимое ответа** указывает оставшийся интервал, после которого повторы будут успешными.</span><span class="sxs-lookup"><span data-stu-id="254c6-219">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="254c6-220">При действующей политике ограничения скорости в 10 вызовов в минуту дальнейшие вызовы будут неудачными, пока не пройдет 60 секунд после первых 10 успешных вызовов продукта, после которых ограничение скорости было превышено.</span><span class="sxs-lookup"><span data-stu-id="254c6-220">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="254c6-221">В этом примере оставшийся интервал составляет 54 секунды.</span><span class="sxs-lookup"><span data-stu-id="254c6-221">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="254c6-222"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="254c6-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="254c6-223">Демонстрацию настройки ограничений скорости и квот см. в следующем видео.</span><span class="sxs-lookup"><span data-stu-id="254c6-223">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
