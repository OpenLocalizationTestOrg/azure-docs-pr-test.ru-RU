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
# <a name="delete-a-site-recovery-vault"></a>Удаление хранилища Site Recovery
Зависимости не позволяют удалить хранилище Azure Site Recovery. Hello действиях, необходимых tootake различаются в зависимости от сценария hello Site Recovery: VMware tooAzure tooAzure Hyper-V (с и без System Center Virtual Machine Manager) и службы архивации Azure. в разделе toodelete хранилища, используемого для резервного копирования Azure, [удалить резервное хранилище в Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Если вы тестируете hello продукта и не беспокоиться о потере данных, используйте hello принудительно удалить метод toorapidly удалить хранилище hello и все его зависимости.

> Hello команду PowerShell удаляет все содержимое hello хранилища hello и отменить нельзя.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Использование PowerShell tooforce удалить хранилище hello 

hello toodelete хранилище Site Recovery, даже если есть защищенные элементы, с помощью этих команд:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Удаление хранилища Site Recovery 
хранилище toodelete hello, hello выполните рекомендуемые действия для вашего сценария.

### <a name="vmware-vms-tooazure"></a>TooAzure виртуальных машин VMware

1. Удалите все защищенные виртуальные машины, следуя указаниям hello [отключите защиту для VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Удалить все политики репликации с помощью инструкции hello в [удалить политику репликации](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Удалить ссылки на toovCenter по hello следующих шагов в [удалить vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Удалить сервер конфигурации hello, следуя указаниям hello [списать сервер конфигурации](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Удалите хранилище hello.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>TooAzure виртуальных машин Hyper-V (с Virtual Machine Manager)
1. Удалите все защищенные виртуальные машины, следуя указаниям hello [отключить защиту для виртуальной Машины VMware или физических серверов](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Удалить все политики репликации с помощью инструкции hello в [удалить политику репликации](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  DELETE ссылается на tooVirtual диспетчера серверов с помощью инструкции hello в [регистрацию подключенным сервером VMM](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Удалите хранилище hello.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>TooAzure виртуальных машин Hyper-V (без Virtual Machine Manager)
1. Удалите все защищенные виртуальные машины, следуя указаниям hello [отключить защиту для виртуальной Машины VMware или физических серверов](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Удалить все политики репликации с помощью инструкции hello в [удалить политику репликации](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. DELETE ссылается на серверах tooHyper-V с помощью инструкции hello в [регистрацию узла Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Удалите узел hello Hyper-V.

5. Удалите хранилище hello.
