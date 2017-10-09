---
title: "aaaGet работы с Azure DNS, с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять первый DNS-зоны и записи с помощью hello Azure CLI 1.0."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a>Начало работы со службой DNS Azure с помощью Azure CLI 1.0

> [!div class="op_single_selector"]
> * [Портал Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

В этой статье поможет выполнить шаги toocreate hello вашей первой зоны DNS и записи с помощью hello Azure CLI кросс платформенных 1.0, которая доступна для Windows, Mac и Linux. Также можно выполнить следующие действия с помощью hello портал Azure или Azure PowerShell.

Зоны DNS-записей DNS используется toohost hello для определенного домена. toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена. Каждая запись DNS для вашего домена создается внутри этой зоны DNS. Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello. Каждый из этих шагов описан ниже.

Эти инструкции предполагают, вы уже установили и вход выполнен tooAzure CLI 1.0. Справочные сведения см. в разделе [как toomanage DNS-зоны с помощью Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Перед созданием hello зоны DNS, зоны DNS hello toocontain создания группы ресурсов. Hello ниже показана команда hello.

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зоны DNS создается с помощью hello `azure network dns zone create` команды. toosee справку для этой команды, введите `azure network dns zone create -h`.

Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*. Используйте toocreate пример hello зону DNS, подставив собственные значения hello.

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a>Создание записи DNS

запись DNS toocreate использовать hello `azure network dns record-set add-record` команды. Чтобы получить справку, см. `azure network dns record-set add-record -h`.

Hello в примере создается запись с hello относительное имя «www» в зону DNS «contoso.com» в группе ресурсов «MyResourceGroup» hello. Hello полное имя набора записей hello — «www.contoso.com». Тип записи Hello — «A» с IP-адресом «1.2.3.4», и используется значение по умолчанию срок ЖИЗНИ 3600 секунд (1 час).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

Для других типов записей для наборов записей с более одной записи для альтернативных значений срока ЖИЗНИ и toomodify существующие записи, в разделе [Управление DNS-записи и с помощью наборов записей hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).


## <a name="view-records"></a>Просмотр записей

toolist hello DNS-записи в зоне, используйте:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a>Обновление серверов доменных имен

Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами. Это позволяет другим пользователям на hello Internet toofind DNS-записей.

Hello серверы имен для зоны определяются hello `azure network dns zone show` команды:

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя). Регистратор предлагают tooset параметр hello hello серверов имя домена hello. Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Удаление всех ресурсов
 
toodelete все ресурсы созданы в этой статье hello выполните следующий шаг:

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).

toolearn Дополнительные сведения об управлении зонами DNS в Azure DNS, в разделе [зоны DNS, управление в Azure DNS, с помощью Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и записи задает в Azure DNS, с помощью Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).

