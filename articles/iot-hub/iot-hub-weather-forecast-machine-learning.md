---
title: "Прогноз с использованием машинного обучения Azure с помощью данных из центра IoT aaaWeather | Документы Microsoft"
description: "Используйте машинное обучение Azure, вероятность hello toopredict дождь на основе hello температуры и влажности данные, которые собирает концентратор IoT из датчика."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Прогнозирование погоды с помощью машинного обучения"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Прогноз погоды, используя данные датчика hello из вашего центра IoT в машинном обучении Azure

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Машинное обучение методика обработки и анализа данных, позволяет компьютерам узнать из будущих поведения tooforecast существующих данных, результаты и тенденций. Машинное обучение Azure — облачной службы прогнозирующей аналитики, которая упрощает возможных tooquickly Создание и развертывание прогнозных моделей в качестве решения для аналитики.

## <a name="what-you-learn"></a>Что вы узнаете

Вы узнаете, как с помощью toouse машинного обучения Azure toodo прогноз погоды (вероятность дождь) Здравствуйте, температуры и влажности данные из вашего центра Azure IoT. вероятность Hello дождь выводится hello подготовленного погоды модели прогнозирования. Hello модель построена на основе вероятность на основе температуры и влажности дождь tooforecast данные за прошедший период.

## <a name="what-you-do"></a>В рамках этого руководства мы:

- Развертывание модели прогноза погоды hello в виде веб-службы.
- добавим группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей;
- Создание задания Stream Analytics и задать для задания hello:
  - получение данных о температуре и влажности от Центра Интернета вещей;
  - Вызов hello web service tooget hello дождь вероятность.
  - Сохраните хранилище больших двоичных объектов tooan результат hello.
- Используйте прогноз погоды hello tooview обозреватель хранилищ Microsoft Azure.

## <a name="what-you-need"></a>Необходимые элементы

- Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:
  - Активная подписка Azure.
  - Центр Интернета вещей Azure в подписке;
  - Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.
- учетную запись Студии машинного обучения Azure. ([Бесплатно ознакомьтесь с работой студии машинного обучения](https://studio.azureml.net/).)

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Развертывание модели прогноза погоды hello в виде веб-службы

1. Go toohello [страницы модели прогноза погоды](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Щелкните **Открыть в Studio** в Студии машинного обучения Microsoft Azure.
   ![Страница модели прогноза погоды Привет открыть в коллекции Cortana аналитики](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Нажмите кнопку **запуска** toovalidate hello шагов в модели hello. Этот шаг может занять toocomplete 2 минуты.
   ![Привет открыть модель прогноза погоды в студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Щелкните действие **SET UP WEB SERVICE** (Настроить веб-службу)  > **Predictive Web Service** (Прогнозная веб-служба).
   ![Развертывание модели прогноза погоды hello в студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. В диаграмме hello перетащите hello **веб-службе входные данные** модуля, где-нибудь рядом hello **модель оценки** модуля.
1. Подключение hello **веб-службе входные данные** toohello модуль **модель оценки** модуля.
   ![Соединение модулей в Студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Нажмите кнопку **ЗАПУСКА** toovalidate hello шагов в модели hello.
1. Нажмите кнопку **развертывание веб-службы** toodeploy hello модели веб-службы.
1. На панели мониторинга hello hello модели, загрузите hello **Excel 2010 или более ранних книги** для **ЗАПРОСОВ и ОТВЕТОВ**.

   > [!Note]
   > Убедитесь, необходимо загрузить hello **Excel 2010 или более ранних книги** даже если на компьютере более поздней версии Excel на компьютере.

   ![Загрузите hello Excel для конечной точки ОТВЕТА запрос hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Откройте книгу Excel hello, запишите hello **URL веб-службы** и **ключ доступа**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Создание, настройка и выполнение заданий Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics

1. В hello [портал Azure](https://ms.portal.azure.com/), нажмите кнопку **New** > **Интернета вещей** > **задания Stream Analytics**.
1. Введите следующую информацию для задания hello hello.

   **Имя задания**: hello имя задания hello. Hello имя должно быть глобально уникальным.

   **Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.

   **Расположение**: используйте hello же расположении, что и группы ресурсов.

   **ПИН-код toodashboard**: Установите этот флажок для центра IoT tooyour простой доступ из панели мониторинга hello.

   ![Создание задания Stream Analytics в Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Щелкните **Создать**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Добавьте задание Stream Analytics входного toohello

1. Задание Stream Analytics откройте hello.
1. В разделе **Топология задания** щелкните **Входные данные**.
1. В hello **входные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:

   **Входной псевдоним**: hello уникальный псевдоним для hello входных данных.

   **Источник**. Выберите **Центр Интернета вещей**.

   **Группа потребителей**: созданную группу потребителей выберите hello.

   ![Добавить задание Stream Analytics ввода toohello в Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Щелкните **Создать**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Добавление выходных данных задания Stream Analytics toohello

1. В разделе **Топология задания** щелкните **Выходные данные**.
1. В hello **выходные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:

   **Псевдоним вывода**: hello уникальный псевдоним для выходной hello.

   **Приемник.** Выберите **хранилище BLOB-объектов**.

   **Учетная запись хранения**: hello учетной записи хранилища для хранилища больших двоичных объектов. Можно использовать существующую учетную запись хранения или создать новую.

   **Контейнер**: hello контейнер хранения больших двоичных объектов hello. Вы можете создать новый контейнер или использовать уже существующий.

   **Формат сериализации событий.** Выберите вариант **CSV**.

   ![Добавить задание Stream Analytics toohello выходные данные в Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Щелкните **Создать**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Добавление функции toohello Stream Analytics задания toocall hello веб-службы, развернутые

1. В разделе **Топология задания** щелкните **Функции** > **Добавить**.
1. Введите hello следующую информацию:

   **Псевдоним функции**: введите значение `machinelearning`.

   **Тип функции**: выберите вариант **Azure ML**.

   **Метод импорта**: выберите **Импортировать из другой подписки**.

   **URL-адрес**: Введите URL веб-службы, отмеченный вниз hello из книги Excel hello.

   **Ключ**: Введите ключ доступа, отмеченный вниз hello из книги Excel hello.

   ![Добавить задание Stream Analytics toohello функции в Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Щелкните **Создать**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Настройка запроса hello задания Stream Analytics hello

1. В разделе **Топология задания** щелкните **Запрос**.
1. Замените существующий код hello hello, следующий код:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Замените `[YourInputAlias]` с псевдонимом входного hello hello задания.

   Замените `[YourOutputAlias]` с Псевдоним выхода hello hello задания.

1. Щелкните **Сохранить**.

### <a name="run-hello-stream-analytics-job"></a>Запустить задание Stream Analytics hello

В задании Stream Analytics hello, нажмите кнопку **запустить** > **теперь** > **запустить**. После успешного запуска задания hello hello состояние задания меняется с **остановлена** слишком**под управлением**.

![Запустить задание Stream Analytics hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Использовать прогноз погоды hello tooview обозреватель хранилищ Microsoft Azure

Выполните сбор toostart hello клиентского приложения и отправку температуры и влажности центра IoT tooyour данных. Для каждого сообщения, получающего концентратор IoT задание Stream Analytics hello вызывает hello прогноз погоды web service tooproduce hello вероятность дождь. Затем результат Hello сохраняется tooyour хранилище больших двоичных объектов. Azure Storage Explorer — это средство, можно использовать tooview hello результат.

1. [Скачайте и установите обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/).
1. Откройте обозреватель службы хранилища Azure.
1. Войдите в tooyour учетная запись Azure.
1. Выберите свою подписку.
1. Щелкните подписку Azure > **Учетные записи хранения** > учетная запись хранения > **Контейнеры больших двоичных объектов** и выберите нужный контейнер.
1. Откройте результат hello toosee файл CSV-файл. последний столбец записи Hello hello вероятность дождь.

   ![Получение прогноза погоды с помощью машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Сводка

Вы использовали успешно вероятность hello tooproduce машинного обучения Azure на основе данных температуры и влажности hello, получающий концентратор IoT дождь.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]