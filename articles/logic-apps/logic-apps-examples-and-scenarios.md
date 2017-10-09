---
title: "aaaExamples & распространенные сценарии - приложения логики Azure | Документы Microsoft"
description: "Узнайте больше о приложениях логики, используя примеры, сценарии и руководства."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Примеры и распространенные сценарии для Azure Logic Apps

Здравствуйте toohelp, Узнайте больше о многих шаблонов, а также возможности приложения логики Azure, ниже приведены распространенные примеры и сценарии.

## <a name="key-scenarios-for-logic-apps"></a>Основные сценарии для приложений логики

Служба Azure Logic Apps обеспечивает устойчивую оркестрацию и интеграцию для различных служб. Hello логику приложения службы «без сервера», таким образом, нет tooworry о масштаб или экземпляры — все, что есть toodo является определение рабочего процесса hello (триггера и действия). базовая платформа Hello обрабатывает масштабирования, доступности и производительности. Любой сценарий, где должны toocoordinate несколько действий, особенно в нескольких системах — это отличный вариант использования для приложения логики Azure. Ниже приведено несколько шаблонов и примеров.

## <a name="respond-tootriggers-and-extend-actions"></a>Ответ tootriggers и расширять действия

Каждое приложение логики начинается с триггера. Например, рабочий процесс можно начать с запланированного события, вручную вызова или события из внешней системы, такие как hello «при добавлении файла tooan FTP-сервер» триггера. Приложения логики Azure в настоящее время поддерживает более 100 соединители готовые к использованию, начиная от локальной SAP tooMicrosoft Когнитивных служб. Для систем и служб, для которых соединители не опубликованы, можно также расширить приложения логики.

* [Создание настраиваемых триггеров или действий](../logic-apps/logic-apps-create-api-app.md)
* [Настройка длительных действий для запусков рабочего процесса](../logic-apps/logic-apps-create-api-app.md)
* [Ответ tooexternal события и действия с веб-перехватчиков](../logic-apps/logic-apps-create-api-app.md)
* [Вызывать срабатывание триггера, или вложить рабочих процессов с синхронной ответы tooHTTP запросов](../logic-apps/logic-apps-http-endpoint.md)
* [Учебник: Ответ веб-перехватчиков tooTwilio SMS и отправки ответа текста](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Руководство. Создание панели мониторинга социальных сетей на базе ИИ за несколько минут с помощью Logic Apps и Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Возможности обработки ошибок, ведения журнала и потока управления

Служба Logic Apps предоставляет широкие возможности для расширенного потока управления, в том числе условия, выключатели, циклы и области. tooensure устойчивым решений, вы также можете реализовать ошибки и обработка исключений в рабочих процессах. Для ведения журналов уведомлений и диагностики состояния рабочего процесса служба Azure Logic Apps обеспечивает средства мониторинга и уведомления.

* [Выполнение различных действий с помощью операторов switch](../logic-apps/logic-apps-switch-case.md)
* [Обработка элементов в массивах и коллекциях с помощью циклов и пакетов в приложениях логики](../logic-apps/logic-apps-loops-and-scopes.md)
* [Реализация обработки ошибок и исключений в рабочем процессе](../logic-apps/logic-apps-exception-handling.md)
* [Включение мониторинга, ведения журнала и оповещений для существующих приложений логики](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Включение мониторинга и ведения журнала диагностики при создании приложений логики](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Вариант использования. Как компания в сфере здравоохранения использует обработку исключений в приложении логики для рабочих процессов HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Развертывание приложений логики и управление ими

Можно полностью разработать и развернуть приложения логики с помощью Visual Studio, Visual Studio Team Services или любых других инструментов системы управления версиями и автоматической сборки. toosupport развертывания для рабочих процессов и зависимых соединений в шаблон ресурсов, логика приложения используют шаблоны развертывания ресурсов Azure. Набор средств Visual Studio автоматически создавать эти шаблоны, которые можно проверить в toosource управления версиями.

* [Создание шаблона для автоматического развертывания](../logic-apps/logic-apps-create-deploy-template.md)
* [Развертывание из Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Монитор работоспособности hello приложений логики](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Типы содержимого и их преобразование во время выполнения

Доступ, преобразование и преобразование несколько типов содержимого с помощью hello многими функциями в hello приложения логики Azure [язык определения рабочих процессов](http://aka.ms/logicappsdocs). Например, можно выполнять преобразование из строки, JSON и XML с hello `@json()` и `@xml()` выражения рабочего процесса. Hello Logic Apps engine сохраняет передачи содержимого toosupport типов содержимого в режиме без потерь между службами.

* [Обработка типов содержимого, отличных от JSON](../logic-apps/logic-apps-content-type.md), например `application/xml`, `application/octet-stream` и `multipart/formdata`
* [Как выражения рабочего процесса работают в приложениях логики](../logic-apps/logic-apps-author-definitions.md)
* [Справочник. Язык определения рабочего процесса Azure Logic Apps](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Прочие возможности интеграции и функции

Служба Logic Apps также поддерживает интеграцию со многими службами, включая Функции Azure, управление API Azure, службы приложений Azure и пользовательские конечные точки HTTP, например REST и SOAP.

* [Создание панели мониторинга сведений о клиентах в режиме реального времени с помощью Функций Azure и Azure Logic Apps](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Вызов Функций Azure из приложений логики](../logic-apps/logic-apps-azure-functions.md)
* [Сценарий. Активация приложений логики с помощью Функций Azure](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Блог. Вызов конечных точек SOAP из приложения логики](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>Комплексные сценарии

* [End-to-end case management integration in the utilities industry with Azure services](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps) (Интеграция комплексного управления случаями в отрасли служебных программ с помощью служб Azure)

## <a name="next-steps"></a>Дальнейшие действия

- [Обработка ошибок и исключений в приложениях логики](../logic-apps/logic-apps-exception-handling.md)
- [Создания определений рабочих процессов с языком определения рабочего процесса hello](../logic-apps/logic-apps-author-definitions.md)
- [Отправка комментариев, вопросов, отзывов или предложений по улучшению Azure Logic Apps](https://feedback.azure.com/forums/287593-logic-apps)