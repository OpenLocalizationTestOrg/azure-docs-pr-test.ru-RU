---
title: "Управление зонами DNS в службе DNS Azure (Azure CLI 2.0) | Документация Майкрософт"
description: "Зонами DNS можно управлять с помощью Azure CLI 2.0. В этой статье показано, как обновлять, удалять и создавать зоны DNS в службе DNS Azure."
services: dns
documentationcenter: na
author: KumudD
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: kumud
ms.openlocfilehash: 2042d9c2864a4f8da474e0df38882414bfe3417e
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a>Как управлять зонами DNS в службе DNS Azure с помощью Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Портал](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


В этом руководстве показано, как управлять зонами DNS с помощью кроссплатформенного интерфейса командной строки Azure, доступного для Windows, Mac и Linux. Зонами DNS также можно управлять с помощью [Azure PowerShell](dns-operations-dnszones.md) или портала Azure.

## <a name="introduction"></a>Общие сведения

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Настройка Azure CLI 2.0 для Azure DNS

### <a name="before-you-begin"></a>Перед началом работы

Перед началом настройки убедитесь, что у вас есть следующие компоненты.

* Подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).

* Установите последнюю версию Azure CLI 2.0 для Windows, Linux или Mac. Дополнительные сведения см. в статье [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (Установка Azure CLI 2.0).

### <a name="sign-in-to-your-azure-account"></a>Вход в учетную запись Azure

Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных. Дополнительные сведения см. в статье "Вход в Azure из командной строки Azure".

```
az login
```

### <a name="select-the-subscription"></a>Выбор подписки

Просмотрите подписки учетной записи.

```
az account list
```

Выберите, какие подписки Azure будут использоваться.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Диспетчер ресурсов Azure требует, чтобы все группы ресурсов указывали расположение. Оно используется в качестве расположения по умолчанию для всех ресурсов данной группы. Но так как все ресурсы DNS глобальные, а не региональные, выбор расположения группы ресурсов не влияет на Azure DNS.

Если используется существующая группа ресурсов, можно пропустить этот шаг.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Получение справки

Все команды CLI 2.0 для Azure DNS начинаются с `az network dns`. Справку для каждой команды можно отобразить с помощью параметра `--help` (краткая форма: `-h`).  Например: 

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зона DNS создается с помощью команды `az network dns zone create`. Чтобы получить справку, см. `az network dns zone create -h`.

В следующем примере создается зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a>Создание зоны DNS с тегами

В следующем примере демонстрируется создание зоны DNS с двумя [тегами Azure Resource Manager](dns-zones-records.md#tags) (*project = demo* и *env = test*) с помощью параметра `--tags` (краткая форма: `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Получение зоны DNS

Чтобы получить зону DNS, используйте команду `az network dns zone show`. Чтобы получить справку, см. `az network dns zone show --help`.

В следующем примере возвращается зона DNS *contoso.com* и связанные с ней данные из группы ресурсов *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Ниже приведен пример ответа.

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

Обратите внимание, что записи DNS не возвращаются командой `az network dns zone show`. Для вывода списка записей DNS используйте `az network dns record-set list`.


## <a name="list-dns-zones"></a>Перечисление зон DNS

Чтобы перечислить зоны DNS, используйте `az network dns zone list`. Чтобы получить справку, см. `az network dns zone list --help`.

Если указать группу ресурсов, то будут перечислены только зоны в этой группе ресурсов.

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Если не указать группу ресурсов, то будут перечислены все зоны в подписке.

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Обновление зоны DNS

Изменить ресурс зоны DNS можно с помощью командлета `az network dns zone update`. Чтобы получить справку, см. `az network dns zone update --help`.

Это команда не обновляет ни один набор записей DNS в пределах зоны (прочитайте статью [Управление записями и наборами записей DNS с помощью PowerShell](dns-operations-recordsets-cli.md)). Эта команда используется только для обновления свойств самого ресурса зоны. В настоящее время к этим свойствам относятся только [теги Azure Resource Manager](dns-zones-records.md#tags) для ресурса зоны.

В приведенном ниже примере показано, как обновить теги для зоны DNS. Существующие теги заменяются указанным значением.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Удаление зоны DNS

Зоны DNS можно удалить с помощью команды `az network dns zone delete`. Чтобы получить справку, см. `az network dns zone delete --help`.

> [!NOTE]
> При удалении зоны DNS также удаляются все записи DNS в этой зоне. Эту операцию нельзя отменить. Если зона DNS используется, то после ее удаления произойдет сбой служб, которые ее используют.
>
>Сведения о защите от случайного зоны удаления см. в разделе [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Как защитить зоны и записи DNS).

Эта команда запрашивает подтверждение. Необязательный параметр `--yes` позволяет отключить этот запрос.

В следующем примере показано, как удалить зону *contoso.com* из группы ресурсов *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как [управлять наборами записей и записями](dns-getstarted-create-recordset-cli.md) в зоне DNS.

Узнайте, как [делегировать свой домен в Azure DNS](dns-domain-delegation.md).

