---
title: "правила с помощью маршрутизации URL-адрес шлюза приложения aaaCreate | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, настройте шлюз приложения Azure с помощью правила маршрутизации URL-адрес"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Создание шлюза приложений с помощью маршрутизации на основе пути

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

Маршрутизация URL-адрес на основе пути позволяет вам tooassociate маршрутов на основе hello пути URL-адреса HTTP-запроса. Он проверяет, существует ли пул серверной части tooa маршрута, настроенный для hello URL-адрес, представленных в hello шлюз приложений. После этого он отправляет hello сетевой трафик toohello определенного пула серверной части. Обычно используются для маршрутизации на основе URL-адрес — tooload балансировать нагрузку по запросам для различных типов содержимого toodifferent серверных пулов.

Маршрутизация на основе URL-адрес появился новый шлюз tooapplication тип правила. Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути. Основное правило тип предоставляет циклического службы для внутреннего интерфейса hello пулов при PathBasedRouting Кроме распространения tooround циклический перебор, также учитывает шаблон пути URL-адреса запроса hello при выборе hello внутренний пул.

## <a name="scenario"></a>Сценарий

В следующем примере hello, шлюз приложений обслуживает трафика для contoso.com с помощью двух серверных пулов: видео сервера пул и пул серверов изображения.

Запросы на http://contoso.com/image * направляются в пул серверов tooimage (pool1) и http://contoso.com/video * направляются пул серверов toovideo (pool2). Если ни один из шаблонов путей hello соответствует выбирается пула сервера по умолчанию (pool1).

![Маршрут URL-адреса](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. Создайте виртуальную сеть и подсеть для шлюза приложений. Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети. шлюз приложения Hello должен быть сам по себе в подсети виртуальной сети.
3. серверы Hello добавлены серверной части пула toouse toohello hello использование шлюза приложений должен существовать или в виртуальной сети hello или открытый IP/VIP-адрес, назначенный созданы их конечные точки.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Что такое необходимые toocreate шлюза приложения

* **Пул серверных:** hello список IP-адресов серверов hello серверной части. Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает hello прослушивателя, пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

Hello различие между использованием классический Azure и Azure Resource Manager — создать шлюз приложения hello и hello элементы, которые должны toobe настроить порядок hello.

С помощью диспетчера ресурсов все элементы, которые делают шлюза приложения настраиваются отдельно, а затем указать ресурс шлюза приложения hello toocreate.

Ниже приведены шаги hello, необходимые toocreate шлюз приложений.

1. Создание группы ресурсов для диспетчера ресурсов.
2. Создайте виртуальную сеть, подсеть и общедоступный IP-адрес для шлюза приложения hello.
3. Создание объекта конфигурации шлюза приложений.
4. Создание ресурса шлюза приложений.

## <a name="create-a-resource-group-for-resource-manager"></a>Создание группы ресурсов для диспетчера ресурсов

Убедитесь, что используется последняя версия Azure PowerShell hello. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Шаг 1

Войдите в tooAzure

```powershell
Login-AzureRmAccount
```

С помощью учетных данных, запрашиваемых tooauthenticate.<BR>

### <a name="step-2"></a>Шаг 2

Проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Шаг 3.

Выберите, какие toouse вашей подписки Azure. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Шаг 4.

Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

В качестве альтернативы можно также создать теги группы ресурсов для шлюза приложений:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Эта группа ресурсов используются как расположение по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды toocreate hello использование шлюза приложений одну группу ресурсов.

В приведенном выше примере hello мы создали группу ресурсов под названием «appgw RG» и расположение «West US».

> [!NOTE]
> Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md). Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Создание виртуальной сети и подсети для шлюза приложения hello

Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов. В этом примере создается виртуальная сеть для шлюза приложения hello. Шлюз приложений требуется собственный подсети по этой причине hello подсети для шлюза приложения hello меньше, чем hello адресное пространство виртуальной сети. Это обеспечивает другие ресурсы, включая, но не только tooweb toobe серверы настроить в hello же виртуальной сети.

### <a name="step-1"></a>Шаг 1

Назначьте hello диапазон адресов 10.0.0.0/24 toohello подсети переменной toobe используется toocreate виртуальной сети.  Это создает hello объекта конфигурации подсети для шлюза приложения, который используется в следующем примере hello hello.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Шаг 2

Создайте виртуальную сеть с именем **appgwvnet** в группе ресурсов **appgw rg** для региона hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24. Это завершает конфигурацию hello hello виртуальную сеть с одной подсетью для hello tooreside шлюз приложений.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Шаг 3.

Присвойте переменной hello подсети для hello дальнейшие действия, он передается toohello `New-AzureRMApplicationGateway` командлета на следующем шаге.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Создать общедоступный IP-адрес для интерфейса конфигурации hello

Создание общих ресурсов IP **publicIP01** в группе ресурсов **appgw rg** для региона hello Запад США. Шлюз приложений можно использовать общедоступный IP-адрес, внутренний IP-адрес или обоих запросов tooreceive для балансировки нагрузки.  В этом примере используется общедоступный IP-адрес. В следующем примере hello имя DNS не настраивается для создания hello общедоступный IP-адрес.  Шлюз приложений не поддерживает пользовательские DNS-имена в общедоступных IP-адресах.  Если пользовательское имя является обязательным для hello общедоступную конечную точку, запись CNAME должны создаваться toopoint toohello автоматически создается DNS-имя для hello общедоступный IP-адрес.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

IP-адрес назначается шлюз приложений toohello при запуске службы hello.

## <a name="create-application-gateway-configuration"></a>Создание конфигурации шлюза приложений

Необходимо настроить все элементы конфигурации, перед созданием шлюза приложения hello. Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.

### <a name="step-1"></a>Шаг 1

Создайте конфигурацию IP-адресов шлюза приложений с именем **gatewayIP01**. При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello. Помните, что для каждого экземпляра требуется отдельный IP-адрес.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Шаг 2

Настройка hello серверной части IP-адресов с именем **pool01** и **pool2** с IP-адреса для **pool1** и **pool2**. Эти IP-адреса — hello IP-адреса ресурсов hello, размещающие приложения hello web toobe с защищен шлюза приложения hello. Эти члены пула серверной части являются все проверенные toobe зонды работоспособности как основные проверки, так и пользовательские зонды.  Трафик направляется toothem при поступлении запросов на шлюз приложения hello. Внутренние пулы может использоваться несколько правил в шлюза приложения hello, что означает один внутренний пул может использоваться для нескольких веб-приложений, которые располагаются на hello таким же узла.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

В этом примере существует два внутренней пулы tooroute трафика на основе hello URL-адрес. Один пул принимает трафик для URL-пути /video, а другой — для пути /image. Замените hello, предшествующий IP адресов tooadd собственных конечных точек приложения IP адрес. 

### <a name="step-3"></a>Шаг 3.

Настройка параметров шлюза приложения **poolsetting01** и **poolsetting02** hello балансировки нагрузки сетевого трафика в пуле hello серверной части. В этом примере вы настройки другой пул серверной части для пулов hello серверной части. Для каждого пула тыловых серверов параметры можно настроить отдельно.  Параметры HTTP серверной используются членами правила tooroute трафика toohello правильный внутренний пул. Определяет hello протокол и порт, используемый при отправке трафика члены пула toohello серверной части. Сеансы на основе файлов cookie, также определяются hello параметров серверного HTTP.  Если параметр включен, сходство сеансов на основе файлов cookie отправляет трафик toohello один внутренний как предыдущие запросы для каждого пакета.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Шаг 4.

Настройте интерфейсный IP hello общедоступную конечную точку IP. Hello интерфейсный IP конфигурации используется объект hello toorelate прослушивателя наружу с выходом IP-адрес с hello прослушивателя.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Шаг 5

Настройте hello интерфейсный порт для шлюза приложения. Объект конфигурации Hello интерфейсный порт используется toodefine прослушивателя что порт прослушивает трафик через прослушиватель hello шлюза приложения hello.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Шаг 6

Настройте прослушиватель hello. Этот шаг позволяет настроить прослушиватель hello hello общедоступный IP-адрес и порт, используемый tooreceive входящего сетевого трафика. Следующий пример Hello принимает hello ранее настроен интерфейсный IP-конфигурации, конфигурацию интерфейсный порт и протокол (http или https) и настраивает hello прослушивателя. В этом примере hello прослушиватель tooHTTP трафик через порт 80 на hello общедоступный IP-адрес, который был создан ранее.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Шаг 7

Настройте правило пути URL-адресов для пулов hello серверной части. Этот шаг настраивает hello относительный путь, используемый шлюзом приложения и определяет сопоставление hello hello URL-адрес и hello внутренней пул, назначенный toohandle hello входящего трафика.

> [!IMPORTANT]
> Каждый путь должен начинаться с / и hello единственное место «\*» допускается, находится в конце hello. Примеры допустимых значений: /xyz, /xyz* или /xyz/*. Hello строка переданы сопоставителе toohello путь не содержит текст после hello сначала «?» или «#» и эти знаки не допускаются. 

Hello в примере создаются два правила: одно для маршрутизации путь «/ изображения /» трафик tooback-end «pool1» и еще один — для маршрутизации трафика tooback-end «pool2.» путь «/ видео и» Эти правила убедитесь, что трафик для каждого набора URL-адресов серверной части перенаправленного toohello. Например http://contoso.com/image/figure1.jpg переходит toopool1 и http://contoso.com/video/example.mp4 становится toopool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Если путь hello не соответствует ни одному из правил предопределенный путь hello, hello правило пути карты конфигурация также настраивает пул адресов серверной части по умолчанию. Например http://contoso.com/shoppingcart/test.html переходит toopool1 как она определена в качестве пула по умолчанию hello для несопоставленных трафика.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Шаг 8

Создайте параметр правила. Этот шаг позволяет настроить hello приложения шлюза toouse маршрутизация URL-адресов на основе пути. Hello `$urlPathMap` переменная, определенная в hello ранее является сейчас используется toocreate hello правила на основе пути. На этом шаге мы связать правило hello прослушивателя и сопоставление пути URL-адрес hello, созданного ранее.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Шаг 9.

Настройте hello число экземпляров и размер для шлюза приложения hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Создание шлюза приложений

Создание шлюза приложения со всеми объектами конфигурации из hello в предыдущих шагах.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Получение DNS-имени шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS. tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello. [Настройка пользовательского имени домена в Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure hello интерфейсных IP запись CNAME, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений. шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME. Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.

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

Если toolearn разгрузки Secure Sockets Layer (SSL), см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl-arm.md).

