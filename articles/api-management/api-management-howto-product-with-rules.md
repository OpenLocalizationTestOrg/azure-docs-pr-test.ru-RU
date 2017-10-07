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
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Защита API путем ограничения скорости с помощью управления API Azure
В этом руководстве показано, как просто можно tooadd защиту для API внутреннего сервера, настроив политики и ограничения скорости со службой управления API Azure.

В этом учебнике вы создадите продукт «Бесплатной пробной версии» API-Интерфейс, который позволяет разработчикам toomake too10 вызовов в минуту и копирование максимум 200 вызовов в API tooyour неделю, с помощью hello tooa [ограничение частоты вызовов для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) и [ Задание квоты использования для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) политики. Затем опубликуйте hello API и тестирования политики ограничения скорости hello.

Более сложные сценарии, использующие hello регулирования [скорость ограничение по ключ](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [ключ квоты](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) политики, см. [расширенный запрос регулирования со службой управления API Azure](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate продукта
На этом шаге создается бесплатная пробная версия продукта, которая не требует утверждения подписки.

> [!NOTE]
> Если вы уже настроен продукта и toouse его в этом учебнике, можно перейти вперед слишком[Настройка политики и ограничения частоты вызовов] [ Configure call rate limit and quota policies] и следуйте инструкциям учебника hello оттуда с использованием продукта Вместо hello бесплатной пробной версии продукта.
> 
> 

tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.

![Портал издателя][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [управление первый API в Azure API Management] [ Manage your first API in Azure API Management] учебника.
> 
> 

Нажмите кнопку **продуктов** в hello **API управления** меню hello hello левой toodisplay **продуктов** страницы.

![Добавление продукта][api-management-add-product]

Нажмите кнопку **установка продукта** toodisplay hello **добавить новый продукт** диалоговое окно.

![Добавление нового продукта][api-management-new-product-window]

В hello **заголовок** введите **бесплатной пробной версии**.

В hello **описание** поле, тип hello следующий текст: **подписчики будут может toorun 10 вызовов в минуту вверх tooa более 200 вызовов в неделю после которого отказано в доступе.**

Продукты в службе управления API могут быть защищенными или открытыми. Защищенные продуктов должен быть подписанным toobefore может использоваться. Открытые продукты могут использоваться без подписки. Убедитесь, что **требует подписки** является выбранного toocreate защищенных продукт, который требует наличия подписки. Это параметр по умолчанию hello.

Если требуется tooreview администратора и принять или отклонить подписки пытается toothis продукта, установите **утверждение подписки**. Если снят флажок "hello", подписки попыток будет автоматически выполнено. В этом примере автоматически утверждаются подписок, поэтому не устанавливайте флажок hello.

Разработчик tooallow учетные записи toosubscribe несколько раз toohello новым продуктом, выберите hello **разрешить несколько одновременных подписок** флажок. В этом руководстве не используются несколько одновременных подписок, поэтому не устанавливайте этот флажок.

После ввода всех значений щелкните **Сохранить** toocreate hello продукта.

![Продукт создан][api-management-product-added]

По умолчанию новые продукты являются видимыми toousers в hello **Администраторы** группы. Мы будем tooadd hello **разработчики** группы. Нажмите кнопку **бесплатной пробной версии**, а затем нажмите кнопку hello **видимость** вкладки.

> В службе управления API группы — видимость hello используется toomanage toodevelopers продуктов. Видимость toogroups предоставления продуктов и разработчики могут просматривать и подписываться toohello продуктов, которые являются видимыми toohello групп, в которых они принадлежат. Дополнительные сведения см. в разделе [сопоставление toocreate и использования групп в службе управления API Azure][How toocreate and use groups in Azure API Management].
> 
> 

![Добавление группы разработчиков][api-management-add-developers-group]

Выберите hello **разработчики** флажок и нажмите кнопку **Сохранить**.

## <a name="add-api"></a>tooadd API toohello продукта
На этом шаге учебника hello мы добавим hello Echo API toohello нового бесплатной пробной версии продукта.

> Каждый экземпляр службы управления API поставляется в предварительно настроенную Echo API, который можно использовать tooexperiment с и Дополнительные сведения о службе управления API. Дополнительные сведения см. в статье [Начало работы со службой управления Azure API][Manage your first API in Azure API Management].
> 
> 

Нажмите кнопку **продуктов** из hello **API управления** меню hello слева, а затем нажмите **бесплатной пробной версии** tooconfigure hello продукта.

![Настройка продукта][api-management-configure-product]

Нажмите кнопку **tooproduct добавить API**.

![Добавить API tooproduct][api-management-add-api]

Выберите **Echo API**, а затем нажмите кнопку **Сохранить**.

![Добавление Echo API][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure политики и ограничения частоты вызовов
Пределы скорости и квот, настраиваются в редактор политики hello. Hello двух политики, будут добавлены в этом учебнике это hello [ограничение частоты вызовов для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) и [задание квоты использования для каждой подписки](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) политики. Эти политики, применимые в области продукта hello.

Нажмите кнопку **политики** под hello **управления API** меню слева hello. В hello **продукта** выберите **бесплатной пробной версии**.

![Политика продукта][api-management-product-policy]

Нажмите кнопку **добавить политику** tooimport hello шаблон политики и приступить к созданию hello политики и ограничения скорости.

![добавление политики;][api-management-add-policy]

Скорость и ограничения являются входящих политиками, так курсора hello позиции в элементе входящих hello.

![Редактор политики][api-management-policy-editor-inbound]

Прокрутите список политик hello и найдите hello **ограничение частоты вызовов для каждой подписки** запись политики.

![Правила политики][api-management-limit-policies]

После hello курсор помещается в hello **входящий** элемента политики, нажмите кнопку со стрелкой hello рядом с **ограничение частоты вызовов для каждой подписки** tooinsert его шаблон политики.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Как видно из фрагмента hello hello политика позволяет ограничение операций и API hello продукта. В этом учебнике мы не будет использовать эту возможность, поэтому удалите hello **api** и **операции** элементы из hello **ограничение скорости** элементом, таким образом, что только hello внешнего **ограничение скорости** элемент остается, как показано в следующий пример hello.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

Hello бесплатной пробной версии продукта, hello максимальный допустимый вызов долю 10 вызовов в минуту, поэтому введите **10** как значение hello для hello **вызовы** атрибут, и **60** для hello **период обновления** атрибута.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

tooconfigure hello **задание квоты использования для каждой подписки** политики, позиция курсора сразу под hello новых добавленных **ограничение скорости** элемент в пределах hello **входящего** элемент, найдите и щелкните hello стрелка влево toohello из **задание квоты использования для каждой подписки**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Аналогичным образом toohello **задание квоты использования для каждой подписки** политики, **задание квоты использования для каждой подписки** политики позволяет настроить прописные для на API и операции hello продукта. В этом учебнике мы не будет использовать эту возможность, поэтому удалите hello **api** и **операции** элементы из hello **квоты** элемента, как показано в следующий пример hello.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Квоты могут основываться на hello количество вызовов на интервал, пропускную способность или оба. В этом учебнике мы не регулирование полосы пропускания на основе, поэтому удалите hello **пропускной способности** атрибута.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Hello бесплатной пробной версии продукта hello Квота составляет 200 вызовов в неделю. Укажите **200** как значение hello для hello **вызовы** атрибута, а затем укажите **604800** как значение hello для hello **период обновления** атрибут.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Интервалы политики указываются в секундах. Интервал приветствия toocalculate за неделю, умножьте hello количество дней (7) hello число часов в день (24) hello число минут в течение часа (60) hello число секунд в минуту (60): 7 * 24 * 60 * 60 = 604800.
> 
> 

После завершения настройки политики hello, он должен соответствовать hello в следующем примере.

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

После hello необходимых политик, нажмите кнопку **Сохранить**.

![Сохранение политики][api-management-policy-save]

## <a name="publish-product"></a> toopublish hello продукта
Теперь, когда hello hello API-интерфейсы добавляются и политик hello, hello продукта должен быть опубликован, чтобы он может использоваться разработчиками. Нажмите кнопку **продуктов** из hello **API управления** меню hello слева, а затем нажмите **бесплатной пробной версии** tooconfigure hello продукта.

![Настройка продукта][api-management-configure-product]

Нажмите кнопку **публикации**, а затем нажмите кнопку **Да, опубликуйте его** tooconfirm.

![Публикация продукта][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe продукт toohello учетную запись разработчика
После публикации продукта hello это tooand доступных toobe подписка используется разработчиками.

> Администраторы управления API экземпляра являются автоматически подписанных tooevery продукта. На этом шаге учебника будет подписаться один hello разработчика без прав администратора учетных записей toohello бесплатной пробной версии продукта. Если учетной записи разработчика является частью роли "Администраторы" hello, после этого можно выполнить вместе с этот шаг, несмотря на то, что вы уже подписаны.
> 
> 

Нажмите кнопку **пользователей** на hello **управления API** меню hello слева, затем щелкните имя учетной записи разработчика hello. В этом примере мы используем hello **Gragg Бежина** учетную запись разработчика.

![Настройка разработчика][api-management-configure-developer]

Нажмите кнопку **Добавить подписку**.

![Добавить подписку][api-management-add-subscription-menu]

Выберите **Бесплатная пробная версия**, а затем нажмите кнопку **Подписаться**.

![Добавить подписку][api-management-add-subscription]

> [!NOTE]
> В этом учебнике несколько одновременных подписок не включены для hello бесплатной пробной версии продукта. Если бы они были будет запрашиваемые tooname hello подписки, как показано в следующий пример hello.
> 
> 

![Добавить подписку][api-management-add-subscription-multiple]

После нажатия кнопки **Subscribe**, продукт hello появляется в hello **подписки** списка для пользователя hello.

![Подписка добавлена][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall операции и тестирование предела скорости hello
Hello бесплатной пробной версии продукта настройки и публикации, мы вызов некоторых операций и проверить политику ограничение скорости hello.
Портал разработчиков toohello коммутатора, щелкнув **портал разработчиков** в правом верхнем меню hello.

![Портал разработчика][api-management-developer-portal-menu]

Нажмите кнопку **API-интерфейсы** в верхнем меню hello и нажмите кнопку **Echo API**.

![Портал разработчика][api-management-developer-portal-api-menu]

Щелкните **GET Resource** (Ресурс GET), а затем нажмите кнопку **Попробовать**.

![Открытие консоли][api-management-open-console]

Оставьте значения параметров по умолчанию hello, а затем выберите ключ подписки для hello бесплатной пробной версии продукта.

![Ключ подписки][api-management-select-key]

> [!NOTE]
> Если у вас несколько подписок, быть убедиться, что ключ hello tooselect для **бесплатной пробной версии**, или else hello политики, которые были настроены в предыдущих шагах hello не будет действовать.
> 
> 

Нажмите кнопку **отправки**и просмотрите hello ответа. Примечание hello **состояние ответа** из **200 ОК**.

![Результаты операции][api-management-http-get-results]

Нажмите кнопку **отправки** быстрее, чем политика ограничение скорости hello 10 вызовов в минуту. После превышения политики ограничения скорости hello состояние ответа для **429 слишком много запросов** возвращается.

![Результаты операции][api-management-http-get-429]

Hello **содержимого отклика** указывает hello оставшихся интервал повторных попыток будет успешной.

Если действует политика ограничение скорости hello 10 вызовов в минуту, последующие вызовы завершатся ошибкой до 60 секунд, прошедших с hello первый hello 10 успешных вызовов toohello прежде, чем было превышено ограничение частоты hello продукта. В этом примере hello оставшихся интервал — 54 секунды.

## <a name="next-steps"> </a>Дальнейшие действия
* Просмотрите демонстрационную версию Задание пределов скорости и квот в hello следующие видео.

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
