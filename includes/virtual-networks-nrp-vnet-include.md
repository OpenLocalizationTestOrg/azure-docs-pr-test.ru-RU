## <a name="virtual-network"></a>Виртуальная сеть
Ресурсы виртуальных сетей (VNET) и подсетей позволяют определить периметр безопасности для рабочих нагрузок, выполняемых в Azure. Виртуальная сеть характеризуется набором адресных пространств, которые также называются блоками CIDR. 

> [!NOTE]
> Сетевым администраторам знакомы нотации CIDR. Если вы не знакомы с методом CIDR, [узнайте больше о нем](http://whatismyipaddress.com/cidr).
> 
> 

![Виртуальная сеть с несколькими подсетями](./media/resource-groups-networking/Figure4.png)

Виртуальные сети содержать hello следующие свойства.

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **addressSpace** |Коллекция префиксов адресов, составляющих hello виртуальной сети в нотации CIDR |192.168.0.0/16 |
| **Подсети** |Коллекция подсетей, составляющих hello виртуальной сети |См. раздел [Подсети](#Subnets) ниже. |
| **ipAddress** |Tooobject назначить IP-адрес. Это свойство доступно только для чтения. |104.42.233.77 |

### <a name="subnets"></a>Подсети
Подсеть является дочерним ресурсом виртуальной сети, который помогает определить сегменты адресных пространств в пределах блока CIDR на основе префиксов IP-адресов. Сетевые адаптеры могут добавляться toosubnets и подключенных tooVMs, предоставляя возможность подключения к для различных рабочих нагрузок.

Подсети содержат hello следующие свойства. 

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **addressPrefix** |Один префикс адреса, которые образуют hello подсети в нотации CIDR |192.168.1.0/24 |
| **networkSecurityGroup** |NSG применяется toohello подсети |См. раздел [Группы безопасности сети](#Network-Security-Group). |
| **routeTable** |Таблица маршрутов применяется toohello подсети |См. раздел [Определяемые пользователем маршруты](#Route-table). |
| **ipConfigurations** |Коллекция объектов конфигурации IP, используемые подсети toohello подключенных сетевых адаптеров |См. раздел [Определяемые пользователем маршруты](#Route-table). |

Пример виртуальной сети в формате JSON:

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>Дополнительные ресурсы
* Более подробная информация о [виртуальной сети](../articles/virtual-network/virtual-networks-overview.md).
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163650.aspx) для виртуальных сетей.
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163618.aspx) для подсетей.

