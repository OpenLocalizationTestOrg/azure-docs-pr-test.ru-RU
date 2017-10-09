---
title: "aaaConfigure SSL разгрузки классический - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Эта статья содержит инструкции, toocreate разгрузки шлюза приложения с помощью протокола SSL с помощью hello Azure классической модели развертывания."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Настройка шлюза приложения для разгрузки SSL с помощью hello классической модели развертывания

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-ssl-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-ssl-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы. Разгрузка SSL также упрощает hello интерфейсном сервере настройку и управление ими hello веб-приложения.

## <a name="before-you-begin"></a>Перед началом работы

1. Установите последнюю версию hello hello командлетов Azure PowerShell с помощью установщика веб-платформы hello. Можно загрузить и установить последнюю версию hello из hello **Windows PowerShell** раздел hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. Убедитесь, что у вас есть рабочая виртуальная сеть с действительной подсетью. Убедитесь, что нет виртуальных машин или развертывания в облаке hello подсети. шлюз приложения Hello должен быть сам по себе в подсети виртуальной сети.
3. должен существовать настройки шлюза приложения hello toouse серверы Hello или назначенные их конечных точек, созданных в hello виртуальной сети или с помощью открытого IP-адрес или VIP.

tooconfigure SSL разгрузки на шлюза приложения, hello шагов в порядке hello:

1. [Создание шлюза приложений](#create-an-application-gateway)
2. [Загрузка SSL-сертификатов](#upload-ssl-certificates)
3. [Настройка шлюза hello](#configure-the-gateway)
4. [Набор конфигурации шлюза hello](#set-the-gateway-configuration)
5. [Запуск шлюза hello](#start-the-gateway)
6. [Проверить состояние шлюза hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

шлюз toocreate hello, используйте hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные. Выставление счетов для шлюза hello не начинается на этом этапе. Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate, hello шлюза был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.

В образце hello *описание*, *InstanceCount*, и *GatewaySize* являются необязательными параметрами. Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10. Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium. Также доступны значения Small (Маленький) и Large (Большой). *Адреса Virtualip* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась. Эти значения создаются после hello шлюз находится в рабочем состоянии hello.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Загрузка SSL-сертификатов

Используйте `Add-AzureApplicationGatewaySslCertificate` tooupload сертификат сервера hello в *pfx* шлюз приложений toohello формат. Имя сертификата Hello является именем выбранные пользователем и должно быть уникальным в пределах шлюза приложения hello. Этот сертификат является ссылка tooby этим именем на все операции управления сертификата для шлюза приложения hello.

Это показано в следующем образце hello командлета, замените собственными значениями hello в образце hello.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Затем проверьте hello загрузки сертификата. Используйте hello `Get-AzureApplicationGatewayCertificate` командлета.

Это пример hello командлета на первую строку hello, следуют hello выходных данных.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> Пароль сертификата Hello имеет toobe между 4 символов too12, буквы или цифры. Специальные знаки не допускаются.

## <a name="configure-hello-gateway"></a>Настройка шлюза hello

Конфигурация шлюза приложений состоит из нескольких значений. Hello значения могут быть привязаны конфигурации hello tooconstruct вместе.

доступны следующие значения Hello:

* **Пул серверных:** hello список IP-адресов серверов hello серверной части. Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.
* **Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie. Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.
* **Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello. Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.
* **Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).
* **Правило:** правило hello привязывает прослушивателя hello и пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя. В настоящее время только hello *основные* правило поддерживается. Hello *основные* правило — распределение нагрузки с циклическим перебором.

**Дополнительные примечания по настройке конфигурации**

Для настройки сертификатов SSL, hello протокола в **HttpListener** следует изменить слишком*Https* (с учетом регистра). Hello **SslCert** слишком добавляется элемент**HttpListener** с hello значение toohello точно такое же имя, как в hello передачи из выше разделе сертификатов SSL. Hello интерфейсный порт должен быть обновленные too443.

**сопоставление на основе файла cookie tooenable**: шлюза приложения может быть настроенный tooensure запроса из сеанса клиента всегда является направленным toohello одной виртуальной Машины hello веб-ферме. Этот сценарий выполняется путем внедрения кода файла cookie сеанса, которое разрешает трафик toodirect шлюза hello соответствующим образом. Задайте сопоставление на основе файла cookie tooenable **CookieBasedAffinity** слишком*включено* в hello **BackendHttpSettings** элемента.

Настроить конфигурацию можно либо путем создания объекта конфигурации, либо с помощью XML-файла конфигурации.
использовать конфигурацию с помощью XML-файл конфигурации tooconstruct hello следующий пример:

**Пример XML-конфигурации**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

Затем нужно установить шлюз приложения hello. Можно использовать hello `Set-AzureApplicationGatewayConfig` командлет с объектом конфигурации или с помощью файла конфигурации XML.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Запуск шлюза hello

После завершения настройки шлюза hello использовать hello `Start-AzureApplicationGateway` командлет toostart hello шлюза. Выставление счетов для шлюза приложения начинается после успешного запуска шлюза hello.

> [!NOTE]
> Hello `Start-AzureApplicationGateway` командлет может занимать toofinish too15-20 минут.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Проверить состояние шлюза hello

Используйте hello `Get-AzureApplicationGateway` командлет toocheck hello состояние шлюза hello. Если `Start-AzureApplicationGateway` успешно hello в предыдущем шаге, *состояние* должна быть запущена, и *адреса Virtualip* и *DnsName* должны иметь допустимые записи.

Этот образец показывает, копирование, запущена и готов tootake трафик шлюза приложения.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

