---
title: "Введение aaaAPI приложений | Документы Microsoft"
description: "Узнайте, как служба приложений Azure помогает разрабатывать, размещать и использовать интерфейсы RESTful API."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Обзор приложений API
Приложения API в службе приложений Azure предложение возможностей, которые позволяют упростить toodevelop узлов и использовать интерфейсы API в hello облака и локально. Приложения API обеспечивают преимущества безопасности корпоративного класса, простого контроля доступа, возможности гибридного подключения, автоматического создания пакетов SDK и непрерывной интеграции с [приложениями логики](../logic-apps/logic-apps-what-are-logic-apps.md).

[Служба приложений Azure](../app-service/app-service-value-prop-what-is.md) — это полностью управляемая платформа для сценариев веб- и мобильных приложений, а также интеграции. Приложения API являются одним из четырех типов приложений, предлагаемых [службой приложений Azure](../app-service/app-service-value-prop-what-is.md).

![Типы приложений в службе приложений Azure](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>Возможности приложений API
Вот несколько ключевых функций приложений API.

* **Перевести существующие API как-—** - не toochange любой hello код в существующих tootake преимущество для API-интерфейсы API приложений — просто развернуть приложение tooan API кода. API может использовать любой язык или платформу, поддерживаемые службой приложений, включая ASP.NET и C#, Java, PHP, Node.js и Python.
* **Простое использование.** Интегрированная поддержка [метаданных API Swagger](http://swagger.io/) упрощает использование ваших API множеством разных клиентов.  Автоматически создавайте код клиента для API на разных языках, включая C#, Java и Javascript. Легко настраивайте [CORS](app-service-api-cors-consume-javascript.md) без изменения кода. Дополнительные сведения см. в статьях [Метаданные приложений API службы приложений для обнаружения API и создания кода](app-service-api-metadata.md) и [Использование приложения API из JavaScript с помощью CORS](app-service-api-cors-consume-javascript.md). 
* **Управление доступом простой** -предотвратить доступ без проверки подлинности tooyour без изменения кода приложения API. Службы встроенной проверки подлинности защищают API для доступа других служб и клиентов, представляющих пользователей. В число поддерживаемых поставщиков удостоверений входят: Azure Active Directory, Facebook, Twitter, Google и учетная запись Майкрософт. Клиенты могут использовать библиотеки проверки подлинности Active Directory (ADAL) или hello пакет SDK для мобильных приложений. Дополнительные сведения см. в статье [Проверка подлинности и авторизация для приложений API в службе приложений Azure](app-service-api-authentication.md).
* **Интеграция с Visual Studio** -выделенного средства в Visual Studio упрощения работы hello создания, развертывания, использования, отладка и управление приложениями API. Дополнительные сведения см. в разделе [Announcing hello 2.8.1 пакет SDK Azure для .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Интеграция с приложениями логики.** Созданные вами приложения API могут использоваться [приложениями логики службы приложений](../logic-apps/logic-apps-what-are-logic-apps.md).  Дополнительные сведения см. в статьях [Использование настраиваемого интерфейса API, размещенного в службе приложений, с приложениями логики](../logic-apps/logic-apps-custom-hosted-api.md) и [Новая версия схемы 2015-08-01-preview](../logic-apps/logic-apps-schema-2015-08-01.md).

Кроме того, приложение API может использовать преимущества функций, предоставляемых [веб-приложениями](../app-service-web/app-service-web-overview.md) и [мобильными приложениями](../app-service-mobile/app-service-mobile-value-prop.md). Hello обратного также имеет значение true: при использовании веб-приложения или toohost мобильное приложение API-Интерфейс, он может использовать преимущества функций API приложений, таких как метаданные Swagger для клиента создание кода и CORS для браузера междоменного доступа. Hello разность hello трех типов приложений (API-интерфейса, веб-, мобильных устройств) — hello имя и значок, используемый для них в hello портал Azure.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Что такое hello различие между приложениями API и API управления Azure
Приложения API и [служба управления API Azure](../api-management/api-management-key-concepts.md) являются взаимодополняющими.

* Служба управления API имеет отношение к управлению API-интерфейсами. Уделено toomonitor API интерфейса API управления и регулировать использование ресурсов, управлять ввода и вывода, объединять несколько интерфейсов API в одну конечную точку и так далее. Hello управляемых интерфейсов API может размещаться в любом месте.
* Приложения API связаны с размещением API-интерфейсов. Служба Hello включает возможности, облегчающие разработку и развертывание API-интерфейсов, но это не hello видов мониторинга, регулирование, обработка или объединения, которые выполняют API управления. Если вам не требуются возможности управления API, можно размещать интерфейсы API в приложениях API без использования этой службы.

Ниже приведена схема, которая демонстрирует использование службы управления API для интерфейсов API, размещенных в приложениях API и в другом месте.

![Приложения API и служба управления API Azure](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Некоторые компоненты службы управления API и приложений API имеют аналогичные функции.  Например, они могут автоматизировать поддержку CORS. При совместном использовании hello две службы используется API-Интерфейс управления для CORS с момента его функции как hello tooyour API приложений переднего плана. 

## <a name="getting-started"></a>Приступая к работе
tooget работы с приложениями API, развернув tooone образец кода, см. Учебник hello для любой платформы, вы предпочитаете:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask вопросы о приложениях API запустить поток в hello [форуме по API приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

