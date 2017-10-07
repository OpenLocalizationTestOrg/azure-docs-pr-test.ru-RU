---
title: "aaaPrepare System Center VMM для tooAzure репликации Hyper-V | Документы Microsoft"
description: "Описывает способ tooprepare сервера System Center VMM для tooAzure репликации Hyper-V, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Шаг 6: Подготовка серверов VMM и узлы Hyper-V для tooAzure репликации Hyper-V

После настройки [компонентов Azure](vmm-to-azure-walkthrough-prepare-azure.md) hello развертывания, используйте инструкции hello в этой статье tooprepare локальных серверов VMM и toointeract узлов Hyper-V с помощью Azure Site Recovery.

После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Подготовка серверов VMM

- Необходим по крайней мере один сервер VMM, который отвечает требованиям hello поддержки для восстановления сайта репликации (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Убедитесь, что вы подготовили hello сервера VMM для [сетевое сопоставление](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Убедитесь, что этот сервер VMM hello доступны такие URL-адреса

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.
- Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).
- Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).

Во время развертывания службы восстановления сайтов Загрузите hello поставщика восстановления сайта и установить его на каждом сервере VMM. Hello сервер VMM зарегистрирован в hello в хранилище служб восстановления.




## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 7: Создание хранилища](vmm-to-azure-walkthrough-create-vault.md)

