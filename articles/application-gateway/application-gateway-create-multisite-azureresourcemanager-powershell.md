---
title: "Шлюз приложений для размещения нескольких узлов aaaCreate | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, настройте шлюз приложения Azure для размещения нескольких веб-приложений на hello одного шлюза."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Создание шлюза приложений для размещения нескольких веб-приложений

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-multisite-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Размещение нескольких сайтов позволяет toodeploy более одного веб-приложения на hello же шлюз приложений. Он основывается на присутствие заголовка узла в hello входящего запроса HTTP, toodetermine прослушивателя, который будет получать трафик. затем Hello прослушиватель направляет трафик tooappropriate внутреннего пула, настроенным в определение правил hello hello шлюза. В веб-приложениях включен протокол SSL шлюз приложений зависит от hello Указание имени сервера (SNI) расширения toochoose hello правильный прослушивателя для hello веб-трафика. Обычно используются для размещения нескольких сайтов — tooload балансировать нагрузку по запросам для другом доменах toodifferent серверных пулов. Аналогичным образом несколько поддомены одного корневого домена также может быть размещена на приветствия hello же шлюз приложений.

## <a name="scenario"></a>Сценарий

В следующем примере hello, шлюз приложений обслуживает трафик для contoso.com и fabrikam.com с помощью двух серверных пулов: contoso пул серверов и fabrikam пул серверов. Аналогичную программу установки может быть поддомены toohost используется как app.contoso.com и blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. серверы Hello добавлены серверной части пула toouse toohello hello использование шлюза приложений должен существовать или либо в виртуальной сети hello в отдельной подсети или открытый IP/VIP-адрес, назначенный созданы их конечные точки.

## <a name="requirements"></a>Требования

* **Пул серверных:** hello список IP-адресов серверов hello серверной части. Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP. Можно также использовать полное доменное имя.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки). Для шлюзов приложений с поддержкой нескольких сайтов также добавляются имя узла и индикаторы SNI.
* **Правило:** правило hello привязывает hello прослушивателя, пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя. Правила обрабатываются в порядке hello, в котором они перечислены, а трафик будет направляться через hello первое подходящее правило вне зависимости от точности. Например при наличии правила с помощью базовых прослушивателя и правила с помощью прослушивателя несколькими сайтами обоих на hello же порт, правило hello с прослушивателя hello нескольких сайтов, необходимо указать перед hello правило с прослушивателем basic hello в порядке для hello toofunction правило нескольких сайтов, как ожидается.

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

представлены шаги hello нужен toocreate шлюза приложения Hello:

1. Создание группы ресурсов для диспетчера ресурсов.
2. Создание виртуальной сети, подсети и общедоступный IP-адрес для шлюза приложения hello.
3. Создание объекта конфигурации шлюза приложений.
4. Создание ресурса шлюза приложений.

## <a name="create-a-resource-group-for-resource-manager"></a>Создание группы ресурсов для диспетчера ресурсов

Убедитесь, что используется последняя версия Azure PowerShell hello. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Шаг 1

Войдите в tooAzure

```powershell
Login-AzureRmAccount
```
С помощью учетных данных, запрашиваемых tooauthenticate.

### <a name="step-2"></a>Шаг 2

Проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Шаг 3.

Выберите, какие toouse вашей подписки Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Шаг 4.

Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

В качестве альтернативы можно также создать теги группы ресурсов для шлюза приложений:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.

В приведенном выше примере hello, мы создали группу ресурсов под названием **appgw RG** с расположением **Запад США**.

> [!NOTE]
> Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md). Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).

## <a name="create-a-virtual-network-and-subnets"></a>Создание виртуальной сети и подсетей

Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов. На этом шаге создаются две подсети. для самого шлюза приложения hello — первая подсеть Hello. Шлюз приложений требуется собственный toohold подсети его экземпляров. В этой подсети могут развертываться только другие шлюзы приложений. второй подсеть Hello — используется toohold hello приложения внутренних серверов.

### <a name="step-1"></a>Шаг 1

Назначьте hello адрес диапазона 10.0.0.0/24 toohello подсети переменной toobe используется toohold hello шлюз приложений.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Шаг 2

Назначьте hello адрес диапазона 10.0.1.0/24 toohello подсети2 переменных toobe для hello внутренних пулов.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Шаг 3.

Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **appgw rg** для региона hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24, а 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Шаг 4.

Присвоить значение переменной подсети для hello дальнейшие действия, который создает шлюза приложения.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Создать общедоступный IP-адрес для интерфейса конфигурации hello

Создание общих ресурсов IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

IP-адрес назначается шлюз приложений toohello при запуске службы hello.

## <a name="create-application-gateway-configuration"></a>Создание конфигурации шлюза приложений

Перед созданием шлюза приложения hello имеют tooset копирование всех элементов конфигурации. Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.

### <a name="step-1"></a>Шаг 1

Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**. При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello. Помните, что для каждого экземпляра требуется отдельный IP-адрес.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Шаг 2

Настройка hello серверной части IP-адресов с именем **pool01** и **pool2** с IP-адресами **134.170.185.46**, **134.170.188.221**, **134.170.185.50** для **pool1** и **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  для **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

В этом примере существует два внутренней пулы tooroute трафика на основе hello запрошенного узла. Один пул принимает трафик от сайта contoso.com, а другой — от сайта fabrikam.com. У вас есть tooreplace hello, предшествующий IP адресов tooadd собственных конечных точек приложения IP адрес. Вместо внутренних IP-адресов для серверных экземпляров можно также использовать общедоступные IP-адреса, полное доменное имя или сетевую карту виртуальной машины. toospecify полных доменных имен, а не IP-адресов в PowerShell, используйте «-BackendFQDNs» параметра.

### <a name="step-3"></a>Шаг 3.

Настройка параметров шлюза приложения **poolsetting01** и **poolsetting02** hello балансировки нагрузки сетевого трафика в пуле hello серверной части. В этом примере вы настройки другой пул серверной части для пулов hello серверной части. Для каждого пула тыловых серверов параметры можно настроить отдельно.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Шаг 4.

Настройте интерфейсный IP hello общедоступную конечную точку IP.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Шаг 5

Настройте hello интерфейсный порт для шлюза приложения.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Шаг 6

Настройте два сертификата SSL для веб-сайтов hello двух мы будем toosupport в этом примере. Один сертификат является трафика contoso.com и fabrikam.com трафика hello других. Это должны быть сертификаты, выданные веб-сайтам центром сертификации. Самозаверяющие сертификаты поддерживаются, но их не рекомендуется использовать трафика в рабочих средах.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Шаг 7

Настройка двух прослушивателей для hello двух веб-сайтов в этом примере. Этот шаг позволяет настроить hello прослушиватели для открытого IP-адреса, порта и узла используется tooreceive входящего трафика. Параметр имени узла требуется для поддержки нескольких веб-узлов и toohello соответствующий набор веб-сайт, для которого hello трафика. Параметр RequireServerNameIndication должен быть установлен tootrue веб-сайтах, требуется поддержка протокола SSL в случае нескольких узлов. Если требуется поддержка протокола SSL, необходимо также toospecify hello SSL сертификат, используемый toosecure трафика для этого веб-приложения. сочетание Hello FrontendIPConfiguration, FrontendPort и имя узла должно быть уникальным tooa прослушивателя. Каждый прослушиватель может поддерживать один сертификат.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Шаг 8

Создайте два правила, задание для hello два веб-приложений в этом примере. Правило объединяет прослушиватели, серверные пулы и параметры протокола HTTP. Этот шаг позволяет настроить hello приложения шлюза toouse основные правила маршрутизации, один для каждого веб-сайта. Веб-сайт tooeach трафик полученных его настроенного прослушивателя и перенаправляться tooits настройки внутреннего пула, с помощью свойства hello, указанные в hello BackendHttpSettings.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Шаг 9.

Настройте hello число экземпляров и размер для шлюза приложения hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Создание шлюза приложений

Создание шлюза приложения со всеми объектами конфигурации из hello в предыдущих шагах.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Подготовка шлюза приложения — это длительная операция и может занять некоторое время toocomplete.
> 
> 

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

Узнайте, как tooprotect веб-сайты с [шлюз приложений - брандмауэр веб-приложения](application-gateway-webapplicationfirewall-overview.md)

