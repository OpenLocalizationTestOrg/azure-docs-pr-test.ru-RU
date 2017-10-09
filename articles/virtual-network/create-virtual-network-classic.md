---
title: "aaaCreate виртуальной сети Azure (классические) с несколькими подсетями | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети (классической) с несколькими подсетями в Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Создание (классической) виртуальной сети с несколькими подсетями

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует создать большинство новые виртуальные сети через hello [диспетчера ресурсов](virtual-networks-create-vnet-arm-pportal.md) модели развертывания.

В этом учебнике показано, как toocreate основные виртуальной сети Azure (классические), имеющий разделения открытых и закрытых подсетей. Ресурсы Azure, такие как виртуальные машины и облачные службы, можно создавать в подсети. Ресурсы, созданные в виртуальных сетях (классические) могут взаимодействовать друг с другом и с ресурсами в других сетях подключенных tooa виртуальной сети.

Дополнительные сведения обо всех параметрах виртуальной сети и подсети см. в [этой](virtual-network-manage-network.md) и [этой](virtual-network-manage-subnet.md) статье.

> [!WARNING]
> При [отключении подписки](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit) классические виртуальные сети сразу же удаляются Azure Виртуальные сети (классической) удаляются независимо от того, существуют ли ресурсов в виртуальной сети hello. Если после повторного включения подписки hello, необходимо повторно создать ресурсы, которые существовали в виртуальной сети hello.

Можно создать виртуальную сеть (классические) с помощью hello [портал Azure](#portal), hello [Azure командной строки (CLI) 1.0](#azure-cli), или [PowerShell](#powershell).

## <a name="portal"></a>Microsoft Azure

1. В веб-браузере перейдите toohello [портал Azure](https://portal.azure.com). Войдите с использованием [учетной записи Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи Azure, вы можете зарегистрироваться и получить [бесплатную пробную версию](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Нажмите кнопку **+ создать** hello портала.
3. Введите *виртуальная сеть* в hello **поиска hello Marketplace** поле вверху hello hello **New** колонки, отображается.  Нажмите кнопку **виртуальная сеть** когда он появится в результатах поиска hello.
4. Выберите **классический** в hello **выберите модель развертывания** поле в hello **виртуальной сети** колонки, отображается, нажмите кнопку **создать**. 
5. Введите следующие значения на hello hello **Создание виртуальной сети (классические)** колонку и нажмите кнопку **создать**:

    |Настройка|Значение|
    |---|---|
    |Имя|myVnet|
    |Пространство адресов|10.0.0.0/16|
    |Имя подсети|Общедоступные|
    |Диапазон адресов подсети|10.0.0.0/24|
    |Группа ресурсов|Оставьте выбранным пункт **Создать**, а затем введите **MyResourceGroup**.|
    |Подписка и расположение|Выберите подписку и расположение.

    Если вы новый tooAzure, Дополнительные сведения о [групп ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [подписки](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), и [расположения](https://azure.microsoft.com/regions) (также называется tooas *областей*).
4. На портале hello при создании виртуальной сети можно создать только одну подсеть. В этом учебнике создается второй подсети после создания виртуальной сети hello. Позже может создать ресурсы, доступном через Интернет в hello **открытый** подсети. Можно также создать ресурсы, которые недоступны из hello Интернета в hello **закрытый** подсети. toocreate Здравствуйте вторую подсеть, введите **myVnet** в hello **Найдите ресурсы** поле вверху hello страницы приветствия. Нажмите кнопку **myVnet** когда он появится в результатах поиска hello.
5. Нажмите кнопку **подсети** (в hello **параметры** раздела) на hello **Создание виртуальной сети (классические)** колонки, отображается.
6. Нажмите кнопку **+ добавить** на hello **myVnet - подсети** колонки, отображается.
7. Введите **закрытый** для **имя** на hello **добавить подсеть** колонку. Для **Диапазон адресов** введите **10.0.1.0/24**.  Нажмите кнопку **ОК**.
8. На hello **myVnet - подсети** колонку, вы увидите hello **открытый** и **закрытый** подсети, которые были созданы.
9. **Необязательный**: после завершения этого учебника, может потребоваться toodelete hello ресурсы, которые были созданы, чтобы не будет взиматься плата за использование:
    - Нажмите кнопку **Обзор** на hello **myVnet** колонку.
    - Нажмите кнопку hello **удаление** значок hello **myVnet** колонку.
    - tooconfirm hello удаления, нажмите кнопку **Да** в hello **удаления виртуальной сети** поле.

## <a name="azure-cli"></a>Инфраструктура CLI Azure

1. Вы можете либо [Установка и настройка hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), или использовать hello CLI в hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. Введите tooget справочные сведения о командах CLI, `azure <command> --help`. 
2. В сеансе CLI вход tooAzure командой hello ниже. Если щелкнуть **опробовать** hello флажок ниже, открывается оболочки облака. Вы можете войти tooyour подписки Azure, не вводя hello следующую команду:

    ```azurecli-interactive
    azure login
    ```

3. hello tooensure CLI находится в режиме управления службой, введите следующую команду hello:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Создайте виртуальную сеть с частной подсетью:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Создание общей подсети в виртуальной сети hello:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Просмотрите hello виртуальную сеть и подсети.

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Необязательный**: toodelete hello ресурсы, созданные после завершения этого учебника, чтобы не будет взиматься плата за использование может потребоваться:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Хотя нельзя указать toocreate группы ресурсов виртуальной сети (классической) с помощью hello CLI, Azure создает виртуальную сеть hello в группе ресурсов с именем *сети по умолчанию*.

## <a name="powershell"></a>PowerShell

1. Установите последнюю версию hello hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) модуля. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Запустите сеанс PowerShell.
3. В PowerShell, войдите в tooAzure, указав hello `Add-AzureAccount` команды.
4. Изменить hello следующий путь и имя файла, при необходимости экспортировать существующий файл конфигурации сети:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate виртуальная сеть с общедоступных и частных подсетях, используйте любой текстовый редактор tooadd hello **VirtualNetworkSite** элемента, следующего toohello файла конфигурации сети.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Просмотрите hello полного [схема файла конфигурации сети](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Импорт файла конфигурации сети hello:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Импорт файла конфигурации сети измененные может привести к изменения tooexisting виртуальные сети (классической) для вашей подписки. Убедитесь в добавлении hello предыдущих виртуальной сети и не изменить или удалить все существующие виртуальные сети из подписки. 

7. Просмотрите hello виртуальную сеть и подсети.

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Необязательный**: может потребоваться toodelete hello ресурсы, созданные после завершения этого учебника, чтобы не будет взиматься плата за использование. toodelete hello виртуальной сети, полный шаги 4 – 6, это время удаления hello **VirtualNetworkSite** элемент, добавленный на шаге 5.
 
> [!NOTE]
> Хотя нельзя указать toocreate группы ресурсов виртуальной сети (классической) с помощью PowerShell, Azure создает виртуальную сеть hello в группе ресурсов с именем *сети по умолчанию*.

---

## <a name="next-steps"></a>Дальнейшие действия

- toolearn о все параметры виртуальной сети и подсети, в разделе [управлять виртуальными сетями](virtual-network-manage-network.md) и [управление подсети виртуальной сети](virtual-network-manage-subnet.md). Имеются различные варианты использования виртуальных сетей и подсетей в рабочей среде toomeet различные требования к среде.
- toofilter входящего и исходящего трафика подсети, создание и применение [сетевых групп безопасности](virtual-networks-nsg.md) toosubnets.
- Создание [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) виртуальной машины и подключите его tooan существующей виртуальной сети.
- tooconnect двух виртуальных сетей в hello же расположению Azure, создание [виртуальную сеть пиринга](create-peering-different-deployment-models.md) между виртуальными сетями hello. Можно установить равноправное подключение к виртуальной сети (диспетчера ресурсов) tooa виртуальной сети (классические), но не удается создать пиринг между двумя виртуальными сетями (классические).
- Подключения hello виртуальной сети tooan в локальной сети с помощью [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) канала.
