---
title: "aaaChoose между потока, логику приложения, функции и веб-заданий | Документы Microsoft"
description: "Сравнение и сопоставление hello для облачных служб integration services корпорации Майкрософт и решите, какие службы следует использовать."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "microsoft flow, поток, logic apps, функции azure, функции, веб-задания azure, веб-задания, обработка событий, динамическое вычисление, независимая от сервера архитектура"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Сравнение Microsoft Flow, Logic Apps, функций и веб-заданий Azure
В этой статье сравнивает и противопоставляет hello следующие службы в облаке Microsoft hello, который можно все устранить проблемы интеграции и автоматизации бизнес-процессов:

* [Microsoft Flow](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Функции Azure](https://azure.microsoft.com/services/functions/)
* [веб-задания службы приложений Azure](../app-service-web/web-sites-create-web-jobs.md)

Все эти службы особенно полезны при объединении разрозненных систем. Они позволяют определять входные данные, действия, условия и выходные данные. Каждую отдельную службу можно запускать по расписанию или активировать по запросу. Тем не менее каждая служба добавляет уникальный набор значений, и их сравнения не вопрос «какая служба является лучшим hello?» Поэтому цель сравнения служб — определить не лучшую из них, а самую подходящую в определенном сценарии. Часто сочетание этих служб является лучшим способом hello, toorapidly построение масштабируемых, полный важная интеграции решения.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Сравнение Flow Logic Apps
Рассмотрим, Microsoft Flow и Azure Logic Apps друг с другом, так как оба *конфигурации первого* службы integration services, которые делает его легко toobuild процессов и рабочих процессов и интеграцию с различными SaaS и enterprise приложения. 

* Служба Flow создана на основе Logic Apps.
* Они имеют hello же конструктор рабочих процессов
* [Соединители](../connectors/apis-list.md) , работу в одном также может работать на других hello

Потоки, повышает эффективность любой worker office tooperform простой интеграции (например получить SMS для важных сообщений электронной почты) без перехода на разработчиков или ИТ. На Здравствуйте другой стороны, приложения логики можно включить дополнительные или критически важных интеграции (например, процессы B2B) и где требуются рекомендации DevOps и безопасность корпоративного уровня. Он является типичным для toogrow бизнеса рабочего процесса в сверхурочной работы сложности. Соответствующим образом можно начать с потоком на первый, а затем преобразовать его tooa логику приложения, при необходимости.

Hello Следующая таблица помогает определить, является ли поток или логику приложений наилучшим образом подходит для данной интеграции.

|  | Поток | Приложения логики |
| --- | --- | --- |
| Аудитория |Офисные сотрудники, бизнес-пользователи |ИТ-специалисты, разработчики |
| Сценарии |Самообслуживание |Критически важные интеграции |
| Средство разработки |В браузере и мобильном приложении, только пользовательский интерфейс |В браузере и [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md) доступно [представление кода](../logic-apps/logic-apps-author-definitions.md). |
| Разработка и операции |Ad-hoc, разработка в рабочей среде |Система управления версиями, тестирование, поддержка, автоматизация и управление в [Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md) |
| Административные функции |[https://flow.microsoft.com](https://flow.microsoft.com) |[https://portal.azure.com](https://portal.azure.com) |
| Безопасность |Стандартные методы безопасности: [независимость данных](https://wikipedia.org/wiki/Technological_Sovereignty), [шифрование при хранении](https://wikipedia.org/wiki/Data_at_rest#Encryption) для конфиденциальных данных и т. д. |Обеспечение безопасности Azure: [безопасность Azure](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [центр безопасности](https://azure.microsoft.com/services/security-center/), [журналы аудита](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/) и многое другое. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Сравнение функций и Веб-задания
Функции Azure и веб-задания службы приложений Azure рассматриваются вместе, так как они являются службами интеграции на основе модели *code-first* и предназначены для разработчиков. Они позволяют toorun сценарий или часть кода в ответ toovarious события, такие как [новых больших двоичных объектов хранилища](functions-bindings-storage.md) или [запрос веб-перехватчика](functions-bindings-http-webhook.md). Сходства между функциями Azure и веб-заданиями службы приложений Azure: 

* Созданы на основе [службы приложений Azure](../app-service/app-service-value-prop-what-is.md) и поддерживают одинаковые возможности, такие как [система управления версиями](../app-service-web/app-service-continuous-deployment.md), [аутентификация](../app-service/app-service-authentication-overview.md) и [мониторинг](../app-service-web/web-sites-monitor.md).
* Предназначены для разработчиков.
* Поддерживают стандартные языки программирования и скриптов.
* Поддерживают NuGet и NPM.

Функции — hello развитием веб-заданий, поскольку она принимает hello лучших особенностей веб-задания и улучшает их работу. Hello усовершенствования включают следующие: 

* Упрощенное разработки, тестирования и выполнения кода непосредственно в браузере hello.
* Встроенная интеграция с большим количеством служб Azure и сторонних служб, таких как [Объекты Webhook GitHub](https://developer.github.com/webhooks/creating/).
* Оплата за использование, нет необходимости toopay для [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Автоматизация, [динамическое масштабирование](functions-scale.md).
* Для существующих клиентов службы приложений, работающих на службы приложений плана все еще возможно (tootake преимуществами недостаточно ресурсов).
* Интеграция с Logic Apps.

Hello в следующей таблице обобщены hello различия между функциями и веб-заданий:

|  | Функции | Веб-задания |
| --- | --- | --- |
| Масштабирование |Масштабирование без настройки |Масштабирование в рамках плана службы приложений |
| Цены |Оплата за использование или в рамках плана службы приложений |В рамках плана службы приложений |
| Тип запуска |Активация, по расписанию (с помощью триггера таймера) |Активация, непрерывная работа, по расписанию |
| События триггера |[Таймер](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [концентраторы событий Azure](functions-bindings-event-hubs.md), [HTTP или Webhook (GitHub, Slack)](functions-bindings-http-webhook.md), [мобильные приложения службы приложений Azure](functions-bindings-mobile-apps.md), [центры уведомлений Azure](functions-bindings-notification-hubs.md), [служебная шина Azure](functions-bindings-service-bus.md), [служба хранилища Azure](functions-bindings-storage.md) |[Служба хранилища Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [служебная шина Azure](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Разработка в браузере |Поддерживается | Не поддерживается |
| Написание скриптов в окне |Экспериментальная возможность |Поддерживается |
| PowerShell |Экспериментальная возможность |Поддерживается |
| C# |Поддерживается |Поддерживается |
| F# |Поддерживается |Не поддерживается |
| Bash |Экспериментальная возможность |Поддерживается |
| PHP |Экспериментальная возможность |Поддерживается |
| Python |Экспериментальная возможность |Поддерживается |
| JavaScript |Поддерживается |Поддерживается |

Ли toouse функции или веб-заданий в конечном счете зависит то, что вы уже выполните службе приложений. Если у вас есть приложение службы приложений, для которого требуется toorun фрагменты кода, и требуется toomanage Здравствуйте, их вместе в одной среде DevOps, следует использовать веб-заданий. Если требуется toorun фрагменты кода для других служб Azure или даже сторонних приложений, или если требуется слишком управлять фрагменты кода интеграции отдельно от приложений служб приложений или требуется toocall фрагменты кода из логики приложения, следует воспользоваться всеми преимуществами улучшения Hello в функции.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, Logic Apps и функции
Как упоминалось ранее какая служба является наилучшим образом подходит tooyou зависит от конкретной ситуации. 

* Для оптимизации простых бизнес-процессов используйте Flow.
* Если сценарий интеграции слишком сложный для Flow или требуются возможности разработки и операций и обеспечения соответствия требованиям безопасности, то используйте Logic Apps.
* Если в рамках сценария интеграции требуется выполнить значительные преобразования или написать специализированный код, нужно создать приложение-функцию, а затем активировать функцию в качестве действия.

Приложение логики можно вызвать в потоке. Функцию также можно вызвать в приложении логики, а приложение логики — в функции. Интеграция Hello потока, логику приложения и функции по-прежнему tooimprove сверхурочной работы. Можно построения каких-либо в одной службе и использовать его в hello других служб. Поэтому все вложенные в эти три технологии средства оправданы.

## <a name="next-steps"></a>Дальнейшие действия
Начало работы с каждой из служб hello путем создания вашего первого потока, приложение логики, функция приложения или веб-задания. Щелкните одну из hello ссылкам:

* [Начало работы с Microsoft Flow](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md)
* [Создание первой функции Azure](functions-create-first-azure-function.md)
* [Развертывание веб-заданий с помощью Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Также можно получить дополнительные сведения об этих служб интеграции с hello ссылкам:

* [Leveraging Azure Functions & Azure App Service for integration scenarios by Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/) (Использование функций Azure и службы приложений Azure в сценариях интеграции. Автор: Кристофер Андерсон (Christopher Anderson))
* [Integrations Made Simple by Charles Lamanna](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/) (Упрощенные возможности интеграции. Автор: Чарльз Ламанна (Charles Lamanna))
* [Logic Apps Live Webcast](http://aka.ms/logicappslive)
* [Часто задаваемые вопросы о Microsoft Flow](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Документация по веб-заданиям Azure](../app-service-web/websites-webjobs-resources.md)

