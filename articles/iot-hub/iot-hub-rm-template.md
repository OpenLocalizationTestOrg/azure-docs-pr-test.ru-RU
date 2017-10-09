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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="08dbd-103">Создание Центра Интернета вещей с помощью шаблона Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="08dbd-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="08dbd-104">Можно использовать toocreate диспетчера ресурсов Azure и программно управлять центры Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="08dbd-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="08dbd-105">В этом учебнике показано как toouse toocreate шаблона диспетчера ресурсов Azure центра IoT из программы на C#.</span><span class="sxs-lookup"><span data-stu-id="08dbd-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="08dbd-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="08dbd-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="08dbd-107">В этой статье описан с помощью модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08dbd-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="08dbd-108">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="08dbd-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="08dbd-109">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="08dbd-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="08dbd-110">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="08dbd-110">An active Azure account.</span></span> <br/><span data-ttu-id="08dbd-111">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="08dbd-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="08dbd-112">[Учетная запись хранения Azure][lnk-storage-account], в которой можно хранить файлы шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08dbd-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="08dbd-113">[Azure PowerShell 1.0][lnk-powershell-install] или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="08dbd-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="08dbd-114">Подготовка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08dbd-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="08dbd-115">В Visual Studio создайте проект Visual C# классического рабочего стола Windows, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="08dbd-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="08dbd-116">Имя проекта hello **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="08dbd-117">В обозревателе решений щелкните правой кнопкой мыши свой проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="08dbd-118">Проверьте в диспетчере пакетов NuGet **включить предварительный выпуск**, а на hello **Обзор** страница поиска для **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="08dbd-119">Выберите пакет hello, щелкните **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **я принимаю** tooaccept hello лицензий.</span><span class="sxs-lookup"><span data-stu-id="08dbd-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="08dbd-120">В диспетчере пакетов NuGet найдите **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="08dbd-121">Нажмите кнопку **установить**в **просмотрите изменения** щелкните **ОК**, нажмите кнопку **принимаю** tooaccept hello лицензии.</span><span class="sxs-lookup"><span data-stu-id="08dbd-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="08dbd-122">В Program.cs заменить существующий hello **с помощью** инструкции с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="08dbd-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="08dbd-123">В Program.cs добавьте следующие статические переменные, заменив заполнители значениями hello hello.</span><span class="sxs-lookup"><span data-stu-id="08dbd-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="08dbd-124">Ранее в этом учебнике вы записали **ApplicationId**, **SubscriptionId**, **TenantId** и **Password**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="08dbd-125">**Имя учетной записи хранилища Azure** — имя hello hello учетной записи хранилища Azure, где хранятся файлы шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="08dbd-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="08dbd-126">**Имя группы ресурсов** hello имя группы ресурсов hello, используемого при создании центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="08dbd-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="08dbd-127">Hello имя может быть предварительно существующую или новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="08dbd-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="08dbd-128">**Имя развертывания** — это имя для развертывания hello, таких как **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="08dbd-129">Отправить шаблон toocreate центра IoT</span><span class="sxs-lookup"><span data-stu-id="08dbd-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="08dbd-130">Используйте JSON шаблонов и параметров файла toocreate центр IoT в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="08dbd-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="08dbd-131">Также можно использовать существующий концентратор IoT toomake изменения диспетчера ресурсов Azure шаблона tooan.</span><span class="sxs-lookup"><span data-stu-id="08dbd-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="08dbd-132">В обозревателе решений щелкните правой кнопкой мыши проект, выберите пункт **Добавить**, а затем щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="08dbd-133">Добавить файл JSON с именем **template.json** tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="08dbd-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="08dbd-134">tooadd стандартный toohello концентратора IoT **Восток США** область, содержимое hello замены **template.json** с hello после определения ресурса.</span><span class="sxs-lookup"><span data-stu-id="08dbd-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="08dbd-135">Hello текущий список регионов, которые поддерживают Центр IoT. в разделе [состояние Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="08dbd-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="08dbd-136">В обозревателе решений щелкните правой кнопкой мыши проект, выберите пункт **Добавить**, а затем щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="08dbd-137">Добавить файл JSON с именем **parameters.json** tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="08dbd-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="08dbd-138">Замените содержимое hello **parameters.json** с hello следующие сведения о параметрах, таких как задает имя для нового центра IoT hello **{инициалы} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="08dbd-139">Имя концентратора IoT Hello должно быть глобально уникальным, поэтому она должна содержать имя или инициалы:</span><span class="sxs-lookup"><span data-stu-id="08dbd-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="08dbd-140">В **обозревателя серверов**, соединение tooyour подписки Azure, и в хранилище Azure учетной записи создайте контейнер с именем **шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="08dbd-141">В hello **свойства** панель, набор hello **общего доступа на чтение** разрешения для hello **шаблоны** контейнера слишком**большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="08dbd-142">В **обозревателя серверов**, щелкните правой кнопкой мыши на hello **шаблоны** контейнера, а затем нажмите кнопку **контейнер больших двоичных объектов представления**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="08dbd-143">Щелкните hello **отправить BLOB-объект** кнопку, выберите два файла hello, **parameters.json** и **templates.json**, а затем нажмите кнопку **откройте** tooupload hello JSON файлы toohello **шаблоны** контейнера.</span><span class="sxs-lookup"><span data-stu-id="08dbd-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="08dbd-144">URL-адреса Hello hello больших двоичных объектов, содержащий hello данных JSON являются:</span><span class="sxs-lookup"><span data-stu-id="08dbd-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="08dbd-145">Добавьте следующий метод tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="08dbd-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="08dbd-146">Добавьте следующий код toohello hello **CreateIoTHub** метод toosubmit hello шаблонов и параметров файлы toohello диспетчера ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="08dbd-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="08dbd-147">Добавьте следующий код toohello hello **CreateIoTHub** метод, который отображает состояние hello и hello ключи для hello новый центр IoT:</span><span class="sxs-lookup"><span data-stu-id="08dbd-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="08dbd-148">Приложение hello завершения и выполнения</span><span class="sxs-lookup"><span data-stu-id="08dbd-148">Complete and run hello application</span></span>

<span data-ttu-id="08dbd-149">Теперь вы можете завершить приложение hello, вызывающему Привет **CreateIoTHub** метод перед построением и запустите его.</span><span class="sxs-lookup"><span data-stu-id="08dbd-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="08dbd-150">Добавить следующий код toohello конец hello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="08dbd-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="08dbd-151">Щелкните **Построить** и **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="08dbd-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="08dbd-152">Исправьте все ошибки.</span><span class="sxs-lookup"><span data-stu-id="08dbd-152">Correct any errors.</span></span>

3. <span data-ttu-id="08dbd-153">Нажмите кнопку **отладки** и затем **начать отладку** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="08dbd-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="08dbd-154">Он может занять несколько минут для развертывания toorun hello.</span><span class="sxs-lookup"><span data-stu-id="08dbd-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="08dbd-155">tooverify добавлено приложение hello новый центр IoT hello посещение [портал Azure] [ lnk-azure-portal] и Просмотр списка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="08dbd-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="08dbd-156">Можно также использовать hello **Get-AzureRmResource** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08dbd-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="08dbd-157">В этом примере приложения добавляется стандартный Центр Интернета вещей S1, который подлежит оплате.</span><span class="sxs-lookup"><span data-stu-id="08dbd-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="08dbd-158">Вы можете удалить центр IoT hello через hello [портал Azure] [ lnk-azure-portal] или с помощью hello **Remove-AzureRmResource** командлета PowerShell при завершении.</span><span class="sxs-lookup"><span data-stu-id="08dbd-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08dbd-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08dbd-159">Next steps</span></span>
<span data-ttu-id="08dbd-160">Теперь развертывания с помощью шаблона Azure Resource Manager с помощью программы C# центра IoT можно дополнительно tooexplore:</span><span class="sxs-lookup"><span data-stu-id="08dbd-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="08dbd-161">Узнайте о возможностях hello hello [поставщика ресурсов центра IoT API-интерфейса REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="08dbd-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="08dbd-162">Чтение [Обзор диспетчера ресурсов Azure] [ lnk-azure-rm-overview] toolearn больше о возможностях hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="08dbd-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="08dbd-163">toolearn Дополнительные сведения о разработке приложений для центра IoT см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="08dbd-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="08dbd-164">[Введение tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="08dbd-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="08dbd-165">[IoT Hub SDKs][lnk-sdks] (Пакеты SDK для Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="08dbd-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="08dbd-166">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="08dbd-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="08dbd-167">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="08dbd-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
