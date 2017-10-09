---
title: "Соединитель базы данных Oracle aaaAdd hello в свои приложения логики Azure | Документы Microsoft"
description: "Использовать соединитель базы данных Oracle hello в приложение логики"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Начало работы с соединителем hello базы данных Oracle

Используя соединитель hello базы данных Oracle, создать организации рабочие процессы, использующие данные в существующей базе данных. Этот соединитель может подключаться tooan установке базы данных Oracle в локальной или виртуальной машине Azure с базой данных Oracle. С помощью соединителя вы можете:

* Сборки рабочего процесса, добавив новую базу данных клиентам tooa клиента или обновления заказа в базе данных заказов.
* Используйте действия tooget строки данных, вставить новую строку и даже удалять. Например, создание записи в Dynamics CRM Online (триггер) может приводить к добавлению строки в базу данных Oracle (действие). 

В этом разделе показано, как toouse hello соединителю базы данных Oracle в приложение логики.

## <a name="prerequisites"></a>Предварительные требования

* Поддерживаемые версии Oracle: 
    * Oracle 9 и более поздних версий;
    * клиентское программное обеспечение Oracle 8.1.7 и более поздних версий.

* Установите hello локальный шлюз данных. [Подключение tooon локальные данные из приложения логики](../logic-apps/logic-apps-gateway-connection.md) списки hello действия. шлюз Hello — tooan tooconnect требуется локальная база данных Oracle или Виртуальной машине Azure с установлена база данных Oracle. 

    > [!NOTE]
    > Hello локального шлюза данных выступает в качестве моста и предоставляет безопасную передачу данных между локальными данными (данные, находится не в облаке hello) и приложениях для логики. Здравствуйте, один шлюз может использоваться с несколькими службами и несколько источников данных. Таким образом может достаточно шлюза hello tooinstall один раз.

* Установите клиент Oracle hello на машине hello, где установлен на локальный шлюз данных hello. Убедитесь, что tooinstall hello 64-разрядный поставщик данных Oracle для .NET из Oracle:  

  [ODAC 12c, 64-разрядная версия 4 (12.1.0.2.4) для Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Если не установлен клиент Oracle hello, произошла ошибка при попытке toocreate или использовать подключение hello. В разделе hello типичных ошибок в этом разделе.


## <a name="add-hello-connector"></a>Добавление соединителя hello

> [!IMPORTANT]
> Этот соединитель не содержит триггеров. В нем есть только действия. Таким образом при создании логики приложения, добавьте другой триггер toostart логику приложения, такие как **расписание - повторения**, или **запрос / ответ - ответ**. 

1. В hello [портал Azure](https://portal.azure.com), создание пустого логику приложения.

2. Во время запуска hello логики приложения, выберите hello **запрос / ответ - запрос** триггер: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Щелкните **Сохранить**. При сохранении данных автоматически создается URL-адрес запроса. 

4. Выберите **Новый шаг**, а затем — **Добавить действие**. Введите в `oracle` toosee hello доступных действий: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Кроме того, это самый быстрый способ toosee hello hello триггеров и действий, доступных для всех соединителей. Введите часть имени соединителя hello, такие как `oracle`. Конструктор Hello указаны какие-либо триггеры и каких-либо действий. 

5. Выберите одно из действий hello, таких как **базы данных Oracle - Get строки**. Установите флажок **Connect via on-premises data gateway** (Подключение через локальный шлюз данных). Введите имя сервера Oracle hello, метод проверки подлинности, имя пользователя, пароль и выберите hello шлюза:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. После подключения выберите таблицу из списка hello и введите идентификатор tooyour hello строки таблицы. Требуется идентификатор toohello tooknow hello таблицы. Если вы не знаете, обратитесь к администратору базы данных Oracle и получить hello выходные данные `select * from yourTableName`. Это дает hello сведения, необходимые tooproceed.

    В следующем примере hello задания данных возвращается из базы данных трудовых ресурсов: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. В следующем шаге вы можно использовать любой из hello другие соединители toobuild рабочего процесса. Если вы tootest получение данных из Oracle, а затем отправить себе электронное сообщение hello Oracle с данными с помощью одного из hello отправьте соединители электронной почты, такие Office 365 или Gmail. Используйте маркеры динамических hello из таблицы toobuild hello Oracle hello `Subject` и `Body` вашей электронной почты:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Сохраните** приложение логики, а затем выберите **Выполнить**. Закройте конструктор hello и просмотрите журнал запусков hello статуса hello. В случае неудачи, выделите строку неудачное сообщение hello. Откроется конструктор Hello и показывает, что шаг выполнен и просмотреть hello сведения об ошибке. В случае успеха, вы должны получить электронное сообщение hello сведения, которые вы добавили.


### <a name="workflow-ideas"></a>Идеи для рабочих процессов

* Хотите хэштегом hello #oracle toomonitor и поместить твиты hello в базе данных, их можно запросить и использовать в других приложениях. В приложении логики, добавить hello `Twitter - When a new tweet is posted` триггер и введите hello **#oracle** хэштегом. Затем добавьте hello `Oracle Database - Insert row` действие и выберите таблицу:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* Сообщения отправляются в очередь Service Bus tooa. Необходимо tooget эти сообщения и поместить их в базе данных. В приложении логики, добавить hello `Service Bus - when a message is received in a queue` триггер и выберите hello очереди. Затем добавьте hello `Oracle Database - Insert row` действие и выберите таблицу:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Распространенные ошибки

#### <a name="error-cannot-reach-hello-gateway"></a>**Ошибка**: не удается связаться с hello шлюза

**Причина**: hello локальный шлюз данных не может tooconnect toohello облака. 

**Устранение рисков**: Убедитесь, что шлюз находится под управлением hello на локальном компьютере, где он установлен, и что он может подключаться toohello Интернета.  Рекомендуется не устанавливать hello шлюза на компьютере, могут быть отключены или спящего режима. Можно также перезапустить службы шлюза данных локальной hello (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Ошибка**: используемого поставщика hello устарел: "System.Data.OracleClient требуется клиентское программное обеспечение версии 8.1.7 или более поздней.". Перейдите на страницу [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello официальным поставщиком.

**Причина**: SDK не установлен на компьютере hello там, где hello клиента Oracle hello локальный шлюз данных работает.  

**Разрешение**: Загрузите и установите пакет SDK для клиента Oracle hello на hello компьютере hello локальный шлюз данных.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Ошибка.** В таблице [Имя_таблицы] не определены ключевые столбцы.

**Причина**: hello таблица имеет первичный ключ.  

**Разрешение**: hello базы данных Oracle соединитель требует использования таблицы со столбцом первичного ключа.

#### <a name="currently-not-supported"></a>Сейчас не поддерживаются:

* представления и хранимые процедуры; 
* таблицы с составными ключами;
* типы вложенных объектов в таблицах.
 
## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/oracle/). 

## <a name="get-some-help"></a>Справочные сведения

Hello [приложения логики Azure форум](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) лучшие поместите tooask вопросы, ответить на вопросы и см. другие приложения логики их действия. 

Вы можете улучшить Logic Apps и соединители, внеся свои предложения или проголосовав за уже внесенные на сайте [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md)и просмотрите доступные соединители hello в приложениях для логики в наших [список API-интерфейсы](apis-list.md).
