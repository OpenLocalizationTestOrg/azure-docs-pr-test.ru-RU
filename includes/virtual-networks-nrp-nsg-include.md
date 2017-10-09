## <a name="network-security-group"></a>Группа безопасности сети
Ресурс NSG обеспечивает создание hello защитная граница для рабочих нагрузок, путем реализации разрешать и запрещать правила. Такие правила могут быть применены tooa виртуальной Машины, сетевой Адаптер или подсети.

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **Подсети** |Список идентификаторов подсети hello NSG применяется. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Список правил безопасности, которые составляют hello NSG |См. раздел [Правило безопасности](#Security-rule) ниже. |
| **defaultSecurityRules** |Список правил безопасности по умолчанию в каждой группе безопасности сети. |См. раздел [Правила безопасности по умолчанию](#Default-security-rules) ниже. |

* **Правило безопасности** : для NSG можно определить несколько правил безопасности. Каждое правило может разрешать или запрещать различные типы трафика.

### <a name="security-rule"></a>Правило безопасности
Правило безопасности является дочерний ресурс NSG, содержащий свойства hello ниже.

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **description** |Описание для правила hello |Разрешить входящий трафик для всех виртуальных машин в подсети X. |
| **protocol** |Протокол toomatch для правила hello |TCP, UDP или * |
| **sourcePortRange** |Toomatch диапазон портов источника для правила hello |80, 100–200, * |
| **destinationPortRange** |Toomatch диапазон портов назначения для правила hello |80, 100–200, * |
| **sourceAddressPrefix** |Toomatch префикс адреса источника для правила hello |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |Toomatch префикс адреса назначения для правила hello |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **direction** |Направление трафика toomatch для правила hello |inbound или outbound |
| **priority** |Приоритет для правила hello. Правила проверяются в порядке приоритета. Когда применяется правило, соответствие дополнительным правилам не проверяется. |10, 100, 65000 |
| **access** |Тип доступа tooapply ли соответствует правилу hello |allow или deny |

Пример группы безопасности сети в формате JSON:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Правила безопасности по умолчанию

Правила безопасности по умолчанию имеют hello и те же свойства, доступные в правилах безопасности. Они существуют tooprovide базовых соединений между ресурсами, имеющих toothem Nsg применяется. Вам следует знать, какие существуют [правила безопасности по умолчанию](../articles/virtual-network/virtual-networks-nsg.md#default-rules).

### <a name="additional-resources"></a>Дополнительные ресурсы
* Более подробная информация о [группах безопасности сети](../articles/virtual-network/virtual-networks-nsg.md).
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163615.aspx) для Nsg.
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163580.aspx) для правил безопасности.
