---
title: "Визуализация данных времени aaaReal датчиков данных из вашего центра Azure IoT — веб-приложений | Документы Microsoft"
description: "Используйте функцию службу приложений Microsoft Azure toovisualize температуры и влажности данные, полученные от датчика hello и отправляются в центр Iot tooyour hello веб-приложений."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "визуализация данных, полученных в реальном времени, визуализация интерактивных данных, визуализация данных датчиков"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Визуализация данных датчика в режиме реального времени из вашего центра Azure IoT с помощью функции hello веб-приложениях службы приложений Azure

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Что вы узнаете

В этом учебнике вы узнаете, как toovisualize в режиме реального времени датчиков, получающий концентратор IoT путем запуска веб-приложения, размещенного на веб-приложения. Если вам нужны данные hello toovisualize tootry в ваш центр IoT с помощью Power BI, см. раздел [данных датчика в режиме реального времени toovisualize используйте Power BI из центра IoT Azure](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>В рамках этого руководства мы:

- Создание веб-приложения в hello портал Azure.
- добавим группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей;
- Настройте hello web app tooread датчиков из вашего центра IoT.
- Отправьте toobe приложения web, расположенных на веб-приложения hello.
- Откройте hello веб-приложения toosee в режиме реального времени температуры и влажности данных из вашего центра IoT.

## <a name="what-you-need"></a>Необходимые элементы

- [Настройка устройства](iot-hub-raspberry-pi-kit-node-get-started.md), который охватывает hello следующие требования:
  - активная подписка Azure;
  - Центр Интернета вещей в подписке;
  - Клиентское приложение, которое отправляет сообщения tooyour Iot hub
- [Скачайте Git](https://www.git-scm.com/downloads).

## <a name="create-a-web-app"></a>Создание веб-приложения

1. В hello [портал Azure](https://ms.portal.azure.com/), нажмите кнопку **New** > **Интернет + мобильные устройства** > **веб-приложения**.
2. Введите имя задания уникальных проверьте hello подписки, укажите группу ресурсов и расположение, выберите **toodashboard ПИН-код**, а затем нажмите кнопку **создать**.

   Рекомендуется выбирать hello же расположении, что и группы ресурсов. Это помогает выполнять скорость обработки и снижает затраты hello передачи данных.

   ![Создание веб-приложения](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Настройка hello веб-приложения tooread данных из вашего центра IoT

1. Откройте веб-приложения hello, который только что провизионировал.
2. Нажмите кнопку **параметры приложения**, а затем на вкладке **параметры приложения**, добавить следующие пары "ключ значение" hello:

   | Ключ                                   | Значение                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Получено из обозревателя Центра Интернета вещей                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | Имя группы потребителей hello добавления центра IoT tooyour Hello  |

   ![Добавить параметры tooyour веб-приложения с парами «ключ значение»](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Нажмите кнопку **параметры приложения**в разделе **Общие параметры**, переключение hello **веб-сокеты** , а затем щелкните **Сохранить**.

   ![Переключить режим сокеты hello Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Отправка toobe приложения web, расположенных на веб-приложения hello

Теперь веб-приложение доступно в GitHub. В нем отображаются данные, поступающие с датчиков в реальном времени, из Центра Интернета вещей. Все, что нужно toodo — настройки hello web app toowork с репозиторием Git, загрузка веб-приложения hello из GitHub и затем передать его tooAzure для toohost приложения hello web.

1. В веб-приложения hello, нажмите кнопку **варианты развертывания** > **Выбор источника** > **локального репозитория Git**, а затем нажмите кнопку **ОК**.

   ![Настройка web app развертывания toouse hello локальный репозиторий Git](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Нажмите кнопку **учетные данные развертывания**, создайте пользователя имя и пароль toouse tooconnect toohello репозитории в Azure и нажмите кнопку **Сохранить**.

3. Нажмите кнопку **Обзор**и запишите значение hello **URL-адрес клонирования Git**.

   ![Получить URL-адрес клона Git hello веб-приложения](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Откройте окно терминала или командной строки на локальном компьютере.

5. Загрузите веб-приложения hello из GitHub и отправьте его tooAzure для toohost приложения hello web. toodo таким образом, выполните следующие команды hello.

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<URL-адрес клона Git\> hello URL-адрес репозитория Git hello, найденных на hello **Обзор** страницы приветствия веб-приложения.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Откройте hello веб-приложения toosee в режиме реального времени температуры и влажности данных из вашего центра IoT

На hello **Обзор** страницы веб-приложения, нажмите кнопку hello URL-адрес tooopen hello веб-приложения.

![Получить hello URL-адрес веб-приложения](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Вы увидите hello в режиме реального времени температуры и влажности данные из вашего центра IoT.

![Страница веб-приложения с данными о температуре и влажности, полученными в реальном времени](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Убедитесь, что приложение hello образец выполняется на устройстве. Если нет, вы получите пустую диаграмму, можно обратиться учебники toohello под [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Дальнейшие действия
Успешно вы использовали данные в режиме реального времени датчика toovisualize web приложений из вашего центра IoT.

Альтернативный способ toovisualize данные из центра IoT Azure, см. [используйте Power BI toovisualize датчика в режиме реального времени, данные из вашего центра IoT](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
