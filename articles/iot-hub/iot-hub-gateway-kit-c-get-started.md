---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT | Документация Майкрософт"
description: "Приступая к работе с IoT шлюза начального набора, создать ваш центр Azure IoT Подключите концентратор IoT toohello SensorTag и шлюза"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot hub, шлюз iot, Приступая к работе с hello Интернет вещей, набор средств iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Приступая к работе с начальным набором шлюза Интернета вещей

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Имитация устройства](iot-hub-gateway-kit-c-sim-get-started.md)

В этом учебнике, начните с изучения hello основы работы с [IoT шлюза начального набора](https://aka.ms/gateway-kit). Вы будете работать с Intel NUC под управлением Linux воздушного р. и hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). Вы узнаете, как tooseamleesly подключаться toohello облачных устройств с помощью центра IoT Azure.

***
**Нет начального набора?** Щелкните [здесь](https://aka.ms/gateway-kit). **Нет SensorTag?** [Начните имитацию устройства](iot-hub-gateway-kit-c-sim-get-started.md) или [купите SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag).
***

## <a name="lesson-1-configure-your-nuc"></a>Урок 1. Настройка NUC
![Урок 1. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

На этом занятии настроить NUC Intel (Далее единицы для вычисления) в hello Kit виде шлюза Azure IoT, установите пакет Azure IoT Edge hello на NUC и запуска шлюза функциональность tooverify hello образца приложения.

*Предполагаемое время toocomplete: 15 минут*

Go слишком[Настройка NUC Intel виде шлюза IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Урок 2. Создание Центра Интернета вещей
![Урок 2. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

На этом занятии устанавливается hello средств и программного обеспечения на компьютере узла. Затем можно создать бесплатную учетную запись Azure, подготовки ваш центр Azure IoT и создания своим первым устройством в центр IoT hello.

Прежде чем продолжать, завершите урок 1.

### <a name="get-hello-tools"></a>Получить средства hello
На главном компьютере установите hello средств и программного обеспечения.

*Предполагаемое время toocomplete: 20 минут*

Go слишком[средства hello](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Создание Центра Интернета вещей и регистрация устройства
Создание группы ресурсов, подготовки к первой центр Azure IoT и добавить вашего первого устройства toohello центр IoT с помощью hello Azure CLI.

*Предполагаемое время toocomplete: 10 минут*

Go слишком[создать центр IoT и регистрация устройства](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Урок 3. Получение сообщений из SensorTag и чтение сообщений из Центра Интернета вещей
На этом занятии будет использовать конфигурации hello tooautomate сценарии и выполнение примера приложения ЛЮЧИТЬ шлюза. Такие приложения использовать коллекцию модулей tooaggregate и преобразования данных, обработки команд и выполнять любое количество связанных задач. Модули взаимодействуют друг с другом через брокер сообщений. Пример приложения Hello имеет ЛЮЧИТЬ модуля и модуль концентратора IoT. Hello ЛЮЧИТЬ модуль получает данные из SensorTag отключить. Здравствуйте, пакеты модуля концентратора IoT данных hello полученных и отправляет его центр IoT tooyour через шлюз платформы hello в Azure IoT Edge.

![Урок 3. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>Настройка и выполнение примера приложения hello ЛЮЧИТЬ
Настройте подключение hello между SensorTag и шлюза. Затем завершите настройку hello и запустить пример приложения hello отключить.

*Предполагаемое время toocomplete: 15 минут*

Go слишком[настройки и выполнения hello ЛЮЧИТЬ пример приложения](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Чтение сообщений из Центра Интернета вещей
Запустите образец кода на вашем узле компьютер tooread сообщения из вашего центра IoT.

*Предполагаемое время toocomplete: 15 минут*

Go слишком[чтения сообщений из вашего центра IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Урок 4: Сохранить сообщения tooAzure хранилище таблиц
Создайте приложение Azure функции, которое получает входящие сообщения от вашего центра IoT и записывает их в хранилище таблиц tooAzure.

![Урок 4. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Создание учетной записи хранения Azure и приложения-функции Azure
Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетную запись хранилища Azure.

*Предполагаемое время toocomplete: 10 минут*

Go слишком[создать учетную запись хранилища Azure и Azure функции приложения](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Чтение сообщений, сохраненных в Хранилище таблиц Azure
Они записываются в хранилище таблиц tooAzure наблюдать за сообщений hello шлюза в облако.

*Предполагаемое время toocomplete: 5 минут*

Go слишком[чтения сообщения сохраняются в хранилище таблиц Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Устранение неполадок
Если у вас возникнут проблемы во время занятия hello поиск решений в hello [Устранение неполадок](iot-hub-gateway-kit-c-troubleshooting.md) статьи.

## <a name="explore-more"></a>Изучить подробнее
Посетите hello [Intel IoT шлюза для разработчика зоны](http://software.intel.com/iot/microsoft-azure) toolearn дополнительные.
