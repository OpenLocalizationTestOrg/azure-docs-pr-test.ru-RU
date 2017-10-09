---
title: "aaaCreate центр IoT Azure с помощью шаблона (PowerShell) | Документы Microsoft"
description: "Как toouse toocreate шаблона диспетчера ресурсов Azure центр IoT с помощью PowerShell."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Можно использовать toocreate диспетчера ресурсов Azure и программно управлять центры Azure IoT. В этом учебнике показано как toouse toocreate шаблона диспетчера ресурсов Azure центр IoT с помощью PowerShell.

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.

toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. <br/>Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.

> [!TIP]
> статья Hello [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure] [ lnk-powershell-arm] предоставляет дополнительные сведения о том, как toouse PowerShell и диспетчера ресурсов Azure шаблоны toocreate Azure ресурсы.

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

Можно использовать следующие команды toodiscover, где вы можете развернуть центр IoT и hello в настоящее время поддерживаемые версии API hello:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Создайте группы ресурсов toocontain IoT концентраторе, используя следующую команду в одном из расположений hello поддерживается для центра IoT hello. В этом примере создается группа ресурсов с именем **MyIoTRG1**.

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Отправить шаблон toocreate центра IoT

Используйте toocreate шаблона JSON центр IoT в группе ресурсов. Также можно использовать существующий концентратор IoT toomake изменения диспетчера ресурсов Azure шаблона tooan.

1. Использовать toocreate текстовый редактор, вызывается шаблона Azure Resource Manager **template.json** с hello следующие toocreate определения ресурсов Стандартная центр IoT. В этом примере добавляется hello центр IoT в hello **Восток США** области, создает две группы потребителей (**cg1** и **cg2**) на конечной точке hello совместимое концентратора событий и использует hello **2016-02-03** версия API. Этот шаблон также ожидает, что вы toopass имя концентратора IoT hello как параметр с именем **hubName**. Текущий список расположений, которые поддерживают Центр IoT hello. в разделе [состояние Azure][lnk-status].

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. Сохраните файл шаблона диспетчера ресурсов Azure hello на локальном компьютере. В этом примере предполагается, что файл сохраняется в папке **c:\templates**.

3. Выполните следующие команды toodeploy hello новый концентратор IoT, передавая имя вашего центра IoT hello в качестве параметра. В этом примере hello центра IoT hello называется `abcmyiothub`. имя вашего центра IoT Hello должно быть глобально уникальным:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. для вывода Hello hello ключи для центра IoT hello, созданный.

5. tooverify добавлено приложение hello новый центр IoT hello посещение [портал Azure] [ lnk-azure-portal] и Просмотр списка ресурсов. Можно также использовать hello **Get-AzureRmResource** командлета PowerShell.

> [!NOTE]
> В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате. Вы можете удалить центр IoT hello через hello [портал Azure] [ lnk-azure-portal] или с помощью hello **Remove-AzureRmResource** командлета PowerShell при завершении.

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы развернули центр IoT, с помощью шаблона Azure Resource Manager с помощью PowerShell, вы можете tooexplore дальнейшей:

* Узнайте о возможностях hello hello [поставщика ресурсов центра IoT API-интерфейса REST][lnk-rest-api].
* Чтение [Обзор диспетчера ресурсов Azure] [ lnk-azure-rm-overview] toolearn больше о возможностях hello диспетчера ресурсов Azure.

toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.

* [Введение tooC SDK][lnk-c-sdk]
* [IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
