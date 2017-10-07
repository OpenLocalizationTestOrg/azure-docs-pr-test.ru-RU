---
title: "aaaManage DNS-зоны в DNS Azure - Azure CLI 1.0 | Документы Microsoft"
description: "Зонами DNS можно управлять с помощью Azure CLI 1.0. В этой статье показано, как tooupdate, удалите и создайте зон DNS на Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Как toomanage зоны DNS в Azure DNS с помощью hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [Портал](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

В этом руководстве показано, как toomanage DNS-зоны с помощью hello кросс платформенных Azure CLI 1.0, которая доступна для Windows, Mac и Linux. Также можно управлять с помощью зон DNS [Azure PowerShell](dns-operations-dnszones.md) или hello портал Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.

## <a name="introduction"></a>Введение

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Получение справки

Все команды CLI 1.0 связанные tooAzure DNS начинаются с `azure network dns`. Справка доступна для каждой команды, с помощью hello `--help` параметр (Краткая форма `-h`).  Например:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зоны DNS создается с помощью hello `azure network dns zone create` команды. Чтобы получить справку, см. `azure network dns zone create -h`.

Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate зоны DNS с тегами

Hello следующем примере показано, как toocreate DNS зоны с двумя [диспетчера ресурсов Azure теги](dns-zones-records.md#tags), *проекта = Демонстрация* и *env = test*, с помощью hello `--tags` параметр (Краткая форма `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Получение зоны DNS

использовать tooretrieve зону DNS `azure network dns zone show`. Чтобы получить справку, см. `azure network dns zone show -h`.

Hello следующий пример возвращает зоны DNS hello *contoso.com* и связанные с ним данные из группы ресурсов *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Следующий пример Hello — ответ hello.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Обратите внимание, что записи DNS не возвращаются командой `azure network dns zone show`. toolist DNS-записи, используйте `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Перечисление зон DNS

использовать tooenumerate зон DNS, `azure network dns zone list`. Чтобы получить справку, см. `azure network dns zone list -h`.

Указание группы ресурсов hello перечислены только те зоны в группе ресурсов hello.

```azurecli
azure network dns zone list MyResourceGroup
```

Пропуск группы ресурсов hello список всех зон в подписке hello:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Обновление зоны DNS

Изменения tooa ресурсов зоны DNS можно при помощи `azure network dns zone set`. Чтобы получить справку, см. `azure network dns zone set -h`.

Эта команда не обновляет hello наборы записей DNS в зоне hello (см. [как DNS-записи tooManage](dns-operations-recordsets-cli-nodejs.md)). Это свойства только используемые tooupdate сам ресурс hello зоны. Эти свойства доступны в настоящее время составляет toohello [диспетчера ресурсов Azure «теги»](dns-zones-records.md#tags) для ресурса зоны hello.

Hello следующем примере показано, как tooupdate hello тегов в зоне DNS. существующие теги Hello заменяются указано значение hello.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Удаление зоны DNS

Зоны DNS можно удалить с помощью команды `azure network dns zone delete`. Чтобы получить справку, см. `azure network dns zone delete -h`.

> [!NOTE]
> Зоны DNS при удалении также удаляются все записи DNS в зоне hello. Эту операцию нельзя отменить. Если зона DNS hello, службы, используя зоны hello сможет hello зона удаляется.
>
>tooprotect от зоны случайного удаления, в разделе [как tooprotect DNS-зоны и записывает](dns-protect-zones-recordsets.md).

Эта команда запрашивает подтверждение. Необязательный Hello `--quiet` переключения (Краткая форма `-q`) отключает это предупреждение.

Hello следующем примере показано, как toodelete hello зоны *contoso.com* из группы ресурсов *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[управления наборов записей и записи](dns-getstarted-create-recordset-cli-nodejs.md) в зоне DNS.

Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).

