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
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Как toocreate и публикация продукта в службе управления API Azure
В службе управления API Azure продукт содержит один или несколько интерфейсов API, а также использование квот и hello условия использования. После публикации продукта разработчики могут подписаться toohello продукта и начать toouse hello его интерфейсы API. раздел Hello содержит toocreating руководство по продукции, добавление API и публикации для разработчиков.

## <a name="create-product"> </a>Создание продукта
Операции являются добавляется и настраивается tooan API hello портала издателя. tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.

![Портал издателя][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Щелкните **продуктов** выберите в меню слева toodisplay hello hello hello **продуктов** и нажмите кнопку **добавить продукт**.

![Продукты][api-management-products]

![Новый продукт][api-management-add-new-product]

Введите описательное имя для продукта hello в hello **имя** и описание продукта hello в hello **описание** поля.

Продукты в службе управления API могут быть **открытыми** или **защищенными**. Защищенные продуктов должен быть подписанным toobefore, они могут использоваться, во время открытия продуктов может быть использован без подписки. Проверьте **требует подписки** toocreate защищенных продукт, который требует наличия подписки. Это параметр по умолчанию hello.

Проверьте **утверждение подписки** при необходимости tooreview администратора и принять или отклонить подписки пытается toothis продукта. Если hello флажок не установлен, попыток подписка будет автоматически выполнено. Дополнительные сведения о подписках см. в разделе [tooa подписчиков просмотр продукта][View subscribers tooa product].

toosubscribe учетных записей tooallow разработчиков продукта toohello несколько раз, проверьте hello **допускать несколько подписок** флажок. Если этот флажок не установлен, каждой учетной записи разработчика можно подписаться только один раз toohello продукта.

![Неограниченное количество подписок][api-management-unlimited-multiple-subscriptions]

число hello toolimit несколько одновременных подписок, проверьте hello **максимальное число одновременных подписок** флажок и введите лимит подписки hello. В следующем примере hello одновременных подписки, ограниченный toofour на учетную запись разработчика.

![Четыре подписки][api-management-four-multiple-subscriptions]

После настройки все новые параметры продукта щелкните **Сохранить** toocreate hello нового продукта.

![Продукты][api-management-products-page]

> По умолчанию еще не опубликованы новые продукты и являются видимыми только toohello **Администраторы** группы.
> 
> 

tooconfigure продукта, щелкните имя продукта hello в hello **продуктов** вкладки.

## <a name="add-apis"></a>Добавить API-интерфейсы tooa продукта
Hello **продуктов** страница содержит четыре ссылки для конфигурации: **Сводка**, **параметры**, **видимость**, и  **Подписчики**. Hello **Сводка** вкладка, где можно добавить API-интерфейсов и опубликовать или отменить публикацию продукта.

![Сводка][api-management-new-product-summary]

Перед публикацией продукта необходимо tooadd один или несколько интерфейсов API. toodo, нажмите кнопку **tooproduct добавить API**.

![Добавление интерфейсов API][api-management-add-apis-to-product]

Выберите hello требуемого API-интерфейсы и нажмите кнопку **Сохранить**.

## <a name="add-description"></a>Добавить описательную информацию tooa продукта
Hello **параметры** вкладке можно tooprovide подробные сведения о продукте hello, такие как его назначение, hello он обеспечивает доступ к API-интерфейсы и другие полезные сведения. содержимое Hello ориентирована на разработчиков hello, вызова hello API и могут записываться в обычный текст или HTML-разметка.

![Параметры продукта][api-management-product-settings]

Проверьте **требует подписки** toocreate защищенных продукт, который требует toobe подписки используется или очистить hello toocreate флажок Открыть продукта, который может вызываться без подписки.

Выберите **утверждение подписки** Если требуется toomanually утвердить все запросы подписки продукта. По умолчанию все подписки на продукт предоставляются автоматически.

toosubscribe учетных записей tooallow разработчиков продукта toohello несколько раз, проверьте hello **допускать несколько подписок** флажок и при необходимости укажите ограничение. Если этот флажок не установлен, каждой учетной записи разработчика можно подписаться только один раз toohello продукта.

При необходимости заполните hello **условия использования** поле, описывающее hello условия использования для hello продукта, который необходимо принять подписчиков в порядке toouse hello продукта.

## <a name="publish-product"> </a>Публикация продукта
Перед вызовом hello интерфейсы API в продукте hello продукта должен быть опубликован. На hello **Сводка** hello продукта, нажмите кнопку **публикации**, а затем нажмите кнопку **Да, опубликуйте его** tooconfirm. Щелкните toomake закрытый ранее опубликованные продукта, **отменить публикацию**.

![Публикация продукта][api-management-publish-product]

## <a name="make-visible"></a>Сделать видимым toodevelopers продукта
Hello **видимость** вкладке можно toochoose, какие роли могут toosee hello продукта на портал разработчиков hello и подписываться toohello продукта.

![Видимость продукта][api-management-product-visiblity]

tooenable или отключить видимость продукта для разработчиков hello в группе, установите или снимите флажок hello рядом с hello группы и нажмите кнопку **Сохранить**.

> Дополнительные сведения см. в разделе [как разработчик toomanage группы toocreate и использование учетных записей в Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Просмотр подписчиков tooa продукта
Hello **подписчиков** вкладке перечисляются hello разработчиков, которые подписаны toohello продукта. Hello сведения и параметры на каждом компьютере разработчика можно просмотреть, щелкнув имя разработчика hello. В этом примере не разработчики еще подписаны toohello продукта.

![Разработчики][api-management-developer-list]

## <a name="next-steps"> </a>Дальнейшие действия
Один раз hello требуемого API-интерфейсы добавляются и опубликован продукт hello, разработчики могут подписаться toohello продукта и начать hello toocall API-интерфейсы. Руководство, в котором рассматриваются эти операции, а также подробно описывается конфигурация продукта, см. в статье [Защита API путем ограничения скорости с помощью управления API Azure][How create and configure advanced product settings in Azure API Management].

Дополнительные сведения о работе с продуктами см. следующие видео hello.

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
