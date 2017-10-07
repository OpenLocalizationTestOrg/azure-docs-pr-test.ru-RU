---
title: "aaaDeploy в виртуальную Машину с помощью C# и шаблона диспетчера ресурсов | Документы Microsoft"
description: "Дополнительные сведения, toouse toohow C# и toodeploy шаблона диспетчера ресурсов виртуальной Машины Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="e9f60-103">Развертывание виртуальной машины Azure с помощью C# и шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e9f60-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="e9f60-104">В этой статье показано, как toodeploy шаблона Azure Resource Manager с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="e9f60-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="e9f60-105">Hello шаблон, который вы создаете развертывает одной виртуальной машины под управлением Windows Server в новую виртуальную сеть с одной подсетью.</span><span class="sxs-lookup"><span data-stu-id="e9f60-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="e9f60-106">Подробное описание hello ресурса виртуальной машины см. в разделе [виртуальные машины в шаблоне Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="e9f60-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="e9f60-107">Дополнительные сведения обо всех ресурсах hello в шаблоне см. в разделе [Пошаговое руководство шаблона Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e9f60-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="e9f60-108">Занимает около 10 минут toodo следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e9f60-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="e9f60-109">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9f60-109">Create a Visual Studio project</span></span>

<span data-ttu-id="e9f60-110">На этом шаге вы убедитесь, что установлена среда Visual Studio и создать шаблон консольного приложения, используемого toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="e9f60-111">Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="e9f60-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="e9f60-112">Выберите **разработки настольных приложений .NET** на hello рабочих нагрузок страницы и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="e9f60-113">В hello сводки, можно видеть, что **средства разработки .NET Framework 4 4.6** автоматически выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="e9f60-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="e9f60-114">Если вы уже установили Visual Studio, можно добавить hello рабочей нагрузки .NET с помощью hello запуска Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9f60-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="e9f60-115">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="e9f60-116">В **шаблоны** > **Visual C#**выберите **консольного приложения (.NET Framework)**, введите *myDotnetProject* имени hello Здравствуйте, проект, выберите hello расположение проекта hello, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="e9f60-117">Установить пакеты hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-117">Install hello packages</span></span>

<span data-ttu-id="e9f60-118">Пакеты NuGet — это hello простым способом tooinstall hello библиотеки требуется toofinish следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e9f60-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="e9f60-119">tooget hello библиотеки, необходимые в Visual Studio, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e9f60-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="e9f60-120">Щелкните **Сервис** > **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="e9f60-121">В консоли hello, введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e9f60-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="e9f60-122">Создание файлов hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-122">Create hello files</span></span>

<span data-ttu-id="e9f60-123">На этом шаге создается файл шаблона, которая развертывает hello ресурсы и файл параметров, который предоставляет шаблон toohello значения параметра.</span><span class="sxs-lookup"><span data-stu-id="e9f60-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="e9f60-124">Можно также создать файла авторизации, который является используется tooperform операции диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e9f60-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="e9f60-125">Создайте файл шаблона hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-125">Create hello template file</span></span>

1. <span data-ttu-id="e9f60-126">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="e9f60-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e9f60-127">Имя файла hello *CreateVMTemplate.json*, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="e9f60-128">Добавьте этот файл toohello JSON код, созданный вами:</span><span class="sxs-lookup"><span data-stu-id="e9f60-128">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. <span data-ttu-id="e9f60-129">Сохраните файл CreateVMTemplate.json hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="e9f60-130">Создание файла параметров hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-130">Create hello parameters file</span></span>

<span data-ttu-id="e9f60-131">toospecify значения для параметров ресурсов hello, которые определены в шаблоне hello, создайте файл параметров, содержащий значения hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="e9f60-132">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="e9f60-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e9f60-133">Имя файла hello *Parameters.json*, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="e9f60-134">Добавьте этот файл toohello JSON код, созданный вами:</span><span class="sxs-lookup"><span data-stu-id="e9f60-134">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. <span data-ttu-id="e9f60-135">Сохраните файл Parameters.json hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="e9f60-136">Создание файла авторизации hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-136">Create hello authorization file</span></span>

<span data-ttu-id="e9f60-137">Перед развертыванием шаблона убедитесь, что доступ tooan [участника-службы Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e9f60-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="e9f60-138">Из hello участника-службы получить токен для проверки подлинности запросов tooAzure диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e9f60-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="e9f60-139">Также следует записать идентификатор приложения hello, ключ проверки подлинности hello и hello ИД клиента, необходимо в файле авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="e9f60-140">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="e9f60-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="e9f60-141">Имя файла hello *azureauth.properties*, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="e9f60-142">Добавьте следующие свойства авторизации:</span><span class="sxs-lookup"><span data-stu-id="e9f60-142">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="e9f60-143">Замените  **&lt;идентификатор подписки&gt;**  на идентификатор вашей подписки  **&lt;идентификатор приложения&gt;**  с hello приложение Active Directory идентификатор,  **&lt;ключ проверки подлинности&gt;**  с ключом приложения hello, и  **&lt;ИД клиента&gt;**  с клиентом hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e9f60-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="e9f60-144">Сохраните файл azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="e9f60-145">Задать переменную среды в Windows с именем AZURE_AUTH_LOCATION и hello полный путь tooauthorization файл, созданный, например hello следующие можно использовать команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e9f60-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="e9f60-146">Создание клиента управления hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-146">Create hello management client</span></span>

1. <span data-ttu-id="e9f60-147">Откройте файл Program.cs hello для hello проект, созданный и затем добавьте следующие инструкции toohello существующие операторы using в верхней части файла hello:</span><span class="sxs-lookup"><span data-stu-id="e9f60-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="e9f60-148">клиент управления toocreate hello, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="e9f60-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="e9f60-149">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e9f60-149">Create a resource group</span></span>

<span data-ttu-id="e9f60-150">toospecify значений для приложения hello, добавьте метод Main toohello кода:</span><span class="sxs-lookup"><span data-stu-id="e9f60-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e9f60-151">Создать учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="e9f60-151">Create a storage account</span></span>

<span data-ttu-id="e9f60-152">Hello шаблона и параметров развертываются из учетной записи хранилища в Azure.</span><span class="sxs-lookup"><span data-stu-id="e9f60-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="e9f60-153">На этом шаге создания учетной записи hello и отправить файлы hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="e9f60-154">toocreate Здравствуйте, учетная запись, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="e9f60-154">toocreate hello account, add this code toohello Main method:</span></span>

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a><span data-ttu-id="e9f60-155">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-155">Deploy hello template</span></span>

<span data-ttu-id="e9f60-156">Развертывание шаблона hello и параметров из учетной записи хранения hello, который был создан.</span><span class="sxs-lookup"><span data-stu-id="e9f60-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="e9f60-157">шаблон toodeploy hello, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="e9f60-157">toodeploy hello template, add this code toohello Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a><span data-ttu-id="e9f60-158">Удаление ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-158">Delete hello resources</span></span>

<span data-ttu-id="e9f60-159">Поскольку вы оплачивать ресурсы, используемые в Azure, всегда является хорошей практикой toodelete ресурсы, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="e9f60-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="e9f60-160">Не нужно toodelete каждого ресурса, отдельно от группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e9f60-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="e9f60-161">Удаление группы ресурсов hello и всех его ресурсов автоматически удаляются.</span><span class="sxs-lookup"><span data-stu-id="e9f60-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="e9f60-162">toodelete hello ресурсов группы, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="e9f60-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="e9f60-163">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="e9f60-163">Run hello application</span></span>

<span data-ttu-id="e9f60-164">Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish.</span><span class="sxs-lookup"><span data-stu-id="e9f60-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="e9f60-165">toorun hello консольное приложение, нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="e9f60-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="e9f60-166">Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify hello Создание ресурсов hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e9f60-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="e9f60-167">Щелкните hello развертывания toosee сведения о состоянии развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="e9f60-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9f60-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9f60-168">Next steps</span></span>
* <span data-ttu-id="e9f60-169">Если возникли проблемы с развертыванием hello, следующим шагом будет toolook в [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e9f60-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e9f60-170">Узнайте, как toodeploy виртуальной машины и ее вспомогательные ресурсы, просмотрев [развертывания Azure виртуальной машины с помощью C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e9f60-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
