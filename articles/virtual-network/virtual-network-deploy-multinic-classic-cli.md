---
title: "aaaCreate виртуальной Машины (классические) с несколькими сетевыми адаптерами - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины (классические) с несколькими сетевыми картами с помощью hello Azure командной строки (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Создание виртуальной Машины (классические) с несколькими сетевыми адаптерами, используя hello Azure CLI 1.0

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Можно создавать виртуальные машины (ВМ) в Azure и присоединить несколько tooeach сетевых интерфейсов (NIC) виртуальных машин. Применение нескольких сетевых карт дает возможность разделять типы трафика между сетевыми картами. Например один сетевой Адаптер может обмениваться данными с hello Интернета, пока другой взаимодействует только с внутренним ресурсам, не подключен toohello Интернета. для многих виртуальных сетевых устройств, таких как предоставление приложений и решений ГЛОБАЛЬНОЙ оптимизации требуется Hello возможность tooseparate сетевой трафик по нескольким сетевым картам.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, как tooperform следующие действия с помощью hello [модели развертывания диспетчера ресурсов](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.

## <a name="prerequisites"></a>Предварительные требования
Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария. toocreate эти ресурсы, полный Здравствуйте, описанных ниже. Создание виртуальной сети с помощью инструкции hello в hello [создать виртуальную сеть](virtual-networks-create-vnet-classic-cli.md) статьи.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Развертывание внутренней hello виртуальные машины
Hello ВМ внутренней зависят от создания hello hello следующие ресурсы:

* **Учетная запись хранения для дисков данных**. Для повышения производительности hello диски с данными на серверах баз данных hello будет использовать технологию твердотельный накопитель (SSD), которая требуется учетная запись хранения premium. Убедитесь, что hello расположение Azure, развертывание toosupport хранилище premium.
* **Сетевые карты**. У каждой виртуальной машины будет две сетевые карты: одна для доступа к базе данных, другая — для управления.
* **Группа доступности**. Все серверы баз данных будет добавлен tooa одну группу доступности, хотя бы один из виртуальных машин hello tooensure работает и запущена во время обслуживания.

### <a name="step-1---start-your-script"></a>Шаг 1. Запуск сценария
Вы можете загрузить hello bash полный сценарий [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Выполните следующие toowork действия toochange hello скрипта в среде hello.

1. Изменить значения hello hello переменных ниже в зависимости от вашего развертывания выше в существующую группу ресурсов [необходимых компонентов](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Изменить значения hello hello следующих переменных на основе значений hello нужно toouse для развертывания базы данных.

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Шаг 2. Создание необходимых ресурсов для виртуальных машин
1. Создайте облачную службу для всех внутренних виртуальных машин. Использование уведомления hello hello `$backendCSName` переменных для имени группы ресурсов hello, и `$location` для hello регион Azure.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Создайте учетную запись хранения premium для hello ОС и toobe дисков данных, используемые вашим виртуальных машин.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>Шаг 3. Создание виртуальных машин с несколькими сетевыми картами
1. Запуск нескольких виртуальных машин, в зависимости от hello toocreate цикла `numberOfVMs` переменных.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Для каждой виртуальной Машины укажите имя hello и IP-адрес каждого hello двух сетевых адаптеров.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Создайте hello виртуальной Машины. Обратите внимание, использование hello hello `--nic-config` параметр, содержащий список всех сетевых адаптеров с именем, подсети и IP-адрес.

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. Создайте по два диска данных для каждой виртуальной машины.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Шаг 4. выполнение сценариев hello
Теперь, когда вы загрузили и изменить скрипт hello с учетом ваших потребностей, выполнение архивации hello сценария toocreate hello последний ВМ базы данных с несколькими сетевыми адаптерами.

1. Сохраните сценарий и запустите его в терминале **Bash** . Вы увидите выходные данные начальной hello, как показано ниже.

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. Через несколько минут hello выполнение будет завершено, и вы увидите rest hello hello выходных данных, как показано ниже.

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
