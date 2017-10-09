### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>Поддерживается ли политика IPsec/IKE во всех номерах SKU VPN-шлюзов Azure?
Политика IPsec/IKE поддерживается в VPN-шлюзах Azure класса **VpnGw1, VpnGw2, VpnGw3, Standard** и **HighPerformance**. **Basic** не поддерживается.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Сколько политик можно указать для подключения?
Можно указать только ***одну*** комбинацию политик для каждого подключения.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Можно ли указать частичную политику для подключения (например, только алгоритмы IKE без IPsec)?
Нет, следует указать все алгоритмы и параметры для IKE (основной режим) и IPsec (быстрый режим). Указать частичную политику нельзя.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Что такое алгоритмы hello и значений длины ключа, поддерживаемые в настраиваемой политике hello
Hello перечислены hello поддерживается алгоритмов шифрования и значений длины ключа можно настроить hello клиентами. Необходимо выбрать один вариант для каждого поля.

| **IPsec/IKEv2**  | **Варианты**                                                                   |
| ---              | ---                                                                           |
| Шифрование IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Проверка целостности IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Группа DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, нет |
| Шифрование IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, нет      |
| Целостность IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Группа PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, нет                              |
| Время существования QM SA   | Секунды (целое число, **минимум 300**, по умолчанию — 27 000 с)<br>Килобайты (целое число, **минимум 1024**, по умолчанию — 102 400 000 КБ)           |
| Селектор трафика | UsePolicyBasedTrafficSelectors ($True/$False; по умолчанию — $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 являются hello же, как группы Диффи-Хелмана **14** в IKE и IPsec PFS. См. в разделе [группы Диффи-Хелмана](#DH) для hello выполните сопоставления.
> 2. Алгоритмы GCMAES необходимо указать hello одинаковую длину алгоритма и ключа GCMAES для шифрования IPsec и целостности.
> 3. Время существования сопоставления безопасности основного режима IKEv2 имеет фиксированный размер 28800 секунд на шлюзах Azure VPN hello
> 4. Время существования QM SA указывать необязательно. Если эти значения не указаны, по умолчанию используются значения 27 000 с (7,5 ч) и 102 400 000 КБ (102 ГБ).
> 5. UsePolicyBasedTrafficSelector является параметр подключения hello. См. в разделе часто задаваемые вопросы о Далее hello элемента для «UsePolicyBasedTrafficSelectors»

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Нужны ли все toomatch между hello политики шлюза Azure VPN и Мои настройки устройства VPN локальной?
В локальной конфигурации устройства VPN должны быть согласованы или содержать следующие алгоритмы hello и параметры, указывающие на hello Azure IPsec/IKE политики:

* Алгоритм шифрования IKE
* Алгоритм проверки целостности IKE
* Группа DH
* Алгоритм шифрования IPsec
* Алгоритм проверки целостности IPsec
* Группа PFS
* Селектор трафика (*)

время существования Hello SA только локальные спецификации, не обязательно toomatch.

При включении **UsePolicyBasedTrafficSelectors**, требуется tooensure устройство VPN имеет hello сопоставления селекторы трафик, имеющий все сочетания свои префиксы (шлюз локальной сети) в локальной сети из hello Префиксы виртуальной сети Azure, вместо any к any. Например при свои префиксы в локальной сети, 10.1.0.0/16 и 10.2.0.0/16 и префиксы вашей виртуальной сети: 192.168.0.0/16 и 172.16.0.0/16, необходимо toospecify hello, следуя селекторы трафика:
* 10.1.0.0/16 <====> 192.168.0.0/16;
* 10.1.0.0/16 <====> 172.16.0.0/16;
* 10.2.0.0/16 <====> 192.168.0.0/16;
* 10.2.0.0/16 <====> 172.16.0.0/16.

См. слишком[подключения нескольких устройств VPN на основе политики локальной](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) Дополнительные сведения о том, как toouse этот параметр.

### <a name ="DH"></a>Поддерживаемые группы Диффи-Хелмана
в следующей таблице Hello перечислены hello поддерживается группы Диффи-Хелмана IKE (DHGroup) и IPsec (PFSGroup):

| **Группа Диффи-Хелмана**  | **DHGroup**              | **PFSGroup** | **Длина ключа** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP (768 бит)   |
| 2                         | DHGroup2                 | PFS2         | MODP (1024 бит)  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP (2048 бит)  |
| 19                        | ECP256                   | ECP256       | ECP (256 бит)    |
| 20                        | ECP384                   | ECP284       | ECP (384 бит)    |
| 24                        | DHGroup24                | PFS24        | MODP (2048 бит)  |
|                           |                          |              |                |

См. слишком[RFC3526](https://tools.ietf.org/html/rfc3526) и [RFC5114](https://tools.ietf.org/html/rfc5114) для получения дополнительных сведений.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Заменяет настраиваемой политики hello hello по умолчанию наборы политики IPsec/IKE для VPN-шлюзы Azure?
Да, после на подключение указано пользовательскую политику, VPN-шлюз Azure будет использовать только политики hello hello подключения, в качестве IKE инициатор и респондент IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Если удалить пользовательскую политику IPsec/IKE hello подключения становится незащищенных?
Нет, hello подключения будет по-прежнему защищен IPsec/IKE. После удаления hello настраиваемой политики из соединения, hello VPN-шлюз Azure вернется к задней toohello [по умолчанию список предложений IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) и повторно запустить hello подтверждения IKE с локальными VPN-устройства.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Прерывается ли VPN-подключение при добавлении или обновлении политики IPsec/IKE?
Да, это может привести к небольшой прерывания (в несколько секунд) как hello VPN-шлюз Azure будут разделять hello существующее подключение и повторно запускать hello toore подтверждения IKE-туннель IPsec hello hello новых алгоритмов шифрования и параметрами. Убедитесь, что устройство VPN локальной настроен алгоритма сопоставления hello и ключевые преимущества toominimize hello перебоев в работе.

### <a name="can-i-use-different-policies-on-different-connections"></a>Можно ли использовать разные политики для разных подключений?
Да. Настраиваемая политика применяется на уровне подключения. Можно создавать и применять разные политики IPsec/IKE для разных подключений. Можно также выбрать tooapply настраиваемых политик на подмножестве подключений. Осталось те Hello будет использовать наборы политики IPsec/IKE hello Azure по умолчанию.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Можно использовать настраиваемую политику hello также подключения VNet-VNet
Да, настраиваемую политику можно применять для подключений IPsec между локальными или виртуальными сетями.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Требуется toospecify hello одной политике на оба ресурса подключения VNet-VNet?
Да. Туннель подключения между виртуальными сетями состоит из двух ресурсов Azure: для каждого направления используется один ресурс. Необходимо иметь оба ресурса подключения tooensure hello одной политике не устанавливает hello othereise подключения VNet-VNet.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>Работает ли настраиваемая политика IPsec/IKE для подключения ExpressRoute?
Нет. Политики IPsec/IKE работает только с S2S VPN и соединения VNet-VNet через hello VPN-шлюзы Azure.
