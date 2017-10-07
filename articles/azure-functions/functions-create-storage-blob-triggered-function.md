---
title: "функция в Azure, активируемых хранилища больших двоичных объектов aaaCreate | Документы Microsoft"
description: "Использование функции Azure toocreate данной функции, которая вызывается для элементов добавлен tooAzure хранилища больших двоичных объектов."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Создание функции, активируемой хранилищем BLOB-объектов Azure

Узнайте, как toocreate функции, вызываемые при файлы, загрузить tooor обновляется в хранилище больших двоичных объектов Azure.

![Представление сообщений в журналах hello.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Предварительные требования

+ Загрузите и установите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Подписка Azure. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Создание приложения-функции Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

Создайте функцию в приложение новые функции hello.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Создание функции, активируемой хранилищем BLOB-объектов

1. Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**. Если это первая функция hello в приложении функции, выберите **пользовательские функции**. Откроется hello полный набор шаблонов функций.

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Выберите hello **BlobTrigger** шаблона для нужного языка и использовать параметры hello, как указано в таблице hello.

    ![Создайте функцию запуска хранилища больших двоичных объектов hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Настройка | Рекомендуемое значение | Описание |
    |---|---|---|
    | **Путь**   | mycontainer/{name}    | Расположение в хранилище BLOB-объектов отслеживается. Имя файла Hello hello большого двоичного объекта передается в привязке hello как hello _имя_ параметра.  |
    | **Подключение к учетной записи хранения** | AzureWebJobStorage | Можно использовать уже используется приложением функции подключения к учетной записи хранилища hello или создайте новую.  |
    | **Имя функции** | Уникальное для вашего приложения-функции | Имя функции, активируемой большим двоичным объектом. |

3. Нажмите кнопку **создать** toocreate функции.

Затем подключите учетную запись хранилища Azure tooyour и создать hello **mycontainer** контейнера.

## <a name="create-hello-container"></a>Создание контейнера hello

1. Щелкните **Интегрировать** в своей функции, затем разверните узел **Документация** и скопируйте **имя учетной записи** и **ключ учетной записи**. Можно использовать учетную запись хранения tooconnect toohello эти учетные данные. Если вы уже подключились вашей учетной записи хранилища, пропустите toostep 4.

    ![Получите учетные данные для подключения учетной записи хранилища hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Запустите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) инструмент, нажмите кнопку hello значок слева hello подключения, выберите **использовать имя учетной записи хранения и ключ**и нажмите кнопку **Далее**.

    ![Запустите средство hello обозреватель учетной записи хранилища.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Введите hello **имя учетной записи** и **ключ учетной записи** из шага 1, нажмите кнопку **Далее** и затем **Connect**. 

    ![Введите учетные данные хранилища hello и подключения.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Hello присоединенного учетной записи хранилища, щелкните правой кнопкой **контейнеры больших двоичных объектов**, нажмите кнопку **создать контейнер больших двоичных объектов**, тип `mycontainer`, и нажмите клавишу ВВОД.

    ![Создание очереди службы хранилища](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Теперь, когда контейнер больших двоичных объектов, можно проверить функции hello передав toohello контейнера файлов.

## <a name="test-hello-function"></a>Проверка функции hello

1. Обратно в hello портал Azure, функция tooyour обзора разверните hello **журналы** hello нижней части страницы hello и убедитесь, что не приостановлен, журналов потоковой передачи.

1. В обозревателе хранилищ разверните вашу учетную запись хранения, **Blob containers** (Контейнеры больших двоичных объектов) и **mycontainer**. Щелкните **Отправка**, а затем **Отправка файлов**.

    ![Отправьте файл toohello BLOB-контейнере.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. В hello **передачи файлов** диалоговое окно, нажмите кнопку hello **файлы** поля. Обзор tooa файл на локальном компьютере, таких как файл изображения, выберите его и нажмите кнопку **откройте** и затем **отправить**.

1. Вернитесь к предыдущему окну tooyour журналов функций и убедитесь, что были прочитаны hello большого двоичного объекта.

   ![Представление сообщений в журналах hello.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > При выполнении функции приложения в плане использования по умолчанию hello могут существовать задержки вверх tooseveral минут между hello добавлении или обновлении большого двоичного объекта и hello функции запустилась. Выполняйте свое приложение-функцию в рамках плана службы приложений, если требуется малая задержка в функции, активируемой большим двоичным объектом.

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы создали функцию, которая выполняется при добавлении tooor обновить большой двоичный объект в хранилище больших двоичных объектов. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения о триггерах хранилища BLOB-объектов см.в статье [Привязки больших двоичных объектов службы хранилища для Функций Azure](functions-bindings-storage-blob.md).
