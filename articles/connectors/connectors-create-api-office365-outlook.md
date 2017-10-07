---
title: "Соединитель Office 365 Outlook aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Для создания логики приложений Office 365 соединитель tooenable взаимодействие с Office 365. Например, он позволяет создавать, редактировать и обновлять контакты и элементы календаря."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Приступая к работе с Office 365 Outlook соединителя hello
Соединитель Office 365 Outlook Hello разрешает взаимодействие с Outlook в Office 365. Используйте этот соединитель toocreate, изменения и обновления контактов и элементы календаря, также получить, отправки и ответ tooemail.

Office 365 Outlook позволяет следующее:

* Сборки рабочего процесса с помощью функций электронной почты и календаря hello в Office 365. 
* Использование триггеров toostart рабочего процесса при наличии новых сообщений электронной почты, при обновлении элемента календаря и многое другое.
* Использовать действия toosend сообщение электронной почты, создайте нового события календаря и многое другое. Например, при наличии нового объекта в Salesforce (триггер), отправить сообщение электронной почты tooyour Outlook Office 365 (действие). 

В этом разделе показано, как toouse hello соединителя Office 365 Outlook в приложение логики, а также списки hello триггеров и действий.

> [!NOTE]
> Эта версия статьи hello применяется tooLogic приложений общедоступной (версии GA).
> 
> 

toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Подключение tooOffice 365
Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы. Таким образом вы установите соединение между приложением логики и другой службой. Например, tooconnect tooOffice 365 Outlook, необходимо сначала Office 365 *соединения*. toocreate соединения, введите учетные данные hello, обычно используется служба hello tooaccess которых надо tooconnect для. Поэтому с Office 365 Outlook, введите tooyour hello учетные данные подключения к hello toocreate учетной записи Office 365.

## <a name="create-hello-connection"></a>Создайте соединение hello
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Использование триггера
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. Триггеры «опрос» hello службы в частоту и интервал. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. В приложение логику hello введите «office 365» tooget список триггеров hello:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Выберите триггер Office 365 Outlook **When an upcoming event is starting soon** (Если приближается время начала предстоящего события). Если подключение уже существует, затем выберите календарь из раскрывающегося списка hello.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Если, запрашиваемые toosign в, а затем введите знак hello в соединении hello toocreate сведения. [Создайте соединение hello](connectors-create-api-office365-outlook.md#create-the-connection) в этом разделе перечислены шаги hello. 
   
   > [!NOTE]
   > В этом примере логика приложения hello выполняются обновления события календаря. результаты hello toosee триггера, добавьте другое действие, которое отправляет вам текстовое сообщение. Например, добавить hello Twilio *отправляемого сообщения* действие, которое запускает текстов, когда hello календарь событий в течение 15 минут. 
   > 
   > 
3. Выберите hello **изменить** кнопку и задайте hello **частоты** и **интервал** значения. Например, если требуется toopoll триггер hello каждые 15 минут, задайте hello **частоты** слишком**минуту**и набор hello **интервал** слишком**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Сохранить** изменения (левом верхнем углу панели инструментов hello). Приложение логики сохранено и теперь может быть включено автоматически.

## <a name="use-an-action"></a>Использование действий
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Выберите hello "плюс". Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Выберите **Добавить действие**.
3. В текстовом поле hello введите «office 365» tooget список всех доступных действий hello.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. В этом примере мы выберем действие Office 365 Outlook **Создание контакта**. Если подключение уже существует, а затем выберите hello **идентификатор папки**, **заданное имя**и другие свойства:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения. [Создайте соединение hello](connectors-create-api-office365-outlook.md#create-the-connection) в этом разделе описываются эти свойства. 
   
   > [!NOTE]
   > В этом примере мы создадим контакт в Office 365 Outlook. Можно использовать результаты из другого триггера toocreate hello контакта. Например, добавить hello SalesForce *при создании объекта* триггера. Затем добавьте hello Office 365 Outlook *создать контакт* действие, которое использует hello SalesForce полей toocreate hello новый новый контакт в Office 365. 
   > 
   > 
5. **Сохранить** изменения (левом верхнем углу панели инструментов hello). Приложение логики сохранено и теперь может быть включено автоматически.

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/office365connector/). 

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md). Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).

