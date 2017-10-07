---
title: "aaaCreate классические пользовательский зонд - шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate пользовательской проверки для шлюза приложения с помощью PowerShell в hello классической модели развертывания"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Создание пользовательской проверки для шлюза приложений (классического) Azure с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-probe-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-probe-ps.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-probe-classic-ps.md)

В этой статье добавьте пользовательский зонд tooan существующего приложения шлюза с помощью PowerShell. Пользовательские зонды полезны для приложений, имеющих страницы проверки работоспособности конкретного или для приложений, которые не предоставляют успешный ответ на веб-приложения по умолчанию hello.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Создание шлюза приложений

toocreate шлюза приложения:

1. Создание ресурса шлюза приложений.
2. Создайте XML-файл конфигурации или объект конфигурации.
3. Зафиксируйте toohello конфигурации hello созданного ресурса шлюза приложения.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Создание ресурса шлюза приложений с пользовательской пробой

шлюз toocreate hello, используйте hello `New-AzureApplicationGateway` командлета, заменив значения hello собственные. Выставление счетов для шлюза hello не начинается на этом этапе. Выставление счетов начинается на более позднем этапе hello шлюза успешно запущен.

Hello следующий пример создает шлюза приложения, используя виртуальную сеть с именем «testvnet1» и подсети, называется «подсеть-1».

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate, hello шлюза был создан, можно использовать hello `Get-AzureApplicationGateway` командлета.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Здравствуйте, значение по умолчанию для *InstanceCount* 2, с максимальным значением 10. Здравствуйте, значение по умолчанию для *GatewaySize* используется значение Medium. Можно выбрать значения Small, Medium или Large.
> 
> 

*Адреса Virtualip* и *DnsName* , отображаются как пустые, потому что hello шлюза еще не началась. Эти значения создаются после hello шлюз находится в рабочем состоянии hello.

### <a name="configure-an-application-gateway-by-using-xml"></a>Настройка шлюза приложений с помощью XML-файла

В следующем примере hello используйте все параметры шлюза приложения tooconfigure файла XML и зафиксировать их ресурса шлюза toohello приложения.  

Скопируйте следующий текст tooNotepad hello.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Изменение значений hello заключено в круглые скобки hello для элементов конфигурации hello. Сохраните hello файл с расширением .xml.

Hello следующем примере показано, как toouse tooset файл конфигурации вверх tooload шлюза приложения hello найти баланс между HTTP-трафика на открытый порт 80 и отправлять tooback конечный порт 80 между двумя IP-адресами с помощью пользовательский зонд сетевой трафик.

> [!IMPORTANT]
> Hello элемент протокола Http или Https с учетом регистра.

Новый элемент конфигурации \<проверки\> добавляется tooconfigure пользовательские зонды.

используются следующие параметры конфигурации Hello.

|Параметр|Описание|
|---|---|
|**Имя** |Имя пользовательской пробы. |
* **Protocol** | Используемый протокол (возможные значения: HTTP или HTTPS).|
| **Host** и **Path** | Полный путь к URL-адрес, вызываемая hello приложения шлюза toodetermine hello работоспособности экземпляра hello. Например если у вас http://contoso.com/ веб-сайта можно настроить пользовательский зонд hello для «http://contoso.com/path/custompath.htm» для проверки проверяет toohave успешного ответа HTTP.|
| **Интервал** | Настраивает hello выборки интервала проверки в секундах.|
| **Время ожидания** | Определяет время ожидания проверки hello для проверки ответа HTTP.|
| **UnhealthyThreshold** | Здравствуйте, количество неудачных откликов HTTP необходимости tooflag hello внутренней экземпляр как *неработоспособное*.|

Имя пробы Hello упоминается в hello \<BackendHttpSettings\> tooassign конфигурации серверной части пул использует пользовательский зонд параметры.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Добавление шлюза пользовательский зонд tooan существующего приложения

Изменение hello текущую конфигурацию шлюза приложения состоит из трех действий: получение hello текущего файла конфигурации XML, изменения toohave пользовательский зонд и настройки шлюза приложения hello hello новыми параметрами XML.

1. Получить hello XML-файл с помощью `Get-AzureApplicationGatewayConfig`. Этот командлет экспортирует hello конфигурации XML toobe изменить tooadd параметр пробы.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Привет открыть XML-файл в текстовом редакторе. Добавьте раздел `<probe>` после `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  В разделе backendHttpSettings hello hello XML добавьте имя пробы hello, как показано в следующий пример hello:

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Сохраните hello XML-файл.

1. Обновление конфигурации шлюза приложения hello hello новый XML-файл с помощью `Set-AzureApplicationGatewayConfig`. Этот командлет обновляет шлюз приложения hello новую конфигурацию.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Дальнейшие действия

Если tooconfigure разгрузки Secure Sockets Layer (SSL), см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).

Если tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, см. [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).

