---
title: "Развертывание виртуальной машины с помощью C# и шаблона Resource Manager | Документация Майкрософт"
description: "Узнайте, как использовать C# и шаблон Resource Manager для развертывания виртуальной машины Azure."
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
ms.openlocfilehash: bd1c860db026f948202cd1f3aa763b4547c597b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="5e32f-103">Развертывание виртуальной машины Azure с помощью C# и шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5e32f-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="5e32f-104">В этой статье описывается развертывание шаблона Azure Resource Manager с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="5e32f-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="5e32f-105">Создаваемый шаблон позволяет выполнить развертывание одной виртуальной машины под управлением Windows Server в новой виртуальной сети с одной подсетью.</span><span class="sxs-lookup"><span data-stu-id="5e32f-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="5e32f-106">Подробное описание ресурса виртуальной машины см. в статье [Виртуальные машины в шаблоне Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="5e32f-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="5e32f-107">Дополнительные сведения обо всех ресурсах в шаблоне см. в статье [Пошаговое руководство по созданию шаблона Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5e32f-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="5e32f-108">На выполнение этих действий требуется примерно 10 минут.</span><span class="sxs-lookup"><span data-stu-id="5e32f-108">It takes about 10 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="5e32f-109">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5e32f-109">Create a Visual Studio project</span></span>

<span data-ttu-id="5e32f-110">На этом шаге нужно убедиться, что экземпляр Visual Studio установлен, и создать консольное приложение, используемое для развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="5e32f-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span></span>

1. <span data-ttu-id="5e32f-111">Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="5e32f-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="5e32f-112">На странице рабочих нагрузок выберите **Разработка классических приложений .NET** и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-112">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="5e32f-113">В сводке вы увидите, что **средства разработки .NET Framework 4–4.6** выберутся автоматически.</span><span class="sxs-lookup"><span data-stu-id="5e32f-113">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="5e32f-114">Если вы уже установили Visual Studio, можно добавить рабочую нагрузку .NET с помощью средства запуска Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e32f-114">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="5e32f-115">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="5e32f-116">В разделе **Шаблоны** > **Visual C#** выберите пункт **Консольное приложение (.NET Framework)**, укажите имя *myDotnetProject* и расположение проекта, а затем нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-packages"></a><span data-ttu-id="5e32f-117">Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="5e32f-117">Install the packages</span></span>

<span data-ttu-id="5e32f-118">Самый простой способ установить библиотеки, необходимые для выполнения этих инструкций, — это использовать пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e32f-118">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="5e32f-119">Чтобы получить эти библиотеки в Visual Studio, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5e32f-119">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="5e32f-120">Щелкните **Сервис** > **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="5e32f-121">В консоли введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5e32f-121">Type these commands in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-the-files"></a><span data-ttu-id="5e32f-122">Создание файлов</span><span class="sxs-lookup"><span data-stu-id="5e32f-122">Create the files</span></span>

<span data-ttu-id="5e32f-123">На этом шаге вы создадите файл шаблона, который развертывает ресурсы, и файл параметров, который предоставляет значения для параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="5e32f-123">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="5e32f-124">Кроме того, создается файл авторизации, который используется для выполнения операций Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5e32f-124">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

### <a name="create-the-template-file"></a><span data-ttu-id="5e32f-125">Создание файла шаблона</span><span class="sxs-lookup"><span data-stu-id="5e32f-125">Create the template file</span></span>

1. <span data-ttu-id="5e32f-126">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="5e32f-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="5e32f-127">Назовите файл *CreateVMTemplate.json*, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-127">Name the file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="5e32f-128">Добавьте следующий код JSON в созданный файл:</span><span class="sxs-lookup"><span data-stu-id="5e32f-128">Add this JSON code to the file that you created:</span></span>

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

3. <span data-ttu-id="5e32f-129">Сохраните файл CreateVMTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5e32f-129">Save the CreateVMTemplate.json file.</span></span>

### <a name="create-the-parameters-file"></a><span data-ttu-id="5e32f-130">Создание файла параметров</span><span class="sxs-lookup"><span data-stu-id="5e32f-130">Create the parameters file</span></span>

<span data-ttu-id="5e32f-131">Чтобы задать значения для параметров ресурсов, определенных в шаблоне, создайте файл параметров, содержащий эти значения.</span><span class="sxs-lookup"><span data-stu-id="5e32f-131">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span></span>

1. <span data-ttu-id="5e32f-132">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="5e32f-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="5e32f-133">Назовите файл *Parameters.json*, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-133">Name the file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="5e32f-134">Добавьте следующий код JSON в созданный файл:</span><span class="sxs-lookup"><span data-stu-id="5e32f-134">Add this JSON code to the file that you created:</span></span>

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

4. <span data-ttu-id="5e32f-135">Сохраните файл Parameters.json.</span><span class="sxs-lookup"><span data-stu-id="5e32f-135">Save the Parameters.json file.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="5e32f-136">Создание файла авторизации</span><span class="sxs-lookup"><span data-stu-id="5e32f-136">Create the authorization file</span></span>

<span data-ttu-id="5e32f-137">Перед развертыванием шаблона убедитесь в наличии доступа к [субъекту-службе Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5e32f-137">Before you can deploy a template, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="5e32f-138">Субъект-служба предоставляет маркер для аутентификации запросов к Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5e32f-138">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span> <span data-ttu-id="5e32f-139">Кроме того, необходимо записать идентификатор приложения, ключ проверки подлинности и идентификатор клиента, которые понадобятся в файле авторизации.</span><span class="sxs-lookup"><span data-stu-id="5e32f-139">You should also record the application ID, the authentication key, and the tenant ID that you need in the authorization file.</span></span>

1. <span data-ttu-id="5e32f-140">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="5e32f-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="5e32f-141">Назовите файл *azureauth.properties* и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-141">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="5e32f-142">Добавьте следующие свойства авторизации:</span><span class="sxs-lookup"><span data-stu-id="5e32f-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="5e32f-143">Замените **&lt;subscription-id&gt;** своим идентификатором подписки, **&lt;application-id&gt;** — идентификатором приложения Active Directory, **&lt;authentication-key&gt;** — ключом приложения, а **&lt;tenant-id&gt;** — идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="5e32f-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="5e32f-144">Сохраните файл azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="5e32f-144">Save the azureauth.properties file.</span></span>
4. <span data-ttu-id="5e32f-145">Задайте переменную среды в Windows с именем AZURE_AUTH_LOCATION с полным путем к файлу авторизации, созданному вами. Например, можно использовать такую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5e32f-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created, for example the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-the-management-client"></a><span data-ttu-id="5e32f-146">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="5e32f-146">Create the management client</span></span>

1. <span data-ttu-id="5e32f-147">Откройте файл Program.cs для созданного проекта и добавьте в начало файла (к существующим операторам) следующие операторы using:</span><span class="sxs-lookup"><span data-stu-id="5e32f-147">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="5e32f-148">Чтобы создать клиент управления, добавьте следующий код в метод Main:</span><span class="sxs-lookup"><span data-stu-id="5e32f-148">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="5e32f-149">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5e32f-149">Create a resource group</span></span>

<span data-ttu-id="5e32f-150">Чтобы задать значения для приложения, добавьте код в метод Main:</span><span class="sxs-lookup"><span data-stu-id="5e32f-150">To specify values for the application, add code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="5e32f-151">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="5e32f-151">Create a storage account</span></span>

<span data-ttu-id="5e32f-152">Шаблон и параметры развертываются из учетной записи хранения в Azure.</span><span class="sxs-lookup"><span data-stu-id="5e32f-152">The template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="5e32f-153">На этом шаге создается учетная запись и отправляются файлы.</span><span class="sxs-lookup"><span data-stu-id="5e32f-153">In this step, you create the account and upload the files.</span></span> 

<span data-ttu-id="5e32f-154">Чтобы создать учетную запись, добавьте следующий код в метод Main:</span><span class="sxs-lookup"><span data-stu-id="5e32f-154">To create the account, add this code to the Main method:</span></span>

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

## <a name="deploy-the-template"></a><span data-ttu-id="5e32f-155">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="5e32f-155">Deploy the template</span></span>

<span data-ttu-id="5e32f-156">Разверните шаблон и параметры из созданной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5e32f-156">Deploy the template and parameters from the storage account that was created.</span></span> 

<span data-ttu-id="5e32f-157">Для развертывания шаблона добавьте следующий код в метод Main.</span><span class="sxs-lookup"><span data-stu-id="5e32f-157">To deploy the template, add this code to the Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter to delete the resource group...");
Console.ReadLine();
```

## <a name="delete-the-resources"></a><span data-ttu-id="5e32f-158">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="5e32f-158">Delete the resources</span></span>

<span data-ttu-id="5e32f-159">Так как за использование ресурсов Azure взимается плата, рекомендуется всегда удалять ресурсы, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="5e32f-159">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="5e32f-160">Не нужно отдельно удалять каждый ресурс из группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5e32f-160">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="5e32f-161">Удалите группу ресурсов, и все ее ресурсы будут автоматически удалены.</span><span class="sxs-lookup"><span data-stu-id="5e32f-161">Delete the resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="5e32f-162">Чтобы удалить группу ресурсов, добавьте следующий код в метод Main:</span><span class="sxs-lookup"><span data-stu-id="5e32f-162">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="5e32f-163">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="5e32f-163">Run the application</span></span>

<span data-ttu-id="5e32f-164">На полное выполнение этого консольного приложения потребуется примерно 5 минут.</span><span class="sxs-lookup"><span data-stu-id="5e32f-164">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="5e32f-165">Чтобы запустить консольное приложение, щелкните **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="5e32f-165">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="5e32f-166">Прежде чем нажать клавишу **ВВОД** и начать удаление ресурсов, потратьте несколько минут и проверьте на портале Azure, созданы ли эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5e32f-166">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="5e32f-167">Щелкните состояние развертывания, чтобы просмотреть сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="5e32f-167">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e32f-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e32f-168">Next steps</span></span>
* <span data-ttu-id="5e32f-169">При наличии проблем с развертыванием ознакомьтесь с информацией об [устранении распространенных ошибок при развертывании Azure с помощью Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="5e32f-169">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="5e32f-170">Узнайте, как развернуть виртуальную машину и ее вспомогательные ресурсы, ознакомившись с разделом [Развертывание ресурсов Azure с помощью языка C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="5e32f-170">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
