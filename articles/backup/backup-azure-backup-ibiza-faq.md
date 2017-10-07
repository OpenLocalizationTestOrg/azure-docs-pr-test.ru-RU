---
title: "часто задаваемые вопросы о хранилище службы aaaRecovery | Документы Microsoft"
description: "Эта версия hello часто задаваемые вопросы о поддерживает выпуск общедоступной предварительной версии hello hello службы архивации Azure. Вопросы и ответы о hello резервного копирования, резервного копирования и хранения, восстановления, безопасности и другие распространенные вопросы о hello решение для резервного копирования Azure toofrequently ответы."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "решение для архивации; служба архивации"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Хранилище служб восстановления — вопросы и ответы
В этой статье содержатся сведения о конкретных tooRecovery служб хранилища и используется в качестве дополнения hello [резервного копирования Azure часто задаваемые вопросы о](backup-azure-backup-faq.md). Hello часто задаваемые вопросы резервного копирования Azure предоставляет полный набор hello вопросы и ответы о hello службы архивации Azure.  

Можно задать вопросы о службе архивации Azure в hello Disqus раздел в данной статье или связанные статьи. Вы также можете публиковать вопросы о hello службы архивации Azure в hello [дискуссионный форум](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Хранилища служб восстановления развернуты с помощью Resource Manager. Поддерживаются ли еще хранилища службы архивации, развернутые с помощью классической модели? <br/>
Да, хранилища службы архивации по-прежнему поддерживаются. Создание хранилищ архивации в hello [классический портал](https://manage.windowsazure.com). Создание хранилищ служб восстановления в hello [портал Azure](https://portal.azure.com). Однако настоятельно рекомендуется вы toocreate хранилище служб восстановления все будущие улучшения будут доступны только в хранилище служб восстановления.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Можно перенести хранилище служб восстановления хранилище tooa резервной копии <br/>
К сожалению нет, в данный момент нельзя перенести содержимое hello tooa хранилища резервной копии, в хранилище служб восстановления. Мы работаем над добавлением этих функциональных возможностей, но они не входят в этот общедоступный предварительный выпуск.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Какие виртуальные машины поддерживают хранилища служб восстановления: классические ВМ или ВМ на основе Resource Manager? <br/>
Хранилища служб восстановления поддерживают обе модели.  Можно выполнять резервное копирование виртуальной Машины, созданной на портале классический hello (которые являются виртуальными машинами в классическом режиме) или создать виртуальную Машину в hello портал Azure (они диспетчер ресурсов на основе) в хранилище служб восстановления tooa.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>Резервные копии классических виртуальных машин созданы в хранилище службы архивации. Теперь я хочу toomigrate моих виртуальных машин из диспетчера tooResource классический режим.  Как выполнить их резервное копирование в хранилище служб восстановления?
Резервные копии в резервном хранилище для классических ВМ не будет автоматически перенести toorecovery хранилище служб, при переносе hello виртуальных машин из tooResource классический режим диспетчера. Выполнить перенос резервных копий виртуальных машин можно так.

1. В резервном хранилище go слишком**защищенные элементы** и выберите hello виртуальной Машины. Щелкните [Остановить защиту](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). *Снимите* флажок **Удаление связанных архивируемых данных**.
2. В hello [портал Azure](https://portal.azure.com), go toohello **расширения** меню hello ВМ и удалить hello **VMSnapshot/VMSnapshotLinux** расширения.
3. Миграция виртуальной машины hello из диспетчера tooResource классический режим. Убедитесь, что хранилища и сети соответствующий toovirtual машины, также режим перенесенных tooResource диспетчера.
4. Создать хранилище служб восстановления и настроить виртуальную машину с помощью резервной копии на hello перенести **резервного копирования** действия на основе мониторинга хранилища. Дополнительные сведения о том, как слишком[включить резервное копирование в хранилище служб восстановления](backup-azure-vms-first-look-arm.md)
