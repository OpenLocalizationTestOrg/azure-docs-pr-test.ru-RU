---
title: "aaaProtect API управления API Azure | Документы Microsoft"
description: "Узнайте, как tooprotect API с помощью квот и регулирования (ограничение скорости) политики."
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
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="03d54-103">Защита API путем ограничения скорости с помощью управления API Azure</span><span class="sxs-lookup"><span data-stu-id="03d54-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="03d54-104">В этом руководстве показано, как просто можно tooadd защиту для API внутреннего сервера, настроив политики и ограничения скорости со службой управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="03d54-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="03d54-105">В этом учебнике вы создадите продукт «Бесплатной пробной версии» API-Интерфейс, который позволяет разработчикам toomake too10 вызовов в минуту и копирование максимум 200 вызовов в API tooyour неделю, с помощью hello tooa [ограничение частоты вызовов для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) и [ Задание квоты использования для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) политики.</span><span class="sxs-lookup"><span data-stu-id="03d54-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="03d54-106">Затем опубликуйте hello API и тестирования политики ограничения скорости hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="03d54-107">Более сложные сценарии, использующие hello регулирования [скорость ограничение по ключ](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [ключ квоты](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) политики, см. [расширенный запрос регулирования со службой управления API Azure](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="03d54-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="03d54-108"><a name="create-product"></a>toocreate продукта</span><span class="sxs-lookup"><span data-stu-id="03d54-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="03d54-109">На этом шаге создается бесплатная пробная версия продукта, которая не требует утверждения подписки.</span><span class="sxs-lookup"><span data-stu-id="03d54-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="03d54-110">Если вы уже настроен продукта и toouse его в этом учебнике, можно перейти вперед слишком[Настройка политики и ограничения частоты вызовов] [ Configure call rate limit and quota policies] и следуйте инструкциям учебника hello оттуда с использованием продукта Вместо hello бесплатной пробной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="03d54-111">tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="03d54-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="03d54-113">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [управление первый API в Azure API Management] [ Manage your first API in Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="03d54-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="03d54-114">Нажмите кнопку **продуктов** в hello **API управления** меню hello hello левой toodisplay **продуктов** страницы.</span><span class="sxs-lookup"><span data-stu-id="03d54-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Добавление продукта][api-management-add-product]

<span data-ttu-id="03d54-116">Нажмите кнопку **установка продукта** toodisplay hello **добавить новый продукт** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="03d54-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Добавление нового продукта][api-management-new-product-window]

<span data-ttu-id="03d54-118">В hello **заголовок** введите **бесплатной пробной версии**.</span><span class="sxs-lookup"><span data-stu-id="03d54-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="03d54-119">В hello **описание** поле, тип hello следующий текст: **подписчики будут может toorun 10 вызовов в минуту вверх tooa более 200 вызовов в неделю после которого отказано в доступе.**</span><span class="sxs-lookup"><span data-stu-id="03d54-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="03d54-120">Продукты в службе управления API могут быть защищенными или открытыми.</span><span class="sxs-lookup"><span data-stu-id="03d54-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="03d54-121">Защищенные продуктов должен быть подписанным toobefore может использоваться.</span><span class="sxs-lookup"><span data-stu-id="03d54-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="03d54-122">Открытые продукты могут использоваться без подписки.</span><span class="sxs-lookup"><span data-stu-id="03d54-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="03d54-123">Убедитесь, что **требует подписки** является выбранного toocreate защищенных продукт, который требует наличия подписки.</span><span class="sxs-lookup"><span data-stu-id="03d54-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="03d54-124">Это параметр по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-124">This is hello default setting.</span></span>

<span data-ttu-id="03d54-125">Если требуется tooreview администратора и принять или отклонить подписки пытается toothis продукта, установите **утверждение подписки**.</span><span class="sxs-lookup"><span data-stu-id="03d54-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="03d54-126">Если снят флажок "hello", подписки попыток будет автоматически выполнено.</span><span class="sxs-lookup"><span data-stu-id="03d54-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="03d54-127">В этом примере автоматически утверждаются подписок, поэтому не устанавливайте флажок hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="03d54-128">Разработчик tooallow учетные записи toosubscribe несколько раз toohello новым продуктом, выберите hello **разрешить несколько одновременных подписок** флажок.</span><span class="sxs-lookup"><span data-stu-id="03d54-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="03d54-129">В этом руководстве не используются несколько одновременных подписок, поэтому не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="03d54-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="03d54-130">После ввода всех значений щелкните **Сохранить** toocreate hello продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Продукт создан][api-management-product-added]

<span data-ttu-id="03d54-132">По умолчанию новые продукты являются видимыми toousers в hello **Администраторы** группы.</span><span class="sxs-lookup"><span data-stu-id="03d54-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="03d54-133">Мы будем tooadd hello **разработчики** группы.</span><span class="sxs-lookup"><span data-stu-id="03d54-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="03d54-134">Нажмите кнопку **бесплатной пробной версии**, а затем нажмите кнопку hello **видимость** вкладки.</span><span class="sxs-lookup"><span data-stu-id="03d54-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="03d54-135">В службе управления API группы — видимость hello используется toomanage toodevelopers продуктов.</span><span class="sxs-lookup"><span data-stu-id="03d54-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="03d54-136">Видимость toogroups предоставления продуктов и разработчики могут просматривать и подписываться toohello продуктов, которые являются видимыми toohello групп, в которых они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="03d54-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="03d54-137">Дополнительные сведения см. в разделе [сопоставление toocreate и использования групп в службе управления API Azure][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="03d54-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Добавление группы разработчиков][api-management-add-developers-group]

<span data-ttu-id="03d54-139">Выберите hello **разработчики** флажок и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03d54-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="03d54-140"><a name="add-api"></a>tooadd API toohello продукта</span><span class="sxs-lookup"><span data-stu-id="03d54-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="03d54-141">На этом шаге учебника hello мы добавим hello Echo API toohello нового бесплатной пробной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="03d54-142">Каждый экземпляр службы управления API поставляется в предварительно настроенную Echo API, который можно использовать tooexperiment с и Дополнительные сведения о службе управления API.</span><span class="sxs-lookup"><span data-stu-id="03d54-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="03d54-143">Дополнительные сведения см. в статье [Начало работы со службой управления Azure API][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="03d54-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="03d54-144">Нажмите кнопку **продуктов** из hello **API управления** меню hello слева, а затем нажмите **бесплатной пробной версии** tooconfigure hello продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Настройка продукта][api-management-configure-product]

<span data-ttu-id="03d54-146">Нажмите кнопку **tooproduct добавить API**.</span><span class="sxs-lookup"><span data-stu-id="03d54-146">Click **Add API tooproduct**.</span></span>

![Добавить API tooproduct][api-management-add-api]

<span data-ttu-id="03d54-148">Выберите **Echo API**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03d54-148">Select **Echo API**, and then click **Save**.</span></span>

![Добавление Echo API][api-management-add-echo-api]

## <span data-ttu-id="03d54-150"><a name="policies"></a>tooconfigure политики и ограничения частоты вызовов</span><span class="sxs-lookup"><span data-stu-id="03d54-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="03d54-151">Пределы скорости и квот, настраиваются в редактор политики hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="03d54-152">Hello двух политики, будут добавлены в этом учебнике это hello [ограничение частоты вызовов для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) и [задание квоты использования для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) политики.</span><span class="sxs-lookup"><span data-stu-id="03d54-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="03d54-153">Эти политики, применимые в области продукта hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="03d54-154">Нажмите кнопку **политики** под hello **управления API** меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="03d54-155">В hello **продукта** выберите **бесплатной пробной версии**.</span><span class="sxs-lookup"><span data-stu-id="03d54-155">In hello **Product** list, click **Free Trial**.</span></span>

![Политика продукта][api-management-product-policy]

<span data-ttu-id="03d54-157">Нажмите кнопку **добавить политику** tooimport hello шаблон политики и приступить к созданию hello политики и ограничения скорости.</span><span class="sxs-lookup"><span data-stu-id="03d54-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![добавление политики;][api-management-add-policy]

<span data-ttu-id="03d54-159">Скорость и ограничения являются входящих политиками, так курсора hello позиции в элементе входящих hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Редактор политики][api-management-policy-editor-inbound]

<span data-ttu-id="03d54-161">Прокрутите список политик hello и найдите hello **ограничение частоты вызовов для каждой подписки** запись политики.</span><span class="sxs-lookup"><span data-stu-id="03d54-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Правила политики][api-management-limit-policies]

<span data-ttu-id="03d54-163">После hello курсор помещается в hello **входящий** элемента политики, нажмите кнопку со стрелкой hello рядом с **ограничение частоты вызовов для каждой подписки** tooinsert его шаблон политики.</span><span class="sxs-lookup"><span data-stu-id="03d54-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="03d54-164">Как видно из фрагмента hello hello политика позволяет ограничение операций и API hello продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="03d54-165">В этом учебнике мы не будет использовать эту возможность, поэтому удалите hello **api** и **операции** элементы из hello **ограничение скорости** элементом, таким образом, что только hello внешнего **ограничение скорости** элемент остается, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="03d54-166">Hello бесплатной пробной версии продукта, hello максимальный допустимый вызов долю 10 вызовов в минуту, поэтому введите **10** как значение hello для hello **вызовы** атрибут, и **60** для hello **период обновления** атрибута.</span><span class="sxs-lookup"><span data-stu-id="03d54-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="03d54-167">tooconfigure hello **задание квоты использования для каждой подписки** политики, позиция курсора сразу под hello новых добавленных **ограничение скорости** элемент в пределах hello **входящего** элемент, найдите и щелкните hello стрелка влево toohello из **задание квоты использования для каждой подписки**.</span><span class="sxs-lookup"><span data-stu-id="03d54-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="03d54-168">Аналогичным образом toohello **задание квоты использования для каждой подписки** политики, **задание квоты использования для каждой подписки** политики позволяет настроить прописные для на API и операции hello продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="03d54-169">В этом учебнике мы не будет использовать эту возможность, поэтому удалите hello **api** и **операции** элементы из hello **квоты** элемента, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="03d54-170">Квоты могут основываться на hello количество вызовов на интервал, пропускную способность или оба.</span><span class="sxs-lookup"><span data-stu-id="03d54-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="03d54-171">В этом учебнике мы не регулирование полосы пропускания на основе, поэтому удалите hello **пропускной способности** атрибута.</span><span class="sxs-lookup"><span data-stu-id="03d54-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="03d54-172">Hello бесплатной пробной версии продукта hello Квота составляет 200 вызовов в неделю.</span><span class="sxs-lookup"><span data-stu-id="03d54-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="03d54-173">Укажите **200** как значение hello для hello **вызовы** атрибута, а затем укажите **604800** как значение hello для hello **период обновления** атрибут.</span><span class="sxs-lookup"><span data-stu-id="03d54-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="03d54-174">Интервалы политики указываются в секундах.</span><span class="sxs-lookup"><span data-stu-id="03d54-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="03d54-175">Интервал приветствия toocalculate за неделю, умножьте hello количество дней (7) hello число часов в день (24) hello число минут в течение часа (60) hello число секунд в минуту (60): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="03d54-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="03d54-176">После завершения настройки политики hello, он должен соответствовать hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="03d54-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

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

<span data-ttu-id="03d54-177">После hello необходимых политик, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03d54-177">After hello desired policies are configured, click **Save**.</span></span>

![Сохранение политики][api-management-policy-save]

## <span data-ttu-id="03d54-179"><a name="publish-product"></a> toopublish hello продукта</span><span class="sxs-lookup"><span data-stu-id="03d54-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="03d54-180">Теперь, когда hello hello API-интерфейсы добавляются и политик hello, hello продукта должен быть опубликован, чтобы он может использоваться разработчиками.</span><span class="sxs-lookup"><span data-stu-id="03d54-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="03d54-181">Нажмите кнопку **продуктов** из hello **API управления** меню hello слева, а затем нажмите **бесплатной пробной версии** tooconfigure hello продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Настройка продукта][api-management-configure-product]

<span data-ttu-id="03d54-183">Нажмите кнопку **публикации**, а затем нажмите кнопку **Да, опубликуйте его** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="03d54-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Публикация продукта][api-management-publish-product]

## <span data-ttu-id="03d54-185"><a name="subscribe-account"></a>toosubscribe продукт toohello учетную запись разработчика</span><span class="sxs-lookup"><span data-stu-id="03d54-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="03d54-186">После публикации продукта hello это tooand доступных toobe подписка используется разработчиками.</span><span class="sxs-lookup"><span data-stu-id="03d54-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="03d54-187">Администраторы управления API экземпляра являются автоматически подписанных tooevery продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="03d54-188">На этом шаге учебника будет подписаться один hello разработчика без прав администратора учетных записей toohello бесплатной пробной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="03d54-189">Если учетной записи разработчика является частью роли "Администраторы" hello, после этого можно выполнить вместе с этот шаг, несмотря на то, что вы уже подписаны.</span><span class="sxs-lookup"><span data-stu-id="03d54-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="03d54-190">Нажмите кнопку **пользователей** на hello **управления API** меню hello слева, затем щелкните имя учетной записи разработчика hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="03d54-191">В этом примере мы используем hello **Gragg Бежина** учетную запись разработчика.</span><span class="sxs-lookup"><span data-stu-id="03d54-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Настройка разработчика][api-management-configure-developer]

<span data-ttu-id="03d54-193">Нажмите кнопку **Добавить подписку**.</span><span class="sxs-lookup"><span data-stu-id="03d54-193">Click **Add Subscription**.</span></span>

![Добавить подписку][api-management-add-subscription-menu]

<span data-ttu-id="03d54-195">Выберите **Бесплатная пробная версия**, а затем нажмите кнопку **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="03d54-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Добавить подписку][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="03d54-197">В этом учебнике несколько одновременных подписок не включены для hello бесплатной пробной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="03d54-198">Если бы они были будет запрашиваемые tooname hello подписки, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Добавить подписку][api-management-add-subscription-multiple]

<span data-ttu-id="03d54-200">После нажатия кнопки **Subscribe**, продукт hello появляется в hello **подписки** списка для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Подписка добавлена][api-management-subscription-added]

## <span data-ttu-id="03d54-202"><a name="test-rate-limit"></a>toocall операции и тестирование предела скорости hello</span><span class="sxs-lookup"><span data-stu-id="03d54-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="03d54-203">Hello бесплатной пробной версии продукта настройки и публикации, мы вызов некоторых операций и проверить политику ограничение скорости hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="03d54-204">Портал разработчиков toohello коммутатора, щелкнув **портал разработчиков** в правом верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="03d54-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="03d54-206">Нажмите кнопку **API-интерфейсы** в верхнем меню hello и нажмите кнопку **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="03d54-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![Портал разработчика][api-management-developer-portal-api-menu]

<span data-ttu-id="03d54-208">Щелкните **GET Resource** (Ресурс GET), а затем нажмите кнопку **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="03d54-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Открытие консоли][api-management-open-console]

<span data-ttu-id="03d54-210">Оставьте значения параметров по умолчанию hello, а затем выберите ключ подписки для hello бесплатной пробной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Ключ подписки][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="03d54-212">Если у вас несколько подписок, быть убедиться, что ключ hello tooselect для **бесплатной пробной версии**, или else hello политики, которые были настроены в предыдущих шагах hello не будет действовать.</span><span class="sxs-lookup"><span data-stu-id="03d54-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="03d54-213">Нажмите кнопку **отправки**и просмотрите hello ответа.</span><span class="sxs-lookup"><span data-stu-id="03d54-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="03d54-214">Примечание hello **состояние ответа** из **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="03d54-214">Note hello **Response status** of **200 OK**.</span></span>

![Результаты операции][api-management-http-get-results]

<span data-ttu-id="03d54-216">Нажмите кнопку **отправки** быстрее, чем политика ограничение скорости hello 10 вызовов в минуту.</span><span class="sxs-lookup"><span data-stu-id="03d54-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="03d54-217">После превышения политики ограничения скорости hello состояние ответа для **429 слишком много запросов** возвращается.</span><span class="sxs-lookup"><span data-stu-id="03d54-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Результаты операции][api-management-http-get-429]

<span data-ttu-id="03d54-219">Hello **содержимого отклика** указывает hello оставшихся интервал повторных попыток будет успешной.</span><span class="sxs-lookup"><span data-stu-id="03d54-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="03d54-220">Если действует политика ограничение скорости hello 10 вызовов в минуту, последующие вызовы завершатся ошибкой до 60 секунд, прошедших с hello первый hello 10 успешных вызовов toohello прежде, чем было превышено ограничение частоты hello продукта.</span><span class="sxs-lookup"><span data-stu-id="03d54-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="03d54-221">В этом примере hello оставшихся интервал — 54 секунды.</span><span class="sxs-lookup"><span data-stu-id="03d54-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="03d54-222"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03d54-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="03d54-223">Просмотрите демонстрационную версию Задание пределов скорости и квот в hello следующие видео.</span><span class="sxs-lookup"><span data-stu-id="03d54-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
