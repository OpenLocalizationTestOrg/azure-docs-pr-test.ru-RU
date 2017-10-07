---
title: "aaaCreate функции в Azure, активируемых сообщений очереди | Документы Microsoft"
description: "Использовать функции Azure toocreate без сервера функция, вызываемая сообщений отправить tooan очереди службы хранилища Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Создание функции, активируемой хранилищем очередей Azure

Узнайте, как toocreate функции, вызываемые при сообщения, отправленные tooan очереди службы хранилища Azure.

![Представление сообщений в журналах hello.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Предварительные требования

- Загрузите и установите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

- Подписка Azure. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Создание приложения-функции Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

Создайте функцию в приложение новые функции hello.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Создание функции, активируемой очередью

1. Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**. Если это первая функция hello в приложении функции, выберите **пользовательские функции**. Откроется hello полный набор шаблонов функций.

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Выберите hello **QueueTrigger** шаблона для нужного языка и использовать параметры hello, как указано в таблице hello.

    ![Создание функции активации очереди хранилища hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Настройка | Рекомендуемое значение | Описание |
    |---|---|---|
    | **Имя очереди**   | myqueue-items    | Имя hello очереди tooconnect tooin вашей учетной записи хранилища. |
    | **Подключение к учетной записи хранения** | AzureWebJobStorage | Можно использовать уже используется приложением функции подключения к учетной записи хранилища hello или создайте новую.  |
    | **Имя функции** | Уникальное для вашего приложения-функции | Имя функции, активируемой очередью. |

3. Нажмите кнопку **создать** toocreate функции.

Затем подключите учетную запись хранилища Azure tooyour и создать hello **myqueue элементы** очереди хранилища.

## <a name="create-hello-queue"></a>Создать очередь hello

1. Щелкните **Интегрировать** в своей функции, затем разверните узел **Документация** и скопируйте **имя учетной записи** и **ключ учетной записи**. Можно использовать учетную запись хранения tooconnect toohello эти учетные данные. Если вы уже подключились вашей учетной записи хранилища, пропустите toostep 4.

    ![Получите учетные данные для подключения учетной записи хранилища hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Запустите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) инструмент, нажмите кнопку hello значок слева hello подключения, выберите **использовать имя учетной записи хранения и ключ**и нажмите кнопку **Далее**.

    ![Запустите средство hello обозреватель учетной записи хранилища.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Введите hello **имя учетной записи** и **ключ учетной записи** из шага 1, нажмите кнопку **Далее** и затем **Connect**.

    ![Введите учетные данные хранилища hello и подключения.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Hello присоединенного учетной записи хранилища, щелкните правой кнопкой **очереди**, нажмите кнопку **создать очередь**, тип `myqueue-items`, и нажмите клавишу ВВОД.

    ![Создание очереди службы хранилища](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Теперь, когда очередь хранилища можно проверить функции hello, добавив toohello очереди сообщений.

## <a name="test-hello-function"></a>Проверка функции hello

1. Обратно в hello портал Azure, функция tooyour обзора разверните hello **журналы** hello нижней части страницы hello и убедитесь, что не приостановлен, журналов потоковой передачи.

1. Разверните свою учетную запись в обозревателе хранилищ, узел **Очереди** и **myqueue-items**, а затем щелкните **Add message** (Добавить сообщение).

    ![Добавьте toohello очереди сообщений.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. Введите сообщение Hello World в поле **Текст сообщения** и щелкните **ОК**.

1. Подождите несколько секунд, а затем вернитесь tooyour журналов функций и убедитесь, что новые сообщения hello уже считаны из очереди hello.

    ![Представление сообщений в журналах hello.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. Назад в обозреватель хранилищ щелкните **обновление** и убедитесь, что приветственное сообщение было обработано и hello очереди больше не.

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы создали функцию, которая выполняется при добавлении tooa хранилища очереди сообщений.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения о триггерах хранилища очередей см. в статье [Привязки очередей службы хранилища для Функций Azure](functions-bindings-storage-queue.md).