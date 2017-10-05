---
title: "Установка службы Mobility Service для репликации из физических серверов в Azure | Документация Майкрософт"
description: "В этой статье описано, как с помощью службы Azure Site Recovery установить на физических серверах агент службы Mobility Service для репликации в Azure."
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
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="bcb34-103">Шаг 9. Установка службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="bcb34-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="bcb34-104">В этой статье описано, как установить компонент службы Mobility Service при репликации локальных физических серверов Windows или Linux в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb34-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="bcb34-105">Служба Mobility Service фиксирует операции записи данных на компьютере и перенаправляет их на сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="bcb34-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="bcb34-106">Ее необходимо установить на каждом сервере, который будет реплицироваться в Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb34-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="bcb34-107">Службу Mobility Service можно установить вручную, используя принудительную установку с сервера обработки Site Recovery, когда репликация включена, или с помощью такого средства, как System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bcb34-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="bcb34-108">При использовании принудительной установки служба устанавливается на сервере после включения репликации.</span><span class="sxs-lookup"><span data-stu-id="bcb34-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="bcb34-109">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bcb34-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="bcb34-110">Установка вручную</span><span class="sxs-lookup"><span data-stu-id="bcb34-110">Install manually</span></span>

1. <span data-ttu-id="bcb34-111">Проверьте, выполнены ли [предварительные требования](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) для установки вручную.</span><span class="sxs-lookup"><span data-stu-id="bcb34-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="bcb34-112">Следуйте [этим инструкциям](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui), чтобы выполнить установку вручную с помощью портала.</span><span class="sxs-lookup"><span data-stu-id="bcb34-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="bcb34-113">Если вам удобнее выполнить установку из командной строки, то следуйте [этим инструкциям](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="bcb34-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="bcb34-114">Установка с сервера обработки</span><span class="sxs-lookup"><span data-stu-id="bcb34-114">Install from the process server</span></span>

<span data-ttu-id="bcb34-115">Если требуется принудительно установить службу Mobility Service с сервера обработки при включении репликации компьютера, то необходима учетная запись, которая может использоваться сервером обработки для доступа к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="bcb34-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="bcb34-116">Эта учетная запись предназначена только для принудительной установки.</span><span class="sxs-lookup"><span data-stu-id="bcb34-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="bcb34-117">Если вы еще не создали учетную запись, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="bcb34-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="bcb34-118">Можно использовать доменную или локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="bcb34-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="bcb34-119">Для Windows, если учетная запись домена не используется, на локальном компьютере потребуется отключить контроль удаленного доступа пользователей.</span><span class="sxs-lookup"><span data-stu-id="bcb34-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="bcb34-120">Для этого в разделе реестра **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** добавьте запись **LocalAccountTokenFilterPolicy** DWORD и задайте для нее значение 1.</span><span class="sxs-lookup"><span data-stu-id="bcb34-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="bcb34-121">Если требуется добавить запись в реестр Windows из командной строки, введите:</span><span class="sxs-lookup"><span data-stu-id="bcb34-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="bcb34-122">Для Linux учетная запись должна принадлежать привилегированному пользователю на исходном сервере Linux.</span><span class="sxs-lookup"><span data-stu-id="bcb34-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="bcb34-123">Затем следуйте [этим инструкциям](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery), чтобы принудительно установить службу Mobility Service на виртуальные машины под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="bcb34-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="bcb34-124">Другие методы установки</span><span class="sxs-lookup"><span data-stu-id="bcb34-124">Other installation methods</span></span>

- <span data-ttu-id="bcb34-125">Сведения об установке службы Mobility Service с помощью Configuration Manager см. [здесь](site-recovery-install-mobility-service-using-sccm.md).</span><span class="sxs-lookup"><span data-stu-id="bcb34-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="bcb34-126">Сведения об установке службы Mobility Service с помощью Azure Automation DSC см. [здесь](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="bcb34-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bcb34-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bcb34-127">Next steps</span></span>

<span data-ttu-id="bcb34-128">Перейдите к статье [Шаг 10. Включение репликации для физических серверов в Azure](physical-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="bcb34-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
