---
title: "aaaCreate и управлять Azure виртуальной машины с помощью C# | Документы Microsoft"
description: "Используйте C# и диспетчера ресурсов Azure toodeploy виртуальную машину, а также все вспомогательные ресурсы."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Развертывание виртуальной машины Azure с помощью C# #

[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure. В этой статье описывается создание, управление и удаление ресурсов виртуальной машины, с помощью C#. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание проекта Visual Studio
> * Установить пакет hello
> * Создание учетных данных
> * Создание ресурсов.
> * Выполнение задач управления.
> * Удаление ресурсов
> * Запустите приложение hello

Занимает около 20 минут toodo следующие действия.

## <a name="create-a-visual-studio-project"></a>Создание проекта Visual Studio

1. Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Выберите **разработки настольных приложений .NET** на hello рабочих нагрузок страницы и нажмите кнопку **установить**. В hello сводки, можно видеть, что **средства разработки .NET Framework 4 4.6** автоматически выбирается автоматически. Если вы уже установили Visual Studio, можно добавить hello рабочей нагрузки .NET с помощью hello запуска Visual Studio.
2. В Visual Studio выберите **Файл** > **Создать** > **Проект**.
3. В **шаблоны** > **Visual C#**выберите **консольного приложения (.NET Framework)**, введите *myDotnetProject* имени hello Здравствуйте, проект, выберите hello расположение проекта hello, а затем нажмите кнопку **ОК**.

## <a name="install-hello-package"></a>Установить пакет hello

Пакеты NuGet — это hello простым способом tooinstall hello библиотеки требуется toofinish следующие действия. tooget hello библиотеки, необходимые в Visual Studio, выполните следующие действия:

1. Щелкните **Сервис** > **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.
2. В консоли hello, введите следующую команду:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Создание учетных данных

Перед началом этого шага убедитесь, что доступ tooan [участника-службы Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Также необходимо записать идентификатор приложения hello, hello ключ проверки подлинности и ИД клиента hello, необходимое на более позднем этапе.

### <a name="create-hello-authorization-file"></a>Создание файла авторизации hello

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
4. Задайте переменную среды, в Windows с именем AZURE_AUTH_LOCATION и hello полный путь tooauthorization созданного файла. Например можно использовать следующую команду PowerShell hello:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Создание клиента управления hello

1. Откройте файл Program.cs hello для hello проект, созданный и затем добавьте следующие инструкции toohello существующие операторы using в верхней части файла hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
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

## <a name="create-resources"></a>Создание ресурсов

### <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).

toospecify значений для приложения hello и создать группу ресурсов hello, добавьте этот код toohello метод Main:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Создать группу доступности hello

[Наборы доступности](tutorial-availability-sets.md) упростить для вас toomaintain hello виртуальных машин, используемых приложением.

доступность hello toocreate значение, добавьте этот код toohello метод Main:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Создать общедоступный IP-адрес hello

Объект [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) — необходимые toocommunicate с виртуальной машиной hello.

toocreate hello общедоступный IP-адрес для виртуальной машины hello, добавьте этот код toohello метода Main.
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Создайте виртуальную сеть hello

Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

toocreate a подсети и виртуальной сети, добавьте этот код toohello метод Main:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Создание сетевого интерфейса hello

Виртуальная машина должна toocommunicate интерфейса сети hello виртуальной сети.

toocreate сетевого интерфейса, добавьте этот код toohello метода Main.

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a>Создание виртуальной машины hello

Теперь, когда вы создали все hello, ресурсы поддержки, можно создать виртуальную машину.

toocreate Здравствуйте виртуальной машины, добавьте этот код toohello метод Main:

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> Данный учебник создает виртуальную машину под управлением версии операционной системы Windows Server hello. toolearn Дополнительные сведения о выборе других изображений. в разделе [перехода, а затем выберите образы виртуальных машин Azure с помощью Windows PowerShell и hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Если вы хотите toouse существующий диск вместо образа marketplace, используйте следующий код:

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a>Выполнение задач управления

Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины. Кроме того вы можете toocreate tooautomate повторяющихся или сложных задач кода.

Если вам требуется toodo никаких действий с hello виртуальной Машины, необходимые tooget его экземпляр.

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Получение сведений о hello виртуальной Машины

tooget сведения о виртуальной машине hello, добавьте этот код toohello метода Main.

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a>Остановить hello виртуальной Машины

Остановка виртуальной машины и оставьте все параметры, но продолжить toobe оплачивать или можно остановить виртуальную машину и освободить ее. При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.

toostop hello виртуальной машины не освобождает его, добавьте этот код toohello метода Main.

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

При необходимости toodeallocate hello виртуальной машины, измените hello выключена вызов toothis кода:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Запуск hello виртуальной Машины

toostart Здравствуйте виртуальной машины, добавьте этот код toohello метод Main:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Изменение размера виртуальной Машины hello

При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания. Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).  

размер toochange hello виртуальной машины, добавьте этот код toohello метод Main:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Добавить toohello диска данных виртуальной Машины

tooadd виртуальная машина toohello диск данных добавьте этот код toohello основной метод tooadd диск, который имеет размер, Хань LUN 0 и типом кэширования ReadWrite в 2 ГБ.

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Удаление ресурсов

Поскольку вы оплачивать ресурсы, используемые в Azure, всегда является хорошей практикой toodelete ресурсы, которые больше не нужны. Если необходимо, чтобы toodelete hello виртуальных машин и поддержку ресурсов все hello, все, что есть toodo — удалить группу ресурсов hello.

toodelete hello ресурсов группы, добавьте этот код toohello метод Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Запустите приложение hello

Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish. 

1. toorun hello консольное приложение, нажмите кнопку **запустить**.

2. Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify hello Создание ресурсов hello в hello портал Azure. Щелкните hello развертывания toosee сведения о состоянии развертывания hello.

## <a name="next-steps"></a>Дальнейшие действия
* Воспользоваться преимуществами toocreate шаблона виртуальной машины, используя сведения о hello в [развертывание виртуальной машины Azure с помощью C# и шаблона диспетчера ресурсов](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Дополнительные сведения об использовании hello [библиотек Azure для .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

