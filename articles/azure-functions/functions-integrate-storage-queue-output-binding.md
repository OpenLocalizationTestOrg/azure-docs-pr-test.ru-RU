---
title: "aaaCreate функции в Azure, активируемых сообщений очереди | Документы Microsoft"
description: "Использовать функции Azure toocreate без сервера функция, вызываемая сообщений отправить tooan очереди службы хранилища Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>Добавление очереди хранилища Azure tooan сообщения, с помощью функции

В функциях Azure привязки ввода-вывода предоставляют декларативным способом tooconnect tooexternal данные службы при помощи функции. В этом разделе рассказано, как tooupdate существующую функцию, добавив выход привязки, которая отправляет сообщения tooAzure очереди хранилища.  

![Представление сообщений в журналах hello.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Предварительные требования 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Установка hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="add-binding"></a>Добавление выходной привязки
 
1. Разверните ваше приложение-функцию и функцию.

2. Выберите **Интегрировать** и **+Новые выходные данные**, а затем выберите **Хранилище очередей Azure** и **Выбрать**.
    
    ![Добавление функции tooa хранения выходных данных очереди привязки в hello портал Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Используйте параметры hello, как указано в таблице hello: 

    ![Добавление функции tooa хранения выходных данных очереди привязки в hello портал Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Настройка      |  Рекомендуемое значение   | Описание                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Имя очереди**   | myqueue-items    | Имя Hello hello очереди tooconnect tooin вашей учетной записи хранилища. |
    | **Подключение к учетной записи хранения** | AzureWebJobStorage | Можно использовать уже используется приложением функции подключения к учетной записи хранилища hello или создайте новую.  |
    | **Имя параметра сообщения** | outputQueueItem | Имя Hello hello выходной параметр привязки. | 

4. Нажмите кнопку **Сохранить** tooadd hello привязки.
 
Теперь, когда выходные данные привязки, определенной необходима tooupdate toouse кода hello hello привязки tooa сообщения tooadd очередь.  

## <a name="update-hello-function-code"></a>Изменения кода hello

1. Выберите код функции hello toodisplay функции в редакторе hello. 

2. Для функции C#, обновите определение функции следующим образом: tooadd hello **outputQueueItem** параметр привязки хранилища. Пропустите этот шаг для функции JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Добавьте следующие функции toohello кода непосредственно перед методом hello hello. Используйте соответствующий фрагмент hello для языка hello этой функции.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. Выберите **Сохранить** toosave изменений.

Hello значению, переданному в toohello HTTP триггер включается в добавленных toohello очереди сообщений.
 
## <a name="test-hello-function"></a>Проверка функции hello 

1. После сохранения изменений кода hello выберите **запуска**. 

    ![Добавление функции tooa хранения выходных данных очереди привязки в hello портал Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Проверьте функции hello успешно toomake журналы hello. Новая очередь с именем **outqueue** по функции среды выполнения, когда привязка для вывода hello сначала используется hello создается в вашей учетной записи хранилища.

Затем можно подключить приветственное сообщение, что вы добавили tooit и tooyour хранилища учетной записи tooverify hello новая очередь. 

## <a name="connect-toohello-queue"></a>Подключение toohello очереди

Пропустить hello первых трех шагов, если вы уже установили обозреватель хранилищ и соединения его tooyour учетной записи хранилища.    

1. В функции, выберите **Интеграция** и новый hello **хранилища очередей Azure** выходной привязки, а затем разверните **документации**. Скопируйте **имя учетной записи** и **ключ учетной записи**. Можно использовать учетную запись хранения tooconnect toohello эти учетные данные.
 
    ![Получите учетные данные для подключения учетной записи хранилища hello.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Запустите hello [обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/) средство, выберите hello значок слева hello подключения, выберите **использовать имя учетной записи хранения и ключ**и выберите **Далее**.

    ![Запустите средство hello обозреватель учетной записи хранилища.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Вставить hello **имя учетной записи** и **ключ учетной записи** из шага 1 в их соответствующие поля, а затем выберите **Далее**, и **Connect**. 
  
    ![Вставьте учетные данные хранилища hello и подключения.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Разверните узлы hello присоединенного учетной записи хранилища, **очереди** и убедитесь, что очередь с именем **myqueue элементы** существует. Вы также увидите сообщение уже находится в очереди hello.  
 
    ![Создание очереди службы хранилища](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы добавили существующей функции tooan выходные данные привязки. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения о хранении tooQueue привязки см. в разделе [привязки очереди хранилища Azure функции](functions-bindings-storage-queue.md). 



