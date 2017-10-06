---
title: "конец aaaConfigure tooend SSL со шлюзом приложения Azure | Документы Microsoft"
description: "В этой статье описывается, как tooconfigure завершить tooend SSL со шлюзом приложений с помощью PowerShell диспетчера ресурсов Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Настройка конечного tooend SSL с помощью шлюза приложения с помощью PowerShell

## <a name="overview"></a>Обзор

Приложение поддерживает шлюза последний tooend шифрования трафика. Шлюз приложений делает это путем прерывания hello соединение SSL на шлюз приложения hello. шлюз Hello затем применяет правила маршрутизации hello трафика toohello повторно шифрует пакет приветствия и переадресует hello пакетов toohello соответствующие базы данных на основе определенных правил маршрутизации hello. Любой ответ с веб-сервера hello проходит через hello же процесс обратной toohello конечного пользователя.

Еще одна поддерживаемая шлюзом приложений функция — отключение определенных версий протокола SSL. Шлюз приложений поддерживает отключение hello следующая версия протокола; **TLSv1.0**, **TLSv1.1**, и **TLSv1.2** также определение hello наборы toouse и hello порядок приоритета шифра.  Посетите toolearn Дополнительные сведения о настраиваемых параметров SSL [Общие сведения о политике SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> Протоколы SSL 2.0 и SSL 3.0 отключены по умолчанию, и их нельзя включать. Они рассматриваются как небезопасные и не может toobe при использовании шлюза приложений.

![Изображение для сценария][scenario]

## <a name="scenario"></a>Сценарий

В этом сценарии вы узнаете toocreate шлюза приложения с помощью конечного tooend SSL с помощью PowerShell.

Вы узнаете:

* как создать группу ресурсов **appgw-rg**;
* как создать виртуальную сеть **appgwvnet** с адресным пространством 10.0.0.0/16;
* как создать две подсети, **appgwsubnet** и **appsubnet**;
* Создайте небольшое приложение шлюза вспомогательные окончания tooend SSL-шифрование, ограничения версии протокола SSL и комплекты шифров.

## <a name="before-you-begin"></a>Перед началом работы

tooconfigure окончания tooend SSL со шлюзом приложений, требуется сертификат для шлюза hello и сертификаты необходимы для hello внутренних серверов. сертификат шлюза Hello — используется tooencrypt и расшифровки hello трафик tooit с помощью протокола SSL. сертификат шлюза Hello должен toobe в формате обмена личной информацией (pfx). Этот формат позволяет для hello закрытого ключа toobe экспортированы, необходимые для hello приложения шлюза tooperform hello шифрованием/дешифрованием трафика.

Для end серверной hello шифрования SSL tooend необходимо включить в список разрешенных со шлюзом приложений. Это делается путем передачи hello сертификат с открытым toohello приложения hello серверных системах шлюза. Это гарантирует, что этот шлюз приложения hello взаимодействует только с экземпляров известных серверной части. Это дополнительно защищает hello tooend обмен данных.

Этот процесс описан в hello следующие шаги:

## <a name="create-hello-resource-group"></a>Создание группы ресурсов hello

В этом разделе описывается создание группы ресурсов, содержащий шлюза приложения hello.

### <a name="step-1"></a>Шаг 1

Войдите в учетную запись Azure tooyour.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Шаг 2

Выберите toouse hello подписку для этого сценария.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Шаг 3.

Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Создание виртуальной сети и подсети для шлюза приложения hello

Hello пример создает виртуальную сеть и две подсети. Одна подсеть — шлюз приложений используется toohold hello. Hello других подсеть используется для веб-приложения hello серверных системах размещения hello.

### <a name="step-1"></a>Шаг 1

Назначьте диапазон адресов для подсети hello использоваться для самого шлюза приложения hello.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Подсети, настроенные для шлюза приложений, должны иметь соответствующий размер. Шлюз приложений можно настроить для копирования too10 экземпляров. Каждый экземпляр имеет один IP-адрес из подсети hello. Слишком маленький размер подсети может отрицательно сказаться на возможности масштабирования шлюза приложений.
> 
> 

### <a name="step-2"></a>Шаг 2

Назначьте toobe диапазон адресов для пула адресов серверной части hello.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Шаг 3.

Создайте виртуальную сеть с подсетями hello, определенные в предыдущих шагах hello.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Шаг 4.

Получить hello виртуального сетевого ресурса и подсети ресурсы toobe используется в hello следующие шаги:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Создать общедоступный IP-адрес для интерфейса конфигурации hello

Создание общих ресурсов toobe IP, используемая для шлюза приложения hello. Этот общедоступный IP-адрес используется на следующем шаге.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Шлюз приложений не поддерживает использование hello общедоступный IP-адрес создан с метками домена. Поддерживается только общедоступный IP-адрес с динамически создаваемой меткой домена. Если требуется понятное DNS-имени для шлюза приложения hello, рекомендуется записать toouse запись CNAME в качестве псевдонима.

## <a name="create-an-application-gateway-configuration-object"></a>Создание объекта конфигурации шлюза приложений

Перед созданием шлюза приложения hello устанавливаются все элементы конфигурации. Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.

### <a name="step-1"></a>Шаг 1

Создайте шлюз IP-адрес приложения, этот параметр позволяет указать, какие шлюз подсети hello приложением. При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и направляет сетевой трафик toohello IP-адресов в пул IP-адресов серверной части hello. Помните, что для каждого экземпляра требуется отдельный IP-адрес.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Шаг 2

Создайте интерфейсный IP-конфигурации, этот параметр сопоставляет частные или общедоступные ip адрес toohello интерфейсную шлюза приложения hello. Привет, даст связывает hello общедоступный IP-адрес в hello предыдущих шага с hello интерфейсный IP-конфигурации.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Шаг 3.

Настройте пул IP-адресов hello серверной части с IP-адресами hello hello серверной части веб-серверов. Эти IP-адреса являются hello IP-адресов, получения сетевого трафика hello, поступающие от hello переднего плана конечную точку IP. Замените следующие IP адресов tooadd hello собственных конечных точек приложения IP адрес.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Полное доменное имя (FQDN) также является допустимым значением вместо IP-адрес для hello внутренних серверов с помощью параметра - BackendFqdns hello. 

### <a name="step-4"></a>Шаг 4.

Настройте hello интерфейсный IP-порт для hello общедоступную конечную точку IP. Это используется порт hello, конечные пользователи подключены.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Шаг 5

Настройка hello сертификата для шлюза приложения hello. Этот сертификат используется toodecrypt и повторное шифрование трафика hello для шлюза приложения hello.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> В этом примере настраивается hello сертификат, используемый для подключения SSL. Hello сертификат должен toobe в формате PFX и hello пароль должен содержать от 4 too12 символов.

### <a name="step-6"></a>Шаг 6

Создайте прослушиватель HTTP hello для шлюза приложения hello. Назначьте hello интерфейсный IP-конфигурации, порта и toouse сертификат SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Шаг 7

Отправьте сертификат hello toobe на hello SSL с включенной внутреннего пула ресурсов.

> [!NOTE]
> проба по умолчанию Hello возвращает hello открытый ключ из hello **по умолчанию** SSL-привязку IP-адрес hello серверной части и сравнивает hello значение открытого ключа получит toohello значение открытого ключа здесь. Hello извлечь открытый ключ, не обязательно сайта toowhich hello предназначен трафик, поступающий **Если** использовании заголовков узлов и SNI на внутреннем hello. Если вы сомневаетесь, посетите https://127.0.0.1/ на сертификат, используемый для hello tooconfirm заканчивается обратной hello **по умолчанию** SSL-привязки. Используйте hello открытого ключа из запроса в этом разделе. Если вы используете заголовки узлов и SNI на HTTPS-привязки и вы не получите ответ и сертификат из toohttps://127.0.0.1/ запрос вручную браузера на задний план hello-элементах, необходимо настроить привязку SSL по умолчанию на задний план hello-элементах. Если это не так, зонды ошибкой и серверной части hello отсутствует в списке разрешений.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> сертификат Hello, делается на этом шаге, должен быть открытый ключ сертификата pfx hello на серверной hello hello. Экспорт hello (не hello корневому сертификату) установлен на центральном сервере hello в. CER отформатировать и использовать его на этом шаге. Этот шаг запрещенного hello серверной со шлюзом приложения hello.

### <a name="step-8"></a>Шаг 8

Настройте hello шлюз http серверной части. Назначение сертификата hello, переданных в предыдущих параметров http toohello шаг hello.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Шаг 9.

Создание маршрута правило подсистемы балансировки нагрузки, предназначенный для настройки поведения подсистемы балансировки нагрузки hello. В этом примере создается базовое правило с циклическим перебором.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Шаг 10

Настройте размер экземпляра hello шлюза приложения hello.  Доступные размеры Hello, **Стандартная\_небольшой**, **Стандартная\_Средний**, и **Стандартная\_большой**.  Ресурсы hello доступные значения: от 1 до 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Для тестирования можно выбрать число экземпляров, равное 1. Очень важно, tooknow, что любой экземпляр подсчет в двух экземпляров не распространяется действие соглашения об уровне ОБСЛУЖИВАНИЯ hello и поэтому не рекомендуется. Небольшой шлюзы, toobe, используемые для разработки тестирования и не в производственных целях.

### <a name="step-11"></a>Шаг 11

Настройка политики toobe hello SSL, использовать для шлюза приложения hello. Шлюз приложений поддерживает возможность hello tooset минимальную версию для версии протокола SSL.

Hello следующие значения: список версий протокола, которые могут быть определены.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Задает hello минимальное семейству слишком**TLSv1_2** и позволяет **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**и **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** только.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Создать hello шлюза приложений

Используя все hello в предыдущих шагах, создайте hello шлюз приложений. Создание Hello hello шлюза — длительного процесса.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Ограничение версий протокола SSL на существующем шлюзе приложений

Hello описанные выше шаги, чтобы перейти по созданию приложения с конечным tooend SSL и отключение определенных версий протокола SSL. Hello следующий пример отключает определенные политики SSL для существующего шлюза приложения.

### <a name="step-1"></a>Шаг 1

Получить tooupdate шлюза приложения hello.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Шаг 2

Определите политику SSL. В следующем примере hello, TLSv1.0 TLSv1.1 отключены и hello шифров **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, и  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** являются только hello.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Шаг 3.

Наконец обновление шлюза hello. Это важные toonote, что последний шаг является длительных задач. При завершении его окончания tooend SSL настраивается на шлюз приложения hello.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Дополнительные сведения о Усиление защиты hello безопасности веб-приложений с брандмауэр веб-приложения через шлюз приложения, посетив [Обзор брандмауэра веб-приложения](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
