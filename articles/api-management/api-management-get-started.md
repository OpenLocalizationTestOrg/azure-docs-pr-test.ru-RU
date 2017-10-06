---
title: "aaaManage первый API в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocreate API, добавьте операции и приступить к работе со службой управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Начало работы со службой управления Azure API 
## <a name="overview"> </a>Содержание раздела
В этом руководстве показано, как tooquickly Приступая к работе с использованием службы управления API Azure и сделать ваш первый вызов API.

## <a name="concepts"> </a>Что такое служба управления Azure API?
Можно использовать любой серверной tootake API управления Azure и запустить программу полноценные API, на его основе.

Ниже приведены распространенные сценарии.

* **Защита мобильной инфраструктуры** путем ограничения доступа с помощью ключей API, а также предотвращения DOS-атак за счет регулирования или использования расширенных политик безопасности, например проверки маркера JWT.
* **Включение экосистемы партнера ISV** , предлагая адаптации быстрого партнера по hello разработки при помощи портала и построение toodecouple оболочкой API из внутренней реализации, не богатыми возможностями потребления партнера.
* **Запущено внутренних API** обеспечивая централизованное hello toocommunicate организации о доступности hello и последних изменений tooAPIs, стробирования доступ на основании учетных записей организации, на основе защищенного канала между шлюз Hello API и серверной hello.

система Hello состоит из hello следующие компоненты:

* Hello **шлюза API** является конечной точкой hello:
  
  * Принимает вызывает API и направляет их tooyour серверных системах.
  * проверяет ключи API, маркеры привязки JWT, сертификаты и другие учетные данные;
  * принудительно применяет квоты использования и ограничения скорости;
  * Преобразует API на лету hello без изменения кода.
  * кэширует ответы сервера, если они настроены;
  * регистрирует метаданные вызова для аналитики.
* Hello **портал издателя** — административный интерфейс hello, где можно настроить программу API. Он используется, чтобы:
  
  * определять или импортировать схемы API;
  * упаковывать интерфейсы API в продукты;
  * Настройка политики, такие как квоты или преобразований на hello API-интерфейсы.
  * получать дополнительную информацию на основе аналитики;
  * управлять пользователями.
* Hello **портал разработчиков** служит в качестве основного веб-приложения hello для разработчиков, где они могут:
  
  * читать документацию по API;
  * Пробное использование API посредством hello интерактивной консоли.
  * Создать учетную запись и подписаться ключи tooget API.
  * получить доступ к аналитике по использованию.

## <a name="create-service-instance"></a>Создание экземпляра управления API
> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Если ее нет, можно создать бесплатную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][Azure Free Trial].
> 
> 

Hello первый шаг при работе со службой управления API — toocreate экземпляра службы. Войдите в toohello [портала Azure] [ Azure Portal] и нажмите кнопку **New**, **Интернет + мобильные устройства**, **управления API**.

![Новый экземпляр службы управления API ][api-management-create-instance-menu]

Для **имя**, укажите toouse поддомене уникальное имя для URL-адрес службы hello.

Выберите требуемого hello **подписки**, **группы ресурсов** и **расположение** для вашего экземпляра службы.

Введите **Contoso Ltd.** для hello **название организации**и введите адрес электронной почты в hello **адрес электронной почты администратора** поля.

> [!NOTE]
> Этот адрес электронной почты используется для получения уведомлений из системы управления API hello. Дополнительные сведения см. в разделе [как tooconfigure уведомления и шаблонов в Azure API Management электронной почты][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Новая служба управления API][api-management-create-instance-step1]

Экземпляры службы управления API доступны на трех уровнях: Developer, Standard и Premium.

> [!NOTE]
> Hello уровень Developer предназначен для разработки, тестирования и пилотного развертывания программ API, где высокий уровень доступности не имеет значения. В hello Standard и Premium уровней можно масштабировать ваш toohandle число зарезервированных единиц большего объема трафика. Hello уровней Standard и Premium обеспечивают вашей службе управления API hello большинство вычислительной мощности и производительности. Вы можете изучать этот учебник, используя любой уровень. Дополнительные сведения об уровнях управления API см. на странице с [расценками на службу управления API][API Management pricing].
> 
> 

Нажмите кнопку **создать** toostart подготовки вашего экземпляра службы.

![Новая служба управления API][api-management-instance-created]

После создания экземпляра службы hello hello следующим шагом является toocreate или импортировать API.

## <a name="create-api"> </a>Импорт API
API представляет набор операций, которые могут быть вызваны клиентскими приложениями. Операции API-интерфейса — tooexisting через прокси веб-службы.

Вы можете создавать интерфейсы API (и добавлять операции) вручную, а также импортировать и то, и другое. В этом учебнике будет Импорт hello API образец калькулятора веб-служб, предоставляемых корпорацией Майкрософт и размещенных в Azure.

> [!NOTE]
> Руководство по созданию API и вручную добавлять операций см. в разделе [как toocreate API-интерфейсы](api-management-howto-create-apis.md) и [как tooan tooadd операций API](api-management-howto-add-operations.md).
> 
> 

API-интерфейсы настроены с портала издателя hello. tooreach его, нажмите кнопку **портал издателя** из инструментов службы hello.

![Портал издателя][api-management-management-console]

Калькулятор hello tooimport API, нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **импорта API**.

![Кнопка импорта API][api-management-import-api]

Выполните следующие шаги tooconfigure hello калькулятора API hello.

1. Нажмите кнопку **URL-адрес из**, введите **http://calcapi.cloudapp.net/calcapi.json** в hello **URL-адрес документа спецификации** текст и нажмите кнопку hello **Swagger**  переключатель.
2. Тип **calc** в hello **суффикс URL-адрес API** текстовое поле.
3. Нажмите кнопку в hello **продуктов (необязательно)** и выберите **начальный**.
4. Нажмите кнопку **Сохранить** tooimport hello API.

![Добавление нового API][api-management-import-new-api]

> [!NOTE]
> **управления API** поддерживает импорт документа Swagger версий 1.2 и 2.0 . Хотя в [спецификации по Swagger 2.0](http://swagger.io/specification) заявлено, что свойства `host`, `basePath` и `schemes` являются необязательными, ваш документ Swagger 2.0 **ДОЛЖЕН** содержать их — в противном случае он не импортируется. 
> 
> 

После импорта hello API hello сводной страницы для hello API отображается в портал издателя hello.

![Сводные данные API][api-management-imported-api-summary]

Hello API разделе есть несколько вкладок. Hello **Сводка** вкладке отображаются основные показатели и сведения о hello API. Hello [параметры](api-management-howto-create-apis.md#configure-api-settings) вкладка — tooview и измените hello конфигурации для API. Hello [операции](api-management-howto-add-operations.md) вкладка — операций hello toomanage используется API-интерфейса. Hello **безопасности** вкладка может быть tooconfigure используется проверка подлинности шлюза для hello внутреннему серверу с помощью обычной проверки подлинности или [взаимной проверки подлинности сертификатов](api-management-howto-mutual-certificates.md)и tooconfigure [ Проверка подлинности пользователя с помощью OAuth 2.0](api-management-howto-oauth2.md).  Hello **проблемы** вкладка — используется tooview неполадках, собранную hello разработчики, использующие собственные интерфейсы API. Hello **продуктов** вкладка — используется tooconfigure hello продуктов, которые содержат этот API.

По умолчанию каждый экземпляр API управления поставляется с двумя демонстрационными продуктами:

* **Starter**
* **Unlimited**

В этом учебнике hello базовый API-Интерфейс калькулятора добавлена продукт начальный toohello при импорте hello API.

В порядке toomake вызовы tooan API разработчики сначала необходимо подписаться tooa продукт, который дает им доступ tooit. Разработчики могут подписаться tooproducts на портале разработчиков hello или Администраторы могут подписаться tooproducts разработчики hello портала издателя. Вы являетесь администратором, с момента создания экземпляра API управления hello в hello предыдущие шаги в учебнике hello, вы уже подписанных tooevery продукта по умолчанию.

## <a name="call-operation"></a>Вызова операции с портала разработчиков hello
Операции могут вызываться непосредственно из портала разработчиков hello, который предоставляет удобный способ tooview и протестировать hello операции API-интерфейса. На этом шаге учебника будет вызывать hello основные калькулятора API-Интерфейсы **добавьте два целых числа** операции. Нажмите кнопку **портал разработчиков** меню hello hello верхнему правому углу портала издателя hello.

![Портал разработчика][api-management-developer-portal-menu]

Нажмите кнопку **API-интерфейсы** hello верхнем меню, и нажмите кнопку **калькулятору** toosee hello доступных операций.

![Портал разработчика][api-management-developer-portal-calc-api]

Обратите внимание, описания образец hello и параметры, которые были импортированы вместе с hello API и операции, предоставляя документации для разработчиков hello, которые будут использовать эту операцию. Эти описания можно также добавить при добавлении операций вручную.

toocall hello **добавьте два целых числа** операцию, нажмите кнопку **опробовать**.

![Попробовать][api-management-developer-portal-calc-api-console]

Можно ввести некоторые значения для параметров hello или оставьте значения по умолчанию hello и нажмите кнопку **отправки**.

![HTTP Get][api-management-invoke-get]

После вызова операции портал разработчиков hello отображает hello **состояние ответа**, hello **заголовки ответа**и любые **содержимого отклика**.

![Ответ][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Просмотр аналитики
Аналитика tooview для калькулятору портал издателя задней toohello коммутатора, выбрав **управление** меню hello hello верхнему правому углу портала разработчиков hello.

![Управление][api-management-manage-menu]

Hello представление по умолчанию для портала издателя hello — hello **мониторинга**, предоставляющее обзор вашего экземпляра управления API.

![Панель мониторинга][api-management-dashboard]

Наведите указатель мыши hello на диаграмме hello для **калькулятору** toosee hello определенных показателей использования hello hello API для определенного периода времени.

> [!NOTE]
> Если вы не видите все линии на диаграмме, переключиться назад toohello портал разработчиков и выполнять некоторые вызовы hello API, подождите несколько секунд и затем вернуться toohello панели мониторинга.
> 
> 

Нажмите кнопку **Просмотр сведений о** tooview hello Сводная страница hello API, включая увеличения hello отображаемых метрик.

![Аналитика][api-management-mouse-over]

![Сводка][api-management-api-summary-metrics]

Подробные метрики и отчеты, щелкните **Analytics** из hello **управления API** меню слева hello.

![Обзор][api-management-analytics-overview]

Hello **Analytics** раздел имеет hello следующие четыре вкладки:

* **Краткий обзор** предоставляет общее использование и метрики работоспособности также hello крупнейших разработчиков лучших продуктов, верхнем API-интерфейсы операции и top.
* **Использование** содержит обзор деталей вызовов API и полосы пропускания, включая географическое представление.
* **Работоспособность** содержит коды состояний, показатели успешных попаданий в кэш и времена ответов API и служб.
* **Действие** предоставляет отчеты, которые детализируют на конкретное действие hello, developer, продукт, API и операции.

## <a name="next-steps"> </a>Дальнейшие действия
* Узнайте, каким образом слишком[защиты API с пределы скорости](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
