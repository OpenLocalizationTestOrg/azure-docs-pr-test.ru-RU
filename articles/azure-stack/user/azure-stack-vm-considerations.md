---
title: "Важные особенности виртуальных машин в Azure Stack и рекомендации по работе с ними | Документация Майкрософт"
description: "Сведения об особенностях виртуальных машин в Azure Stack и рекомендации по работе с ними."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 6613946D-114C-441A-9F74-38E35DF0A7D7
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2018
ms.author: brenduns
ms.openlocfilehash: 6eafa2a5058ef1309cbf50be069ea1bb12f7e5b9
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Рекомендации по работе с виртуальными машинами в Azure Stack

*Область применения: интегрированные системы Azure Stack и пакет SDK для Azure Stack*

Виртуальные машины — это масштабируемые вычислительные ресурсы, предоставляемые по запросу в Azure Stack. Если вы используете виртуальные машины, важно знать о различиях между функциями, доступными в Azure и Azure Stack. В этой статье представлены рекомендации по работе с виртуальными машинами и их возможностями в Azure Stack. Чтобы узнать об общих различиях между Azure Stack и Azure, прочитайте статью [Важные аспекты использования служб и создания приложений в Azure Stack](azure-stack-considerations.md).

## <a name="cheat-sheet-virtual-machine-differences"></a>Памятка: различия виртуальных машин

| Функция | Azure (глобальная) | Azure Stack |
| --- | --- | --- |
| Образы виртуальных машин | Azure Marketplace содержит образы, на основе которых можно создать виртуальную машину. На странице [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) представлен список образов, доступных в Azure Marketplace. | По умолчанию Azure Stack Marketplace не содержит образы. Чтобы пользователи могли использовать образы, администратор облака Azure Stack должен опубликовать или загрузить их в Azure Stack Marketplace. |
| Размер виртуальных машин | Azure поддерживает широкий ассортимент размеров виртуальных машин. Дополнительные сведения о доступных размерах и параметрах см. в статьях [Размеры виртуальных машин Windows в Azure](../../virtual-machines/virtual-machines-windows-sizes.md) и [Размеры виртуальных машин Linux в Azure](../../virtual-machines/linux/sizes.md). | Azure Stack поддерживает подмножество размеров виртуальных машин, доступных в Azure. Чтобы просмотреть список поддерживаемых размеров, изучите раздел [Размеры виртуальных машин](#virtual-machine-sizes) в этой статье. |
| Квоты для виртуальных машин | [Ограничения квот](../../azure-subscription-service-limits.md#service-specific-limits) устанавливаются корпорацией Майкрософт. | Администратор облака Azure Stack должен самостоятельно назначить квоты, прежде чем предлагать виртуальные машины пользователям. |
| Расширения виртуальных машин |Azure поддерживает широкий ассортимент расширений для виртуальных машин. Чтобы узнать о доступных расширениях, изучите статью [Обзор расширений и компонентов виртуальной машины под управлением Windows](../../virtual-machines/windows/extensions-features.md).| Azure Stack поддерживает подмножество расширений, доступных в Azure, и каждое расширение представлено в нескольких версиях. Администратор облака Azure Stack может выбрать, какие расширения будут доступны его пользователям. Чтобы просмотреть список поддерживаемых расширений, изучите раздел [Расширения виртуальных машин](#virtual-machine-extensions) в этой статье. |
| Сетевые ресурсы виртуальных машин | Общедоступные IP-адреса, назначенные для виртуальной машины клиента, доступны через Интернет.<br><br><br>Виртуальные машины Azure имеют фиксированное DNS-имя. | Общедоступные IP-адреса, назначенные для виртуальной машины клиента, доступны только в пределах среды пакета SDK для Azure Stack. Пользователь должен иметь доступ к пакету SDK для Azure Stack через [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) или [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn), чтобы подключиться к виртуальной машине, созданной в Azure Stack.<br><br>Виртуальные машины, созданные в определенном экземпляре Azure Stack, получают DNS-имя в соответствии с параметрами, настроенными администратором облака. |
| Хранилище для виртуальных машин | Поддерживаются [управляемые диски.](../../virtual-machines/windows/managed-disks-overview.md) | Управляемые диски в Azure Stack пока не поддерживаются. |
| Версии API | Azure всегда использует последние версии API для всех компонентов виртуальной машины. | Azure Stack поддерживает только определенный набор служб Azure и конкретные версии API для каждой из этих служб. Чтобы просмотреть список поддерживаемых версий API, изучите раздел [Версии API](#api-versions) в этой статье. |
|Группы доступности виртуальных машин|Несколько доменов сбоя (2 или 3 в каждом регионе)<br>Несколько доменов обновления<br>Поддержка управляемых дисков|Один домен сбоя<br>Один домен обновления<br>Без поддержки управляемых дисков|
|наборы для масштабирования виртуальных машин|Автомасштабирование поддерживается|Автомасштабирование не поддерживается<br>В масштабируемый набор можно добавить дополнительные экземпляры с помощью портала, шаблонов Resource Manager или PowerShell.

## <a name="virtual-machine-sizes"></a>Размер виртуальных машин

Azure Stack поддерживает следующие размеры:

| type | Размер | Диапазон поддерживаемых размеров |
| --- | --- | --- |
|Универсальные |Basic A|A0–A4|
|Универсальные |Standard A|A0–A7|
|Универсальные |Серия D|D1–D4|
|Универсальные |Серия Dv2|D1_v2–D5_v2|
|Универсальные |Серия DS|DS1–DS4|
|Универсальные |Серия DSv2|DS1_v2–DS5_v2|
|Оптимизированные для памяти|Серия DS|DS11–DS14|
|Оптимизированные для памяти |Серия DSv2|DS11_v2–DS14_v2|

Размеры виртуальных машин и объемы связанных с ними ресурсов в Azure Stack и Azure полностью совпадают. Это, например, включает объем памяти, число ядер, число и размеры создаваемых дисков данных. Однако фактическая производительность виртуальных машин зависит от базовых характеристик конкретной среды Azure Stack.

## <a name="virtual-machine-extensions"></a>Расширения виртуальных машин

 Azure Stack поддерживает следующие версии расширений для виртуальных машин:

![Расширения виртуальных машин](media/azure-stack-vm-considerations/vm-extensions.png)

Используйте следующий скрипт PowerShell, чтобы получить список расширений виртуальной машины, доступных в вашей среде Azure Stack:

```powershell
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize
```

## <a name="api-versions"></a>Версии API

Компоненты виртуальных машин в Azure Stack поддерживают следующие версии API:

![Типы ресурсов виртуальных машин](media/azure-stack-vm-considerations/vm-resoource-types.png)

Используйте следующий скрипт PowerShell, чтобы получить список версий API для компонентов виртуальной машины, доступных в вашей среде Azure Stack:

```powershell
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
Список поддерживаемых типов ресурсов и версий API может измениться, если оператор облака обновит среду Azure Stack до более новой версии.

## <a name="next-steps"></a>Дополнительная информация

[Создание виртуальной машины Windows с помощью PowerShell в Azure Stack](azure-stack-quick-create-vm-windows-powershell.md)
