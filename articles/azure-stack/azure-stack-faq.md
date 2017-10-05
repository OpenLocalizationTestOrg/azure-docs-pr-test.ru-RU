---
title: "Часто задаваемые вопросы про Azure стек | Документы Microsoft"
description: "Стек Azure часто задаваемые вопросы."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: b5ba09a1cc26e49c80bf50d6155bd0d938f1885b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a>Часто задаваемые вопросы про Azure стека
## <a name="deployment"></a>Развертывание
### <a name="do-i-need-to-format-my-data-disks-before-starting-or-restarting-an-installation"></a>Нужно ли форматировать диски с данными до запуска или перезапуска установки?
Диски должны находиться в необработанном формате. Если необходимо переустановить операционную систему, может потребоваться проверить, если все еще присутствует старый пул носителей и удалить, выполнив следующие действия:

1. Откройте диспетчер сервера.
2. Выберите пулы носителей.
3. Если пул носителей отображается в разделе.
4. Щелкните правой кнопкой мыши **пула носителей** Если в списке и включить чтения / записи.
5. Щелкните правой кнопкой мыши **виртуальный жесткий диск** (нижнем левом углу) и выберите Удалить.
6. Щелкните правой кнопкой мыши **пула носителей** и нажмите кнопку Удалить.
7. Перед повторным запуском сценария Azure стека и проверьте, проходит проверку на диске.

Кроме того можно использовать следующий скрипт:

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-the-storage-pool-in-the-poc-installation"></a>Можно использовать все диски SSD для пула носителей во время установки проверки Концепции
Дополнительные сведения о конфигурации хранилища см. в разделе [руководство по требованиям к](azure-stack-deploy.md).

### <a name="can-i-use-nvme-data-disks-for-the-microsoft-azure-stack-poc"></a>Можно использовать NVMe диски с данными для проверки Концепции стека Microsoft Azure?
Хотя Storage Spaces Direct поддерживает NVMe дисков, стек Azure поддерживает только подмножество типов возможных дисков и возможных сочетаний для дисковых пространств.  В разделе [руководство по требованиям к](azure-stack-deploy.md) для получения дополнительной информации. 

### <a name="how-can-i-reinstall-azure-stack"></a>Как можно переустановить стек Azure
Можно выполнить действия в [руководство повторного развертывания](azure-stack-redeploy.md).  

## <a name="tenant"></a>Клиент
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a>Можно развернуть собственный изображения как клиента
Да, так же, как в Azure, клиент можно отправить изображения в стек Azure, наряду с использованием изображения у администратора службы. Общие сведения см. в разделе [Добавление образа виртуальной Машины](azure-stack-add-vm-image.md). 

## <a name="testing"></a>Тестирование
### <a name="can-i-use-nested-virtualization-to-test-the-microsoft-azure-stack-poc"></a>Можно использовать вложенной виртуализации для тестирования подтверждение Концепции стека Microsoft Azure?
Вложенная виртуализация не поддерживается и не протестированы с Azure стека Technical Preview 3.

## <a name="virtual-machines"></a>Виртуальные машины
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a>Стек Azure поддерживает динамические диски для виртуальных машин?
Стек Azure не поддерживает динамические диски.


## <a name="next-steps"></a>Дальнейшие действия
[Устранение неполадок](azure-stack-troubleshooting.md)

