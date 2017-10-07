---
title: "Виртуальная сеть Azure с несколькими подсетями aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной сети с несколькими подсетями в Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Создание виртуальной сети с несколькими подсетями

В этом учебнике показано, как toocreate основные виртуальной сети Azure с разделения открытых и закрытых подсетей. В подсетях можно создавать различные ресурсы Azure, например виртуальные машины, среды службы приложений Azure, масштабируемые наборы виртуальных машин, Azure HDInsight и облачные службы. Ресурсы в виртуальные сети могут взаимодействовать друг с другом и с ресурсами в других сетях подключенных tooa виртуальной сети.

Hello следующие разделы содержат действия, которые можно предпринять toocreate виртуальной сети с помощью hello [портал Azure](#portal), hello Azure интерфейс командной строки ([Azure CLI](#azure-cli)), [Azure PowerShell ](#powershell)и [шаблона Azure Resource Manager](#resource-manager-template). результат Hello — hello же, независимо от того, какие средства используется виртуальная сеть toocreate hello. Щелкните ссылку средство toogo toothat раздел учебника hello. Дополнительные сведения обо всех параметрах виртуальной сети и подсети см. в [этой](virtual-network-manage-network.md) и [этой](virtual-network-manage-subnet.md) статье.

Эта статья содержит действия toocreate виртуальной сети с помощью модели развертывания диспетчера ресурсов hello, которая используется модель развертывания hello, рекомендуется использовать при создании новых виртуальных сетей. При необходимости toocreate виртуальной сети (классические). в разделе [Создание виртуальной сети (классические)](create-virtual-network-classic.md). Если вы не знакомы с моделями развертывания Azure, см. статью [Развертывание с помощью Azure Resource Manager и классическое развертывание: сведения о моделях развертывания и состоянии ресурсов](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Портал Azure

1. В веб-браузере перейдите toohello [портал Azure](https://portal.azure.com). Войдите с использованием [учетной записи Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи Azure, вы можете зарегистрироваться и получить [бесплатную пробную версию](https://azure.microsoft.com/offers/ms-azr-0044p).
2. На портале hello щелкните **+ создать** > **сети** > **виртуальная сеть**.
3. На hello **Создание виртуальной сети** колонки, введите следующие значения hello и нажмите кнопку **создать**:

    |Настройка|Значение|
    |---|---|
    |Имя|myVnet|
    |Пространство адресов|10.0.0.0/16|
    |Имя подсети|Общедоступные|
    |Диапазон адресов подсети|10.0.0.0/24|
    |Группа ресурсов|Оставьте выбранным пункт **Создать**, а затем введите **MyResourceGroup**.|
    |Подписка и расположение|Выберите подписку и расположение.

    Если вы новый tooAzure, Дополнительные сведения о [групп ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [подписки](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), и [расположения](https://azure.microsoft.com/regions) (также называется tooas *областей*).
4. На портале hello при создании виртуальной сети можно создать только одну подсеть. В этом учебнике создается второй подсети после создания виртуальной сети hello. Позже может создать ресурсы, доступном через Интернет в hello **открытый** подсети. Можно также создать ресурсы, которые недоступны из hello Интернета в hello **закрытый** подсети. toocreate hello вторую подсеть, в hello **Найдите ресурсы** поле вверху hello страницы приветствия, введите **myVnet**. В результатах поиска hello, нажмите кнопку **myVnet**. При наличии нескольких виртуальных сетей с Здравствуйте таким же именем в подписке, проверьте hello групп ресурсов, которые отображаются в каждой виртуальной сети. Нажимайте hello **myVnet** поиска результат, который содержит группу ресурсов hello **myResourceGroup**.
5. На hello **myVnet** колонки в разделе **параметры**, нажмите кнопку **подсети**.
6. На hello **myVnet - подсети** колонка, щелкните **+ подсети**.
7. На hello **добавить подсеть** колонке для **имя**, введите **частного**. Для **Диапазон адресов** введите **10.0.1.0/24**.  Нажмите кнопку **ОК**.
8. На hello **myVnet - подсети** колонки, просмотрите hello подсетей. Вы увидите hello **открытый** и **закрытый** подсети, которые были созданы.
9. **Необязательно:** ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-portal) в этой статье.

## <a name="azure-cli"></a>Инфраструктура CLI Azure

Azure CLI команды представляют собой hello одинакового ли выполнение команды hello из Windows, Linux или macOS. Тем не менее существуют различия в сценариях между оболочками операционных систем. в оболочке Bash выполняет скрипт Hello в hello следующие шаги. 

1. [Установка и настройка hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что имеется hello самую последнюю версию hello Azure CLI установлен. Введите tooget справочные сведения о командах CLI, `az <command> --help`. Вместо установки hello CLI и его необходимых компонентов можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Hello оболочки облако имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. hello toouse оболочки облака щелкните hello оболочки облака (**> _**) кнопку вверху hello hello [портала](https://portal.azure.com) или просто щелкнуть hello *опробовать* кнопку в hello, описанных ниже. 
2. Локальное выполнение hello CLI, зарегистрируйтесь в системе tooAzure с hello `az login` команды. При использовании hello оболочки в облаке, вы выполнили вход.
3. Просмотрите hello следующий сценарий и его комментариями. В браузере скопировать hello скрипт и вставьте его в сеанс CLI:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. После завершения скрипта hello работает, просмотрите hello подсетей для виртуальной сети hello. Скопируйте следующую команду hello и вставьте его в сеанс CLI:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-cli) в этой статье.

## <a name="powershell"></a>PowerShell

1. Установите последнюю версию hello hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. В сеансе PowerShell войдите в tooAzure с вашей [учетная запись Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) с помощью hello `login-azurermaccount` команды.

3. Просмотрите hello следующий сценарий и его комментариями. В браузере скопируйте скрипт hello и вставьте его в сеансе PowerShell:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. tooreview hello подсетей для виртуальной сети hello, скопируйте hello следующую команду и вставьте его в сеансе PowerShell:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Необязательный**: ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в [удаление ресурсов](#delete-powershell) в этой статье.

## <a name="resource-manager-template"></a>Шаблон Resource Manager

Вы можете развернуть виртуальную сеть с помощью шаблона Azure Resource Manager. toolearn Дополнительные сведения о шаблонах, в разделе [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). шаблон tooaccess hello и toolearn о его параметрах см. раздел hello [создайте виртуальную сеть с двумя подсетями](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) шаблона. Шаблон hello можно развернуть с помощью hello [портала](#template-portal), [Azure CLI](#template-cli), или [PowerShell](#template-powershell).

**Необязательно:** ресурсов hello toodelete, созданных в этом учебнике, hello завершения шагов в любой подразделов [удаление ресурсов](#delete) в этой статье.

### <a name="template-portal"></a>Портал Azure

1. Откройте в браузере, hello [страницы шаблона](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Нажмите кнопку hello **развертывание tooAzure** кнопки. Если вы еще не вошли в tooAzure, войдите в систему на появившемся экране входа Azure портала hello.
3. Войдите в портал toohello с использованием вашей [учетная запись Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Если у вас нет учетной записи Azure, вы можете зарегистрироваться и получить [бесплатную пробную версию](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Введите следующие значения для параметров hello hello:

    |Параметр|Значение|
    |---|---|
    |Подписки|Выберите свою подписку.|
    |Группа ресурсов|myResourceGroup|
    |Расположение|Выберите расположение|
    |Имя виртуальной сети|myVnet|
    |Префикс адреса виртуальной сети|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Общедоступные|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Private|

5. Принимаю условия toohello и нажмите кнопку **покупки** toodeploy hello виртуальной сети.

### <a name="template-cli"></a>Интерфейс командной строки Azure

1. [Установка и настройка hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что имеется hello самую последнюю версию hello Azure CLI установлен. Введите tooget справочные сведения о командах CLI, `az <command> --help`. Вместо установки hello CLI и его необходимых компонентов можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Hello оболочки облако имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. hello toouse оболочки облака щелкните hello оболочки облака **> _** кнопку вверху hello hello [портала](https://portal.azure.com), или просто щелкнуть hello **опробовать** кнопку в hello, описанных ниже. 
2. Локальное выполнение hello CLI, зарегистрируйтесь в системе tooAzure с hello `az login` команды. При использовании hello оболочки в облаке, вы выполнили вход.
3. toocreate группу ресурсов для виртуальной сети hello копирования hello следующую команду и вставьте его в ваш сеанс CLI:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Шаблон hello можно развернуть с помощью одного из hello следующие варианты параметров:
    - **Значений параметров по умолчанию.** Введите следующую команду hello:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Настраиваемых значений параметров.** Загрузка и изменение шаблона hello перед развертыванием hello шаблона. Также можно развернуть шаблон hello с помощью параметров командной строки hello, или развернуть шаблон hello с файлом отдельные параметры. файлы шаблона и параметров hello toodownload, щелкните hello **просмотр на GitHub** кнопку на hello [создайте виртуальную сеть с двумя подсетями](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) страницы шаблона. В GitHub щелкните hello **azuredeploy.parameters.json** или **azuredeploy.json** файла. Нажмите кнопку hello **Raw** файл hello toodisplay кнопки. В браузере скопируйте содержимое файла hello hello. Сохраните файл tooa hello содержимое на компьютере. Можно изменить значения параметров hello в шаблоне hello или развернуть шаблон hello с файлом отдельные параметры.  

    Дополнительные сведения о toolearn как тип toodeploy шаблоны с помощью этих методов `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Установите последнюю версию hello hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) модуля. Если у вас отсутствует новый tooAzure PowerShell, [Обзор Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. В сеансе PowerShell toosign с вашей [учетная запись Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), введите `login-azurermaccount`.
3. toocreate группу ресурсов для виртуальной сети hello, введите следующую команду hello:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Шаблон hello можно развернуть с помощью одного из hello следующие варианты параметров:
    - **Значений параметров по умолчанию.** Введите следующую команду hello:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Настраиваемых значений параметров.** Загрузка и изменение шаблона hello перед ее развертыванием. Также можно развернуть шаблон hello с помощью параметров командной строки hello, или развернуть шаблон hello с файлом отдельные параметры. файлы шаблона и параметров hello toodownload, щелкните hello **просмотр на GitHub** кнопку на hello [создайте виртуальную сеть с двумя подсетями](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) страницы шаблона. В GitHub щелкните hello **azuredeploy.parameters.json** или **azuredeploy.json** файла. Нажмите кнопку hello **Raw** файл hello toodisplay кнопки. В браузере скопируйте содержимое файла hello hello. Сохраните файл tooa hello содержимое на компьютере. Можно изменить значения параметров hello в шаблоне hello или развернуть шаблон hello с файлом отдельные параметры.  

    Дополнительные сведения о toolearn как тип toodeploy шаблоны с помощью этих методов `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Удаление ресурсов

После завершения этого учебника, чтобы не будет взиматься плата за использование может потребоваться toodelete hello ресурсы, которые были созданы. При удалении группы ресурсов также удаляются все ресурсы, которые находятся в группе ресурсов hello.

### <a name="delete-portal"></a>Портал Azure

1. Введите в поле поиска портала hello, **myResourceGroup**. В результатах поиска hello, нажмите кнопку **myResourceGroup**.
2. На hello **myResourceGroup** колонка, щелкните hello **удалить** значок.
3. Удаление hello tooconfirm, в hello **ТИПА hello имя группы РЕСУРСОВ** введите **myResourceGroup**и нажмите кнопку **удалить**.

### <a name="delete-cli"></a>Интерфейс командной строки Azure

В сеансе CLI введите hello следующую команду:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

В сеансе PowerShell введите следующую команду hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Дальнейшие действия

- toolearn о все параметры виртуальной сети и подсети, в разделе [управлять виртуальными сетями](virtual-network-manage-network.md#view-vnet) и [управление подсети виртуальной сети](virtual-network-manage-subnet.md#create-subnet). Имеются различные варианты использования виртуальных сетей и подсетей в рабочей среде toomeet различные требования к среде.
- toofilter входящего и исходящего трафика подсети, создание и применение [сетевых групп безопасности](virtual-networks-nsg.md) toosubnets.
- Создание [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) виртуальной машины и подключите его tooan существующей виртуальной сети.
- tooconnect двух виртуальных сетей в hello же расположению Azure, создание [виртуальную сеть пиринга](virtual-network-peering-overview.md) между виртуальными сетями hello.
- Подключения hello виртуальной сети tooan в локальной сети с помощью [VPN-шлюз](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) канала.
