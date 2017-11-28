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
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="725ec-103">Шаг 9: Установка службы Mobility hello</span><span class="sxs-lookup"><span data-stu-id="725ec-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="725ec-104">В этой статье описывается, как компонент службы hello Mobility tooinstall при репликации локальной tooAzure физических серверов Windows и Linux, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="725ec-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="725ec-105">Hello службы Mobility service записывает записи данных на компьютере и пересылает их toohello сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="725ec-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="725ec-106">Он должен устанавливаться на каждом сервере, которые должны tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="725ec-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="725ec-107">Можно установить службу Mobility hello вручную или с помощью принудительной установки из hello Site Recovery процесса сервера, если включена репликация, или с помощью средства, такие как System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="725ec-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="725ec-108">При использовании принудительной установки службы hello устанавливается на сервере hello при включении репликации.</span><span class="sxs-lookup"><span data-stu-id="725ec-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="725ec-109">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="725ec-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="725ec-110">Установка вручную</span><span class="sxs-lookup"><span data-stu-id="725ec-110">Install manually</span></span>

1. <span data-ttu-id="725ec-111">Проверьте hello [необходимые компоненты](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) для установки вручную.</span><span class="sxs-lookup"><span data-stu-id="725ec-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="725ec-112">Выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) для установки вручную с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="725ec-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="725ec-113">При желании tooinstall hello командной строке выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="725ec-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="725ec-114">Установка с сервера обработки hello</span><span class="sxs-lookup"><span data-stu-id="725ec-114">Install from hello process server</span></span>

<span data-ttu-id="725ec-115">Если требуется hello toopush установки службы Mobility с сервера обработки hello при включении репликации для машины, необходимо учетную запись, которая может использоваться hello процесса tooaccess hello сервере.</span><span class="sxs-lookup"><span data-stu-id="725ec-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="725ec-116">Hello учетная запись используется только для принудительной установки hello.</span><span class="sxs-lookup"><span data-stu-id="725ec-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="725ec-117">Если вы еще не создали учетную запись, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="725ec-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="725ec-118">Можно использовать доменную или локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="725ec-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="725ec-119">Для Windows Если вы не используете учетную запись домена, необходимо toodisable управления удаленного доступа пользователя на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="725ec-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="725ec-120">toodo, hello зарегистрировать под **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, добавьте запись DWORD hello **LocalAccountTokenFilterPolicy**, со значением 1.</span><span class="sxs-lookup"><span data-stu-id="725ec-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="725ec-121">Если требуется запись реестра hello tooadd для Windows с CLI, введите:</span><span class="sxs-lookup"><span data-stu-id="725ec-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="725ec-122">Для Linux hello учетной записи должно быть корневым расположением на hello исходный сервер Linux.</span><span class="sxs-lookup"><span data-stu-id="725ec-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="725ec-123">Затем выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Если toopush hello Mobility service на виртуальные машины под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="725ec-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="725ec-124">Другие методы установки</span><span class="sxs-lookup"><span data-stu-id="725ec-124">Other installation methods</span></span>

- <span data-ttu-id="725ec-125">[Дополнительные сведения о](site-recovery-install-mobility-service-using-sccm.md) Установка службы мобильности hello, с помощью Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="725ec-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="725ec-126">Сведения об установке службы Mobility Service с помощью Azure Automation DSC см. [здесь](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="725ec-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="725ec-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="725ec-127">Next steps</span></span>

<span data-ttu-id="725ec-128">Go слишком[шаг 10: включение репликации](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="725ec-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
