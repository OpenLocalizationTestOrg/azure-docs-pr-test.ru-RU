---
title: "Предварительные требования hello aaaReview Hyper-V tooAzure репликации (System Center VMM) с помощью Azure Site Recovery | Документы Microsoft"
description: "Описание предварительных требований hello для настройки репликации, отработки отказа и восстановления виртуальных машин Hyper-V локально в tooAzure облака VMM, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Шаг 2: Просмотрите hello необходимые условия для tooAzure репликации Hyper-V (с помощью VMM)

Вы ознакомитесь hello [архитектура сценария](vmm-to-azure-walkthrough-architecture.md), чтение этой статьи toomake убедиться, что вы понимаете предварительные условия для развертывания hello. 

## <a name="prerequisites-and-limitations"></a>Предварительные требования и ограничения

**Требование** | **Дополнительные сведения**
--- | ---
**Учетная запись Azure** | Вам потребуется [учетная запись Microsoft Azure](http://azure.microsoft.com/).
**Служба хранилища Azure** | Необходимо, чтобы данные реплицируются toostore учетной записи хранилища Azure.<br/><br/> Учетная запись хранения Hello должна быть в hello же регионе, что hello в хранилище служб восстановления Azure.<br/><br/>Вы можете использовать [геоизбыточное хранилище](../storage/common/storage-redundancy.md#geo-redundant-storage) или локально избыточное хранилище. Рекомендуется использовать геоизбыточное хранилище. С географически избыточное хранилище данных отказоустойчивой региональном сбое происходит ли основной регион hello не может быть восстановлена.<br/><br/> Вы можете использовать стандартную учетную запись хранения Azure или [хранилище Azure класса Premium](../storage/common/storage-premium-storage.md). В хранилище класса Premium могут размещаться рабочие нагрузки с большим количеством операций ввода-вывода. Обычно оно используется для виртуальных машин, которым постоянно требуется высокая производительность операций ввода-вывода и малая задержка. Если вы используете хранилище класса Premium для реплицируемых данных, вам также понадобится стандартная учетная запись хранения. Стандартная учетная запись хранения сохраняет журналов репликации, захватывающих данные локальной tooon текущие изменения.
**Сеть Azure** | Требуется [сети Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md), после отработки отказа подключаться toowhich виртуальных машинах Azure. Hello Azure сеть должна быть в hello же регионе, что hello в хранилище служб восстановления.
**Локальные серверы VMM** | Требуется один или несколько серверов VMM под управлением System Center 2012 R2 или более поздней версии.<br/><br/> Каждый сервер VMM должен содержать одно или несколько частных облаков. Для каждого облака требуется одна или несколько групп узлов.<br/><br/> Сервер VMM Hello требуется доступ к Интернету.
**Локальные серверы Hyper-V** | Серверы узла Hyper-V должны работать под управлением Windows Server 2012 R2 с включенной ролью hello Hyper-V или Microsoft Hyper-V Server 2012 R2. необходимо установить последние обновления Hello.<br/><br/> узел Hyper-V Hello должен быть расположен в группе узлов VMM (находится в облаке VMM).<br/><br/> Узел должен иметь один или несколько виртуальных машин, которые должны tooreplicated.<br/><br/> Узлы Hyper-V должен быть подключенным toohello Интернет для репликации tooAzure, непосредственно или с прокси-сервера. Серверы Hyper-V должны иметь hello исправления, описанные в статье [2961977](https://support.microsoft.com/kb/2961977).
**Локальные виртуальные машины Hyper-V** | Виртуальные машины, нужно tooreplicate должна быть запущена [поддерживаемой операционной системы](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)и соответствовать [Azure необходимые условия](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). После включения репликации можно изменить имя виртуальной Машины Hello. 




## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 3: Планирование емкости](vmm-to-azure-walkthrough-capacity.md)
