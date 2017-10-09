---
title: "Необходимые условия hello aaaReview для Hyper-V репликации tooa вторичный сайт VMM с помощью Azure Site Recovery | Документы Microsoft"
description: "Описание предварительных требований hello для репликации виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Шаг 2: Просмотрите hello предварительные требования и ограничения для виртуальных Машин Hyper-V репликации tooa вторичного сайта, VMM


После знакомства hello [архитектура сценария](vmm-to-vmm-walkthrough-architecture.md), чтение этой статьи toomake изучить предварительные требования для развертывания hello, при репликации в локальной среде Hyper-V виртуальных машин (ВМ) управляемого кода в System Center виртуальный Облаков Machine Manager (VMM), tooa вторичного сайта с помощью [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Предварительные требования и ограничения

**Требование** | **Дополнительные сведения**
--- | ---
**Таблицы Azure** | [Подписка Microsoft Azure](http://azure.microsoft.com/).<br/><br/> Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [дополнительными сведениями](https://azure.microsoft.com/pricing/details/site-recovery/) о ценах на использование Site Recovery.<br/><br/> Проверьте областей hello поддерживается для восстановления сайта в группе географическая доступность в [сведения о ценах Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
**Серверы VMM** | Мы рекомендуем иметь двух серверов VMM, в первичном сайте hello и по одному в hello получателей.<br/><br/> Поддерживается репликация между облаками на одном сервере VMM.<br/><br/> Серверы VMM должен работать под управлением System Center 2012 SP1 с последними обновлениями hello.<br/><br/> Серверам VMM нужен доступ к Интернету.
**Облака VMM** | Каждый сервер VMM, должна иметь на одно или несколько облаков, а все облака должен иметь набор профилей hello емкости Hyper-V. <br/><br/>Облака должны содержать одну или несколько групп узлов VMM.<br/><br/> Если имеется только один сервер VMM, он должен, по крайней мере два облака, tooact как первичный и вторичный.
**Hyper-V** | Серверы Hyper-V должны работать под управлением Windows Server 2012 с ролью Hyper-V hello и иметь hello установлены последние обновления.<br/><br/> Сервер Hyper-V должен содержать одну или несколько виртуальных машин.<br/><br/>  Серверы узла Hyper-V должны находиться в группах узлов в hello Первичное и вторичное облака VMM.<br/><br/> Если Hyper-V выполняется в кластере на платформе Windows Server 2012 R2, установите [обновление 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Если Hyper-V выполняется в кластере на платформе Windows Server 2012, учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов. Вручную настройте брокер кластера hello. [Подробная информация](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Серверам Hyper-V необходим доступ к Интернету.




## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 3: Планирование сети](vmm-to-vmm-walkthrough-network.md).
