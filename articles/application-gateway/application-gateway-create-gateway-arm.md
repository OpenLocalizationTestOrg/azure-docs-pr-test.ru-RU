---
title: "aaaCreate и управления ими шлюза приложения Azure — PowerShell | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, Настройка, запуск и удалить шлюз приложения Azure с помощью диспетчера ресурсов Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a>Создание, запуск или удаление шлюза приложений с помощью диспетчера ресурсов Azure

> [!div class="op_single_selector"]
> * [портал Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-gateway-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-gateway.md)
> * [Шаблон диспетчера ресурсов Azure](application-gateway-create-gateway-arm-template.md)
> * [Интерфейс командной строки Azure](application-gateway-create-gateway-cli.md)

Шлюз приложений — это балансировщик нагрузки уровня 7. Он предоставляет отработки отказа и маршрутизации производительности HTTP-запросов между различными серверами, являются ли они на hello облачной или локальной. Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д. Полный список поддерживаемых функций toofind посетите [Обзор шлюза приложения](application-gateway-introduction.md).

В этой статье рассматриваются действия toocreate hello, Настройка, запуск и удалить шлюз приложения.

> [!IMPORTANT]
> Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчер ресурсов и классическом. Внимательно изучите [модели и средства развертывания](../azure-classic-rm.md), прежде чем начинать работать с любыми ресурсами Azure. Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи. В этом документе рассматривается создание шлюза приложений с помощью Azure Resource Manager. классической версии hello toouse go слишком[создать шлюз классического развертывания приложения с помощью PowerShell](application-gateway-create-gateway.md).

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
1. При наличии существующей виртуальной сети, выберите существующую пустую подсеть или создать подсеть в существующей виртуальной сети для использования исключительно шлюзом приложения hello. Невозможно развернуть hello приложения шлюза tooa другую виртуальную сеть чем hello ресурсы предполагается toodeploy за шлюза приложения hello.
1. должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Что такое необходимые toocreate шлюза приложения

* **Внутренний пул сервера:** список hello IP адресов, полных доменных имен или сетевых адаптеров hello внутренних серверов. При использовании IP-адреса, они должны принадлежать либо к подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.
* **Параметры пула внутренних серверов:** каждый пул имеет такие параметры, как порт, протокол и соответствие на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту и затем получает перенаправленный tooone hello внутренних серверов.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает hello прослушивателя, hello внутреннего сервера пула и определяет, какой трафик hello внутреннего пула сервера должен быть расширенный toowhen попадании конкретного прослушивателя.

## <a name="create-a-resource-group-for-resource-manager"></a>Создание группы ресурсов для диспетчера ресурсов

Убедитесь, что используется последняя версия Azure PowerShell hello. Дополнительные сведения см. в статье [Использование Windows PowerShell с диспетчером ресурсов](../powershell-azure-resource-manager.md).

1. Войдите в tooAzure и введите свои учетные данные.

  ```powershell
  Login-AzureRmAccount
  ```

2. Проверьте hello подписки для учетной записи hello.

  ```powershell
  Get-AzureRmSubscription
  ```

3. Выберите, какие toouse вашей подписки Azure.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. Создайте группу ресурсов. Если вы используете существующую группу, пропустите этот шаг.

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды toocreate, использует шлюз приложений hello таким же группе ресурсов.

В приведенном выше примере hello, мы создали группу ресурсов под названием **ContosoRG** и расположение **Восток США**.

> [!NOTE]
> Если вам требуется пользовательский зонд tooconfigure для шлюза приложения, посетите: [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-ps.md). Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).


## <a name="create-hello-application-gateway-configuration-objects"></a>Создание шлюза приложения hello объекты конфигурации

Необходимо настроить все элементы конфигурации, перед созданием шлюза приложения hello. Hello следующие действия создадут hello элементы конфигурации, которые необходимы для ресурса шлюза приложения.

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

По завершении получить сведения о DNS и виртуальный IP-адрес шлюза приложения hello из hello открытый IP-ресурс toohello вложенного приложения шлюза.

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a>Удалить шлюз приложения hello

Hello следующий пример удаляет шлюз приложения hello.

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> Hello **-принудительно** коммутатор может быть сообщение с подтверждением remove используется toosuppress hello.

tooverify, hello службы были удалены, вы можете использовать hello `Get-AzureRmApplicationGateway` командлета. Этот шаг не является обязательным.

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a>Получение DNS-имени шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS. tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello. toodo сведения, получение шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений. Это можно сделать с помощью Azure DNS или других поставщиков DNS, при создании записи CNAME, точек toohello [общедоступный IP-адрес](../dns/dns-custom-domain.md#public-ip-address). Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.

> [!NOTE]
> IP-адрес назначается шлюз приложений toohello при запуске службы hello.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a>Удаление всех ресурсов

toodelete все ресурсы, созданные в этой статье завершения hello следующий шаг:

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a>Дальнейшие действия

Если вы хотите tooconfigure разгрузки SSL, посетите: [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).

Если вы хотите tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, посетите: [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).

Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)
