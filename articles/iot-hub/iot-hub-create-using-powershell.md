---
title: "Центр IoT Azure с помощью командлета PowerShell aaaCreate | Документы Microsoft"
description: "Как toouse toocreate командлет PowerShell центра IoT."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Создать центр IoT с помощью командлета New-AzureRmIotHub hello

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Введение

Можно использовать toocreate командлетов Azure PowerShell и управление центры Azure IoT. В этом учебнике показано как toocreate центр IoT с помощью PowerShell.

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.

toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. <br/>Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Командлеты Azure PowerShell][lnk-powershell-install].

## <a name="connect-tooyour-azure-subscription"></a>Подключение tooyour подписки Azure
В командной строке PowerShell введите hello, следующая команда toosign в tooyour подписки Azure:

```powershell
Login-AzureRmAccount
```

Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными. Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.

```powershell
Get-AzureRMSubscription
```

Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello. Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a>Создать группу ресурсов

Необходимо toodeploy группы ресурсов центра IoT. Вы можете выбрать существующую группу ресурсов или создать новую.

Можно использовать hello следующих команда toodiscover hello расположения, где можно развернуть центр IoT.

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate группу ресурсов для вашего центра IoT в одном из расположений hello поддерживается для центра IoT, hello используйте следующую команду. Этот пример создает группу ресурсов под названием **MyIoTRG1** в hello **Восток США** области:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Создание центра IoT

toocreate центр IoT в группе ресурсов hello, созданный на предыдущем шаге hello, hello используйте следующую команду. В этом примере создается **S1** концентратора вызывается **MyTestIoTHub** в hello **Восток США** области:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

Hello имя центра IoT hello должно быть уникальным.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


Можно перечислить все центры IoT hello в подписке, используя hello следующую команду:

```powershell
Get-AzureRmIotHub
```

Hello предыдущего примера добавляет S1 Стандартная центр IoT для которого взимается плата. Можно удалить центр IoT hello, с помощью hello следующую команду:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

Кроме того можно удалить группу ресурсов и Здравствуйте, все ресурсы, которые он содержит, с помощью hello следующую команду:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Дальнейшие действия

Теперь развертывания с помощью командлета PowerShell центра IoT вы можете дополнительно tooexplore:

* Узнайте о других [командлетах PowerShell для работы с Центром Интернета вещей][lnk-iothub-cmdlets].
* Узнайте о возможностях hello hello [поставщика ресурсов центра IoT API-интерфейса REST][lnk-rest-api].

toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.

* [Введение tooC SDK][lnk-c-sdk]
* [IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
