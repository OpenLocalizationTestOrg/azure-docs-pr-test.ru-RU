прежних версий (старая) шлюза VPN Hello номера SKU::

* Basic
* Стандартная
* HighPerformance.

VPN-шлюз не использует номер SKU шлюза UltraPerformance hello. Сведения о hello UltraPerformance SKU содержатся hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) документации.

При работе с Здравствуйте устаревших SKU, примите во внимание hello ниже:

* Следует toouse типа VPN на политиках тип VPN необходимо использовать hello Basic SKU. Тип VPN на основе политик (ранее называемый статической маршрутизацией) не поддерживается в других номерах SKU.
* BGP не поддерживается в Basic SKU hello.
* Шлюз ExpressRoute VPN сосуществовать конфигурации не поддерживаются hello Basic SKU.
* Активный / активный S2S подключений VPN-шлюза можно настроить на hello высокопроизводительные SKU только.
