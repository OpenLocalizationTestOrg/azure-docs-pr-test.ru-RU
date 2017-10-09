---
title: "aaaUse tooconnect шлюза IoT tooAzure устройства центра IoT | Документы Microsoft"
description: "Дополнительные сведения об облачных toouse NUC Intel как tooconnect шлюза IoT TI SensorTag и датчик отправки данных tooAzure центр IoT в hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "шлюз IOT подключаться toocloud устройства"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Использование облачного toohello действия tooconnect шлюза IoT - SensorTag tooAzure центра IoT

> [!NOTE]
> Перед началом работы с руководством убедитесь, что вы завершили [настройку Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). В [Настройка NUC Intel виде шлюза IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), настроить устройство Intel NUC hello как шлюз IoT.

## <a name="what-you-will-learn"></a>Новые знания

Вы узнаете, как toouse tooconnect шлюза IoT SensorTag инструментов Техас (CC2650STK) tooAzure центр IoT. шлюз IoT Hello отправляет температуры и влажности собранные данные hello SensorTag tooAzure центр IoT.

## <a name="what-you-will-do"></a>Выполняемая задача

- Создайте Центр Интернета вещей.
- Регистрация устройства в центр IoT hello для hello SensorTag.
- Включите hello подключение между шлюзом IoT hello и hello SensorTag.
- Запустите ЛЮЧИТЬ образец приложения toosend SensorTag данные tooyour центр IoT.

## <a name="what-you-need"></a>Необходимые элементы

- Пройден учебник [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), в котором рассказывается, как настроить устройство Intel NUC в качестве шлюза Интернета вещей.
- * Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
- Клиент SSH, который выполняется на главном компьютере. В Windows рекомендуется использовать PuTTY. Клиент SSH изначально входит в состав ОС Linux и Mac OS.
- Hello IP-адрес и hello имя пользователя и пароль tooaccess hello шлюза из клиента SSH hello.
- Подключение к Интернету.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Здесь следует зарегистрировать новое устройство для SensorTag.

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Включить hello подключение между шлюзом IoT hello и hello SensorTag

В этом разделе выполните следующие задачи hello.

- Получение hello MAC-адрес hello SensorTag для подключения Bluetooth.
- Инициируйте подключение Bluetooth из hello IoT шлюза toohello SensorTag.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Получить hello MAC-адрес hello SensorTag для подключение Bluetooth

1. На главном компьютере hello запустите клиент SSH hello и шлюз IoT toohello подключения.
1. Разблокируйте Bluetooth, выполнив следующую команду hello:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Запустите службу hello Bluetooth на шлюз IoT hello и введите tooconfigure оболочки Bluetooth, hello Bluetooth, выполнив следующие команды:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Питания на контроллере Bluetooth hello, запустив hello следующую команду в hello оболочки Bluetooth:

   ```bash
   power on
   ```

   ![питания на контроллере Bluetooth hello в шлюзе hello IoT с bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Начните поиск ближайших устройствами Bluetooth, выполнив следующую команду hello:

   ```bash
   scan on
   ```

   ![Поиск находящихся поблизости устройств Bluetooth с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Нажмите клавишу связывание кнопки на hello SensorTag hello. Hello зеленый ИНДИКАТОР на мигает SensorTag hello.
1. В hello оболочки Bluetooth вы увидите найден SensorTag приветствия. Запишите hello hello SensorTag MAC-адрес. В этом примере — hello MAC-адрес hello SensorTag `24:71:89:C0:7F:82`.
1. Отключите проверку hello, выполнив следующую команду hello:

   ```bash
   scan off
   ```

   ![Остановка поиска находящихся поблизости устройств Bluetooth с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Инициировать подключение Bluetooth из hello IoT шлюза toohello SensorTag

1. Подключитесь toohello SensorTag, выполнив следующую команду hello:

   ```bash
   connect <MAC address>
   ```

   ![Связь с bluetoothctl toohello SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Отключитесь от hello SensorTag и выйти из оболочки Bluetooth hello, запустив hello, следующие команды:

   ```bash
   disconnect
   exit
   ```

   ![Отключение от hello SensorTag с bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Hello подключению hello SensorTag hello IoT шлюза успешно активирован.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Запустите ЛЮЧИТЬ образец приложения toosend SensorTag данные tooyour центра IoT

энергии низкий Bluetooth (Разрешить) пример приложения Hello обеспечивается Azure IoT Edge. Пример приложения Hello собирает данные от ЛЮЧИТЬ подключения и отправки центра IoT tooyou данных hello. Пример приложения hello toorun, необходимо:

1. Настройте пример приложения hello.
1. Запустите образец приложения hello в шлюзе IoT hello.

### <a name="configure-hello-sample-application"></a>Настройка образца приложения hello

1. Go toohello папки образца приложения hello, выполнив следующую команду hello:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Откройте файл конфигурации hello, выполнив следующую команду hello:

   ```bash
   vi ble_gateway.json
   ```

1. В файле конфигурации hello заполните hello следующие значения:

   **IoTHubName**: hello имя вашего центра IoT.

   **IoTHubSuffix**: получение IoTHubSuffix из hello первичного ключа строки подключения устройства hello, отмеченный вниз. Убедитесь, что получить первичный ключ строки подключения устройств hello hello, не hello первичного ключа в строке подключения концентратора IoT. первичный ключ строки подключения устройств hello Hello указано в формате hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Транспорт**: hello значение по умолчанию — `amqp`. Это значение показывает hello протокола во время transpotation. Оно может быть равным `http`, `amqp` или `mqtt`.

   **macAddress**: hello MAC-адрес hello SensorTag, отмеченный вниз.

   **deviceID**: идентификатор hello устройства, созданный в концентратор IoT.

   **deviceKey**: hello первичного ключа строки подключения устройств hello.

   ![Файл конфигурации завершения hello ЛЮЧИТЬ пример приложения hello](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Нажмите клавишу `ESC` и тип `:wq` toosave hello файла.

### <a name="run-hello-sample-application"></a>Запустить образец приложения hello

1. Убедитесь, что включено SensorTag приветствия.
1. Выполните следующую команду hello.

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Дальнейшие действия

[Использование шлюза Интернета вещей для преобразования данных датчиков с помощью Edge Интернета вещей](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
