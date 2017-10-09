---
title: "aaaDelete хранилище Site Recovery"
description: "Узнайте, как toodelete хранилище Azure Site Recovery на основе сценария hello Site Recovery."
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="a3ad3-103">Удаление хранилища Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a3ad3-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="a3ad3-104">Зависимости не позволяют удалить хранилище Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="a3ad3-105">Hello действиях, необходимых tootake различаются в зависимости от сценария hello Site Recovery: VMware tooAzure tooAzure Hyper-V (с и без System Center Virtual Machine Manager) и службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="a3ad3-106">в разделе toodelete хранилища, используемого для резервного копирования Azure, [удалить резервное хранилище в Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="a3ad3-107">Если вы тестируете hello продукта и не беспокоиться о потере данных, используйте hello принудительно удалить метод toorapidly удалить хранилище hello и все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="a3ad3-108">Hello команду PowerShell удаляет все содержимое hello хранилища hello и отменить нельзя.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="a3ad3-109">Использование PowerShell tooforce удалить хранилище hello</span><span class="sxs-lookup"><span data-stu-id="a3ad3-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="a3ad3-110">hello toodelete хранилище Site Recovery, даже если есть защищенные элементы, с помощью этих команд:</span><span class="sxs-lookup"><span data-stu-id="a3ad3-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="a3ad3-111">Удаление хранилища Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a3ad3-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="a3ad3-112">хранилище toodelete hello, hello выполните рекомендуемые действия для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="a3ad3-113">TooAzure виртуальных машин VMware</span><span class="sxs-lookup"><span data-stu-id="a3ad3-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="a3ad3-114">Удалите все защищенные виртуальные машины, следуя указаниям hello [отключите защиту для VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="a3ad3-115">Удалить все политики репликации с помощью инструкции hello в [удалить политику репликации](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="a3ad3-116">Удалить ссылки на toovCenter по hello следующих шагов в [удалить vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="a3ad3-117">Удалить сервер конфигурации hello, следуя указаниям hello [списать сервер конфигурации](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="a3ad3-118">Удалите хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="a3ad3-119">TooAzure виртуальных машин Hyper-V (с Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="a3ad3-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="a3ad3-120">Удалите все защищенные виртуальные машины, следуя указаниям hello [отключить защиту для виртуальной Машины VMware или физических серверов](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="a3ad3-121">Удалить все политики репликации с помощью инструкции hello в [удалить политику репликации](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="a3ad3-122">DELETE ссылается на tooVirtual диспетчера серверов с помощью инструкции hello в [регистрацию подключенным сервером VMM](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="a3ad3-123">Удалите хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="a3ad3-124">TooAzure виртуальных машин Hyper-V (без Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="a3ad3-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="a3ad3-125">Удалите все защищенные виртуальные машины, следуя указаниям hello [отключить защиту для виртуальной Машины VMware или физических серверов](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="a3ad3-126">Удалить все политики репликации с помощью инструкции hello в [удалить политику репликации](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="a3ad3-127">DELETE ссылается на серверах tooHyper-V с помощью инструкции hello в [регистрацию узла Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="a3ad3-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="a3ad3-128">Удалите узел hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="a3ad3-129">Удалите хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="a3ad3-129">Delete hello vault.</span></span>
