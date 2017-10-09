## <a name="nic"></a>Сетевая карта
Ресурс сетевого интерфейса адаптер (NIC) обеспечивает подключение tooan существующей подсети в виртуальной сети ресурс. Несмотря на то, что вы сможете создать сетевой Адаптер в виде отдельного объекта, необходимо tooassociate его tooactually объекта tooanother обеспечить подключение. Сетевой Адаптер может быть используется tooconnect tooa подсеть виртуальной Машины, общедоступный IP-адрес или подсистемы балансировки нагрузки.  

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **virtualMachine** |С которым связан hello виртуальной Машины сетевого Адаптера. |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |MAC-адрес для сетевого Адаптера hello |любое значение от 4 до 30 |
| **networkSecurityGroup** |NSG связанные toohello сетевого Адаптера |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Параметры DNS для сетевого Адаптера hello |См. раздел [Общедоступный IP-адрес](#Public-IP-address). |

Сетевой адаптер или сетевой Адаптер, представляет сетевого интерфейса, который может быть связан tooa виртуальной машины (VM). У виртуальной машины может быть одна или несколько сетевых карт.

![Сетевая карта на одной виртуальной машине](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>Конфигурации IP
Сетевые адаптеры имеют дочерний объект с именем **IP-конфигураций** содержащий hello следующие свойства:

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **subnet** |Подсети hello сетевого Адаптера — подключенного к. |/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |IP-адрес для hello сетевых Адаптеров в подсети hello |10.0.0.8 |
| **privateIPAllocationMethod** |Метод выделения IP-адресов |Динамический или статический |
| **enableIPForwarding** |Hello сетевой Адаптер может использоваться для маршрутизации |Значение true или false |
| **primary** |Является ли сетевой Адаптер hello hello первичный сетевой Адаптер для виртуальной Машины hello |Значение true или false |
| **publicIPAddress** |PIP-адрес, связанный с hello сетевого Адаптера |См. раздел [Параметры DNS](#DNS-settings). |
| **loadBalancerBackendAddressPools** |Резервное hello пулов адресов конечного сетевого Адаптера, которое связано с | |
| **loadBalancerInboundNatRules** |Входящий hello правил NAT подсистемы балансировки нагрузки сетевого Адаптера, которое связано с | |

Пример общедоступного IP-адреса в формате JSON:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Дополнительные ресурсы
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163579.aspx) для сетевых адаптеров.

