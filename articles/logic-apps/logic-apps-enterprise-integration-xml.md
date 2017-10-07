---
title: "сообщения о aaaWorking с XML в рабочие процессы — приложения логики Azure | Документы Microsoft"
description: "Обработка, проверка, преобразования и обогащения XML сообщения в логику приложения и с помощью бизнес tooscenarios hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Проверка и преобразование XML, кодирование и декодирование неструктурированных файлов и обогащение сообщений в приложениях логики

С помощью приложения логики, имеется XML-сообщения hello возможность tooprocess, которые отправляют и получают. Этот компонент входит в состав hello пакет интеграции Enterprise. Для этих пользователей на фоне BizTalk Server hello пакет интеграции Enterprise предоставляет аналогичные возможности tootransform и проверки сообщений, работать с плоскими файлами и даже использовать XPath tooenrich или извлечения определенного свойства из сообщения. 

Для пользователей, которым новые toothis места на диске эти функции разверните обработку сообщений в рамках рабочего процесса. Например если вы являетесь в бизнес-сценарии и работать с определенной схемы XML, можно использовать пакет интеграции Enterprise tooenhance hello как компании обрабатывает эти сообщения. 

Hello пакет интеграции Enterprise включает в себя: 

* [Проверка XML](logic-apps-enterprise-integration-xml-validation.md "Узнайте о проверке сообщений XML") позволяет проверить входящее или исходящее сообщение XML на соответствие указанной схеме.
* [Преобразование XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Дополнительные сведения о преобразования сообщений XML и карт") - преобразования или настроить на основе требований или требований hello участника XML-сообщения.
* [Кодирование и декодирование неструктурированных файлов](logic-apps-enterprise-integration-flatfile.md "См. дополнительные сведения о кодировании и декодировании неструктурированных файлов") позволяет кодировать и декодировать неструктурированный файл. Например, SAP принимает и отправляет IDOC-файлы в виде неструктурированных файлов. Многие платформы интеграции создают сообщения XML, включая Logic Apps. Таким образом можно создать приложение логики, что кодировщик неструктурированных файлов использует hello слишком «преобразование» tooflat файлы XML-файлов. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) - обогатить сообщение и извлечения определенного свойства из сообщения hello. После этого можно hello использования извлеченных назначения tooa сообщения hello tooroute свойства или промежуточной конечной точки.

## <a name="try-it-out"></a>Попробуйте сейчас
[Развертывание приложения, полностью логику ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (пример использования GitHub) с помощью функции hello XML в логику приложения Azure.

## <a name="learn-more"></a>Подробнее
[Дополнительные сведения о hello пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")
