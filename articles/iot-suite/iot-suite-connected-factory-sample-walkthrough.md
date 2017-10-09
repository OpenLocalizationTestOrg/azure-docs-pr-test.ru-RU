---
title: "Пошаговое руководство по решениям Azure IoT Suite фабрики aaaConnected | Документы Microsoft"
description: "Описание hello Azure IoT предварительно настроенное решение подключен фабрики и его архитектуры."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Пошаговое руководство по работе с предварительно настроенным решением подключенной фабрики

Hello IoT Suite подключен фабрики [предварительно настроенное решение] [ lnk-preconfigured-solutions] представляет собой реализацию решения промышленным начала до конца:

* Подключается tooboth имитируемые промышленных устройств работает OPC UA серверов в производственных линиях имитацию фабрики и реального устройства server OPC UA. Дополнительные сведения о OPC UA см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).
* Показывает оперативные ключевые показатели эффективности и общую эффективность оборудования этих устройств и производственных линий.
* Демонстрирует, как приложение на основе облака может быть используется toointeract с OPC UA серверных систем.
* Позволяет вам tooconnect устройства server OPC UA.
* Позволяет toobrowse и изменения hello OPC UA данные сервера.
* Интегрируется с hello tooprovide службы аналитики ряда времени Azure (TSI) пользовательских представлений данных hello серверов OPC UA.

Hello решения можно использовать в качестве отправной точки для свою собственную реализацию и [настроить] [ lnk-customize] его toomeet требованиями бизнеса.

В этой статье поможет выполнить некоторые ключевые элементы hello hello подключен фабрики решения tooenable toounderstand ее работы. Эти знания помогут вам:

* Устранение неполадок в решении hello.
* Планирование как toocustomize toohello решения toomeet конкретным требованиям.
* спроектировать собственное решение IoT, использующее службы Azure.

Дополнительные сведения см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Логическая архитектура

Следующая схема Hello представлен краткий обзор hello логические компоненты hello предварительно настроенных решений.

![Логическая архитектура подключенной фабрики][connected-factory-logical]

## <a name="communication-patterns"></a>Модели связи

Hello решение использует hello [спецификации OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT данные телеметрии OPC UA концентратора в формате JSON. Hello решение использует hello [издатель OPC](https://github.com/Azure/iot-edge-opc-publisher) модуль IoT Edge для этой цели.

Hello решение также включает клиент OPC UA интегрированы в веб-приложении, смогут устанавливать соединения с локальными серверами OPC UA. Hello клиент использует [обратного прокси-сервера](https://wikipedia.org/wiki/Reverse_proxy) и получает справки из центра IoT toomake hello соединения без необходимости открыть порты в брандмауэре hello в локальной среде. Эта модель связи называется [взаимодействием с поддержкой службы](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). Hello решение использует hello [прокси OPC](https://github.com/Azure/iot-edge-opc-proxy/) модуль IoT Edge для этой цели.


## <a name="simulation"></a>Моделирование

Hello имитировать станции и имитировать hello производством, систем (MES) составляют производственной линии. Hello имитации устройства и hello OPC издателя модуль на основе hello [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] опубликованное hello OPC Foundation.

Hello OPC прокси-сервер и издатель OPC реализованы в виде модулей на основе [Azure IoT Edge][lnk-Azure-IoT-Gateway]. К каждой виртуальной производственной линии подключен отдельный шлюз.

Все виртуальные компоненты работают в контейнерах Docker, размещенных на виртуальной машине Azure под управлением Linux. Моделирование Hello является настроенным toorun восемь имитации рабочей строки по умолчанию.

## <a name="simulated-production-line"></a>Виртуальная производственная линия

Производственная линия изготавливает детали. Она состоит из различных станций: станция сборки, станция тестирования и станция упаковки.

Моделирование Hello запускается и обновляет данные hello, доступных через узлы OPC UA hello. Все строки имитации рабочей станции оркестрация hello MES через OPC UA.

## <a name="simulated-manufacturing-execution-system"></a>Виртуальная система управления производственными процессами

Hello MES отслеживает каждой станции в hello рабочей строки до изменения состояния станции toodetect OPC UA. Он вызывает методы toocontrol hello станции OPC UA и передает продукта из одной станции toohello далее вплоть до его завершения.

## <a name="gateway-opc-publisher-module"></a>Модуль издателя OPC шлюза

Модуль издателя OPC подключается toohello станции OPC UA серверов и подписывается toohello OPC узлы toobe публикации. модуль Hello hello узел данные преобразуются в формат JSON, шифрует его и отправляет tooIoT концентратора как сообщения OPC UA Pub/Sub.

модуль издателя OPC Hello только требует исходящих https-порт (443) и может работать с существующие инфраструктуры предприятия.

## <a name="gateway-opc-proxy-module"></a>Модуль прокси OPC шлюза

Hello модуль прокси-сервера шлюза OPC UA туннели двоичные сообщения управления OPC UA и требуется только порт исходящей https (443). Он может работать с существующей инфраструктурой предприятия, в том числе с веб-прокси.

Он использует устройства IoT Hub методы tootransfer пакетный TCP/IP данные на уровне приложения hello и таким образом гарантирует доверия конечной точки, шифрование данных и целостности с помощью SSL/TLS.

Hello OPC UA двоичный протокол с ретрансляцией через прокси-сервер hello сам использует агент пользователя проверку подлинности и шифрование.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Hello шлюза OPC издателя модуль подписывается tooOPC UA сервера узлов toodetect изменения в значениях данных hello. Если обнаружено изменение данных в одном из узлов hello, этот модуль отправляет сообщения tooAzure центр IoT.

Центр IoT предоставляет tooAzure источника событий TSI. TSI хранит данные в течение 30 дней, в зависимости от отметки времени присоединенного toohello сообщений. Эти данные включают:

* OPC UA ApplicationUri;
* OPC UA NodeId;
* Значение узла hello
* метка времени источника;
* OPC UA DisplayName.

В настоящее время TSI не позволяет клиентам toocustomize продолжительность ими данные hello tookeep для.

TSI отправляет запрос к данным узла с помощью SearchSpan (Time.From, Time.To) и выполняет вычисление на основе значений OPC UA ApplicationUri, OPC UA NodeId или OPC UA DisplayName.

данные hello tooretrieve для hello OEE и ключевого показателя Эффективности датчики и диаграммы ряда времени hello, данные агрегируются по число событий, Sum, Avg, Min и Max.

Hello временных рядов создаются с помощью другого процесса. OEE и ключевые показатели эффективности, вычисленный на основе базовых данных станции и подниматься для топологии hello (производственных линиях, фабрики, enterprise) в приложении hello.

Кроме того каждый раз, когда отображается timespan готов временных рядов для топологии OEE и ключевого показателя Эффективности вычисляется в приложение hello. Например представление дня hello обновляется каждый полный час.

данные узла представления ряда времени Hello поступающие непосредственно из TSI, с помощью агрегата для timespan.

## <a name="iot-hub"></a>Центр IoT
Hello [центр IoT] [ lnk-IoT Hub] получает данные, отправляемые hello OPC издателя модуля в облаке hello и делает ее доступной toohello Azure TSI службы. 

Hello центр IoT в решении hello также:
- Хранит в реестре удостоверений, сохраняет hello идентификаторы для всех модуля OPC издателя и всех модулей OPC прокси-сервера.
- Используется как канал транспорта для двусторонней связи из hello OPC модуль прокси-сервера.

## <a name="azure-storage"></a>Хранилище Azure
Hello решение использует хранилище больших двоичных объектов как дискового хранилища для данных развертывания виртуальной Машины и toostore hello.

## <a name="web-app"></a>Веб-приложение
веб-приложение Hello развернут как часть hello предварительно настроенное решение состоит из встроенный клиент OPC UA, обработки оповещений и визуализации данных телеметрии.

## <a name="next-steps"></a>Дальнейшие действия

Вы можете продолжить, Приступая к работе с IoT Suite, считывая hello следующих статей.

* [Разрешения на сайт azureiotsuite.com hello][lnk-permissions]
* [Развертывание шлюза в Windows или Linux для hello подключен фабрики предварительно настроенных решений](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
