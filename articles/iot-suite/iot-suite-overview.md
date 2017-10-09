---
title: "Общие сведения о Azure IoT Suite aaaMicrosoft | Документы Microsoft"
description: "Общие сведения о том, как Azure IoT Suite доставляет Интернет вещей toocollect предварительно настроенных решений, анализ и хранения данных, предоставляют визуализацию и интеграцию с другими системами."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Общие сведения о наборе Azure IoT Suite

Hello Azure Интернета вещей (IoT) служб предоставляют широкий спектр возможностей. Это службы корпоративного уровня, которые обеспечивают:

* сбор данных с устройств;
* анализ движения потоков данных;
* хранение больших наборов данных и создание запросов к ним;
* визуализацию данных, получаемых в реальном времени, и архивных данных;
* интеграцию с системами операционных отделов организации.
* управление устройствами.

toodeliver эти возможности Azure IoT Suite вместе пакеты несколько служб Azure с пользовательскими расширениями как *предварительно настроенных решений*. Эти заранее настроенных решений являются базовой реализацией распространенные шаблоны решения IoT, сократить время hello tooreduce принимать toodeliver вашего решения IoT. С помощью hello [пакеты средств разработки программного обеспечения IoT][lnk-sdks], можно настроить и расширить эти решения toomeet требованиями. Эти решения также можно использовать как примеры и шаблоны при разработке новых решений IoT.

Hello следующие видеоматериалы содержат введение tooAzure IoT Suite:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Службы Azure IoT в наборе Azure IoT Suite
Hello предварительно настроенных решений обычно используют hello следующие службы:

* Основные tooAzure IoT Suite — hello [центр IoT Azure] [ lnk-iot-hub] службы. Эта служба предоставляет hello устройства в облако и возможности обмена сообщениями облака на устройство и действует как шлюз toohello hello облака и других ключевых служб IoT Suite hello. Hello службы позволяет tooreceive сообщений из устройства в масштабе, а также отправки команд tooyour устройств. Hello служба также позволяет слишком[управления устройствами][lnk-device-management]. Например можно настроить, перезагрузить или восстановить заводские на один или несколько концентратора toohello подключенных устройств.
* [Azure Stream Analytics][lnk-asa] обеспечивает оперативный анализ данных. IoT Suite использует службы tooprocess входящие данные телеметрии, выполнить агрегирование и обнаружения событий. Hello предварительно настроенных решений также использовать поток analytics tooprocess информационные сообщения, содержащие данные, например ответы метаданных или команды с устройств. Hello решения используют сообщения hello tooprocess Stream Analytics с устройств и доставка этих сообщений tooother служб.
* [Хранилище Azure] [ lnk-azure-storage] и [Azure Cosmos DB] [ lnk-document-db] предоставляют возможности хранения данных hello. Hello предварительно настроенного решения используют телеметрии toostore хранилища больших двоичных объектов и toomake его доступным для анализа. Hello решения с помощью Cosmos DB toostore устройства метаданных и предоставляют возможности управления устройствами hello hello решений.
* [Azure веб-приложений] [ lnk-web-apps] и [Microsoft Power BI] [ lnk-power-bi] предоставляют возможности визуализации данных hello. гибкость Hello Power BI позволяет tooquickly построения интерактивных панелей мониторинга, использующие данные IoT Suite.

Обзор архитектуры hello стандартного решения IoT см. в разделе [Microsoft Azure и hello Интернета вещей (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>предварительно настроенные решения

IoT Suite включает в себя предварительно настроенных решений, включите tooquickly вам начать работу с и tooexplore hello стандартных IoT сценариев, таких как:

* удаленный мониторинг;
* диагностическое обслуживание;
* подключенная фабрика.

Можно развернуть эти решения tooyour подписки Azure и затем запустите сценарий IoT завершения, начала до конца.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда у вас есть общие сведения о возможностях IoT Suite и каковы ее основные компоненты, Дополнительные сведения о решениях hello предварительно настроен в IoT Suite. Дополнительные сведения см. в разделе [Каковы hello Azure IoT предварительно настроенных решений?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
