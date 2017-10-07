---
title: "брандмауэр веб-приложения aaaConfigure - шлюз приложений Azure | Документы Microsoft"
description: "Это статье предоставлены рекомендации по как с помощью toostart веб-приложение брандмауэра на шлюза существующего или нового приложения."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Настройка брандмауэра веб-приложения на новом или существующем шлюзе приложений

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Интерфейс командной строки Azure](application-gateway-web-application-firewall-cli.md)

Узнайте, как toocreate брандмауэр веб-приложения включено использование шлюза приложений или добавьте web приложение брандмауэра tooan существующий шлюз приложений.

Hello брандмауэр веб-приложения (WAF) в шлюз приложений Azure защищает веб-приложений из распространенных веб-атак, например путем внедрения кода SQL, атак с использованием межсайтовых сценариев и сеанса захвата.

Шлюз приложений — это балансировщик нагрузки уровня 7. Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной. Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д. Полный список поддерживаемых функций toofind посетите: [шлюза Обзор приложений](application-gateway-introduction.md).

Hello следующей статье показано, каким образом слишком[Добавить web приложение брандмауэра tooan существующий шлюз приложений](#add-web-application-firewall-to-an-existing-application-gateway) и [создания шлюза приложения, использующего брандмауэр веб-приложения](#create-an-application-gateway-with-web-application-firewall).

![Изображение для сценария][scenario]

## <a name="waf-configuration-differences"></a>Различия в конфигурации WAF

Если вы прочитали [Создание шлюза приложения с помощью PowerShell](application-gateway-create-gateway-arm.md), при создании шлюза приложения, понять tooconfigure параметры hello SKU. WAF предоставляет дополнительные параметры toodefine при настройке hello SKU для шлюза приложения. Отсутствуют дополнительные изменения, внесенные на сам шлюз приложения hello.

| **Параметр** | **Дополнительные сведения**
|---|---|
|**SKU** |Обычный шлюз приложений без WAF поддерживает размеры **Standard\_Small**, **Standard\_Medium** и **Standard\_Large**. С появлением hello WAF, приведены два дополнительных конфигураций, **WAF\_Средний** и **WAF\_большой**. WAF не поддерживается в шлюзах приложения уровня "Мелкий".|
|**Уровень** | Доступные значения Hello: **Стандартная** или **WAF**. При использовании брандмауэра веб-приложения требуется выбрать уровень **WAF**.|
|**Режим** | Этот параметр является режимом hello WAF. Допустимые значения: **Обнаружение** и **Предотвращение**. Если WAF работает в режиме обнаружения, все угрозы заносятся в файл журнала. В режиме защиты от по-прежнему регистрируются события, но hello злоумышленник получит 403 несанкционированного ответ от hello шлюз приложений.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Добавить web приложение брандмауэра tooan существующего шлюза приложений

Убедитесь, что используется последняя версия Azure PowerShell hello. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

1. Войдите в учетную запись Azure tooyour.

    ```powershell
    Login-AzureRmAccount
    ```

2. Выберите toouse hello подписку для этого сценария.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Получить hello шлюза, который вы добавляете брандмауэр веб-приложения для.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Настройте приложение брандмауэра hello web sku. Доступные размеры Hello **WAF\_большой** и **WAF\_Средний**. Если используется брандмауэр веб-приложения hello уровня должен быть **WAF**, необходимо подтвердить hello емкости при задании номера sku hello.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Настройте параметры hello WAF, как определено в следующий пример hello.

   Для **FirewallMode**, hello доступные значения: Предотвращение и обнаружения.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Замена hello шлюза приложения hello параметры, определенные в предыдущих шага hello.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Эта команда обновляет hello шлюз приложений брандмауэр веб-приложения. Посетите [диагностику шлюза приложения](application-gateway-diagnostics.md) toounderstand как tooview журналы для шлюза приложения. Из-за особенностей безопасности toohello WAF toobe необходимость журналы регулярно контролировать состояние безопасности hello toounderstand веб-приложений.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Создание шлюза приложений с брандмауэром веб-приложения

Hello следующие шаги помогут выполнить весь процесс hello из начала tooend для создания шлюза приложения с помощью брандмауэр веб-приложения.

Убедитесь, что используется последняя версия Azure PowerShell hello. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

1. Войдите в tooAzure, запустив `Login-AzureRmAccount`, являются tooauthenticate запрос с учетными данными.

1. Проверьте hello подписки для учетной записи hello, выполнив команду`Get-AzureRmSubscription`

1. Выберите, какие toouse вашей подписки Azure.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов для шлюза приложения hello.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды, которые использует toocreate объект шлюза приложения hello одну группу ресурсов.

В предыдущих пример hello мы создали группу ресурсов под названием «Appgw RG» и расположение «Западная часть США.»

> [!NOTE]
> Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md). Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).

### <a name="configure-virtual-network"></a>Настройка виртуальной сети

Шлюзу приложений требуется собственная подсеть. На этом шаге создается виртуальная сеть с адресным пространством 10.0.0.0/16 и две подсети: для шлюза приложения hello и для внутренних членов пула.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Настройка диапазонов общедоступных IP-адресов

В порядке toohandle внешние запросы шлюз приложений требуется общедоступный IP-адрес. Этот общедоступный IP-адрес не должен иметь `DomainNameLabel` определенные toobe используемые hello шлюз приложений.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Настройка шлюза приложения hello

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Шлюзы приложений, созданных с помощью конфигурации брандмауэра hello основные веб-приложений, настроенных с CRS 3.0 для защиты.

## <a name="get-application-gateway-dns-name"></a>Получение DNS-имени шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS. tooensure конечным пользователям возможность нажать hello шлюза приложения, запись CNAME может быть используется toopoint toohello общедоступная конечная точка hello шлюз приложений. [Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure псевдоним, получить сведения о hello шлюз приложений и соответствующее IP или DNS-имя с помощью hello PublicIPAddress вложен toohello шлюз приложений. Шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя. Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.

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

Узнайте, как ведение журнала диагностики tooconfigure, toolog hello события, которые обнаружены или предотвратить брандмауэр веб-приложения, посетив [диагностики шлюза приложений](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
