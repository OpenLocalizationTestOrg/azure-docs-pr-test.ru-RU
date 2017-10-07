---
title: "aaaManage DNS-зоны в Azure DNS - PowerShell | Документы Microsoft"
description: "Зонами DNS можно управлять с помощью Azure Powershell. В этой статье описывается, как tooupdate, удалите и создайте зон DNS на Azure DNS"
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
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>Как toomanage зон DNS, с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

В этой статье показано, как toomanage DNS-зоны с помощью Azure PowerShell. Также можно управлять с помощью hello кросс платформенных зон DNS [Azure CLI](dns-operations-dnszones-cli.md) или hello портал Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Создание зоны DNS

Зоны DNS создается с помощью hello `New-AzureRmDnsZone` командлета.

Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hello следующем примере показано, как toocreate DNS зоны с двумя [диспетчера ресурсов Azure теги](dns-zones-records.md#tags), *проекта = Демонстрация* и *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Получение зоны DNS

tooretrieve зоны DNS, используйте hello `Get-AzureRmDnsZone` командлета. Эта операция возвращает объект соответствующего tooan существующей зоны в Azure DNS зоны DNS. Hello объекта содержит данные о зоне hello (например hello число наборов записей), но не содержит наборы записей hello сами (см. `Get-AzureRmDnsRecordSet`).

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

Имя зоны hello из `Get-AzureRmDnsZone`, можно перечислить все зоны в группе ресурсов. Эта операция возвращает массив объектов зоны.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Не указывайте имя зоны hello и имя группы ресурсов hello из `Get-AzureRmDnsZone`, можно перечислить все зоны в hello подписки Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Обновление зоны DNS

Изменения ресурсов зоны DNS можно сделать с помощью tooa `Set-AzureRmDnsZone`. Этот командлет не обновляет hello наборы записей DNS в зоне hello (см. [как DNS-записи tooManage](dns-operations-recordsets.md)). Только свойства tooupdate сам ресурс hello зоны. свойства для записи зоны Hello, в настоящее время составляет toohello [диспетчера ресурсов Azure «теги» для ресурса зоны hello](dns-zones-records.md#tags).

Используйте один из следующих двух способов tooupdate hello зоны DNS.

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Укажите hello зоны с помощью hello зоны имя и группе ресурсов

Этот подход заменяет существующие теги зоны hello значениями hello.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Укажите hello зоны с помощью объекта $zone

Этот подход извлекает существующий объект зоны hello, изменяющий теги hello и затем фиксирует изменения hello. Благодаря этому существующие теги могут сохраняться.

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

При использовании `Set-AzureRmDnsZone` с объектом $zone [проверяет Etag](dns-zones-records.md#etags) используются tooensure параллельных изменений не перезаписываются. Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.

## <a name="delete-a-dns-zone"></a>Удаление зоны DNS

Зоны DNS-сервера могут быть удалены с помощью hello `Remove-AzureRmDnsZone` командлета.

> [!NOTE]
> Зоны DNS при удалении также удаляются все записи DNS в зоне hello. Эту операцию нельзя отменить. Если зона DNS hello, службы, используя зоны hello сможет hello зона удаляется.
>
>tooprotect от зоны случайного удаления, в разделе [как tooprotect DNS-зоны и записывает](dns-protect-zones-recordsets.md).


Используйте один из следующих двух способов toodelete hello зоны DNS.

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Укажите hello зоны с помощью имени зоны hello и имя группы ресурсов

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Укажите hello зоны с помощью объекта $zone

Можно указать toobe зоны hello, удаляются с помощью `$zone` объект, возвращаемый `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

Hello объекта зоны также можно направить вместо передан в качестве параметра:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Как и в `Set-AzureRmDnsZone`, указав hello зоны с помощью `$zone` объекта включает Etag проверяет tooensure параллельных изменений не удаляются. Используйте hello `-Overwrite` переключения toosuppress этих проверок.

## <a name="confirmation-prompts"></a>Запросы на подтверждение

Hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, и `Remove-AzureRmDnsZone` все командлеты поддерживают запросы подтверждения.

Оба `New-AzureRmDnsZone` и `Set-AzureRmDnsZone` запрашивать подтверждение при hello `$ConfirmPreference` PowerShell Привилегированная переменная имеет значение `Medium` или ниже. Из-за toohello потенциально высокая степень влияния на удаления зоны DNS, hello `Remove-AzureRmDnsZone` командлет запрашивает подтверждение, если hello `$ConfirmPreference` переменной PowerShell имеет любое значение, отличное от `None`.

Так как значение по умолчанию hello `$ConfirmPreference` — `High`только `Remove-AzureRmDnsZone` запрашивает подтверждение по умолчанию.

Можно переопределить текущего hello `$ConfirmPreference` параметр с помощью hello `-Confirm` параметра. При указании `-Confirm` или `-Confirm:$True` , hello командлет запросит подтверждение перед его запуска. При указании `-Confirm:$False` , командлет hello не запрашивает вашего подтверждения.

Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[управления наборов записей и записи](dns-operations-recordsets.md) в зоне DNS.
<br>
Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).
<br>
Просмотрите hello [справочная документация по Azure DNS PowerShell](/powershell/module/azurerm.dns).

