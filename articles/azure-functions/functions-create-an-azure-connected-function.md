---
title: "aaaCreate функцию, которая подключается tooAzure services | Документы Microsoft"
description: "Использовать функции Azure toocreate без сервера приложение, которое подключается tooother Azure службы."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Использовать функции Azure toocreate функцию, которая подключается tooother Azure службы

В этом разделе показано, как функции в функции Azure, ожидающий toomessages на хранилища Azure, очереди и копии hello toocreate сообщения toorows в таблице хранилища Azure. Таймер запускается функция является используется tooload сообщения в очередь hello. Вторая функция считывает из очереди hello и записывает сообщения toohello таблицы. Hello очереди и таблицы hello создаются автоматически на основе hello привязки определений функций Azure. 

наиболее интересных вещей toomake, одна функция написан на языке JavaScript и другие hello записывается в скрипт C#. На этом примере показано, что приложение-функция может содержать функции на разных языках. 

Этот сценарий можно просмотреть в [видеоролике на сайте Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Создайте функцию, которая записывает toohello очереди

Перед подключением tooa очередь хранилища необходимо toocreate функцию, которая загружает очереди сообщений hello. Эта функция JavaScript использует триггер таймера, который записывает toohello очереди сообщений каждые 10 секунд. Если у вас еще нет учетной записи Azure, извлечь hello [повторите функции Azure](https://functions.azure.com/try) возникают, или [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/).

1. Вернитесь к toohello портал Azure и найдите функции приложения.

2. Щелкните **Новая функция** > **TimerTrigger-JavaScript**. 

3. Имя функции hello **FunctionsBindingsDemo1**, введите значение выражения cron `0/10 * * * * *` для **расписания**, а затем нажмите кнопку **создать**.
   
    ![Добавление функции, активируемой с помощью таймера](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    Вы создали функцию, активируемую с помощью таймера, которая запускается каждые 10 секунд.

5. На hello **разработка** щелкните **журналы** и просмотреть в журнале hello hello. Каждые 10 секунд в журнале будет появляться запись.
   
    ![Просмотр работы функции hello tooverify журнала hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Добавление выходной привязки очереди сообщений

1. На hello **Интеграция** выберите **новый Выход** > **хранилища очередей Azure** > **выберите**.

    ![Добавление функции триггера с таймером](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Введите `myQueueItem` для **имя параметра сообщение** и `functions-bindings` для **имя очереди**, выберите существующую **подключения к учетной записи хранилища** или нажмите кнопку **новый** toocreate хранилища учетной записи подключения и нажмите кнопку **Сохранить**.  

    ![Создание hello выходные данные привязки toohello хранилища очереди](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Вернитесь в hello **разработка** вкладку, добавьте следующие функции toohello кода hello:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Найдите hello *Если* инструкции около строки 9 функции hello и вставки hello следующий код после этого оператора.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Этот код создает **myQueueItem** и задает его **время** Текущая отметка времени toohello свойство. Затем он добавляет hello новой очереди toohello контекстного элемента **myQueueItem** привязки.

3. Щелкните **Сохранить и запустить**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Просмотр обновлений хранилища с помощью обозревателя службы хранилища
Можно проверить работоспособность функции, просматривая сообщения в очереди hello, которую вы создали.  Очередь хранилища tooyour можно подключиться с помощью Cloud Explorer в Visual Studio. Однако портал hello делает его учетной записи хранилища tooyour легко tooconnect, используя обозреватель хранилищ Microsoft Azure.

1. В hello **Интеграция** щелкните очереди привязка для вывода > **документации**, Показать hello строку подключения для вашей учетной записи хранилища и скопируйте значение hello. Можно использовать учетную запись хранения tooconnect tooyour это значение.

    ![Скачивание обозревателя службы хранилища Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Если это еще не сделано, скачайте и установите [обозреватель службы хранилища Microsoft Azure](http://storageexplorer.com). 
 
3. В обозревателе хранилищ щелкните hello tooAzure хранилища значок подключения, вставьте строку подключения hello в поле hello и мастером hello.

    ![Добавление подключения в обозревателе службы хранилища](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. В разделе **локальной и вложенных**, разверните **учетные записи хранения** > учетной записи хранилища > **очереди** > **функции привязок**и убедитесь, что сообщения записываются toohello очереди.

    ![Представление сообщений в очереди hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Hello очередь не существует или является пустым, существует ли скорее проблема с привязка функции или кода.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Создайте функцию, которая считывает из очереди hello

Теперь, когда добавляется toohello очереди сообщений, можно создать другую функцию, которая считывает из очереди hello и hello записи без возможности восстановления сообщения tooan таблице хранилища Azure.

1. Щелкните **Новая функция** > **QueueTrigger-CSharp**. 
 
2. Имя функции hello `FunctionsBindingsDemo2`, введите **функции привязок** в hello **имя очереди** поля, выберите существующую учетную запись хранения или создайте его и нажмите кнопку **создать**.

    ![Добавление функции таймера выходной очереди](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Необязательно) Можно проверить работоспособность новой функции hello, просмотрев hello новую очередь в обозревателе хранилищ как перед. Кроме того, можно использовать Cloud Explorer в Visual Studio.  

4. (Необязательно) Обновить hello **функции привязок** очередь и обратите внимание, что элементы были удалены из очереди hello. Hello удаления возникает из-за функции hello привязанного toohello **функции привязок** очередь, так как очередь hello считывает входной функции триггер и hello. 
 
## <a name="add-a-table-output-binding"></a>Добавление выходной привязки таблицы

1. В FunctionsBindingsDemo2 щелкните **Интегрировать** > **Новые выходные данные** > **Хранилище таблиц Azure** > **Выбрать**.

    ![Добавление таблицы привязки tooan хранилища Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Введите `functionbindings` в поле **Имя таблицы** и `myTable` — в поле **Имя параметра таблицы**, выберите **подключение к учетной записи хранения** или создайте его и нажмите кнопку **Сохранить**.

    ![Настройка привязки таблицы хранилища hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. В hello **разработка** вкладки, замените существующий код функции hello hello следующее:
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Hello **TableItem** класса представляет строку в таблицу хранилища hello и добавить элемент toohello hello `myTable` коллекцию **TableItem** объектов. Необходимо задать hello **PartitionKey** и **RowKey** свойства toobe может tooinsert в таблицу hello.

4. Щелкните **Сохранить**.  Наконец можно проверить работы функции hello, просмотреть таблицу hello в обозреватель хранилищ или Visual Studio Cloud Explorer.

5. (Необязательно) В вашей учетной записи хранения в обозревателе хранилищ разверните **таблиц** > **functionsbindings** и убедитесь, что toohello таблицы добавляются строки. Можно сделать же hello в Cloud Explorer в Visual Studio.

    ![Просмотр строк в таблице hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Hello таблицы не существует или является пустым, существует ли скорее проблема с привязка функции или кода. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о функциях Azure см. в разделе hello следующие вопросы:

* [Справочник разработчика по функциям Azure](functions-reference.md)  
  Справочник программиста по созданию функций, а также определению триггеров и привязок.
* [Testing Azure Functions](functions-test-a-function.md)  
  (Тестирование функций Azure) Описание различных средств и методов тестирования функций.
* [Как tooscale функции Azure](functions-scale.md)  
  Описание функций Azure, включая план размещения потребления hello и как toochoose hello продуманный план планов обслуживания. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

