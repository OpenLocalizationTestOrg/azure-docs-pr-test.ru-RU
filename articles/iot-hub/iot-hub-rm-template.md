---
title: "aaaCreate центр IoT Azure с помощью шаблона (.NET) | Документы Microsoft"
description: "Как toouse toocreate шаблона диспетчера ресурсов Azure центр IoT с помощью программы C#."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Можно использовать toocreate диспетчера ресурсов Azure и программно управлять центры Azure IoT. В этом учебнике показано как toouse toocreate шаблона диспетчера ресурсов Azure центра IoT из программы на C#.

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. <br/>Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Учетная запись хранения Azure][lnk-storage-account], в которой можно хранить файлы шаблона Azure Resource Manager.
* [Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Подготовка проекта Visual Studio

1. В Visual Studio создайте проект Visual C# классического рабочего стола Windows, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Имя проекта hello **CreateIoTHub**.

2. В обозревателе решений щелкните правой кнопкой мыши свой проект и выберите **Управление пакетами NuGet**.

3. Проверьте в диспетчере пакетов NuGet **включить предварительный выпуск**, а на hello **Обзор** страница поиска для **Microsoft.Azure.Management.ResourceManager**. Выберите пакет hello, щелкните **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **я принимаю** tooaccept hello лицензий.

4. В диспетчере пакетов NuGet найдите **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Нажмите кнопку **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **принимаю** tooaccept hello лицензии.

5. В Program.cs заменить существующий hello **с помощью** инструкции с hello, следующий код:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. В Program.cs добавьте следующие статические переменные, заменив заполнители значениями hello hello. Ранее в этом учебнике вы записали **ApplicationId**, **SubscriptionId**, **TenantId** и **Password**. **Имя учетной записи хранилища Azure** — имя hello hello учетной записи хранилища Azure, где хранятся файлы шаблонов диспетчера ресурсов Azure. **Имя группы ресурсов** hello имя группы ресурсов hello, используемого при создании центра IoT hello. Hello имя может быть предварительно существующую или новую группу ресурсов. **Имя развертывания** — это имя для развертывания hello, таких как **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Отправить шаблон toocreate центра IoT

Используйте JSON шаблонов и параметров файла toocreate центр IoT в группе ресурсов. Также можно использовать существующий концентратор IoT toomake изменения диспетчера ресурсов Azure шаблона tooan.

1. В обозревателе решений щелкните правой кнопкой мыши проект, выберите пункт **Добавить**, а затем щелкните **Новый элемент**. Добавить файл JSON с именем **template.json** tooyour проекта.

2. tooadd стандартный toohello концентратора IoT **Восток США** область, содержимое hello замены **template.json** с hello после определения ресурса. Hello текущий список регионов, которые поддерживают Центр IoT. в разделе [состояние Azure][lnk-status]:

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

3. В обозревателе решений щелкните правой кнопкой мыши проект, выберите пункт **Добавить**, а затем щелкните **Новый элемент**. Добавить файл JSON с именем **parameters.json** tooyour проекта.

4. Замените содержимое hello **parameters.json** с hello следующие сведения о параметрах, таких как задает имя для нового центра IoT hello **{инициалы} mynewiothub**. Имя концентратора IoT Hello должно быть глобально уникальным, поэтому она должна содержать имя или инициалы:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. В **обозревателя серверов**, соединение tooyour подписки Azure, и в хранилище Azure учетной записи создайте контейнер с именем **шаблоны**. В hello **свойства** панель, набор hello **общего доступа на чтение** разрешения для hello **шаблоны** контейнера слишком**большого двоичного объекта**.

6. В **обозревателя серверов**, щелкните правой кнопкой мыши на hello **шаблоны** контейнера, а затем нажмите кнопку **контейнер больших двоичных объектов представления**. Щелкните hello **отправить BLOB-объект** кнопку, выберите два файла hello, **parameters.json** и **templates.json**, а затем нажмите кнопку **откройте** tooupload hello JSON файлы toohello **шаблоны** контейнера. URL-адреса Hello hello больших двоичных объектов, содержащий hello данных JSON являются:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Добавьте следующий метод tooProgram.cs hello:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Добавьте следующий код toohello hello **CreateIoTHub** метод toosubmit hello шаблонов и параметров файлы toohello диспетчера ресурсов Azure:

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. Добавьте следующий код toohello hello **CreateIoTHub** метод, который отображает состояние hello и hello ключи для hello новый центр IoT:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Приложение hello завершения и выполнения

Теперь вы можете завершить приложение hello, вызывающему Привет **CreateIoTHub** метод перед построением и запустите его.

1. Добавить следующий код toohello конец hello hello **Main** метод:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Щелкните **Построить** и **Построить решение**. Исправьте все ошибки.

3. Нажмите кнопку **отладки** и затем **начать отладку** toorun приложения hello. Он может занять несколько минут для развертывания toorun hello.

4. tooverify добавлено приложение hello новый центр IoT hello посещение [портал Azure] [ lnk-azure-portal] и Просмотр списка ресурсов. Можно также использовать hello **Get-AzureRmResource** командлета PowerShell.

> [!NOTE]
> В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате. Вы можете удалить центр IoT hello через hello [портал Azure] [ lnk-azure-portal] или с помощью hello **Remove-AzureRmResource** командлета PowerShell при завершении.

## <a name="next-steps"></a>Дальнейшие действия
Теперь развертывания с помощью шаблона Azure Resource Manager с помощью программы C# центра IoT можно дополнительно tooexplore:

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
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
