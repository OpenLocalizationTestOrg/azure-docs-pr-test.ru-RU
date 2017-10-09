> [!div class="op_single_selector"]
> * [Портал](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [Интерфейс командной строки 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [Интерфейс командной строки 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Шаблон](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Виртуальные машины (ВМ) Azure подключен один или несколько сетевых интерфейсов (NIC) tooit. Любому сетевому Адаптеру может иметь одно или статический или динамический общедоступных и частных IP-адресов, назначенных tooit. Назначение нескольких IP-адресов tooa виртуальной Машины обеспечивает hello следующие возможности:

* Возможность размещать на одном сервере несколько веб-сайтов или служб с разными IP-адресами и SSL-сертификатами.
* возможность использовать виртуальную машину в качестве виртуального сетевого устройства, такого как брандмауэр или балансировщик нагрузки.
* Здравствуйте, возможность tooadd любой hello частных IP-адресов для любой из сетевых адаптеров hello tooan пула внутренней подсистемы балансировки нагрузки Azure. В hello за только hello основной IP-адрес для hello первичный сетевой Адаптер может быть добавлена tooa внутренней пула. Дополнительные сведения о toolearn tooload сбалансировать несколько IP-конфигурации чтения hello [несколько IP-конфигурации балансировки нагрузки](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи.

Каждого сетевого Адаптера, подключенного tooa виртуальная машина имеет один или несколько IP-конфигурации связанных tooit. Каждая конфигурация получает один статический или динамический частный IP-адрес. Каждая конфигурация может также иметь один открытый tooit ресурс, связанный адрес IP. Открытый ресурс IP-адреса имеет либо динамический или статический открытый IP-адреса, назначенного tooit. toolearn более о IP-адреса в Azure, ознакомьтесь со статьей hello [IP-адресов в Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) статьи. 

Имеется много частного IP toohow предел адреса можно назначать tooa сетевого адаптера. Имеется также toohow предел много общих IP-адресов, которые могут использоваться в подписку Azure. В разделе hello [Azure ограничивает](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) Дополнительные сведения см.
