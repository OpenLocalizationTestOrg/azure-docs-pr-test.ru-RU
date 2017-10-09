---
title: "aaaAutomate NSG аудита и представление \"Группа безопасности Наблюдатель сети Azure\" | Документы Microsoft"
description: "Эта страница содержит инструкции о том, как аудит tooconfigure группы безопасности сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Автоматизация аудита группы безопасности сети с помощью представления группы безопасности в Наблюдателе за сетями Azure

Пользователи часто сталкиваются с проблемой hello проверки уровня безопасности hello своей инфраструктуры. Это же характерно и для виртуальных машин в Azure. Это важные toohave как профиль безопасности на основе hello группы безопасности сети (NSG) правил применения. Используя представление "Группа безопасности" hello, теперь вы можете получить список правил, применяемых tooa ВМ в NSG hello. Можно определить профиль безопасности золотой NSG и инициировать представление группы безопасности в еженедельно ритме и сравнить профиль toohello золотой вывода hello и создать отчет. Таким образом можно определить с легкостью все виртуальные машины hello, которые не соответствуют toohello предписанные профиля безопасности.

Подробную информацию о группах безопасности сети см. в статье [Управление потоком сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Перед началом работы

В этом случае сравнение группу безопасности toohello известного хорошую основу просматривать результаты, возвращаемые для виртуальной машины.

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

Hello сценарий, описанный в этой статье возвращает hello представление группы безопасности для виртуальной машины.

Вам предстоит:

- получить набор известных проверенных правил;
- получить виртуальную машину с помощью REST API;
- получить представление группы безопасности для виртуальной машины;
- оценить ответ.

## <a name="retrieve-rule-set"></a>Получение набора правил

Первым шагом Hello в этом примере является toowork с существующего шаблона. Hello следующий пример — некоторые json, извлеченных из существующей группы безопасности сети с помощью hello `Get-AzureRmNetworkSecurityGroup` командлет, который используется в качестве базовой hello в этом примере.

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a>Преобразование объектов tooPowerShell набора правил

На этом шаге мы читаете json-файл, который был создан ранее с правилами hello, ожидаемый toobe на hello сетевой группы безопасности для этого примера.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Извлечение Наблюдателя за сетями

Hello следующим шагом является экземпляр Наблюдатель сети tooretrieve hello. Hello `$networkWatcher` переменной передается toohello `AzureRmNetworkWatcherSecurityGroupView` командлета.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Получение виртуальной машины

Виртуальная машина — hello необходимые toorun `Get-AzureRmNetworkWatcherSecurityGroupView` командлета для. Следующий пример Hello получает объект виртуальной Машины.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Получение представления группы безопасности

Hello следующим шагом является результат представления группы безопасности hello tooretrieve. Этот результат является json сравниваемых toohello «базовые показатели», показанном выше.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Анализ результатов hello

ответ Hello группируются по сетевых интерфейсов. различные типы возвращаемых правил Hello, вступают в силу и по умолчанию правила безопасности. результат Hello дальнейшей разбивкой на способы применения, либо в подсети или виртуальный сетевой адаптер.

Hello следующий сценарий PowerShell сравнивает результаты hello hello представление группы безопасности tooan существующие выходные данные NSG. Hello ниже приведен простой пример сравнение результатов hello с `Compare-Object` командлета.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Следующий пример Hello является результатом hello. Вы увидите два hello правил, которые были в hello первый набор правил, которые не hello сравнения.

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a>Дальнейшие действия

Если параметры были изменены, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, в вопросе.













