---
title: "Создание пиринга виртуальных сетей Azure с разными моделями развертывания в одной подписке | Документация Майкрософт"
description: "Узнайте, как создать пиринг между виртуальными сетями, созданными с помощью разных моделей развертывания Azure, которые существуют в одной подписке Azure."
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
ms.date: 09/25/2017
ms.author: jdial;anavin
ms.openlocfilehash: ebe489b6e0993dad42950acdafac48e662da7f77
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Создание пиринга виртуальных сетей с разными моделями развертывания в одной подписке 

В этом руководстве вы узнаете, как создать пиринг между виртуальными сетями, созданными с помощью разных моделей развертывания. Обе виртуальные сети размещены в одной подписке. Установление пиринга между двумя виртуальными сетями позволяет ресурсам в разных виртуальных сетях взаимодействовать друг с другом с такими же пропускной способностью и задержкой, как если бы эти ресурсы находились в одной виртуальной сети. Узнайте больше о [пиринге виртуальных сетей](virtual-network-peering-overview.md). 

Действия по созданию пиринга виртуальных сетей зависят от того, находятся ли виртуальные сети в одной или разных подписках, и того, какая [модель развертывания Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) использовалась для их создания. Узнайте, как создать пиринг виртуальных сетей в других сценариях, щелкнув сценарий в следующей таблице.

|Модель развертывания Azure  | Подписка Azure.  |
|--------- |---------|
|[Обе виртуальные сети Resource Manager](virtual-network-create-peering.md) |Аналогично|
|[Обе виртуальные сети Resource Manager](create-peering-different-subscriptions.md) |Разные|
|[Одна виртуальная сеть Resource Manager, одна классическая виртуальная сеть](create-peering-different-deployment-models-subscriptions.md) |Разные|

Невозможно создать пиринг между двумя виртуальными сетями, созданными с помощью классической модели развертывания. Если вам необходимо подключить виртуальные сети, созданные с помощью классической модели развертывания, можно использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure. 

Это руководство по созданию пиринга между виртуальными сетями в одном регионе. Возможность установки пиринга между виртуальными сетями в разных регионах сейчас находится в предварительной версии. Выполните шаги в разделе [Регистрация для предварительной версии пиринга между виртуальными сетями в разных регионах](#register), прежде чем совершить попытку создать пиринг между виртуальными сетями в разных регионах (в противном случае пиринг завершится сбоем). Возможность подключения между виртуальными сетями в разных регионах с использованием [VPN-шлюза](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure находится в общем доступе и не требует регистрации.

Для создания пиринга виртуальных сетей можно использовать [портал Azure](#portal), [интерфейс командной строки](#cli) Azure (CLI), Azure [PowerShell](#powershell) или [шаблон Azure Resource Manager](#template). Щелкните любую из предыдущих ссылок на инструмент, чтобы перейти непосредственно к инструкциям по созданию пиринга виртуальных сетей с помощью выбранного инструмента.

## <a name="create-peering---azure-portal"></a>Создание пиринга с помощью портала Azure

1. Войдите на [портал Azure](https://portal.azure.com). У учетной записи, используемой для входа, должны быть необходимые разрешения для создания пиринга виртуальных сетей. Дополнительные сведения см. в разделе [Разрешения](#permissions) этой статьи.
2. Щелкните **+ Создать**, выберите **Сети** и щелкните **Виртуальная сеть**.
3. В колонке **Создание виртуальной сети** введите или выберите значения для приведенных ниже параметров и щелкните **Создать**.
    - **Имя**: *myVnet1*.
    - **Адресное пространство**: *10.0.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети**: *10.0.0.0/24*.
    - **Подписка**: выберите свою подписку.
    - **Группа ресурсов**: установите флажок **Создать** и введите *myResourceGroup*.
    - **Расположение**: *Восточная часть США*.
4. Щелкните **+ Создать**. В поле **Поиск по Marketplace** введите *Виртуальная сеть*. Когда в результатах поиска появится пункт **Виртуальная сеть**, щелкните его. 
5. В колонке **Виртуальная сеть** в поле **Выбор модели развертывания** выберите **Классический** и нажмите кнопку **Создать**.
6. В колонке **Создание виртуальной сети** введите или выберите значения для приведенных ниже параметров и щелкните **Создать**.
    - **Имя**: *myVnet2*.
    - **Адресное пространство**: *10.1.0.0/16*.
    - **Имя подсети**: *по умолчанию*.
    - **Диапазон адресов подсети:** *10.1.0.0/24*.
    - **Подписка**: выберите свою подписку.
    - **Группа ресурсов**: установите флажок **Использовать существующий** и выберите *myResourceGroup*.
    - **Расположение**: *Восточная часть США*.
7. В поле **Поиск ресурсов**, находящемся в верхней части портала, введите *myResourceGroup*. Когда группа ресурсов **myResourceGroup** появится в результатах поиска, щелкните ее. Откроется колонка группы ресурсов **myResourceGroup**. Эта группа ресурсов содержит две виртуальные сети, созданные на предыдущих шагах.
8. Щелкните сеть **myVNet1**.
9. В вертикальном списке параметров в левой части отобразившейся колонки **myVnet1** щелкните **Пиринги**.
10. В открывшейся колонке **myVnet1 — пиринги** щелкните **+ Добавить**.
11. В открывшейся колонке **Добавить пиринг** введите или выберите значения приведенных ниже параметров, после чего нажмите кнопку **ОК**.
     - **Имя**: *myVnet1ToMyVnet2*.
     - **Модель развертывания виртуальной сети**: выберите **Классический**. 
     - **Подписка**: выберите свою подписку.
     - **Виртуальная сеть**: щелкните **Выбор виртуальной сети**, затем выберите **myVnet2**.
     - **Разрешить доступ к виртуальным сетям**: убедитесь, что выбрано значение **Включено**.
    Другие параметры в этом руководстве не используются. Чтобы узнать о всех параметрах пиринга, прочитайте раздел [Создание, изменение и удаление пиринга в виртуальной сети](virtual-network-manage-peering.md#create-a-peering).
12. После нажатия кнопки **ОК** на предыдущем шаге колонка **Добавить пиринг** закроется, и вы снова увидите колонку **myVnet1 — пиринги**. Через несколько секунд созданный пиринг отобразится в этой колонке. В столбце **Состояние пиринга** для созданного пиринга **myVnet1ToMyVnet2** указано состояние **Подключено**.

    Пиринг установлен. Теперь все ресурсы Azure, созданные в любой из виртуальных сетей, могут взаимодействовать друг с другом, используя свои IP-адреса. Если вы используете разрешение имен Azure по умолчанию для виртуальных сетей, то ресурсы в этих виртуальных сетях не смогут разрешать имена между виртуальными сетями. Если требуется разрешение имен между виртуальными сетями в пиринге, необходимо создать собственный DNS-сервер. Узнайте, как настроить [разрешение имен с помощью собственного DNS-сервера](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Необязательно**. Хотя в этом руководстве не рассматривается создание виртуальных машин, можно создать по виртуальной машине в каждой виртуальной сети и подключить их между собой, чтобы проверить связь.
14. **Необязательно**. Чтобы удалить ресурсы, созданные в этом руководстве, выполните инструкции в разделе [Удаление ресурсов](#delete-portal) этой статьи.

## <a name="cli"></a>Создание пиринга с помощью Azure CLI

1. [Установите](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure CLI 1.0 для создания классической виртуальной сети.
2. Запустите сеанс командной строки и войдите в Azure с помощью команды `azure login`.
3. Запустите интерфейс командной строки в режиме управления службами, введя команду `azure config mode asm`.
4. Чтобы создать классическую виртуальную сеть, введите приведенную ниже команду.
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Создайте группу ресурсов и виртуальную сеть Resource Manager. Можно использовать Azure CLI 1.0 или 2.0 ([установить](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). В этом руководстве для создания виртуальной сети Resource Manager используется Azure CLI 2.0, так как для создания пиринга должна использоваться версия 2.0. Выполните следующий сценарий Bash для интерфейса командной строки на локальном компьютере, на котором установлен Azure CLI 2.0.4 или более поздней версии. Сведения о параметрах выполнения сценариев Bash для интерфейса командной строки в клиенте Windows см. в статье [Использование Azure CLI в Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Можно также запустить сценарий с помощью Azure Cloud Shell. Azure Cloud Shell — это бесплатная оболочка Bash, которую можно запускать непосредственно на портале Azure. Она включает предварительно установленный интерфейс Azure CLI и настроена для использования с вашей учетной записью. Нажмите кнопку **Попробовать** в следующем сценарии, чтобы запустить службу Cloud Shell, с помощью которой можно войти в свою учетную запись Azure. Чтобы выполнить сценарий, нажмите кнопку **Скопировать** и вставьте содержимое в Cloud Shell. Нажмите клавишу `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create the virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Создайте пиринг между двумя виртуальными сетями, созданными с помощью разных моделей развертывания. Скопируйте следующий сценарий в текстовый редактор на своем компьютере. Замените `<subscription id>` идентификатором своей подписки. Если вам неизвестен идентификатор подписки, введите команду `az account show`. Значение **id** (Идентификатор) в выходных данных является идентификатором вашей подписки. Вставьте измененный сценарий в окно сеанса интерфейса командной строки и нажмите клавишу `Enter`.

    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. После выполнения сценария просмотрите сведения о пиринге виртуальной сети Resource Manager. Скопируйте следующую команду, вставьте ее в окно сеанса интерфейса командной строки и нажмите клавишу `Enter`.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    В выходных данных в столбце **PeeringState** (Состояние пиринга) указано состояние **Connected** (Подключен). 

    Теперь все ресурсы Azure, созданные в любой из виртуальных сетей, могут взаимодействовать друг с другом, используя свои IP-адреса. Если вы используете разрешение имен Azure по умолчанию для виртуальных сетей, то ресурсы в этих виртуальных сетях не смогут разрешать имена между виртуальными сетями. Если требуется разрешение имен между виртуальными сетями в пиринге, необходимо создать собственный DNS-сервер. Узнайте, как настроить [разрешение имен с помощью собственного DNS-сервера](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Необязательно**. Хотя в этом руководстве не рассматривается создание виртуальных машин, можно создать по виртуальной машине в каждой виртуальной сети и подключить их между собой, чтобы проверить связь.
9. **Необязательно**. Чтобы удалить ресурсы, созданные в этом руководстве, выполните инструкции, описанные в разделе [Удаление ресурсов](#delete-cli) этой статьи.

## <a name="powershell"></a>Создание пиринга с помощью PowerShell

1. Установите последние версии модулей PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) и [AzureRm](https://www.powershellgallery.com/packages/AzureRM/). Если вы еще не работали с Azure PowerShell, ознакомьтесь со статьей [Overview of Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) (Общие сведения об Azure PowerShell).
2. Запустите сеанс PowerShell.
3. В PowerShell войдите в Azure, введя команду `Add-AzureAccount`.
4. Чтобы создать классическую виртуальную сеть с помощью PowerShell, необходимо создать новый или изменить существующий файл конфигурации сети. Узнайте, как [экспортировать, обновлять и импортировать файлы конфигурации сети](virtual-networks-using-network-configuration-file.md). Файл должен содержать приведенный ниже элемент **VirtualNetworkSite** для виртуальной сети, используемой в этом руководстве.

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
    > Импорт измененного файла конфигурации сети может привести к изменениям в классических виртуальных сетях в вашей подписке. Убедитесь, что вы добавили только указанную выше виртуальную сеть и не изменили или удалили имеющиеся в своей подписке виртуальные сети. 
5. Войдите в Azure для создания виртуальной сети Resource Manager, введя команду `login-azurermaccount`. У учетной записи, используемой для входа, должны быть необходимые разрешения для создания пиринга виртуальных сетей. Дополнительные сведения см. в разделе [Разрешения](#permissions) этой статьи.
6. Создайте группу ресурсов и виртуальную сеть Resource Manager. Скопируйте сценарий, вставьте его в окно сеанса PowerShell и нажмите клавишу `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create the virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Создайте пиринг между двумя виртуальными сетями, созданными с помощью разных моделей развертывания. Скопируйте следующий сценарий в текстовый редактор на своем компьютере. Замените `<subscription id>` идентификатором своей подписки. Если вам неизвестен идентификатор подписки, введите команду `Get-AzureRmSubscription`, чтобы просмотреть его. Значение **Id** (Идентификатор) в полученных выходных данных является идентификатором вашей подписки. Чтобы выполнить сценарий, скопируйте измененный сценарий из текстового редактора, затем щелкните правой кнопкой мыши в окне сеанса PowerShell и нажмите клавишу `Enter`.

    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. После выполнения сценария просмотрите сведения о пиринге виртуальной сети Resource Manager. Скопируйте следующую команду, вставьте ее в окно сеанса PowerShell и нажмите клавишу `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    В выходных данных в столбце **PeeringState** (Состояние пиринга) указано состояние **Connected** (Подключен).

    Теперь все ресурсы Azure, созданные в любой из виртуальных сетей, могут взаимодействовать друг с другом, используя свои IP-адреса. Если вы используете разрешение имен Azure по умолчанию для виртуальных сетей, то ресурсы в этих виртуальных сетях не смогут разрешать имена между виртуальными сетями. Если требуется разрешение имен между виртуальными сетями в пиринге, необходимо создать собственный DNS-сервер. Узнайте, как настроить [разрешение имен с помощью собственного DNS-сервера](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Необязательно**. Хотя в этом руководстве не рассматривается создание виртуальных машин, можно создать по виртуальной машине в каждой виртуальной сети и подключить их между собой, чтобы проверить связь.
10. **Необязательно**. Чтобы удалить ресурсы, созданные в этом руководстве, выполните инструкции, описанные в разделе [Удаление ресурсов](#delete-powershell) этой статьи.
 
## <a name="permissions"></a>Разрешения

У учетных записей, используемых для создания пиринга виртуальных сетей, должна быть необходимая роль или разрешения. Например, при создании пиринга между двумя виртуальными сетями myVnet1 и myVnet2 вашей учетной записи должны быть назначены следующие минимальные роли или разрешения для каждой виртуальной сети.
    
|Виртуальная сеть|Модель развертывания|Роль|Разрешения|
|---|---|---|---|
|myVnet1|Диспетчер ресурсов|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Классический|[Участник классической сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Недоступно|
|myVnet2|Диспетчер ресурсов|[Участник сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Классический|[Участник классической сети](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Узнайте больше о [встроенных ролях](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) и назначении разрешений, определенных для [настраиваемых ролей](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (только для Resource Manager).

## <a name="delete"></a>Удаление ресурсов
По завершении работы с этим руководством может потребоваться удалить созданные в его рамках ресурсы, чтобы за их использование не взималась плата. При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.

### <a name="delete-portal"></a>Портал Azure

1. В поле поиска на портале введите **myResourceGroup**. В результатах поиска щелкните **myResourceGroup**.
2. В колонке **myResourceGroup** щелкните значок **Удалить**.
3. Чтобы подтвердить удаление, введите **myResourceGroup** в поле **Введите имя группы ресурсов**, а затем щелкните **Удалить**.

### <a name="delete-cli"></a>Интерфейс командной строки Azure

1. Используйте Azure CLI 2.0, чтобы удалить виртуальную сеть Resource Manager с помощью приведенной ниже команды.

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Используйте Azure CLI 1.0, чтобы удалить классическую виртуальную сеть с помощью приведенных ниже команд.

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Введите приведенную ниже команду, чтобы удалить виртуальную сеть Resource Manager.

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. Чтобы удалить классическую виртуальную сеть с помощью PowerShell, необходимо изменить существующий файл конфигурации сети. Узнайте, как [экспортировать, обновлять и импортировать файлы конфигурации сети](virtual-networks-using-network-configuration-file.md). Удалите приведенный ниже элемент VirtualNetworkSite для виртуальной сети, используемой в этом руководстве.

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
    > Импорт измененного файла конфигурации сети может привести к изменениям в классических виртуальных сетях в вашей подписке. Убедитесь, что вы удалили только указанную выше виртуальную сеть и не изменили или удалили другие виртуальные сети в своей подписке. 

## <a name="register"></a>Регистрация для предварительной версии пиринга между виртуальными сетями в разных регионах

Возможность установки пиринга между виртуальными сетями в разных регионах сейчас находится в предварительной версии. Эта возможность доступна в ограниченном ряде регионов (изначально в центрально-западной части США, центральной Канаде и западной части США 2). Пиринг между виртуальными сетями в разных регионах может не предоставлять тот же уровень доступности и надежности, что и пиринг между виртуальными сетями в одном регионе. Актуальные сведения о доступности и состоянии этой функции см. на странице [обновлений виртуальной сети Azure](https://azure.microsoft.com/updates/?product=virtual-network).

Чтобы создать пиринг между виртуальными сетями в разных регионах, сначала нужно зарегистрироваться для использования предварительной версии, выполнив приведенные ниже действия (в рамках подписки каждой виртуальной сети, для которой требуется пиринг), используя Azure PowerShell или Azure CLI.

### <a name="powershell"></a>PowerShell

1. Установите последнюю версию модуля [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) PowerShell. Если вы еще не работали с Azure PowerShell, ознакомьтесь со статьей [Overview of Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) (Общие сведения об Azure PowerShell).
2. Запустите сеанс PowerShell и войдите в Azure с помощью команды `Login-AzureRmAccount`.
3. Зарегистрируйте подписку, в которой находится каждая виртуальная сеть, для которой нужно создать пиринг, чтобы использовать предварительную версию, введя следующие команды:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowGlobalVnetPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
4. Убедитесь, что регистрация прошла успешно, выполнив следующую команду:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowGlobalVnetPeering `
      -ProviderNamespace Microsoft.Network
    ```

    Не выполняйте инструкции в разделах для портала, PowerShell, Azure CLI или шаблона Resource Manager в этой статье, пока значение **RegistrationState** (Состояние регистрации) в выходных данных приведенной выше команды не станет **Registered** (Зарегистрировано) для обеих подписок.

### <a name="azure-cli"></a>Инфраструктура CLI Azure

1. [Установить и настроить Azure CLI](/cli/azure/install-azure-cli?toc=%2Fazure%2Fvirtual-network%2Ftoc.json).
2. Убедитесь, вы используете Azure CLI версии 2.0.18 или более поздней, введя команду `az --version`. Если это не так, установите последнюю версию.
3. Войдите в Azure с помощью команды `az login`.
4. Зарегистрируйтесь для использования предварительной версии, выполнив следующие команды:

    ```azurecli-interactive
    az feature register --name AllowGlobalVnetPeering --namespace Microsoft.Network
    az provider register --name Microsoft.Network
    ```

5. Убедитесь, что регистрация прошла успешно, выполнив следующую команду:

    ```azurecli-interactive
    az feature show --name AllowGlobalVnetPeering --namespace Microsoft.Network
    ```

    Не выполняйте инструкции в разделах для портала, PowerShell, Azure CLI или шаблона Resource Manager в этой статье, пока значение **RegistrationState** (Состояние регистрации) в выходных данных приведенной выше команды не станет **Registered** (Зарегистрировано) для обеих подписок.

## <a name="next-steps"></a>Дальнейшие действия

- Внимательно ознакомьтесь с важными [ограничениями и особенностями работы пиринга виртуальных сетей](virtual-network-manage-peering.md#requirements-and-constraints), прежде чем создавать пиринг виртуальных сетей для рабочей среды.
- Узнайте о [параметрах пиринга виртуальных сетей](virtual-network-manage-peering.md#create-a-peering).
- Узнайте, как [создать звездообразную топологию сети](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) с помощью пиринга виртуальных сетей.
