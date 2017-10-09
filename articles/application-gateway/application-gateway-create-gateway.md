---
title: "aaaCreate, запуск или удаление шлюза приложения | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, Настройка, запуск и удалить шлюз приложения Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Создание, запуск или удаление шлюза приложений с помощью PowerShell 

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-gateway-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-gateway.md)
> * [Шаблон диспетчера ресурсов Azure](application-gateway-create-gateway-arm-template.md)
> * [Интерфейс командной строки Azure](application-gateway-create-gateway-cli.md)

Шлюз приложений — это балансировщик нагрузки уровня 7. Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной. Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д. Полный список поддерживаемых функций toofind посетите [Обзор шлюза приложения](application-gateway-introduction.md)

В этой статье рассматриваются действия toocreate hello, Настройка, запуск и удалить шлюз приложения.

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. При наличии существующей виртуальной сети, выберите существующую пустую подсеть или создать новую подсеть в существующей виртуальной сети для использования исключительно шлюзом приложения hello. Невозможно развернуть hello приложения шлюза tooa другую виртуальную сеть чем hello ресурсы предполагается toodeploy за шлюза приложения hello, если не используется пиринг виртуальной сети. более посетите toolearn [Пиринг виртуальной сети](../virtual-network/virtual-network-peering-overview.md)
3. Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью. Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети. шлюз приложения Hello должен быть сам по себе в подсети виртуальной сети.
4. должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Что такое необходимые toocreate шлюза приложения

При использовании hello `New-AzureApplicationGateway` шлюза приложения hello toocreate команды, конфигурация не установлено на этом этапе и hello только что созданный ресурс настраиваются с помощью XML или объект конфигурации.

доступны следующие значения Hello:

* **Пул серверных:** hello список IP-адресов серверов hello серверной части. Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

toocreate шлюза приложения:

1. Создание ресурса шлюза приложений.
2. Создайте XML-файл конфигурации или объект конфигурации.
3. Зафиксируйте toohello конфигурации hello созданного ресурса шлюза приложения.

> [!NOTE]
> Если вам требуется пользовательский зонд tooconfigure шлюза приложения, см. раздел [создать шлюз приложений с пользовательской проверки с помощью PowerShell](application-gateway-create-probe-classic-ps.md). Дополнительные сведения см. в статье [Обзор мониторинга работоспособности шлюза приложений](application-gateway-probe-overview.md).

![Пример сценария][scenario]

### <a name="create-an-application-gateway-resource"></a>Создание ресурса шлюза приложений.

шлюз toocreate hello, используйте hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные. Выставление счетов для шлюза hello не начинается на этом этапе. Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.

Hello следующий пример создает шлюза приложения, используя виртуальную сеть с именем «testvnet1» и подсети, называется «подсеть-1»:

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* и *GatewaySize* — необязательные параметры.

toovalidate, hello шлюза был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10. Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium. Можно выбрать размер Small (Малый), Medium (Средний) или Large (Большой).

*Адреса Virtualip* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась. Эти отчеты создаются после hello шлюз находится в рабочем состоянии hello.

## <a name="configure-hello-application-gateway"></a>Настройка шлюза приложения hello

Шлюз приложения hello можно настроить с помощью XML-индекс или объект конфигурации.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Настройка шлюза hello приложения с помощью XML

В следующем примере hello используйте все параметры шлюза приложения tooconfigure файла XML и зафиксировать их ресурса шлюза toohello приложения.  

#### <a name="step-1"></a>Шаг 1

Скопируйте следующий текст tooNotepad hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Изменение значений hello заключено в круглые скобки hello для элементов конфигурации hello. Сохраните hello файл с расширением .xml.

> [!IMPORTANT]
> Hello элемент протокола Http или Https с учетом регистра.

Hello в следующем примере показано, как toouse конфигурации файла tooset Создание шлюза приложения hello. Загрузка пример Hello распределяет трафик HTTP на открытый порт 80 и отправляет сетевой трафик tooback конечный порт 80 между двумя IP-адресами.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a>Шаг 2

Затем задайте шлюза приложения hello. Используйте hello `Set-AzureApplicationGatewayConfig` командлет с помощью файла конфигурации XML.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Настройка шлюза hello приложения с помощью объекта конфигурации

Hello в следующем примере показано, как tooconfigure hello шлюз приложений с помощью объектов конфигурации. Все элементы конфигурации, которые необходимо настроить отдельно и затем добавляются объект конфигурации шлюза tooan приложения. После создания объекта конфигурации hello, использовать hello `Set-AzureApplicationGateway` toohello конфигурации hello toocommit команда создала ресурса шлюза приложения.

> [!NOTE]
> Перед назначением объект конфигурации tooeach значения, необходимо toodeclare объект какого типа PowerShell использует для хранения данных. Определяет, что Hello первой строки toocreate hello отдельных элементов `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` используются.

#### <a name="step-1"></a>Шаг 1

Создайте все отдельные элементы конфигурации.

Создайте hello интерфейсный IP, как показано в следующий пример hello.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Создайте интерфейсный порт hello, как показано в следующий пример hello.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Создайте пул серверных hello.

Определите hello IP-адресов, которые добавляются в пул серверных toohello, как показано в следующем примере hello.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Используйте объект toohello серверной части пула tooadd hello hello $server объекта значения ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Создайте пул приветствия на внутреннем сервере.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Создайте прослушиватель hello.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Создание правила hello.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Шаг 2

Назначьте все отдельные элементы tooan приложения шлюза конфигурации объект конфигурации ($appgwconfig).

Добавьте hello интерфейсный IP-toohello конфигурации.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Добавьте конфигурацию toohello интерфейсный порт hello.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Добавьте конфигурацию toohello пула серверных hello.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Добавьте hello внутренней параметр toohello конфигурацию пула.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Добавьте конфигурацию toohello hello прослушивателя.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Добавьте конфигурацию toohello правило hello.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Шаг 3.
Зафиксировать ресурс шлюза для объекта toohello hello конфигурации приложения с помощью `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Запуск шлюза hello

После завершения настройки шлюза hello использовать hello `Start-AzureApplicationGateway` командлет toostart hello шлюза. Выставление счетов для шлюза приложения начинается после успешного запуска шлюза hello.

> [!NOTE]
> Hello `Start-AzureApplicationGateway` командлет может занимать toofinish too15-20 минут.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Проверить состояние шлюза hello

Используйте hello `Get-AzureApplicationGateway` командлет toocheck hello состояние шлюза hello. Если `Start-AzureApplicationGateway` успешно hello в предыдущем шаге, *состояние* должна быть запущена, и *Vip* и *DnsName* должны иметь допустимые записи.

Hello пример шлюза приложения, активированы, запущены и готов tootake трафик, поступающий для `http://<generated-dns-name>.cloudapp.net`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Удалить шлюз приложения hello

шлюз приложения hello toodelete:

1. Используйте hello `Stop-AzureApplicationGateway` командлет toostop hello шлюза.
2. Используйте hello `Remove-AzureApplicationGateway` командлет tooremove hello шлюза.
3. Убедитесь, что hello шлюза был удален с помощью hello `Get-AzureApplicationGateway` командлета.

Hello пример hello `Stop-AzureApplicationGateway` на первую строку hello, командлет следуют hello выходных данных.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

После шлюза приложения hello в остановленном состоянии используйте hello `Remove-AzureApplicationGateway` командлет tooremove hello службы.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

tooverify, hello службы были удалены, вы можете использовать hello `Get-AzureApplicationGateway` командлета. Этот шаг не является обязательным.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Дальнейшие действия

Если tooconfigure разгрузки SSL, см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).

Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).

Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
