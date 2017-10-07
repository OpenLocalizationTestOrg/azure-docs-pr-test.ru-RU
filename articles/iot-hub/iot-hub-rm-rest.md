---
title: "Здравствуйте, aaaCreate концентратора Azure IoT с помощью REST API поставщика ресурсов | Документы Microsoft"
description: "Как toouse hello toocreate API-интерфейса REST поставщика ресурсов центра IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Создать центр IoT с помощью поставщика ресурсов hello REST API (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Можно использовать hello [поставщика ресурсов центра IoT API-интерфейса REST] [ lnk-rest-api] toocreate и программно управлять центры Azure IoT. Этот учебник показывает, как toouse hello toocreate API-интерфейса REST поставщика ресурсов центра IoT центр IoT из программы на C#.

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. <br/>Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Подготовка проекта Visual Studio

1. В Visual Studio создайте проект Visual C# классического рабочего стола Windows, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Имя проекта hello **CreateIoTHubREST**.

2. В обозревателе решений щелкните правой кнопкой мыши свой проект и выберите **Управление пакетами NuGet**.

3. Проверьте в диспетчере пакетов NuGet **включить предварительный выпуск**, а на hello **Обзор** страница поиска для **Microsoft.Azure.Management.ResourceManager**. Выберите пакет hello, щелкните **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **я принимаю** tooaccept hello лицензий.

4. В диспетчере пакетов NuGet найдите **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Нажмите кнопку **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **принимаю** tooaccept hello лицензии.

5. В Program.cs заменить существующий hello **с помощью** инструкции с hello, следующий код:

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. В Program.cs добавьте следующие статические переменные, заменив заполнители значениями hello hello. Ранее в этом учебнике вы записали **ApplicationId**, **SubscriptionId**, **TenantId** и **Password**. **Имя группы ресурсов** hello имя группы ресурсов hello, используемого при создании центра IoT hello. Вы можете использовать существующую группу ресурсов или новую. **Имя центра IoT** — имя hello hello создается, такие как центр IoT **MyIoTHub**. имя вашего центра IoT Hello должно быть глобально уникальным. **Имя развертывания** — это имя для развертывания hello, таких как **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Используйте API-интерфейса REST поставщика toocreate центр IoT для hello ресурсов

Используйте hello [поставщика ресурсов центра IoT API-интерфейса REST] [ lnk-rest-api] toocreate центр IoT в группе ресурсов. Также можно использовать hello ресурсов поставщик API-интерфейса REST toomake изменения tooan существующий центр IoT.

1. Добавьте следующий метод tooProgram.cs hello:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Добавьте следующий код toohello hello **CreateIoTHub** метод. Этот код создает **HttpClient** hello токена проверки подлинности в заголовках hello объекта:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Добавьте следующий код toohello hello **CreateIoTHub** метод. Этот код описывает toocreate концентратора IoT hello и создает представление JSON. Текущий список расположений, которые поддерживают Центр IoT hello. в разделе [состояние Azure][lnk-status]:

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. Добавьте следующий код toohello hello **CreateIoTHub** метод. Этот код отправляет запрос tooAzure hello REST. затем кода Hello проверяет ответ hello и извлекает hello URL-адрес, состояние hello toomonitor hello задачи развертывания можно использовать:

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. Добавить следующий код toohello конец hello hello **CreateIoTHub** метод. Этот код использует hello **asyncStatusUri** адрес извлекается в toowait предыдущего шага hello для hello toocomplete развертывания:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Добавить следующий код toohello конец hello hello **CreateIoTHub** метод. Этот код извлекает ключи hello hello центр IoT был создан и выводит их toohello консоли:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Приложение hello завершения и выполнения

Теперь вы можете завершить приложение hello, вызывающему Привет **CreateIoTHub** метод перед построением и запустите его.

1. Добавить следующий код toohello конец hello hello **Main** метод:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Щелкните **Построить** и **Построить решение**. Исправьте все ошибки.

3. Нажмите кнопку **отладки** и затем **начать отладку** toorun приложения hello. Он может занять несколько минут для развертывания toorun hello.

4. tooverify добавленный приложения hello новый центр IoT hello посещение [портал Azure] [ lnk-azure-portal] и Просмотр списка ресурсов. Можно также использовать hello **Get-AzureRmResource** командлета PowerShell.

> [!NOTE]
> В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате. Когда вы закончите, можно удалить центр IoT hello через hello [портал Azure] [ lnk-azure-portal] или с помощью hello **Remove-AzureRmResource** командлета PowerShell при завершении.

## <a name="next-steps"></a>Дальнейшие действия
Теперь развертывания с помощью поставщика ресурсов hello API-интерфейса REST центра IoT можно дополнительно tooexplore:

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

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
