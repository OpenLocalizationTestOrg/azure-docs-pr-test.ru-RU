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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Создание виртуальных машин Windows в Azure и управление ими с помощью Java

[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure. В этой статье описывается создание, управление и удаление ресурсов виртуальной машины с помощью Java. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание проекта Maven
> * Добавление зависимостей
> * Создание учетных данных
> * Создание ресурсов.
> * Выполнение задач управления.
> * Удаление ресурсов
> * Запустите приложение hello

Занимает около 20 минут toodo следующие действия.

## <a name="create-a-maven-project"></a>Создание проекта Maven

1. Установите [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html), если это еще не сделано.
2. Установите [Maven](http://maven.apache.org/download.cgi).
3. Создайте новый проект папку и hello:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Добавление зависимостей

1. В разделе hello `testAzureApp` папки, откройте hello `pom.xml` и добавьте конфигурацию сборки hello слишком&lt;проекта&gt; tooenable hello построение приложения:

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

2. Добавьте зависимости hello, необходимые tooaccess hello Java Azure SDK.

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

3. Сохраните файл hello.

## <a name="create-credentials"></a>Создание учетных данных

Перед началом этого шага убедитесь, что доступ tooan [участника-службы Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Также необходимо записать идентификатор приложения hello, hello ключ проверки подлинности и ИД клиента hello, необходимое на более позднем этапе.

### <a name="create-hello-authorization-file"></a>Создание файла авторизации hello

1. Создайте файл с именем `azureauth.properties` и добавьте эти свойства tooit:

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

2. Сохраните файл hello.
3. Задайте переменную среды с именем AZURE_AUTH_LOCATION в оболочка с toohello проверки подлинности hello полный путь к файлу.

### <a name="create-hello-management-client"></a>Создание клиента управления hello

1. Откройте hello `App.java` файл `src\main\java\com\fabrikam` и убедитесь, что эта инструкция пакета вверху hello:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. В области инструкции пакета hello, добавьте следующие операторы импорта:
   
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

2. учетные данные Active Directory hello toocreate необходимые запросы toomake, добавьте этот код toohello основного метода класса приложения hello:
   
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

## <a name="create-resources"></a>Создание ресурсов

### <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).

toospecify значений для приложения hello и создать группу ресурсов hello, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Создать группу доступности hello

[Наборы доступности](tutorial-availability-sets.md) упростить для вас toomaintain hello виртуальных машин, используемых приложением.

доступность hello toocreate значение, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Создать общедоступный IP-адрес hello

Объект [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) — необходимые toocommunicate с виртуальной машиной hello.

toocreate hello общедоступный IP-адрес для виртуальной машины hello, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Создайте виртуальную сеть hello

Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

toocreate a подсети и виртуальной сети, добавьте этот блок try toohello код в метод main hello:

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

### <a name="create-hello-network-interface"></a>Создание сетевого интерфейса hello

Виртуальная машина должна toocommunicate интерфейса сети hello виртуальной сети.

toocreate сетевого интерфейса, добавьте этот блок try toohello код в метод main hello:

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

### <a name="create-hello-virtual-machine"></a>Создание виртуальной машины hello

Теперь, когда вы создали все hello, ресурсы поддержки, можно создать виртуальную машину.

toocreate Здравствуйте виртуальной машины, добавьте этот блок try toohello код в метод main hello:

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
> Данный учебник создает виртуальную машину под управлением версии операционной системы Windows Server hello. toolearn Дополнительные сведения о выборе других изображений. в разделе [перехода, а затем выберите образы виртуальных машин Azure с помощью Windows PowerShell и hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Если вы хотите toouse существующий диск вместо образа marketplace, используйте следующий код: 

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

## <a name="perform-management-tasks"></a>Выполнение задач управления

Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины. Кроме того вы можете toocreate tooautomate повторяющихся или сложных задач кода.

При необходимости toodo никаких действий с hello ВМ необходимо tooget его экземпляр. Добавьте этот код блока try toohello hello основного метода:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Получение сведений о hello виртуальной Машины

tooget сведения о виртуальной машине hello, добавьте этот блок try toohello код в метод main hello:

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

### <a name="stop-hello-vm"></a>Остановить hello виртуальной Машины

Остановка виртуальной машины и оставьте все параметры, но продолжить toobe оплачивать или можно остановить виртуальную машину и освободить ее. При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.

toostop hello виртуальной машины не освобождает его, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

При необходимости toodeallocate hello виртуальной машины, измените hello выключена вызов toothis кода:

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Запуск hello виртуальной Машины

toostart Здравствуйте виртуальной машины, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Изменение размера виртуальной Машины hello

При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания. Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).  

toochange размер виртуальной машины hello, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Добавить toohello диска данных виртуальной Машины

tooadd данных диска toohello виртуальной машины, составляет 2 ГБ в размере, имеет LUN 0 и типом кэширования ReadWrite, добавьте этот блок try toohello код в метод main hello:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Удаление ресурсов

Поскольку вы оплачивать ресурсы, используемые в Azure, всегда является хорошей практикой toodelete ресурсы, которые больше не нужны. Если необходимо, чтобы toodelete hello виртуальных машин и поддержку ресурсов все hello, все, что есть toodo — удалить группу ресурсов hello.

1. ресурс hello toodelete группу, добавить блок try toohello этот код в метод main hello:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Сохраните файл App.java hello.

## <a name="run-hello-application"></a>Запустите приложение hello

Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish.

1. toorun Здравствуйте, приложения, используйте следующую команду Maven:

    ```
    mvn compile exec:java
    ```

2. Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify hello Создание ресурсов hello в hello портал Azure. Щелкните hello развертывания toosee сведения о состоянии развертывания hello.


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения об использовании hello [библиотек Azure для Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

