---
title: "решения aaaCreate B2B - приложения логики Azure | Документы Microsoft"
description: "Получение данных в приложениях для логики с помощью функций hello B2B в hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Получение данных в приложениях для логики с функциями B2B hello в hello пакет интеграции Enterprise

После создания учетной записи интеграции с партнерами и соглашениями, будут готовы toocreate toobusiness (B2B) рабочий процесс для логики приложения с hello [пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Предварительные требования

toouse Здравствуйте, AS2 и X12 действия, необходимо иметь учетную запись интеграции Enterprise. Дополнительные сведения [toocreate интеграцию учетной записи](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Создание приложения логики с помощью соединителей B2B

Выполните эти шаги toocreate B2B приложения логики, использующий hello AS2 и X12 действия tooreceive данных от торгового партнера:

1. Создание приложения логики, затем [связать свою учетную запись интеграции приложения tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Добавить **запрос — при HTTP-запрос получен** триггер tooyour логику приложения.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. tooadd hello **декодировать AS2** действия, выберите **добавить действие**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter все toohello действия, который вы хотите ввести слово hello **as2** в поле поиска hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Выберите hello **AS2 - сообщения AS2 декодировать** действие.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Добавить hello **текст** , которые должны toouse в качестве входных данных. В этом примере выберите текст hello hello HTTP-запроса, что триггеры hello приложения логики. Или введите выражение, которое получает на входе заголовки hello в hello **ЗАГОЛОВКИ** поля:

    @triggerOutputs()['headers']

7. Добавьте необходимые hello **заголовки** для AS2, который можно найти в заголовках hello HTTP-запроса. В этом примере выберите hello заголовки HTTP-запроса hello этого триггера hello логику приложения.

8. Теперь добавьте действие сообщения hello декодирования X12. Выберите **Добавить действие**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter все toohello действия, который вы хотите ввести слово hello **x12** в поле поиска hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Выберите hello **X12-декодирование X12 сообщение** действие.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Теперь необходимо указать входной toothis действие hello. Входные данные — hello выходные данные предыдущего действия AS2 hello.

    содержимое фактическое сообщение Hello объекта JSON и имеет кодировку base64, поэтому необходимо указать выражение в качестве входного hello. 
    Введите следующее выражение в hello hello **X12 НЕСТРУКТУРИРОВАННОГО файла сообщения tooDECODE** поля ввода:
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    Теперь добавьте шаги toodecode hello X12 данных получено от торгового партнера hello и выходных элементов в объекте JSON. 
    Получено toonotify hello партнера, который hello данных, можно отправить обратно ответ, содержащий hello AS2 сообщения метода обработки уведомления (MDN) в действие ответа HTTP.

12. tooadd hello **ответ** действия, выберите **добавить действие**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter все toohello действия, который вы хотите ввести слово hello **ответ** в поле поиска hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Выберите hello **ответ** действие.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello MDN из вывода hello hello **сообщение декодирования X12** действие, hello ответ набора **текст** поля в этом выражении:

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Сохраните результаты своих действий.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

Настройка приложения логики B2B завершена. Такого приложения может потребоваться toostore hello декодировать X12 данных в хранилище данных или приложение бизнес-(LOB). tooconnect собственные бизнес-приложений и использовать эти API-интерфейсы в приложение логику, можно добавить дополнительные действия или писать пользовательские API.

## <a name="features-and-use-cases"></a>Функции и варианты использования

* Hello AS2 X12 декодирования и кодирования действия позволяют обмен данными между торговыми партнерами с помощью стандартных отраслевых протоколов в логике приложения.
* tooexchange данных с торговыми партнерами, можно использовать AS2 и X12 с или без друг с другом.
* Hello B2B действия позволяют легко создавать партнеров и соглашений в вашей учетной записи интеграции и использовать их в приложение логики.
* Вы можете дополнительно расширить возможности приложения логики, настроив обмен данными с другими приложениями и службами, например Salesforce.

## <a name="learn-more"></a>Подробнее
[Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md)
