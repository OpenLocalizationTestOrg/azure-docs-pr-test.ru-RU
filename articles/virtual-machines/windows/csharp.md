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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="88be1-103">Развертывание виртуальной машины Azure с помощью C#</span><span class="sxs-lookup"><span data-stu-id="88be1-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="88be1-104">[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="88be1-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="88be1-105">В этой статье описывается создание, управление и удаление ресурсов виртуальной машины, с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="88be1-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="88be1-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="88be1-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88be1-107">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88be1-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="88be1-108">Установить пакет hello</span><span class="sxs-lookup"><span data-stu-id="88be1-108">Install hello package</span></span>
> * <span data-ttu-id="88be1-109">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="88be1-109">Create credentials</span></span>
> * <span data-ttu-id="88be1-110">Создание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="88be1-110">Create resources</span></span>
> * <span data-ttu-id="88be1-111">Выполнение задач управления.</span><span class="sxs-lookup"><span data-stu-id="88be1-111">Perform management tasks</span></span>
> * <span data-ttu-id="88be1-112">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="88be1-112">Delete resources</span></span>
> * <span data-ttu-id="88be1-113">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="88be1-113">Run hello application</span></span>

<span data-ttu-id="88be1-114">Занимает около 20 минут toodo следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88be1-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="88be1-115">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88be1-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="88be1-116">Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="88be1-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="88be1-117">Выберите **разработки настольных приложений .NET** на hello рабочих нагрузок страницы и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="88be1-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="88be1-118">В hello сводки, можно видеть, что **средства разработки .NET Framework 4 4.6** автоматически выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="88be1-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="88be1-119">Если вы уже установили Visual Studio, можно добавить hello рабочей нагрузки .NET с помощью hello запуска Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88be1-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="88be1-120">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="88be1-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="88be1-121">В **шаблоны** > **Visual C#**выберите **консольного приложения (.NET Framework)**, введите *myDotnetProject* имени hello Здравствуйте, проект, выберите hello расположение проекта hello, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="88be1-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="88be1-122">Установить пакет hello</span><span class="sxs-lookup"><span data-stu-id="88be1-122">Install hello package</span></span>

<span data-ttu-id="88be1-123">Пакеты NuGet — это hello простым способом tooinstall hello библиотеки требуется toofinish следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88be1-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="88be1-124">tooget hello библиотеки, необходимые в Visual Studio, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="88be1-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="88be1-125">Щелкните **Сервис** > **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="88be1-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="88be1-126">В консоли hello, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="88be1-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="88be1-127">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="88be1-127">Create credentials</span></span>

<span data-ttu-id="88be1-128">Перед началом этого шага убедитесь, что доступ tooan [участника-службы Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88be1-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="88be1-129">Также необходимо записать идентификатор приложения hello, hello ключ проверки подлинности и ИД клиента hello, необходимое на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="88be1-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="88be1-130">Создание файла авторизации hello</span><span class="sxs-lookup"><span data-stu-id="88be1-130">Create hello authorization file</span></span>

1. <span data-ttu-id="88be1-131">В обозревателе решений щелкните правой кнопкой мыши *myDotnetProject* > **Добавить** > **Новый элемент** и в списке **Элементы Visual C#** выберите *Текстовый файл*.</span><span class="sxs-lookup"><span data-stu-id="88be1-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="88be1-132">Имя файла hello *azureauth.properties*, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="88be1-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="88be1-133">Добавьте следующие свойства авторизации:</span><span class="sxs-lookup"><span data-stu-id="88be1-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="88be1-134">Замените  **&lt;идентификатор подписки&gt;**  на идентификатор вашей подписки  **&lt;идентификатор приложения&gt;**  с hello приложение Active Directory идентификатор,  **&lt;ключ проверки подлинности&gt;**  с ключом приложения hello, и  **&lt;ИД клиента&gt;**  с клиентом hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="88be1-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="88be1-135">Сохраните файл azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="88be1-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="88be1-136">Задайте переменную среды, в Windows с именем AZURE_AUTH_LOCATION и hello полный путь tooauthorization созданного файла.</span><span class="sxs-lookup"><span data-stu-id="88be1-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="88be1-137">Например можно использовать следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="88be1-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="88be1-138">Создание клиента управления hello</span><span class="sxs-lookup"><span data-stu-id="88be1-138">Create hello management client</span></span>

1. <span data-ttu-id="88be1-139">Откройте файл Program.cs hello для hello проект, созданный и затем добавьте следующие инструкции toohello существующие операторы using в верхней части файла hello:</span><span class="sxs-lookup"><span data-stu-id="88be1-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="88be1-140">клиент управления toocreate hello, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="88be1-141">Создание ресурсов</span><span class="sxs-lookup"><span data-stu-id="88be1-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="88be1-142">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="88be1-142">Create hello resource group</span></span>

<span data-ttu-id="88be1-143">Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88be1-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="88be1-144">toospecify значений для приложения hello и создать группу ресурсов hello, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="88be1-145">Создать группу доступности hello</span><span class="sxs-lookup"><span data-stu-id="88be1-145">Create hello availability set</span></span>

<span data-ttu-id="88be1-146">[Наборы доступности](tutorial-availability-sets.md) упростить для вас toomaintain hello виртуальных машин, используемых приложением.</span><span class="sxs-lookup"><span data-stu-id="88be1-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="88be1-147">доступность hello toocreate значение, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="88be1-148">Создать общедоступный IP-адрес hello</span><span class="sxs-lookup"><span data-stu-id="88be1-148">Create hello public IP address</span></span>

<span data-ttu-id="88be1-149">Объект [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) — необходимые toocommunicate с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="88be1-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="88be1-150">toocreate hello общедоступный IP-адрес для виртуальной машины hello, добавьте этот код toohello метода Main.</span><span class="sxs-lookup"><span data-stu-id="88be1-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="88be1-151">Создайте виртуальную сеть hello</span><span class="sxs-lookup"><span data-stu-id="88be1-151">Create hello virtual network</span></span>

<span data-ttu-id="88be1-152">Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88be1-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="88be1-153">toocreate a подсети и виртуальной сети, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="88be1-154">Создание сетевого интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="88be1-154">Create hello network interface</span></span>

<span data-ttu-id="88be1-155">Виртуальная машина должна toocommunicate интерфейса сети hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="88be1-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="88be1-156">toocreate сетевого интерфейса, добавьте этот код toohello метода Main.</span><span class="sxs-lookup"><span data-stu-id="88be1-156">toocreate a network interface, add this code toohello Main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="88be1-157">Создание виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="88be1-157">Create hello virtual machine</span></span>

<span data-ttu-id="88be1-158">Теперь, когда вы создали все hello, ресурсы поддержки, можно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="88be1-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="88be1-159">toocreate Здравствуйте виртуальной машины, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

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
> <span data-ttu-id="88be1-160">Данный учебник создает виртуальную машину под управлением версии операционной системы Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="88be1-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="88be1-161">toolearn Дополнительные сведения о выборе других изображений. в разделе [перехода, а затем выберите образы виртуальных машин Azure с помощью Windows PowerShell и hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88be1-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="88be1-162">Если вы хотите toouse существующий диск вместо образа marketplace, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="88be1-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="88be1-163">Выполнение задач управления</span><span class="sxs-lookup"><span data-stu-id="88be1-163">Perform management tasks</span></span>

<span data-ttu-id="88be1-164">Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="88be1-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="88be1-165">Кроме того вы можете toocreate tooautomate повторяющихся или сложных задач кода.</span><span class="sxs-lookup"><span data-stu-id="88be1-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="88be1-166">Если вам требуется toodo никаких действий с hello виртуальной Машины, необходимые tooget его экземпляр.</span><span class="sxs-lookup"><span data-stu-id="88be1-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="88be1-167">Получение сведений о hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="88be1-167">Get information about hello VM</span></span>

<span data-ttu-id="88be1-168">tooget сведения о виртуальной машине hello, добавьте этот код toohello метода Main.</span><span class="sxs-lookup"><span data-stu-id="88be1-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

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

### <a name="stop-hello-vm"></a><span data-ttu-id="88be1-169">Остановить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="88be1-169">Stop hello VM</span></span>

<span data-ttu-id="88be1-170">Остановка виртуальной машины и оставьте все параметры, но продолжить toobe оплачивать или можно остановить виртуальную машину и освободить ее.</span><span class="sxs-lookup"><span data-stu-id="88be1-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="88be1-171">При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="88be1-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="88be1-172">toostop hello виртуальной машины не освобождает его, добавьте этот код toohello метода Main.</span><span class="sxs-lookup"><span data-stu-id="88be1-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="88be1-173">При необходимости toodeallocate hello виртуальной машины, измените hello выключена вызов toothis кода:</span><span class="sxs-lookup"><span data-stu-id="88be1-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="88be1-174">Запуск hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="88be1-174">Start hello VM</span></span>

<span data-ttu-id="88be1-175">toostart Здравствуйте виртуальной машины, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="88be1-176">Изменение размера виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="88be1-176">Resize hello VM</span></span>

<span data-ttu-id="88be1-177">При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания.</span><span class="sxs-lookup"><span data-stu-id="88be1-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="88be1-178">Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="88be1-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="88be1-179">размер toochange hello виртуальной машины, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="88be1-180">Добавить toohello диска данных виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="88be1-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="88be1-181">tooadd виртуальная машина toohello диск данных добавьте этот код toohello основной метод tooadd диск, который имеет размер, Хань LUN 0 и типом кэширования ReadWrite в 2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="88be1-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="88be1-182">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="88be1-182">Delete resources</span></span>

<span data-ttu-id="88be1-183">Поскольку вы оплачивать ресурсы, используемые в Azure, всегда является хорошей практикой toodelete ресурсы, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="88be1-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="88be1-184">Если необходимо, чтобы toodelete hello виртуальных машин и поддержку ресурсов все hello, все, что есть toodo — удалить группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="88be1-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="88be1-185">toodelete hello ресурсов группы, добавьте этот код toohello метод Main:</span><span class="sxs-lookup"><span data-stu-id="88be1-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="88be1-186">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="88be1-186">Run hello application</span></span>

<span data-ttu-id="88be1-187">Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish.</span><span class="sxs-lookup"><span data-stu-id="88be1-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="88be1-188">toorun hello консольное приложение, нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="88be1-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="88be1-189">Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify hello Создание ресурсов hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="88be1-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="88be1-190">Щелкните hello развертывания toosee сведения о состоянии развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="88be1-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88be1-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="88be1-191">Next steps</span></span>
* <span data-ttu-id="88be1-192">Воспользоваться преимуществами toocreate шаблона виртуальной машины, используя сведения о hello в [развертывание виртуальной машины Azure с помощью C# и шаблона диспетчера ресурсов](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88be1-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="88be1-193">Дополнительные сведения об использовании hello [библиотек Azure для .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="88be1-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

