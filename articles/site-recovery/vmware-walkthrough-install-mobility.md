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
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="cd0be-103">Шаг 10: Установка службы Mobility hello</span><span class="sxs-lookup"><span data-stu-id="cd0be-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="cd0be-104">В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure виртуальные машины VMware, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0be-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="cd0be-105">Hello службы Mobility service записывает записи данных на компьютере и пересылает их toohello сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="cd0be-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="cd0be-106">Он должен устанавливаться на каждом компьютере, которые должны tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cd0be-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="cd0be-107">Можно установить hello Mobility service вручную, с помощью принудительной установки с сервера обработки hello Site Recovery, если включена репликация, или воспользоваться средством System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="cd0be-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="cd0be-108">При использовании принудительной установки службы hello устанавливается на hello виртуальной Машины при включена репликация.</span><span class="sxs-lookup"><span data-stu-id="cd0be-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="cd0be-109">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cd0be-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="cd0be-110">Установка вручную</span><span class="sxs-lookup"><span data-stu-id="cd0be-110">Install manually</span></span>

1. <span data-ttu-id="cd0be-111">Проверьте hello [необходимые компоненты](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) для установки вручную.</span><span class="sxs-lookup"><span data-stu-id="cd0be-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="cd0be-112">Выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) для установки вручную с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="cd0be-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="cd0be-113">При желании tooinstall hello командной строке выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="cd0be-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="cd0be-114">Установка с сервера обработки hello</span><span class="sxs-lookup"><span data-stu-id="cd0be-114">Install from hello process server</span></span>

<span data-ttu-id="cd0be-115">Если требуется установка службы Mobility hello toopush с сервера обработки hello при включении репликации для виртуальной Машины, необходимо учетную запись, которая может использоваться hello процесса сервера tooaccess hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cd0be-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="cd0be-116">Hello учетная запись используется только для принудительной установки hello.</span><span class="sxs-lookup"><span data-stu-id="cd0be-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="cd0be-117">Необходимо [создать учетную запись](vmware-walkthrough-prepare-vmware.md), которая может использоваться для принудительной установки.</span><span class="sxs-lookup"><span data-stu-id="cd0be-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="cd0be-118">Затем следует указать hello имени учетной записи которого toouse во время настройки источника во время развертывания службы восстановления сайтов.</span><span class="sxs-lookup"><span data-stu-id="cd0be-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="cd0be-119">Затем выполните [эти инструкции](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Если toopush hello Mobility service на виртуальные машины под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="cd0be-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="cd0be-120">Другие методы</span><span class="sxs-lookup"><span data-stu-id="cd0be-120">Other methods</span></span>

<span data-ttu-id="cd0be-121">Дополнительные сведения о [Установка службы мобильности hello, с помощью Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), или с помощью [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="cd0be-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd0be-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd0be-122">Next steps</span></span>

<span data-ttu-id="cd0be-123">Go слишком[шаг 11: включение репликации](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cd0be-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
