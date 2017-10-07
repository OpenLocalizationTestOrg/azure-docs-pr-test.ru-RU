---
title: "Здравствуйте, aaaManage DNS-записей в Azure DNS с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Управляйте наборами записей и записями DNS в службе Azure DNS при размещении вашего домена в Azure DNS. Все команды CLI 1.0 для операций с наборами записей и записями."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>Управление записями DNS в Azure DNS с помощью hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [Портал Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

В этой статье показано, как toomanage записи DNS для зоны DNS с помощью hello кросс платформенных Azure командной строки (CLI), которое доступно для Windows, Mac и Linux. Также можно управлять с помощью DNS-записей [Azure PowerShell](dns-operations-recordsets.md) или hello [портал Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.

Hello в этой статье примерах уже имеется [hello Azure CLI 1.0 вход и создали зоны DNS](dns-operations-dnszones-cli-nodejs.md).

## <a name="introduction"></a>Введение

Прежде чем создавать DNS-записи в Azure DNS, необходимо сначала toounderstand как Azure DNS организует DNS-записей в наборы записей DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Создание записи DNS

запись DNS toocreate использовать hello `azure network dns record-set add-record` команды. Чтобы получить справку, см. `azure network dns record-set add-record -h`.

При создании записи, необходимо, чтобы имя группы ресурсов hello toospecify имя зоны, имя, тип записи hello и hello подробные сведения о записи hello набор записей. Hello имя набора записей должно быть *относительный* имя, то есть его необходимо исключить hello имя зоны.

Набор записей hello еще не существует, эта команда создает для вас. Если набор записей hello уже существует, добавьте это команда hello запись, укажите toohello существующего набора записей.

При создании набора записей используется срок жизни (TTL) по умолчанию — 3600. Инструкции по toouse различных TTLs статье [создать набор записей DNS](#create-a-dns-record-set).

Hello следующий пример создает запись называется *www* в зоне hello *contoso.com* в группе ресурсов hello *MyResourceGroup*. Здравствуйте, IP-адрес hello запись — *1.2.3.4*.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

toocreate записью в вершине зоны hello hello (в данном случае «contoso.com»), используйте имя записи hello «@», кавычками hello:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Создание набора записей DNS

В hello выше примеры hello DNS-запись была либо добавлены tooan существующего набора записей или был создан набор записей hello *неявно*. Также можно создать набор записей hello *явно* до добавления записывает tooit. Azure DNS поддерживает «empty» наборы записей, которые может выступать в качестве tooreserve заполнитель DNS-имя перед созданием записи DNS. Пустые наборы записей, отображаются в hello Azure DNS панели управления, но не отображаются в hello Azure DNS-серверами.

Наборы записей создаются с помощью hello `azure network dns record-set create` команды. Чтобы получить справку, см. `azure network dns record-set create -h`.

Создание записи hello задано явным образом позволяет toospecify свойства набора записей, такие как hello [срока жизни (TTL)](dns-zones-records.md#time-to-live) и метаданные. [Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".

Hello следующем примере создается пустой записи устанавливается со сроком ЖИЗНИ 60 секунд, с помощью hello `--ttl` параметра (Краткая форма `-l`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

Hello следующий пример создает записей с две записи метаданных» dept = finance» и «среды = рабочей», с помощью hello `--metadata` параметр (Краткая форма `-m`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

После создания пустого набора записей в него можно добавить записи с помощью команды `azure network dns record-set add-record`, как описано в разделе [Создание записи DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Создание записей других типов

Рассматривать подробно порядок записей toocreate «A» hello, в следующих примерах показано, как запись toocreate других типов записи поддерживается службой Azure DNS.

использовать параметры Hello toospecify hello записи данных зависит от типа hello hello записи. Например, для записи типа «A», можно указать hello IPv4-адрес с параметром hello `-a <IPv4 address>`. Здравствуйте параметров для каждого типа записи могут быть перечислены с помощью `azure network dns record-set add-record -h`.

В каждом случае показано, как toocreate отдельную запись. Hello запись будет добавлена toohello существующего набора записей или неявно создан набор записей. Дополнительные сведения о создании наборов записей и явной настройке параметра набора см. в разделе [Создание набора записей DNS](#create-a-dns-record-set).

Мы не предоставляем toocreate примере SOA набор записей, так как создаются SOA и удалены вместе с каждой зоны DNS и не удается создать или удалить отдельно. Тем не менее [SOA могут быть изменены, как показано в пример hello](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Создание записи типа AAAA

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Создание записи CNAME

> [!NOTE]
> Hello стандартах DNS не допускают записи CNAME на вершине hello зоны (`-Name "@"`), и не следует разрешать или запрещать наборы записей, содержащая более одной записи.
> 
> Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Создание записи типа MX

В этом примере мы используем имя набора записей hello «@» hello toocreate MX-записи на вершине зоны hello (в данном случае «contoso.com»).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Создание записи типа NS

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Создание записи типа PTR

В этом случае "my-arpa-zone.com" представляет hello зоны ARPA, представляющий ваш диапазон IP-адресов. Каждая запись PTR в этой зоне соответствует tooan IP-адрес в этот диапазон IP-адресов.  Имя записи Hello "10" представляет hello последний октет hello IP-адрес в этот диапазон IP-адресов, представленного данной записью.

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Создание записи типа SRV

При создании [набор записей типа SRV](dns-zones-records.md#srv-records), укажите hello  *\_службы* и  *\_протокола* в hello имя набора записей. Нет нет необходимости tooinclude «@» в hello запись имя набора при создании записи SRV набора в вершине зоны hello.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>Создание записи типа TXT

Hello следующем примере показано, как записать toocreate TXT. Дополнительные сведения о hello Максимальная длина строки поддерживается в записи TXT в разделе [записи TXT](dns-zones-records.md#txt-records).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>Получение набора записей

использовать существующий набор записей, tooretrieve `azure network dns record-set show`. Чтобы получить справку, см. `azure network dns record-set show -h`.

При создании записи или набора записей записи hello задать имя, присвоенное должен быть *относительный* имя, то есть его необходимо исключить hello имя зоны. Требуется тип записи toospecify hello, hello зоны, содержащей записи hello задать и hello группы ресурсов, содержащую зону hello.

Hello следующий пример извлекает записи hello *www* типа a из зоны *contoso.com* в группе ресурсов *MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>Перечисление наборов записей

Список всех записей в зоне DNS можно с помощью hello `azure network dns record-set list` команды. Чтобы получить справку, см. `azure network dns record-set list -h`.

Этот пример возвращает задает все записи в зоне hello *contoso.com*, в группе ресурсов *MyResourceGroup*, независимо от того, имя или тип записи:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

Этот пример возвращает все наборы записей, которые соответствуют hello данного типа записи (в данном случае записи 'A'):

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>Добавление записей tooan существующего набора записей

Можно использовать `azure network dns record-set add-record` как toocreate записи в новой записи или tooadd существующую запись tooan записей.

Дополнительные сведения см. в разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types) выше.

## <a name="remove-a-record-from-an-existing-record-set"></a>Удаление записи из существующего набора записей

запись tooremove DNS из существующего набора записей, используйте `azure network dns record-set delete-record`. Чтобы получить справку, см. `azure network dns record-set delete-record -h`.

Эта команда удаляет запись DNS из набора записей. При удалении hello последней записи в наборе записей — набора сам записей hello **не** удалены. В таком случае набор записей будет пустым. см. Вместо этого набора записей hello toodelete [удалить набор записей](#delete-a-record-set).

Требуется toospecify записей toobe hello удален и hello зоны, он должен быть удален из, с помощью hello такими же параметрами, при создании записи с помощью `azure network dns record-set add-record`. Эти параметры описаны в предыдущих разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types).

Эта команда запрашивает подтверждение. Это предупреждение можно подавить при помощи hello `--quiet` переключения (Краткая форма `-q`).

Следующий пример удаляет Hello hello запись со значением "1.2.3.4» из записи hello набор *www* в зоне hello *contoso.com*, в группе ресурсов hello *MyResourceGroup*. запрос подтверждения Hello подавляется.

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>Обновление существующего набора записей

В каждом наборе записей указан [срок жизни](dns-zones-records.md#time-to-live), [метаданные](dns-zones-records.md#tags-and-metadata) и записи DNS. Hello следующих разделах объясняется, как toomodify каждого из этих свойств.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify запись A, AAAA, MX, NS, SRV, PTR или TXT

toomodify существующую запись типа A, AAAA, MX, NS, SRV, PTR или TXT, сначала следует добавить новую запись и удаление существующей записи hello. Подробные инструкции о том, как toodelete и добавьте записи см. в разделе hello в предыдущих разделах данной статьи.

Hello в следующем примере показано, как запись «A» из tooIP IP адрес 1.2.3.4 toomodify устранить 5.6.7.8:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify запись CNAME

Используйте toomodify запись CNAME `azure network dns record-set add-record` tooadd hello новое значение записи. В отличие от других типов записей, набор записей CNAME может содержать только одну запись. Таким образом, является существующей записи hello *заменить* при добавляется новая запись hello и не требует toobe удалена отдельно.  Вам будет запрашиваемые tooaccept Эта замена.

Hello пример изменяет набор записей типа CNAME hello *www* в зоне hello *contoso.com*, в группе ресурсов *MyResourceGroup*, toopoint слишком «www.fabrikam.net» вместо его существующее значение:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify записи SOA

Используйте `azure network dns record-set set-soa-record` toomodify hello SOA для данной зоны DNS. Чтобы получить справку, см. `azure network dns record-set set-soa-record -h`.

Hello следующем примере показано, как свойство tooset hello «электронная почта» hello начальной записи зоны hello *contoso.com* в группе ресурсов hello *MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>записей toomodify NS на вершине зоны hello

запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS. Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.

Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS. Можно также изменить hello TTL и метаданные для этого набора записей. Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.

Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello. Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.

Привет, в следующем примере показано, как tooadd запись NS toohello дополнительное имя сервера задать на вершине зоны hello:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>задать hello toomodify TTL существующей записи

задать hello toomodify TTL существующей записи, используйте `azure network dns record-set set`. Чтобы получить справку, см. `azure network dns record-set set -h`.

Hello в следующем примере показано, как toomodify набора записей TTL, в этом случае too60 секунд:

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify hello метаданных из существующего набора записей

[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение". задать toomodify hello метаданных из существующей записи, используйте `azure network dns record-set set`. Чтобы получить справку, см. `azure network dns record-set set -h`.

Hello следующем примере показано, как toomodify набор записей с две записи метаданных» dept = finance» и «среды = рабочей», с помощью hello `--metadata` параметра (Краткая форма `-m`). Обратите внимание, что все существующие метаданные *заменить* по заданным значениям hello.

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>Удаление набора записей

Наборы записей можно удалить с помощью hello `azure network dns record-set delete` команды. Чтобы получить справку, см. `azure network dns record-set delete -h`. При удалении набора записей также удаляются все записи в наборе записей hello.

> [!NOTE]
> Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (`-Name "@"`).  Эти отчеты создаются автоматически при hello зона была создана и автоматически удаляются при удалении hello зоны.

Hello следующий пример удаляет набор именованных записей hello *www* типа a из зоны hello *contoso.com* в группе ресурсов *MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

Все операции удаления запрашиваемые tooconfirm hello. Этот запрос toosuppress использовать hello `--quiet` переключения (Краткая форма `-q`).

## <a name="next-steps"></a>Дальнейшие действия

См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).
<br>
Узнайте, каким образом слишком[защиты зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.
