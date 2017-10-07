---
title: "aaaDelegate tooAzure вашего домена DNS | Документы Microsoft"
description: "Понять, как toochange делегирования домена и Azure DNS используйте имя размещение домена tooprovide серверов."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Делегат tooAzure домена DNS

Azure DNS позволяет toohost зоны DNS и управлять hello записей DNS для домена в Azure. Чтобы запросы DNS для домена tooreach Azure DNS, hello домен имеет toobe делегировать tooAzure DNS из родительского домена hello. Имейте в виду Azure DNS не hello регистратора домена. В этой статье объясняется, как toodelegate tooAzure вашего домена DNS.

Для доменов, приобретенных у регистратора регистратор предлагает tooset параметр hello этих записей NS. У вас tooown домена toocreate зоны DNS с помощью этого доменного имени в Azure DNS. Тем не менее следует соблюдать tooset домена hello tooown копирование tooAzure hello делегирование DNS у регистратора hello.

Например предположим, вы приобрели hello домена «contoso.net» и создать зону с именем hello «contoso.net» в Azure DNS. Как владелец домена hello hello регистратор предлагает hello параметр tooconfigure hello имя адреса сервера (то есть записи hello NS) для своего домена. Эти записи NS сохраняет регистратора Hello в hello родительский домен, в данном случае «.net». Затем клиенты вокруг Здравствуй, мир! можно направленной tooyour домена в зоне Azure DNS при попытке tooresolve DNS-записи в «contoso.net».

## <a name="create-a-dns-zone"></a>Создание зоны DNS

1. Войдите в toohello портал Azure
1. Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.

    ![Зона DNS](./media/dns-domain-delegation/dns.png)

1. На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:

   | **Параметр** | **Значение** | **Дополнительные сведения** |
   |---|---|---|
   |**Имя**|contoso.net|Имя зоны DNS hello Hello|
   |**Подписка**|[Ваша подписка]|Выберите шлюз приложения hello toocreate подписки в.|
   |**Группа ресурсов**|**Создать:** contosoRG|Создайте группу ресурсов. Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной. Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.|
   |**Расположение**|Запад США||

> [!NOTE]
> Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS. расположение зоны DNS Hello всегда «глобальные» и не отображается.

## <a name="retrieve-name-servers"></a>Получение серверов имен

Прежде чем делегировать вашей tooAzure зоны DNS DNS, необходимо сначала tooknow hello имя сервера имен для зоны. Когда создается зона, служба DNS Azure выделяет серверы имен из пула.

1. С помощью зоны DNS hello, созданные в hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**. Нажмите кнопку hello **contoso.net** зоны DNS в hello **все ресурсы** колонку. Если подписка hello, уже содержит несколько ресурсов, можно ввести **contoso.net** в hello фильтр по имени... шлюз приложения hello доступа tooeasily поле. 

1. Получить серверы имен hello из колонки зоны DNS hello. В этом примере hello зоны «contoso.net» назначаемые серверы имен "ns1-01.azure-dns.com", «ns2-01.azure dns .net», "ns3-01.azure-dns.org", и "ns4-01.azure-dns.info":

 ![Сервер имен DNS](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS автоматически создает записи заслуживающих доверия NS в зоне содержащий hello, назначаемые серверы имен.  Имя сервера toosee hello имена через Azure PowerShell или Azure CLI, необходимо просто tooretrieve этих записей.

Hello следующие примеры также предоставляют действия hello серверы имен hello tooretrieve для зоны DNS Azure с помощью PowerShell и Azure CLI.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Следующий пример Hello — ответ hello.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>Инфраструктура CLI Azure

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Следующий пример Hello — ответ hello.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Делегат hello домена

Теперь, когда создается зона DNS hello и у вас есть серверы имен hello, hello родительский домен должен toobe обновляется hello Azure DNS-серверами. Каждый регистратор имеет свои собственные управления средств toochange hello имя сервера записи DNS для домена. На странице управления hello регистратора DNS редактирования записей NS hello и замените записей NS hello hello из них созданы Azure DNS.

При делегировании tooAzure домена DNS, необходимо использовать имена серверов имя hello, предоставляемые Azure DNS. Рекомендуется toouse все четыре имен сервера имен, независимо от того, hello имя вашего домена. Делегирование доменов не требует hello имя сервера имя toouse hello домену верхнего уровня, в домене.

Не следует использовать «делегирование» toopoint toohello Azure DNS имя сервера IP-адресов, так как эти IP-адреса может измениться в будущем. Делегирование с использованием имен серверов доменных имен в собственной зоне (также известны как серверы личных имен) в настоящее время не поддерживается в Azure DNS.

## <a name="verify-name-resolution-is-working"></a>Проверка работы разрешения имен

После завершения hello делегирование, можно проверить, что разрешение имен работает с помощью такого средства, как «nslookup» tooquery hello начальной записи для зоны (который также создается автоматически при создании зоны hello).

Нет toospecify hello Azure DNS-серверами, если делегирование hello была настроена неправильно, hello обычный DNS процесс разрешения находит серверы приветствия имен автоматически.

```
nslookup -type=SOA contoso.com
```

Hello ниже приведен пример ответа от предшествующих команда hello.

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Делегирование поддоменов в Azure DNS

Если вы хотите tooset копирование отдельной дочерней зоне, вы можете делегировать дочерний домен в Azure DNS. Например, Настройка и делегированные «contoso.net» в Azure DNS, предположим, что хотелось бы tooset копирование отдельной дочерней зоне, «partners.contoso.net».

1. Создайте дочерние зоны hello «partners.contoso.net» в Azure DNS.
2. Поиск записей заслуживающих доверия NS hello в hello дочерние зоны tooobtain hello серверы имен размещение hello дочерней зоны в Azure DNS.
3. Настройка записей NS в родительской зоне hello, указывающий toohello дочерней зоны делегировать hello дочерней зоны.

### <a name="create-a-dns-zone"></a>Создание зоны DNS

1. Войдите в toohello портал Azure
1. Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.

    ![Зона DNS](./media/dns-domain-delegation/dns.png)

1. На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:

   | **Параметр** | **Значение** | **Дополнительные сведения** |
   |---|---|---|
   |**Имя**|partners.contoso.net|Имя зоны DNS hello Hello|
   |**Подписка**|[Ваша подписка]|Выберите шлюз приложения hello toocreate подписки в.|
   |**Группа ресурсов**|**Использовать существующий:** contosoRG|Создайте группу ресурсов. Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной. Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.|
   |**Расположение**|Запад США||

> [!NOTE]
> Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS. расположение зоны DNS Hello всегда «глобальные» и не отображается.

### <a name="retrieve-name-servers"></a>Получение серверов имен

1. С помощью зоны DNS hello, созданные в hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**. Нажмите кнопку hello **partners.contoso.net** зоны DNS в hello **все ресурсы** колонку. Если подписка hello, уже содержит несколько ресурсов, можно ввести **partners.contoso.net** в hello фильтр по имени... зона DNS hello доступа tooeasily поле.

1. Получить серверы имен hello из колонки зоны DNS hello. В этом примере hello зоны «contoso.net» назначаемые серверы имен "ns1-01.azure-dns.com", «ns2-01.azure dns .net», "ns3-01.azure-dns.org", и "ns4-01.azure-dns.info":

 ![Сервер имен DNS](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS автоматически создает записи заслуживающих доверия NS в зоне содержащий hello, назначаемые серверы имен.  Имя сервера toosee hello имена через Azure PowerShell или Azure CLI, необходимо просто tooretrieve этих записей.

### <a name="create-name-server-record-in-parent-zone"></a>Создание записи сервера имен в родительской зоне

1. Перейдите toohello **contoso.net** зоны DNS в hello портал Azure.
1. Щелкните **+ Record set** (+ Набор записей).
1. На hello **добавить набор записей** колонки, введите следующие значения hello, затем щелкните **ОК**:

   | **Параметр** | **Значение** | **Дополнительные сведения** |
   |---|---|---|
   |**Имя**|partners|Имя Hello hello дочерней зоны DNS|
   |**Тип**|NS|Используйте NS для записей серверов имен.|
   |**Срок жизни**|1|Время toolive.|
   |**Единица срока жизни**|Часы|Задает toohours toolive единица времени|
   |**Сервер доменных имен**|{серверы доменных имен из зоны partners.contoso.net}|Введите все 4 hello серверы имен из partners.contoso.net зоны. |

   ![Сервер имен DNS](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Делегирование поддоменов в Azure DNS с помощью других средств

Hello ниже приведены примеры hello действия toodelegate поддоменов в Azure DNS с помощью PowerShell и интерфейс командной строки:

#### <a name="powershell"></a>PowerShell

Следующий пример PowerShell Hello показано, как это работает. Здравствуйте, одну последовательность шагов может быть выполнен через портал Azure hello, или через hello кросс платформенных Azure CLI.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Используйте `nslookup` tooverify, все настроено правильно, произведя поиск hello начальной записи зоны дочерних hello.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>Инфраструктура CLI Azure

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Получить hello серверы доменных имен для hello `partners.contoso.net` зоны hello в выходных данных.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Создайте набор записей hello и записи NS для каждого имени сервера.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Удаление всех ресурсов

toodelete все ресурсы, которые созданы в этой статье завершения hello, следующие шаги:

1. В hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**. Нажмите кнопку hello **contosorg** группа ресурсов в hello все колонки ресурсов. Если подписка hello, уже содержит несколько ресурсов, можно ввести **contosorg** в hello **фильтрация по имени...** Группа ресурсов hello доступа tooeasily поле.
1. В hello **contosorg** колонка, щелкните hello **удалить** кнопки.
1. Hello портала требуется имя hello tootype tooconfirm группы ресурсов hello, что требуется toodelete его. Тип *contosorg* hello имя группы ресурсов, нажмите кнопку **удалить**. При удалении группы ресурсов будут удалены все ресурсы в группе ресурсов hello, поэтому всегда tooconfirm убедиться, что содержимое hello группу ресурсов перед его удалением. портал Hello удаляет все ресурсы, содержащиеся в группе ресурсов hello, а затем удаляет hello самой группе ресурсов. Этот процесс занимает несколько минут.

## <a name="next-steps"></a>Дальнейшие действия

[Управление зонами DNS](dns-operations-dnszones.md)

[Управление зонами DNS](dns-operations-recordsets.md)
