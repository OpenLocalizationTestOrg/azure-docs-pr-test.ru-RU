---
title: "aaaManage DNS-зоны в DNS Azure - CLI Azure 2.0 | Документы Microsoft"
description: "Зонами DNS можно управлять с помощью Azure CLI 2.0. В этой статье показано, как tooupdate, удалите и создайте зон DNS на Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Как toomanage зоны DNS в Azure DNS с помощью hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Портал](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


В этом руководстве показано, как toomanage DNS-зоны с помощью hello кросс платформенных Azure CLI, который доступен для Windows, Mac и Linux. Также можно управлять с помощью зон DNS [Azure PowerShell](dns-operations-dnszones.md) или hello портал Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.

## <a name="introduction"></a>Введение

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Настройка Azure CLI 2.0 для Azure DNS

### <a name="before-you-begin"></a>Перед началом работы

Проверьте наличие следующих элементов перед началом настройки hello.

* Подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).

* Установить последнюю версию hello hello Azure 2.0 CLI, доступные для Windows, Linux или MAC. Дополнительные сведения можно найти по адресу [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Войдите в tooyour учетная запись Azure

Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных. Дополнительные сведения см. в журнале в tooAzure из hello Azure CLI

```
az login
```

### <a name="select-hello-subscription"></a>Выберите подписку hello

Проверьте hello подписки для учетной записи hello.

```
az account list
```

Выберите, какие toouse вашей подписки Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов. Тем не менее так как все ресурсы DNS глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на Azure DNS.

Если используется существующая группа ресурсов, можно пропустить этот шаг.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Получение справки

Все команды CLI 2.0, относящихся tooAzure DNS начинаются с `az network dns`. Справка доступна для каждой команды, с помощью hello `--help` параметр (Краткая форма `-h`).  Например:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зоны DNS создается с помощью hello `az network dns zone create` команды. Чтобы получить справку, см. `az network dns zone create -h`.

Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate зоны DNS с тегами

Hello следующем примере показано, как toocreate DNS зоны с двумя [диспетчера ресурсов Azure теги](dns-zones-records.md#tags), *проекта = Демонстрация* и *env = test*, с помощью hello `--tags` параметр (Краткая форма `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Получение зоны DNS

использовать tooretrieve зону DNS `az network dns zone show`. Чтобы получить справку, см. `az network dns zone show --help`.

Hello следующий пример возвращает зоны DNS hello *contoso.com* и связанные с ним данные из группы ресурсов *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Следующий пример Hello — ответ hello.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Обратите внимание, что записи DNS не возвращаются командой `az network dns zone show`. toolist DNS-записи, используйте `az network dns record-set list`.


## <a name="list-dns-zones"></a>Перечисление зон DNS

использовать tooenumerate зон DNS, `az network dns zone list`. Чтобы получить справку, см. `az network dns zone list --help`.

Указание группы ресурсов hello перечислены только те зоны в группе ресурсов hello.

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Пропуск группы ресурсов hello список всех зон в подписке hello:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Обновление зоны DNS

Изменения tooa ресурсов зоны DNS можно при помощи `az network dns zone update`. Чтобы получить справку, см. `az network dns zone update --help`.

Эта команда не обновляет hello наборы записей DNS в зоне hello (см. [как DNS-записи tooManage](dns-operations-recordsets-cli.md)). Это свойства только используемые tooupdate сам ресурс hello зоны. Эти свойства доступны в настоящее время составляет toohello [диспетчера ресурсов Azure «теги»](dns-zones-records.md#tags) для ресурса зоны hello.

Hello следующем примере показано, как tooupdate hello тегов в зоне DNS. существующие теги Hello заменяются указано значение hello.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Удаление зоны DNS

Зоны DNS можно удалить с помощью команды `az network dns zone delete`. Чтобы получить справку, см. `az network dns zone delete --help`.

> [!NOTE]
> Зоны DNS при удалении также удаляются все записи DNS в зоне hello. Эту операцию нельзя отменить. Если зона DNS hello, службы, используя зоны hello сможет hello зона удаляется.
>
>tooprotect от зоны случайного удаления, в разделе [как tooprotect DNS-зоны и записывает](dns-protect-zones-recordsets.md).

Эта команда запрашивает подтверждение. Необязательный Hello `--yes` подавляет этот запрос.

Hello следующем примере показано, как toodelete hello зоны *contoso.com* из группы ресурсов *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[управления наборов записей и записи](dns-getstarted-create-recordset-cli.md) в зоне DNS.

Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).

