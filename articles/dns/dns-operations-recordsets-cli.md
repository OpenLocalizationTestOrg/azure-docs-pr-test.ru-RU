---
title: "Здравствуйте, aaaManage DNS-записей в Azure DNS с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Управляйте наборами записей и записями DNS в службе Azure DNS при размещении вашего домена в Azure DNS. Все команды CLI 2.0 для операций с наборами записей и записями."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a>Управление DNS-записи и наборов записей в Azure DNS, с помощью Azure CLI 2.0 hello

> [!div class="op_single_selector"]
> * [Портал Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

В этой статье показано, как toomanage записи DNS для зоны DNS с помощью hello кросс платформенных Azure командной строки (CLI) 2.0, которое доступно для Windows, Mac и Linux. Также можно управлять с помощью DNS-записей [Azure PowerShell](dns-operations-recordsets.md) или hello [портал Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.

Hello в этой статье примерах уже имеется [hello Azure CLI 2.0, вход и создали зоны DNS](dns-operations-dnszones-cli.md).

## <a name="introduction"></a>Введение

Прежде чем создавать DNS-записи в Azure DNS, необходимо сначала toounderstand как Azure DNS организует DNS-записей в наборы записей DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Создание записи DNS

toocreate запись DNS использовать hello `az network dns record-set <record-type> set-record` команду (где `<record-type>` является hello типа записи, т. е. a, srv, txt и т. д.). Чтобы получить справку, см. `az network dns record-set --help`.

При создании записи, необходимо, чтобы имя группы ресурсов hello toospecify имя зоны, имя, тип записи hello и hello подробные сведения о записи hello набор записей. Hello имя набора записей должно быть *относительный* имя, то есть его необходимо исключить hello имя зоны.

Набор записей hello еще не существует, эта команда создает для вас. Если существует запись hello уже настроено, эта команда добавляет запись hello, укажите toohello существующего набора записей.

При создании набора записей используется срок жизни (TTL) по умолчанию — 3600. Инструкции по toouse различных TTLs статье [создать набор записей DNS](#create-a-dns-record-set).

Hello следующий пример создает запись называется *www* в зоне hello *contoso.com* в группе ресурсов hello *MyResourceGroup*. Здравствуйте, IP-адрес hello запись — *1.2.3.4*.

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

задать toocreate запись в вершине зоны hello hello (в этом случае «contoso.com»), используйте имя записи hello, «@», кавычками hello:

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Создание набора записей DNS

В hello выше примеры hello DNS-запись была либо добавлены tooan существующего набора записей или был создан набор записей hello *неявно*. Также можно создать набор записей hello *явно* до добавления записывает tooit. Azure DNS поддерживает «empty» наборы записей, которые может выступать в качестве tooreserve заполнитель DNS-имя перед созданием записи DNS. Пустые наборы записей, отображаются в hello Azure DNS панели управления, но не отображаются в hello Azure DNS-серверами.

Наборы записей создаются с помощью hello `az network dns record-set <record-type> create` команды. Чтобы получить справку, см. `az network dns record-set <record-type> create --help`.

Создание записи hello задано явным образом позволяет toospecify свойства набора записей, такие как hello [срока жизни (TTL)](dns-zones-records.md#time-to-live) и метаданные. [Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".

Hello следующем примере создается пустой набор записей типа «A» со сроком ЖИЗНИ 60 секунд, с помощью hello `--ttl` параметра (Краткая форма `-l`):

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

Hello следующий пример создает записей с две записи метаданных» dept = finance» и «среды = рабочей», с помощью hello `--metadata` параметр:

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

После создания пустого набора записей в него можно добавить записи с помощью команды `azure network dns record-set <record-type> set-record`, как описано в разделе [Создание записи DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Создание записей других типов

Рассматривать подробно порядок записей toocreate «A» hello, в следующих примерах показано, как запись toocreate других типов записи поддерживается службой Azure DNS.

использовать параметры Hello toospecify hello записи данных зависит от типа hello hello записи. Например, для записи типа «A», можно указать hello IPv4-адрес с параметром hello `--ipv4-address <IPv4 address>`. Здравствуйте параметров для каждого типа записи могут быть перечислены с помощью `az network dns record-set <record-type> set-record --help`.

В каждом случае показано, как toocreate отдельную запись. Hello запись будет добавлена toohello существующего набора записей или неявно создан набор записей. Дополнительные сведения о создании наборов записей и явной настройке параметра набора см. в разделе [Создание набора записей DNS](#create-a-dns-record-set).

Мы не предоставляем toocreate примере SOA набор записей, так как создаются SOA и удалены вместе с каждой зоны DNS и не удается создать или удалить отдельно. Тем не менее [SOA могут быть изменены, как показано в пример hello](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Создание записи типа AAAA

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Создание записи CNAME

> [!NOTE]
> Hello стандартах DNS не допускают записи CNAME на вершине hello зоны (`--Name "@"`), и не следует разрешать или запрещать наборы записей, содержащая более одной записи.
> 
> Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Создание записи типа MX

В этом примере мы используем имя набора записей hello «@» hello toocreate MX-записи на вершине зоны hello (в данном случае «contoso.com»).

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Создание записи типа NS

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Создание записи типа PTR

В этом случае "my-arpa-zone.com" представляет hello зоны ARPA, представляющий ваш диапазон IP-адресов. Каждая запись PTR в этой зоне соответствует tooan IP-адрес в этот диапазон IP-адресов.  Имя записи Hello "10" представляет hello последний октет hello IP-адрес в этот диапазон IP-адресов, представленного данной записью.

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a>Создание записи типа SRV

При создании [набор записей типа SRV](dns-zones-records.md#srv-records), укажите hello  *\_службы* и  *\_протокола* в hello имя набора записей. Нет нет необходимости tooinclude «@» в hello запись имя набора при создании записи SRV набора в вершине зоны hello.

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a>Создание записи типа TXT

Hello следующем примере показано, как записать toocreate TXT. Дополнительные сведения о hello Максимальная длина строки поддерживается в записи TXT в разделе [записи TXT](dns-zones-records.md#txt-records).

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a>Получение набора записей

использовать существующий набор записей, tooretrieve `az network dns record-set <record-type> show`. Чтобы получить справку, см. `az network dns record-set <record-type> show --help`.

При создании записи или набора записей записи hello задать имя, присвоенное должен быть *относительный* имя, то есть его необходимо исключить hello имя зоны. Требуется тип записи toospecify hello, hello зоны, содержащей записи hello задать и hello группы ресурсов, содержащую зону hello.

Hello следующий пример извлекает записи hello *www* типа a из зоны *contoso.com* в группе ресурсов *MyResourceGroup*:

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a>Перечисление наборов записей

Список всех записей в зоне DNS можно с помощью hello `az network dns record-set list` команды. Чтобы получить справку, см. `az network dns record-set list --help`.

Этот пример возвращает задает все записи в зоне hello *contoso.com*, в группе ресурсов *MyResourceGroup*, независимо от того, имя или тип записи:

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

Этот пример возвращает все наборы записей, которые соответствуют hello данного типа записи (в данном случае записи 'A'):

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a>Добавление записей tooan существующего набора записей

Можно использовать `az network dns record-set <record-type> set-record` как toocreate записи в новой записи или tooadd существующую запись tooan записей.

Дополнительные сведения см. в разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types) выше.

## <a name="remove-a-record-from-an-existing-record-set"></a>Удаление записи из существующего набора записей

запись tooremove DNS из существующего набора записей, используйте `az network dns record-set <record-type> remove-record`. Чтобы получить справку, см. `az network dns record-set <record-type> remove-record -h`.

Эта команда удаляет запись DNS из набора записей. При удалении hello последней записи в наборе записей набора сам записей hello также удаляется. набор пустой записей hello tookeep используйте hello `--keep-empty-record-set` параметр.

Требуется toospecify записей toobe hello удален и hello зоны, он должен быть удален из, с помощью hello такими же параметрами, при создании записи с помощью `az network dns record-set <record-type> set-record`. Эти параметры описаны в предыдущих разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types).

Следующий пример удаляет Hello hello запись со значением "1.2.3.4» из записи hello набор *www* в зоне hello *contoso.com*, в группе ресурсов hello *MyResourceGroup*.

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a>Обновление существующего набора записей

В каждом наборе записей указан [срок жизни](dns-zones-records.md#time-to-live), [метаданные](dns-zones-records.md#tags-and-metadata) и записи DNS. Hello следующих разделах объясняется, как toomodify каждого из этих свойств.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify запись A, AAAA, MX, NS, SRV, PTR или TXT

toomodify существующую запись типа A, AAAA, MX, NS, SRV, PTR или TXT, сначала следует добавить новую запись и удаление существующей записи hello. Подробные инструкции о том, как toodelete и добавьте записи см. в разделе hello в предыдущих разделах данной статьи.

Hello в следующем примере показано, как запись «A» из tooIP IP адрес 1.2.3.4 toomodify устранить 5.6.7.8:

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

Нельзя добавлять, удалять или изменять hello записи автоматически создается набор на вершине зоны hello записей NS hello (`--Name "@"`, включая кавычки). Для этого набора записей hello допускается могут только запись hello toomodify набор TTL, а также метаданные.

### <a name="toomodify-a-cname-record"></a>toomodify запись CNAME

В отличие от большинства других типов записей, набор записей CNAME может содержать только одну запись.  Таким образом невозможно заменить текущее значение hello, добавив новую запись и удаление существующей записи hello, как и для других типов записей.

Вместо этого используйте toomodify запись CNAME `az network dns record-set cname set-record`. Чтобы получить справку, см. `az network dns record-set cname set-record --help`.

Hello пример изменяет набор записей типа CNAME hello *www* в зоне hello *contoso.com*, в группе ресурсов *MyResourceGroup*, toopoint слишком «www.fabrikam.net» вместо его существующее значение:

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify записи SOA

В отличие от большинства других типов записей, набор записей CNAME может содержать только одну запись.  Таким образом невозможно заменить текущее значение hello, добавив новую запись и удаление существующей записи hello, как и для других типов записей.

Вместо этого используйте toomodify hello начальной записи `az network dns record-set soa update`. Чтобы получить справку, см. `az network dns record-set soa update --help`.

Hello следующем примере показано, как свойство tooset hello «электронная почта» hello начальной записи зоны hello *contoso.com* в группе ресурсов hello *MyResourceGroup*:

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>записей toomodify NS на вершине зоны hello

запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS. Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.

Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS. Можно также изменить hello TTL и метаданные для этого набора записей. Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.

Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello. Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.

Привет, в следующем примере показано, как tooadd запись NS toohello дополнительное имя сервера задать на вершине зоны hello:

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>задать hello toomodify TTL существующей записи

задать hello toomodify TTL существующей записи, используйте `azure network dns record-set <record-type> update`. Чтобы получить справку, см. `azure network dns record-set <record-type> update --help`.

Hello в следующем примере показано, как toomodify набора записей TTL, в этом случае too60 секунд:

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify hello метаданных из существующего набора записей

[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение". задать toomodify hello метаданных из существующей записи, используйте `az network dns record-set <record-type> update`. Чтобы получить справку, см. `az network dns record-set <record-type> update --help`.

Hello следующем примере показано, как toomodify набор записей с две записи метаданных «dept = процент» и «среды = производства». Обратите внимание, что все существующие метаданные *заменить* по заданным значениям hello.

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a>Удаление набора записей

Наборы записей можно удалить с помощью hello `az network dns record-set <record-type> delete` команды. Чтобы получить справку, см. `azure network dns record-set <record-type> delete --help`. При удалении набора записей также удаляются все записи в наборе записей hello.

> [!NOTE]
> Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (`--name "@"`).  Эти отчеты создаются автоматически при hello зона была создана и автоматически удаляются при удалении hello зоны.

Hello следующий пример удаляет набор именованных записей hello *www* типа a из зоны hello *contoso.com* в группе ресурсов *MyResourceGroup*:

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

Все операции удаления запрашиваемые tooconfirm hello. Этот запрос toosuppress использовать hello `--yes` переключения.

## <a name="next-steps"></a>Дальнейшие действия

См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).
<br>
Узнайте, каким образом слишком[защиты зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.
