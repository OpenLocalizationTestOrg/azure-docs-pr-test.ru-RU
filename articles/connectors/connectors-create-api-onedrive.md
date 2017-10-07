---
title: "Соединитель OneDrive aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Обзор соединителя hello OneDrive с параметрами REST API"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Начало работы с соединителем OneDrive hello
Подключите tooOneDrive toomanage файлов, отправки, get, удалите файлы и многое другое. 

С помощью OneDrive вы можете: 

* создавать рабочие процессы, сохраняя файлы в OneDrive, или обновлять имеющиеся файлы; 
* Используйте триггеры toostart рабочего процесса, если файл создается или обновляется в OneDrive.
* Используйте действия toocreate файл, удалите файл и многое другое. Например, после получения нового сообщения электронной почты Office 365 с вложением (триггер) может создаваться файл в OneDrive (действие).

В этом разделе показано, как toouse hello соединитель OneDrive в приложение логики, а также списки hello триггеров и действий.

toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Подключение tooOneDrive
Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы. Таким образом вы установите соединение между приложением логики и другой службой. Например, tooconnect tooOneDrive, необходимо сначала OneDrive *соединения*. toocreate соединения, введите учетные данные hello, обычно используется служба hello tooaccess которых надо tooconnect для. Таким образом OneDrive, введите hello учетные данные tooyour OneDrive toocreate hello подключения к учетной записи.

### <a name="create-hello-connection"></a>Создайте соединение hello
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Использование триггера
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. Триггеры «опрос» hello службы в частоту и интервал. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. В приложение логику hello введите «onedrive» tooget список триггеров hello:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Выберите триггер **When a file is modified** (При изменении файла). Если подключение уже существует, выберите tooselect кнопку hello Показать выбора папки.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Если, запрашиваемые toosign в, а затем введите знак hello в соединении hello toocreate сведения. [Создайте соединение hello](connectors-create-api-onedrive.md#create-the-connection) в этом разделе перечислены шаги hello. 
   
   > [!NOTE]
   > В этом примере логика приложения hello выполняется при создании файла в папке hello по выбору обновляется. результаты hello toosee триггера, добавьте другое действие, которое отправляет вам сообщение электронной почты. Например, добавить hello Office 365 Outlook *отправить сообщение электронной почты* действие, которое сообщение электронной почты, при обновлении файла. 

3. Выберите hello **изменить** кнопку и задайте hello **частоты** и **интервал** значения. Например, если требуется toopoll триггер hello каждые 15 минут, задайте hello **частоты** слишком**минуту**и набор hello **интервал** слишком**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Сохранить** изменения (левом верхнем углу панели инструментов hello). Приложение логики сохранено и теперь может быть включено автоматически.

## <a name="use-an-action"></a>Использование действий
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Выберите hello "плюс". Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Выберите **Добавить действие**.
3. В текстовом поле hello введите «onedrive» tooget список всех доступных действий hello.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. В этом примере для OneDrive мы выберем действие **Создать файл**. Если подключение уже существует, то выберите hello **путь к папке** tooput hello, введите hello **имя файла**и выберите hello **содержимое файла** необходимо:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения. [Создайте соединение hello](connectors-create-api-onedrive.md#create-the-connection) в этом разделе описываются эти свойства. 
   
   > [!NOTE]
   > В этом примере мы создадим файл в папке OneDrive. Можно использовать результаты из другого файла OneDrive hello toocreate триггера. Например, добавить hello Office 365 Outlook *при поступлении новой почты* триггера. Затем добавьте hello OneDrive *создать файл* действие, которое использует hello вложений и Content-Type поля внутри ForEach toocreate hello новый файл в OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Сохранить** изменения (левом верхнем углу панели инструментов hello). Приложение логики сохранено и теперь может быть включено автоматически.


## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Дополнительные сведения о соединителях
Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).
