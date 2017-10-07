---
title: "aaaConfigure сетевое сопоставление для репликации виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery | Документы Microsoft"
description: "Описывает, каким образом tooconfigure сетевое сопоставление, при репликации виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Шаг 9: Настройка сопоставления сетей для Hyper-V tooAzure репликации (с помощью VMM)

После настройки hello [исходной и целевой настройки репликации](vmm-to-azure-walkthrough-source-target.md), используйте этот toomap статьи tooconfigure сетевого сопоставления между локальными сетями виртуальной Машины VMM и сетями Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Перед началом

- Узнайте о [сопоставлении сети](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [Подготовьте VMM к сопоставлению сети](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Убедитесь, виртуальные машины на сервере VMM hello tooa подключенной сети виртуальной Машины, и что вы создали по крайней мере одна виртуальная сеть Azure. Несколько сетей виртуальной Машины может быть сопоставленных tooa одной сетью Azure.

## <a name="configure-mapping"></a>Настройка сопоставления

Настройте сопоставление следующим образом:

1. В **инфраструктура Site Recovery** > **сетевого сопоставления** > **сетевое сопоставление**, нажмите кнопку hello **+ сетевое сопоставление**  значок.

    ![Сетевое сопоставление](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. В **добавить сопоставление сети**выберите hello исходном сервере VMM, и **Azure** как целевой hello.
3. Проверка подписки hello и модель развертывания hello после отработки отказа.
4. В **Исходная сеть**выберите hello исходную сеть виртуальных Машин в локальной среде требуется toomap из списка hello, связанные с сервером VMM hello.
5. В **целевой сети**, выберите hello реплик виртуальных машин Azure будет находиться во время создания сети Azure. Нажмите кнопку **ОК**.

    ![Сетевое сопоставление](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Когда начинается сопоставление сетей, происходит следующее:

* Существующих виртуальных машин в исходной сети VM hello, подключенных toohello целевой сети, когда начинает сопоставление. Новые виртуальные машины подключенных toohello исходную сеть виртуальных Машин подключены toohello сопоставлено сетью Azure при выполнении репликации.
* Можно изменить существующее сопоставление сети, виртуальные машины реплики подключаться с использованием новых параметров hello.
* Если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, то виртуальная машина реплики hello подключается toothat целевой подсети после отработки отказа.
* Если никакой целевой подсети с совпадающим именем виртуальной машины hello подключается toohello первой подсети в сети hello.



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 10: Создание политики репликации](vmm-to-azure-walkthrough-replication.md)
