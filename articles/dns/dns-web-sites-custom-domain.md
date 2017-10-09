---
title: "aaaCreate пользовательские записи DNS для веб-приложения | Документы Microsoft"
description: "Порядок toocreate пользовательский домен DNS записей для веб-приложения с помощью Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Создание записей DNS для веб-приложения в пользовательском домене

Azure DNS toohost пользовательского домена можно использовать для развертывания веб-приложений. Например, вы создаете веб-приложение Azure и требуется вашей tooaccess пользователи его, либо используя в качестве полного доменного ИМЕНИ contoso.com или www.contoso.com.

toodo, у вас есть toocreate две записи:

* Записи указывающего toocontoso.com корневой «A»
* Запись «» CNAME hello www имя, которое указывает toohello запись

Имейте в виду, что при создании записи для веб-приложения в Azure, записи, необходимо вручную обновить если приветствия hello базовый IP-адрес для изменения приложения hello web.

## <a name="before-you-begin"></a>Перед началом работы

Прежде чем начать, необходимо сначала создать зону DNS в Azure DNS и делегировать зону hello в tooAzure вашего регистратора DNS.

1. toocreate зоны DNS, следуйте указаниям hello [создать зону DNS](dns-getstarted-create-dnszone.md).
2. toodelegate вашей tooAzure DNS DNS, выполните действия hello в [делегирование DNS домена](dns-domain-delegation.md).

После создания зоны и делегирования его tooAzure DNS, затем можно создавать записи для вашего домена.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Создание записи A для пользовательского домена

Запись — используется toomap имя tooits IP-адрес. В следующий пример hello мы назначит как tooan записи A IPv4-адрес:

### <a name="step-1"></a>Шаг 1

Создать запись и присвоить переменной $rs tooa

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Шаг 2

Добавление набора записей toohello ранее созданные значение hello IPv4 «@» с помощью назначен переменной hello $rs. Присвоенное значение IPv4 Hello будет hello IP-адрес для веб-приложения.

toofind hello IP-адрес для веб-приложения, выполните действия hello в [настроить пользовательское доменное имя в службе приложений Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Шаг 3.

Фиксация набора записей toohello изменения hello. Используйте `Set-AzureRMDnsRecordSet` tooupload hello изменяет tooAzure toohello набора записей DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Создание записи CNAME для личного домена

Если домен уже находится под управлением Azure DNS (см. [делегирование DNS домена](dns-domain-delegation.md), можно использовать следующий пример hello toocreate запись CNAME для contoso.azurewebsites.net hello.

### <a name="step-1"></a>Шаг 1

Откройте PowerShell и создайте новый набор записей типа CNAME и назначьте tooa переменной $rs. В этом примере создается набор записей типа CNAME с «временем toolive» 600 секунд в зоне DNS с именем «contoso.com».

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Следующий пример Hello — ответ hello.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Шаг 2

После создания набора записей CNAME hello toocreate необходимо значение псевдонима, которое будет указывать toohello веб-приложения.

С помощью ранее назначены переменной «$rs» hello можно использовать команду PowerShell hello ниже toocreate hello псевдоним для contoso.azurewebsites.net приложения hello web.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Следующий пример Hello — ответ hello.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Шаг 3.

Подтверждение изменений hello, с помощью hello `Set-AzureRMDnsRecordSet` командлета:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Можно проверить правильность создания записи hello запросив hello «www.contoso.com» с помощью команды nslookup, как показано ниже:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Создание записи awverify для веб-приложений

Если вы решите toouse записи для веб-приложения, вы должны проходить через tooensure процесс проверки вы hello собственный пользовательский домен. Для прохождения этой проверки требуется создать специальную запись CNAME с именем awverify. Этот раздел применим только для записи tooA.

### <a name="step-1"></a>Шаг 1

Создайте запись «awverify» hello. В следующем примере hello мы создадим hello записи «aweverify» для contoso.com tooverify владения для пользовательского домена hello.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Следующий пример Hello — ответ hello.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Шаг 2

После создания набора записей hello «awverify» назначьте псевдоним набора записей CNAME hello. В следующем примере hello мы назначит tooawverify.contoso.azurewebsites.net псевдоним набора записей CNAMe hello.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Следующий пример Hello — ответ hello.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Шаг 3.

Подтверждение изменений hello, с помощью hello `Set-AzureRMDnsRecordSet cmdlet`, как показано в следующей команде hello.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Дальнейшие действия

Следуйте указаниям hello [Настройка имени пользовательского домена для служб приложений](../app-service-web/web-sites-custom-domain-name.md) tooconfigure вашей toouse приложения web пользовательского домена.
