---
title: "aaaVM несколько IP-адресов с помощью Azure CLI 1.0 hello | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальную машину с помощью Azure CLI 1.0 \"hello\" | Диспетчер ресурсов."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Назначить несколько IP-адресов с помощью Azure CLI 1.0 машины toovirtual

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью hello Azure Resource Manager развертывания модели с помощью hello Azure CLI 1.0. Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания. Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами

Выполнить эту задачу с помощью hello Azure CLI 1.0 (Эта статья) или hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md). Привет, описанных ниже объясняется, как toocreate пример виртуальной Машины с несколькими IP-адресов, как описано в сценарии hello. Измените имена переменных и типы IP-адресов в соответствии с требованиями этой реализации.

1. Установка и настройка hello Azure CLI 1.0 с hello следующие шаги в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статью и войдите в учетную запись Azure с hello `azure-login` команды.

2. Создайте группу ресурсов:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Создайте виртуальную сеть:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Создание подсети в виртуальной сети hello:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Создайте учетную запись хранилища для hello виртуальной Машины. Перед запуском hello следующую команду, замените *mystorageaccount* с уникальным именем. Hello имя должно быть уникальным в пределах Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Создайте hello IP-конфигурации, сетевой Адаптер и назначьте hello IP конфигураций toohello сетевого адаптера. Можно добавить, удалить или изменить hello конфигурации при необходимости. Hello конфигурации описаны в сценарии hello:

    **IPConfig-1**

    Введите команды hello, следующие за toocreate:

    - ресурс общедоступного IP-адреса с общедоступным статическим IP-адресом;
    - Сетевой Адаптер, назначение hello общедоступный IP-адрес и статические tooit частного IP-адрес.
    
    Замените *mypublicdns* с именем, которое является уникальным в пределах hello расположение Azure.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.

    **IPConfig-2**

     Введите следующие команды toocreate hello ресурс открытый IP-адреса и новой конфигурации IP с статический общедоступный IP-адрес и статический частный IP-адрес:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    Введите следующие команды toocreate IP-адрес с статический частный IP-адрес и не общедоступный IP-адрес hello:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Хотя в данной статье назначает все tooa IP-конфигурации один сетевой Адаптер, также можно назначить несколько tooany конфигурации IP сетевого Адаптера на виртуальной машине. toolearn как прочитано виртуальной Машины с несколькими сетевыми картами toocreate hello Создание виртуальной Машины с помощью нескольких сетевых адаптеров в статье.

7. Создание виртуальной машины Linux 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello v2 tooStandard DS2 размер виртуальной Машины, например, просто добавьте следующие свойства hello `--vm-size Standard_DS3_v2` toohello `azure vm create` команду на шаге 6.

8. Введите следующая команда tooview hello Сетевых hello и hello связанные IP-конфигурации:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.

## <a name="add"></a>Добавьте IP адресов tooa виртуальной Машины

Можно добавить дополнительные частных и общедоступных IP адресов tooan существующего сетевого Адаптера, выполнив hello, описанных ниже. Hello примеры созданы на основе hello [сценарий](#Scenario) описано в этой статье.

1. Откройте Azure CLI и завершения hello, оставшиеся шаги в этом разделе в одном сеансе CLI. Если у вас еще нет Azure CLI установлен и настроен, hello завершения шагов в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статью и войдите в учетную запись Azure.

2. Выполните действия hello в одном из следующих разделах, в зависимости от требований hello.

    - **Добавление частного IP-адреса**
    
        tooadd закрытый tooa адрес IP сетевого Адаптера, необходимо создать IP-конфигурации, с помощью следующей команды hello. Hello статический адрес должен быть неиспользуемый адрес для подсети hello.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).

    - **Добавление общедоступного IP-адреса**
    
        Общедоступный IP-адрес будет добавлен, связав ее tooeither новой конфигурации IP или существующей конфигурации IP. Этапы hello в одном hello следующих разделах, сколько требуется.

        > [!NOTE]
        > За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.
        >

        **Связать новую конфигурацию IP hello ресурсов tooa**
    
        Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес. В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый. toocreate новый, введите следующую команду hello:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        toocreate новой конфигурации IP с статический частный IP-адрес и связанные hello *myPublicIP3* общедоступный IP-адрес адрес ресурса, введите следующую команду hello:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Связать существующую конфигурацию IP hello ресурсов tooan**

        Открытый ресурс IP-адреса можно только связанные tooan IP-конфигурации, уже не связан. Можно определить, имеет ли связанный общий IP-адрес IP-адрес, введя следующую команду hello.

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Поиск строки аналогично toohello, том, что следует для IPConfig 3 в hello, возвращаемые выходные данные:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        С момента hello **общедоступный IP-адрес** столбца для *IpConfig 3* является пустым, не открытого ресурса IP-адреса является в настоящее время связаны tooit. Можно добавить существующие открытый IP адрес ресурса tooIpConfig-3, или введите hello, следующая команда toocreate один:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Введите следующую команду, общедоступный IP-адрес tooassociate hello адресов toohello существующие IP конфигурации ресурса с именем hello *IPConfig 3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Просмотр hello частных IP-адресов и hello открытый IP адрес ресурсы назначенного toohello hello сетевого Адаптера, введя следующую команду:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Hello возвращено выходные данные выглядят аналогично toohello следующее:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Добавить hello частных IP-адресов вы добавили операционной системы ВМ toohello toohello сетевой Адаптер, следуя инструкциям hello hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адресов toohello операционной системы.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
