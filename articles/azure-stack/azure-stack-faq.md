---
title: "вопросы и ответы для стека Azure aaaFrequently | Документы Microsoft"
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
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a>Часто задаваемые вопросы про Azure стека
## <a name="deployment"></a>Развертывание
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a>Нужен ли мне tooformat диски с данными до запуска или перезапуска установки?
Диски должны находиться в необработанном формате. При переустановке операционной системы hello может требуется toocheck, если пул носителей старого hello по-прежнему присутствует и удаления с помощью hello следующие шаги:

1. Откройте диспетчер сервера.
2. Выберите пулы носителей.
3. Если пул носителей отображается в разделе.
4. Щелкните правой кнопкой мыши **пула носителей** Если в списке и включить чтения / записи.
5. Щелкните правой кнопкой мыши **виртуальный жесткий диск** (нижнем левом углу) и выберите Удалить.
6. Щелкните правой кнопкой мыши **пула носителей** и нажмите кнопку Удалить.
7. Перед повторным запуском сценария Azure стека и проверьте, проходит проверку диска hello.

При необходимости можно использовать следующий скрипт hello:

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a>Можно использовать все диски SSD в пуле носителей hello в hello подтверждения Концепции установки?
Дополнительные сведения о конфигурации хранилища см. в разделе hello [руководство по требованиям к](azure-stack-deploy.md).

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a>Можно использовать диски данных NVMe для hello эта стека Microsoft Azure?
Хотя Storage Spaces Direct поддерживает NVMe дисков, стек Azure поддерживает только подмножество типов возможных дисков hello и возможных сочетаний для дисковых пространств.  В разделе hello [руководство по требованиям к](azure-stack-deploy.md) для получения дополнительной информации. 

### <a name="how-can-i-reinstall-azure-stack"></a>Как можно переустановить стек Azure
Выполните действия hello в hello [руководство повторного развертывания](azure-stack-redeploy.md).  

## <a name="tenant"></a>Клиент
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a>Можно развернуть собственный изображения как клиента
Да, так же, как в Azure, клиент может отправить изображений в стек Azure, кроме администратора службы toousing hello изображений из hello. Общие сведения см. в разделе hello [Добавление образа виртуальной Машины](azure-stack-add-vm-image.md). 

## <a name="testing"></a>Тестирование
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a>Можно использовать hello tootest вложенной виртуализации эта стека Microsoft Azure?
Вложенная виртуализация не поддерживается и не протестированы с Azure стека Technical Preview 3.

## <a name="virtual-machines"></a>Виртуальные машины
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a>Стек Azure поддерживает динамические диски для виртуальных машин?
Стек Azure не поддерживает динамические диски.


## <a name="next-steps"></a>Дальнейшие действия
[Устранение неполадок](azure-stack-troubleshooting.md)

