---
title: "Приступая к работе с API в службе управления API Azure | Документация Майкрософт"
description: "Узнайте, как создавать API, добавлять операции и начать работу со службой управления API."
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
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Начало работы со службой управления Azure API 
## <a name="overview"> </a>Содержание раздела
Это руководство поможет быстро начать работу со службой управления API Azure и создать первый вызов API.

## <a name="concepts"> </a>Что такое служба управления Azure API?
Службу управления Azure API можно использовать для запуска полноценной программы API на основе любого внутреннего сервера.

Ниже приведены распространенные сценарии.

* **Защита мобильной инфраструктуры** путем ограничения доступа с помощью ключей API, а также предотвращения DOS-атак за счет регулирования или использования расширенных политик безопасности, например проверки маркера JWT.
* **Включение партнерской экосистемы независимого поставщика программного обеспечения** путем предложения быстрой партнерской адаптации на портале разработчика и создания интерфейсной части API поможет отделиться от внутренних реализаций, не готовых для использования партнером.
* **Выполнение внутренней программы API** за счет предложения организации централизованного расположения для обмена данными о доступности и последних изменениях в интерфейсах API, а также ограничения доступа на основе учетных записей организации, которые основаны на защищенном канале между шлюзом API и сервером.

Система состоит из следующих компонентов.

* **Шлюз API** – конечная точка, которая:
  
  * принимает вызовы API и направляет их на серверы;
  * проверяет ключи API, маркеры привязки JWT, сертификаты и другие учетные данные;
  * принудительно применяет квоты использования и ограничения скорости;
  * преобразует API в режиме реального времени без изменения кода;
  * кэширует ответы сервера, если они настроены;
  * регистрирует метаданные вызова для аналитики.
* **Портал издателя** — административный интерфейс, предназначенный для настройки программы API. Он используется, чтобы:
  
  * определять или импортировать схемы API;
  * упаковывать интерфейсы API в продукты;
  * настраивать политики,например квоты или преобразования, в интерфейсах API;
  * получать дополнительную информацию на основе аналитики;
  * управлять пользователями.
* **Портал разработчика** выступает в качестве основной веб-платформы для разработчиков, которая позволяет:
  
  * читать документацию по API;
  * использовать API через интерактивную консоль;
  * создать учетную запись и оформить подписку, чтобы получить ключи API;
  * получить доступ к аналитике по использованию.

## <a name="create-service-instance"></a>Создание экземпляра управления API
> [!NOTE]
> Для работы с этим учебником требуется учетная запись Azure. Если ее нет, можно создать бесплатную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][Azure Free Trial].
> 
> 

Создание экземпляра службы — это первый шаг в работе с API Management. Войдите на [портал Azure][Azure Portal] и щелкните **Создать**, **Интернет+мобильные устройства**, **Управление API**.

![Новый экземпляр службы управления API ][api-management-create-instance-menu]

В качестве **имени** укажите уникальное имя поддомена для использования в качестве URL-адреса службы.

Выберите необходимые значения в поле **Подписка**, **Группа ресурсов** и **Расположение** для своего экземпляра службы.

Введите **Contoso Ltd.** в поле **Имя организации** и укажите свой электронный адрес в поле **Адрес электронной почты администратора**.

> [!NOTE]
> Этот адрес электронный почты используется для получения уведомлений от системы API Management. Дополнительные сведения см. в статье о [настройке уведомлений и почтовых шаблонов в службе управления Azure API][How to configure notifications and email templates in Azure API Management].
> 
> 

![Новая служба управления API][api-management-create-instance-step1]

Экземпляры службы управления API доступны на трех уровнях: Developer, Standard и Premium.

> [!NOTE]
> Уровень Developer предназначен для разработки, тестирования и пилотного запуска приложений API, для которых доступность — это некритичный параметр. На уровнях Standard и Premium можно масштабировать зарезервированное число единиц для обслуживания большего объема трафика. На уровнях Standard и Premium служба управления API обеспечивает наибольший уровень мощности и производительности. Вы можете изучать этот учебник, используя любой уровень. Дополнительные сведения об уровнях управления API см. на странице с [расценками на службу управления API][API Management pricing].
> 
> 

Щелкните **Создать**, чтобы начать подготовку экземпляра службы.

![Новая служба управления API][api-management-instance-created]

После создания экземпляра службы на следующем шаге создается или импортируется API.

## <a name="create-api"> </a>Импорт API
API представляет набор операций, которые могут быть вызваны клиентскими приложениями. Операции API передаются существующей веб-службе.

Вы можете создавать интерфейсы API (и добавлять операции) вручную, а также импортировать и то, и другое. В этом учебнике мы импортируем API для примера веб-службы калькулятора, предоставляемой корпорацией Майкрософт и размещенной в Azure.

> [!NOTE]
> Указания о создании API и добавлении операций вручную см. в статьях, посвященных [созданию интерфейсов API в службе управления Azure API](api-management-howto-create-apis.md) и [добавлению операций в службе управления Azure API](api-management-howto-add-operations.md).
> 
> 

Интерфейсы API настраиваются на портале издателя. Чтобы открыть его, щелкните **Publisher portal** (Портал издателя) на панели инструментов службы.

![Портал издателя][api-management-management-console]

Чтобы импортировать API калькулятора, щелкните **API** в расположенном слева меню **Управление API**, а затем выберите **Импортировать API**.

![Кнопка импорта API][api-management-import-api]

Выполните следующие действия, чтобы настроить API калькулятора.

1. Щелкните **Из URL-адреса**, введите **http://calcapi.cloudapp.net/calcapi.json** в текстовое поле **URL-адрес документа спецификаций** и щелкните переключатель **Swagger**.
2. В текстовое поле **Суффикс URL-адреса веб-API** введите **calc**.
3. Щелкните в поле **Продукты (необязательно)** и выберите **Starter**.
4. Щелкните **Сохранить** , чтобы импортировать API.

![Добавление нового API][api-management-import-new-api]

> [!NOTE]
> **управления API** поддерживает импорт документа Swagger версий 1.2 и 2.0 . Хотя в [спецификации по Swagger 2.0](http://swagger.io/specification) заявлено, что свойства `host`, `basePath` и `schemes` являются необязательными, ваш документ Swagger 2.0 **ДОЛЖЕН** содержать их — в противном случае он не импортируется. 
> 
> 

После импорта API на портале издателя выводится страница сводных данных для API.

![Сводные данные API][api-management-imported-api-summary]

Раздел API содержит несколько вкладок. Вкладка **Сводные данные** содержит базовые показатели и информацию об API. Вкладка [Параметры](api-management-howto-create-apis.md#configure-api-settings) используется для проверки и изменения конфигурации для API. Вкладка [Операции](api-management-howto-add-operations.md) используется для управления операциями API. Вкладка **Безопасность** используется для настройки проверки подлинности шлюза для внутреннего сервера с помощью базовой проверки подлинности или [взаимной проверки подлинности с помощью сертификатов](api-management-howto-mutual-certificates.md) и настройки [авторизации пользователя с помощью OAuth 2.0](api-management-howto-oauth2.md).  На вкладке **Проблемы** отображаются проблемы, о которых сообщают разработчики, использующие интерфейсы API. На вкладке **Продукты** можно настроить продукты, которые содержат этот API.

По умолчанию каждый экземпляр API управления поставляется с двумя демонстрационными продуктами:

* **Starter**
* **Unlimited**

В этом учебнике базовый API калькулятора был добавлен в продукт Starter при импорте API.

Чтобы делать вызовы к API, разработчикам сначала необходимо подписаться на продукт, что дает им возможность доступа к нему. Разработчики могут подписываться на продукты в портале разработчика. За них это также могут сделать администраторы в издательском портале. Вы становитесь администратором по умолчанию, так как создали экземпляр API управления на предыдущих шагах руководства, и поэтому вы подписаны на каждый продукт по умолчанию.

## <a name="call-operation"> </a>Вызов операции с портала разработчика
Операции могут быть вызваны из портала разработчика, в который встроен удобный способ просмотра и проверки операций API. На этом шаге учебника будет вызвана операция **Добавление двух целых** базового API калькулятора. Выберите **Портал разработчика** в правом верхнем меню в портале издателя.

![Портал разработчика][api-management-developer-portal-menu]

Выберите **API** в верхнем меню и щелкните **Базовый калькулятор**, чтобы увидеть доступные операции.

![Портал разработчика][api-management-developer-portal-calc-api]

Обратите внимание на описание и параметры примера, импортированные с API и с операциями, благодаря чему разработчики, которые будут использовать эту операцию, получают необходимую документацию. Эти описания можно также добавить при добавлении операций вручную.

Чтобы вызвать операцию **Добавление двух целых**, нажмите кнопку **Попробовать**.

![Попробовать][api-management-developer-portal-calc-api-console]

Вы можете ввести некоторые значения для параметров или оставить значения по умолчанию и щелкнуть **Отправить**.

![HTTP Get][api-management-invoke-get]

После вызова операции портал разработчика отображает **состояние ответа**, **заголовки ответа** и **содержимое ответа**.

![Ответ][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Просмотр аналитики
Чтобы просмотреть аналитику для базового калькулятора, снова перейдите к порталу разработчика, выбрав **Управление** в верхнем правом меню пользователя на портале разработчика.

![Управление][api-management-manage-menu]

Представление портала издателя по умолчанию представляет собой **панель мониторинга**, где присутствует информация об экземпляре управления API.

![панель мониторинга][api-management-dashboard]

Наведите указатель мыши на диаграмму **базового калькулятора** , чтобы просмотреть конкретные показатели использования API за данный период времени.

> [!NOTE]
> Если на диаграмме нет показателей, перейдите назад к порталу разработчика и сделайте несколько вызовов API, подождите немного, а затем вернитесь к панели мониторинга.
> 
> 

Щелкните **Просмотр сведений** для просмотра страницы сводной информации по API, включая расширенную версию выводимых показателей.

![Аналитика][api-management-mouse-over]

![Сводка][api-management-api-summary-metrics]

Для просмотра более подробных метрик и отчетов щелкните пункт **Аналитика** в меню **Управление API** слева.

![Обзор][api-management-analytics-overview]

Раздел **Аналитика** имеет следующие четыре вкладки.

* **Вкратце** содержит общую информацию об использовании и показатели состояния, а также информацию о наиболее активных разработчиках, продуктах, API и операциях.
* **Использование** содержит обзор деталей вызовов API и полосы пропускания, включая географическое представление.
* **Работоспособность** содержит коды состояний, показатели успешных попаданий в кэш и времена ответов API и служб.
* **Активность** содержит отчеты по конкретной активности для разработчиков, продуктов, API и операций.

## <a name="next-steps"> </a>Дальнейшие действия
* Информация о [защите интерфейсов API с помощью ограничений скорости](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
