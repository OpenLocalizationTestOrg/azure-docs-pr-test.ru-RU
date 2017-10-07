---
title: "aaaOverview края IoT Azure | Документы Microsoft"
description: "Описываются hello основные принципы в Azure IoT Edge как шлюзы, модули и брокеры."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Сведения об архитектуре Azure IoT Edge

Прежде чем проверить любой пример кода, или создать собственные поля шлюз, с помощью IoT края, проанализируйте hello основные понятия, которые обеспечивают архитектура hello IoT края.

## <a name="iot-edge-modules"></a>Модули Edge Интернета вещей

Шлюз создается с использованием Azure IoT Edge путем создания и сборки *модулей IoT Edge*. Модули используют *сообщений* tooexchange данные друг с другом. Модуль получает сообщение, выполняющий некоторое действие, при необходимости преобразует их в новое сообщение и затем публикует его для других модулей tooprocess. Некоторые модули могут только создавать сообщения и никогда не обрабатывают входящие сообщения. Цепочка модулей создает конвейера обработки данных с каждого модуля, выполняя преобразование данных hello в одной точке в этом конвейере.

![Цепочка модулей в шлюзе, созданном с помощью Edge Интернета вещей Azure][1]

IoT Edge содержит hello следующие компоненты:

* Предварительно написанные модули, которые выполняют общие функции шлюза.
* интерфейсы Hello a developer можно использовать пользовательские модули toowrite.
* Здравствуйте, необходимые toodeploy инфраструктуры и запустите набор модулей.

Hello SDK предоставляет уровень абстракции, который позволяет toorun toobuild шлюзов в различных операционных системах и платформах.

![Уровень абстракции Edge Интернета вещей Azure][2]

## <a name="messages"></a>Сообщения

Несмотря на то, что говорить о модулях передачи сообщения tooeach других является tooconceptualize удобным способом, как функции шлюза, он не отражать, что происходит. Модули IoT Edge используют broker toocommunicate друг с другом. Модули публикации broker toohello сообщений (с помощью шаблонов обмена сообщениями, например шины или публикации или подписки) и подождите, пока hello broker маршрута hello сообщение toohello модули подключенных tooit.

Модуль использует hello **Broker_Publish** функции toopublish toohello посредник сообщений. Hello broker доставляет сообщения tooa модуль путем вызова функции обратного вызова. Сообщение состоит из набора пар ключ-значение, а содержимое передается как блок памяти.

![роль Hello hello брокера в Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a>Маршрутизация и фильтрация сообщений

Существует два способа toodirect сообщения toohello правильный IoT Edge модули:

* Вы можете передать набор ссылок могут быть переданы toohello брокера, чтобы hello broker знал hello источника и приемника для каждого модуля.
* Модуль можно фильтровать по свойствам приветственное сообщение hello.

Модуль только следует обрабатывают сообщения, если приветственное сообщение предназначено для него. Фильтрация ссылок и сообщений создает конвейер сообщений.

## <a name="next-steps"></a>Дальнейшие действия

toosee этих основных понятий в образец можно запустить, в разделе [архитектура исследовать Edge Azure IoT][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md