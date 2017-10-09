---
title: "aaaCreate виртуальной Машины (классические) с несколькими сетевыми адаптерами - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины (классические) с несколькими сетевыми адаптерами, с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Создание виртуальных машин (классическая модель) с несколькими сетевыми интерфейсами с помощью PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Можно создавать виртуальные машины (ВМ) в Azure и присоединить несколько tooeach сетевых интерфейсов (NIC) виртуальных машин. Применение нескольких сетевых карт дает возможность разделять типы трафика между сетевыми картами. Например один сетевой Адаптер может обмениваться данными с hello Интернета, пока другой взаимодействует только с внутренним ресурсам, не подключен toohello Интернета. для многих виртуальных сетевых устройств, таких как предоставление приложений и решений ГЛОБАЛЬНОЙ оптимизации требуется Hello возможность tooseparate сетевой трафик по нескольким сетевым картам.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, как tooperform следующие действия с помощью hello [модели развертывания диспетчера ресурсов](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.

## <a name="prerequisites"></a>Предварительные требования

Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария. toocreate эти ресурсы, полный Здравствуйте, описанных ниже. Создание виртуальной сети с помощью инструкции hello в hello [создать виртуальную сеть](virtual-networks-create-vnet-classic-netcfg-ps.md) статьи.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Создать hello внутренней виртуальные машины
Hello ВМ внутренней зависят от создания hello hello следующие ресурсы:

* **Внутренняя подсеть**. серверы баз данных Hello будет частью отдельной подсети toosegregate трафика. Приведенный ниже сценарий Hello ожидает tooexist этой подсети в виртуальной сети с именем *WTestVnet*.
* **Учетная запись хранения для дисков данных**. Для повышения производительности hello диски с данными на серверах баз данных hello будет использовать технологию твердотельный накопитель (SSD), которая требуется учетная запись хранения premium. Убедитесь, что hello расположение Azure, развертывание toosupport хранилище premium.
* **Группа доступности**. Все серверы баз данных будет добавлен tooa одну группу доступности, хотя бы один из виртуальных машин hello tooensure работает и запущена во время обслуживания.

### <a name="step-1---start-your-script"></a>Шаг 1. Запуск сценария
Вы можете загрузить hello использовать полный скрипт PowerShell [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Выполните действия hello ниже toowork сценария toochange hello в вашей среде.

1. Изменить значения hello hello переменных ниже в зависимости от вашего развертывания выше в существующую группу ресурсов [необходимых компонентов](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Изменить значения hello hello следующих переменных на основе значений hello нужно toouse для развертывания базы данных.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Шаг 2. Создание необходимых ресурсов для виртуальных машин
Необходимо toocreate новой облачной службы и хранилища учетной записи для hello дисков данных для всех виртуальных машин. Необходимо также toospecify изображения, а учетная запись локального администратора для hello виртуальных машин. завершить эти ресурсы toocreate hello следующие действия:

1. Создайте облачную службу.

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Создайте учетную запись хранения класса Premium.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Набор hello учетной записи хранения создана выше как hello текущей учетной записи хранения для вашей подписки.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Выберите изображение для hello виртуальной Машины.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Задайте учетные данные учетной записи локального администратора hello.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Шаг 3. Создание виртуальных машин
Необходимо toouse toocreate цикла, как много виртуальных машин, а создать hello необходимые сетевые адаптеры и виртуальные машины в цикле hello. hello toocreate сетевых адаптеров и виртуальных машин, выполните hello следующие шаги.

1. Запуск `for` hello toorepeat цикла команды toocreate виртуальной Машины, а также две сетевые платы как столько раз, сколько необходимо, на основе hello значения hello `$numberOfVMs` переменной.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Создание `VMConfig` объект, указывающий hello изображение, размер и доступности для hello виртуальной Машины.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Здравствуйте, подготовить виртуальную Машину в качестве виртуальной Машины Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Установите сетевой Адаптер по умолчанию hello и назначьте его статический IP-адрес.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Добавьте вторую сетевую карту для каждой виртуальной машины.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Создание дисков toodata для каждой виртуальной Машины.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. Создайте каждой виртуальной Машины и hello конец цикла.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Шаг 4. выполнение сценариев hello
Теперь, когда вы загрузили и изменить скрипт hello зависимости от потребностей, runt он скрипт toocreate hello базой данных виртуальных машин с несколькими сетевыми адаптерами.

1. Сохраните сценарий и запустите его из hello **PowerShell** командной строки или **интегрированной среды Сценариев PowerShell**. Вы увидите выходные данные начальной hello, как показано ниже.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Заполните hello сведения, необходимые в hello запрос учетных данных и нажмите кнопку **ОК**. Вывод Hello ниже возвращается.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
