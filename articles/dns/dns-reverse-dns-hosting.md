---
title: "aaaHosting DNS зоны обратного просмотра в Azure DNS | Документы Microsoft"
description: "Узнайте, как hello toohost toouse Azure DNS DNS зоны обратного просмотра для диапазонов IP-"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Размещение зон обратного просмотра DNS в Azure DNS

В этой статье объясняется, как toohost hello DNS зоны обратного просмотра для назначенных диапазонов IP-в Azure DNS. Hello диапазоны IP-адресов, представленный зоны обратного просмотра hello должны быть назначены организации tooyour обычно поставщиком услуг Интернета.

tooconfigure обратного просмотра DNS для принадлежащие Azure IP-адреса, назначенного tooyour службы Azure см. в разделе [Настройка hello обратного просмотра для IP-адреса hello выделяются tooyour службы Azure](dns-reverse-dns-for-azure-services.md).

Перед прочтением этой статьи ознакомьтесь со статьей [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).

В этой статье описывается toocreate действия hello вашей первой зоны обратного просмотра DNS и запись с помощью hello портал Azure, Azure PowerShell, CLI Azure 1.0 или Azure CLI 2.0.

## <a name="create-a-reverse-lookup-dns-zone"></a>Создание зоны обратного просмотра DNS

1. Войдите в toohello [портал Azure](https://portal.azure.com)
1. Hello концентратора меню и нажмите кнопку **New** > **сети** > и нажмите кнопку **зоны DNS** tooopen hello **создать DNS-зоны**колонку.

   ![Зона DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. На hello **создать DNS-зоны** колонке имя вашей зоны DNS. Имя зоны hello Hello сконструированных по-разному для IPv4 и IPv6 префиксов. Используйте либо hello инструкции для [IPV4](#ipv4) или [IPv6](#ipv6) tooname зоны. По завершении нажмите кнопку **создать** toocreate hello зоны.

### <a name="ipv4"></a>IPv4

Имя зоны обратного просмотра IPv4 Hello основан на диапазон IP-адресов hello, которое он представляет. Он должен находиться в hello следующий формат: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Примеры см. в [обзоре записей в обратной зоне DNS и поддержки в Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> При создании classless зоны обратного просмотра DNS в Azure DNS, необходимо использовать дефис (`-`) вместо косой черты («/») в имени зоны hello.
>
> Например, для 192.0.2.128/26 диапазон hello IP, необходимо использовать `128-26.2.0.192.in-addr.arpa` имени зоны hello вместо `128/26.2.0.192.in-addr.arpa`.
>
> Это происходит потому, что хотя оба поддерживаются стандартами DNS hello, зоны DNS, имена, содержащие hello косой черты (`/`) символ, не поддерживаются в Azure DNS.

Hello следующем примере показано, как toocreate «Класс C» обратная зона DNS с именем `2.0.192.in-addr.arpa` в Azure DNS через портал Azure hello:

 ![Создание зоны DNS](./media/dns-reverse-dns-hosting/figure2.png)

Hello «Расположение группы ресурсов» определяет hello расположение группы ресурсов hello и не оказывает влияния на hello зоны DNS. расположение зоны DNS Hello всегда «global» и не отображается.

Hello следующих примерах показано, как toocomplete это задач с помощью Azure PowerShell и hello Azure CLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Hello имя зоны обратного просмотра IPv6 должно быть в hello следующие формы: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Примеры см. в [обзоре записей в обратной зоне DNS и поддержки в Azure](dns-reverse-dns-overview.md#ipv6).


Hello следующем примере показано, как toocreate зоне уточняющего запроса DNS обратного просмотра IPv6 именоваться `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` в Azure DNS через портал Azure hello:

 ![Создание зоны DNS](./media/dns-reverse-dns-hosting/figure3.png)

Hello «Расположение группы ресурсов» определяет hello расположение группы ресурсов hello и не оказывает влияния на hello зоны DNS. расположение зоны DNS Hello всегда «global» и не отображается.

Hello следующих примерах показано, как toocomplete это задач с помощью Azure PowerShell и hello Azure CLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>Azure CLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>Azure CLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Делегирование зоны обратного просмотра DNS

После создания вашего обратного просмотра зоны DNS, необходимо убедиться, что этой зоны hello делегирования в родительской зоне hello. Делегирование DNS позволяет hello DNS-имя разрешения процесса toofind hello серверами размещения вашего обратного просмотра зоны DNS. Это позволяет этих имя серверов tooanswer обратных запросов DNS для hello IP-адреса в диапазоне адресов.

Для зоны прямого просмотра делегирование зоны DNS hello процесс описан в [делегировать tooAzure вашего домена DNS](dns-delegate-domain-azure-dns.md). Делегирование для зоны обратного просмотра работает hello таким же образом. Hello отличается только необходимость серверы имен hello tooconfigure с hello поставщика услуг Интернета, предоставившего вашей диапазон IP-адресов, вместо регистратора доменных имен.

## <a name="create-a-dns-ptr-record"></a>Создание записи DNS типа PTR

### <a name="ipv4"></a>IPv4

Hello в примере описывается процесс создания записи PTR в зону обратного просмотра DNS в Azure DNS hello. Для других типов записей и toomodify существующих записей в разделе [Управление DNS-записи и наборы записей с помощью hello портал Azure](dns-operations-recordsets-portal.md).

1.  Вверху hello hello **зоны DNS** колонке выберите **+ запись набора** tooopen hello **добавить набор записей** колонку.

 ![Зона DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. На hello **добавить набор записей** колонку. 
1. Выберите **PTR** из записи hello»**тип**» меню.  
1. Hello имя набора записей hello для PTR-запись должна toobe hello остальной части hello IPv4-адрес в обратном порядке. В этом примере hello первые три октета уже заполнены как часть имени зоны hello (.2.0.192). Таким образом только последний октет hello содержится в поле имени hello. Например, для ресурса с IP-адресом 192.0.2.15 можно назвать набор записей **15**.  
1. В hello»**доменное имя**» введите hello полное доменное имя (FQDN) использует hello IP-адрес ресурса hello.
1. Выберите **ОК** hello нижней части колонки toocreate hello hello-запись DNS.

 ![Добавление набора записей](./media/dns-reverse-dns-hosting/figure5.png)

Hello ниже приведены примеры, демонстрирующие toocomplete этой задачи с помощью PowerShell и hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>Azure CLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>Azure CLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Следующий пример Hello помогает выполнить процесс создания новой записи «PTR» hello. Для других типов записей и toomodify существующих записей в разделе [Управление DNS-записи и наборы записей с помощью hello портал Azure](dns-operations-recordsets-portal.md).

1. Вверху hello hello **колонке зоны DNS**выберите **+ запись набора** tooopen hello **добавить набор записей** колонку.

  ![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. На hello **добавить набор записей** колонку. 
3. Выберите **PTR** из записи hello»**тип**» меню.  
4. Hello имя набора записей hello для PTR-запись должна toobe hello остальной части hello IPv6-адрес в обратном порядке. Сжатие за счет нулей не должно использоваться. В этом примере hello первых 64 бит hello IPv6 уже заполнены как часть имени зоны hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). Таким образом в поле имя hello предоставляются только hello последние 64 бита. Hello последние 64 бита hello IP-адресов вводятся в обратном порядке, с помощью точки в качестве разделителя hello между каждое шестнадцатеричное число. Например, для ресурса с IP-адресом 2001:0db8:abdc:0000:f524:10bc:1af9:405e набор записей можно назвать **e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**.  
5. В hello»**доменное имя**» введите hello полное доменное имя (FQDN) использует hello IP-адрес ресурса hello.
6. Выберите **ОК** hello нижней части колонки toocreate hello hello-запись DNS.

![Колонка добавления набора записей](./media/dns-reverse-dns-hosting/figure7.png)

Hello ниже приведены примеры, демонстрирующие toocomplete этой задачи с помощью PowerShell и hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>Azure CLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>Azure CLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Просмотр записей

tooview hello записи, которые вы создали перейдите tooyour зоны DNS в hello портал Azure. В hello понизить часть hello **зоны DNS** колонку, вы увидите hello записей для DNS-зоны hello. Вы увидите hello по умолчанию записи NS и SOA, которые создаются в каждой зоне, а также любые новые записи, который был создан.

### <a name="ipv4"></a>IPv4

Колонка зоны DNS с записями IPv4 типа PTR:

![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure8.png)

Hello следующие примеры Показать порядок tooview hello PTR записей с помощью PowerShell или Azure CLI hello:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Колонка зоны DNS с записями IPv6 типа PTR:

![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure9.png)

Hello ниже приведены примеры на порядок tooview hello записей с помощью PowerShell и hello AzureCLI.

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>Часто задаваемые вопросы

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>Можно ли разместить зоны обратного просмотра DNS для блоков IP-адресов, назначенных поставщиком услуг Интернета, в DNS Azure?

Да. Полностью поддерживается размещение hello зоны обратного просмотра (ARPA) для диапазонов IP-в Azure DNS.

Создание зоны обратного просмотра hello в Azure DNS, как описано в этой статье, а затем работать с поставщиком услуг Интернета, слишком[зоны hello делегат](dns-domain-delegation.md).  Затем можно будет управлять hello PTR-записей для каждого обратного просмотра в hello так же, как другие типов записей.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>Сколько стоит размещение зоны обратного просмотра DNS?

Размещение hello зоны обратного просмотра DNS для вашей услуг Интернета IP-блоков в Azure DNS оплачивается по [стандартные тарифы Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Можно ли разместить в Azure DNS зоны обратного просмотра DNS для адресов IPv4 и IPv6?

Да. В этой статье объясняется, как toocreate IPv4 и IPv6 DNS зоны обратного просмотра в Azure DNS.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>Можно ли импортировать существующую зону обратного просмотра DNS?

Да. Можно использовать существующие зон DNS hello Azure CLI tooimport в Azure DNS. Он работает как с зонами прямого просмотра, так и с зонами обратного просмотра.

Дополнительные сведения см. в разделе [импорта и экспорта в файл зоны DNS с помощью hello Azure CLI](dns-import-export.md).

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. [в статье Википедии об обратном просмотре DNS](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Узнайте, каким образом слишком[управление обратного DNS-записи для служб Azure](dns-reverse-dns-for-azure-services.md).
