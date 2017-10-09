---
title: "выдает aaaVM перезапуске и изменении размера в Azure | Документы Microsoft"
description: "Устранение неполадок в развертывании Resource Manager при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Устранение неполадок в развертывании при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure
При попытке toostart остановленной виртуальной машины (ВМ) Azure, или изменить размер существующей ВМ Azure, hello распространенных ошибок, возникающих — ошибки выделения. Эта ошибка возникает, когда hello кластера или регион либо не имеет доступных ресурсов или не hello поддержки запрошенный размер виртуальной Машины.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Сбор журналов действий
Устранение неполадок, toostart действие сбор hello записывает ошибку tooidentify hello, связанной с проблемой hello. Hello следующие ссылки содержат подробные сведения о процессе hello:

[Просмотр операций развертывания с помощью Azure Resource Manager](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Просматривать журналы действий toomanage Azure ресурсы](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Проблема: ошибка во время запуска остановленной виртуальной машины
Повторите toostart остановленной виртуальной Машины, но получить ошибки выделения.

### <a name="cause"></a>Причина:
запрос Hello toostart hello остановлен, виртуальная машина имеет toobe попытки в hello исходного кластера, на котором размещена hello облачной службы. Однако hello кластер не имеет запрос hello доступных toofulfill свободного места.

### <a name="resolution"></a>Способы устранения:
* Остановите все hello виртуальных машин в доступности hello установить, а затем перезапустите каждой виртуальной Машины.
  
  1. Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.
  2. После того как все Здравствуйте остановка виртуальных машин, выберите каждый hello остановлена виртуальные машины и нажмите кнопку Пуск.
* Повторите запрос перезапуск hello позже.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Проблема: ошибка при изменении размера существующей виртуальной машины
Повторите tooresize существующей виртуальной Машины, но получить ошибки выделения.

### <a name="cause"></a>Причина:
Hello hello tooresize виртуальная машина имеет toobe пытался выполнить запрос в исходном кластере hello, узлы hello облачной службы. Однако кластер hello не поддерживает hello запрошенный размер виртуальной Машины.

### <a name="resolution"></a>Способы устранения:
* Повторите запрос hello, с использованием меньшего размера виртуальной Машины.
* Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:
  
  1. Остановите все виртуальные машины hello в наборе доступности hello.
     
     * Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.
  2. После того как все Здравствуйте остановка виртуальных машин, изменение размера hello требуемого ВМ tooa большего размера.
  3. Выберите hello размера виртуальной Машины и нажмите кнопку **запустить**, и затем запустите все hello остановлено виртуальных машин.

## <a name="next-steps"></a>Дальнейшие действия
При возникновении проблем во время создания виртуальной машины Linux в Azure см. статью, посвященную [устранению неполадок в развертывании](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

