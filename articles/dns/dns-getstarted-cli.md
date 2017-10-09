---
title: "aaaGet работы с Azure DNS, с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять первый DNS-зоны и записи с помощью Azure CLI 2.0 hello."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a>Начало работы со службой DNS Azure с помощью Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Портал Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

В этой статье поможет выполнить шаги toocreate hello вашей первой зоны DNS и записи с помощью hello Azure CLI кросс платформенных 2.0, которая доступна для Windows, Mac и Linux. Также можно выполнить следующие действия с помощью hello портал Azure или Azure PowerShell.

Зоны DNS-записей DNS используется toohost hello для определенного домена. toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена. Каждая запись DNS для вашего домена создается внутри этой зоны DNS. Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello. Каждый из этих шагов описан ниже.

Эти инструкции предполагают, вы уже установили и вход выполнен tooAzure CLI 2.0. Справочные сведения см. в разделе [как toomanage DNS-зоны с помощью Azure CLI 2.0](dns-operations-dnszones-cli.md).

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Перед созданием hello зоны DNS, зоны DNS hello toocontain создания группы ресурсов. Hello ниже показана команда hello.

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зоны DNS создается с помощью hello `az network dns zone create` команды. toosee справку для этой команды, введите `az network dns zone create -h`.

Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello *MyResourceGroup*. Используйте toocreate пример hello зону DNS, подставив собственные значения hello.

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a>Создание записи DNS

запись DNS toocreate использовать hello `az network dns record-set [record type] add-record` команды. Чтобы получить справку, например по записям типа A, см. `azure network dns record-set A add-record -h`.

Hello в примере создается запись с hello относительное имя «www» в зону DNS «contoso.com» в группе ресурсов «MyResourceGroup» hello. Hello полное имя набора записей hello — «www.contoso.com». Тип записи Hello — «A» с IP-адресом «1.2.3.4», и используется значение по умолчанию срок ЖИЗНИ 3600 секунд (1 час).

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

Для других типов записей для наборов записей с более одной записи для альтернативных значений срока ЖИЗНИ и toomodify существующие записи, в разделе [Управление DNS-записи и с помощью наборов записей hello Azure CLI 2.0](dns-operations-recordsets-cli.md).


## <a name="view-records"></a>Просмотр записей

toolist hello DNS-записи в зоне, используйте:

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a>Обновление серверов доменных имен

Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами. Это позволяет другим пользователям на hello Internet toofind DNS-записей.

Hello серверы имен для зоны определяются hello `az network dns zone show` команды. имена серверов имя toosee hello, используйте выходных данных, JSON, как показано в следующий пример hello.

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя). Регистратор предлагают tooset параметр hello hello серверов имя домена hello. Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Удаление всех ресурсов
 
toodelete все ресурсы созданы в этой статье hello выполните следующий шаг:

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).

toolearn Дополнительные сведения об управлении зонами DNS в Azure DNS, в разделе [зоны DNS, управление в Azure DNS, с помощью Azure CLI 2.0](dns-operations-dnszones-cli.md).

toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и записи задает в Azure DNS, с помощью Azure CLI 2.0](dns-operations-recordsets-cli.md).
