---
title: "Создание Центра Интернета вещей Azure с помощью REST API поставщика ресурсов | Документация Майкрософт"
description: "Создание Центра Интернета вещей с помощью REST API поставщика ресурсов."
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
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="ca840-103">Создание Центра Интернета вещей с помощью REST API поставщика ресурсов (.NET)</span><span class="sxs-lookup"><span data-stu-id="ca840-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="ca840-104">[REST API поставщика ресурсов Центра Интернета вещей][lnk-rest-api] можно использовать для создания Центров Интернета вещей Azure и управления ими программными методами.</span><span class="sxs-lookup"><span data-stu-id="ca840-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="ca840-105">В этом учебнике показано, как использовать REST API поставщика ресурсов Центра Интернета вещей для создания Центра Интернета вещей из программы на C#.</span><span class="sxs-lookup"><span data-stu-id="ca840-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="ca840-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ca840-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ca840-107">В этой статье описывается использование модели развертывания на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca840-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ca840-108">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="ca840-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ca840-109">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ca840-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ca840-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ca840-110">An active Azure account.</span></span> <br/><span data-ttu-id="ca840-111">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ca840-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ca840-112">[Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ca840-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="ca840-113">Подготовка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca840-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="ca840-114">В Visual Studio создайте проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ca840-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ca840-115">Дайте проекту имя **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="ca840-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="ca840-116">В обозревателе решений щелкните правой кнопкой мыши свой проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ca840-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="ca840-117">В диспетчере пакетов NuGet выберите **Включить предварительные выпуски** и на странице **Обзор** найдите **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="ca840-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="ca840-118">Выберите пакет, щелкните **Установить**, на странице **Просмотр изменений** нажмите кнопку **ОК** и выберите **Я принимаю**, чтобы принять условия лицензий.</span><span class="sxs-lookup"><span data-stu-id="ca840-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="ca840-119">В диспетчере пакетов NuGet найдите **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="ca840-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="ca840-120">Щелкните **Установить**, на странице **Просмотр изменений** нажмите кнопку **ОК** и выберите **Я принимаю**, чтобы принять условия лицензии.</span><span class="sxs-lookup"><span data-stu-id="ca840-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="ca840-121">Откройте файл Program.cs и замените существующие инструкции **using** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ca840-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

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

6. <span data-ttu-id="ca840-122">В Program.cs добавьте следующие статические переменные, заменив значения заполнителей.</span><span class="sxs-lookup"><span data-stu-id="ca840-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="ca840-123">Ранее в этом учебнике вы записали **ApplicationId**, **SubscriptionId**, **TenantId** и **Password**.</span><span class="sxs-lookup"><span data-stu-id="ca840-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="ca840-124">**Resource group name** — это имя группы ресурсов, используемой при создании Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ca840-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="ca840-125">Вы можете использовать существующую группу ресурсов или новую.</span><span class="sxs-lookup"><span data-stu-id="ca840-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="ca840-126">**IoT Hub name** — это имя создаваемого Центра Интернета вещей, например **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="ca840-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="ca840-127">Имя Центра Интернета вещей должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="ca840-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="ca840-128">**Deployment name** — это имя развертывания, например **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="ca840-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="ca840-129">Использование REST API поставщика ресурсов для создания Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ca840-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="ca840-130">Используйте [REST API поставщика ресурсов Центра Интернета вещей][lnk-rest-api] для создания Центра Интернета вещей в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ca840-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="ca840-131">REST API поставщика ресурсов также можно использовать для изменения имеющегося Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ca840-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="ca840-132">Добавьте в класс Program.cs следующий метод:</span><span class="sxs-lookup"><span data-stu-id="ca840-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="ca840-133">Добавьте в метод **CreateIoTHub** следующий код.</span><span class="sxs-lookup"><span data-stu-id="ca840-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="ca840-134">Этот код создает объект **HttpClient** с маркером аутентификации в заголовках:</span><span class="sxs-lookup"><span data-stu-id="ca840-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="ca840-135">Добавьте в метод **CreateIoTHub** следующий код.</span><span class="sxs-lookup"><span data-stu-id="ca840-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="ca840-136">Этот код описывает создаваемый Центр Интернета вещей и создает представление JSON.</span><span class="sxs-lookup"><span data-stu-id="ca840-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="ca840-137">Текущий список расположений, которые поддерживают Центр Интернета вещей, указан на странице [Состояние Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="ca840-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="ca840-138">Добавьте в метод **CreateIoTHub** следующий код.</span><span class="sxs-lookup"><span data-stu-id="ca840-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="ca840-139">Этот код отправляет запрос REST в Azure.</span><span class="sxs-lookup"><span data-stu-id="ca840-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="ca840-140">Затем код проверяет ответ и получает URL-адрес, который можно использовать для контроля состояния задачи развертывания:</span><span class="sxs-lookup"><span data-stu-id="ca840-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

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

5. <span data-ttu-id="ca840-141">Добавьте в конец метода **CreateIoTHub** следующий код.</span><span class="sxs-lookup"><span data-stu-id="ca840-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="ca840-142">Этот код ожидает завершения развертывания с помощью адреса **asyncStatusUri**, полученного на предыдущем шаге:</span><span class="sxs-lookup"><span data-stu-id="ca840-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="ca840-143">Добавьте в конец метода **CreateIoTHub** следующий код.</span><span class="sxs-lookup"><span data-stu-id="ca840-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="ca840-144">Этот код получает созданные ключи Центра Интернета вещей и выводит их на консоль:</span><span class="sxs-lookup"><span data-stu-id="ca840-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="ca840-145">Завершение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ca840-145">Complete and run the application</span></span>

<span data-ttu-id="ca840-146">Теперь можно завершить приложение, вызвав метод **CreateIoTHub** , а затем собрать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="ca840-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="ca840-147">Добавьте в конец метода **Main** следующий код:</span><span class="sxs-lookup"><span data-stu-id="ca840-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="ca840-148">Щелкните **Построить** и **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="ca840-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="ca840-149">Исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="ca840-149">Correct any errors.</span></span>

3. <span data-ttu-id="ca840-150">Щелкните **Отладка** и **Начать отладку** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="ca840-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="ca840-151">Для запуска развертывания может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ca840-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="ca840-152">Чтобы убедиться, что в приложение добавлен новый Центр Интернета вещей, посетите [портал Azure][lnk-azure-portal] и просмотрите список ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ca840-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="ca840-153">Вы также можете воспользоваться командлетом PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="ca840-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="ca840-154">В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="ca840-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="ca840-155">По завершении можете удалить Центр Интернета вещей через [портал Azure][lnk-azure-portal] или с помощью командлета PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="ca840-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca840-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca840-156">Next steps</span></span>
<span data-ttu-id="ca840-157">После развертывания Центра Интернета вещей с использованием REST API вам могут понадобиться дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="ca840-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="ca840-158">Ознакомьтесь с возможностями [REST API поставщика ресурсов Центра Интернета вещей][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="ca840-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="ca840-159">Сведения о возможностях Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="ca840-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="ca840-160">Дополнительные сведения о разработке для Центра Интернета вещей см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="ca840-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="ca840-161">[Знакомство с пакетом SDK для устройств Azure IoT для C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="ca840-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="ca840-162">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="ca840-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="ca840-163">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="ca840-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ca840-164">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ca840-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
