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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="6d487-103">Создать центр IoT с помощью поставщика ресурсов hello REST API (.NET)</span><span class="sxs-lookup"><span data-stu-id="6d487-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6d487-104">Можно использовать hello [поставщика ресурсов центра IoT API-интерфейса REST] [ lnk-rest-api] toocreate и программно управлять центры Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6d487-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="6d487-105">Этот учебник показывает, как toouse hello toocreate API-интерфейса REST поставщика ресурсов центра IoT центр IoT из программы на C#.</span><span class="sxs-lookup"><span data-stu-id="6d487-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="6d487-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d487-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6d487-107">В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6d487-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="6d487-108">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6d487-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6d487-109">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6d487-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6d487-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6d487-110">An active Azure account.</span></span> <br/><span data-ttu-id="6d487-111">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6d487-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6d487-112">[Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6d487-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="6d487-113">Подготовка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d487-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="6d487-114">В Visual Studio создайте проект Visual C# классического рабочего стола Windows, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="6d487-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="6d487-115">Имя проекта hello **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="6d487-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="6d487-116">В обозревателе решений щелкните правой кнопкой мыши свой проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6d487-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="6d487-117">Проверьте в диспетчере пакетов NuGet **включить предварительный выпуск**, а на hello **Обзор** страница поиска для **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="6d487-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="6d487-118">Выберите пакет hello, щелкните **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **я принимаю** tooaccept hello лицензий.</span><span class="sxs-lookup"><span data-stu-id="6d487-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="6d487-119">В диспетчере пакетов NuGet найдите **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="6d487-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="6d487-120">Нажмите кнопку **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **принимаю** tooaccept hello лицензии.</span><span class="sxs-lookup"><span data-stu-id="6d487-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="6d487-121">В Program.cs заменить существующий hello **с помощью** инструкции с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="6d487-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="6d487-122">В Program.cs добавьте следующие статические переменные, заменив заполнители значениями hello hello.</span><span class="sxs-lookup"><span data-stu-id="6d487-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="6d487-123">Ранее в этом учебнике вы записали **ApplicationId**, **SubscriptionId**, **TenantId** и **Password**.</span><span class="sxs-lookup"><span data-stu-id="6d487-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="6d487-124">**Имя группы ресурсов** hello имя группы ресурсов hello, используемого при создании центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="6d487-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="6d487-125">Вы можете использовать существующую группу ресурсов или новую.</span><span class="sxs-lookup"><span data-stu-id="6d487-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="6d487-126">**Имя центра IoT** — имя hello hello создается, такие как центр IoT **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="6d487-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="6d487-127">имя вашего центра IoT Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="6d487-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="6d487-128">**Имя развертывания** — это имя для развертывания hello, таких как **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="6d487-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="6d487-129">Используйте API-интерфейса REST поставщика toocreate центр IoT для hello ресурсов</span><span class="sxs-lookup"><span data-stu-id="6d487-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="6d487-130">Используйте hello [поставщика ресурсов центра IoT API-интерфейса REST] [ lnk-rest-api] toocreate центр IoT в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d487-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="6d487-131">Также можно использовать hello ресурсов поставщик API-интерфейса REST toomake изменения tooan существующий центр IoT.</span><span class="sxs-lookup"><span data-stu-id="6d487-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="6d487-132">Добавьте следующий метод tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="6d487-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="6d487-133">Добавьте следующий код toohello hello **CreateIoTHub** метод.</span><span class="sxs-lookup"><span data-stu-id="6d487-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d487-134">Этот код создает **HttpClient** hello токена проверки подлинности в заголовках hello объекта:</span><span class="sxs-lookup"><span data-stu-id="6d487-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="6d487-135">Добавьте следующий код toohello hello **CreateIoTHub** метод.</span><span class="sxs-lookup"><span data-stu-id="6d487-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d487-136">Этот код описывает toocreate концентратора IoT hello и создает представление JSON.</span><span class="sxs-lookup"><span data-stu-id="6d487-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="6d487-137">Текущий список расположений, которые поддерживают Центр IoT hello. в разделе [состояние Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="6d487-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="6d487-138">Добавьте следующий код toohello hello **CreateIoTHub** метод.</span><span class="sxs-lookup"><span data-stu-id="6d487-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d487-139">Этот код отправляет запрос tooAzure hello REST.</span><span class="sxs-lookup"><span data-stu-id="6d487-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="6d487-140">затем кода Hello проверяет ответ hello и извлекает hello URL-адрес, состояние hello toomonitor hello задачи развертывания можно использовать:</span><span class="sxs-lookup"><span data-stu-id="6d487-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="6d487-141">Добавить следующий код toohello конец hello hello **CreateIoTHub** метод.</span><span class="sxs-lookup"><span data-stu-id="6d487-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d487-142">Этот код использует hello **asyncStatusUri** адрес извлекается в toowait предыдущего шага hello для hello toocomplete развертывания:</span><span class="sxs-lookup"><span data-stu-id="6d487-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="6d487-143">Добавить следующий код toohello конец hello hello **CreateIoTHub** метод.</span><span class="sxs-lookup"><span data-stu-id="6d487-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d487-144">Этот код извлекает ключи hello hello центр IoT был создан и выводит их toohello консоли:</span><span class="sxs-lookup"><span data-stu-id="6d487-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="6d487-145">Приложение hello завершения и выполнения</span><span class="sxs-lookup"><span data-stu-id="6d487-145">Complete and run hello application</span></span>

<span data-ttu-id="6d487-146">Теперь вы можете завершить приложение hello, вызывающему Привет **CreateIoTHub** метод перед построением и запустите его.</span><span class="sxs-lookup"><span data-stu-id="6d487-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="6d487-147">Добавить следующий код toohello конец hello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="6d487-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="6d487-148">Щелкните **Построить** и **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="6d487-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="6d487-149">Исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="6d487-149">Correct any errors.</span></span>

3. <span data-ttu-id="6d487-150">Нажмите кнопку **отладки** и затем **начать отладку** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6d487-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="6d487-151">Он может занять несколько минут для развертывания toorun hello.</span><span class="sxs-lookup"><span data-stu-id="6d487-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="6d487-152">tooverify добавленный приложения hello новый центр IoT hello посещение [портал Azure] [ lnk-azure-portal] и Просмотр списка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d487-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="6d487-153">Можно также использовать hello **Get-AzureRmResource** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d487-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="6d487-154">В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="6d487-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="6d487-155">Когда вы закончите, можно удалить центр IoT hello через hello [портал Azure] [ lnk-azure-portal] или с помощью hello **Remove-AzureRmResource** командлета PowerShell при завершении.</span><span class="sxs-lookup"><span data-stu-id="6d487-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d487-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d487-156">Next steps</span></span>
<span data-ttu-id="6d487-157">Теперь развертывания с помощью поставщика ресурсов hello API-интерфейса REST центра IoT можно дополнительно tooexplore:</span><span class="sxs-lookup"><span data-stu-id="6d487-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="6d487-158">Узнайте о возможностях hello hello [поставщика ресурсов центра IoT API-интерфейса REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="6d487-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="6d487-159">Чтение [Обзор диспетчера ресурсов Azure] [ lnk-azure-rm-overview] toolearn больше о возможностях hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6d487-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="6d487-160">toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="6d487-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="6d487-161">[Введение tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="6d487-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="6d487-162">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="6d487-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="6d487-163">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="6d487-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6d487-164">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6d487-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
