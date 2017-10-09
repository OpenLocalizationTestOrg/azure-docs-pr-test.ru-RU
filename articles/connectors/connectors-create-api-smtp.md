---
title: "Соединитель aaaSMTP в приложения логики Azure | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите tooSMTP toosend по электронной почте."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Приступая к работе с hello соединитель SMTP
Подключите tooSMTP toosend по электронной почте.

toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики. Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Подключение tooSMTP
Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы. Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой. Например, tooconnect tooSMTP, необходимо сначала SMTP *соединения*. toocreate соединения, введите учетные данные hello, обычно используется tooaccess hello службы при подключении. Таким образом в примере hello SMTP введите имя подключения tooyour hello учетные данные, адреса SMTP-сервера и подключение пользователя входа сведения toocreate hello tooSMTP.  

### <a name="create-a-connection-toosmtp"></a>Создание tooSMTP подключения
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Использование триггера SMTP
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

В этом примере, поскольку SMTP не имеет триггер свои собственные, мы будем использовать hello **Salesforce - при создании объекта** триггера. Этот триггер активируется при создании объекта в Salesforce. В нашем примере мы составим его таким образом, что каждый раз создается новый интерес в Salesforce, *письмо* действие выполняется с помощью соединителя hello SMTP уведомление создается новый интерес hello.

1. Введите *salesforce* в поле поиска hello в конструкторе приложений логики hello выберите hello **Salesforce - при создании объекта** триггера.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Hello **при создании объекта** отображается элемент управления.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Выберите hello **тип объекта** выберите *привести* hello списке объектов. На этом шаге вы указываете, что создаете триггер, который будет уведомлять приложение логики о создании интереса в Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. был создан триггер Hello.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Использование действия SMTP
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Теперь, когда hello триггер был добавлен, выполните эти шаги tooadd SMTP действие, которое будет выполняться при создании нового интереса в Salesforce.

1. Выберите **+ новый шаг** действие hello tooadd хотелось бы tootake при создании нового интереса.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Выберите **Добавить действие**. Открывает окна поиска hello поиска для любого действия вы хотели бы tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Введите *smtp* toosearch для tooSMTP связанные действия.  
4. Выберите **SMTP - Отправка сообщения** как hello tootake действие, когда создается новый интерес hello. Открывает блок управления действие Hello. Если вы еще не сделали это будет иметь tooestablish подключения к smtp в блоке конструктора hello.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Входные данные требуемой электронной почты в hello **SMTP - Отправка сообщения** блока.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Сохраните изменения в порядке tooactivate рабочего процесса.  

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Дополнительные сведения о соединителях
Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).
