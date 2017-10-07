---
title: "aaaDifferences и рекомендации для виртуальных машин в Azure стек | Документы Microsoft"
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
ms.openlocfilehash: cee03e3e83b54efabaecd2647ec7defe371ee870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Рекомендации для виртуальных машин в стек Azure

Виртуальные машины находятся по требованию, масштабируемые вычислительные ресурсы, предоставляемые Azure стека. При использовании виртуальных машин, необходимо понимать, что существуют различия между hello функции, доступные в Azure и Azure стека. В этой статье общие вопросы уникальный hello для виртуальных машин и его компонентах в стек Azure. toolearn об отличиях высокого уровня стека Azure и Azure, в разделе hello [основные вопросы](azure-stack-considerations.md) раздела.

## <a name="cheat-sheet-virtual-machine-differences"></a>Памятка: различия виртуальной машины

| Функция | (Глобальная) Azure | Azure Stack |
| --- | --- | --- |
| Образы виртуальных машин | Hello Azure Marketplace содержит изображения, которые можно использовать toocreate виртуальной машины. В разделе hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) страницы tooview hello список изображений, доступных в hello Azure Marketplace. | По умолчанию отсутствуют все образы в hello стек Azure marketplace. облако Azure стека Здравствуйте, администратор должен [публикации](azure-stack-add-default-image.md) или [загрузка изображений](azure-stack-download-azure-marketplace-item.md) toohello стека Azure marketplace, чтобы пользователи могли использовать их. |
| Размер виртуальных машин | Azure поддерживает широкий набор размеров виртуальных машин. toolearn о доступных размерах hello и параметры, см. toohello [размеры виртуальных машин Windows](../virtual-machines/virtual-machines-windows-sizes.md) и [размеры виртуальных машин Linux](../virtual-machines/linux/sizes.md) разделы. | Стек Azure поддерживает подмножество размеры виртуальных машин, доступных в Azure. tooview hello список поддерживаемых размерах см. в toohello [размеры виртуальных машин](#virtual-machine-sizes) этой статьи. |
| Квоты виртуальной машины | [Квоты](../azure-subscription-service-limits.md#service-specific-limits) установленную корпорацией Майкрософт | облако Azure стека Здравствуйте, администратор должен [назначать квоты](azure-stack-setting-quotas.md) прежде, чем они предоставляют пользователям tootheir виртуальных машин. |
| Расширения виртуальных машин |Azure поддерживает широкий спектр расширения виртуальных машин. toolearn о доступных расширениях hello, ссылаться toohello [расширения виртуальной машины и компоненты](../virtual-machines/windows/extensions-features.md) раздела.| Стек Azure поддерживает подмножество расширений, доступных в Azure и расширения hello имеют конкретных версий. Hello стек Azure облачной администратор может выбрать, какие расширения toobe внесенные toofor доступных пользователей. Список hello tooview поддерживаемые расширения см. в toohello [расширения виртуальных машин](#virtual-machine-extensions) этой статьи. |
| Сеть виртуальной машины | Общих IP-адресов, назначенных виртуальной машины tootenant доступны через Интернет hello.<br><br><br>Виртуальные машины Azure имеет основного DNS-имя | Общих IP-адресов, назначенных виртуальная машина клиента tooa доступны в пределах hello только в среде Azure стека Development Kit. Пользователь должен иметь доступ toohello пакет средств разработки стек Azure через [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) или [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect tooa виртуальную машину, созданную в стек Azure.<br><br>Виртуальные машины, созданные в определенном экземпляре стек Azure имеют DNS-имя, на основе значения hello, настроенный администратором облака hello. |
| Хранилище виртуальной машины | Поддерживает [управляемых дисках.](../virtual-machines/windows/managed-disks-overview.md) | Управляемый диски пока не поддерживаются в Azure стека. |
| Версии API | Azure всегда имеет hello последние версии API для всех функций hello виртуальной машины. | Стек Azure поддерживает определенных служб Azure и определенные версии API для этих служб. tooview hello список поддерживаемых версий API см. в toohello [версий API](#api-versions) этой статьи. |
|Группы доступности виртуальной машины|Разным доменам отказоустойчивости (2 или 3 в одном регионе)<br>Несколько доменов обновления<br>Поддержка диска управляемого|Одна ошибка домена<br>Одно обновление домена<br>Нет поддержки управляемого диска|
|наборы для масштабирования виртуальных машин|Автомасштабирование поддерживается|Автоматически масштабировать не поддерживается.<br>Добавьте дополнительные экземпляры tooa масштабного набора с помощью портала hello, шаблоны диспетчера ресурсов или PowerShell.

## <a name="virtual-machine-sizes"></a>Размер виртуальных машин 

пакет средств разработки Azure стека Hello поддерживает hello следующие размеры: 

| Тип | Размер | Диапазон поддерживаемых размеров |
| --- | --- | --- |
|Универсальные |Basic A|A0 A4|
|Универсальные |Стандартный объект|A0–A7|
|Универсальные |Стандартная D|D1 D4|
|Универсальные |Стандартная Dv2|D1v2 D5v2|
|Оптимизированные для памяти|Серия D|D11 D14|
|Оптимизированные для памяти |Серия Dv2|D11v2 D14v2|

Размеры виртуальных машин в стек Azure и Azure согласуются с точки зрения hello памяти, ядер ЦП, пропускную способность сети, производительности диска и других факторов, которые определяют размер hello. Например согласуется hello D стандартный размер виртуальной машины в Azure и Azure стека. 

## <a name="virtual-machine-extensions"></a>Расширения виртуальных машин 

 пакет средств разработки Azure стека Hello поддерживает hello следующих версий расширения виртуальной машины:

![Расширения виртуальных машин](media/azure-stack-vm-considerations/vm-extensions.png)

Используйте hello после списка hello tooget сценария PowerShell расширений виртуальной машины, которые доступны в среде Azure стека:

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>Версии API 

Особенности виртуальных машин в пакете средств разработки стек Azure поддерживают следующие версии API hello:

![Типы ресурсов виртуальной Машины](media/azure-stack-vm-considerations/vm-resoource-types.png)

Можно использовать следующие версии API hello tooget сценария PowerShell для функции hello виртуальной машины, доступные в вашей среде Azure стека hello.

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
Hello список поддерживаемых типов ресурсов и версии API могут различаться, если оператор облака hello обновления вашей среды Azure стека tooa новой версии.

## <a name="next-steps"></a>Дальнейшие действия

[Создание виртуальной машины Windows с помощью PowerShell в стек Azure](azure-stack-quick-create-vm-powershell.md)
