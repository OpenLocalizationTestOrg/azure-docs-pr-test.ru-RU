---
title: "aaaEnterprise интеграции для B2B - приложения логики Azure | Документы Microsoft"
description: "Создавать рабочие процессы B2B и поддержки корпоративных сценариев интеграции для логики приложений с помощью hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Обзор: Сценарии B2B и обмена данными с hello пакет интеграции Enterprise

Для рабочих процессов в бизнес бизнес (B2B) и беспроблемную связь с приложениями логики Azure можно включить корпоративных сценариях интеграции с корпорации Майкрософт Облачное решение, hello пакет интеграции Enterprise. Организации могут обмениваться электронными сообщениями, даже если они используют разные протоколы и форматы. пакет Hello преобразует различных форматах в формат, который систем организации могут распознавать и обрабатывать. Организации могут обмениваться сообщениями с помощью стандартных протоколов, в том числе [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) и [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). Сообщения можно защитить с помощью шифрования и цифровой подписи.

Если вы знакомы с BizTalk Server или служб BizTalk Microsoft Azure, компоненты интеграции предприятия hello, легко toouse, потому что большинство понятия похожи. Одно из основных отличий заключается в том, что интеграцию используется интеграции учетных записей toosimplify hello хранения и управления артефакты, используемые во взаимодействии B2B. 

С точки зрения архитектуры hello пакет интеграции Enterprise основывается на «интеграция учетных записей». Эти учетные записи являются облачными контейнерами, которые хранят все ваши артефакты, такие как схемы, партнеры, сертификаты, карты и соглашения. Использовать эти артефакты toodesign, развертывать и поддерживать B2B приложениях и также toobuild B2B рабочих процессов для логики приложений. Но прежде чем использовать эти артефакты, необходимо сначала связать логику приложения tooyour вашей учетной записи интеграции. После этого приложение логики будет иметь доступ к артефактам учетной записи интеграции.

## <a name="why-should-you-use-enterprise-integration"></a>Для чего следует использовать интеграцию Enterprise?

* Благодаря интеграции Enterprise можно хранить все артефакты в одном расположении — в своей учетной записи интеграции.
* Можно создавать рабочие процессы B2B и интегрировать сторонние приложения для браузера программное обеспечение как услуга (SaaS), локальные приложения и пользовательские приложения с помощью подсистемы приложения логики Azure hello и все соединители.
* Вы можете создать пользовательский код для приложения логики с помощью функций Azure.

## <a name="how-tooget-started-with-enterprise-integration"></a>Как tooget работу с интеграции предприятия?

Создавать и управлять приложениями B2B с hello пакет интеграции Enterprise через hello конструктор логику приложения в hello **портал Azure**. Вы также можете управлять приложениями логики с помощью [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Разделы о PowerShell, посвященные приложениям логики").

Ниже приведены hello высокоуровневые действия, которые необходимо выполнить перед созданием приложения hello портал Azure.

![Изображение для обзора](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Каковы наиболее распространенные сценарии применения?

Интеграция Enterprise поддерживает следующие отраслевые стандарты:

* EDI — электронный обмен данными;
* EAI — интеграция приложений.

## <a name="heres-what-you-need-tooget-started"></a>Вот что нужно tooget работы

* Подписка Azure с учетной записью интеграции.
* Visual Studio 2015 toocreate карты и схемы
* [Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0.](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Попробуйте сейчас

[Развертывание образца полностью AS2 send и получать приложение логики](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) , использующий функции hello B2B для логики приложения Azure.

## <a name="learn-more"></a>Подробнее
* [Соглашения](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях интеграции Enterprise")
* [Бизнес-сценарии (B2B) tooBusiness](../logic-apps/logic-apps-enterprise-integration-b2b.md "сведения как toocreate логики приложения с функциями B2B")  
* [Сертификаты](logic-apps-enterprise-integration-certificates.md "Узнайте о сертификатах интеграции Enterprise")
* [Плоский файл кодирование и декодирование](logic-apps-enterprise-integration-flatfile.md "сведения как tooencode и декодирование неструктурированного файла содержимого")  
* [Учетные записи интеграции](../logic-apps/logic-apps-enterprise-integration-accounts.md "Узнайте больше об учетных записях интеграции")
* [Карты](../logic-apps/logic-apps-enterprise-integration-maps.md "Узнайте о картах интеграции Enterprise")
* [Партнеры](logic-apps-enterprise-integration-partners.md "Узнайте о партнерах интеграции Enterprise")
* [Схемы](logic-apps-enterprise-integration-schemas.md "Узнайте о схемах интеграции Enterprise")
* [Проверка XML-сообщение](logic-apps-enterprise-integration-xml.md "узнать, как toovalidate XML сообщения с приложениями логики")
* [Преобразование XML-файла](logic-apps-enterprise-integration-transform.md "Узнайте о картах интеграции Enterprise")
* [Корпоративные соединители интеграции](../connectors/apis-list.md "Узнайте о соединителях пакета интеграции Enterprise.")
* [Метаданные учетной записи интеграции](../logic-apps/logic-apps-enterprise-integration-metadata.md "Узнайте о метаданных учетной записи интеграции")
* [Мониторинг сообщений "бизнес — бизнес"](logic-apps-monitor-b2b-message.md "Узнайте больше о мониторинге сообщений "бизнес — бизнес"")
* [Отслеживание сообщений "бизнес — бизнес" на портале OMS](logic-apps-track-b2b-messages-omsportal.md "Узнайте больше об отслеживании сообщений "бизнес — бизнес" на портале OMS")

