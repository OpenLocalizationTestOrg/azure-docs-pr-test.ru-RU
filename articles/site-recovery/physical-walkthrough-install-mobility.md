---
title: "hello aaaInstall службы Mobility service для физического сервера репликации tooAzure | Документы Microsoft"
description: "В этой статье описывается, как tooinstall hello агент службы Mobility service на физических серверах репликации tooAzure со службой Azure Site Recovery hello."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Шаг 9: Установка службы Mobility hello


В этой статье описывается, как компонент службы hello Mobility tooinstall при репликации локальной tooAzure физических серверов Windows и Linux, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Hello службы Mobility service записывает записи данных на компьютере и пересылает их toohello сервер обработки. Он должен устанавливаться на каждом сервере, которые должны tooreplicate tooAzure.

Можно установить службу Mobility hello вручную или с помощью принудительной установки из hello Site Recovery процесса сервера, если включена репликация, или с помощью средства, такие как System Center Configuration Manager. При использовании принудительной установки службы hello устанавливается на сервере hello при включении репликации.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Установка вручную

1. Проверьте hello [необходимые компоненты](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) для установки вручную.
2. Выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) для установки вручную с помощью портала hello.
3. При желании tooinstall hello командной строке выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Установка с сервера обработки hello

Если требуется hello toopush установки службы Mobility с сервера обработки hello при включении репликации для машины, необходимо учетную запись, которая может использоваться hello процесса tooaccess hello сервере. Hello учетная запись используется только для принудительной установки hello.

1. Если вы еще не создали учетную запись, придерживайтесь следующих рекомендаций:

    - Можно использовать доменную или локальную учетную запись.
    - Для Windows Если вы не используете учетную запись домена, необходимо toodisable управления удаленного доступа пользователя на локальном компьютере hello. toodo, hello зарегистрировать под **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, добавьте запись DWORD hello **LocalAccountTokenFilterPolicy**, со значением 1.
    - Если требуется запись реестра hello tooadd для Windows с CLI, введите:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Для Linux hello учетной записи должно быть корневым расположением на hello исходный сервер Linux.

2. Затем выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Если toopush hello Mobility service на виртуальные машины под управлением Windows или Linux.

## <a name="other-installation-methods"></a>Другие методы установки

- [Дополнительные сведения о](site-recovery-install-mobility-service-using-sccm.md) Установка службы мобильности hello, с помощью Configuration Manager
- Сведения об установке службы Mobility Service с помощью Azure Automation DSC см. [здесь](site-recovery-automate-mobility-service-install.md).


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 10: включение репликации](physical-walkthrough-enable-replication.md)
