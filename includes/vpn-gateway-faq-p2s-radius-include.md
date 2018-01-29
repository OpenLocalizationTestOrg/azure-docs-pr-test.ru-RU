[!INCLUDE [P2S FAQ All](vpn-gateway-faq-p2s-all-include.md)]

### <a name="is-radius-authentication-supported-on-all-azure-vpn-gateway-skus"></a>Поддерживается ли аутентификация RADIUS во всех номерах SKU VPN-шлюзов Azure?

Аутентификация RADIUS поддерживается в таких номерах SKU, как VpnGw1, VpnGw2 и VpnGw3. Если используются устаревшие номера SKU, аутентификация RADIUS поддерживается только в категориях "Стандартный" и "Высокая производительность". Она не поддерживается в номерах SKU шлюза категории "Базовый". 
 
### <a name="is-radius-authentication-supported-for-the-classic-deployment-model"></a>Поддерживается ли аутентификация RADIUS в классической модели развертывания?
 
Нет. Аутентификация RADIUS не поддерживается в классической модели развертывания.
 
### <a name="are-3rd-party-radius-servers-supported"></a>Поддерживаются ли сторонние серверы RADIUS?

Да, сторонние серверы RADIUS поддерживаются.
 
### <a name="what-are-the-connectivity-requirements-to-ensure-that-the-azure-gateway-is-able-to-reach-an-on-premises-radius-server"></a>Какие требования к подключению необходимо выполнить, чтобы обеспечить шлюзу Azure доступ к локальному серверу RADIUS?

Требуется VPN-подключение типа "сеть — сеть" к локальному сайту с правильно настроенными маршрутами.  
 
### <a name="can-traffic-to-an-on-premises-radius-server-from-the-azure-vpn-gateway-be-routed-over-an-expressroute-connection"></a>Может ли трафик направляться на локальный сервер RADIUS (из VPN-шлюза Azure) через подключение ExpressRoute?

Нет. Он может направляться только через подключение типа "сеть — сеть".
 
### <a name="is-there-a-change-in-the-number-of-sstp-connections-supported-with-radius-authentication-what-is-the-maximum-number-of-sstp-and-ikev2-connections-supported"></a>Изменилось ли количество поддерживаемых SSTP-подключений с аутентификацией RADIUS? Каково максимальное количество поддерживаемых SSTP- и IKEv2-подключений?

Количество поддерживаемых шлюзом SSTP-подключений с аутентификацией RADIUS не менялось. Как и раньше, максимальное количество — 128. Поддерживается не больше 128 подключений, независимо от того, настроено ли в шлюзе SSTP-подключение, IKEv2-подключение либо и то и другое.
 
### <a name="what-is-the-difference-between-doing-certificate-authentication-using-a-radius-server-vs-using-azure-native-certificate-authentication-by-uploading-a-trusted-certificate-to-azure"></a>В чем разница между аутентификацией на основе сертификата с помощью сервера RADIUS и собственной аутентификацией Azure на основе сертификата (путем передачи доверенного сертификата в Azure)?

Если используется аутентификация RADIUS на основе сертификата, запрос на аутентификацию передается на сервер RADIUS, который проверяет действующий сертификат. Этот вариант целесообразно применять, если требуется выполнить интеграцию с уже существующей инфраструктурой аутентификации RADIUS на основе сертификата.
  
Если используется аутентификация Azure на основе сертификата, проверку сертификата выполняет VPN-шлюз Azure. Вам нужно передать шлюзу открытый ключ сертификата. Вы также можете указать список отмененных сертификатов, подключение с помощью которых следует запретить.

### <a name="does-radius-authentication-work-with-both-ikev2-and-sstp-vpn"></a>Работает ли аутентификация RADIUS с IKEv2 и SSTP для VPN?

Да, аутентификация RADIUS поддерживается для IKEv2 и SSTP для VPN.  