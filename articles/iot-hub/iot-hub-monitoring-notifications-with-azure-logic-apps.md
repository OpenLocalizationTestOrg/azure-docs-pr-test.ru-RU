---
title: "удаленный мониторинг aaaIoT и уведомлений с приложениями логики Azure | Документы Microsoft"
description: "Использование приложения логики Azure IoT температуры отслеживания на ваш центр IoT и автоматически отправлять почтовому ящику tooyour уведомления для любых аномалий обнаружил."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "мониторинг Центра Интернета вещей, уведомления Центра Интернета вещей, мониторинг температуры в Центре Интернета вещей"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Удаленный мониторинг и отправка уведомлений в Центре Интернета вещей с помощью службы Azure Logic Apps, обеспечивающей подключение между Центром Интернета вещей и почтовым ящиком

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Приложения логики Azure предоставляет способ tooautomate процессы, так как последовательность шагов. Приложение логики поддерживает подключение к различным службам по различным протоколам. Сначала в нем срабатывает триггер, например "При добавлении учетной записи", а затем выполняется набор действий, например "отправка push-уведомления". Благодаря этой функции Logic Apps, помимо прочего, идеально подходит для мониторинга Центра Интернета вещей, например оповещения об аномалиях.

## <a name="what-you-learn"></a>Что вы узнаете

Вы узнаете, как toocreate приложения логики, который подключается ваш центр IoT и почтового ящика для мониторинга температуры и уведомлений. При hello температуры выше 30 C hello метки приложение клиента `temperatureAlert = "true"` в приветственное сообщение, он отправляет tooyour центр IoT. приветственное сообщение, триггеры hello toosend логику приложения вам уведомление по электронной почте.

## <a name="what-you-do"></a>В рамках этого руководства мы:

* Создайте пространство имен служебной шины и добавьте tooit очереди.
* Добавьте конечную точку и маршрутизации центра IoT tooyour правила.
* Создадим, настроим и протестируем приложение логики.

## <a name="what-you-need"></a>Необходимые элементы

* Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:
  * Активная подписка Azure.
  * Центр Интернета вещей Azure в подписке;
  * Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Создайте пространство имен шины обслуживания и добавьте tooit очереди

### <a name="create-a-service-bus-namespace"></a>Создание пространства имен служебной шины

1. На hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **интеграцию** > **Service Bus**.
1. Укажите hello следующую информацию:

   **Имя**: hello имя hello служебной шины.

   **Ценовая категория**. Щелкните **Базовая** > **Выбрать**. для этого учебника, достаточно Hello базового уровня.

   **Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.

   **Расположение**: используйте hello же местоположения, которое использует ваш центр IoT.
1. Щелкните **Создать**.

   ![Создать пространство имен служебной шины в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Добавление очереди служебной шины

1. Откройте hello пространства имен шины обслуживания и нажмите кнопку **+ очередь**.
1. Введите имя для очереди hello и нажмите кнопку **создать**.
1. Откройте очередь service bus hello и нажмите кнопку **политики общего доступа** > **+ добавить**.
1. Введите имя для политики hello, проверка **управление**, а затем нажмите кнопку **создать**.

   ![Добавить очередь служебной шины в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Добавить конечную точку и маршрутизации центра IoT tooyour правило

### <a name="add-an-endpoint"></a>Добавление конечной точки

1. Откройте Центр Интернета вещей и щелкните "Конечные точки > + Добавить".
1. Введите hello следующую информацию:

   **Имя**: hello имя конечной точки hello.

   **Тип конечной точки**. Выберите **Очередь служебной шины**.

   **Пространство имен служебной шины**: выберите созданную имен hello.

   **Очередь Service Bus**: hello выберите очереди, вы создали.
1. Нажмите кнопку **ОК**.

   ![Добавление конечной точки центра IoT tooyour в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Добавление правила маршрутизации

1. В Центре Интернета вещей щелкните **Маршруты** > **+ Добавить**.
1. Введите hello следующую информацию:

   **Имя**: hello имя правила маршрутизации hello.

   **Источник данных**. Выберите **DeviceMessages**.

   **Конечная точка**: выберите созданную конечную точку hello.

   **Строка запроса**. Введите `temperatureAlert = "true"`.
1. Щелкните **Сохранить**.

   ![Добавление правила маршрутизации в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Создание и настройка приложения логики

### <a name="create-a-logic-app"></a>Создайте приложение логики

1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **New** > **интеграцию** > **приложения логики**.
1. Введите hello следующую информацию:

   **Имя**: hello имя hello логику приложения.

   **Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.

   **Расположение**: используйте hello же местоположения, которое использует ваш центр IoT.
1. Щелкните **Создать**.

### <a name="configure-hello-logic-app"></a>Настройка логики приложения hello

1. Откройте приложение hello логику, которая открывается в конструкторе логики приложения hello.
1. В hello конструктора логики приложения, щелкните **пустое приложение логики**.

   ![Начать с пустой логику приложения в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Щелкните **Служебная шина**.

   ![Выберите Создание логику приложения в hello портал Azure toostart Service Bus](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Щелкните **Служебная шина — Когда одно или несколько сообщений поступает в очередь (автозавершение)**.
1. Создайте подключение к служебной шине.
   1. Введите имя подключения.
   1. Выберите пространство имен шины обслуживания hello > Здравствуйте service bus политики > **создать**.

      ![Создание подключения service bus логику приложения в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Нажмите кнопку **Продолжить** после создания подключения service bus hello.
   1. Выберите очередь hello, созданный и введите `175` для **максимальное количество сообщений**

      ![Укажите число максимальное сообщение hello для подключения service bus hello в приложении логики](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Нажмите кнопку «Сохранить» hello toosave кнопке изменится.

1. Создайте подключение к службе SMTP.
   1. Выберите **Новый шаг** > **Добавить действие**.
   1. Тип `SMTP`, нажмите кнопку hello **SMTP** службы в результате поиска hello и нажмите кнопку **SMTP - Отправка сообщения**.

      ![Создание соединения SMTP в приложении логику в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Введите сведения hello SMTP почтового ящика и нажмите кнопку **создать**.

      ![Введите сведения о подключении к SMTP в приложении логику в hello портал Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Получить сведения о hello SMTP для [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), и [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).
   1. Введите адрес электронной почты в полях **От** и **Кому** и укажите `High temperature detected` в **теме** и **тексте сообщения**.
   1. Щелкните **Сохранить**.

приложение Hello логика находится в рабочем состоянии, при его сохранении.

## <a name="test-hello-logic-app"></a>Приложения логики теста hello

1. Запустите клиентское приложение hello развертываемой tooyour устройство в [tooAzure ESP8266 подключения центр IoT](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Увеличить температуры среды hello вокруг toobe SensorTag hello выше 30 C. Например легкий свечи вокруг вашего SensorTag.
1. Вы получите уведомление по электронной почте, отправленных hello логику приложения.

   > [!NOTE]
   > Поставщик услуг электронной почты может потребоваться tooverify hello отправителя удостоверения toomake том, что кто отправляет электронное сообщение hello.

## <a name="next-steps"></a>Дальнейшие действия

Вы успешно создали приложение логики, обеспечивающее подключение между Центром Интернета вещей и почтовым ящиком для мониторинга температуры и отправки уведомлений.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
