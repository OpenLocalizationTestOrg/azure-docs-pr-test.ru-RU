---
title: "aaaCreate Azure виртуальные сети пиринга - развертывания моделей - одной подписке | Документы Microsoft"
description: "Узнайте, как toocreate пиринг виртуальной сети между виртуальными сетями создана с помощью различных развертывания Azure существующие в модели, hello же подписки Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Создание пиринга виртуальных сетей с разными моделями развертывания в одной подписке 

В этом учебнике вы узнаете, toocreate виртуальную сеть пиринга между виртуальными сетями, созданные с помощью модели развертывания. Обе виртуальные сети существуют в hello же подписки. Пиринг два ресурса включает виртуальные сети в разных виртуальных сетей toocommunicate друг с другом и с hello же полосы пропускания и задержки, как будто hello ресурсы в hello одной виртуальной сети. Узнайте больше о [пиринге виртуальных сетей](virtual-network-peering-overview.md). 

Hello действия toocreate виртуальную сеть пиринга различаются, в зависимости от того, являются ли виртуальные сети hello hello в одном или разных, подписки и который [модели развертывания Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello виртуальные сети создаются через. Узнайте, как toocreate в виртуальной сети пиринг в других сценариях, щелкнув hello сценарий из hello в следующей таблице:

|Модель развертывания Azure  | Подписка Azure.  |
|--------- |---------|
|[Обе виртуальные сети Resource Manager](virtual-network-create-peering.md) |Аналогично|
|[Обе виртуальные сети Resource Manager](create-peering-different-subscriptions.md) |Разные|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models-subscriptions.md) |Разные|

Невозможно создать виртуальную сеть пиринга между двумя виртуальными сетями, развернутые с помощью hello классической модели развертывания. Пиринг виртуальной сети могут быть созданы только между двумя виртуальными сетями, существующие в hello же регионе Azure. Если вам требуется tooconnect виртуальных сетей, оба созданным с помощью hello классической модели развертывания или существуют в разных регионах Azure, можно использовать Azure [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello виртуальных сетей. 

Можно использовать hello [портал Azure](#portal), hello Azure [интерфейс командной строки](#cli) (CLI), или Azure [PowerShell](#powershell) toocreate пиринг виртуальной сети. Щелкните любой hello предыдущего средства ссылки toogo напрямую toohello шаги для создания виртуальной сети пиринг с помощью нравятся.

## <a name="cli"></a>Создание пиринга с помощью портала

1. Войдите в toohello [портал Azure](https://portal.azure.com). Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
2. Щелкните **+ Создать**, выберите **Сети** и щелкните **Виртуальная сеть**.
3. В hello **Создание виртуальной сети** колонки, введите, или выбрать значения для hello следующие параметры, а затем нажмите кнопку **создать**:
    - **Имя**: *myVnet1*.
    - **Адресное пространство**: *10.0.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети**: *10.0.0.0/24*.
    - **Подписка**: выберите свою подписку.
    - **Группа ресурсов**: установите флажок **Создать** и введите *myResourceGroup*.
    - **Расположение**: *Восточная часть США*.
4. Щелкните **+ Создать**. В hello **поиска hello Marketplace** введите *виртуальная сеть*. Нажмите кнопку **виртуальная сеть** когда он появится в результатах поиска hello. 
5. В hello **виртуальная сеть** колонке выберите **классический** в hello **выберите модель развертывания** , а затем щелкните **создать**.
6. В hello **Создание виртуальной сети** колонки, введите, или выбрать значения для hello следующие параметры, а затем нажмите кнопку **создать**:
    - **Имя**: *myVnet2*.
    - **Адресное пространство**: *10.1.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети:** *10.1.0.0/24*.
    - **Подписка**: выберите свою подписку.
    - **Группа ресурсов**: установите флажок **Использовать существующий** и выберите *myResourceGroup*.
    - **Расположение**: *Восточная часть США*.
7. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myResourceGroup*. Нажмите кнопку **myResourceGroup** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myresourcegroup** группы ресурсов. Группа ресурсов Hello содержит hello двух виртуальных сетей в предыдущих шагах.
8. Щелкните сеть **myVNet1**.
9. В hello **myVnet1** колонки, отображается, нажмите кнопку **Пиринги** из hello вертикальной список параметров в hello левая сторона колонка hello.
10. В hello **myVnet1 - Пиринги** колонки, которое было открыто, нажмите кнопку **+ добавить**
11. В hello **пиринг добавить** колонки, отображается, введите, или выберите hello следующие параметры, а затем нажмите кнопку **ОК**:
     - **Имя**: *myVnet1ToMyVnet2*.
     - **Модель развертывания виртуальной сети**: выберите **Классический**. 
     - **Подписка**: выберите свою подписку.
     - **Виртуальная сеть**: щелкните **Выбор виртуальной сети**, затем выберите **myVnet2**.
     - **Разрешить доступ к виртуальным сетям**: убедитесь, что выбрано значение **Включено**.
    Другие параметры в этом руководстве не используются. чтение toolearn обо всех параметрах пиринга, [управления пиринги виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
12. После нажатия кнопки **ОК** hello в предыдущем шаге, hello **пиринг добавить** колонке закрывается, и вы увидите hello **myVnet1 - Пиринги** колонке еще раз. Через несколько секунд hello пиринг был создан появится в колонке hello. **Подключение** перечисленные в hello **ПИРИНГ состояние** столбца для hello **myVnet1ToMyVnet2** пиринг можно создать.

    Hello пиринг установлен. Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
14. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete-portal) этой статьи.

## <a name="cli"></a>Создание пиринга с помощью Azure CLI

1. [Установка](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello виртуальной сети (классические).
2. Откройте окно командной строки и выполните вход с помощью hello tooAzure `azure login` команды.
3. Запустите hello CLI в режиме управления службой, введя hello `azure config mode asm` команды.
4. Введите следующую команду, toocreate hello виртуальной сети (классические) hello:
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Создайте группу ресурсов и виртуальную сеть Resource Manager. Можно использовать hello CLI 1.0 или 2.0 ([установить](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). В этом учебнике hello CLI 2.0 является виртуальной сети используется toocreate hello (диспетчера ресурсов), поскольку 2.0 должен быть пиринг используется toocreate hello. Выполнение hello следующие bash CLI сценария с локального компьютера с hello CLI 2.0.4 или более поздней версии. Параметры, на котором установлена bash сценариев CLI на клиенте Windows, см. в разделе [работающих в Windows Azure CLI hello](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Можно также запустить скрипт hello, используя hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. Нажмите кнопку hello **опробовать** кнопку в скрипте hello, показано ниже, которые вызывает облака оболочке, которая будет входить tooyour учетная запись Azure с. tooexecute Здравствуйте сценарий, нажмите кнопку hello **копирования** кнопки и вставить содержимое hello в оболочка облака, нажмите клавишу `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Создайте виртуальную сеть пиринга между hello двух виртуальных сетей создана с помощью модели развертывания hello. Скопируйте следующий скрипт tooa текстовый редактор на вашем ПК hello. Замените `<subscription id>` идентификатором своей подписки. Если вы не знаете идентификатор подписки, введите hello `az account show` команды. Здравствуйте, значение для **идентификатор** в hello выходные данные являются идентификатор вашей подписки. Вставьте скрипт hello изменен в сеансе tooyour CLI и нажмите клавишу `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. После выполнения скрипта hello, просмотрите hello пиринг для hello виртуальной сети (диспетчера ресурсов). Копировать hello следующие команды, вставьте его в текущем сеансе CLI и нажмите клавишу `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hello выходных данных указывается **подключен** в hello **PeeringState** столбца. 

    Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
9. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-cli) в этой статье.

## <a name="powershell"></a>Создание пиринга с помощью PowerShell

1. Установите последнюю версию hello hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) и [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модулей. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Запустите сеанс PowerShell.
3. В PowerShell, войдите в tooAzure, указав hello `Add-AzureAccount` команды.
4. toocreate виртуальной сети (классической) с помощью PowerShell, необходимо создать новую или изменить существующий файл конфигурации сети. Узнайте, каким образом слишком[экспорт, обновления и импорт файлов конфигурации сети](virtual-networks-using-network-configuration-file.md). Hello файл должен содержать следующие hello **VirtualNetworkSite** элемент для hello виртуальной сети, используемые в этом учебнике:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Импорт файла конфигурации сети измененные может привести к изменения tooexisting виртуальные сети (классической) для вашей подписки. Убедитесь в добавлении hello предыдущих виртуальной сети и не изменить или удалить все существующие виртуальные сети из подписки. 
5. Войдите в tooAzure toocreate hello виртуальной сети (диспетчера ресурсов), указав hello `login-azurermaccount` команды. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
6. Создайте группу ресурсов и виртуальную сеть Resource Manager. Скопируйте сценарий hello, вставьте его в PowerShell и нажмите клавишу `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Создайте виртуальную сеть пиринга между hello двух виртуальных сетей создана с помощью модели развертывания hello. Скопируйте следующий скрипт tooa текстовый редактор на вашем ПК hello. Замените `<subscription id>` идентификатором своей подписки. Если вы не знаете идентификатор подписки, введите hello `Get-AzureRmSubscription` команда tooview его. Здравствуйте, значение для **идентификатор** в hello возвращаются выводится идентификатор вашей подписки. сценарий tooexecute hello, hello копирования изменить скрипт из текстового редактора, щелкните правой кнопкой мыши в сеансе PowerShell и нажмите клавишу `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. После выполнения скрипта hello, просмотрите hello пиринг для hello виртуальной сети (диспетчера ресурсов). Копировать hello следующие команды, вставьте его в сеансе PowerShell и нажмите клавишу `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hello выходных данных указывается **подключен** в hello **PeeringState** столбца.

    Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
10. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-powershell) в этой статье.
 
## <a name="permissions"></a>Разрешения

Привет, используется toocreate пиринг виртуальной сети должны иметь hello необходимые роли и разрешения. Например если две виртуальные сети с именем myVnet1 и myVnet2 пиринг, учетной записи должно быть назначено hello следующие минимальные роли или разрешения для каждой виртуальной сети:
    
|Виртуальная сеть|Модель развертывания|Роль|Разрешения|
|---|---|---|---|
|myVnet1|Диспетчер ресурсов|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Классический|[Участник классической сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Недоступно|
|myVnet2|Диспетчер ресурсов|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Классический|[Участник классической сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Дополнительные сведения о [встроенные роли](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) и назначение разрешений для конкретного слишком[пользовательские роли](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (только для диспетчера ресурсов).

## <a name="delete"></a>Удаление ресурсов
После завершения этого учебника вы можете toodelete hello ресурсы, созданный в учебнике hello, поэтому не приводит к дополнительным расходам. При удалении группы ресурсов также удаляются все ресурсы, которые находятся в группе ресурсов hello.

### <a name="delete-portal"></a>Портал Azure

1. Введите в поле поиска портала hello, **myResourceGroup**. В результатах поиска hello, нажмите кнопку **myResourceGroup**.
2. На hello **myResourceGroup** колонка, щелкните hello **удалить** значок.
3. Удаление hello tooconfirm, в hello **ТИПА hello имя группы РЕСУРСОВ** введите **myResourceGroup**и нажмите кнопку **удалить**.

### <a name="delete-cli"></a>Интерфейс командной строки Azure

1. Используйте hello Azure CLI 2.0 toodelete hello виртуальной сети (диспетчера ресурсов) hello следующую команду:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Используйте hello Azure CLI 1.0 toodelete hello виртуальной сети (классические) hello, следующие команды:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Введите следующую команду, toodelete hello виртуальной сети (диспетчера ресурсов) hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello виртуальной сети (классической) с помощью PowerShell, необходимо изменить существующий файл конфигурации сети. Узнайте, каким образом слишком[экспорт, обновления и импорт файлов конфигурации сети](virtual-networks-using-network-configuration-file.md). Удалите следующий элемент VirtualNetworkSite для hello виртуальной сети, используемые в этом учебнике hello:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Импорт файла конфигурации сети измененные может привести к изменения tooexisting виртуальные сети (классической) для вашей подписки. Убедитесь в удалении hello предыдущих виртуальной сети и не изменить или удалить любые другие существующие виртуальные сети из подписки. 

## <a name="next-steps"></a>Дальнейшие действия

- Внимательно ознакомьтесь с важными [ограничениями и особенностями работы пиринга виртуальных сетей](virtual-network-manage-peering.md#requirements-and-constraints), прежде чем создавать пиринг виртуальных сетей для рабочей среды.
- Узнайте о [параметрах пиринга виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
- Узнайте, каким образом слишком[создать концентратор и топология сети резервный](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) с пиринг виртуальной сети.
