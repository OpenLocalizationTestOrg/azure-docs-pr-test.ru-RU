---
title: "aaaTroubleshoot развертывания виртуальной Машины с Linux-RM | Документы Microsoft"
description: "Устранение неполадок развертывания Resource Manager при создании виртуальной машины Linux в Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Устранение неполадок в развертывании Resource Manager при создании виртуальной машины Linux в Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Наиболее важные проблемы
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Описание других ситуаций и вопросов, связанных с развертыванием виртуальных машин, см. в статье [Устранение неполадок при развертывании виртуальных машин Linux в Azure](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Сбор журналов действий
Устранение неполадок, toostart действие сбор hello записывает ошибку tooidentify hello, связанной с проблемой hello. Hello следующие ссылки содержат подробную информацию по toofollow процесса hello.

[Просмотр операций развертывания с помощью Azure Resource Manager](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Просматривать журналы действий toomanage Azure ресурсы](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** Если hello ОС Linux обобщены и его отправки и/или записанный с помощью hello обобщенный параметр, то не будет ошибок. Аналогично Если hello ОС Linux специализированные и его отправки и/или захватить с hello специализированные параметр, то не будет ошибок.

**Ошибки передачи:**

**N<sup>1</sup>:** Если hello ОС Linux обобщенный и передается как специализированными, вы получите подготовки ошибку времени ожидания, так как на стадии подготовки hello застряла hello виртуальной Машины.

**N<sup>2</sup>:** Если hello ОС Linux специализированные и отправкой как обобщенный, вы получите инициализации: сбой, так как hello новой виртуальной Машины, выполнив hello исходное имя компьютера, имя пользователя и пароль.

**Способы устранения:**

Отправить tooresolve оба эти ошибки Здравствуйте исходного VHD, доступных в локальной среде, с hello же задание, что и для hello ОС (обобщенный/специализированные). tooupload как обобщены, помните toorun-сначала отзыв.

**Ошибки записи:**

**N<sup>3</sup>:** Если hello ОС Linux обобщенный и записывается в виде специализированными, вы получите подготовки ошибка тайм-аута из-за hello исходной виртуальной Машины не может использоваться как она помечена как обобщенный.

**N<sup>4</sup>:** Если специализированные Linux, и она записывается как обобщенный hello операционной системы, вы получите инициализации: сбой, так как hello новой виртуальной Машины, выполнив hello исходное имя компьютера, имя пользователя и пароль. Кроме того, исходный hello виртуальной Машины не выполняется, так как она помечена как специальные.

**Способы устранения:**

tooresolve оба эти ошибки удалить текущее изображение hello из портала hello и [захватить снова из hello текущего виртуальные жесткие диски](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) с "hello" того же параметра, что и для hello ОС (обобщенный/специализированные).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Проблема: ошибка выделения (пользовательский образ, образ из коллекции или Marketplace)
Эта ошибка возникает в ситуациях, при получении новой виртуальной Машины запроса hello закрепленных tooa кластера, либо не поддерживает размер виртуальной Машины hello запрашиваемого, либо не имеет доступного свободного места tooaccommodate hello запроса.

**Причина 1:** hello кластера не поддерживают hello запрошенный размер виртуальной Машины.

**Способ устранения 1.**

* Повторите запрос hello, с использованием меньшего размера виртуальной Машины.
* Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:
  * Остановите все виртуальные машины hello в наборе доступности hello.
    Для этого последовательно выберите **Группы ресурсов** > *имя вашей группы ресурсов* > **Ресурсы** > *имя вашей группы доступности* > **Виртуальные машины** > *имя вашей виртуальной машины* > **Остановить**.
  * После всех hello остановка виртуальных машин, создайте hello новой виртуальной Машины в hello требуемого размера.
  * Запустить сначала hello новой виртуальной Машины, а затем выберите каждый hello остановлен, виртуальные машины и нажмите кнопку **запустить**.

**Причина 2:** hello кластер не имеет свободных ресурсов.

**Способ устранения 2.**

* Повторите запрос hello позже.
* Если hello новой виртуальной Машины можно указать различные доступности
  * Создание новой виртуальной Машины в наборе доступности на другой (в hello одного региона).
  * Добавление новой виртуальной Машины toohello hello одной виртуальной сети.

## <a name="next-steps"></a>Дальнейшие действия
При возникновении проблем во время запуска остановленной виртуальной машины Linux или в случае изменения размера существующей виртуальной машины Linux в Azure см. раздел [Устранение неполадок в развертывании Resource Manager при перезагрузке или изменении размера существующей виртуальной машины Linux в Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

