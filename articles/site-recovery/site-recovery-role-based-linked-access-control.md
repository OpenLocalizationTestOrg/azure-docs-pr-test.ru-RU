---
title: "Управление доступом на основе ролей aaaUsing toomanage Azure Site Recovery | Документы Microsoft"
description: "В этой статье описывается, как tooapply и использование средств управления (RBAC) toomanage развертываний Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Используйте развертывания Azure Site Recovery toomanage управления доступом на основе ролей

Контроль доступа на основе ролей (RBAC) Azure обеспечивает точное управление доступом для Azure. RBAC можно разделять обязанности в вашу рабочую группу и предоставить специальный доступ toousers разрешения как необходимые tooperform конкретного задания.

Azure Site Recovery предоставляет 3 встроенные роли операций управления toocontrol Site Recovery. Дополнительные сведения см. в статье о [встроенных ролях RBAC в Azure](../active-directory/role-based-access-built-in-roles.md).

* [Сайт восстановления участника](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) — эта роль имеет все операции восстановления сайтов Azure требуется toomanage разрешений в хранилище служб восстановления. Пользователь с этой ролью, тем не менее, нельзя создать или удалить хранилище служб восстановления или назначения tooother пользователи с правами доступа. Эта роль является наилучшим образом подходит для администраторов аварийного восстановления, которые можно настроить и управлять аварийного восстановления для приложений или всей организации, как hello случай может быть.
* [Оператор восстановления сайта](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) — эта роль имеет разрешения tooexecute и manager при сбое и операций. Пользователь с этой ролью нельзя включить или отключить репликацию, создать или удалять хранилища, зарегистрировать новую инфраструктуру или назначения tooother пользователи с правами доступа. Эта роль лучше всего подходит для оператора аварийного восстановления, который может выполнять отработку отказа виртуальных машин или приложений по указанию владельцев приложений и ИТ-администраторов в случае действительной аварии или ее имитации, например отработки аварийного восстановления. После разрешения аварийного hello, оператор hello аварийного восстановления можно повторно защитить и восстановления размещения hello виртуальных машин.
* [Сайт восстановления чтения](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) — эта роль имеет разрешения tooview все операции управления Site Recovery. Эта роль является наилучшим образом подходит для мониторинга администратора ИТ, кто может отслеживать текущее состояние защиты hello и вызывать запросами в службу поддержки, если это необходимо.

Если вам нужна toodefine свои собственные роли для дополнительного управления, см. раздел как слишком[сборки пользовательских ролей](../active-directory/role-based-access-control-custom-roles.md) в Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Разрешения, необходимые для новых виртуальных машин tooEnable репликации
При новой виртуальной машины является реплицированной tooAzure, с помощью Azure Site Recovery, уровни доступа hello связанных пользователей не проверенные tooensure, hello пользователя hello необходимые разрешения toouse hello Azure ресурсов, предоставленных tooSite восстановления.

репликация tooenable для новой виртуальной машины, пользователь должен иметь:
* Разрешение toocreate виртуальной машины в hello выбранной группы ресурсов
* Разрешение toocreate виртуальной машины в выбранной виртуальной сети hello
* Разрешение toowrite toohello выбранную учетную запись хранения

Пользователю требуется hello после репликации toocomplete разрешения новой виртуальной машины.

> [!IMPORTANT]
>Убедитесь, что соответствующие разрешения добавляются в модель развертывания hello (диспетчера ресурсов / классической) для развертывания ресурсов.

| **Тип ресурса** | **Модель развертывания** | **Разрешение** |
| --- | --- | --- |
| Среда выполнения приложений | Диспетчер ресурсов | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Классический | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Сеть | Диспетчер ресурсов | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Классический | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Хранилище | Диспетчер ресурсов | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Классический | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Группа ресурсов | Диспетчер ресурсов | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Рассмотрите возможность использования hello «Участник виртуальной машины» и «Участник классической виртуальной машины» [встроенные роли](../active-directory/role-based-access-built-in-roles.md) для развертывания диспетчера ресурсов и классической модели соответственно.

## <a name="next-steps"></a>Дальнейшие действия
* [Управление доступом на основе ролей](../active-directory/role-based-access-control-configure.md): Приступая к работе с RBAC в hello портал Azure.
* Узнайте, как доступ к toomanage с:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Интерфейс командной строки Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [ИНТЕРФЕЙС REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [Устранение неполадок при управлении доступом на основе ролей](../active-directory/role-based-access-control-troubleshooting.md). Рекомендации по устранению распространенных проблем.
