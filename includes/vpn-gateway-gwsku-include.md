При создании шлюза виртуальной сети, необходимо toospecify hello шлюза, которые должны toouse SKU. Выберите hello SKU, которые удовлетворяют требованиям на основе hello типов рабочих нагрузок, пропускной способности, функции и соглашений об уровне обслуживания.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Производственная рабочая нагрузка *и* рабочая нагрузка для разработки и тестирования

Из-за различий toohello соглашений об уровне обслуживания и наборы функций, мы рекомендуем следующие номера SKU для производства hello *и* разработки и тестирования:

| **Рабочая нагрузка**                       | **Номера SKU**               |
| ---                                | ---                    |
| **Производственные, критически важные рабочие нагрузки** | VpnGw1, VpnGw2, VpnGw3 |
| **Разработка и тестирование или подтверждение концепции**   | Basic                  |
|                                    |                        |

При использовании старых hello SKU рекомендации SKU рабочей hello, Standard и высокопроизводительные SKU. Сведения о hello содержатся старые SKU [SKU шлюза (устаревший конфигурации)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Наборы функций для номеров SKU шлюзов

Новый шлюз Hello SKU оптимизировать hello наборы функций, предлагаемых на шлюзах hello:

| **SKU**| **Функции**|
| ---    | ---         |
|**базовая;**   | **VPN на основе маршрутов:** 10 туннелей с P2S<br><br>**VPN на основе политик:** (IKEv1) 1 туннель; без P2S|
| **VpnGw1, VpnGw2 и VpnGw3** | **VPN на основе маршрута**: копирование туннели too30 (*), P2S, BGP, "активный / активный", пользовательские политики IPsec/IKE, ExpressRoute или VPN-совместной работы |
|        |             |

(*) Устройства можно настроить tooconnect «PolicyBasedTrafficSelectors» на основе маршрутов VPN шлюза (VpnGw1, VpnGw2, VpnGw3) toomultiple в локальной среде на основе политики брандмауэра. См. слишком[toomultiple шлюзах VPN для подключения локального устройства VPN на основе политик с помощью PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) подробные сведения.

###  <a name="resize"></a>Изменение размеров SKU шлюза

1. Размер SKU можно изменять, выбирая между следующими вариантами: VpnGw1, VpnGw2 и VpnGw3.
2. При работе со шлюзом старого hello SKU, можно изменить между Basic, Standard и высокопроизводительные SKU.
2. Вы **нельзя** изменение размеров с SKU Basic, Standard и высокопроизводительные toohello новых VpnGw1/VpnGw2/VpnGw3 SKU. Необходимо, вместо этого [перенести](#migrate) toohello новых SKU.

###  <a name="migrate"></a>Миграция от старого SKU toohello новых SKU

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
