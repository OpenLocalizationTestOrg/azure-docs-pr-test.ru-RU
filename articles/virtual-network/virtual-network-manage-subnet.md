---
title: "aaaAdd, изменить или удалить подсеть виртуальной сети Azure | Документы Microsoft"
description: "Узнайте, как tooadd, изменить или удалить подсеть виртуальной сети в Azure."
services: virtual-network
documentationcenter: na
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
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Создание, изменение или удаление виртуальной сети

Узнайте, как tooadd, изменить или удалить подсеть виртуальной сети. 

Если вы не работали с виртуальными сетями, прежде чем создавать, изменять и удалять подсеть, мы рекомендуем прочитать [обзор виртуальных сетей Azure ](virtual-networks-overview.md), а также статью [Создание, изменение и удаление виртуальной сети](virtual-network-manage-network.md). Все ресурсы Azure, развернутые в виртуальной сети, также развертываются в подсети виртуальной сети. Как правило, в виртуальной сети создается несколько подсетей для решения следующих задач.
- **Фильтрация трафика между подсетями**. Можно применить toosubnets группы безопасности сети toofilter, входящий и исходящий сетевой трафик для всех ресурсов (например, виртуальные машины), которые находятся в виртуальной сети hello. Дополнительные сведения о toolearn toocreate группу безопасности сети в статье [создавать группы безопасности сети](virtual-networks-create-nsg-arm-pportal.md).
- **Управление маршрутизацией между подсетями**. Azure создает маршруты по умолчанию, чтобы трафик автоматически направлялся между подсетями. Вы можете переопределить стандартные маршруты Azure, создав определяемые пользователем маршруты. в разделе toolearn Дополнительные сведения об определяемых пользователем маршрутов, [создания определяемых пользователем маршрутов](virtual-network-create-udr-arm-ps.md). 

В этой статье объясняется, как tooadd, изменить и удалить подсеть для виртуальных сетей, которые были созданы с помощью модели развертывания диспетчера ресурсов Azure hello.
 
## <a name="before"></a>Перед началом работы

Перед началом hello задачи, описанные в этой статье, выполните hello следующие предварительные требования:

- Если вы новый tooworking с виртуальными сетями, рекомендуется изучить упражнения hello в [создания первой виртуальной сети Azure](virtual-network-get-started-vnet-subnet.md). Это руководство поможет вам ознакомиться с принципами работы виртуальных сетей.
- toolearn об ограничениях для виртуальных сетей, проверки [ограничения Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Войдите в портал Azure toohello, hello средство командной строки Azure (Azure CLI) или Azure PowerShell с помощью учетной записи Azure. Если у вас нет учетной записи Azure, зарегистрируйтесь, чтобы получить [бесплатную пробную учетную запись](https://azure.microsoft.com/free).
- Если планируется toouse команды PowerShell toocomplete hello задач, описанных в этой статье, необходимо сначала [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Обеспечьте hello самую последнюю версию hello установлены командлеты Azure PowerShell. Введите tooget справки по командам PowerShell в примерах hello `get-help <command> -full`.
- Если планируется toouse Azure CLI команды toocomplete hello задач, описанных в этой статье, необходимо:
    - [Установка и настройка hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что hello самую последнюю версию Azure CLI установлен.
    - Используйте hello оболочки облако Azure. Вместо установки hello CLI и его зависимости, можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. hello toouse оболочки облака щелкните hello оболочки облака (**> _**) вверху hello hello портал Azure значок. 

  Введите tooget справки с помощью команд Azure CLI `az <command> --help`.

## <a name="create-subnet"></a>Создание подсети

tooadd подсети:

1. Войдите в toohello [портала](https://portal.azure.com) с помощью учетной записи назначены разрешения для роли участника сети hello (как минимум) для вашей подписки. . в разделе toolearn Дополнительные сведения о назначении ролей и разрешений tooaccounts, [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Введите в поле поиска портала hello, **виртуальных сетей**. В результатах поиска hello, нажмите кнопку **виртуальные сети**.
3. На hello **виртуальные сети** колонка, щелкните требуется tooadd подсети в виртуальной сети hello.
4. В колонке hello виртуальной сети, нажмите кнопку **подсети**.
5. Щелкните **Добавить подсеть**.
6. На hello **добавить подсеть** колонки, введите значения для hello следующие параметры:
    - **Имя**: hello имя должно быть уникальным в пределах виртуальной сети hello.
    - **Диапазон адресов**: hello диапазон должен быть уникальным в пределах hello адресное пространство виртуальной сети hello. Hello диапазон не может перекрываться с другими диапазонами адресов подсети в виртуальной сети hello. адресное пространство Hello указывается с помощью нотации бесклассовой междоменной маршрутизации (CIDR). Например, в виртуальной сети с адресным пространством 10.0.0.0/16 можно определить адресное пространство подсети 10.0.0.0/24. Hello минимальный диапазон, который можно указать — / 29, который предоставляет восемь IP-адреса для подсети hello. Azure резервирует сначала hello и последнего адрес в каждой подсети для соответствия протоколу. Еще три адреса резервируются для служб Azure. В результате определения подсети с/29 адрес диапазона результаты в трех пригодных IP-адресов в подсети hello. Если планируется tooconnect tooa VPN-шлюза виртуальной сети, необходимо создать подсеть шлюза. Узнайте больше о [рекомендациях по диапазонам адресов для подсетей шлюза](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Можно изменить диапазон адресов hello после добавления hello подсети, при определенных условиях. toochange диапазон адресов подсети. в статье toolearn [подсети в настройках](#change-subnet) в этой статье.
    - **Сетевая группа безопасности**: при необходимости можно связать существующую группу безопасности сети с toocontrol подсети hello входящий и исходящий сетевой трафик, фильтрации для подсети hello. Hello сетевая группа безопасности должна существовать в hello же подписке и расположении, что виртуальная сеть hello. Он также должен создаваться с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn toocreate группу безопасности сети в статье [сетевых групп безопасности](virtual-networks-create-nsg-arm-pportal.md).
    - **Таблица маршрутов**: при необходимости можно связать существующую таблицу маршрутов с hello подсети toocontrol сетевого трафика маршрутизации tooother сетей. Hello маршрута таблица должна существовать в hello же подписке и расположении, что виртуальная сеть hello. Он также должен создаваться с помощью модели развертывания диспетчера ресурсов hello. Дополнительные сведения о toolearn toocreate таблиц маршрутов, в статье [определяемых пользователем маршрутов](virtual-network-create-udr-arm-ps.md).
    - **Пользователи**: подсети toohello доступа можно управлять с помощью встроенных ролей или собственные настраиваемые роли. toolearn Дополнительные сведения о назначении ролей и пользователей подсети tooaccess hello, в разделе [использовать роли назначения toomanage доступа tooyour Azure ресурсов](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. Щелкните tooadd hello подсети toohello виртуальную сеть, которую вы выбрали, **ОК**.

**Команды**

|Средство|Команда|
|---|---|
|Инфраструктура CLI Azure|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Изменение параметров подсети

Можно изменить сетевые группы безопасности, таблицы маршрутов и подсети tooa доступа пользователей, управление ресурсами, которые находятся в подсети. toolearn об этих параметрах в [добавить подсеть](#create-subnet), см. шаг 6. Если требуется toochange hello адресное пространство подсети, необходимо сначала удалить все ресурсы, которые находятся в подсети hello. шаги Hello занять toodelete ресурс зависит от ресурса hello. как toodelete ресурсы, которые находятся в подсетях, чтения hello документацию для каждого ресурса, тип, которые должны toodelete toolearn. toochange hello диапазон адресов для подсети:

1. Войдите в toohello [портала](https://portal.azure.com) с помощью учетной записи назначены разрешения для роли участника сети hello (как минимум) для вашей подписки. . в разделе toolearn Дополнительные сведения о назначении ролей и разрешений tooaccounts, [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Введите в поле поиска портала hello, **виртуальных сетей**. В результатах поиска hello, нажмите кнопку **виртуальные сети**.
3. На hello **виртуальные сети** колонка, щелкните hello виртуальной сети, для которого требуется toochange диапазон адресов подсети.
4. Выберите подсеть hello, для которого требуется диапазон адресов toochange hello.
5. В колонке подсети hello в hello **диапазона адресов** введите новый диапазон адресов hello. Hello диапазон должен быть уникальным в пределах hello адресное пространство виртуальной сети hello. Hello диапазон не может перекрываться с другими диапазонами адресов подсети в виртуальной сети hello. адресное пространство Hello указывается с помощью нотации CIDR. Например, в виртуальной сети с адресным пространством 10.0.0.0/16 можно определить адресное пространство подсети 10.0.0.0/24. Hello минимальный диапазон, который можно указать — / 29, который предоставляет восемь IP-адреса для подсети hello. Azure резервирует сначала hello и последнего адрес в каждой подсети для соответствия протоколу. Еще три адреса резервируются для служб Azure. В результате подсеть с диапазоном адресов /29 содержит только три пригодных для использования IP-адреса. Если планируется tooconnect tooa VPN-шлюза виртуальной сети, необходимо создать подсеть шлюза. Узнайте больше о [рекомендациях по диапазонам адресов для подсетей шлюза](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Диапазон адресов hello можно изменить после создания hello подсети, при определенных условиях. toochange диапазон адресов подсети. в статье toolearn [подсети в настройках](#change-subnet) в этой статье.
6. Щелкните **Сохранить**.

**Команды**

|Средство|Команда|
|---|---|
|Инфраструктура CLI Azure|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Удаление подсети

Подсети можно удалить только в том случае, если нет ресурсов, в подсети hello. Если в подсети hello ресурсов, необходимо удалить hello ресурсы, которые находятся в подсети hello, прежде чем удалять hello подсети. шаги Hello занять toodelete ресурс зависит от ресурса hello. как toodelete ресурсы, которые находятся в подсетях, чтения hello документацию для каждого ресурса, тип, которые должны toodelete toolearn. toodelete подсети:

1. Войдите в toohello [портала](https://portal.azure.com) с помощью учетной записи назначены разрешения для роли участника сети hello (как минимум) для вашей подписки. . в разделе toolearn Дополнительные сведения о назначении ролей и разрешений tooaccounts, [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Введите в поле поиска портала hello, **виртуальных сетей**. В результатах поиска hello, нажмите кнопку **виртуальные сети**.
3. На hello **виртуальные сети** колонка, щелкните требуется toodelete подсети из виртуальной сети hello.
4. На hello виртуального сетевого колонке в группе **параметры**, нажмите кнопку **подсети**.
5. В списке hello подсетей, появится в колонке hello подсетей, щелкните правой кнопкой мыши hello подсети должны toodelete, нажмите кнопку **удаление**и нажмите кнопку **Да** toodelete hello подсети.

**Команды**

|Средство|Команда|
|---|---|
|Инфраструктура CLI Azure|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Дальнейшие действия

toocreate виртуальной машины в подсети, в разделе [создать виртуальную сеть и развертывать виртуальные машины в подсети hello](virtual-network-get-started-vnet-subnet.md#create-vms).
