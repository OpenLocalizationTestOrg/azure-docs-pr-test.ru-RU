---
title: "aaaRemove серверы и отключите защиту | Документы Microsoft"
description: "Эта статья описывает, как хранилище toounregister серверы из Site Recovery и toodisable защиты для виртуальных машин и физических серверов."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="97442-103">Удаление серверов и отключение защиты</span><span class="sxs-lookup"><span data-stu-id="97442-103">Remove servers and disable protection</span></span>

<span data-ttu-id="97442-104">вносит свой вклад Hello службы Azure Site Recovery, tooyour бесперебойной работе и стратегии аварийного восстановления (BCDR).</span><span class="sxs-lookup"><span data-stu-id="97442-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="97442-105">управляет служба Hello, репликации, отработки отказа и восстановления виртуальных машин и физических серверов.</span><span class="sxs-lookup"><span data-stu-id="97442-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="97442-106">Машины могут быть реплицированной tooAzure или tooa получателя на локальном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="97442-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="97442-107">Краткий обзор см. в статье [Что такое Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="97442-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="97442-108">Эта статья описывает, как серверы toounregister из служб восстановления хранилище в hello портал Azure, и как toodisable защиту для машин защищена службой восстановления сайтов.</span><span class="sxs-lookup"><span data-stu-id="97442-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="97442-109">Отправьте все комментарии или вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="97442-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="97442-110">Отмена регистрации подключенного сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="97442-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="97442-111">Если выполняется репликация виртуальных машин VMware или tooAzure физических серверов Windows и Linux, подключенных конфигурации сервера в хранилище можно отменить регистрацию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97442-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="97442-112">Отключите защиту виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97442-112">Disable machine protection.</span></span> <span data-ttu-id="97442-113">В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97442-114">Отмените связь для всех политик.</span><span class="sxs-lookup"><span data-stu-id="97442-114">Disassociate any policies.</span></span> <span data-ttu-id="97442-115">В **инфраструктура Site Recovery** > **для VMWare и физических машин** > **политики репликации**, дважды щелкните hello связанные политики.</span><span class="sxs-lookup"><span data-stu-id="97442-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97442-116">Щелкните правой кнопкой мыши сервер конфигурации hello > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="97442-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="97442-117">Удалите дополнительные локальные процессы или главные целевые серверы.</span><span class="sxs-lookup"><span data-stu-id="97442-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="97442-118">В **инфраструктура Site Recovery** > **для VMWare и физических машин** > **серверы конфигурации**, щелкните правой кнопкой мыши сервер hello > **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="97442-119">Удалите сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="97442-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="97442-120">Вручную удалить hello Mobility service на главном целевом сервере hello (это будет либо отдельный сервер или на сервере конфигурации hello).</span><span class="sxs-lookup"><span data-stu-id="97442-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="97442-121">Удалите все дополнительные серверы обработки.</span><span class="sxs-lookup"><span data-stu-id="97442-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="97442-122">Удалите сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="97442-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="97442-123">На сервере конфигурации hello удаления hello экземпляра MySQL, установленной с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="97442-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="97442-124">В реестре hello сервера конфигурации hello удалить ключ hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="97442-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="97442-125">Отмена регистрации неподключенного сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="97442-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="97442-126">Если выполняется репликация виртуальных машин VMware или tooAzure физических серверов Windows и Linux, изолированной конфигурации сервера в хранилище можно отменить регистрацию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97442-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="97442-127">Отключите защиту виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97442-127">Disable machine protection.</span></span> <span data-ttu-id="97442-128">В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="97442-129">Выберите **прекратить управление машиной hello**.</span><span class="sxs-lookup"><span data-stu-id="97442-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="97442-130">Удалите дополнительные локальные процессы или главные целевые серверы.</span><span class="sxs-lookup"><span data-stu-id="97442-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="97442-131">В **инфраструктура Site Recovery** > **для VMWare и физических машин** > **серверы конфигурации**, щелкните правой кнопкой мыши сервер hello > **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="97442-132">Удалите сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="97442-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="97442-133">Вручную удалить hello Mobility service на главном целевом сервере hello (это будет либо отдельный сервер или на сервере конфигурации hello).</span><span class="sxs-lookup"><span data-stu-id="97442-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="97442-134">Удалите все дополнительные серверы обработки.</span><span class="sxs-lookup"><span data-stu-id="97442-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="97442-135">Удалите сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="97442-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="97442-136">На сервере конфигурации hello удаления hello экземпляра MySQL, установленной с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="97442-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="97442-137">В реестре hello сервера конфигурации hello удалить ключ hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="97442-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="97442-138">Отмена регистрации подключенного сервера VMM</span><span class="sxs-lookup"><span data-stu-id="97442-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="97442-139">По соображениям рекомендуется отменить регистрацию сервера VMM hello при tooAzure соединения.</span><span class="sxs-lookup"><span data-stu-id="97442-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="97442-140">Это гарантирует, что параметры на серверах VMM hello (и на других серверах VMM с облаками парной) будут правильно удалены.</span><span class="sxs-lookup"><span data-stu-id="97442-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="97442-141">Удалять неподключенный сервер рекомендуется только в случае постоянных проблем с соединением.</span><span class="sxs-lookup"><span data-stu-id="97442-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="97442-142">Если сервер VMM hello не подключен, вам потребуется toomanually запуска сценария tooclean параметров.</span><span class="sxs-lookup"><span data-stu-id="97442-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="97442-143">Остановите репликацию виртуальных машин в облаках на сервер VMM требуется tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="97442-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="97442-144">Удалите все сопоставления сетей, используемых облаков на сервер VMM требуется toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="97442-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="97442-145">В **инфраструктура Site Recovery** > **для System Center VMM** > **сетевое сопоставление**, щелкните правой кнопкой мыши сетевое сопоставление hello >  **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="97442-146">Отмена связи политики репликации из облака на сервер VMM требуется tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="97442-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="97442-147">В **инфраструктура Site Recovery** > **для System Center VMM** >  **политики репликации**, дважды щелкните политику связанные hello.</span><span class="sxs-lookup"><span data-stu-id="97442-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97442-148">Щелкните правой кнопкой мыши облака hello > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="97442-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="97442-149">Удалите сервер VMM hello или активного узла VMM.</span><span class="sxs-lookup"><span data-stu-id="97442-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="97442-150">В **инфраструктура Site Recovery** > **для System Center VMM** > **серверов VMM**, щелкните правой кнопкой мыши сервер hello >  **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="97442-151">Удалите hello поставщик вручную на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="97442-152">При наличии кластера удалите его со всех узлов.</span><span class="sxs-lookup"><span data-stu-id="97442-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="97442-153">При реплицировании tooAzure, вручную удалите агент служб восстановления Microsoft hello из узлов Hyper-V в облаках hello удален.</span><span class="sxs-lookup"><span data-stu-id="97442-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="97442-154">Отмена регистрации неподключенного сервера VMM</span><span class="sxs-lookup"><span data-stu-id="97442-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="97442-155">Остановите репликацию виртуальных машин в облаках на сервер VMM требуется tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="97442-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="97442-156">Удалите все сопоставления сетей, используемых облаков на сервере VMM hello, которое следует toodelete.</span><span class="sxs-lookup"><span data-stu-id="97442-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="97442-157">В **инфраструктура Site Recovery** > **для System Center VMM** > **сетевое сопоставление**, щелкните правой кнопкой мыши сетевое сопоставление hello >  **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="97442-158">Обратите внимание, идентификатор hello hello сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="97442-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="97442-159">Отмена связи политики репликации из облака на сервер VMM требуется tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="97442-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="97442-160">В **инфраструктура Site Recovery** > **для System Center VMM** >  **политики репликации**, дважды щелкните политику связанные hello.</span><span class="sxs-lookup"><span data-stu-id="97442-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97442-161">Щелкните правой кнопкой мыши облака hello > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="97442-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="97442-162">Удалите сервер VMM hello или активного узла.</span><span class="sxs-lookup"><span data-stu-id="97442-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="97442-163">В **инфраструктура Site Recovery** > **для System Center VMM** > **серверов VMM**, щелкните правой кнопкой мыши сервер hello >  **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="97442-164">Загрузите и запустите hello [скрипт очистки](http://aka.ms/asr-cleanup-script-vmm) на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="97442-165">Откройте PowerShell с hello **Запуск от имени администратора** параметр политики выполнения hello toochange для области по умолчанию (LocalMachine) hello.</span><span class="sxs-lookup"><span data-stu-id="97442-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="97442-166">В сценарии hello укажите идентификатор hello hello требуется tooremove сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="97442-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="97442-167">сценарий Hello Удаляет регистрацию и связывания с сервера hello облаков.</span><span class="sxs-lookup"><span data-stu-id="97442-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="97442-168">Выполните сценарий очистки hello на других серверах VMM, содержащие облака, связывать с облаками на сервер VMM требуется tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="97442-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="97442-169">Выполните сценарий очистки hello на любые другие пассивных узлах кластера VMM, имеющих приветствия установлен поставщик.</span><span class="sxs-lookup"><span data-stu-id="97442-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="97442-170">Удалите hello поставщик вручную на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="97442-171">При наличии кластера удалите его со всех узлов.</span><span class="sxs-lookup"><span data-stu-id="97442-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="97442-172">Если вы tooAzure репликации можно удалить агент служб восстановления Microsoft hello из узлов Hyper-V в облаках hello удален.</span><span class="sxs-lookup"><span data-stu-id="97442-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="97442-173">Отмена регистрации узла Hyper-V на сайте Hyper-V</span><span class="sxs-lookup"><span data-stu-id="97442-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="97442-174">Узлы Hyper-V, которые не управляются с помощью VMM, расположены на сайте Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="97442-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="97442-175">Удалите узел на сайте Hyper-V следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97442-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="97442-176">Отключите репликацию для виртуальных машин Hyper-V, расположенных в узле hello.</span><span class="sxs-lookup"><span data-stu-id="97442-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="97442-177">Отмена связи политики для узла Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="97442-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="97442-178">В **инфраструктура Site Recovery** > **для узлов Hyper-V** >  **политики репликации**, дважды щелкните политику связанные hello.</span><span class="sxs-lookup"><span data-stu-id="97442-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97442-179">Щелкните правой кнопкой мыши узел hello > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="97442-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="97442-180">Удалите узлы Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="97442-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="97442-181">В **инфраструктура Site Recovery** > **для System Center VMM** > **узлов Hyper-V**, щелкните правой кнопкой мыши сервер hello >  **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="97442-182">Удалите узел hello Hyper-V, после все узлы будут удалены из него.</span><span class="sxs-lookup"><span data-stu-id="97442-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="97442-183">В **инфраструктура Site Recovery** > **для System Center VMM** > **узлов Hyper-V**, щелкните правой кнопкой мыши узел hello >  **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="97442-184">Запустите следующий сценарий на каждом узле Hyper-V, который вы удалили hello.</span><span class="sxs-lookup"><span data-stu-id="97442-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="97442-185">Hello скрипт очищает параметры сервера hello и отменяет его регистрацию в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="97442-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="97442-186">Отключение защиты для виртуальной машины VMware или физического сервера</span><span class="sxs-lookup"><span data-stu-id="97442-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="97442-187">В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97442-188">В разделе **Удалить виртуальную машину** выберите один из следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="97442-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="97442-189">**Отключите защиту для машины hello (рекомендуется)**.</span><span class="sxs-lookup"><span data-stu-id="97442-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="97442-190">Используйте этот параметр toostop, репликация машины hello.</span><span class="sxs-lookup"><span data-stu-id="97442-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="97442-191">Параметры Site Recovery будут очищены автоматически.</span><span class="sxs-lookup"><span data-stu-id="97442-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="97442-192">Вы увидите только этот параметр в hello при следующих обстоятельствах:</span><span class="sxs-lookup"><span data-stu-id="97442-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="97442-193">**Вы изменили размер тома виртуальной Машины hello**— при изменении размера тома hello виртуальной машина переходит в критическое состояние.</span><span class="sxs-lookup"><span data-stu-id="97442-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="97442-194">Выберите этот параметр toodisables защиту, а также сохранения точек восстановления в Azure.</span><span class="sxs-lookup"><span data-stu-id="97442-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="97442-195">Если вы снова включите защиту для машины hello, hello данные для hello изменения размера тома будут переносятся tooAzure.</span><span class="sxs-lookup"><span data-stu-id="97442-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="97442-196">**После недавно выполнения отработки отказа**— после запуска tootest отработки отказа среды, выберите этот параметр toostart, снова защиты локальных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="97442-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="97442-197">Он отключает каждой виртуальной машины, а затем необходимо tooenable защиты для них еще раз.</span><span class="sxs-lookup"><span data-stu-id="97442-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="97442-198">Отключение компьютера hello, этот параметр не влияет на hello реплики виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="97442-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="97442-199">Не удаляйте hello Mobility service из машины hello.</span><span class="sxs-lookup"><span data-stu-id="97442-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="97442-200">**Прекратить управление машиной hello**.</span><span class="sxs-lookup"><span data-stu-id="97442-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="97442-201">Если этот флажок установлен, hello машина будет удалена только из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="97442-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="97442-202">Параметры защиты в локальной машины hello не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="97442-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="97442-203">Параметры tooremove на компьютере hello и tooremove машины hello из hello подписки Azure, требуется задать tooclean hello параметры путем удаления hello Mobility service.</span><span class="sxs-lookup"><span data-stu-id="97442-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="97442-204">Отключение защиты для виртуальной машины Hyper-V в облаке VMM</span><span class="sxs-lookup"><span data-stu-id="97442-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="97442-205">В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97442-206">В разделе **Удалить виртуальную машину** выберите один из следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="97442-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="97442-207">**Отключите защиту для машины hello (рекомендуется)**.</span><span class="sxs-lookup"><span data-stu-id="97442-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="97442-208">Используйте этот параметр toostop, репликация машины hello.</span><span class="sxs-lookup"><span data-stu-id="97442-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="97442-209">Параметры Site Recovery будут очищены автоматически.</span><span class="sxs-lookup"><span data-stu-id="97442-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="97442-210">**Прекратить управление машиной hello**.</span><span class="sxs-lookup"><span data-stu-id="97442-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="97442-211">Если этот флажок установлен, hello машина будет удалена только из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="97442-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="97442-212">Параметры защиты в локальной машины hello не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="97442-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="97442-213">Параметры tooremove на компьютере hello и tooremove машины hello из hello подписки Azure, требуется tooclean hello параметры копирования вручную, hello приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="97442-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="97442-214">Обратите внимание, что если выбрать toodelete hello виртуальной машины и ее жестких дисков, они будут удалены из hello целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="97442-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="97442-215">Очистить параметры защиты — вторичный сайт VMM репликации tooa</span><span class="sxs-lookup"><span data-stu-id="97442-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="97442-216">Если вы выбрали **прекратить управление машиной hello** и репликация tooa вторичного сайта, выполнения этого скрипта в tooclean сервера-источника hello hello параметров hello основной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97442-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="97442-217">В консоли VMM hello щелкните консоль VMM PowerShell hello tooopen кнопку hello PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97442-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="97442-218">Замените SQLVM1 hello имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97442-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="97442-219">На вторичном сервере VMM hello выполните этот сценарий tooclean параметров hello hello дополнительная виртуальная машина:</span><span class="sxs-lookup"><span data-stu-id="97442-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="97442-220">На вторичном сервере VMM hello обновите hello виртуальных машин на сервере узла Hyper-V hello, позволяя hello вторичная виртуальная машина получает обнаружил попытку в консоли VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="97442-221">Hello выше шаги очистить hello параметры репликации на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="97442-222">Если требуется toostop репликации для виртуальной машины hello, запустите следующий сценарий ах hello hello первичных и вторичных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="97442-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="97442-223">Замените SQLVM1 hello имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97442-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="97442-224">Очистить параметры защиты - tooAzure репликации</span><span class="sxs-lookup"><span data-stu-id="97442-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="97442-225">Если вы выбрали **прекратить управление машиной hello** и реплицировать tooAzure, запустите этот скрипт на hello исходном сервере VMM, с помощью PowerShell из консоли VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="97442-226">Hello выше шаги снимите hello параметры репликации на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="97442-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="97442-227">репликация toostop для hello виртуальная машина, работающая на сервере узла Hyper-V hello, запустите этот скрипт.</span><span class="sxs-lookup"><span data-stu-id="97442-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="97442-228">Замените SQLVM1 hello имя виртуальной машины и host01.contoso.com с именем hello hello сервера узла Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="97442-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="97442-229">Отключение защиты для виртуальной машины Hyper-V на сайте Hyper-V</span><span class="sxs-lookup"><span data-stu-id="97442-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="97442-230">Эта процедура используется в том случае, если выполняется репликация виртуальных машин Hyper-V tooAzure без сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="97442-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="97442-231">В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.</span><span class="sxs-lookup"><span data-stu-id="97442-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97442-232">В **удалить машины**, можно выбрать hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="97442-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="97442-233">**Отключите защиту для машины hello (рекомендуется)**.</span><span class="sxs-lookup"><span data-stu-id="97442-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="97442-234">Используйте этот параметр toostop, репликация машины hello.</span><span class="sxs-lookup"><span data-stu-id="97442-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="97442-235">Параметры Site Recovery будут очищены автоматически.</span><span class="sxs-lookup"><span data-stu-id="97442-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="97442-236">**Прекратить управление машиной hello**.</span><span class="sxs-lookup"><span data-stu-id="97442-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="97442-237">Если выбран этот параметр hello машина будет удалена только из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="97442-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="97442-238">Параметры защиты в локальной машины hello не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="97442-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="97442-239">Параметры tooremove на компьютере hello и tooremove hello виртуальную машину из hello подписки Azure, требуется tooclean hello параметры копирования вручную.</span><span class="sxs-lookup"><span data-stu-id="97442-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="97442-240">При выборе toodelete hello виртуальной машины и ее жестких дисков, они будут удалены из целевого расположения hello.</span><span class="sxs-lookup"><span data-stu-id="97442-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="97442-241">Если вы выбрали **прекратить управление машиной hello**, запустите этот сценарий на сервере узла Hyper-V источника hello, tooremove репликации для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="97442-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="97442-242">Замените SQLVM1 hello имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="97442-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
