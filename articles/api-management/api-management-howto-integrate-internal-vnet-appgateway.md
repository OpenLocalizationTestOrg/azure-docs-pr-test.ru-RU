---
title: "aaaHow toouse управления API Azure в виртуальной сети со шлюзом приложений | Документы Microsoft"
description: "Узнайте, как toosetup и настройка службы управления API Azure в внутреннюю виртуальную сеть с помощью приложения шлюза (WAF) в качестве внешнего интерфейса"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Интеграция службы управления API во внутреннюю сеть со шлюзом приложений 

##<a name="overview"> </a> Обзор
 
Hello службы управления API можно настроить в виртуальной сети в режиме внутренней, который делает доступными только из hello виртуальной сети. Шлюз приложений Azure — это служба PaaS, выполняющая функции подсистемы балансировки нагрузки на сетевом уровне 7. Это служба обратного прокси-сервера, которая содержит также брандмауэр веб-приложения (WAF).

Объединение API управления подготовкой в внутренней виртуальной сети с сервера переднего плана для шлюза приложения hello обеспечивает hello следующие сценарии:

* Используйте hello же ресурсов API-Интерфейс управления для использования, потребители внутренних и внешних потребителей.
* Использовать один ресурс управления API, определив для него в службе управления API подмножество API-интерфейсов, доступных для внешних потребителей.
* Укажите способ под ключ tooswitch доступа tooAPI управления из hello общедоступный Интернет и отключать. 

##<a name="scenario"> </a> Сценарий
В этой статье будет охватывать как toouse единого управления API службы для внутренних и внешних потребителей и сделать ее выступать в качестве одного сервера переднего плана для обоих локальных и облачных API-интерфейсы. Также отображается как tooexpose только подмножество собственные интерфейсы API (в примере hello, они будут выделены зеленым цветом) для внешнего использования, с помощью hello PathBasedRouting функциональные возможности, доступные в шлюз приложений.

В первом примере установки hello все интерфейсы API можно управлять только с внутри виртуальной сети. Внутренние потребители (выделены оранжевым цветом) могут обращаться ко всем внутренним и внешним API. Трафик никогда не идет через цепи Express Route tooInternet доставки высокой производительности.

![Маршрут URL-адреса](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"> </a> Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. Создайте виртуальную сеть и отдельные подсети в ней для службы управления API и шлюза приложений. 
3. Если предполагается toocreate пользовательского DNS-сервера для hello виртуальной сети, сделать это перед началом развертывания hello. Проверьте ее работы за счет того, виртуальную машину, созданную в новую подсеть в hello виртуальной сети можно разрешить и открывать все конечные точки службы Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>Что такое необходимые toocreate интеграцию между API управления и шлюз приложений?

* **Пул серверных:** это hello внутренний виртуальный IP-адрес hello службы управления API.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры используются примененных tooall серверы в пуле hello.
* **Интерфейсный порт:** hello открытый порт, открытый для шлюза приложения hello. Трафик попадание он получает перенаправленный tooone hello внутренними серверами.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает пул серверных tooa прослушивателя.
* **Пользовательский зонд работоспособности:** шлюз приложений по умолчанию использует IP адрес на основе проб toofigure какие серверов в hello BackendAddressPool активны. Hello службы управления API отвечает только toorequests, имеющих правильный заголовок hello, поэтому пробы по умолчанию hello сбой. Зонд пользовательских работоспособности требуется toobe определенные toohelp шлюз приложений определить hello служба находится в активном состоянии и пересылать запросы.
* **Сертификат для пользовательского домена:** tooaccess управления API из hello Интернет необходимо toocreate сопоставление CNAME его имя узла toohello шлюз приложений интерфейса DNS-имя. Это обеспечивает hello заголовок узла и сертификат, отправленный tooApplication шлюза, который пересылается tooAPI управления, который APIM может распознать как допустимый.

## <a name="overview-steps"> </a> Действия по интеграции управления API со шлюзом приложений 

1. Создание группы ресурсов для диспетчера ресурсов.
2. Создайте виртуальную сеть, подсеть и общедоступный IP-адрес для шлюза приложения hello. Создайте еще одну подсеть для управления API.
3. Создать службу управления API внутри hello подсети виртуальной сети, созданной ранее и убедитесь, что используется внутренний режим hello.
4. Настройте пользовательское доменное имя hello в службе управления API hello.
5. Создайте объект конфигурации шлюза приложений.
6. Создайте ресурс шлюза приложений.
7. Создайте запись CNAME из hello открытому DNS-имени имя узла прокси-сервера управления API toohello шлюза приложения hello.

## <a name="create-a-resource-group-for-resource-manager"></a>Создание группы ресурсов для диспетчера ресурсов

Убедитесь, что используется последняя версия Azure PowerShell hello. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Шаг 1

Войдите в tooAzure

```powershell
Login-AzureRmAccount
```

Выполните аутентификацию со своими учетными данными.<BR>

### <a name="step-2"></a>Шаг 2

Проверьте hello подписки для учетной записи hello и выберите его.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Шаг 3.

Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Создание виртуальной сети и подсети для шлюза приложения hello

Hello в следующем примере показано, как toocreate виртуальной сети с помощью hello диспетчера ресурсов.

### <a name="step-1"></a>Шаг 1

Назначьте hello адрес диапазона 10.0.0.0/24 toohello подсети переменной toobe использовать для шлюза приложения при создании виртуальной сети.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Шаг 2

Назначьте hello адрес диапазона 10.0.1.0/24 toohello подсети переменной toobe используется для управления API при создании виртуальной сети.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Шаг 3.

Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **apim appGw группы Маршрутизации** для регионе hello Запад США, с помощью 10.0.0.0/16 hello префикс подсети 10.0.0.0/24 и 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Шаг 4.

Присвоить значение переменной подсети для получения дальнейших указаний hello

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Создание службы управления API в виртуальной сети, настроенной в режиме внутренней сети

Hello следующем примере показано, как toocreate службу управления API в виртуальной сети настроена только для внутренней.

### <a name="step-1"></a>Шаг 1
Создайте объект API управления виртуальной сети с помощью подсети hello $apimsubnetdata созданной выше.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Шаг 2
Создание службы управления API внутри hello виртуальной сети.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
После успешного завершения hello выше команда ссылаться слишком[tooaccess внутреннюю службу управления API виртуальной сети требуется настройки DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess его.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Настройка пользовательского доменного имени в службе управления API

### <a name="step-1"></a>Шаг 1
Отправьте hello сертификат с закрытым ключом для домена hello. В нашем примере это `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Шаг 2
После отправки сертификата hello создать объект конфигурации имя узла для hello прокси-сервера с именем узла из `api.contoso.net`, как сертификат пример hello обеспечивает полномочия для hello `*.contoso.net` домена. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Создать общедоступный IP-адрес для интерфейса конфигурации hello

Создание общих ресурсов IP **publicIP01** в группе ресурсов **apim appGw-RG** для региона hello Запад США.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

IP-адрес назначается шлюз приложений toohello при запуске службы hello.

## <a name="create-application-gateway-configuration"></a>Создание конфигурации шлюза приложений

Необходимо настроить все элементы конфигурации, перед созданием шлюза приложения hello. Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.

### <a name="step-1"></a>Шаг 1

Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**. При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello. Помните, что для каждого экземпляра требуется отдельный IP-адрес.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Шаг 2

Настройте hello интерфейсный IP-порт для hello общедоступную конечную точку IP. Это используется порт hello, конечные пользователи подключены.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Шаг 3.

Настройте интерфейсный IP hello общедоступную конечную точку IP.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Шаг 4.

Настройте сертификат hello для hello шлюз приложений, используемых toodecrypt и повторное шифрование трафика hello, проходящие через.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Шаг 5

Создайте прослушиватель HTTP hello для шлюза приложения hello. Назначьте hello интерфейсный IP-конфигурации, порта и tooit сертификат ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Шаг 6

Создать пользовательский зонд toohello службы управления API `ContosoApi` конечная точка прокси для домена. путь Hello `/status-0123456789abcdef` работоспособности конечной точки по умолчанию, размещенных на все службы управления API hello. Задать `api.contoso.net` как toosecure пользовательский зонд имя узла с помощью SSL-сертификат.

> [!NOTE]
> Здравствуйте, имя узла `contosoapi.azure-api.net` узла прокси-сервера по умолчанию hello настраивается при службы с именем `contosoapi` создается в открытый Azure. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Шаг 7

Отправьте сертификат hello toobe используется hello протокол SSL включен внутреннего пула ресурсов. Это hello же сертификат, который вы указали в шаге 4 выше.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Шаг 8

Серверная часть настройки для hello шлюз приложений HTTP. К настройкам относится и предел времени ожидания, по истечении которого запрос к внутренним серверам отменяется. Это значение отличается от времени ожидания проверки hello.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Шаг 9.

Настройка внутренней пул IP-адресов с именем **apimbackend** hello внутренний виртуальный IP-адрес службы управления API hello созданной выше.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Шаг 10

Создайте параметры для фиктивного (несуществующего) внутреннего пула. Пути tooAPI запросы, которые нам не нужно будет попаданий этой базы данных и возвращают 404 tooexpose из API управления через шлюз приложений.

Настройте параметры HTTP для внутреннего фиктивный hello.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Настройка фиктивный серверной **dummyBackendPool**, который указывает адрес полного доменного ИМЕНИ tooa **dummybackend.com**. Этот адрес полного доменного ИМЕНИ не существует в виртуальной сети hello.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Создать правило, установка этого hello, будет использовать шлюз приложения по умолчанию, указывающая серверной несуществующий toohello **dummybackend.com** в hello виртуальной сети.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Шаг 11

Настройте правило пути URL-адресов для пулов hello серверной части. Это позволяет, выбор только некоторые hello интерфейсы API управления API, предоставляемые toohello public. Например, из набора `Echo API` (/echo/), `Calculator API` (/calc/) и т. д. сделать доступным из Интернета только `Echo API`. 

Hello пример создает простое правило для hello «/ echo /» путь маршрутизации трафика toohello серверной части «apimProxyBackendPool».

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Если путь hello не соответствует пути hello правила мы хотим tooenable из системы управления API, путь конфигурации карты также настраивает пула адресов серверной части по умолчанию с именем правила hello **dummyBackendPool**. Например, http://api.contoso.net/calc/ * становится слишком**dummyBackendPool** как она определена в качестве пула по умолчанию hello несовпадающие трафика.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Hello выше шаг гарантирует только по запросу для hello путь «/ echo» разрешается доступ через шлюз приложения hello. Запросы tooother настроенного API-интерфейсов в API управления вызовет ошибки 404 из шлюза приложения, если доступ осуществляется из Интернета hello. 

### <a name="step-12"></a>Шаг 12

Создание параметра правила для hello шлюз приложений toouse URL-адрес на основе пути маршрутизации.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Шаг 13

Настройте hello число экземпляров и размер для шлюза приложения hello. Здесь мы используем hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) для повышения уровня безопасности hello ресурса управления API.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Шаг 14

Настройка WAF toobe в режиме «Защита».
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Создание шлюза приложений

Создание шлюза приложения со всеми объектами конфигурации hello из hello в предыдущих шагах.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>Запись CNAME hello API управления прокси-сервера имя узла toohello открытому DNS-имени hello ресурсов шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. При использовании общедоступных IP-адресов, шлюз приложений требуется динамически назначаемый имени DNS, которое может быть легко toouse. 

Hello шлюз приложений DNS-имя должно быть используется toocreate запись CNAME, которое указывает имя узла hello APIM прокси-сервера (например `api.contoso.net` в вышеприведенных примерах hello) toothis DNS-имя. tooconfigure hello интерфейсных IP запись CNAME, получить hello сведения о hello шлюз приложений и соответствующее IP или DNS-имя с помощью элемента PublicIPAddress hello. Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезапуске шлюза.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"> </a> Сводка
Управления API Azure, настроенные в виртуальной сети предоставляет интерфейс один шлюз для всех настроенных интерфейсов API, размещенной в локальной среде ли они в облаке hello. Интеграция шлюза приложений со службой управления API обеспечивает гибкость hello выборочного включения определенного toobe API-интерфейсы доступны на hello Интернета, а также предоставление брандмауэр веб-приложения как экземпляр интерфейса API управления tooyour переднего плана.

##<a name="next-steps"> </a> Дальнейшие действия
* Дополнительные сведения о шлюзе приложений Azure:
  * [Обзор шлюза приложений](../application-gateway/application-gateway-introduction.md)
  * [Application Gateway Web Application Firewall (preview)](../application-gateway/application-gateway-webapplicationfirewall-overview.md) (Брандмауэр веб-приложения шлюза приложений (предварительная версия))
  * [Создание шлюза приложений с помощью маршрутизации на основе пути](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* См. дополнительные сведения о службе управлении API и виртуальных сетях
  * [С помощью API управления доступен только в пределах hello виртуальной сети](api-management-using-with-internal-vnet.md)
  * [How to use Azure API Management with virtual networks](api-management-using-with-vnet.md) (Использование управления API Azure в виртуальных сетях)
