---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT | Документация Майкрософт"
description: "Приступая к работе с IoT шлюза начального набора, создать ваш центр Azure IoT Подключите концентратор IoT toohello шлюза"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot hub, шлюз iot, Приступая к работе с hello Интернет вещей, набор средств iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Приступая к работе с начальным набором шлюза Интернета вещей с имитацией устройства

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Имитация устройства](iot-hub-gateway-kit-c-sim-get-started.md)

В этом учебнике, начните с изучения hello основы работы с [IoT шлюза начального набора](https://aka.ms/gateway-kit). Вы будете работать с Intel NUC под управлением Wind River Linux. Вы узнаете, как tooseamleesly подключаться toohello облачных устройств с помощью центра IoT Azure.

***
**Нет начального набора?** Щелкните [здесь](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Урок 1. Настройка NUC
![Урок 1. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

На этом занятии настроить NUC Intel (Далее единицы для вычисления) в hello Kit виде шлюза Azure IoT, установите пакет Azure IoT Edge hello на NUC и запуска шлюза функциональность tooverify hello образца приложения.

*Предполагаемое время toocomplete: 15 минут*

Go слишком[Настройка NUC Intel виде шлюза IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Урок 2. Создание Центра Интернета вещей
![Урок 2. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

На этом занятии устанавливается hello средств и программного обеспечения на компьютере узла. Затем можно создать бесплатную учетную запись Azure, подготовки ваш центр Azure IoT и создания своим первым устройством в центр IoT hello.

Прежде чем продолжать, завершите урок 1.

### <a name="get-hello-tools"></a>Получить средства hello
На главном компьютере установите hello средств и программного обеспечения.

*Предполагаемое время toocomplete: 20 минут*

Go слишком[средства hello](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Создание Центра Интернета вещей и регистрация устройства
Создание группы ресурсов, подготовки к первой центр Azure IoT и добавить вашего первого устройства toohello центр IoT с помощью hello Azure CLI.

*Предполагаемое время toocomplete: 10 минут*

Go слишком[создать центр IoT и регистрация устройства](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Занятие 3: Получение сообщений от устройств, имитация hello и чтение сообщений в концентратор IoT
На этом занятии будет использовать конфигурации hello tooautomate сценариев и выполнением приложения имитированное устройство шлюза. приложение Hello имитированное устройство создает температуры образец данных и отправляет его tooan IoT hub модуля. Здравствуйте, пакеты модуля концентратора IoT данных hello полученных и отправляет его центр IoT tooyour через шлюз платформы hello в Azure IoT Edge.

![Урок 3. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Настройка и запуск имитации устройства
Подготовьте коды образец hello. Затем настроить и запустить пример приложения hello имитируемые устройства.

*Предполагаемое время toocomplete: 15 минут*

Go слишком[настроить и запустить имитированное устройство](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Чтение сообщений из Центра Интернета вещей
Запустите образец кода на сообщения hello tooread компьютера узла из вашего центра IoT.

*Предполагаемое время toocomplete: 15 минут*

Go слишком[чтения сообщений из вашего центра IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Урок 4: Сохранить сообщения tooAzure хранилище таблиц
Создайте приложение Azure функции, которое получает входящие сообщения от вашего центра IoT и записывает их в хранилище таблиц tooAzure.

![Урок 4. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Создание учетной записи хранения Azure и приложения-функции Azure
Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетную запись хранилища Azure.

*Предполагаемое время toocomplete: 10 минут*

Go слишком[создать учетную запись хранилища Azure и Azure функции приложения](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Чтение сообщений, сохраненных в Хранилище таблиц Azure
Они записываются в хранилище таблиц tooAzure наблюдать за сообщений hello шлюза в облако.

*Предполагаемое время toocomplete: 5 минут*

Go слишком[чтения сообщения сохраняются в хранилище таблиц Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Устранение неполадок
Если у вас возникнут проблемы во время занятия hello поиск решений в hello [Устранение неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md) статьи.

## <a name="explore-more"></a>Изучить подробнее
Посетите hello [Intel IoT шлюза для разработчика зоны](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn дополнительные.
