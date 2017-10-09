---
title: "aaaSet монитор событий концентраторов событий Azure для приложения логики Azure с | Документы Microsoft"
description: "Наблюдения за событиями tooreceive потоки данных и отправки событий для приложения логики Azure с помощью концентраторов событий Azure"
services: logic-apps
keywords: "поток данных, монитор событий, концентраторы событий"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Отслеживание, получать и отправлять события с соединителем hello концентраторов событий

tooset монитор событий, что логика приложения можно обнаруживать события, получать события и отправлять события, подключения tooan [концентратор событий Azure](https://azure.microsoft.com/services/event-hubs) из логики приложения. Ознакомьтесь с дополнительными сведениями о [концентраторах событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Требования

* У вас есть toohave [пространство имен концентраторов событий и концентратора событий](../event-hubs/event-hubs-create.md) в Azure. Дополнительные сведения [как toocreate пространство имен концентраторов событий и концентратора событий](../event-hubs/event-hubs-create.md). 

* toouse [всех соединителей](https://docs.microsoft.com/azure/connectors/apis-list) в приложении логику имеется toocreate логику приложение сначала. Дополнительные сведения [как toocreate приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Проверьте разрешения имен концентраторов событий и найдите строку подключения hello

Для вашего tooaccess логику приложения любой службы, имеют toocreate [ *подключения* ](./connectors-overview.md) между логику hello и приложения службы, если это еще не сделано. Это подключение авторизует данные tooaccess логику приложения.
Для вашего tooaccess логику приложения концентратора событий, у вас есть toohave **управление** разрешения и hello строку подключения для пространства имен концентраторов событий.

toocheck разрешения и строки подключения hello get, выполните следующие действия.

1.  Войдите в toohello [портал Azure](https://portal.azure.com "портал Azure"). 

2.  Go концентраторов событий tooyour *имен*, не hello конкретный концентратор событий. В колонке hello пространства имен в разделе **параметры**, выберите **политики общего доступа**. В разделе **Утверждения** убедитесь, что у вас есть разрешения на **управление** для этого пространства имен.

    ![Управление разрешениями для пространства имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  Выберите строку подключения hello toocopy для пространства имен hello концентраторов событий, **RootManageSharedAccessKey**. Далее tooyour первичного ключа строки подключения, выберите "Копировать" hello ".

    ![Скопируйте строку подключения к пространству имен концентраторов событий](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm ли указана строка соединения, связанного с пространством имен концентраторов событий или с конкретный концентратор событий, проверять hello строку подключения для hello `EntityPath` параметра. Если этот параметр, hello строка подключения для конкретного концентратора событий «entity» и не toouse правильными hello с логикой приложения.

4.  Теперь когда появится запрос учетных данных после добавления концентраторов событий триггера или действие tooyour логику приложения, можно подключиться пространство имен tooyour концентраторов событий. Присвойте имя подключения, введите строку подключения hello, которые скопированы и выберите **создать**.

    ![Ввод строки подключения к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    После создания подключения, имя подключения hello появится в триггер hello концентраторов событий или действия. 
    После этого можно продолжить с hello других шагов в логике приложения.

    ![Созданное подключение к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Запуск рабочего процесса при получении новых событий от концентратора событий

[*Триггер*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) — это событие, которое запускает рабочий процесс приложения логики. Чтобы запустить рабочий процесс, когда новые события отправляются tooyour концентратора событий, выполните следующие действия для добавления hello триггер, который обнаруживает это событие.

1.  В hello [портал Azure](https://portal.azure.com "портал Azure"), go tooyour существующего логику приложения или создания пустой логику приложения.

2.  Введите в поле поиска hello для hello конструктор логики приложения, `event hubs` для фильтра. Выберите триггер с именем **При наличии событий в концентраторе событий**.

    ![Выбор триггера, срабатывающего при получении концентратором событий новых событий](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Если у вас еще нет концентраторов событий tooyour пространство имен подключения, вам предложат toocreate теперь это подключение. Присвойте имя подключения и введите строку подключения hello концентраторов событий пространства имен. 
    При необходимости сведения [как toofind строки подключения](#permissions-connection-string).

    ![Ввод строки подключения к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    После создания соединения hello hello параметры для hello **при возникновении события в концентратор событий** отображаются триггера.

    ![Настройки триггера, срабатывающего при получении концентратором событий новых событий](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Введите или выберите имя hello hello концентратора событий, которые должны toomonitor. Выберите частоту hello и интервала для частоту hello toocheck концентратора событий.

    > [!TIP]
    > toooptionally выберите группу потребителей для чтения событий, выберите **Показывать дополнительные параметры**. 

    ![Выбор концентратора событий или группы потребителей](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Теперь настройки toostart триггера рабочего процесса для логики приложения. 
    Логика приложения проверяет hello указан на основе расписания hello, устанавливаемое концентратора событий. 
    Если приложение находит новые события в концентратор событий hello, другие действия или триггеры выполняется триггер hello в логике приложения.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Отправка событий tooyour концентратор событий из логики приложения

[*Действие*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) — это задание, выполняемое рабочим процессом приложения логики. После добавления в приложение логику tooyour триггера, можно добавить действие tooperform операций с данными, созданный с помощью этого триггера. toosend tooyour события концентратора событий, от логики приложения, выполните следующие действия.

1.  В конструкторе Logic App выберите для созданного триггера приложения логики пункты **Новый шаг** > **Добавить действие**.

    ![Выбор действий "Новый шаг" и "Добавить действие"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Теперь можно найти и выбрать tooperform действие. 
    Хотя можно выбрать любое действие, например, мы хотим действие toosend hello событий концентраторов событий.

2.  Введите в поле поиска hello, `event hubs` для фильтра.
Выберите действие **Отправка события**.

    ![Выбор действия "Концентраторы событий — отправка события"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Введите hello необходимые сведения для события hello, например имя hello hello место toosend hello события концентратора событий. Введите любые другие дополнительные сведения о событии hello, например содержимого для этого события.

    > [!TIP]
    > toooptionally указать раздел hello концентратора событий, где toosend hello событий, выберите **Показывать дополнительные параметры**. 

    ![Ввод имени концентратора событий и необязательных сведений о событии](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Сохраните изменения.

    ![Сохранение приложения логики](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    Теперь настройки событий toosend действие с логикой приложения. 

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/eventhubs/). 

## <a name="get-help"></a>Получение справки

tooask вопросы, ответы на вопросы и см. какие другие пользователи приложения логики Azure делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp улучшить логику приложений и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Дальнейшие действия

*  Изучите [список соединителей](./apis-list.md) для приложений логики в Azure Logic Apps.