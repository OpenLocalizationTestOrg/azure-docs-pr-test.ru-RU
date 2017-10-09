---
title: "сообщения aaaDecode AS2 - приложения логики Azure | Документы Microsoft"
description: "Как toouse hello декодер AS2 в hello пакет интеграции Enterprise для приложения логики Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Декодирование сообщения AS2 для приложения логики Azure с hello пакет интеграции Enterprise 

tooestablish безопасность и надежность при передаче сообщений, использовать соединитель сообщение hello декодировать AS2. Этот соединитель выполняет цифровое подписывание, расшифровку и подтверждение через уведомления о состоянии сообщений (MDN).

## <a name="before-you-start"></a>Перед началом работы

Вот hello необходимых элементов.

* Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).
* [Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure. Необходимо иметь соединителя интеграции декодировать AS2 hello учетной записи toouse сообщения.
* В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).
* В учетной записи интеграции должно быть определено [соглашение AS2](logic-apps-enterprise-integration-as2.md).

## <a name="decode-as2-messages"></a>Декодирование сообщений AS2

1. [Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

2. Соединитель сообщения AS2 декодировать Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса. В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.

3.  В поле поиска hello введите «AS2» для фильтра. Выберите **AS2 — Decode AS2 message** (AS2 — декодирование сообщения AS2).
   
    ![Поиск по запросу "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение. Имя подключения и установите hello интеграции учетной записью, которую tooconnect.
   
    ![Создание подключения к системе интеграции](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    Свойства со звездочкой обязательные.

    | Свойство | Сведения |
    | --- | --- |
    | Имя подключения* |Введите имя подключения |
    | Учетная запись интеграции* |Выберите имя для учетной записи интеграции. Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения. |

5.  После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis. toofinish при создании подключения, выберите **создать**.

    ![Сведения для подключения учетной записи интеграции](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. После создания подключения, как показано в следующем примере, выберите **текст** и **заголовки** с hello запрашивать выходные данные.
   
    ![подключение к системе интеграции создано](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    Например:

    ![Выберите текст и заголовки из выходных данных запроса](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>Сведения о декодере AS2

Соединитель декодировать AS2 Hello выполняет следующие задачи: 

* обрабатывает заголовки AS2 и HTTP;
* Проверяет подпись hello (если настроено)
* Расшифровывает сообщений hello (если настроено)
* Распаковывает приветственное сообщение (если настроено)
* Согласование полученных MDN с исходной исходящего сообщения hello
* Обновляет и сопоставляет записей в неотказуемой базе данных hello
* сохраняет записи отчетов о состоянии AS2;
* Hello вывода полезных данных состоит в кодировке base64
* Определяет ли уведомление MDN является обязательным и ли hello MDN должны синхронной или асинхронной на основе конфигурации в соглашении AS2
* создает синхронное или асинхронное MDN (в зависимости от конфигурации соглашения);
* Задает токенов корреляции hello и свойства для hello MDN

## <a name="try-this-sample"></a>Пробное использование примера

развертывания полностью логику приложения и образец сценария AS2, tootry разделе hello [AS2 шаблон логику приложения и сценария](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Представление hello swagger
В разделе hello [swagger сведения](/connectors/as2/). 

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md) 

