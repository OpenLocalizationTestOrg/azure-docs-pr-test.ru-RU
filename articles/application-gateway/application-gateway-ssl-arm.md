---
title: "aaaConfigure SSL разгрузки - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate разгрузки шлюза приложения с помощью протокола SSL с помощью диспетчера ресурсов Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Настройка шлюза приложений для разгрузки SSL с помощью диспетчера ресурсов Azure

> [!div class="op_single_selector"]
> * [портал Azure](application-gateway-ssl-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-ssl-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы. Разгрузка SSL также упрощает hello интерфейсном сервере настройку и управление ими hello веб-приложения.

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. Создание виртуальной сети и подсети для шлюза приложения hello. Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети. Сам шлюз приложений должен находиться в подсети виртуальной сети.
3. Настройка шлюза приложения hello toouse серверы Hello должен существовать или в виртуальной сети hello или открытый IP/VIP-адрес, назначенный создания конечных точек.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Что такое необходимые toocreate шлюза приложения

* **Пул серверных:** hello список IP-адресов серверов hello серверной части. Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти параметры зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя. В настоящее время только hello *основные* правило поддерживается. Hello *основные* правило — распределение нагрузки с циклическим перебором.

**Дополнительные примечания по настройке конфигурации**

Для настройки сертификатов SSL, hello протокола в **HttpListener** следует изменить слишком*Https* (с учетом регистра). Hello **SslCertificate** слишком добавляется элемент**HttpListener** с hello значения переменной, настроенных для hello SSL-сертификат. Hello интерфейсный порт должен быть обновленные too443.

**сопоставление на основе файла cookie tooenable**: шлюза приложения может быть настроенный tooensure запроса из сеанса клиента всегда является направленным toohello одной виртуальной Машины hello веб-ферме. Этот сценарий выполняется путем внедрения кода файла cookie сеанса, которое разрешает трафик toodirect шлюза hello соответствующим образом. Задайте сопоставление на основе файла cookie tooenable **CookieBasedAffinity** слишком*включено* в hello **BackendHttpSettings** элемента.

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

Создание шлюза и hello элементов приложения, требующие toobe настроен порядок hello указывается Hello различие между использованием hello Azure классической модели развертывания и диспетчера ресурсов Azure.

С помощью диспетчера ресурсов все компоненты шлюза приложения настраиваются отдельно и затем поместить вместе toocreate шлюза ресурса приложения.

Ниже приведены шаги, которые необходимы toocreate hello шлюза приложения.

1. Создание группы ресурсов для диспетчера ресурсов
2. Создание виртуальной сети, подсети и общедоступный IP-адрес для шлюза приложения hello
3. Создание объекта конфигурации шлюза приложений
4. Создание ресурса шлюза приложений.

## <a name="create-a-resource-group-for-resource-manager"></a>Создание группы ресурсов для диспетчера ресурсов

Убедитесь, что переключения командлеты PowerShell режим toouse hello диспетчера ресурсов Azure. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Шаг 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Шаг 2

Проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

С помощью учетных данных, запрашиваемых tooauthenticate.

### <a name="step-3"></a>Шаг 3.

Выберите, какие toouse вашей подписки Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Шаг 4.

Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Этот параметр используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды toocreate, использует шлюз приложений hello таким же группе ресурсов.

В приведенном выше примере hello, мы создали группу ресурсов под названием **appgw RG** и расположение **Запад США**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Создание виртуальной сети и подсети для шлюза приложения hello

Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов:

### <a name="step-1"></a>Шаг 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Этот образец присваивает hello диапазон адресов 10.0.0.0/24 tooa подсети переменной toobe используется toocreate виртуальной сети.

### <a name="step-2"></a>Шаг 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

В этом примере создается виртуальная сеть с именем **appgwvnet** в группе ресурсов **appgw rg** для региона hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24.

### <a name="step-3"></a>Шаг 3.

```powershell
$subnet = $vnet.Subnets[0]
```

В этом примере назначает подсети hello объекта toovariable $subnet hello дальнейшими указаниями.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Создать общедоступный IP-адрес для интерфейса конфигурации hello

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

В этом примере создается открытому ресурсу IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США.

## <a name="create-an-application-gateway-configuration-object"></a>Создание объекта конфигурации шлюза приложений

### <a name="step-1"></a>Шаг 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Этот пример создает конфигурацию IP-адреса шлюза приложений с именем **gatewayIP01**. При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello. Помните, что для каждого экземпляра требуется отдельный IP-адрес.

### <a name="step-2"></a>Шаг 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

В этом примере настраивается hello серверной части IP-адресов с именем **pool01** с IP-адресами **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Эти значения являются hello IP-адресов, получения сетевого трафика hello, поступающие от hello переднего плана конечную точку IP. Замените hello IP-адресов из hello предшествующий пример hello IP-адреса вашего конечных точек веб-приложения.

### <a name="step-3"></a>Шаг 3.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

В этом примере настраиваются параметры шлюза приложения **poolsetting01** tooload трафика, обрабатываемого в пуле hello серверной части.

### <a name="step-4"></a>Шаг 4.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

В этом примере настраивается hello интерфейсный IP-порта с именем **frontendport01** для hello общедоступную конечную точку IP.

### <a name="step-5"></a>Шаг 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

В этом примере настраивается hello сертификат, используемый для подключения SSL. Hello сертификат должен toobe в формате PFX и hello пароль должен содержать от 4 too12 символов.

### <a name="step-6"></a>Шаг 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

В этом примере создается hello интерфейсный IP-конфигурации с именем **fipconfig01** и связывает hello общедоступный IP-адрес с hello интерфейсный IP-конфигурации.

### <a name="step-7"></a>Шаг 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

В этом примере создается имя прослушивателя hello **listener01** и связывает hello интерфейсный порт toohello интерфейса конфигурации IP и сертификат.

### <a name="step-8"></a>Шаг 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

В этом примере создается hello правило подсистемы балансировки нагрузки маршрутизации с именем **rule01** , предназначенный для настройки поведения подсистемы балансировки нагрузки hello.

### <a name="step-9"></a>Шаг 9.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

В этом примере настраивается hello размер экземпляра шлюза приложения hello.

> [!NOTE]
> Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10. Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium. Можно выбрать Standard_Small, Standard_Medium или Standard_Large.

### <a name="step-10"></a>Шаг 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Этот шаг определяет toouse политики hello SSL для шлюза приложения hello. Посетите [версии политики настройки SSL и комплектов шифров на использование шлюза приложений](application-gateway-configure-ssl-policy-powershell.md) toolearn дополнительные.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Создание шлюза приложений с помощью командлета New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

В этом примере создается шлюза приложения со всех элементов конфигурации из hello в предыдущих шагах. В примере hello называется шлюза приложения hello **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Получение DNS-имени шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS. tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello. [Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений. шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя. Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.


```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Дальнейшие действия

Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки (ILB), см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).

Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

