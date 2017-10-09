## <a name="route-tables"></a>Таблицы маршрутов
Ресурсы таблицы маршрутизации содержит маршруты toodefine потоки трафика в рамках инфраструктуры Azure. Можно использовать определяемых пользователем маршрутов (UDR) toosend весь трафик с данной подсети tooa виртуального устройства, например брандмауэром или вторжений обнаружения системы (IDS). Можно связать toosubnets таблицы маршрутов. 

Таблицы маршрутов содержат hello следующие свойства.

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **routes** |Коллекция определяемых пользователем маршрутов в таблице маршрутов hello |См. раздел [Определяемые пользователем маршруты](#User-defined-routes). |
| **Подсети** |Коллекция таблицы маршрутов для подсети hello применяется слишком|См. раздел [Подсети](#Subnets). |

### <a name="user-defined-routes"></a>Определяемые пользователем маршруты
Toospecify UDRs, где следует отправлять трафик, можно создать на основе его адреса назначения. Маршрут можно считать определение шлюза по умолчанию hello, на основе адреса назначения hello сетевого пакета.

UDRs содержат hello следующие свойства. 

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **addressPrefix** |Префикс адреса или полного IP-адрес для назначения hello |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Тип трафика hello устройства будут отправляться слишком|VirtualAppliance, VPN-шлюз, Интернет |
| **nextHopIpAddress** |IP-адрес следующего прыжка hello |192.168.1.4 |

Пример таблицы маршрутов в формате JSON:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Дополнительные ресурсы
* Более подробная информация об [определяемых пользователем маршрутах](../articles/virtual-network/virtual-networks-udr-overview.md).
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt502549.aspx) для таблицы маршрутов.
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt502539.aspx) для пользователя определено маршрутов (UDRs).

