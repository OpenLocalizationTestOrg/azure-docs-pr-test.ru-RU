---
title: "Различия и рекомендации для виртуальных машин в Azure стек | Документы Microsoft"
description: "Дополнительные сведения о различия и рекомендации при работе с виртуальными машинами в Azure стека."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/4/2017
ms.author: sngun
ms.openlocfilehash: f97433d7db5811c69851002e459eb01b6e97a722
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Рекомендации для виртуальных машин в стек Azure

Виртуальные машины находятся по требованию, масштабируемые вычислительные ресурсы, предоставляемые Azure стека. При использовании виртуальных машин, необходимо понимать, что существуют различия между средства, доступные в Azure и Azure стека. В этой статье Общие рекомендации, уникальным для виртуальных машин и его компонентах в стек Azure. Дополнительные сведения о высокоуровневых различия между стек Azure и Azure см. в разделе [основные вопросы](azure-stack-considerations.md) раздела.

## <a name="cheat-sheet-virtual-machine-differences"></a>Памятка: различия виртуальной машины

| Функция | (Глобальная) Azure | Azure Stack |
| --- | --- | --- |
| Образы виртуальных машин | В Azure Marketplace содержит изображения, которые можно использовать для создания виртуальной машины. В разделе [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) страницу, чтобы просмотреть список изображений, доступных в Azure Marketplace. | По умолчанию отсутствуют все образы в стек Azure marketplace. Администратору облака Azure стек должен [публикации](azure-stack-add-default-image.md) или [загрузка изображений](azure-stack-download-azure-marketplace-item.md) в стек Azure Marketplace, чтобы пользователи могли использовать их. |
| Размер виртуальных машин | Azure поддерживает широкий набор размеров виртуальных машин. Дополнительные сведения о доступных размерах и параметрах, см. [размеры виртуальных машин Windows](../virtual-machines/virtual-machines-windows-sizes.md) и [размеры виртуальных машин Linux](../virtual-machines/linux/sizes.md) разделы. | Стек Azure поддерживает подмножество размеры виртуальных машин, доступных в Azure. Чтобы просмотреть список поддерживаемых форматов, обратитесь к [размеры виртуальных машин](#virtual-machine-sizes) этой статьи. |
| Квоты виртуальной машины | [Квоты](../azure-subscription-service-limits.md#service-specific-limits) установленную корпорацией Майкрософт | Стек Azure администратору облака необходимо [назначать квоты](azure-stack-setting-quotas.md) прежде, чем предлагают виртуальных машин для пользователей. |
| Расширения виртуальных машин |Azure поддерживает широкий спектр расширения виртуальных машин. Чтобы узнать о доступных расширениях см [расширения виртуальной машины и компоненты](../virtual-machines/windows/extensions-features.md) раздела.| Стек Azure поддерживает подмножество расширений, доступных в Azure и расширения имеют конкретных версий. Администратору облака Azure стека можно выбрать какие расширения должны быть доступны для своим пользователям. Чтобы просмотреть список поддерживаемых модулей, обратитесь к [расширения виртуальных машин](#virtual-machine-extensions) этой статьи. |
| Сеть виртуальной машины | Общедоступные IP-адреса, назначенные для клиента виртуальной машины, доступны через Интернет.<br><br><br>Виртуальные машины Azure имеет основного DNS-имя | В среде Azure стека Development Kit только доступны общих IP-адресов, назначенных виртуальной машины клиента. Пользователь должен иметь доступ к набору разработки Azure стека через [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) или [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) для подключения к виртуальной машине, создаваемой в Azure стека.<br><br>Виртуальные машины, созданные в определенном экземпляре Azure стека имеет DNS-имя, основанного на значении, настроенный администратором облака. |
| Хранилище виртуальной машины | Поддерживает [управляемых дисках.](../virtual-machines/windows/managed-disks-overview.md) | Управляемый диски пока не поддерживаются в Azure стека. |
| Версии API | Azure всегда были установлены последние версии API для всех компонентов виртуальной машины. | Стек Azure поддерживает определенных служб Azure и определенные версии API для этих служб. Чтобы просмотреть список поддерживаемых версий API, обратитесь к [версий API](#api-versions) этой статьи. |
|Группы доступности виртуальной машины|Разным доменам отказоустойчивости (2 или 3 в одном регионе)<br>Несколько доменов обновления<br>Поддержка диска управляемого|Одна ошибка домена<br>Одно обновление домена<br>Нет поддержки управляемого диска|
|наборы для масштабирования виртуальных машин|Автомасштабирование поддерживается|Автоматически масштабировать не поддерживается.<br>Добавьте дополнительные экземпляры в наборе с помощью портала, шаблоны диспетчера ресурсов или PowerShell масштабирования.

## <a name="virtual-machine-sizes"></a>Размер виртуальных машин 

Пакет средств разработки стек Azure поддерживает следующие размеры: 

| Тип | Размер | Диапазон поддерживаемых размеров |
| --- | --- | --- |
|Универсальные |Basic A|A0 A4|
|Универсальные |Стандартный объект|A0–A7|
|Универсальные |Стандартная D|D1 D4|
|Универсальные |Стандартная Dv2|D1v2 D5v2|
|Оптимизированные для памяти|Серия D|D11 D14|
|Оптимизированные для памяти |Серия Dv2|D11v2 D14v2|

Размеры виртуальных машин в стек Azure и Azure согласуются с точки зрения памяти, ядер ЦП, пропускную способность сети, производительности диска и других факторов, которые определяют размер. Например Стандартная D размер виртуальной машины в Azure и Azure стека согласована. 

## <a name="virtual-machine-extensions"></a>Расширения виртуальных машин 

 Пакет средств разработки стек Azure поддерживает следующие версии расширения виртуальной машины:

![Расширения виртуальных машин](media/azure-stack-vm-considerations/vm-extensions.png)

Используйте следующий сценарий PowerShell, чтобы получить список расширений виртуальной машины, доступные в вашей среде Azure стека:

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>Версии API 

Особенности виртуальных машин в пакете средств разработки стек Azure поддерживают следующие версии API:

![Типы ресурсов виртуальной Машины](media/azure-stack-vm-considerations/vm-resoource-types.png)

Следующий сценарий PowerShell можно использовать для получения версии API для функции виртуальной машины, доступные в вашей среде Azure стека:

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
Список поддерживаемых типов ресурсов и версий API может меняться, если оператор облака обновления среды стека Azure до более новой версии.

## <a name="next-steps"></a>Дальнейшие действия

[Создание виртуальной машины Windows с помощью PowerShell в стек Azure](azure-stack-quick-create-vm-powershell.md)
