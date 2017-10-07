---
title: "сообщения aaaEncode AS2 - приложения логики Azure | Документы Microsoft"
description: "Как toouse hello кодировщика AS2 в hello пакет интеграции Enterprise для приложения логики Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Кодирование сообщения AS2 для приложения логики Azure с помощью hello пакет интеграции Enterprise

tooestablish безопасность и надежность при передаче сообщений, использовать соединитель сообщение hello кодирования AS2. Этот соединитель обеспечивает цифровой подписи, шифрования и подтверждений через сообщения метода обработки уведомления (MDN), что также приводит toosupport для Неотказуемость.

## <a name="before-you-start"></a>Перед началом работы

Вот hello необходимых элементов.

* Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).
* [Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure. Необходимо иметь соединителя интеграции кодирования AS2 hello учетной записи toouse сообщения.
* В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).
* В учетной записи интеграции должно быть определено [соглашение AS2](logic-apps-enterprise-integration-as2.md).

## <a name="encode-as2-messages"></a>Кодирование сообщений AS2

1. [Создание приложения логики](logic-apps-create-a-logic-app.md).

2. Соединитель сообщения AS2 кодирования Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса. В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.

3.  В поле поиска hello введите «AS2» для фильтра. Выберите **AS2 — Encode AS2 message** (AS2 — кодирование сообщения AS2).
   
    ![Поиск по запросу "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение. Имя подключения и установите hello интеграции учетной записью, которую tooconnect. 
   
    ![Создайте учетную запись toointegration подключения](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Свойства со звездочкой обязательные.

    | Свойство | Сведения |
    | --- | --- |
    | Имя подключения* |Введите имя подключения |
    | Учетная запись интеграции* |Выберите имя для учетной записи интеграции. Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения. |

5.  После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis. toofinish при создании подключения, выберите **создать**.
   
    ![Сведения для подключения учетной записи интеграции](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. После создания подключения, как показано в следующем примере, введите данные для **AS2-из**, **AS2 tooidentifiers** согласно настройкам в лицензионном соглашении и **текст**, который является полезные данные сообщения Hello.
   
    ![заполнение обязательных полей](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Сведения о кодировщике AS2

Соединитель кодирования AS2 Hello выполняет следующие задачи: 

* Обработка заголовков AS2 и HTTP.
* Подписывание исходящих сообщений (если настроено).
* Кодирование исходящих сообщений (если настроено).
* Сжимает приветственное сообщение (если настроено)

## <a name="try-this-sample"></a>Пробное использование примера

развертывания полностью логику приложения и образец сценария AS2, tootry разделе hello [AS2 шаблон логику приложения и сценария](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Представление hello swagger
В разделе hello [swagger сведения](/connectors/as2/). 

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

