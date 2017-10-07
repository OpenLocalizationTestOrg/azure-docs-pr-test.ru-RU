---
title: "размещает aaaPrepare Hyper-V (без System Center VMM) для репликации tooAzure | Документы Microsoft"
description: "Описывает способ размещения tooprepare Hyper-V для tooAzure репликации с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Шаг 6: Подготовка узлов Hyper-V для репликации tooAzure

Используйте инструкции hello в этой статье tooprepare локальной toointeract узлов Hyper-V с помощью Azure Site Recovery.

После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Подготовка узлов

- Убедитесь, что узлы Hyper-V hello соответствуют hello [необходимых компонентов](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Убедитесь, что доступность узлов hello hello требуется URL-адреса:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.
- Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).
- Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).

Во время развертывания службы восстановления сайтов Добавление узлов Hyper-V, содержащие виртуальные машины, вы хотите узел tooreplicate tooa Hyper-V. Hello поставщика Site Recovery и агента служб восстановления устанавливаются на каждом узле. узел Hyper-V Hello зарегистрирован в hello в хранилище служб восстановления.

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 7: Создание хранилища](hyper-v-site-walkthrough-create-vault.md)

