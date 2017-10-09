---
title: "aaaVirtual сетей и виртуальных машинах в Azure | Документы Microsoft"
description: "Дополнительные сведения о сетевых относительно toohello основные принципы создания виртуальных машинах в Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Виртуальные сети и виртуальные машины Windows в Azure 

При создании виртуальной машины Azure вам потребуется [виртуальная сеть](../../virtual-network/virtual-networks-overview.md). Вы можете создать ее или использовать уже готовую. Необходимо также toodecide как виртуальные машины находятся нужные toobe доступе к hello виртуальной сети. Очень важно слишком[плана, прежде чем создавать ресурсы](../../virtual-network/virtual-network-vnet-plan-design-arm.md) и убедитесь, что вы понимаете hello [ограничений на сетевые ресурсы](../../azure-subscription-service-limits.md#networking-limits).

В следующий рисунок hello виртуальные машины, представляются в виде веб-серверов и серверов баз данных. Каждый набор виртуальных машин, назначается tooseparate подсетей в виртуальной сети hello.

![виртуальной сети Azure](./media/network-overview/vnetoverview.png)

До создания виртуальной Машины или hello виртуальной сети можно создать при создании виртуальной Машины можно создать виртуальную сеть. Вы можете создать виртуальную сеть самостоятельно или использовать сеть, которая будет создана при развертывании виртуальной машины.

Виртуальная машина toosupport связи создайте эти ресурсы:

- Сетевые интерфейсы
- IP-адреса;
- Виртуальные сети и подсети

В дополнение к этому toothose основные ресурсы, необходимо учитывать следующие дополнительные ресурсы:

- Группы безопасности сети
- Балансировщики нагрузки 

## <a name="network-interfaces"></a>Сетевые интерфейсы

Объект [сетевого интерфейса (NIC)](../../virtual-network/virtual-network-network-interface.md) — hello взаимосвязь между виртуальной Машины и виртуальной сети (VNet). Виртуальная машина должен иметь по крайней мере один сетевой Адаптер, но может иметь несколько, в зависимости от размера hello hello создания виртуальной Машины. Дополнительные сведения о количестве сетевых интерфейсов, поддерживаемых каждым из размеров виртуальной машины, см. в статье [Размеры виртуальных машин в Azure](sizes.md). 

Если вы хотите toocreate виртуальной Машины с более чем одной сетевой КАРТОЙ, необходимо создать hello виртуальной Машины с по крайней мере два.  После создания можно добавить дополнительные сетевые адаптеры toohello номер поддерживается hello размер виртуальной Машины, но нельзя добавить дополнительные сетевые адаптеры tooa создана только с одной виртуальной Машины, независимо от того, какое количество сетевых поддерживает hello размер виртуальной Машины. 

Если hello виртуальной Машины будет добавлен набор доступности tooan, все виртуальные машины в наборе доступности hello должен иметь один или несколько сетевых адаптеров. Виртуальные машины с более чем одного сетевого Адаптера не требуется toohave hello одинаковое число сетевых адаптеров, но все они должны иметь по крайней мере два.

Каждый tooa сетевого Адаптера, подключенного в виртуальной Машине должна присутствовать hello же местоположение и подписку как hello виртуальной Машины. Каждый сетевой Адаптер должен быть подключенным tooa виртуальную сеть, существует hello же расположение Azure и подписки как hello сетевого адаптера. После создания сетевой КАРТЫ можно изменить hello подсети, в которой он подключен к, но невозможно изменить hello он подключен к виртуальной сети.  Каждый сетевой Адаптер подключен tooa ВМ назначено MAC-адрес, не меняется, пока не будет удалена hello виртуальной Машины.

В этой таблице перечислены hello методы, которые можно использовать toocreate сетевого интерфейса.

| Метод | Описание |
| ------ | ----------- |
| Портал Azure | При создании виртуальной Машины в Azure portal hello сетевого интерфейса автоматически создается (нельзя использовать сетевой Адаптер, создаются отдельно). портал Hello создает виртуальную Машину с только один сетевой адаптер. Если вы хотите toocreate виртуальной Машины с более чем одной сетевой КАРТОЙ, необходимо создать его с другой метод. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Используйте [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) с hello **- PublicIpAddressId** параметр tooprovide hello идентификатор hello общедоступный IP-адрес, созданный ранее. |
| [Интерфейс командной строки Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | Идентификатор hello tooprovide hello общедоступных IP-адрес, который используется ранее созданный [Создание сетевого адаптера сети az](https://docs.microsoft.com/cli/azure/network/nic#create) с hello **--public-ip адрес** параметра. |
| [Шаблон](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Используйте шаблон [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) (Сетевой интерфейс в виртуальной сети с общедоступным IP-адресом) в качестве руководства по развертыванию сетевого интерфейса с помощью шаблона. |

## <a name="ip-addresses"></a>IP-адреса; 

Можно назначить эти типы [IP-адреса](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa сетевой Адаптер в Azure:

- **Общедоступные IP-адреса** -использовать toocommunicate входящих и исходящих подключений (без преобразования сетевых адресов (NAT)) с hello Интернета и другим ресурсам Azure не подключены tooa виртуальной сети. Назначение общих tooa адрес IP сетевого Адаптера является необязательным. За общедоступные IP-адреса взимается номинальная плата. В рамках подписки их использование ограничено.
- **Частные IP-адреса** — служат для обмена данными в пределах виртуальной сети, локальной сети и hello Интернет, (NAT). Необходимо назначить хотя бы один закрытый tooa адрес IP виртуальной Машины. чтение toolearn Дополнительные сведения о NAT в Azure, [основные сведения об исходящих подключений в Azure](../../load-balancer/load-balancer-outbound-connections.md).

Можно назначить открытый tooVMs IP-адреса или подсистемы балансировки нагрузки с выходом в Интернет. Можно назначить закрытый tooVMs IP-адреса и внутренних подсистем балансировки нагрузки. Можно назначить IP адресов tooa виртуальную Машину с помощью сетевого интерфейса.

Существует два метода, в которых выделенный ресурс tooa - динамический или статический IP-адрес. метод распределения по умолчанию Hello является динамическим, где IP-адрес не выделен, при его создании. Вместо этого hello IP-адрес назначается при создании виртуальной Машины или запуске остановленной виртуальной Машины. Hello IP-адрес освобождается, когда останавливать или удалять hello виртуальной Машины. 

hello tooensure hello IP-адрес для hello, ВМ остается таким же, можно задать способ распределения hello явно toostatic. В рамках этого способа IP-адрес назначается немедленно, Оно освобождается только в том случае, когда hello виртуальной Машины удалить или изменить его toodynamic метод распределения.
    
В этой таблице перечислены hello методы, которые можно использовать toocreate IP-адрес.

| Метод | Описание |
| ------ | ----------- |
| [Портал Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | По умолчанию общие IP-адреса являются динамическими и toothem hello адрес, связанный может измениться при hello виртуальная машина остановлена или удалена. использует tooguarantee, всегда hello ВМ hello же общедоступный IP-адрес, создайте статический общедоступный IP-адрес. По умолчанию hello портала назначает динамического частного IP адрес tooa сетевого Адаптера при создании виртуальной Машины. Можно изменить этот toostatic после hello создания виртуальной Машины.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Вы используете [New AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) с hello **- AllocationMethod** параметра, как динамический или статический. |
| [Интерфейс командной строки Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Вы используете [создания сети az public-ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) с hello **--способ распределения** параметра, как динамический или статический. |
| [Шаблон](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Используйте шаблон [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) (Сетевой интерфейс в виртуальной сети с общедоступным IP-адресом) в качестве руководства по развертыванию общедоступного IP-адреса с помощью шаблона. |

После создания общедоступный IP-адрес, его можно связать с виртуальной Машины назначив tooa сетевого адаптера.

## <a name="virtual-network-and-subnets"></a>Виртуальные сети и подсети

Подсеть — это диапазон IP-адресов в hello виртуальной сети. Виртуальную сеть можно разделить на несколько подсетей, чтобы организовать ее и повысить безопасность. Каждый сетевой Адаптер на виртуальной машине — подключенных tooone подсети в одной виртуальной сети. Сетевые адаптеры подключенных toosubnets (одном или разных) в виртуальной сети могут взаимодействовать друг с другом без какой-либо дополнительные настройки.

При настройке виртуальной сети указываются топология hello, включая hello доступных адресные пространства и подсети. Если tooother toobe подключенных виртуальных сетей или локальных сетей hello виртуальной сети, необходимо выбрать диапазоны адресов, которые не перекрываются. Hello IP-адреса являются личными и не доступен из Интернета, который имел значение true только для hello-routeable IP-адресов 10.0.0.0/8, 172.16.0.0/12 или 192.168.0.0/16 hello. Теперь Azure обрабатывает любой диапазон адресов в рамках пространства hello частной виртуальной сети IP-адресов, доступный только в пределах hello виртуальной сети, в пределах взаимосвязанных виртуальных сетей и из локальной папки. 

Если вы работаете в рамках организации, в котором кто отвечает за hello внутренним сетям, необходимо обратиться toothat пользователя перед выбором пространство имен. Убедитесь, что не перекрываются и сообщите hello дискового пространства, toouse, они не пытаются выполнить toouse hello же диапазон IP-адресов. 

По умолчанию нет существует границы безопасности между подсетями, поэтому виртуальные машины в каждой из этих подсетей можно говорить tooone другой. Тем не менее можно настроить группы безопасности сети (Nsg), что позволит вам tooand поток трафика hello toocontrol из подсетей и tooand из виртуальных машин. 

В этой таблице перечислены методы hello, можно использовать toocreate виртуальной сети и подсети.   

| Метод | Описание |
| ------ | ----------- |
| [Портал Azure](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Если позволить создать виртуальную сеть при создании виртуальной Машины Azure hello имя представляет собой сочетание hello имя группы ресурсов, содержащий hello виртуальной сети и **- vnet**. адресное пространство Hello 10.0.0.0/24, имя подсети требуется hello **по умолчанию**, и диапазон адресов подсети hello 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Вы используете [New AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) и [New AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate подсети и виртуальной сети. Можно также использовать [добавить AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd tooan подсети существующей виртуальной сети. |
| [Интерфейс командной строки Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Hello подсети и виртуальной сети hello создаются в hello же время. Укажите **--имя подсети** параметр слишком[создания az сети vnet](https://docs.microsoft.com/cli/azure/network/vnet#create) с именем подсети hello. |
| [Шаблон](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Здравствуйте, наиболее простым способом toocreate виртуальной сети и подсети является toodownload существующего шаблона, например [виртуальной сети с двумя подсетями](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)и измените его вашим потребностям. |

## <a name="network-security-groups"></a>Группы безопасности сети

Объект [группы безопасности сети (NSG)](../../virtual-network/virtual-networks-nsg.md) содержит список правил список управления доступом (ACL), которые разрешают или запрещают toosubnets сетевого трафика и сетевые адаптеры. Nsg можно связать с подсетями или отдельных подсети tooa подключенных сетевых адаптеров. Когда NSG связана с подсетью, правила ACL hello применяются hello tooall виртуальные машины в этой подсети. Кроме того, передача трафика tooan отдельный сетевой Адаптер может быть ограничено связывание NSG непосредственно tooa сетевого адаптера.

Группы безопасности сети содержат два набора правил: для входящего и исходящего трафика. Hello приоритет для правила должен быть уникальным в пределах каждого набора. Каждое правило имеет свойства протокола, диапазоны исходных портов и портов назначения, префиксы адресов, направление трафика, приоритет и тип доступа. 

Все группы NSG содержат набор правил по умолчанию. правила по умолчанию Hello не может быть удалена, но так как они будут назначены hello самый низкий приоритет, они могут быть переопределены созданных вами правил hello. 

При связывании NSG tooa Сетевых hello правила доступа к сети в hello NSG, примененные только toothat сетевого адаптера. Если NSG tooa применен один сетевой Адаптер на виртуальной Машине multi-NIC, он не влияет на toohello трафик других сетевых адаптеров. Можно связать другой Nsg tooa сетевой Адаптер (или виртуальных Машин, в зависимости от модели развертывания hello) и hello подсети, к которому привязан через сетевой Адаптер или виртуальной Машины. Приоритет отдается на основе hello направление трафика.

Убедитесь, что слишком[план](../../virtual-network/virtual-networks-nsg.md#planning) Nsg при планировании виртуальные машины и виртуальной сети.

В этой таблице перечислены hello методы, которые можно использовать toocreate группы безопасности сети.

| Метод | Описание |
| ------ | ----------- |
| [Портал Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | При создании виртуальной Машины в Azure portal hello NSG создается автоматически и создает портал hello связанного toohello сетевого Адаптера. Имя Hello hello NSG представляет собой сочетание имени hello hello виртуальной Машины и **- nsg**. Этот NSG содержит одним правилом входящего трафика с приоритета 1000, tooRDP набор служб, набор tooTCP hello протокол, порт значение too3389 и tooAllow задать действие. Если вы хотите tooallow любые другие входящий трафик toohello виртуальной Машины, необходимо добавить toohello Дополнительные правила NSG. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Используйте [New AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) и содержат сведения, необходимые hello правило. Используйте [New AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG. Используйте [AzureRmVirtualNetworkSubnetConfig набор](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) hello tooconfigure NSG для подсети hello. Используйте [набор AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) toohello NSG tooadd hello виртуальной сети. |
| [Интерфейс командной строки Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Используйте [создать az сети nsg](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially создать hello NSG. Используйте [создать правило nsg сети az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd правила toohello NSG. Используйте [обновления подсети виртуальной сети сети az](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) NSG toohello tooadd hello подсети. |
| [Шаблон](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Используйте шаблон [Create a Network Security Group](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) (Создание группы безопасности сети) в качестве руководства по развертыванию группы безопасности сети с помощью шаблона. |

## <a name="load-balancers"></a>Балансировщики нагрузки

[Подсистема балансировки нагрузки Azure](../../load-balancer/load-balancer-overview.md) обеспечивает высокий уровень доступности и сетевой производительности tooyour приложений. Подсистема балансировки нагрузки можно настроить слишком[балансировки входящего трафика Интернета](../../load-balancer/load-balancer-internet-overview.md) tooVMs или [балансировки трафика между виртуальными машинами в виртуальной сети](../../load-balancer/load-balancer-internal-overview.md). Балансировщик нагрузки также можно сбалансировать трафик между виртуальными машинами и локальными компьютерами в сети между организациями или tooa прямого внешнего трафика определенную виртуальную Машину.

Hello нагрузки балансировки maps входящим и исходящим трафиком между hello открытый IP-адрес и порт для балансировки нагрузки hello и hello частный IP-адрес и порт hello виртуальной Машины.

При создании балансировщика нагрузки необходимо также учитывать следующие элементы конфигурации.

- **Конфигурация внешних IP-адресов.** Балансировщик нагрузки может включать в себя один или несколько внешних IP-адресов, которые также называются виртуальными IP-адресами (VIP). Эти IP-адреса используются в качестве входящего трафика hello.
- **Пул адресов серверной части** — распределенных IP-адресов, связанных с нагрузкой toowhich hello сетевого Адаптера.
- **Правила преобразования сетевых адресов** -определяет как входящий трафик через hello интерфейсный IP-адресов и IP toohello распределенной серверной части.
- **Правила подсистемы балансировки нагрузки** -сопоставляет данного переднего плана IP-адрес и порт набор tooa сочетания серверной части IP-адресами и портом. Отдельный балансировщик нагрузки может применять несколько правил балансировки нагрузки. Каждое правило представляет собой сочетание интерфейсных IP-адреса и порта и внутренних IP-адреса и порта, связанных с виртуальными машинами.
- **[Проверяет](../../load-balancer/load-balancer-custom-probe-overview.md)**  -мониторы hello работоспособность виртуальных машин. При сбое toorespond зонда подсистемы балансировки нагрузки hello перестает отправлять новых подключений toohello неработоспособности виртуальной Машины. существующие подключения Hello не затрагиваются и новые соединения отправляются toohealthy виртуальных машин.

В этой таблице перечислены hello методы, которые можно использовать toocreate балансировки нагрузки с выходом в Интернет.

| Метод | Описание |
| ------ | ----------- |
| Портал Azure | Не удается создать балансировки нагрузки с выходом в Интернет, с помощью hello портал Azure в настоящее время. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | Идентификатор hello tooprovide hello общедоступных IP-адрес, который используется ранее созданный [New AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) с hello **- PublicIpAddress** параметра. Используйте [New AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) конфигурации hello toocreate hello пула адресов серверной части. Используйте [New AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate правила NAT, связанные с hello интерфейсный IP-конфигурации, созданный для входящих подключений. Используйте [New AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello проверяет, что нужно. Используйте [New AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) конфигурации подсистемы балансировки нагрузки toocreate hello. Используйте [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) балансировки нагрузки toocreate hello.|
| [Интерфейс командной строки Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Используйте [создать балансировки нагрузки сети az](https://docs.microsoft.com/cli/azure/network/lb#create) конфигурации подсистемы балансировки toocreate hello начальной загрузки. Используйте [ip az сетевой балансировки нагрузки переднего плана создания](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd hello общедоступный IP-адрес, созданный ранее. Используйте [az балансировки нагрузки пул сетевых адресов-создать](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) конфигурации hello tooadd hello пула адресов серверной части. Используйте [az сетевой балансировки нагрузки входящего трафика nat правил создания](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd правила преобразования сетевых адресов. Используйте [создать правило балансировки нагрузки сети az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) правила подсистемы балансировки нагрузки tooadd hello. Используйте [создать зонд балансировки нагрузки сети az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello зонды. |
| [Шаблон](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Используйте [2 ВМ в подсистему балансировки нагрузки и настроить правила преобразования сетевых адресов на hello балансировки Нагрузки](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) в качестве руководства по развертыванию балансировки нагрузки, с помощью шаблона. |
    
В этой таблице перечислены hello методы, которые можно использовать toocreate внутренний балансировщик нагрузки.

| Метод | Описание |
| ------ | ----------- |
| Портал Azure | Не удается создать внутренний балансировщик нагрузки с помощью hello портал Azure в настоящее время. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | частный IP-адрес в подсети сети hello, используйте tooprovide [New AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) с hello **- адрес PrivateIpAddress** параметра. Используйте [New AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) конфигурации hello toocreate hello пула адресов серверной части. Используйте [New AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate правила NAT, связанные с hello интерфейсный IP-конфигурации, созданный для входящих подключений. Используйте [New AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello проверяет, что нужно. Используйте [New AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) конфигурации подсистемы балансировки нагрузки toocreate hello. Используйте [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) балансировки нагрузки toocreate hello.|
| [Интерфейс командной строки Azure](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Используйте hello [создать балансировки нагрузки сети az](https://docs.microsoft.com/cli/azure/network/lb#create) конфигурацию подсистемы балансировки начальной загрузки hello toocreate команды. toodefine hello частный IP-адрес, используйте [ip az сетевой балансировки нагрузки переднего плана создания](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) с hello **— частный IP-адрес** параметра. Используйте [az балансировки нагрузки пул сетевых адресов-создать](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) конфигурации hello tooadd hello пула адресов серверной части. Используйте [az сетевой балансировки нагрузки входящего трафика nat правил создания](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd правила преобразования сетевых адресов. Используйте [создать правило балансировки нагрузки сети az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) правила подсистемы балансировки нагрузки tooadd hello. Используйте [создать зонд балансировки нагрузки сети az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello зонды.|
| [Шаблон](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Используйте [2 ВМ в подсистему балансировки нагрузки и настроить правила преобразования сетевых адресов на hello балансировки Нагрузки](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) в качестве руководства по развертыванию балансировки нагрузки, с помощью шаблона. |

## <a name="vms"></a>Виртуальные машины

Виртуальные машины можно создать в hello же виртуальной сети и они могут подключаться другие tooeach использовании частных IP-адресов. Они могут подключаться, даже если они находятся в разных подсетях, без необходимости tooconfigure hello шлюз или используйте общих IP-адресов. tooput виртуальные машины в виртуальной сети, создайте hello виртуальной сети, и при создании каждой виртуальной Машине можно назначить его toohello виртуальной сети и подсети. Параметры сети виртуальных машин задаются во время развертывания или запуска,  

а IP-адрес назначается во время развертывания. Если в виртуальную сеть или подсеть развертывается несколько виртуальных машин, каждая из них получает свой IP-адрес во время загрузки. Динамический IP-адрес (DIP) — hello внутренний IP-адрес виртуальной Машины. Можно выделить статический DIP-tooa виртуальной Машины. Если выделить статический DIP, можно использовать tooavoid конкретной подсети, случайно повторное использование статического DIP для другой виртуальной Машиной.  

Если создание виртуальной Машины и более поздней версии требуется toomigrate его в виртуальной сети, не простое изменение конфигурации. Необходимо повторно развернуть hello виртуальной Машины в виртуальной сети hello. Hello простым способом tooredeploy — toodelete hello виртуальной Машины, но не все диски подключены tooit и затем повторно создать hello виртуальной Машины с помощью hello исходных дисков в hello виртуальной сети. 

В этой таблице перечислены методы hello, можно использовать toocreate виртуальной Машины в виртуальной сети.

| Метод | Описание |
| ------ | ----------- |
| [Портал Azure](../virtual-machines-windows-hero-tutorial.md) | Сетевые параметры использует hello по умолчанию, которые были ранее упомянутых toocreate виртуальной Машины с одного сетевого адаптера. toocreate виртуальной Машины с несколькими сетевыми адаптерами, необходимо использовать другой метод. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Включает использование hello [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello сетевого Адаптера, созданный ранее toohello конфигурацию виртуальной Машины. |
| [Шаблон](ps-template.md) | Используйте шаблон [Very simple deployment of a Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) (Простое развертывание виртуальной машины Windows) в качестве руководства по развертыванию виртуальной машины с помощью шаблона. |

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, как tooconfigure [определяемые пользователем маршруты и IP-пересылки](../../virtual-network/virtual-networks-udr-overview.md). 
- Узнайте, как tooconfigure [tooVNet подключений виртуальной сети](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Узнайте, каким образом слишком[Устранение маршруты](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
