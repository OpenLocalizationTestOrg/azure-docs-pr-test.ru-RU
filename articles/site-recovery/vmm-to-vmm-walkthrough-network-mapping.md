---
title: "aaaMap сетей для виртуальных Машин Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, каким образом toomap сети при репликации виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Шаг 7: Сопоставление сетей для виртуальных Машин Hyper-V репликации tooa вторичного сайта


После настройки [источника и целевых параметров](vmm-to-vmm-walkthrough-source-target.md) для репликации Hyper-V виртуальных машин (ВМ) tooa вторичный сайт, диспетчер виртуальных машин System Center (VMM), использовать в этой статье tooconfigure сетевое сопоставление для Hyper-V виртуального tooa репликации машины (VM) вторичного сайта, с помощью [Azure Site Recovery](site-recovery-overview.md).

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Перед началом работы

- Прежде чем начинать работу, изучите сведения о [сетевом сопоставлении](vmm-to-vmm-walkthrough-network.md#network-mapping-overview).
- Убедитесь, что виртуальные машины на серверах VMM tooa подключенной сети виртуальной Машины.

## <a name="configure-network-mapping"></a>Настройка сетевого сопоставления

1. В области **Сетевое сопоставление** > **Сетевые сопоставления** щелкните **+Network Mapping** (+Сетевое сопоставление).
2. В **добавить сопоставление сети** выберите hello исходном и целевом серверах VMM. извлекаются Hello сетей виртуальных Машин, связанные с серверами VMM hello.
3. В **Исходная сеть**выберите hello сети, которую требуется toouse из списка hello сетей виртуальных Машин, связанные с hello первичного сервера VMM.
4. В **целевой сети**выберите hello сети, которую требуется toouse на вторичном сервере VMM hello. Нажмите кнопку **ОК**.

    ![Сетевое сопоставление](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Когда начинается сопоставление сетей, происходит следующее:

* Все существующие реплики виртуальных машин, соответствующих toohello исходную сеть виртуальных Машин будет подключенных toohello целевой сети ВМ.
* Новые виртуальные машины, подключенной toohello исходную сеть виртуальных Машин будет подключенных toohello целевой сопоставленные сетевые после репликации.
* При изменении существующего сопоставления с новой сети, виртуальные машины реплики будут подключены с использованием новых параметров hello.
* Если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, а затем hello реплики виртуальной машины после отработки отказа будет подключенных toothat целевой подсети. Если никакой целевой подсети с совпадающим именем, hello виртуальная машина будет подключенных toohello первой подсети в сети hello.



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 8: настроить политику репликации](vmm-to-vmm-walkthrough-replication.md).
