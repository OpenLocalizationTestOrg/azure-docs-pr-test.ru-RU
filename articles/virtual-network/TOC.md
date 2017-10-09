# Обзор
## [Виртуальные сети](virtual-networks-overview.md)
## [Определяемые пользователем маршруты и IP-пересылка](virtual-networks-udr-overview.md)
## [Пиринг между виртуальными сетями](virtual-network-peering-overview.md)
## [Непрерывность бизнес-процессов](virtual-network-disaster-recovery-guidance.md)
## [Часто задаваемые вопросы](virtual-networks-faq.md)
## [Назначение IP-адресов](virtual-network-ip-addresses-overview-arm.md)
## Классический
### [Назначение IP-адресов](virtual-network-ip-addresses-overview-classic.md)
### [Списки управления доступом](virtual-networks-acl.md)

# Начало работы
## [Создание первой собственной виртуальной сети](virtual-network-get-started-vnet-subnet.md)

# Практическое руководство
## Планирование и проектирование
### [Виртуальные сети](virtual-network-vnet-plan-design-arm.md)
### [Группы безопасности сети](virtual-networks-nsg.md)

## Развернуть
### [Виртуальные сети](virtual-networks-create-vnet-arm-pportal.md)
#### [PowerShell](virtual-networks-create-vnet-arm-ps.md)
#### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-create-vnet-arm-cli.md)
#### [Шаблон](virtual-networks-create-vnet-arm-template-click.md)

### Группы безопасности сети
#### [Портал](virtual-networks-create-nsg-arm-pportal.md)
#### [PowerShell](virtual-networks-create-nsg-arm-ps.md)
#### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-create-nsg-arm-cli.md)
#### [Шаблон](virtual-networks-create-nsg-arm-template.md)
#### Классический
##### [PowerShell](virtual-networks-create-nsg-classic-ps.md)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-create-nsg-classic-cli.md)

### Определяемые пользователем маршруты
#### [PowerShell](virtual-network-create-udr-arm-ps.md)
#### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-network-create-udr-arm-cli.md)
#### [Шаблон](virtual-network-create-udr-arm-template.md)
#### Классический
##### [PowerShell](virtual-network-create-udr-classic-ps.md)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-network-create-udr-classic-cli.md)

### Пиринг между виртуальными сетями
#### [Одна модель развертывания — одна подписка](virtual-network-create-peering.md)
#### [Одна модель развертывания — разные подписки](create-peering-different-subscriptions.md)
#### [Разные модели развертывания — одна подписка](create-peering-different-deployment-models.md)
#### [Разные модели развертывания — разные подписки](create-peering-different-deployment-models-subscriptions.md)

### Виртуальные машины
#### Создание виртуальной машины со статическим общедоступным IP-адресом
##### [Портал](virtual-network-deploy-static-pip-arm-portal.md)
##### [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-network-deploy-static-pip-arm-cli.md)
##### [Шаблон](virtual-network-deploy-static-pip-arm-template.md)
##### Классический
###### [PowerShell](virtual-networks-reserved-public-ip.md)

#### Создание виртуальной машины со статическим частным IP-адресом
##### [Портал](virtual-networks-static-private-ip-arm-pportal.md)
##### [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-static-private-ip-arm-cli.md)
##### Классический
###### [Портал](virtual-networks-static-private-ip-classic-pportal.md)
###### [PowerShell](virtual-networks-static-private-ip-classic-ps.md)
###### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-static-private-ip-classic-cli.md)

#### Создание виртуальной машины с несколькими сетевыми интерфейсами
##### [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### Классический
###### [PowerShell](virtual-network-deploy-multinic-classic-ps.md)
###### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-network-deploy-multinic-classic-cli.md)

#### Создание виртуальной машины с несколькими IP-адресами
##### [Портал Azure](virtual-network-multiple-ip-addresses-portal.md)
##### [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-network-multiple-ip-addresses-cli.md)
##### [Шаблон](virtual-network-multiple-ip-addresses-template.md)

#### [Создание виртуальной машины с ускоренной сетью](virtual-network-create-vm-accelerated-networking.md)

### Сценарии подключения
#### [TooVNet виртуальной сети (VNet)](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Виртуальная сеть (диспетчера ресурсов) tooa виртуальной сети (классические)](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Виртуальная сеть tooon локальную сеть (VPN)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Виртуальная сеть tooon локальную сеть (ExpressRoute)](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Архитектура высокодоступной гибридной сети](../guidance/guidance-hybrid-network-expressroute-vpn-failover.md?toc=%2fazure%2fvirtual-network%2ftoc.json)

### Сценарии обеспечения безопасности
#### [Защита сетей с использованием виртуальных устройств](virtual-network-scenario-udr-gw-nva.md)
#### [DMZ между Azure и hello Интернета](../guidance/guidance-iaas-ra-secure-vnet-dmz.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Облачная служба и сетевая безопасность](../best-practices-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Простая сеть периметра с группами безопасности сети](virtual-networks-dmz-nsg-asm.md)
##### [Сеть периметра с брандмауэром и группами безопасности сети](virtual-networks-dmz-nsg-fw-asm.md)
##### [Сеть периметра с брандмауэром, определяемым пользователем маршрутом и группами безопасности сети](virtual-networks-dmz-nsg-fw-udr-asm.md)
##### [Пример приложения](virtual-networks-sample-app.md)

### Классический
#### [Виртуальная сеть](create-virtual-network-classic.md)
##### [Портал](virtual-networks-create-vnet-classic-pportal.md)
##### [PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)
##### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-networks-create-vnet-classic-cli.md)

## Настройка
### Виртуальные машины
#### [Добавление и удаление сетевых интерфейсов](virtual-network-network-interface-vm.md)
#### [Разрешение имен для виртуальных машин и облачных служб](virtual-networks-name-resolution-for-vms-and-role-instances.md)
#### [Оптимизация пропускной способности сети](virtual-network-optimize-network-bandwidth.md)
#### [Просмотр и изменение имен узлов](virtual-networks-viewing-and-modifying-hostnames.md)
### Классический
#### Доступ к спискам управления
##### [Портал](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [PowerShell](virtual-networks-acl-powershell.md)

## Управление
### [Виртуальные сети](virtual-network-manage-network.md)
#### [Подсети](virtual-network-manage-subnet.md)
#### [Пиринг](virtual-network-manage-peering.md)
#### Классический
##### [Файл конфигурации сети](virtual-networks-using-network-configuration-file.md)
##### [Миграция с регионом tooa территориальная группа](virtual-networks-migrate-to-regional-vnet.md)
### Группы безопасности сети
#### [Портал](virtual-network-manage-nsg-arm-portal.md)
#### [PowerShell](virtual-network-manage-nsg-arm-ps.md)
#### [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](virtual-network-manage-nsg-arm-cli.md)
#### [Журналы](virtual-network-nsg-manage-log.md)
### Сетевые интерфейсы
#### [Создание, изменение и удаление сетевых интерфейсов](virtual-network-network-interface.md)
#### [Добавление, изменение и удаление IP-адресов](virtual-network-network-interface-addresses.md)
### Виртуальные машины
#### [Переместить в другой подсети tooa виртуальной Машины](virtual-networks-move-vm-role-to-subnet.md)
### [Типы IP-адресов и методы распределения в Azure](virtual-network-public-ip-address.md)

## Устранение неполадок
### Группы безопасности сети
#### [Портал](virtual-network-nsg-troubleshoot-portal.md)
#### [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
### Маршруты
#### [Портал](virtual-network-routes-troubleshoot-portal.md)
#### [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
### [Тестирование пропускной способности](virtual-network-bandwidth-testing.md)
### [Не удается удалить виртуальные сети](virtual-network-troubleshoot-cannot-delete-vnet.md)
### [Проблемы с подключением tooVM виртуальной Машины](virtual-network-troubleshoot-connectivity-problem-between-vms.md)

# Справочные материалы
## [Примеры кода](https://azure.microsoft.com/en-us/resources/samples/?service=virtual-network)
## [PowerShell (Resource Manager)](/powershell/module/azurerm.network)
## [PowerShell (классическая модель)](/powershell/module/azure/)
## [Интерфейс командной строки Azure](/cli/azure/network)
## [Java](/java/api/)
## [REST (Resource Manager)](https://msdn.microsoft.com/library/mt163658.aspx)
## [REST (классическая модель)](https://msdn.microsoft.com/library/jj157182.aspx)


# Сопутствующие материалы
## [Виртуальные машины](/azure/virtual-machines/)
## [Шлюз приложений](/azure/application-gateway/)
## [Azure DNS](/azure/dns/)
## [Диспетчер трафика](/azure/traffic-manager/)
## [Балансировщик нагрузки](/azure/load-balancer/)
## [VPN-шлюз](/azure/vpn-gateway/)
## [ExpressRoute](/azure/expressroute/)

# Ресурсы
## [Стратегия развития Azure](https://azure.microsoft.com/roadmap/?category=networking)
## [Блог о сетях](http://azure.microsoft.com/blog/topics/networking)
## [Форум по сетям](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [Цены](https://azure.microsoft.com/pricing/details/virtual-network)
## [Калькулятор цен](https://azure.microsoft.com/pricing/calculator/)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-virtual-network)
