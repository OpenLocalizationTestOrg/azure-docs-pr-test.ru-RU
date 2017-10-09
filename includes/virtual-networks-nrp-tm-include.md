## <a name="traffic-manager-profile"></a>Профиль диспетчера трафика
Диспетчер трафика и его дочерних ресурса конечной точки включить tooendpoints по DNS в Azure и за пределами Azure. Такое распределение трафика регулируется с помощью политик. Диспетчер трафика также позволяет отслеживать toobe работоспособности конечной точки и трафика, соответствующим образом распространяется на основе hello работоспособности конечной точки. 

| Свойство | Описание |
| --- | --- |
| **trafficRoutingMethod** |Возможные значения: *Performance* (производительный), *Weighted* (взвешенный) и *Priority* (приоритетный). |
| **dnsConfig** |Полное доменное имя для профиля hello |
| **Протокол** |Протокол мониторинга. Возможные значения: *HTTP* и *HTTPS*. |
| **Порт** |порт мониторинга |
| **Путь** |путь мониторинга |
| **Конечные точки** |контейнер для ресурсов конечных точек |

### <a name="endpoint"></a>Конечная точка
Конечная точка — это дочерний ресурс профиля диспетчера трафика. Он представляет собой службу или веб-трафика пользователя toowhich конечной точке распространяется на основе политики настроен hello в hello ресурс профиля диспетчера трафика. 

| Свойство | Описание |
| --- | --- |
| **Тип** |Здравствуйте, тип конечной точки hello, возможные значения: *Azure конечной точки*, *внешней конечной точки*, и *вложенные конечной точки* |
| **targetResourceId** |общедоступный IP-адрес конечной точки службы или сайта Это может быть конечная точка Azure или внешняя конечная точка. |
| **Вес** |вес конечной точки, используемый при управлении трафиком |
| **Приоритет** |приоритет hello конечной точки, используемые toodefine действие отработки отказа |

Пример диспетчера трафика в формате JSON: 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Дополнительные ресурсы
Дополнительные сведения см. в [документации по REST API для диспетчера трафика](https://msdn.microsoft.com/library/azure/mt163664.aspx).

