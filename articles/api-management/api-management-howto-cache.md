---
title: "кэширование tooimprove производительности в Azure API Management aaaAdd | Документы Microsoft"
description: "Узнайте, как загрузить tooimprove hello задержки, потребление пропускной способности и веб-службы для вызовов службы управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Добавить кэширование tooimprove производительность в службе управления API Azure
Операции в управлении API можно настроить для кэширования ответов. Кэширование ответов может значительно уменьшить время задержки API, потребляемую пропускную способность, и нагрузку на веб-службу применительно к данным, которые изменяются редко.

В этом руководстве показано, как ответ tooadd кэширование для API и настроить политики для операций Echo API пример hello. Затем можно вызвать операцию hello от разработчика hello портала tooverify кэширования в действии.

> [!NOTE]
> Сведения о кэшировании элементов по ключу с помощью выражений политики см. в статье [Пользовательское кэширование в службе управления API Azure](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Перед следующей hello шаги данного руководства, необходимо иметь экземпляра службы управления API с API и настройки продукта. Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.

## <a name="configure-caching"> </a>Настройка операции для кэширования
На этом шаге вы просмотрите hello кэширование параметры hello **получить ресурс (с кэшированием)** операции образца hello Echo API.

> [!NOTE]
> Каждый экземпляр службы управления API поставляется предварительно настроенных Echo API-интерфейсы, можно использовать tooexperiment с и Дополнительные сведения о службе управления API. Дополнительные сведения см. в статье [Начало работы со службой управления Azure API][Get started with Azure API Management].
> 
> 

tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API. Откроется портал издателя управления API toohello.

![Портал издателя][api-management-management-console]

Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **Echo API**.

![Echo API][api-management-echo-api]

Щелкните hello **операции** , а затем щелкните hello **получить ресурс (с кэшированием)** операции hello **операции** списка.

![Операции интерфейса Echo API][api-management-echo-api-operations]

Нажмите кнопку hello **кэширование** hello tooview вкладку Параметры для этой операции кэширования.

![Вкладка "Кэширование"][api-management-caching-tab]

кэширование tooenable для операции select hello **включить** флажок. В этом примере кэширование включено.

Каждый ответ операции различаемых по значениям hello в hello **происходит изменение параметров строки запроса** и **Vary заголовками** поля. Если требуется несколько ответов на основе параметров строки запроса или заголовки toocache, можно настроить их в следующих двух полей.

**Длительность** указывает интервал срока действия hello hello кэширования ответов. В этом примере — интервал приветствия **3600** секунд — эквивалент tooone час.

С помощью конфигурации кэширования в этом примере hello, hello первый запрос toohello **получить ресурс (с кэшированием)** операция возвращает ответ от службы внутренних hello. Этот ответ кэшируются, ключом которых является указанный hello заголовки и запрос строковых параметров. Последующие вызовы операции toohello с соответствующими параметрами, будет иметь hello ответ возвращается, пока не истечет интервал длительности hello кэша в кэше.

## <a name="caching-policies"></a>Hello проверки политики кэширования
На этом шаге, проверьте параметры для hello кэширования hello **получить ресурс (с кэшированием)** операции образца hello Echo API.

Если настроены параметры кэширования для операции на hello **кэширование** вкладке кэширования для операции hello добавляются политики. Эти политики можно просматривать и редактировать в редакторе политики hello.

Нажмите кнопку **политики** из hello **API управления** меню hello слева, а затем выберите **Echo API и получить ресурс (с кэшированием)** из hello **операции**раскрывающегося списка.

![Операция с диапазоном политик][api-management-operation-dropdown]

При этом в редактор политики hello отображаются hello политик для этой операции.

![Редактор политик API Management][api-management-policy-editor]

Определение политики Hello для этой операции включает политик hello, определяющих hello конфигурации кэша, были проверены с помощью hello **кэширование** вкладку в предыдущем шаге hello.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Политики в редакторе hello политики кэширования toohello изменения будут отражены на hello **кэширование** вкладке операции и наоборот.
> 
> 

## <a name="test-operation"></a>Вызов операции и тестирование кэширования hello
toosee hello кэширования в действии, можно вызвать операцию hello с портала разработчиков hello. Нажмите кнопку **портал разработчиков** в правом верхнем меню hello.

![Портал разработчика][api-management-developer-portal-menu]

Нажмите кнопку **API-интерфейсы** в верхнем меню hello, а затем выберите **Echo API**.

![Echo API][api-management-apis-echo-api]

> Если у вас есть только один API-Интерфейс настройки или видимым tooyour учетной записи, выбрав API-интерфейсы вы перейдете непосредственно toohello операции для этого API-интерфейса.
> 
> 

Выберите hello **получить ресурс (с кэшированием)** операции, а затем щелкните **откройте консоль**.

![Открытие консоли][api-management-open-console]

Hello консоли позволяет выполнять операции tooinvoke непосредственно с портала разработчиков hello.

![Консоль][api-management-console]

Сохраните значения по умолчанию hello для **param1** и **param2**.

Здравствуйте, выберите нужный ключ из hello **ключ подписки** раскрывающегося списка. Если ваша учетная запись содержит только одну подписку, он уже будет выбран.

Введите **sampleheader:value1** в hello **заголовки запроса** текстовое поле.

Нажмите кнопку **HTTP Get** и запишите hello заголовки ответа.

Введите **sampleheader:value2** в hello **заголовки запроса** текстовое поле и нажмите кнопку **HTTP Get**.

Обратите внимание, что значение hello **sampleheader** по-прежнему **значение1** в ответ hello. Попробуйте несколько различных значений и обратите внимание, что hello кэшированного ответа от первого вызова hello возвращается.

Введите **25** в hello **param2** , а затем щелкните **HTTP Get**.

Обратите внимание, что значение hello **sampleheader** в hello ответа является **value2**. Поскольку hello результаты операции с ключами, соответствующими строки запроса, не был возвращен hello предыдущего кэшированного ответа.

## <a name="next-steps"> </a>Дальнейшие действия
* Дополнительные сведения о кэшировании политик см. в разделе [политики кэширования] [ Caching policies] в hello [Справочник по политикам управления API][API Management policy reference].
* Сведения о кэшировании элементов по ключу с помощью выражений политики см. в статье [Пользовательское кэширование в службе управления API Azure](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
