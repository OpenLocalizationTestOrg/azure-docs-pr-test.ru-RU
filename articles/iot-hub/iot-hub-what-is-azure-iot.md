---
title: "aaaAzure решений для Интернета вещей (IoT Suite) | Документы Microsoft"
description: "Обзор архитектуры решения IoT образца и его связь toodevices, hello Azure IoT Hub service, пакеты SDK Azure IoT, пакеты SDK службы Azure IoT и другими службами Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>Дальнейшие действия

Центр Интернета вещей Azure — это служба Azure, обеспечивающая надежный и защищенный двунаправленный обмен данными между серверной частью вашего решения и миллионами устройств. Она позволяет hello решения серверной части для:

* получать данные телеметрии с ваших устройств;
* Извлекая данные из потока событий устройств tooa процессора.
* получать отправляемые с устройств файлы;
* Отправка сообщений облака на устройство toospecific устройств.

Можно использовать собственное решение обратно завершить tooimplement центр IoT. Кроме того центр IoT включает удостоверение реестра используется tooprovision устройства, их учетные данные безопасности и их центра IoT toohello tooconnect права. toolearn Дополнительные сведения о центра IoT. в разделе [возможности центр IoT?] [lnk-iot-hub].

toolearn центр IoT Azure обеспечивает управление устройствами, основанную на стандартах tooremotely можно управлять, настраивать и обновлять устройства, в статье [Обзор управления устройствами с центром IoT][lnk-device-management].

tooimplement клиентским приложениям на разнообразных платформах оборудования и операционных систем, можно использовать устройства Azure IoT hello пакетов SDK. устройство Hello SDK включает библиотеки, которые упрощают отправку телеметрии tooan IoT hub и получения облака на устройство сообщений. При использовании устройства hello пакеты SDK, можно выбрать несколько сетевых протоколов toocommunicate с центром IoT. toolearn. более того, в разделе hello [сведения об устройстве SDK][lnk-device-sdks].

запущен написания кода и выполнение некоторых образцов tooget разделе hello [приступить к работе с центром IoT] [ lnk-getstarted] учебника.

Кроме того, рекомендуем ознакомиться с набором [Azure IoT Suite][lnk-iot-suite], который представляет собой коллекцию предварительно настроенных решений. IoT Suite позволяет tooget к работе и масштабировать IoT проекты tooaddress распространенные IoT сценарии — например удаленный мониторинг, управление ресурсами и превентивного обслуживания.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
