---
title: "Визуализация данных во время aaaReal датчиков данных из центра IoT Azure — Power BI | Документы Microsoft"
description: "Используйте Power BI toovisualize температуры и влажности данные, полученные от датчика hello и отправляются tooyour центр Azure IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "визуализация данных, полученных в реальном времени, визуализация интерактивных данных, визуализация данных датчиков"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Визуализация данных, поступающих от датчиков в реальном времени, из Центра Интернета вещей с помощью Power BI

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Что вы узнаете

Вы узнаете, как toovisualize в режиме реального времени датчиков, получающий ваш центр Azure IoT по Power BI. Если вы хотите tootry визуализации данных hello в концентратор IoT с веб-приложений, см. в разделе [веб-приложениях Azure используйте toovisualize в режиме реального времени датчиков из центра IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>В рамках этого руководства мы:

- добавим группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей;
- Создать, настроить и запустить задание Stream Analytics для передачи данных из вашего tooyour концентратора IoT учетной записи Power BI.
- Создание и публикация данных hello toovisualize отчета Power BI.

## <a name="what-you-need"></a>Необходимые элементы

- Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:
  - Активная подписка Azure.
  - Центр Интернета вещей Azure в подписке;
  - Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.
- Учетная запись Power BI. Доступна [бесплатная пробная версия](https://powerbi.microsoft.com/).

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Создание, настройка и выполнение заданий Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics

1. В hello портал Azure, нажмите кнопку Создать > Интернета вещей > задания Stream Analytics.
1. Введите следующую информацию для задания hello hello.

   **Имя задания**: hello имя задания hello. Hello имя должно быть глобально уникальным.

   **Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.

   **Расположение**: используйте hello же расположении, что и группы ресурсов.

   **ПИН-код toodashboard**: Установите этот флажок для центра IoT tooyour простой доступ из панели мониторинга hello.

   ![Создание задания Stream Analytics в Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Щелкните **Создать**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Добавьте задание Stream Analytics входного toohello

1. Задание Stream Analytics откройте hello.
1. В разделе **Топология задания** щелкните **Входные данные**.
1. В hello **входные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:

   **Входной псевдоним**: hello уникальный псевдоним для hello входных данных.

   **Источник**. Выберите **Центр Интернета вещей**.

   **Группа потребителей**: только что созданную группу потребителей выберите hello.
1. Щелкните **Создать**.

   ![Добавить задание Stream Analytics ввода tooa в Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Добавление выходных данных задания Stream Analytics toohello

1. В разделе **Топология задания** щелкните **Выходные данные**.
1. В hello **выходные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:

   **Псевдоним вывода**: hello уникальный псевдоним для выходной hello.

   **Приемник**. Выберите **Power BI**.
1. Щелкните **Авторизовать**, а затем выполните вход в учетную запись Power BI.
1. После авторизации введите hello следующую информацию:

   **Рабочая область группы**. Выберите целевую рабочую область группы.

   **Имя набора данных**. Введите имя набора данных.

   **Имя таблицы**. Введите имя таблицы.
1. Щелкните **Создать**.

   ![Добавить задание Stream Analytics tooa выходные данные в Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Настройка запроса hello задания Stream Analytics hello

1. В разделе **Топология задания** щелкните **Запрос**.
1. Замените `[YourInputAlias]` с псевдонимом входного hello hello задания.
1. Замените `[YourOutputAlias]` с Псевдоним выхода hello hello задания.
1. Щелкните **Сохранить**.

   ![Добавить задание Stream Analytics tooa запросов в Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Запустить задание Stream Analytics hello

В задании Stream Analytics hello, нажмите кнопку **запустить** > **теперь** > **запустить**. После успешного запуска задания hello hello состояние задания меняется с **остановлена** слишком**под управлением**.

![Выполнение задания Stream Analytics в Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Создание и публикация данных hello toovisualize отчета Power BI

1. Убедитесь, что приложение hello образец выполняется на устройстве. Если нет, можно ссылаться учебники toohello в разделе [настроить на устройстве](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Войдите в tooyour [Power BI](https://powerbi.microsoft.com/en-us/) учетной записи.
1. Перейдите в рабочую область группы toohello, заданное при создании hello вывода для задания Stream Analytics hello.
1. Щелкните **Потоковая передача наборов данных**.

   Вы увидите hello в списке набора данных, который был указан при создании hello вывода для задания Stream Analytics hello.
1. В разделе **действия**, щелкните первый hello toocreate значок отчета.

   ![Создание отчета Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Создание строки температуры в режиме реального времени диаграммы tooshow со временем.
   1. На странице создания отчета hello добавьте линейчатую диаграмму.
   1. На hello **поля** области, разверните таблицу hello, указанный при создании hello вывода для задания Stream Analytics hello.
   1. Перетащите **EventEnqueuedUtcTime** слишком**оси** на hello **визуализации** области.
   1. Перетащите **температуры** слишком**значения**.

      График создан. ось x Hello отображает дату и время в часовом поясе UTC hello. ось y Hello отображает температуру из hello датчика.

      ![Добавление графика для tooa температуры отчете Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Создайте другой линии диаграммы tooshow в режиме реального времени влажности со временем. toodo это, выполните же шаги выше hello и поместите **EventEnqueuedUtcTime** по оси x hello и **влажность** на оси y hello.

   ![Добавление графика для tooa влажность отчете Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Нажмите кнопку **Сохранить** toosave hello отчета.
1. Нажмите кнопку **файл** > **публикации tooweb**.
1. Щелкните **Создать код внедрения**, а затем выберите **Опубликовать**.

Введенный hello ссылка на отчет, вы можете совместно использовать с любой пользователь, для доступа к отчетам и отчет hello toointegrate фрагмент кода в блоге или на веб-сайт.

![Публикация отчета Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Корпорация Майкрософт также предлагает hello [мобильных приложений Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) для просмотра и взаимодействия с помощью панелей мониторинга и отчеты на мобильном устройстве.

## <a name="next-steps"></a>Дальнейшие действия

Данные в режиме реального времени датчиков toovisualize Power BI вы использовали успешно из вашего центра Azure IoT.
Отсутствуют данные toovisualize альтернативный способ из центра IoT Azure. В разделе [веб-приложениях Azure используйте toovisualize в режиме реального времени датчиков из центра IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
