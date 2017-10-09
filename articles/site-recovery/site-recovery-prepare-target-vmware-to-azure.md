---
title: "Подготовка целевого (VMware tooAzure) | Документы Microsoft"
description: "В этой статье описывается как tooprepare toostart вашей среды Azure, репликация tooAzure виртуальных машин VMware."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Подготовка целевого (VMware tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Физический tooAzure](./site-recovery-prepare-target-physical-to-azure.md)

В этой статье описывается как tooprepare toostart вашей среды Azure, репликация tooAzure виртуальных машин VMware.

## <a name="prerequisites"></a>Предварительные требования

Hello предполагается hello следующее:
- Вы создали tooprotect хранилище служб восстановления виртуальных машин VMware. Можно создать хранилище служб восстановления из hello [портал Azure](http://portal.azure.com "портал Azure").
- У вас есть [установки в локальной среде](./site-recovery-set-up-vmware-to-azure.md) tooAzure виртуальных машин VMware tooreplicate.

## <a name="prepare-target"></a>Подготовка цели

После завершения hello **цель защиты 1:Select шаг** и **шаг 2: Подготовка источника**, вы попадаете слишком**Step 3: целевой**

![Подготовка цели](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Подписки:** из hello раскрывающееся меню, выберите hello подписку, которую нужно tooreplicate виртуальных машин.
2. **Модель развертывания:** hello выберите модель развертывания (классический или диспетчер ресурсов)

На основании выбранной модели развертывания hello, проверка выполняется tooensure, у вас есть по крайней мере один совместимую учетную запись хранения и виртуальной сети в tooreplicate подписки целевой hello и отработку отказа виртуальной машины.

По завершении проверки приветствия нажмите кнопку ОК toogo toohello следующий шаг.

Если у вас нет совместимых учетной записи диспетчера ресурсов хранилища или виртуальной сети или хотите tooadd дополнительные, это можно сделать, щелкнув hello **+ учетная запись хранения** или **+ сети** кнопками над hello hello колонки.

## <a name="next-steps"></a>Дальнейшие действия
[Настройка параметров репликации](./site-recovery-setup-replication-settings-vmware.md).
