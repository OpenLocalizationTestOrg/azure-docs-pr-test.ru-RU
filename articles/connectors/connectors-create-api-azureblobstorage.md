---
title: "hello aaaAdd хранилище больших двоичных объектов соединителя в приложениях для логики | Документы Microsoft"
description: "Начало работы и настройка соединителя хранилища BLOB-объектов Azure hello в приложение логики"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Использование соединителя хранилища BLOB-объектов Azure hello в приложение логики
Используйте hello Azure BLOB-объекта хранилища соединитель tooupload обновления, получение и удаление больших двоичных объектов в вашей учетной записи хранения, все в пределах приложения логики.  

Хранилище BLOB-объектов Azure позволяет выполнять следующие действия:

* создавать рабочие процессы, отправляя новые проекты или получая недавно обновленные файлы;
* Используйте метаданные файла tooget действия, удалите файл, копирование файлов и многое другое. Например, при обновлении средства на веб-сайте Azure (триггер) будет обновляться файл в хранилище BLOB-объектов (действие). 

В этом разделе показано, как toouse hello больших двоичных объектов хранилища соединителя в приложение логики.

toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>Подключение tooAzure хранилища больших двоичных объектов
Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы. Таким образом вы установите соединение между приложением логики и другой службой. Например, учетная запись хранения tooa tooconnect сначала создать хранилище BLOB-объектов *соединения*. toocreate соединения, введите учетные данные hello, обычно используется tooaccess hello службы, которому вы подключаетесь. Поэтому с хранилищем Azure, введите toocreate соединение hello tooyour хранилища hello учетные данные учетной записи. 

#### <a name="create-hello-connection"></a>Создайте соединение hello
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Использование триггера
Этот соединитель не содержит триггеров. Использование других триггеров toostart hello логики приложения, например повторения триггера, триггер HTTP веб-перехватчика, триггеры, доступных с другими соединители и многое другое. Пример см. в статье о [создании приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-an-action"></a>Использование действий
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.

1. Выберите hello "плюс". Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Выберите **Добавить действие**.
3. В текстовом поле hello введите «большой двоичный объект» tooget список всех доступных действий hello.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. В этом примере для хранилища BLOB-объектов Azure мы выберем действие **Get file metadata using path** (Получить метаданные файла с помощью пути). Если подключение уже существует, то выберите hello **...** Tooselect кнопку (Показать выбор) файла.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения. [Создайте соединение hello](connectors-create-api-azureblobstorage.md#create-the-connection) в этом разделе описываются эти свойства. 
   
   > [!NOTE]
   > В этом примере мы получаем hello метаданные файла. toosee hello метаданные, добавьте другое действие, которое создает новый файл с помощью другого соединителя. Например добавьте OneDrive действие, которое создает новый файл «test» на основе метаданных hello. 


5. **Сохранить** изменения (левом верхнем углу панели инструментов hello). Приложение логики сохранено и теперь может быть включено автоматически.

> [!TIP]
> [Обозреватель хранилищ](http://storageexplorer.com/) мощный инструмент слишком управление несколькими учетными записями хранения.

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md). Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).

