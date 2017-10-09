---
title: "aaaSave концентратор IoT сообщений хранения данных tooAzure | Документы Microsoft"
description: "Используйте приложение Azure функция toosave вашей tooyour сообщений концентратора IoT табличного хранилища Azure. Hello IoT hub сообщения содержат сведения, такие как данные датчика, отправленные с вашего устройства IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "хранилище данных Центра Интернета вещей, хранилище для данных датчиков Центра Интернета вещей"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Сохранить сообщения концентратора IoT, содержащие датчиков данных tooyour табличного хранилища Azure

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Что вы узнаете

Вы узнаете, как toocreate учетную запись хранилища Azure и Azure функцию сообщения концентратора IoT toostore приложения в хранилище таблиц.

## <a name="what-you-do"></a>В рамках этого руководства мы:

- Создайте учетную запись хранения Azure.
- Подготовьте ваш центр IoT сообщений tooread подключения.
- Создайте приложение-функцию Azure и разверните его.

## <a name="what-you-need"></a>Необходимые элементы

- [Настройка устройства](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover следующие требования:
  - активная подписка Azure;
  - Центр Интернета вещей в подписке; 
  - Приложения, отправляющего сообщения tooyour IoT hub

## <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure

1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **хранения** > **учетной записи хранилища**  >   **Создание**.

2. Введите hello необходимые сведения для учетной записи хранения hello.

   ![Создать учетную запись хранилища в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Имя**: hello имя учетной записи хранения hello. Hello имя должно быть глобально уникальным.

   * **Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.

   * **ПИН-код toodashboard**: выберите этот параметр для облегчения доступа центра IoT tooyour из панели мониторинга hello.

3. Щелкните **Создать**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Подготовка концентратор IoT сообщений tooread подключения

Центр IoT представлено встроенные события концентратора совместимой конечной точки tooenable приложений tooread IoT hub сообщений. В то же время приложения используют потребителя данных tooread групп из вашего центра IoT. Перед созданием Azure функций приложения tooread данных-концентратор IoT hello следующие:

- Получите строку hello подключения из вашей конечной точки центра IoT.
- создать группу потребителей для Центра Интернета вещей.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>Получить строку hello подключения из вашей конечной точки центра IoT

1. Откройте Центр Интернета вещей.

2. На hello **центр IoT** панели в разделе **обмен сообщениями**, нажмите кнопку **конечные точки**.

3. В hello правой панели в разделе **встроенных конечных точек**, нажмите кнопку **события**.

4. В hello **свойства** области, Примечание hello следующие значения:
   - конечная точка, совместимая с концентратором событий;
   - имя, совместимое с концентратором событий.

   ![Получить строку подключения к конечной точки центра IoT hello в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. В hello **центр IoT** панели в разделе **параметры**, нажмите кнопку **политики общего доступа**.

6. Щелкните **iothubowner**.

7. Примечание hello **первичного ключа** значение.

8. Создайте hello строка подключения к конечной точки центра IoT следующим образом:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Замените `<Event Hub-compatible endpoint>` и `<Primary key>` со значениями hello, записанные ранее.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Создание группы потребителей для Центра Интернета вещей

1. Откройте Центр Интернета вещей.

2. В hello **центр IoT** панели в разделе **обмен сообщениями**, нажмите кнопку **конечные точки**.

3. В hello правой панели в разделе **встроенных конечных точек**, нажмите кнопку **события**.

4. В hello **свойства** панели в разделе **групп потребителей**, введите имя, а затем запишите его.

5. Щелкните **Сохранить**.

## <a name="create-and-deploy-an-azure-function-app"></a>Создание и развертывание приложения-функции Azure

1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **вычислений** > **функции приложения**  >   **Создание**.

2. Введите необходимые сведения hello для функции приложение hello.

   ![Создание приложения функции в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Имя приложения**: hello имя функции приложение hello. Hello имя должно быть глобально уникальным.

   * **Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.

   * **Учетная запись хранения**: hello созданной учетной записи хранилища.

   * **ПИН-код toodashboard**: выберите этот параметр для приложения функции toohello простой доступ из панели мониторинга hello.

3. Щелкните **Создать**.

4. После создания функции приложение hello, откройте его.

5. В приложении функции hello создайте новую функцию, выполнив hello ниже:

   а. Щелкните **Новая функция**.

   b. Для параметра **Язык** выберите **JavaScript**, а для **Сценарий** — **Обработка данных**.

   c. Щелкните **Создайте эту функцию**, а затем — выберите **Новая функция**.

   d. Выберите **JavaScript** для языка hello и **обработки данных** для сценария hello.

   д. Нажмите кнопку hello **EventHubTrigger JavaScript** шаблона.

   f. Введите необходимые сведения hello для шаблона hello.

      * **Имя функции**: hello имя функции hello.

      * **Имя концентратора событий**: hello события концентратора совместимое имя, записанное ранее.

      * **Подключение концентратора событий**: щелкните строку подключения hello tooadd hello IoT hub созданной конечной точке, **New**.

   ж. Щелкните **Создать**.

6. Настройка выхода функции hello, выполнив hello ниже:

   а. Щелкните **Интегрировать** > **Новое выходное значение** > **Хранилище таблиц Azure** > **Выбрать**.

      ![Добавление таблицы хранилища tooyour функции приложения в hello портал Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Введите необходимые сведения hello.

      * **Имя параметра таблицы**: использование `outputTable`, который будет использоваться в hello Azure кода функции.
      
      * **Имя таблицы**. Используйте `deviceData`.

      * **Подключение к учетной записи хранения**. Щелкните **Новые** и выберите или введите свою учетную запись хранения. Если учетная запись хранения hello не отображается, см. раздел [требования к учетной записи хранилища](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Щелкните **Сохранить**.

7. В разделе **Триггеры** щелкните **Концентратор событий Azure (eventHubMessages)**.

8. В разделе **группы потребителей концентратора событий**, введите имя группы потребителей hello, который был создан и нажмите кнопку hello **Сохранить**.

9. Нажмите кнопку функции hello, созданный для hello слева, а затем нажмите кнопку **Просмотр файлов** на hello вправо.

10. Замените код hello в `index.js` hello следующее:

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. Щелкните **Сохранить**.

Вы создали приложение функции hello. Приложение-функция сохраняет сообщения, которые получает Центр Интернета вещей в хранилище таблиц.

> [!NOTE]
> Можно использовать hello **запуска** приложение функции hello tootest кнопки. При нажатии кнопки **запуска**, отправлено тестовое сообщение hello tooyour центр IoT. Hello прибытия сообщения hello следует активировать toostart приложения hello функции, а затем сохраните хранилище таблиц tooyour сообщение hello. Hello **журналы** области Подробности hello hello процесса.

## <a name="verify-your-message-in-your-table-storage"></a>Проверка сообщений в хранилище таблиц

1. Запустите образец приложения hello на концентратор IoT tooyour устройства toosend сообщений.

2. [Скачайте и установите обозреватель хранилищ Azure](http://storageexplorer.com/).

3. Откройте обозреватель хранилищ, щелкните **добавьте учетную запись Azure** > **вход**и выполните вход в tooyour учетная запись Azure.

4. Щелкните подписку Azure > **Учетные записи хранения** > ваша учетная запись хранения > **Таблицы** > **deviceData**.

   Вы увидите сообщений, отправленных из вашего центра IoT tooyour устройства вход hello `deviceData` таблицы.

## <a name="next-steps"></a>Дальнейшие действия

Вы успешно создали учетную запись хранения Azure и приложение-функцию Azure, которое сохраняет сообщения, поступающие в Центр Интернета вещей, в хранилище таблиц.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
