---
title: "Управление зонами DNS в службе DNS Azure с помощью PowerShell | Документация Майкрософт"
description: "Зонами DNS можно управлять с помощью Azure Powershell. В этой статье описывается, как обновлять, удалять и создавать зоны DNS в службе DNS Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/22/2016
ms.author: gwallace
ms.openlocfilehash: 3f28e70bb6ef46f53375d256a520db40fcb71ad0
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a>Как управлять зонами DNS с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

В этой статье описывается, как управлять зонами DNS с помощью Azure PowerShell. Зонами DNS также можно управлять с помощью кроссплатформенного [интерфейса командной строки Azure](dns-operations-dnszones-cli.md) или портала Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зона DNS создается с помощью командлета `New-AzureRmDnsZone`.

В следующем примере создается зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

В следующем примере демонстрируется создание зоны DNS с двумя [тегами Azure Resource Manager](dns-zones-records.md#tags) (*project = demo* и *env = test*):

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

Теперь Azure DNS также поддерживает частные зоны DNS (в настоящее время в виде предварительной версии).  Инструкции по созданию частной зоны DNS см. в статье [Get started with Azure DNS private zones using PowerShell](./private-dns-getstarted-powershell.md) (Начало работы с частными зонами Azure DNS с помощью PowerShell).

## <a name="get-a-dns-zone"></a>Получение зоны DNS

Чтобы получить зону DNS, используйте командлет `Get-AzureRmDnsZone` . Эта операция возвращает объект зоны DNS, соответствующий существующей зоне в Azure DNS. Объект содержит данные о зоне (например, число наборов записей), но не сами наборы записей (см. `Get-AzureRmDnsRecordSet`).

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>Перечисление зон DNS

Если опустить имя зоны в командлете `Get-AzureRmDnsZone`, можно получить список всех зон в группе ресурсов. Эта операция возвращает массив объектов зоны.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Если опустить имя зоны и имя группы ресурсов в командлете `Get-AzureRmDnsZone`, то можно получить список всех зон в подписке Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Обновление зоны DNS

Изменить ресурс зоны DNS можно с помощью командлета `Set-AzureRmDnsZone`. При этом ни один набор записей DNS в пределах зоны командлетом не обновляется (см. статью [Управление записями и наборами записей DNS с помощью PowerShell](dns-operations-recordsets.md)). Эта команда используется только для обновления свойств самого ресурса зоны. В настоящее время к записываемым свойствам зоны относятся только [теги Azure Resource Manager для ресурса зоны](dns-zones-records.md#tags).

Используйте один из двух описанных ниже способов обновления зоны DNS.

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a>Укажите зону с помощью имени и группы ресурсов.

При этом подходе существующие теги зоны заменяются указанными значениями.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a>Укажите зону с помощью объекта $zone.

При этом подходе извлекается существующий объект зоны, изменяются теги, а затем фиксируются изменения. Благодаря этому существующие теги могут сохраняться.

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

При использовании командлета `Set-AzureRmDnsZone` с объектом $zone применяются [проверки Etag](dns-zones-records.md#etags), чтобы параллельные изменения не были перезаписаны. Чтобы отменить эти проверки, укажите необязательный параметр `-Overwrite`.

## <a name="delete-a-dns-zone"></a>Удаление зоны DNS

Зоны DNS можно удалить с помощью командлета `Remove-AzureRmDnsZone`.

> [!NOTE]
> При удалении зоны DNS также удаляются все записи DNS в этой зоне. Эту операцию нельзя отменить. Если зона DNS используется, то после ее удаления произойдет сбой служб, которые ее используют.
>
>Сведения о защите от случайного зоны удаления см. в разделе [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Как защитить зоны и записи DNS).


Используйте один из двух описанных ниже способов удаления зоны DNS.

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a>Укажите зону с помощью имени зоны и имени группы ресурсов.

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a>Укажите зону с помощью объекта $zone.

Удаляемую зону можно указать с помощью объекта `$zone`, который возвращается командлетом `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

Объект зоны также можно направить в конвейер, а не передавать в качестве параметра:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Как и для командлета `Set-AzureRmDnsZone`, при указании набора записей с помощью объекта `$zone` вы включаете проверки Etag, чтобы убедиться, что параллельные изменения не удаляются. Чтобы отменить эти проверки, используйте параметр `-Overwrite`.

## <a name="confirmation-prompts"></a>Запросы на подтверждение

Командлеты `New-AzureRmDnsZone`, `Set-AzureRmDnsZone` и `Remove-AzureRmDnsZone` поддерживают запросы на подтверждение.

Оба командлета (`New-AzureRmDnsZone` и `Set-AzureRmDnsZone`) запрашивают подтверждение, если привилегированная переменная `$ConfirmPreference` в PowerShell имеет значение `Medium` или ниже. Из-за того, что удаление зоны DNS может иметь значительные последствия, командлет `Remove-AzureRmDnsZone` запрашивает подтверждение, если переменная PowerShell `$ConfirmPreference` имеет любое значение, отличное от `None`.

Поскольку переменная `$ConfirmPreference` по умолчанию имеет значение `High`, то по умолчанию подтверждение запрашивается только командлетом `Remove-AzureRmDnsZone`.

Текущее значение `$ConfirmPreference` можно переопределить с помощью параметра `-Confirm`. Если вы определите `-Confirm` или `-Confirm:$True`, командлет будет запрашивать подтверждение перед выполнением. Если вы определите `-Confirm:$False`, командлет не будет запрашивать подтверждение.

Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как [управлять наборами записей и записями](dns-operations-recordsets.md) в зоне DNS.
<br>
Узнайте, как [делегировать свой домен в Azure DNS](dns-domain-delegation.md).
<br>
Просмотрите [справочную документацию по Azure DNS PowerShell](/powershell/module/azurerm.dns).

