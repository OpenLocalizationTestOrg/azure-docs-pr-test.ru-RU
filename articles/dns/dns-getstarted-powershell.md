---
title: "aaaGet работы с DNS Azure с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять вашей первой зоны DNS и записи с помощью PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Приступая к работе со службой DNS Azure с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

В этой статье описывается toocreate действия hello вашей первой зоны DNS и запись с помощью Azure PowerShell. Также можно выполнить следующие действия с помощью портала Azure hello или hello кросс платформенных Azure CLI.

Зоны DNS-записей DNS используется toohost hello для определенного домена. toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена. Каждая запись DNS для вашего домена создается внутри этой зоны DNS. Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello. Каждый из этих шагов описан ниже.

Эти инструкции предполагают, вы уже установили и вход выполнен tooAzure PowerShell. Справочные сведения см. в разделе [как toomanage DNS-зоны с помощью PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Перед созданием hello зоны DNS, зоны DNS hello toocontain создания группы ресурсов. Hello ниже показана команда hello.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зоны DNS создается с помощью hello `New-AzureRmDnsZone` командлета. Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*. Используйте toocreate пример hello зону DNS, подставив собственные значения hello.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Создание записи DNS

Создание наборов записей с помощью hello `New-AzureRmDnsRecordSet` командлета. Hello в примере создается запись с hello относительное имя «www» в зону DNS «contoso.com» в группе ресурсов «MyResourceGroup» hello. Hello полное имя набора записей hello — «www.contoso.com». Тип записи Hello «A» с IP-адресом «1.2.3.4», который hello TTL 3600 секунд.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Для других типов записей для наборов записей с более чем одной записи и toomodify существующие записи, в разделе [Управление DNS-записи и наборы записей с помощью Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Просмотр записей

toolist hello DNS-записи в зоне, используйте:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Обновление серверов доменных имен

Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами. Это позволяет другим пользователям на hello Internet toofind DNS-записей.

Hello серверы имен для зоны определяются hello `Get-AzureRmDnsZone` командлета:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя). Регистратор предлагают tooset параметр hello hello серверов имя домена hello. Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Удаление всех ресурсов

toodelete все ресурсы созданы в этой статье hello выполните следующий шаг:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).

toolearn Дополнительные сведения об управлении зонами DNS в Azure DNS, в разделе [Управление DNS зоны в DNS Azure с помощью PowerShell](dns-operations-dnszones.md).

toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и записи задает в Azure DNS с помощью PowerShell](dns-operations-recordsets.md).

