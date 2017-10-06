---
title: "Подключение компьютера tooan виртуальной сети Azure, с помощью точки сайтами и сертификат проверки подлинности: PowerShell | Документы Microsoft"
description: "Безопасное подключение виртуальной сети компьютера tooyour путем создания подключения шлюза VPN точки сайтами с использованием проверки подлинности сертификата. В этой статье относится модели развертывания диспетчера ресурсов toohello и использует PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Настройка tooa подключение точка-сайт виртуальной сети с использованием проверки подлинности сертификата: PowerShell

В этой статье показано, как toocreate виртуальную сеть с подключением точки сайтами в развертывании диспетчера ресурсов hello модели с помощью PowerShell. В этой конфигурации используется hello tooauthenticate сертификаты подключения клиента. Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Портал Azure (классический)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Шлюз VPN точки сайтами (P2S) позволяет создавать tooyour безопасное подключение виртуальной сети из отдельных клиентских компьютерах. Точка-сеть VPN-подключений полезны в тех случаях, когда требуется tooconnect tooyour виртуальной сети из удаленного расположения, например, при путем дистанционного доступа из дома или конференц-связи. P2S VPN также является решение toouse вместо VPN сайтами, при наличии только несколько клиентов, которым требуется tooconnect tooa виртуальной сети.

Использует P2S hello Secure Socket туннелирование протокола (SSTP), протокол VPN на основе SSL. P2S VPN-подключения, запустите его из hello клиентского компьютера.

![Подключение компьютера tooan виртуальной сети Azure - схема соединений точка-сеть](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Сертификат точки сайтами проверки подлинности подключений требуется hello следующее:

* VPN-шлюз с маршрутизацией на основе маршрутов.
* Hello открытый ключ (CER-файл) для корневого сертификата, являющегося отправленного tooAzure. После передачи сертификата hello, он считается доверенных сертификатов и используется для проверки подлинности.
* Сертификат клиента, который создается из корневого сертификата hello и установлена на каждом клиентском компьютере, к которому будут подключаться toohello виртуальной сети. Этот сертификат используется для проверки подлинности клиента.
* Пакет конфигурации VPN-клиента. пакет конфигурации VPN-клиента Hello содержит hello сведения, необходимые для hello клиента tooconnect toohello виртуальной сети. пакет Hello настраивает hello существующего VPN-клиента, имеет собственный toohello операционной системы Windows. Каждый клиент, который подключается должен быть настроен с использованием hello конфигурации пакета.

Для подключения типа "точка — сеть" не требуется VPN-устройство или локальный общедоступный IP-адрес. Hello VPN-подключения создается на основе SSTP (Secure Socket Tunneling Protocol). На серверной стороне hello мы поддерживаем SSTP версии 1.0, 1.1 и 1.2. Hello клиент решает, какие версии toouse. Для Windows 8.1 и более поздних версий по умолчанию используется SSTP версии 1.2. 

Дополнительные сведения о подключениях точки сайтами см. в разделе hello [точки сайтами часто задаваемые вопросы о](#faq) в конце hello в этой статье.

## <a name="before-beginning"></a>Подготовка

* Убедитесь в том, что у вас уже есть подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial).
* Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure. Дополнительные сведения об установке командлетов см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Примеры значений

Можно использовать toocreate значения пример hello тестовой среде, или ссылаться значения toothese toobetter понять hello примеры в этой статье. Мы устанавливаем hello переменные в разделе [1](#declare) hello статьи. Можно использовать шаги hello как пошаговое руководство и использовать hello значения, не изменяя их или изменить их tooreflect вашей среде. 

* **Имя: VNet1**.
* **Адресное пространство: 192.168.0.0/16** и **10.254.0.0/16**.<br>В этом примере мы используем несколько tooillustrate пространства адресов, такая конфигурация работает с несколько адресных пространств. Однако это необязательно для этой конфигурации.
* **Имя подсети: FrontEnd**.
  * **Диапазон адресов подсети: 192.168.1.0/24**.
* **Имя подсети: BackEnd.**
  * **Диапазон адресов подсети: 10.254.1.0/24.**
* **Имя подсети: GatewaySubnet.**<br>Имя подсети Hello *GatewaySubnet* является обязательным для toowork шлюза VPN hello.
  * **Диапазон адресов подсети шлюза: 192.168.200.0/24.** 
* **Пул адресов VPN-клиента: 172.16.201.0/24.**<br>VPN-клиенты, подключающиеся toohello виртуальной сети с помощью этого соединения точка-сеть получать IP-адрес из пула адресов VPN-клиента hello.
* **Подписки:** при наличии более чем одной подписке, убедитесь, что вы используете hello правильный выбор.
* **Группа ресурсов: TestRG**.
* **Расположение: восточная часть США**.
* **DNS-сервера: IP-адрес** hello DNS-сервера требуется toouse для разрешения имен.
* **Имя шлюза: Vnet1GW**.
* **Имя общедоступного IP-адреса: VNet1GWPIP**.
* **Тип VPN: RouteBased.** 

## <a name="declare"></a>1. Вход и настройка переменных

В этом разделе вход и объявления hello значения, используемые для этой конфигурации. Привет, объявленные значения используются в скриптах образец hello. Измените значения tooreflect hello собственной среде. Также можно использовать значения объявлены hello и проходят этапы hello в качестве упражнения.

1. Откройте консоль PowerShell с повышенными привилегиями и выполните вход в tooyour учетная запись Azure. Этот командлет запросит учетные данные входа hello. После входа в систему, он загружает параметры учетной записи, чтобы они были доступны tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ```
2. Получите список подписок Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Укажите требуемый toouse подписки hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Объявления переменных hello, которое следует toouse. Здравствуйте, используйте следующий пример, заменив значения hello лично, при необходимости.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Настройка шлюза виртуальной сети

1. Создайте группу ресурсов.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Создайте hello конфигурации подсети виртуальной сети hello, именование их *переднего плана*, *серверной*, и *GatewaySubnet*. Эти префиксы должна входить в адресное пространство виртуальной сети, объявленного hello.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Создайте виртуальную сеть hello.

  В этом примере hello DNS-сервер является необязательным. Если указать значение, DNS-сервер не создается. Hello IP-адрес сервера DNS, указываемое должен быть DNS-сервера, которые позволяют устранить hello имен для ресурсов hello, которому вы подключаетесь. В этом примере мы использовали частный IP-адрес, но скорее всего, что это не hello IP-адрес DNS-сервера. Быть убедиться, что toouse собственные значения.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Укажите переменные hello для hello виртуальной сети, которую вы создали.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. VPN-шлюз должен иметь общедоступный IP-адрес. Запросить ресурс IP-адреса hello и затем ссылаться tooit при создании шлюз виртуальной сети. Hello IP-адрес назначается динамически toohello ресурсов при создании шлюза VPN hello. В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов. Вы не можете запросить назначение статического общедоступного IP-адреса. Однако это не значит, что hello IP-адрес изменяется после назначения tooyour VPN-шлюз. только один раз Hello изменения адреса hello общедоступный IP-адрес когда hello шлюза будет удалена и создана заново. При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.

  Запросите динамически назначенный общедоступный IP-адрес.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Создание шлюза VPN hello

Настройте и создайте hello шлюз виртуальной сети для виртуальной сети.

* Hello *- тип шлюза* должно быть **Vpn** и hello *- VpnType* должно быть **routebased**.
* VPN-шлюза может занять toocomplete too45 минут, в зависимости от hello [номер sku шлюза](vpn-gateway-about-vpn-gateway-settings.md) выбора.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Добавление пула адресов клиента VPN hello

По завершении создания hello VPN-шлюз можно добавить пул адресов клиента VPN hello. Hello пула адресов VPN-клиента — диапазон hello, из которого hello VPN-клиентам получать IP-адрес при подключении. Используйте диапазон частных IP-адресов, не перекрывающийся с hello в локальное расположение, подключение из, или виртуальной сети, требуется tooconnect для hello. В этом примере объявляется hello пула адресов VPN-клиента, как [переменной](#declare) на шаге 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Создайте сертификаты.

Сертификаты используются VPN-клиентами Azure tooauthenticate точка-сеть виртуальных частных сетей. Необходимо отправить hello сведения об открытом ключе для hello корневого сертификата tooAzure. рассматривается как «доверять» Hello открытый ключ. Клиентские сертификаты необходимо сгенерированных hello доверенный корневой сертификат, а затем устанавливается на каждом клиентском компьютере, в хранилище сертификатов Сертификаты-текущий пользователь/персональные hello. сертификат Hello при используется tooauthenticate hello клиент инициирует соединение toohello виртуальной сети. 

Используемые самозаверяющие сертификаты должны быть созданы с помощью определенных параметров. Можно создать самозаверяющий сертификат, с помощью инструкции hello [PowerShell и Windows 10](vpn-gateway-certificates-point-to-site.md), или, если у вас нет Windows 10, можно использовать [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Очень важно следовать hello действия в инструкциях hello при создании самозаверяющие корневые сертификаты и сертификаты клиента. В противном случае hello сертификаты, создаваемые будет несовместим с подключениями P2S и возникнет ошибка соединения.

### <a name="cer"></a>1. Получить hello CER-файл для корневого сертификата hello

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Создание сертификата клиента

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Отправка hello корневого сертификата сведений открытого ключа

Убедитесь, что создание VPN-шлюза завершено. После ее завершения, можно загрузить hello CER-файл (который содержит сведения об открытом ключе hello) для tooAzure доверенного корневого сертификата. После загрузки файла a.cer Azure можно использовать tooauthenticate клиенты, на которых установлен сертификат клиента, созданные из hello доверенный корневой сертификат. При необходимости можно передать файлы сертификатов доверенных корневых - копирование всего tooa 20 – более поздних версиях.

1. Объявите переменную hello для имени сертификата, заменив значение hello свои собственные.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Замените собственными hello путь к файлу, а затем запустите командлеты hello.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Отправьте сведения об открытом ключе tooAzure hello. После загрузки сведений о сертификате hello Azure считает, что это toobe с доверенным корневым сертификатом.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Загрузите пакет конфигурации VPN-клиента hello

tooa tooconnect виртуальной сети с помощью VPN-Подключение точка-сеть, каждому клиенту необходимо установить пакет конфигурации клиента, который настраивает hello собственного клиента VPN с использованием параметров hello и файлы, необходимые tooconnect toohello виртуальной сети. пакет конфигурации VPN-клиента Hello настраивает клиент Windows VPN hello, не устанавливает новые или другие VPN-клиента. 

Можно использовать hello пакета же Настройка VPN-клиента на каждом клиентском компьютере, при условии, что версия hello соответствует hello архитектуры для клиента hello. Hello список клиентских операционных систем, поддерживаемых см hello [точки сайтами соединения часто задаваемые вопросы о](#faq) в конце hello в этой статье.

1. После создания шлюза hello можно создать и загрузить пакет конфигурации клиента hello. В этом примере загружает hello пакет для 64-разрядных клиентах. Если требуется 32-разрядного клиента toodownload hello, «Amd64» замените «x86". Можно также загрузить hello VPN-клиента с помощью портала Azure hello.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Скопируйте и вставьте ссылку hello, возвращается tooa веб-браузера toodownload hello пакета, позаботится tooremove hello кавычки вокруг hello ссылку. 
3. Загрузить и установить на клиентском компьютере hello hello. При появлении всплывающего окна SmartScreen щелкните **Дополнительно**, а затем выберите **Выполнить в любом случае**. Можно также сохранить пакет tooinstall hello на других клиентских компьютерах.
4. На клиентском компьютере hello перейдите слишком**параметры сети** и нажмите кнопку **VPN**. Hello VPN-подключение отображается hello hello виртуальной сети, он подключается.

## <a name="clientcertificate"></a>8. Установка экспортированного сертификата клиента

Подключение toocreate P2S на клиентском компьютере, отличном от hello один использовалась toogenerate hello клиентские сертификаты, необходимые tooinstall сертификат клиента. При установке сертификата клиента, необходимо hello пароль, созданный при экспорте сертификата клиента hello. Как правило это лишь дважды щелкнув сертификат hello и его установки.

Убедитесь, что сертификат клиента hello был экспортирован как PFX-файла вместе с hello всей цепочки сертификатов (он по умолчанию hello). В противном случае сведения о сертификате корневого hello отсутствует на клиентском компьютере hello и hello клиента не будет возможности tooauthenticate должным образом. Дополнительные сведения см. в разделе [Установка экспортированного сертификата клиента](vpn-gateway-certificates-point-to-site.md#install). 

## <a name="connect"></a>9. Подключение tooAzure

1. tooyour tooconnect виртуальной сети, на клиентском компьютере hello, перейдите tooVPN соединения и найдите созданное подключение VPN hello. Он называется hello точно такое же имя вашей виртуальной сети. Щелкните **Подключить**. Появится всплывающее сообщение может оказаться, что означает toousing hello сертификат. Нажмите кнопку **Продолжить** toouse с повышенными привилегиями. 
2. На hello **подключения** страница «состояние», нажмите кнопку **Connect** toostart hello соединения. Если вы видите **Выбор сертификата** экране, убедитесь, что hello отображается именно сертификат клиента hello один нужных toouse tooconnect. Если это не так, используйте правильный сертификат hello tooselect hello стрелку раскрывающегося списка и нажмите кнопку **ОК**.

  ![VPN-клиент подключается tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. Теперь подключение установлено.

  ![Подключение установлено](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Устранение неполадок подключения P2S

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Проверка подключения

1. tooverify, что VPN-подключение активно, откройте командную строку с повышенными привилегиями и выполните *ipconfig/all*.
2. Просмотр результатов hello. Обратите внимание, что hello IP-адрес, который вы получили одно hello адресов в пул адресов клиента VPN hello точки сайтами, указанное в конфигурации. результаты Hello, аналогичный пример toothis:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Подключение tooa виртуальной машины

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="addremovecert"></a>Добавление и удаление корневого сертификата

Вы можете добавлять доверенные корневые сертификаты в Azure, а также удалять их из Azure. При удалении корневого сертификата, клиенты, имеющие сертификат, сформированный из hello корневой сертификат не может проверить подлинность и не будет возможности tooconnect. Tooauthenticate клиента и подключения, необходимо tooinstall нового сертификата клиента, созданный из корневой сертификат, является доверенным tooAzure (переданный).

### <a name="addtrustedroot"></a>tooadd доверенный корневой сертификат

Добавляются файлы .cer tooAzure для too20 корневого сертификата. Hello описанных ниже действий можно добавить корневой сертификат:

#### <a name="certmethod1"></a>Метод 1

Это hello наиболее эффективный метод tooupload корневой сертификат.

1. Подготовка tooupload файл .cer hello.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Отправьте файл hello. Вы можете отправить только один файл за раз.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. загрузить этот файл сертификата hello tooverify:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Метод 2

Этот метод имеет несколько шагов, чем метод 1, но есть hello того же результата. Он включен, при необходимости данные сертификата tooview hello.

1. Создание и подготовка hello tooAzure tooadd на новый корневой сертификат. Экспорт открытого ключа hello как Base64-кодировке X.509 (. (CER) и откройте его в текстовом редакторе. Скопируйте значения hello, как показано в следующий пример hello:

  ![на основе сертификата.](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > При копировании данных сертификата hello, сделать, необходимо скопировать текст hello в виде одной непрерывной строки без возврата каретки и перевода строки. Может потребоваться toomodify представления на too'Show редактор текста hello символа/Показать возвращает все символы toosee hello каретки и перевода строки.
  >
  >

2. Укажите имя сертификата hello и сведения о ключе как переменная. Замените сведения hello собственный, как показано в hello в следующем примере:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Добавьте новый корневой сертификат hello. Можно добавлять только один сертификат за раз.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. Можно проверить, что новый сертификат hello был правильно добавлен, используя следующий пример hello.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove корневой сертификат

1. Объявления переменных hello.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Удалите сертификат hello.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Hello используйте следующий пример tooverify, hello сертификат был успешно удален.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Отзыв сертификата клиента

Можно отозвать сертификаты клиента. список отзыва позволяет tooselectively сертификатов Hello запрещать подключение точка-сеть на основе отдельных клиентских сертификатов. Эта процедура отличается от удаления доверенного корневого сертификата. При удалении .cer доверенного корневого сертификата из Azure, он отменяет hello доступ для всех клиентских сертификатов создан и подписан сертификатом корневого отозванных hello. Отзыва сертификата клиента, а не hello корневого сертификата, позволяет hello другие сертификаты, которые были созданы из hello toobe на toocontinue корневой сертификат для проверки подлинности.

Hello распространенной практикой является toouse hello корневой сертификат toomanage доступа на уровнях команда или организация, при использовании отозванных сертификатов клиентов для детальное управление доступом для отдельных пользователей.

### <a name="revokeclientcert"></a>toorevoke сертификат клиента

1. Получить отпечаток сертификата клиента hello. Дополнительные сведения см. в разделе [как tooretrieve hello отпечаток сертификата](https://msdn.microsoft.com/library/ms734695.aspx).
2. Скопируйте hello сведения tooa текстовом редакторе и удалите все пробелы, чтобы оно было непрерывной строки. Эта строка объявляется как переменная приветствия при следующем шаге.
3. Объявления переменных hello. Убедитесь, что отпечаток hello toodeclare, полученным в предыдущем шаге hello.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Добавьте hello отпечаток toohello список отозванных сертификатов. Вы видите «Succeeded» при добавлении отпечаток hello.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Проверьте, что отпечаток hello Добавление toohello список отзыва сертификатов.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. После добавления hello отпечаток сертификата hello больше не может быть используется tooconnect. Клиенты, пытающиеся tooconnect, с помощью этого сертификата сообщение о том, что этот сертификат hello больше не является допустимым.

### <a name="reinstateclientcert"></a>tooreinstate сертификат клиента

Ее можно возобновить сертификат клиента, удалив hello отпечаток из hello список отозванных сертификатов клиентов.

1. Объявления переменных hello. Убедитесь, что объявления hello правильный отпечаток для hello сертификат, который tooreinstate.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Удалите hello отпечаток сертификата из списка отзыва сертификатов hello.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Проверьте, если отпечаток hello удаляется из списка отозванных hello.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Часто задаваемые вопросы о подключениях типа "точка — сеть"

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand Дополнительные сведения о сети и виртуальные машины в разделе [обзор сети Azure и виртуальных Машин Linux](../virtual-machines/linux/azure-vm-network-overview.md).
