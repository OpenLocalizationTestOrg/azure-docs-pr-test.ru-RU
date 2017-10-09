---
title: "Необходимые условия hello aaaReview для репликации tooAzure по Hyper-V (без System Center VMM) с помощью Azure Site Recovery | Документы Microsoft"
description: "Описание предварительных требований hello для настройки репликации, отработки отказа и восстановления локальных виртуальных машин Hyper-V tooAzure с Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Шаг 2: Просмотрите hello необходимые условия для tooAzure репликации Hyper-V (без VMM)

Предварительные требования Hello, приведены в таблице hello.


**Предварительные требования** | **Дополнительные сведения** 
--- | --- 
**Таблицы Azure** | Ознакомьтесь с [требованиями Azure](site-recovery-prereq.md#azure-requirements).
**Локальные серверы** | [Дополнительные сведения](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) о требованиях для узлов Hyper-V hello в локальной среде.
**Локальные виртуальные машины Hyper-V** | Виртуальные машины, нужно tooreplicate должна быть запущена [поддерживаемой операционной системы](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)и соответствовать [Azure необходимые условия](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL-адреса Azure** | Узлы Hyper-V требуется доступ к toothese URL-адреса:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.<br/></br> Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).<br/></br> Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).



## <a name="next-steps"></a>Дальнейшие действия

- При выполнении полного развертывания, перейдите в слишком[Step 3: Планирование емкости](hyper-v-site-walkthrough-capacity.md)
- Если вы выполняете развертывание простых тестов, слишком перейдите[шаг 4: Планирование сети](hyper-v-site-walkthrough-network.md).
