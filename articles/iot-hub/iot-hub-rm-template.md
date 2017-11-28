---
title: "Создание Центра Интернета вещей Azure с помощью шаблона (.NET) | Документация Майкрософт"
description: "Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager и программы C#."
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
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="2c206-103">Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="2c206-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="2c206-104">Диспетчер ресурсов Azure можно использовать для создания Центров Интернета вещей Azure программным способом и управления ими.</span><span class="sxs-lookup"><span data-stu-id="2c206-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="2c206-105">В этом учебнике показано, как использовать шаблон Azure Resource Manager для создания Центра Интернета вещей из программы на C#.</span><span class="sxs-lookup"><span data-stu-id="2c206-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="2c206-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2c206-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2c206-107">В этой статье описывается использование модели развертывания на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c206-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="2c206-108">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="2c206-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2c206-109">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2c206-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2c206-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2c206-110">An active Azure account.</span></span> <br/><span data-ttu-id="2c206-111">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2c206-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="2c206-112">[Учетная запись хранения Azure][lnk-storage-account], в которой можно хранить файлы шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c206-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="2c206-113">[Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2c206-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="2c206-114">Подготовка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2c206-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="2c206-115">В Visual Studio создайте проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="2c206-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="2c206-116">Дайте проекту имя **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="2c206-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="2c206-117">В обозревателе решений щелкните правой кнопкой мыши свой проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2c206-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="2c206-118">В диспетчере пакетов NuGet выберите **Включить предварительные выпуски** и на странице **Обзор** найдите **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="2c206-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="2c206-119">Выберите пакет, щелкните **Установить**, на странице **Просмотр изменений** нажмите кнопку **ОК** и выберите **Я принимаю**, чтобы принять условия лицензий.</span><span class="sxs-lookup"><span data-stu-id="2c206-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="2c206-120">В диспетчере пакетов NuGet найдите **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="2c206-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="2c206-121">Щелкните **Установить**, на странице **Просмотр изменений** нажмите кнопку **ОК** и выберите **Я принимаю**, чтобы принять условия лицензии.</span><span class="sxs-lookup"><span data-stu-id="2c206-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="2c206-122">Откройте файл Program.cs и замените существующие инструкции **using** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2c206-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="2c206-123">В Program.cs добавьте следующие статические переменные, заменив значения заполнителей.</span><span class="sxs-lookup"><span data-stu-id="2c206-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="2c206-124">Ранее в этом учебнике вы записали **ApplicationId**, **SubscriptionId**, **TenantId** и **Password**.</span><span class="sxs-lookup"><span data-stu-id="2c206-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="2c206-125">**Your Azure Storage account name** — это имя учетной записи хранения Azure, в которой вы храните файлы шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c206-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="2c206-126">**Resource group name** — это имя группы ресурсов, используемой при создании Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="2c206-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="2c206-127">Это может быть существующая группа ресурсов или новая.</span><span class="sxs-lookup"><span data-stu-id="2c206-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="2c206-128">**Deployment name** — это имя развертывания, например **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="2c206-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="2c206-129">Отправка шаблона для создания Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="2c206-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="2c206-130">Для создания Центра Интернета вещей в группе ресурсов используйте шаблон JSON и файл параметров.</span><span class="sxs-lookup"><span data-stu-id="2c206-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="2c206-131">Можно также использовать шаблон Azure Resource Manager для изменения существующего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="2c206-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="2c206-132">В обозревателе решений щелкните правой кнопкой мыши проект, выберите пункт **Добавить**, а затем щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="2c206-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2c206-133">Добавьте файл JSON с именем **template.json** в проект.</span><span class="sxs-lookup"><span data-stu-id="2c206-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="2c206-134">Для добавления стандартного Центра Интернета вещей в регион **Восточная часть США** замените содержимое файла **template.json** следующим определением ресурса.</span><span class="sxs-lookup"><span data-stu-id="2c206-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="2c206-135">Текущий список регионов, которые поддерживают Центр Интернета вещей, указан на странице [Состояние Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="2c206-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="2c206-136">В обозревателе решений щелкните правой кнопкой мыши проект, выберите пункт **Добавить**, а затем щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="2c206-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2c206-137">Добавьте в проект файл JSON с именем **parameters.json** .</span><span class="sxs-lookup"><span data-stu-id="2c206-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="2c206-138">Замените содержимое файла **parameters.json** следующим параметром, который задает имя нового Центра Интернета вещей, например **{ваши_инициалы}mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="2c206-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="2c206-139">Имя Центра Интернета вещей должно быть глобально уникальным, поэтому оно должно включать ваше имя или инициалы:</span><span class="sxs-lookup"><span data-stu-id="2c206-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="2c206-140">В **обозревателе сервера** подключитесь к подписке Azure и в учетной записи хранения Azure создайте контейнер с именем **templates**.</span><span class="sxs-lookup"><span data-stu-id="2c206-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="2c206-141">На панели **Свойства** задайте разрешениям **Общий доступ на чтение** для контейнера **templates** значение **Большой двоичный объект**.</span><span class="sxs-lookup"><span data-stu-id="2c206-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="2c206-142">В **обозревателе сервера** щелкните правой кнопкой мыши контейнер **templates**, а затем выберите **Просмотреть контейнер больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="2c206-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="2c206-143">Нажмите кнопку **Передать BLOB-объект**, выберите файлы **parameters.json** и **templates.json**, а затем нажмите кнопку **Открыть**, чтобы передать файлы JSON в контейнер **templates**.</span><span class="sxs-lookup"><span data-stu-id="2c206-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="2c206-144">URL-адреса больших двоичных объектов, содержащих данные JSON, таковы:</span><span class="sxs-lookup"><span data-stu-id="2c206-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="2c206-145">Добавьте в класс Program.cs следующий метод:</span><span class="sxs-lookup"><span data-stu-id="2c206-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="2c206-146">Добавьте следующий код в метод **CreateIoTHub** для отправки файлов шаблонов и параметров в Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2c206-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="2c206-147">Добавьте следующий код в метод **CreateIoTHub** , который отображает состояние и ключи для нового Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="2c206-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="2c206-148">Завершение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="2c206-148">Complete and run the application</span></span>

<span data-ttu-id="2c206-149">Теперь можно завершить приложение, вызвав метод **CreateIoTHub** , а затем собрать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="2c206-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="2c206-150">Добавьте в конец метода **Main** следующий код:</span><span class="sxs-lookup"><span data-stu-id="2c206-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="2c206-151">Щелкните **Построить** и **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="2c206-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="2c206-152">Исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="2c206-152">Correct any errors.</span></span>

3. <span data-ttu-id="2c206-153">Щелкните **Отладка** и **Начать отладку** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="2c206-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="2c206-154">Для запуска развертывания может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2c206-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="2c206-155">Чтобы убедиться, что в приложение добавлен новый Центр Интернета вещей, посетите [портал Azure][lnk-azure-portal] и просмотрите список ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2c206-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="2c206-156">Вы также можете воспользоваться командлетом PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="2c206-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="2c206-157">В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="2c206-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="2c206-158">Когда закончите, Центр Интернета вещей можно удалить через [портал Azure][lnk-azure-portal] или с помощью командлета PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="2c206-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c206-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c206-159">Next steps</span></span>
<span data-ttu-id="2c206-160">После развертывания Центра Интернета вещей с использованием шаблона Azure Resource Manager и программы на C# вас могут заинтересовать следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="2c206-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="2c206-161">Ознакомьтесь с возможностями [REST API поставщика ресурсов Центра Интернета вещей][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="2c206-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="2c206-162">Сведения о возможностях Azure Resource Manager см. в статье [Общие сведения об Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="2c206-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="2c206-163">Дополнительные сведения о разработке для Центра Интернета вещей см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="2c206-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="2c206-164">[Знакомство с пакетом SDK для устройств Azure IoT для C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="2c206-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="2c206-165">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="2c206-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="2c206-166">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="2c206-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2c206-167">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2c206-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
