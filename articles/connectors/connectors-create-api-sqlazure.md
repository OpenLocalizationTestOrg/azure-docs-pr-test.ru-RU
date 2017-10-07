---
title: "Соединитель базы данных SQL Azure aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Обзор соединителя базы данных SQL Azure с параметрами интерфейса REST API"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Начало работы с соединителем hello базы данных SQL Azure
С помощью соединителя hello базы данных SQL Azure, создайте рабочие процессы для вашей организации, работающие с данными в таблицах. 

С помощью базы данных SQL вы можете:

* Сборки рабочего процесса, добавив новую базу данных клиентам tooa клиента или обновления заказа в базе данных заказов.
* Используйте действия tooget строки данных, вставить новую строку и даже удалять. Например, при создании записи в Dynamics CRM Online (триггер) может вставляться строка в базу данных SQL Azure (действие). 

В этом разделе показано, как toouse hello соединителю базы данных SQL в приложении логику, а также списки hello действия.

toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Подключение tooAzure базы данных SQL
Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы. Таким образом вы установите соединение между приложением логики и другой службой. Например, tooSQL tooconnect базы данных, создания базы данных SQL *соединения*. toocreate подключения введите hello учетные данные, обычно используемые tooaccess hello службы, которому вы подключаетесь. Таким образом в базе данных SQL, введите подключение hello toocreate учетные данные базы данных SQL. 

#### <a name="create-hello-connection"></a>Создайте соединение hello
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Использование триггера
Этот соединитель не содержит триггеров. Использование других триггеров toostart hello логики приложения, например повторения триггера, триггер HTTP веб-перехватчика, триггеры, доступных с другими соединители и многое другое. Пример см. в статье о [создании приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-an-action"></a>Использование действий
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Выберите hello "плюс". Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Выберите **Добавить действие**.
3. В текстовом поле hello введите «sql» tooget список всех доступных действий hello.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. В нашем примере мы выберем действие для SQL Server **Get row** (Получение строки). Если подключение уже существует, то выберите hello **имя таблицы** hello раскрывающемся списке, а затем введите hello **идентификатор строки** требуется tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения. [Создайте соединение hello](connectors-create-api-sqlazure.md#create-the-connection) в этом разделе описываются эти свойства. 
   
   > [!NOTE]
   > В этом примере строка возвращается из таблицы. toosee hello данных в этой строке, добавьте другое действие, которое создает файл с помощью hello поля из таблицы hello. Например добавьте OneDrive действие, которое использует hello FirstName и LastName поля toocreate в новом файле в hello учетная запись облачного хранилища. 
   > 
   > 
5. **Сохранить** изменения (левом верхнем углу панели инструментов hello). Приложение логики сохранено и теперь может быть включено автоматически.

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/sql/). 

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md). Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).

