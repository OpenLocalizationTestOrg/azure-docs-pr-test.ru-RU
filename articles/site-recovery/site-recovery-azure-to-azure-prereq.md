---
title: "aaaPrerequisites для tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "В этой статье перечислены необходимые условия для репликации виртуальных машин и физических машин tooAzure с помощью службы Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Необходимые условия для репликации виртуальных машин Azure tooanother области с помощью Azure Site Recovery

> [!div class="op_single_selector"]
> * [Репликация из Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Репликация из локальной tooAzure](site-recovery-prereq.md)

Hello служба восстановления сайтов Azure поддерживает tooyour бесперебойной работе и стратегии аварийного восстановления (BCDR), управляя операциями:
* Репликация виртуальных машин Azure tooanother регион Azure.
* Репликация локальных физических серверов и виртуальных машин tooAzure или tooa вторичный центр обработки данных. 

При возникновении сбоев в расположение источника, можно выполнить переход tooa вторичное расположение tookeep приложений и рабочих нагрузок доступны. Основное расположение задней tooyour может завершиться ошибкой, при возвращении toonormal операций. Дополнительные сведения о службе Site Recovery см. в [этой статье](site-recovery-overview.md).

В этой статье перечислены необходимые toobegin hello необходимые компоненты репликации Site Recovery из локальной tooAzure.

Отправлять все комментарии внизу hello hello статьи или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Требования Azure

**Требование** | **Дополнительные сведения**
--- | ---
**Учетная запись Azure** | Учетная запись [Microsoft Azure](http://azure.microsoft.com/) .<br/><br/> Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
**Служба Azure Site Recovery** | Дополнительные сведения о ценах на службу Site Recovery см. [здесь](https://azure.microsoft.com/pricing/details/site-recovery/). Рекомендуется создавать хранилище служб восстановления, в конечном hello регион Azure, которые должны toouse как расположение для аварийного восстановления. Например если хотите tooreplicate tooCentral источника виртуальные машины работают в Восток США, рекомендуется создать хранилище hello в центральной части США.|
**Производительность Azure** | Для целевого объекта hello регион Azure, что toouse должен быть точкой восстановления после сбоя необходимо toohave подписки с емкостью, достаточной для виртуальных машин, учетных записей хранения и сетевых компонентов. Вы можете обратиться tooadd поддержки более емкости.
**Рекомендации по выбору хранилища** | Убедитесь, что выполнены hello [руководство по организации хранилища](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) источника Azure виртуальных машин tooavoid проблем производительности. Если следовать параметры по умолчанию hello Site Recovery создает hello необходимые учетные записи хранения на основе конфигурации источника hello. Если настроить и выбрать собственные параметры, убедитесь, что выполнены hello [целевые показатели масштабируемости для дисков виртуальной машины](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Рекомендации по организации сети** | Вам требуется toowhitelist hello исходящие подключения из виртуальной Машины Azure, для определенного URL-адреса или IP-диапазонов. Дополнительные сведения см. в разделе toohello [рекомендации для репликации виртуальных машин Azure к сети](site-recovery-azure-to-azure-networking-guidance.md) статьи.
**Azure** | Убедитесь, что все корневые сертификаты последнюю hello, присутствуют на ВМ Linux или hello Windows. Если отсутствуют последние корневые сертификаты hello, hello виртуальной Машины не может быть зарегистрированных tooSite восстановления из-за ограничений toosecurity.

>[!NOTE]
>Дополнительные сведения о поддержке для конкретных конфигураций чтения hello [Матрица поддержки](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Дальнейшие действия
- Ознакомьтесь со статьей [Руководство по организации сети для репликации виртуальных машин Azure](site-recovery-azure-to-azure-networking-guidance.md).
- Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure](site-recovery-azure-to-azure.md).
