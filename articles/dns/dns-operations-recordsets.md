---
title: "Записывает aaaManage DNS в Azure DNS, с помощью Azure PowerShell | Документы Microsoft"
description: "Управляйте наборами записей и записями DNS в службе Azure DNS при размещении вашего домена в Azure DNS. Все команды PowerShell для операций с наборами записей и записями."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Управление записями и наборами записей DNS в службе DNS Azure с помощью Azure PowerShell

> [!div class="op_single_selector"]
> * [Портал Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

В этой статье показано, как записывает toomanage DNS для зоны DNS с помощью Azure PowerShell. DNS-записи можно также управлять с помощью hello кросс платформенных [Azure CLI](dns-operations-recordsets-cli.md) или hello [портал Azure](dns-operations-recordsets-portal.md).

Hello в этой статье примерах уже имеется [Azure PowerShell, вход и создали зоны DNS](dns-operations-dnszones.md).

## <a name="introduction"></a>Введение

Прежде чем создавать DNS-записи в Azure DNS, необходимо сначала toounderstand как Azure DNS организует DNS-записей в наборы записей DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).


## <a name="create-a-new-dns-record"></a>Создание записи DNS

Если новую запись имеет hello совпадают имя и тип в качестве существующей записи, необходимо слишком[добавьте его в существующий набор записей toohello](#add-a-record-to-an-existing-record-set). Если новую запись имеет разные имена и типы tooall существующие записи, то необходимо toocreate нового набора записей. 

### <a name="create-a-records-in-a-new-record-set"></a>Создание записей А в новом наборе записей

Создание наборов записей с помощью hello `New-AzureRmDnsRecordSet` командлета. При создании набора записей, необходимо имя набора записей toospecify hello, hello зоны, hello время toolive (TTL), тип записи hello и toobe записей hello.

Hello параметры для добавления набора записей tooa записей зависит от типа hello hello набор записей. Например, при использовании набора записей типа «A», требуется toospecify hello IP-адрес с помощью параметра hello `-IPv4Address`. Другие параметры используются для других типов записей (см. [примеры других типов записей](#additional-record-type-examples)).

Hello пример создает записей с hello относительное имя «www», в зону DNS «contoso.com» hello. Hello полное имя набора записей hello — «www.contoso.com». Тип записи Hello «A», который hello TTL 3600 секунд. набор записей Hello содержит одну запись, с IP-адресом "1.2.3.4».

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate набор записей в зоне «вершине» hello (в данном случае «contoso.com»), используйте имя набора записей hello "@" (без кавычек):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Если вам требуется toocreate набор записей, содержащий несколько записей, сначала создать локальный массив и добавить записи hello, а затем передать массив hello слишком`New-AzureRmDnsRecordSet` следующим образом:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение". Hello следующем примере показано, как toocreate набор записей с две записи метаданных "dept = процент" и "среды производственного =".

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

Azure DNS также поддерживает «empty» наборы записей, которые может выступать в качестве tooreserve заполнитель DNS-имя перед созданием записи DNS. Пустые наборы записей, отображаются в плоскости управления hello Azure DNS, но отображаться на hello Azure DNS-серверами. Следующий пример Hello создает пустой набор записей:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Создание записей других типов

Рассматривать подробно порядок записей toocreate «A» hello, в следующих примерах показано, как записи toocreate других записи типы, поддерживаемые системой Azure DNS.

В каждом случае показано, как toocreate запись набор, содержащий одну запись. Hello предыдущих примерах для записей 'A' может быть адаптирован toocreate наборы записей других типов, содержащих несколько записей с метаданными, или пустая запись toocreate задает.

Мы не предоставляем toocreate примере SOA набор записей, так как создаются SOA и удалены вместе с каждой зоны DNS и не удается создать или удалить отдельно. Тем не менее [SOA могут быть изменены, как показано в пример hello](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Создание набора записей типа AAAA с одной записью

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Создание набора записей типа CNAME с одной записью

> [!NOTE]
> Hello стандартах DNS не допускают записи CNAME на вершине hello зоны (`-Name '@'`), и не следует разрешать или запрещать наборы записей, содержащая более одной записи.
> 
> Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Создание набора записей типа MX с одной записью

В этом примере мы используем имя набора записей hello ' @' toocreate MX-записи на вершине зоны hello (в данном случае «contoso.com»).


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Создание набора записей типа NS с одной записью

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Создание набора записей типа PTR с одной записью

В этом случае "my-arpa-zone.com" представляет hello ARPA зоны обратного просмотра, представляющий ваш диапазон IP-адресов. Каждая запись PTR в этой зоне соответствует tooan IP-адрес в этот диапазон IP-адресов. Имя записи Hello "10" представляет hello последний октет hello IP-адрес в этот диапазон IP-адресов, представленного данной записью.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Создание набора записей типа SRV с одной записью

При создании [набор записей типа SRV](dns-zones-records.md#srv-records), укажите hello  *\_службы* и  *\_протокола* в hello имя набора записей. Нет нет необходимости tooinclude "@" в hello запись имя набора при создании записи SRV набора в вершине зоны hello.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Создание набора записей типа TXT с одной записью

Hello следующем примере показано, как записать toocreate TXT. Дополнительные сведения о hello Максимальная длина строки поддерживается в записи TXT в разделе [записи TXT](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Получение набора записей

использовать существующий набор записей, tooretrieve `Get-AzureRmDnsRecordSet`. Этот командлет возвращает локальный объект, представляющий hello записи в Azure DNS.

Как и в `New-AzureRmDnsRecordSet`, должно быть имя набора записей hello *относительный* имя, то есть его необходимо исключить hello имя зоны. Необходимо также тип записи toospecify hello и hello зону, содержащую набор записей hello.

Hello примере показан способ tooretrieve набор записей. В этом примере hello зоны задается с помощью hello `-ZoneName` и `-ResourceGroupName` параметров.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Кроме того, можно также указать hello зоны с помощью объекта зоны, переданные с помощью hello `-Zone` параметра.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Перечисление наборов записей

Можно также использовать `Get-AzureRmDnsZone` наборов toolist записей в зоне, пропустив hello `-Name` и/или `-RecordType` параметров.

Hello следующий пример возвращает все записи задает в зоне hello.

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Hello следующем примере показано, как все записи наборов данного типа, можно получить, указав тип записи hello, пока пропуск записи hello имя набора:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Задает все записи с заданным именем, tooretrieve разных типов записей, необходимо tooretrieve все наборы записей, а затем результаты hello фильтра:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

В все hello выше примеры hello зоны может быть указан с помощью hello `-ZoneName` и `-ResourceGroupName`параметров (как показано), или путем указания объекта зоны:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Добавление записей tooan существующего набора записей

tooadd существующей записи записей tooan задать, выполните следующие три шага hello.

1. Получение существующего набора записей hello

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Добавьте hello новых записей toohello локальный набор записей. Эта операция выполняется в автономном режиме.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Зафиксируйте hello изменений назад toohello служба Azure DNS. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

С помощью `Set-AzureRmDnsRecordSet` *заменяет* hello существующих записей в Azure DNS (и все записи, он содержит) с указанного набора записей hello. [Проверяет eTag](dns-zones-records.md#etags) используются tooensure параллельных изменений не перезаписываются. Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.

Эта последовательность операций также может быть *по конвейеру*, то есть передать hello объекта набора записей, через канал hello вместо передачи его в качестве параметра:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Hello примеры выше показывают, как задать tooadd 'A' записей tooan существующей записи типа «A». Аналогичные последовательности операций является наборов toorecord записей используется tooadd других типов, заменив hello `-Ipv4Address` параметр `Add-AzureRmDnsRecordConfig` с другим типом записи tooeach определенные параметры. Hello параметров для каждого типа записи являются hello же, как и для hello `New-AzureRmDnsRecordConfig` командлет, как показано в [примеры дополнительных тип записи](#additional-record-type-examples) выше.

Наборы записей типа CNAME или SOA не могут содержать более одной записи. Это ограничение возникают из-за стандартах DNS hello. а не Azure DNS.

## <a name="remove-a-record-from-an-existing-record-set"></a>Удаление записи из существующего набора записей

Hello tooremove процесс записи из набора записей — примерно toohello процесс, tooadd в существующие записи tooan записи набора:

1. Получение существующего набора записей hello

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Удалите запись hello из hello объекта локальный набор записей. Эта операция выполняется в автономном режиме. запись Hello, которое удаляется должно быть в точности совпадать с уже имеющейся записи для всех параметров.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Зафиксируйте hello изменений назад toohello служба Azure DNS. Используйте hello необязательно `-Overwrite` переключения toosuppress [проверяет Etag](dns-zones-records.md#etags) для параллельных изменений.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Hello выше последовательности tooremove hello последней записи из набора записей с помощью удаляет hello: набор записей, а остается пустой набор записей. см. набор записей, полностью tooremove [удалить набор записей](#delete-a-record-set).

Аналогичным образом набора записи tooa tooadding записей последовательность hello tooremove операций, который также может быть выведен набор записей:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Записей различных типов поддерживаются, передавая соответствующие параметры конкретного типа hello слишком`Remove-AzureRmDnsRecordSet`. Hello параметров для каждого типа записи являются hello же, как и для hello `New-AzureRmDnsRecordConfig` командлет, как показано в [примеры дополнительных тип записи](#additional-record-type-examples) выше.


## <a name="modify-an-existing-record-set"></a>Обновление существующего набора записей

Hello действия по изменению существующего набора записей приведены действия, аналогичные toohello предпринять при добавлении или удалении записей из набора записей.

1. Получить задание с помощью существующей записи hello `Get-AzureRmDnsRecordSet`.
2. Измените hello объекта локальный набор записей:
    * добавьте или удалите записи;
    * Изменение параметров hello существующих записей
    * Изменение записи hello набора метаданных и времени toolive (TTL)
3. Фиксация изменений с помощью hello `Set-AzureRmDnsRecordSet` командлета. Это *заменяет* hello существующих записей в Azure DNS с указанного набора записей hello.

При использовании `Set-AzureRmDnsRecordSet`, [проверяет Etag](dns-zones-records.md#etags) используются tooensure параллельных изменений не перезаписываются. Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>задать tooupdate записи в существующей записи

В этом примере мы изменяем hello IP-адрес существующего «запись»:

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify записи SOA

Не удается добавить или удаления записей из hello автоматически создается на вершине зоны hello начальной записи (`-Name "@"`, включая кавычки). Однако вы можете изменить любые параметры hello в рамках hello начальной записи зоны (кроме «узел») и записи hello задать значение срока ЖИЗНИ.

Следующий пример показывает как Hello toochange hello *электронной почты* свойство hello начальной записи зоны:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>записей toomodify NS на вершине зоны hello

запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS. Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.

Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS. Можно также изменить hello TTL и метаданные для этого набора записей. Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.

Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello. Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.

Привет, в следующем примере показано, как tooadd запись NS toohello дополнительное имя сервера задать на вершине зоны hello:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>набор записей toomodify метаданных

[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".

Hello ниже приведен пример настройки метаданных hello toomodify существующей записи.

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>Удаление набора записей

Наборы записей можно удалить с помощью hello `Remove-AzureRmDnsRecordSet` командлета. При удалении набора записей также удаляются все записи в наборе записей hello.

> [!NOTE]
> Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (`-Name '@'`).  Azure DNS создается их автоматически при hello зона была создана и удаляет их автоматически при удалении hello зоны.

Hello примере показан способ toodelete набор записей. В этом примере имя набора записей hello, набор записей типа, имени зоны и группы ресурсов каждого указаны явным образом.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Кроме того hello набор записей может быть указан с именем и типом и hello зоны, указанный с помощью объекта:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Как третий параметр — набора сам записей hello может быть задано с помощью объекта набора записей:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

При указании toobe удалена с помощью объекта набора записей, набор записей hello [проверяет Etag](dns-zones-records.md#etags) используются tooensure параллельных изменений не удаляются. Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.

Hello объекта набора записей также можно направить вместо передан в качестве параметра:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Запросы на подтверждение

Hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, и `Remove-AzureRmDnsRecordSet` все командлеты поддерживают запросы подтверждения.

Каждый командлет запрашивает подтверждение, если hello `$ConfirmPreference` PowerShell Привилегированная переменная имеет значение `Medium` или ниже. Так как значение по умолчанию hello `$ConfirmPreference` — `High`, не получают эти запросы при использовании параметров PowerShell по умолчанию hello.

Можно переопределить текущего hello `$ConfirmPreference` параметр с помощью hello `-Confirm` параметра. При указании `-Confirm` или `-Confirm:$True` , hello командлет запросит подтверждение перед его запуска. При указании `-Confirm:$False` , командлет hello не запрашивает вашего подтверждения. 

Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Дальнейшие действия

См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).
<br>
Узнайте, каким образом слишком[защиты зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.
<br>
Просмотрите hello [справочная документация по Azure DNS PowerShell](/powershell/module/azurerm.dns).
