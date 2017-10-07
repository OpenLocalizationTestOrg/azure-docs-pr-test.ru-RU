---
title: "руководство по aaaDeveloper для центр IoT Azure | Документы Microsoft"
description: "Руководство разработчика Azure IoT Hub Hello включает обсуждения конечных точек, безопасности, реестра удостоверений hello, управление устройствами, непосредственные методы, близнецы устройства, передачи файлов, задания, hello язык запросов центр IoT и обмена сообщениями."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Руководство разработчика по центру Azure IoT (IoT — Интернет вещей)

Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения.

Центр Azure IoT обеспечивает следующие возможности:

* безопасную связь благодаря использованию уникальных учетных данных безопасности устройства и контроля доступа;
* несколько вариантов глобального взаимодействия между устройствами и облаком;
* запрашиваемое хранилище, содержащее сведения о состоянии каждого устройства и его метаданные;
* Подключения легко устройств с библиотеками устройства для наиболее распространенных языков hello и платформ.

Это руководство разработчика центра IoT содержит hello в следующих статьях:

* [Device-to-cloud communications guidance][lnk-d2c-guidance] (Руководство по обмену данными между устройством и облаком): помощь в принятии решения об использовании сообщений, отправляемых из устройства в облако, сообщаемых свойств двойника устройства или передачи файлов.
* [Cloud-to-device communication guidance][lnk-c2d-guidance] (Руководство по обмену данными между облаком и устройством): помощь в принятии решения об использовании прямых методов, требуемых свойств двойника устройства и сообщений, отправляемых из облака на устройство.
* [Устройства в облако и облака на устройство обмена сообщениями с центром IoT] [ devguide-messaging] описывает hello функций обмена сообщениями (устройства в облако и облака для устройства), предоставляемых центр IoT.
  * [Отправлять сообщения из устройства в облако tooIoT концентратора][devguide-messages-d2c].
  * [Чтение сообщения из устройства в облако из встроенных hello конечной точки][devguide-builtin].
  * [Использование пользовательских конечных точек и правил маршрутизации для сообщений, отправляемых с устройства в облако][devguide-custom]
  * [Отправка сообщений, пересылаемых из облака на устройство, из Центра Интернета вещей][devguide-messages-c2d]
  * [Создание и чтение сообщений Центра Интернета вещей][devguide-format]
* [Upload files from a device][devguide-upload] (Передача файлов с устройства): сведения о том, как передавать файлы с устройства. Hello статья также содержит сведения о подразделы, такие как hello может отправлять уведомления о процессе загрузки hello.
* [Manage device identities in IoT Hub][devguide-identities] (Управление удостоверениями устройств в Центре Интернета вещей): информация о том, какие сведения хранятся в каждом реестре удостоверений Центра Интернета вещей и как эти сведения можно использовать и изменять.
* [Управление доступом tooIoT концентратора] [ devguide-security] описываются hello безопасности модель, используемая toogrant tooIoT концентратора возможности доступа для устройств и облачные компоненты. Hello статья содержит сведения об использовании маркеров и сертификаты X.509 и подробные сведения о hello разрешения можно предоставить разрешение.
* [Конфигурации и состояния toosynchronize устройства близнецы] [ devguide-device-twins] описывает hello *двойных устройства* понятие и hello функциональных возможностей, предоставляемых как синхронизация устройства с устройством две. Hello статья содержит сведения о hello данные, хранящиеся в двойных устройства.
* [Вызвать метод прямой на устройстве] [ devguide-directmethods] описывает жизненный цикл hello прямой метод, сведения о как методы tooinvoke на устройстве из вашей серверной части приложения и дескриптор hello прямой метод на вашем устройстве.
* [Schedule jobs on multiple devices][devguide-jobs] (Планирование заданий на нескольких устройствах): сведения о планировании заданий на нескольких устройствах. Hello статье описывается, как toosubmit заданий, выполнять задачи, как выполнение прямых метода, обновление устройства с помощью двойных устройства. Он также описывает, каким образом tooquery hello состояния задания.
* [Ссылки: Выбор протокола связи] [ devguide-protocol] описывает hello протоколы связи, что центр IoT поддерживает взаимодействие устройства и списки hello порты, которые должны быть открыты.
* [Ссылка - конечные точки центра IoT] [ devguide-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций среды выполнения и управления. Hello статье также описаны процедуры можно создать дополнительные конечные точки в концентратор IoT и toouse tooyour подключение устройств tooenable шлюз поля центра IoT конечных точек в нестандартных сценариях.
* [Ссылка - язык запросов центр IoT для близнецы устройства, задания и маршрутизация сообщений] [ devguide-query] описывает этот центр IoT язык запросов, который позволяет tooretrieve сведения из концентратор близнецы устройства и заданий.
* [Ссылка — квот и регулирования] [ devguide-quotas] приведены квоты hello hello центра IoT службы и поведение, при превышении квоты можно ожидать toosee регулирования hello.
* [Ссылки - цены] [ devguide-pricing] содержит общие сведения о различных SKU и цены на центр IoT и сведения о способ сообщений hello различные функциональные возможности центр IoT учитываются как в IoT Hub.
* [Ссылка - устройства и службы SDK] [ devguide-sdks] пакеты SDK Azure IoT, можно использовать toodevelop hello списки устройств и служб приложений, взаимодействующих с вашей центр IoT. Hello статьи включает документацию tooonline API ссылки.
* [Ссылка - Поддержка MQTT концентратора IoT] [ devguide-mqtt] предоставляет подробные сведения о поддержке протокола MQTT hello центр IoT. Hello статье рассматривается поддержка hello hello MQTT протокола встроенных toohello пакеты SDK Azure IoT и предоставляет сведения об использовании протокола MQTT hello напрямую.
* [Глоссарий][devguide-glossary]: список распространенных терминов, связанных с Центром Интернета вещей.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
