### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Какие клиентские операционные системы можно использовать для подключения типа "точка — сеть"?

поддерживаются следующие клиентские операционные системы Hello:

* Windows 7 (32-разрядная и 64-разрядная версии)
* Windows Server 2008 R2 (только 64-разрядная версия)
* Windows 8 (32-разрядная и 64-разрядная версии)
* Windows 8.1 (32-разрядная и 64-разрядная версии)
* Windows Server 2012 (только 64-разрядная версия)
* Windows Server 2012 R2 (только 64-разрядная версия)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Можно ли использовать для подключения "точка — сеть" любой VPN-клиент, поддерживающий SSTP?

Нет. Поддерживается только только toohello версии операционной системы Windows перечисленных выше.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Сколько конечных точек VPN-клиента можно настроить в конфигурации "точка — сеть"?

Мы поддерживаем too128 VPN клиенты toobe может tooconnect tooa виртуальной сети в hello, же время.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Можно ли использовать корневой ЦС собственной внутренней системы PKI для подключения "точка — сеть"?

Да. Раньше поддерживались только самозаверяющие корневые сертификаты. Вы по-прежнему можете загружать до 20 корневых сертификатов.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Можно ли просматривать прокси-серверы и брандмауэры с использованием возможности "точка — сеть"?

Да. Мы используем tootunnel SSTP (Secure Socket Tunneling Protocol) через брандмауэры. Этот туннель будет отображаться как HTTPs-соединение.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Если перезапустить клиентского компьютера, настроенного для точки сайтами hello VPN их автоматическое переподключение?

По умолчанию hello клиентский компьютер не восстановит hello VPN-подключение автоматически.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Точка-сайт поддержки автоматическое повторное подключение и DDNS на hello VPN-клиентов?

В конфигурациях VPN "точка — сеть" в настоящее время не поддерживаются автоматическое повторное подключение и DDNS.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Можно ли использовать сеть-сеть и сосуществовать точки сайтами конфигураций для hello таким же виртуальной сети?

Да. Оба этих решения будут работать, если ваш шлюз использует тип VPN на основе маршрутов. Hello классической модели развертывания требуется шлюз с динамической. Мы делаем не поддержки точки сайтами для статического маршрута шлюзах VPN или шлюзы, использующие hello `-VpnType PolicyBased` командлета.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Настроить точки сайтами клиента tooconnect toomultiple виртуальных сетей в hello одновременно?

Да, это возможно. Но hello виртуальных сетей не могут иметь перекрывающиеся префиксы IP и hello точки сайтами адресные пространства не должны пересекаться между виртуальными сетями hello.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>На какую пропускную способность можно рассчитывать в конфигурациях подключения "сеть — сеть" и "точка — сеть"?

Бывает сложно toomaintain hello точную пропускную способность для туннелей VPN hello. IPsec и SSTP — это надежно зашифрованные протоколы VPN. Пропускная способность также ограничивается hello задержки и пропускной способности между вашей организацией и hello Интернета.
