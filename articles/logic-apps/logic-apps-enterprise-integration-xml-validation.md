---
title: "aaaValidate XML - приложения логики Azure | Документы Microsoft"
description: "Проверка XML с помощью схем для сценариев приложения логики Azure и B2B с помощью hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>Проверка XML для интеграции Enterprise

Часто в сценарии B2B hello партнеров в соглашении убедитесь обмена сообщений hello допустимы, до начала обработки данных. Документы с предварительно определенной схемой можно проверить с помощью hello проверки XML hello использование соединителя в пакет интеграции Enterprise hello.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Проверить документ с соединителем hello Проверка XML

1. Создание логики приложения, и [связать учетную запись для интеграции toohello приложения hello](../logic-apps/logic-apps-enterprise-integration-accounts.md "узнать toolink tooa логики интеграции учетной записи приложения") , содержащее схему hello, требуется toouse для проверки XML-данных.

2. Добавить **запрос — при HTTP-запрос получен** триггер tooyour логику приложения.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. tooadd hello **проверки XML** действия, выберите **добавить действие**.

4. Введите все hello toohello действия, который вы хотите toofilter *xml* в поле поиска hello. Выберите действие **Проверка XML**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Выберите toospecify hello XML-содержимое, которое следует toovalidate, **СОДЕРЖИМОГО**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Выберите тег текст hello в качестве содержимого, которое следует toovalidate hello.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. требуется toouse проверки hello предыдущей схемы hello toospecify *содержимого* ввода, выберите **имя СХЕМЫ**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Сохраните результаты своих действий.  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Вы закончили работу с настройкой соединителя проверки. В приложении реального мира может потребоваться toostore hello проверки данных в бизнес-приложения (LOB), например SalesForce. toosend Здравствуйте tooSalesforce проверенные выходных данных, добавить действие.

tootest действие проверки, создадим конечную точку toohello HTTP запроса.

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения о hello пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")   

