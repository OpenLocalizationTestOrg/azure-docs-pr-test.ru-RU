---
title: "aaaCreate и управления ими Java с помощью виртуальной машины Azure | Документы Microsoft"
description: "Используйте Java и диспетчера ресурсов Azure toodeploy виртуальную машину, а также все вспомогательные ресурсы."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="948a7-103">Создание виртуальных машин Windows в Azure и управление ими с помощью Java</span><span class="sxs-lookup"><span data-stu-id="948a7-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="948a7-104">[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="948a7-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="948a7-105">В этой статье описывается создание, управление и удаление ресурсов виртуальной машины с помощью Java.</span><span class="sxs-lookup"><span data-stu-id="948a7-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="948a7-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="948a7-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="948a7-107">Создание проекта Maven</span><span class="sxs-lookup"><span data-stu-id="948a7-107">Create a Maven project</span></span>
> * <span data-ttu-id="948a7-108">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="948a7-108">Add dependencies</span></span>
> * <span data-ttu-id="948a7-109">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="948a7-109">Create credentials</span></span>
> * <span data-ttu-id="948a7-110">Создание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="948a7-110">Create resources</span></span>
> * <span data-ttu-id="948a7-111">Выполнение задач управления.</span><span class="sxs-lookup"><span data-stu-id="948a7-111">Perform management tasks</span></span>
> * <span data-ttu-id="948a7-112">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="948a7-112">Delete resources</span></span>
> * <span data-ttu-id="948a7-113">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="948a7-113">Run hello application</span></span>

<span data-ttu-id="948a7-114">Занимает около 20 минут toodo следующие действия.</span><span class="sxs-lookup"><span data-stu-id="948a7-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="948a7-115">Создание проекта Maven</span><span class="sxs-lookup"><span data-stu-id="948a7-115">Create a Maven project</span></span>

1. <span data-ttu-id="948a7-116">Установите [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html), если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="948a7-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="948a7-117">Установите [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="948a7-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="948a7-118">Создайте новый проект папку и hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="948a7-119">Добавление зависимостей</span><span class="sxs-lookup"><span data-stu-id="948a7-119">Add dependencies</span></span>

1. <span data-ttu-id="948a7-120">В разделе hello `testAzureApp` папки, откройте hello `pom.xml` и добавьте конфигурацию сборки hello слишком&lt;проекта&gt; tooenable hello построение приложения:</span><span class="sxs-lookup"><span data-stu-id="948a7-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="948a7-121">Добавьте зависимости hello, необходимые tooaccess hello Java Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="948a7-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="948a7-122">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="948a7-123">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="948a7-123">Create credentials</span></span>

<span data-ttu-id="948a7-124">Перед началом этого шага убедитесь, что доступ tooan [участника-службы Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="948a7-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="948a7-125">Также необходимо записать идентификатор приложения hello, hello ключ проверки подлинности и ИД клиента hello, необходимое на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="948a7-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="948a7-126">Создание файла авторизации hello</span><span class="sxs-lookup"><span data-stu-id="948a7-126">Create hello authorization file</span></span>

1. <span data-ttu-id="948a7-127">Создайте файл с именем `azureauth.properties` и добавьте эти свойства tooit:</span><span class="sxs-lookup"><span data-stu-id="948a7-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="948a7-128">Замените  **&lt;идентификатор подписки&gt;**  на идентификатор вашей подписки  **&lt;идентификатор приложения&gt;**  с hello приложение Active Directory идентификатор,  **&lt;ключ проверки подлинности&gt;**  с ключом приложения hello, и  **&lt;ИД клиента&gt;**  с клиентом hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="948a7-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="948a7-129">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-129">Save hello file.</span></span>
3. <span data-ttu-id="948a7-130">Задайте переменную среды с именем AZURE_AUTH_LOCATION в оболочка с toohello проверки подлинности hello полный путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="948a7-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="948a7-131">Создание клиента управления hello</span><span class="sxs-lookup"><span data-stu-id="948a7-131">Create hello management client</span></span>

1. <span data-ttu-id="948a7-132">Откройте hello `App.java` файл `src\main\java\com\fabrikam` и убедитесь, что эта инструкция пакета вверху hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="948a7-133">В области инструкции пакета hello, добавьте следующие операторы импорта:</span><span class="sxs-lookup"><span data-stu-id="948a7-133">Under hello package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="948a7-134">учетные данные Active Directory hello toocreate необходимые запросы toomake, добавьте этот код toohello основного метода класса приложения hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="948a7-135">Создание ресурсов</span><span class="sxs-lookup"><span data-stu-id="948a7-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="948a7-136">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="948a7-136">Create hello resource group</span></span>

<span data-ttu-id="948a7-137">Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="948a7-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="948a7-138">toospecify значений для приложения hello и создать группу ресурсов hello, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="948a7-139">Создать группу доступности hello</span><span class="sxs-lookup"><span data-stu-id="948a7-139">Create hello availability set</span></span>

<span data-ttu-id="948a7-140">[Наборы доступности](tutorial-availability-sets.md) упростить для вас toomaintain hello виртуальных машин, используемых приложением.</span><span class="sxs-lookup"><span data-stu-id="948a7-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="948a7-141">доступность hello toocreate значение, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="948a7-142">Создать общедоступный IP-адрес hello</span><span class="sxs-lookup"><span data-stu-id="948a7-142">Create hello public IP address</span></span>

<span data-ttu-id="948a7-143">Объект [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) — необходимые toocommunicate с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="948a7-144">toocreate hello общедоступный IP-адрес для виртуальной машины hello, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="948a7-145">Создайте виртуальную сеть hello</span><span class="sxs-lookup"><span data-stu-id="948a7-145">Create hello virtual network</span></span>

<span data-ttu-id="948a7-146">Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="948a7-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="948a7-147">toocreate a подсети и виртуальной сети, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="948a7-148">Создание сетевого интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="948a7-148">Create hello network interface</span></span>

<span data-ttu-id="948a7-149">Виртуальная машина должна toocommunicate интерфейса сети hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="948a7-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="948a7-150">toocreate сетевого интерфейса, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="948a7-151">Создание виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="948a7-151">Create hello virtual machine</span></span>

<span data-ttu-id="948a7-152">Теперь, когда вы создали все hello, ресурсы поддержки, можно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="948a7-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="948a7-153">toocreate Здравствуйте виртуальной машины, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="948a7-154">Данный учебник создает виртуальную машину под управлением версии операционной системы Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="948a7-155">toolearn Дополнительные сведения о выборе других изображений. в разделе [перехода, а затем выберите образы виртуальных машин Azure с помощью Windows PowerShell и hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="948a7-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="948a7-156">Если вы хотите toouse существующий диск вместо образа marketplace, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="948a7-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="948a7-157">Выполнение задач управления</span><span class="sxs-lookup"><span data-stu-id="948a7-157">Perform management tasks</span></span>

<span data-ttu-id="948a7-158">Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="948a7-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="948a7-159">Кроме того вы можете toocreate tooautomate повторяющихся или сложных задач кода.</span><span class="sxs-lookup"><span data-stu-id="948a7-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="948a7-160">При необходимости toodo никаких действий с hello ВМ необходимо tooget его экземпляр.</span><span class="sxs-lookup"><span data-stu-id="948a7-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="948a7-161">Добавьте этот код блока try toohello hello основного метода:</span><span class="sxs-lookup"><span data-stu-id="948a7-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="948a7-162">Получение сведений о hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="948a7-162">Get information about hello VM</span></span>

<span data-ttu-id="948a7-163">tooget сведения о виртуальной машине hello, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="948a7-164">Остановить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="948a7-164">Stop hello VM</span></span>

<span data-ttu-id="948a7-165">Остановка виртуальной машины и оставьте все параметры, но продолжить toobe оплачивать или можно остановить виртуальную машину и освободить ее.</span><span class="sxs-lookup"><span data-stu-id="948a7-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="948a7-166">При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="948a7-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="948a7-167">toostop hello виртуальной машины не освобождает его, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="948a7-168">При необходимости toodeallocate hello виртуальной машины, измените hello выключена вызов toothis кода:</span><span class="sxs-lookup"><span data-stu-id="948a7-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="948a7-169">Запуск hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="948a7-169">Start hello VM</span></span>

<span data-ttu-id="948a7-170">toostart Здравствуйте виртуальной машины, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="948a7-171">Изменение размера виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="948a7-171">Resize hello VM</span></span>

<span data-ttu-id="948a7-172">При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания.</span><span class="sxs-lookup"><span data-stu-id="948a7-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="948a7-173">Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="948a7-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="948a7-174">toochange размер виртуальной машины hello, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="948a7-175">Добавить toohello диска данных виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="948a7-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="948a7-176">tooadd данных диска toohello виртуальной машины, составляет 2 ГБ в размере, имеет LUN 0 и типом кэширования ReadWrite, добавьте этот блок try toohello код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="948a7-177">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="948a7-177">Delete resources</span></span>

<span data-ttu-id="948a7-178">Поскольку вы оплачивать ресурсы, используемые в Azure, всегда является хорошей практикой toodelete ресурсы, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="948a7-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="948a7-179">Если необходимо, чтобы toodelete hello виртуальных машин и поддержку ресурсов все hello, все, что есть toodo — удалить группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="948a7-180">ресурс hello toodelete группу, добавить блок try toohello этот код в метод main hello:</span><span class="sxs-lookup"><span data-stu-id="948a7-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="948a7-181">Сохраните файл App.java hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="948a7-182">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="948a7-182">Run hello application</span></span>

<span data-ttu-id="948a7-183">Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish.</span><span class="sxs-lookup"><span data-stu-id="948a7-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="948a7-184">toorun Здравствуйте, приложения, используйте следующую команду Maven:</span><span class="sxs-lookup"><span data-stu-id="948a7-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="948a7-185">Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify hello Создание ресурсов hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="948a7-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="948a7-186">Щелкните hello развертывания toosee сведения о состоянии развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="948a7-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="948a7-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="948a7-187">Next steps</span></span>
* <span data-ttu-id="948a7-188">Дополнительные сведения об использовании hello [библиотек Azure для Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="948a7-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

