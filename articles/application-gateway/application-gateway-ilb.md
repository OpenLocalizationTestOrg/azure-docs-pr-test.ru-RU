---
title: "Шлюз приложения Azure с внутренним балансировщиком нагрузки aaaUsing | Документы Microsoft"
description: "На этой странице представлены инструкции tooconfigure шлюза приложения Azure с конечной точкой внутренней балансировки нагрузки"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Создание шлюза приложений с внутренней подсистемой балансировщика нагрузки (ILB)

> [!div class="op_single_selector"]
> * [Классическая модель — Azure PowerShell](application-gateway-ilb.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-ilb-arm.md)

Шлюз приложений можно настроить виртуальный IP-адрес с выходом в Интернет или с toohello внутренняя конечная точка не предоставляется Интернет, также известные как внутренняя Подсистема балансировки нагрузки (ILB) конечной точки. Настройка шлюза hello с ILB полезен для toointernet внутренних бизнес-приложений, в не предоставляется. Также полезно для служб или уровней в многоуровневое приложение, в которой располагается в toointernet не предоставляется границу безопасности, но по-прежнему требуется распределение нагрузки циклического перебора, stickiness сеанса или завершение запросов SSL. В этой статье рассматриваются действия hello tooconfigure шлюза приложения с ILB.

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello установщика веб-платформы с помощью командлетов Azure PowerShell hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницы загрузки](https://azure.microsoft.com/downloads/).
2. Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью.
3. Проверьте наличие внутренних серверов в виртуальной сети hello или открытый IP/VIP-адрес, назначенный.

toocreate шлюза приложения, выполните следующие шаги в порядке hello hello. 

1. [Создание шлюза приложений](#create-a-new-application-gateway)
2. [Настройка шлюза hello](#configure-the-gateway)
3. [Набор конфигурации шлюза hello](#set-the-gateway-configuration)
4. [Запуск шлюза hello](#start-the-gateway)
5. [Проверка шлюза hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

**шлюз hello toocreate**, использовать hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные. Обратите внимание, что выставления счетов для hello шлюза не запущен на этом этапе. Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** hello шлюз был создан, можно использовать hello `Get-AzureApplicationGateway` командлета. 

В образце hello *описание*, *InstanceCount*, и *GatewaySize* являются необязательными параметрами. Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10. Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium. Также доступны значения Small (Маленький) и Large (Большой). *Виртуальный IP-адрес* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась. Эти отчеты создаются после hello шлюз находится в рабочем состоянии hello. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Настройка шлюза hello
Конфигурация шлюза приложений состоит из нескольких значений. Hello значения могут быть привязаны конфигурации hello tooconstruct вместе.

доступны следующие значения Hello:

* **Внутренний пул сервера:** hello список IP-адресов hello внутренних серверов. Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP. 
* **Параметры пула внутренних серверов:** каждый пул имеет такие параметры, как порт, протокол и соответствие на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт открыт для шлюза приложения hello. Трафик обращений к этому порту и затем получает перенаправленный tooone hello внутренних серверов.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, они зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки). 
* **Правило:** правило hello привязывает прослушивателя hello и hello внутреннего сервера пула и определяет, какой трафик hello внутреннего пула сервера должен быть расширенный toowhen попадании конкретного прослушивателя. В настоящее время только hello *основные* правило поддерживается. Hello *основные* правило — распределение нагрузки с циклическим перебором.

Настроить конфигурацию можно либо путем создания объекта конфигурации, либо с помощью XML-файла конфигурации. tooconstruct конфигурацию с помощью XML-файл конфигурации, используйте hello примера ниже.

Обратите внимание hello следующие:

* Hello *FrontendIPConfigurations* описывает hello ILB сведения относятся только к настройке шлюза приложения с ILB. 
* Hello интерфейсных IP-адресов *тип* должно быть установлено too'Private "
* Hello *StaticIPAddress* должно быть установлено toohello требуемого внутренний IP-адрес на какие hello шлюз получает трафик. Обратите внимание, что hello *StaticIPAddress* элемент является необязательным. В противном случае выбирается набор, доступный внутренний IP-адрес из подсети развернут hello. 
* Здравствуйте, значение hello *имя* элемент, указанный в *FrontendIPConfiguration* должны использоваться в hello HTTPListener в *FrontendIP* toohello toorefer элемент FrontendIPConfiguration.
  
  **Пример XML-конфигурации**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a>Набор конфигурации шлюза hello
Затем можно задать шлюза приложения hello. Можно использовать hello `Set-AzureApplicationGatewayConfig` командлет с помощью объекта конфигурации или с помощью файла конфигурации XML. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Запуск шлюза hello

После завершения настройки шлюза hello использовать hello `Start-AzureApplicationGateway` командлет toostart hello шлюза. Выставление счетов для шлюза приложения начинается после успешного запуска шлюза hello. 

> [!NOTE]
> Hello `Start-AzureApplicationGateway` командлет может занимать toocomplete too15-20 минут. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Проверить состояние шлюза hello

Используйте hello `Get-AzureApplicationGateway` командлет toocheck hello состояние шлюза. Если `Start-AzureApplicationGateway` успешно в предыдущем шаге hello hello состояние должно быть *под управлением*, hello виртуальных IP-адресов и DnsName должны иметь допустимые записи. Это пример hello командлета на первую строку hello, следуют hello выходных данных. В этом образце hello шлюз запущен и готов tootake трафика. 

> [!NOTE]
> шлюз приложения Hello настроен tooaccept трафика в hello конечной точке ILB 10.0.0.10 настроен в этом примере.

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

