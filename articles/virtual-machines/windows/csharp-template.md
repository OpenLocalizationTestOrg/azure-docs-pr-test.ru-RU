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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Развертывание виртуальной машины Azure с помощью C# и шаблона Resource Manager
В этой статье показано, как toodeploy шаблона Azure Resource Manager с помощью C#. Hello шаблон, который вы создаете развертывает одной виртуальной машины под управлением Windows Server в новую виртуальную сеть с одной подсетью.

Подробное описание hello ресурса виртуальной машины см. в разделе [виртуальные машины в шаблоне Azure Resource Manager](template-description.md). Дополнительные сведения обо всех ресурсах hello в шаблоне см. в разделе [Пошаговое руководство шаблона Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Занимает около 10 минут toodo следующие действия.

## <a name="create-a-visual-studio-project"></a>Создание проекта Visual Studio

На этом шаге вы убедитесь, что установлена среда Visual Studio и создать шаблон консольного приложения, используемого toodeploy hello.

1. Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Выберите **разработки настольных приложений .NET** на hello рабочих нагрузок страницы и нажмите кнопку **установить**. В hello сводки, можно видеть, что **средства разработки .NET Framework 4 4.6** автоматически выбирается автоматически. Если вы уже установили Visual Studio, можно добавить hello рабочей нагрузки .NET с помощью hello запуска Visual Studio.
2. В Visual Studio выберите **Файл** > **Создать** > **Проект**.
3. В **шаблоны** > **Visual C#**выберите **консольного приложения (.NET Framework)**, введите *myDotnetProject* имени hello Здравствуйте, проект, выберите hello расположение проекта hello, а затем нажмите кнопку **ОК**.

## <a name="install-hello-packages"></a>Установить пакеты hello

Пакеты NuGet — это hello простым способом tooinstall hello библиотеки требуется toofinish следующие действия. tooget hello библиотеки, необходимые в Visual Studio, выполните следующие действия:

1. Щелкните **Сервис** > **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.
2. В консоли hello, введите следующие команды:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Создание файлов hello

На этом шаге создается файл шаблона, которая развертывает hello ресурсы и файл параметров, который предоставляет шаблон toohello значения параметра. Можно также создать файла авторизации, который является используется tooperform операции диспетчера ресурсов Azure.

### <a name="create-hello-template-file"></a>Создайте файл шаблона hello

1. В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*. Имя файла hello *CreateVMTemplate.json*, а затем нажмите кнопку **добавить**.
2. Добавьте этот файл toohello JSON код, созданный вами:

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

3. Сохраните файл CreateVMTemplate.json hello.

### <a name="create-hello-parameters-file"></a>Создание файла параметров hello

toospecify значения для параметров ресурсов hello, которые определены в шаблоне hello, создайте файл параметров, содержащий значения hello.

1. В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*. Имя файла hello *Parameters.json*, а затем нажмите кнопку **добавить**.
2. Добавьте этот файл toohello JSON код, созданный вами:

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

4. Сохраните файл Parameters.json hello.

### <a name="create-hello-authorization-file"></a>Создание файла авторизации hello

Перед развертыванием шаблона убедитесь, что доступ tooan [участника-службы Active Directory](../../resource-group-authenticate-service-principal.md). Из hello участника-службы получить токен для проверки подлинности запросов tooAzure диспетчера ресурсов. Также следует записать идентификатор приложения hello, ключ проверки подлинности hello и hello ИД клиента, необходимо в файле авторизации hello.

1. В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*. Имя файла hello *azureauth.properties*, а затем нажмите кнопку **добавить**.
2. Добавьте следующие свойства авторизации:

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

    Замените  **&lt;идентификатор подписки&gt;**  на идентификатор вашей подписки  **&lt;идентификатор приложения&gt;**  с hello приложение Active Directory идентификатор,  **&lt;ключ проверки подлинности&gt;**  с ключом приложения hello, и  **&lt;ИД клиента&gt;**  с клиентом hello идентификатор.

3. Сохраните файл azureauth.properties hello.
4. Задать переменную среды в Windows с именем AZURE_AUTH_LOCATION и hello полный путь tooauthorization файл, созданный, например hello следующие можно использовать команду PowerShell:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Создание клиента управления hello

1. Откройте файл Program.cs hello для hello проект, созданный и затем добавьте следующие инструкции toohello существующие операторы using в верхней части файла hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. клиент управления toocreate hello, добавьте этот код toohello метод Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a>Создание группы ресурсов

toospecify значений для приложения hello, добавьте метод Main toohello кода:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Создать учетную запись хранения

Hello шаблона и параметров развертываются из учетной записи хранилища в Azure. На этом шаге создания учетной записи hello и отправить файлы hello. 

toocreate Здравствуйте, учетная запись, добавьте этот код toohello метод Main:

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

## <a name="deploy-hello-template"></a>Развертывание шаблона hello

Развертывание шаблона hello и параметров из учетной записи хранения hello, который был создан. 

шаблон toodeploy hello, добавьте этот код toohello метод Main:

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

## <a name="delete-hello-resources"></a>Удаление ресурсов hello

Поскольку вы оплачивать ресурсы, используемые в Azure, всегда является хорошей практикой toodelete ресурсы, которые больше не нужны. Не нужно toodelete каждого ресурса, отдельно от группы ресурсов. Удаление группы ресурсов hello и всех его ресурсов автоматически удаляются. 

toodelete hello ресурсов группы, добавьте этот код toohello метод Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Запустите приложение hello

Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish. 

1. toorun hello консольное приложение, нажмите кнопку **запустить**.

2. Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify hello Создание ресурсов hello в hello портал Azure. Щелкните hello развертывания toosee сведения о состоянии развертывания hello.

## <a name="next-steps"></a>Дальнейшие действия
* Если возникли проблемы с развертыванием hello, следующим шагом будет toolook в [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](../../resource-manager-common-deployment-errors.md).
* Узнайте, как toodeploy виртуальной машины и ее вспомогательные ресурсы, просмотрев [развертывания Azure виртуальной машины с помощью C#](csharp.md).
