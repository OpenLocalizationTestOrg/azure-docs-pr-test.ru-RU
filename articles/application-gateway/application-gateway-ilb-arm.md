---
title: "aaaUsing шлюза приложения Azure с внутренним балансировщиком нагрузки - PowerShell | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, Настройка, запуск и удалить шлюз приложения Azure с внутренней подсистемы балансировки нагрузки (ILB) для диспетчера ресурсов Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Создание шлюза приложений с внутренним балансировщиком нагрузки (ILB) с помощью диспетчера ресурсов Azure

> [!div class="op_single_selector"]
> * [Классическая модель — Azure PowerShell](application-gateway-ilb.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-ilb-arm.md)

Шлюз приложения Azure можно настроить для виртуальных IP-адресов из Интернета или с внутренней конечной точки, не предоставляемых toohello Интернета, также называется конечной точкой (ILB) балансировщик внутренней нагрузки. Настройка шлюза hello с ILB полезен для внутренних бизнес-приложений, не предоставляемых toohello Интернета. Также полезно для служб и уровни в многоуровневое приложение, располагаются в пределах границ безопасности, не предоставляемых toohello Internet, но по-прежнему требуется циклическое загрузить распространения, stickiness сеанса или завершение Secure Sockets Layer (SSL).

В этой статье рассматриваются действия hello tooconfigure шлюза приложения с ILB.

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. Вы создадите виртуальную сеть и подсеть для шлюза приложений. Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети. Сам шлюз приложений должен находиться в подсети виртуальной сети.
3. должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Что такое необходимые toocreate шлюза приложения

* **Пул серверных:** hello список IP-адресов серверов hello серверной части. Hello IP-адресов в списке должны либо относятся toohello виртуальной сети, но в другой подсети для шлюза приложения hello или должен быть открытый IP-адрес или VIP.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, они зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя. В настоящее время только hello *основные* правило поддерживается. Hello *основные* правило — распределение нагрузки с циклическим перебором.

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

Hello различие между использованием классический Azure и Azure Resource Manager — создать шлюз приложения hello и hello элементы, которые должны toobe настроить порядок hello.
С помощью диспетчера ресурсов все элементы, которые делают шлюза приложения настроен по отдельности, а затем указать ресурс шлюза приложения hello toocreate.

Ниже приведены шаги hello, необходимые toocreate шлюз приложений.

1. Создание группы ресурсов для диспетчера ресурсов
2. Создание виртуальной сети и подсети для шлюза приложения hello
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

Создайте группу ресурсов (если вы используете существующую группу, пропустите этот шаг).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов. Убедитесь, что все команды toocreate, использует шлюз приложений hello таким же группе ресурсов.

В предыдущих пример hello мы создали группу ресурсов под названием «Appgw rg» и расположение «West US».

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Создание виртуальной сети и подсети для шлюза приложения hello

Следующий пример показывает как Hello toocreate виртуальной сети с помощью диспетчера ресурсов:

### <a name="step-1"></a>Шаг 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Этот шаг назначает hello диапазон адресов 10.0.0.0/24 tooa подсети переменной toobe используется toocreate виртуальной сети.

### <a name="step-2"></a>Шаг 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Этот шаг создает виртуальную сеть с именем «appgwvnet» в ресурс группы «appgw-rg» для области hello Запад США, с 10.0.0.0/16 hello префикс подсети 10.0.0.0/24.

### <a name="step-3"></a>Шаг 3.

```powershell
$subnet = $vnet.subnets[0]
```

Этот шаг назначает подсети hello объекта toovariable $subnet hello дальнейшими указаниями.

## <a name="create-an-application-gateway-configuration-object"></a>Создание объекта конфигурации шлюза приложений

### <a name="step-1"></a>Шаг 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

На этом шаге создается конфигурация IP-адреса шлюза приложений с именем gatewayIP01. При запуске шлюза приложения, он принимает IP-адрес из подсети hello настроен и маршрутизацию сетевого трафика toohello IP-адресов в пул IP-адресов серверной части hello. Помните, что для каждого экземпляра требуется отдельный IP-адрес.

### <a name="step-2"></a>Шаг 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Этот шаг позволяет настроить hello серверной части IP-адресов с именем «pool01» с IP-адреса «10.1.1.8, 10.1.1.9, 10.1.1.10». Это и есть hello IP-адресов, получения сетевого трафика hello, поступающие от hello переднего плана конечную точку IP. Замените hello предшествующий IP адресов tooadd собственных конечных точек приложения IP адрес.

### <a name="step-3"></a>Шаг 3.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Этот шаг позволяет настроить приложения шлюза параметр «poolsetting01» для загрузки hello балансировки сетевой трафик в пуле hello серверной части.

### <a name="step-4"></a>Шаг 4.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Этот шаг позволяет настроить hello интерфейсный IP-порта с именем «frontendport01» для hello ILB.

### <a name="step-5"></a>Шаг 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Этот шаг создает hello интерфейсный IP-конфигурация называется «fipconfig01» и связывает его с частный IP-адрес в подсети виртуальной сети текущего hello.

### <a name="step-6"></a>Шаг 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Этот шаг создает hello прослушивателя с именем «listener01» и связывает hello интерфейсный порт toohello интерфейсный IP конфигурации.

### <a name="step-7"></a>Шаг 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

На этом шаге создается hello правило подсистемы балансировки нагрузки маршрутизации называется «rule01», предназначенный для настройки поведения подсистемы балансировки нагрузки hello.

### <a name="step-8"></a>Шаг 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Этот шаг позволяет настроить размер экземпляра hello шлюза приложения hello.

> [!NOTE]
> Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10. Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium. Можно выбрать Standard_Small, Standard_Medium или Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Создание шлюза приложений с помощью командлета New-AzureApplicationGateway

Создает все элементы конфигурации из предыдущих шагах hello шлюза приложения. В этом примере шлюза приложения hello называется «appgwtest».

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

На этом шаге создается шлюза приложения со всех элементов конфигурации из hello в предыдущих шагах. В примере hello шлюза приложения hello называется «appgwtest».

## <a name="delete-an-application-gateway"></a>Удаление шлюза приложений

toodelete шлюза приложения необходимые hello toodo следующие шаги в порядке.

1. Используйте hello `Stop-AzureRmApplicationGateway` командлет toostop hello шлюза.
2. Используйте hello `Remove-AzureRmApplicationGateway` командлет tooremove hello шлюза.
3. Убедитесь, что hello шлюза был удален с помощью hello `Get-AzureApplicationGateway` командлета.

### <a name="step-1"></a>Шаг 1

Получите объект шлюза приложения hello и связать его переменной tooa «$getgw».

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Шаг 2

Используйте `Stop-AzureRmApplicationGateway` toostop шлюза приложения hello. В этом примере показано hello `Stop-AzureRmApplicationGateway` на первую строку hello, командлет следуют hello выходных данных.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

После шлюза приложения hello в остановленном состоянии используйте hello `Remove-AzureRmApplicationGateway` командлет tooremove hello службы.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Hello **-принудительно** коммутатор может быть сообщение с подтверждением remove используется toosuppress hello.

tooverify, hello службы были удалены, вы можете использовать hello `Get-AzureRmApplicationGateway` командлета. Этот шаг не является обязательным.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Дальнейшие действия

Если tooconfigure разгрузки SSL, см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).

Tooconfigure toouse шлюза приложения с ILB см [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).

Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

