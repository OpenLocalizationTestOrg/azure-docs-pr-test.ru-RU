---
title: "сообщения EDIFACT aaaEncode - приложения логики Azure | Документы Microsoft"
description: "Проверка EDI и формирования XML с помощью кодировщика сообщений EDIFACT в hello пакет интеграции Enterprise для логики приложений Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Кодирование сообщений EDIFACT для приложения логики Azure с помощью hello пакет интеграции Enterprise

С соединителем сообщение hello кодирования EDIFACT проверки EDI и свойств, создание XML-документа для каждого набора транзакций и запросить Техническое подтверждение и функциональное подтверждение.
toouse этот соединитель, необходимо добавить существующий триггер в приложении логику tooan соединитель hello.

## <a name="before-you-start"></a>Перед началом работы

Вот hello необходимых элементов.

* Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).
* [Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure. Необходимо иметь соединителя интеграции кодирования EDIFACT hello учетной записи toouse сообщения. 
* В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).
* В учетной записи интеграции должно быть определено [соглашение EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="encode-edifact-messages"></a>Кодирование сообщений EDIFACT

1. [Создание приложения логики](logic-apps-create-a-logic-app.md).

2. Соединитель сообщения EDIFACT кодирования Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса. В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.

3.  В поле поиска hello введите «EDIFACT» фильтра. Выберите либо **кодирования сообщения EDIFACT, название соглашения** или **Encode tooEDIFACT сообщение с удостоверениями**.
   
    ![поиск EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение. Имя подключения и установите hello интеграции учетной записью, которую tooconnect.

    ![создание подключения к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Свойства со звездочкой обязательные.

    | Свойство | Сведения |
    | --- | --- |
    | Имя подключения* |Введите имя подключения |
    | Учетная запись интеграции* |Выберите имя для учетной записи интеграции. Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения. |

5.  После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis. toofinish при создании подключения, выберите **создать**.

    ![сведения о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    Подключение создано.

    ![создано подключение к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Кодирование сообщений EDIFACT по названию соглашения

Если вы настроили tooencode сообщения EDIFACT, название соглашения, открыть hello **соглашения имя EDIFACT** введите или выберите имя соглашения EDIFACT. Введите tooencode сообщение hello XML.

![Введите название соглашения EDIFACT и tooencode сообщения XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Кодирование сообщения EDIFACT по идентификаторам

Если выбранное tooencode сообщений EDIFACT удостоверений, введите идентификатор отправителя hello, квалификатор отправителя, идентификатор получателя и квалификатор получателя согласно настройкам в соглашении EDIFACT. Выберите tooencode сообщение hello XML.

![Введите идентификаторы для отправителя и получателя, выберите tooencode сообщения XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Сведения о кодировании EDIFACT

Соединитель кодирования EDIFACT Hello выполняет следующие задачи: 

* Разрешить hello соглашения, сопоставляя квалификатор отправителя hello & идентификатор квалификатор получателя, а и идентификатор
* Сериализует hello обмен EDI, преобразование сообщений XML-кодировке в EDI наборов транзакций в сообщении hello.
* Генерирует сегменты заголовков и окончаний для наборов транзакций.
* Создает контрольное число обмена, контрольное число группы и контрольное число набора транзакций для каждого исходящего обмена.
* Заменяет разделителей в полезных данных hello
* Проверяет EDI и свойства для конкретного партнера.
  * Проверка схемы элементов данных набора транзакций hello по схеме сообщение hello.
  * Выполняет проверку EDI для элементов данных в наборе транзакций.
  * Выполняет расширенную проверку для элементов данных в наборе транзакций.
* Создает XML-документ для каждого набора транзакций.
* Запрашивает техническое и (или) функциональное подтверждение (если настроено).
  * Как Техническое подтверждение CONTRL сообщение hello указывает поступления обмена.
  * Как функциональное подтверждение CONTRL сообщение hello указывает принятия или отклонения hello получил сообщение, группы или сообщения, и список ошибок или неподдерживаемых функций

## <a name="view-swagger-file"></a>Просмотр файла Swagger
tooview hello Swagger сведения для соединителя EDIFACT hello, см. [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

