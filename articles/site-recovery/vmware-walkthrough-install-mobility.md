---
title: "hello aaaInstall Mobility service с VMware tooAzure репликации | Документы Microsoft"
description: "В этой статье описывается, как tooinstall hello агент службы Mobility service для VMware tooAzure репликации со службой Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>Шаг 10: Установка службы Mobility hello


В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure виртуальные машины VMware, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Hello службы Mobility service записывает записи данных на компьютере и пересылает их toohello сервер обработки. Он должен устанавливаться на каждом компьютере, которые должны tooreplicate tooAzure.

Можно установить hello Mobility service вручную, с помощью принудительной установки с сервера обработки hello Site Recovery, если включена репликация, или воспользоваться средством System Center Configuration Manager. При использовании принудительной установки службы hello устанавливается на hello виртуальной Машины при включена репликация.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Установка вручную

1. Проверьте hello [необходимые компоненты](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) для установки вручную.
2. Выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) для установки вручную с помощью портала hello.
3. При желании tooinstall hello командной строке выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Установка с сервера обработки hello

Если требуется установка службы Mobility hello toopush с сервера обработки hello при включении репликации для виртуальной Машины, необходимо учетную запись, которая может использоваться hello процесса сервера tooaccess hello виртуальной Машины. Hello учетная запись используется только для принудительной установки hello.

1. Необходимо [создать учетную запись](vmware-walkthrough-prepare-vmware.md), которая может использоваться для принудительной установки. Затем следует указать hello имени учетной записи которого toouse во время настройки источника во время развертывания службы восстановления сайтов.
2. Затем выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Если toopush hello Mobility service на виртуальные машины под управлением Windows или Linux.

## <a name="other-methods"></a>Другие методы

Дополнительные сведения о [Установка службы мобильности hello, с помощью Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), или с помощью [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 11: включение репликации](vmware-walkthrough-enable-replication.md)
