---
title: "пиринг виртуальная сеть Azure - aaaCreate диспетчера ресурсов - одной подписке | Документы Microsoft"
description: "Узнайте, как toocreate пиринг виртуальной сети между виртуальными сетями создан через диспетчер ресурсов, существует hello же подписки Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Создание пиринга между виртуальными сетями, развернутыми с помощью Resource Manager в одной подписке

В этом учебнике вы узнаете, toocreate виртуальную сеть пиринга между виртуальных сетей, созданные с помощью диспетчера ресурсов. Обе виртуальные сети существуют в hello же подписки. Пиринг два ресурса включает виртуальные сети в разных виртуальных сетей toocommunicate друг с другом и с hello же полосы пропускания и задержки, как будто hello ресурсы в hello одной виртуальной сети. Узнайте больше о [пиринге виртуальных сетей](virtual-network-peering-overview.md). 

Hello действия toocreate виртуальную сеть пиринга различаются, в зависимости от того, являются ли виртуальные сети hello hello в одном или разных, подписки и который [модели развертывания Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello виртуальные сети создаются через. Узнайте, как toocreate в виртуальной сети пиринг в других сценариях, щелкнув hello сценарий из hello в следующей таблице:

|Модель развертывания Azure  | Подписка Azure.  |
|--------- |---------|
|[Обе Resource Manager](create-peering-different-subscriptions.md) |Разные|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models.md) |Аналогично|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models-subscriptions.md) |Разные|

Невозможно создать виртуальную сеть пиринга между двумя виртуальными сетями, развернутые с помощью hello классической модели развертывания. Пиринг виртуальной сети могут быть созданы только между двумя виртуальными сетями, существующие в hello же регионе Azure. Если вам требуется tooconnect виртуальных сетей, оба созданным с помощью hello классической модели развертывания или существуют в разных регионах Azure, можно использовать Azure [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello виртуальных сетей. 

Можно использовать hello [портал Azure](#portal), hello Azure [интерфейс командной строки](#cli) (CLI), Azure [PowerShell](#powershell), или [шаблона Azure Resource Manager](#template) toocreate пиринг виртуальной сети. Щелкните любой hello предыдущего средства ссылки toogo напрямую toohello шаги для создания виртуальной сети пиринг с помощью нравятся.

## <a name="portal"></a>Создание пиринга с помощью портала Azure

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
4. Выполните шаги 2 – 3 опять же указать hello последующих значений на шаге 3.
    - **Имя**: *myVnet2*.
    - **Адресное пространство**: *10.1.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети:** *10.1.0.0/24*.
    - **Подписка**: выберите свою подписку.
    - **Группа ресурсов**: установите флажок **Использовать существующий** и выберите *myResourceGroup*.
    - **Расположение**: *Восточная часть США*.
5. В hello **Найдите ресурсы** поле вверху hello портала hello, тип *myResourceGroup*. Нажмите кнопку **myResourceGroup** когда он появится в результатах поиска hello. Стоечный модуль появится для hello **myresourcegroup** группы ресурсов. Группа ресурсов Hello содержит hello двух виртуальных сетей в предыдущих шагах.
6. Щелкните сеть **myVNet1**.
7. В hello **myVnet1** колонки, отображается, нажмите кнопку **Пиринги** из hello вертикальной список параметров в hello левая сторона колонка hello.
8. В hello **myVnet1 - Пиринги** колонки, которое было открыто, нажмите кнопку **+ добавить**
9. В hello **пиринг добавить** колонки, отображается, введите, или выберите hello следующие параметры, а затем нажмите кнопку **ОК**:
     - **Имя**: *myVnet1ToMyVnet2*.
     - **Модель развертывания виртуальной сети**: выберите **Resource Manager**. 
     - **Подписка**: выберите свою подписку.
     - **Виртуальная сеть**: щелкните **Выбор виртуальной сети**, затем выберите **myVnet2**.
     - **Разрешить доступ к виртуальным сетям**: убедитесь, что выбрано значение **Включено**.
    Другие параметры в этом руководстве не используются. чтение toolearn обо всех параметрах пиринга, [управления пиринги виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
10. После нажатия кнопки **ОК** hello в предыдущем шаге, hello **пиринг добавить** колонке закрывается, и вы увидите hello **myVnet1 - Пиринги** колонке еще раз. Через несколько секунд hello пиринг был создан появится в колонке hello. **Инициировано** перечисленные в hello **ПИРИНГ состояние** столбца для hello **myVnet1ToMyVnet2** пиринг можно создать. Одноранговыми Vnet1 tooVnet2, но теперь необходимо однорангового узла myVnet2 toomyVnet1. пиринг Hello должны создаваться в обоих направлениях tooenable ресурсов в виртуальные сети toocommunicate hello друг с другом.
11. Выполните шаги 5–10 для myVnet2.  Имя пиринга hello *myVnet2ToMyVnet1*.
12. Через несколько секунд после нажатия кнопки **ОК** toocreate hello пиринг для MyVnet2, hello **myVnet2ToMyVnet1** отмечены только что созданный план для пиринга **подключен** в hello  **СОСТОЯНИЕ ПИРИНГА** столбца.
13. Выполните шаги 5–7 для myVnet1. Hello **ПИРИНГ состояние** для hello **myVnet1ToVNet2** пиринг теперь также является **подключен**. пиринг Hello успешно установлено, проверив **подключен** в hello **ПИРИНГ состояние** столбца для обеих виртуальных сетей в пиринге hello.
14. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
15. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete-portal) этой статьи.

Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Создание пиринга с помощью Azure CLI

Здравствуйте, следующий скрипт:

- Требуется hello Azure CLI версия 2.0.4 или более поздней версии. версия toofind hello, запустите hello `az --version` команды. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Этот сценарий работает в оболочке Bash. Параметры запуска на клиенте Windows Azure CLI скриптов см [работающих в Windows Azure CLI hello](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Вместо установки hello CLI и его зависимости, можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. Нажмите кнопку hello **опробовать** кнопку в скрипте hello, показано ниже, которые вызывает облака оболочке, которая будет входить tooyour учетная запись Azure с. tooexecute Здравствуйте сценарий, нажмите кнопку hello **копирования** кнопку и вставьте содержимое hello в облаке оболочка.

1. Создайте группу ресурсов и две виртуальные сети.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Создайте виртуальную сеть пиринга между двумя виртуальными сетями hello.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. После выполнения скрипта hello, просмотрите hello пиринги для каждой виртуальной сети. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hello предыдущего снова выполните команду, заменив *myVnet1* с *myVnet2*. выходные данные Hello обоих команд показано **подключен** в hello **PeeringState** столбца.

     Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
5. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-cli) в этой статье.


## <a name="powershell"></a>Создание пиринга с помощью PowerShell

1. Установите последнюю версию hello hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart сеанс PowerShell перейдите слишком**запустить**, введите **powershell**и нажмите кнопку **PowerShell**.
3. В PowerShell, войдите в tooAzure, указав hello `login-azurermaccount` команды. Hello учетной записи, использованной для входа в систему должен иметь необходимые разрешения toocreate hello пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
4. Создайте группу ресурсов и две виртуальные сети. сценарий tooexecute hello, копировать hello следующую скрипта, вставьте его в PowerShell и нажмите клавишу `Enter` после последняя строка hello отображается на экране приветствия:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Создайте виртуальную сеть пиринга между двумя виртуальными сетями hello. Копирования hello следующий скрипт, вставьте в tooPowerShell и нажмите клавишу `Enter` после последняя строка hello отображается на экране приветствия:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello подсетей для виртуальной сети hello, копировать hello следующую команду, вставьте в tooPowerShell и нажмите клавишу `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hello предыдущего снова выполните команду, заменив *myVnet1* с *myVnet2*. выходные данные Hello обоих команд показано **подключен** в hello **PeeringState** столбца.
7. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
8. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-powershell) в этой статье.

Все ресурсы Azure, созданные в любой виртуальной сети, теперь может toocommunicate друг с другом через свои IP-адреса. При использовании разрешение имен Azure по умолчанию для виртуальных сетей hello hello ресурсы в виртуальных сетях hello не может tooresolve имен между виртуальными сетями hello. Если требуется tooresolve имен между виртуальными сетями в пиринге необходимо создать собственный DNS-сервер. Узнайте, как tooset копирование [разрешение имен с помощью DNS-сервере](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Создание пиринга с помощью шаблона Resource Manager

1. В качестве примера используйте шаблон Azure Resource Manager для [создания пиринга виртуальных сетей](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering). Инструкции приведены шаблоном hello развертывания hello шаблона с помощью hello портал Azure, PowerShell или Azure CLI hello. Журнал в средстве toowhichever выбранный шаблон hello toodeploy с учетной записью, обладающей hello toocreate необходимые разрешения пиринг виртуальной сети. В разделе hello [разрешения](#permissions) Дополнительные сведения см.
2. **Необязательный**: хотя Создание виртуальных машин не освещены в учебнике, можно создать виртуальную машину в каждой виртуальной сети и подключение из одной виртуальной машины toohello других, toovalidate подключения.
3. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в hello [удаление ресурсов](#delete) hello данной статьи с помощью портала Azure, PowerShell или Azure CLI hello.

## <a name="permissions"></a>Разрешения

Привет, используется toocreate пиринг виртуальной сети должны иметь hello необходимые роли и разрешения. Например если две виртуальные сети, с именем VNet1 и VNet2 пиринг, учетной записи должно быть назначено hello следующие минимальные роли или разрешения для каждой виртуальной сети:
    
|Виртуальная сеть|Роль|Разрешения|
|---|---|---|
|VNet1|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Дополнительные сведения о [встроенные роли](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) и назначение разрешений для конкретного слишком[пользовательские роли](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (только для диспетчера ресурсов).

## <a name="delete"></a>Удаление ресурсов
После завершения этого учебника вы можете toodelete hello ресурсы, созданный в учебнике hello, поэтому не приводит к дополнительным расходам. При удалении группы ресурсов также удаляются все ресурсы, которые находятся в группе ресурсов hello.

### <a name="delete-portal"></a>Портал Azure

1. Введите в поле поиска портала hello, **myResourceGroup**. В результатах поиска hello, нажмите кнопку **myResourceGroup**.
2. На hello **myResourceGroup** колонка, щелкните hello **удалить** значок.
3. Удаление hello tooconfirm, в hello **ТИПА hello имя группы РЕСУРСОВ** введите **myResourceGroup**и нажмите кнопку **удалить**.

### <a name="delete-cli"></a>Интерфейс командной строки Azure

Введите следующую команду hello:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Введите следующую команду hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Дальнейшие действия

- Внимательно ознакомьтесь с важными [ограничениями и особенностями работы пиринга виртуальных сетей](virtual-network-manage-peering.md#requirements-and-constraints), прежде чем создавать пиринг виртуальных сетей для рабочей среды.
- Узнайте о [параметрах пиринга виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
- Узнайте, каким образом слишком[создать концентратор и топология сети резервный](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) с пиринг виртуальной сети.
