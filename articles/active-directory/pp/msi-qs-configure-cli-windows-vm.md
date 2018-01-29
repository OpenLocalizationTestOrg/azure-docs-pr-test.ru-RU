---
title: "Настройка назначаемого пользователем MSI для виртуальной машины Azure с помощью Azure CLI"
description: "Пошаговые инструкции по настройке назначаемого пользователем управляемого удостоверения службы (MSI) на виртуальной машине Azure с помощью Azure CLI."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/22/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 4b6f4e2b0e42724276448fd4726c8326de8ea6ee
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2018
---
# <a name="configure-a-user-assigned-managed-service-identity-msi-for-a-vm-using-azure-cli"></a>Настройка назначаемого пользователем управляемого удостоверения службы (MSI) для виртуальной машины с помощью Azure CLI

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Управляемое удостоверение службы предоставляет службы Azure с управляемыми удостоверениями в Azure Active Directory. Это удостоверение можно использовать для аутентификации в службах, которые поддерживают аутентификацию Azure AD, без учетных данных в коде. 

Из этой статьи вы узнаете, как включить и удалить назначаемое пользователем MSI для виртуальных машин Azure с помощью Azure CLI.

## <a name="prerequisites"></a>Необходимые компоненты

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

Запустить примеры сценариев CLI в этом руководстве можно двумя способами:

- Использовать [Azure Cloud Shell](~/articles/cloud-shell/overview.md) на портале Azure или с помощью кнопки "Попробовать", расположенной в правом верхнем углу каждого блока кода.
- [Установить последнюю версию интерфейса командной строки (CLI) 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.23 или более позднюю версию), если вы предпочитаете использовать локальную консоль CLI. Затем войдите в Azure с помощью команды [az login](/cli/azure/#login). Используйте учетную запись, которая связана с подпиской Azure, с помощью которой нужно развернуть назначаемое пользователем MSI и виртуальную машину:

   ```azurecli
   az login
   ```

## <a name="enable-msi-during-creation-of-an-azure-vm"></a>Включение MSI во время создания виртуальной машины Azure

В этом разделе описывается создание виртуальной машины и присвоение ей назначаемого пользователем MSI. Если у вас уже есть виртуальная машина, которую можно использовать, пропустите этот раздел и перейдите к следующему.

1. Если вы уже создали группу ресурсов, которую можно использовать, этот шаг можно пропустить. Создайте [группу ресурсов](~/articles/azure-resource-manager/resource-group-overview.md#terminology) для хранения и развертывания MSI, используя команду [az group create](/cli/azure/group/#create). Не забудьте заменить значения параметров `<RESOURCE GROUP>` и `<LOCATION>` собственными. :

   ```azurecli-interactive 
   az group create --name <RESOURCE GROUP> --location <LOCATION>
   ```

2. Создайте назначаемое пользователем MSI с помощью команды [az identity create](/cli/azure/identity#az_identity_create).  Параметр `-g` указывает группу ресурсов, в которой создается MSI, а параметр `-n` указывает его имя. Не забудьте заменить значения параметров `<RESOURCE GROUP>` и `<MSI NAME>` собственными:

    ```azurecli-interactive
    az identity create -g <RESOURCE GROUP> -n <MSI NAME>
    ```
Ответ содержит подробные сведения о созданном назначаемом пользователем MSI, подобные следующему. Значение ресурса `id`, назначенное MSI, используется на следующем шаге.

   ```json
   {
        "clientId": "73444643-8088-4d70-9532-c3a0fdc190fz",
        "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<MSI NAME>/credentials?tid=5678&oid=9012&aid=73444643-8088-4d70-9532-c3a0fdc190fz",
        "id": "/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<MSI NAME>",
        "location": "westcentralus",
        "name": "<MSI NAME>",
        "principalId": "e5fdfdc1-ed84-4d48-8551-fe9fb9dedfll",
        "resourceGroup": "<RESOURCE GROUP>",
        "tags": {},
        "tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533bl",
        "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
   }
   ```

3. Создайте виртуальную машину, выполнив команду [az vm create](/cli/azure/vm/#create). В следующем примере создается виртуальная машина, связанная с новым назначаемым пользователем MSI, в соответствии с параметром `--assign-identity`. Обязательно замените свойства `<RESOURCE GROUP>`, `<VM NAME>`, `<USER NAME>`, `<PASSWORD>` и `<`MSI ID>` parameter values with your own values. For `<MSI ID>`, use the user-assigned MSI's resource `id`, созданные на предыдущем шаге: 

   ```azurecli-interactive 
   az vm create --resource-group <RESOURCE GROUP> --name <VM NAME> --image UbuntuLTS --admin-username <USER NAME> --admin-password <PASSWORD> --assign-identity <MSI ID>
   ```

## <a name="enable-msi-on-an-existing-azure-vm"></a>Включение MSI на имеющейся виртуальной машине Azure

1. Создайте назначаемое пользователем MSI с помощью команды [az identity create](/cli/azure/identity#az_identity_create).  Параметр `-g` указывает группу ресурсов, в которой создается MSI, а параметр `-n` указывает его имя. Не забудьте заменить значения параметров `<RESOURCE GROUP>` и `<MSI NAME>` собственными:

    ```azurecli-interactive
    az identity create -g <RESOURCE GROUP> -n <MSI NAME>
    ```
Ответ содержит подробные сведения о созданном назначаемом пользователем MSI, подобные следующему. Значение ресурса `id`, назначенное MSI, используется на следующем шаге.

   ```json
   {
        "clientId": "73444643-8088-4d70-9532-c3a0fdc190fz",
        "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<MSI NAME>/credentials?tid=5678&oid=9012&aid=73444643-8088-4d70-9532-c3a0fdc190fz",
        "id": "/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<MSI NAME>",
        "location": "westcentralus",
        "name": "<MSI NAME>",
        "principalId": "e5fdfdc1-ed84-4d48-8551-fe9fb9dedfll",
        "resourceGroup": "<RESOURCE GROUP>",
        "tags": {},
        "tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533bl",
        "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
   }
   ```

2. Назначьте удостоверение MSI, назначаемое пользователем, виртуальной машине с помощью команды [az vm assign-identity](/cli/azure/vm#az_vm_assign_identity). Не забудьте заменить значения параметров `<RESOURCE GROUP>` и `<VM NAME>` собственными. `<MSI ID>` будет свойством ресурса `id` назначаемого пользователем MSI, созданным на предыдущем шаге:

    ```azurecli-interactive
    az vm assign-identity -g <RESOURCE GROUP> -n <VM NAME> --identities <MSI ID>
    ```

## <a name="remove-msi-from-an-azure-vm"></a>Удаление MSI с виртуальной машины Azure

1. Удалите назначаемое пользователем MSI со своей виртуальной машины, используя команду [az vm remove-identity](/cli/azure/vm#az_vm_remove_identity). Не забудьте заменить значения параметров `<RESOURCE GROUP>` и `<VM NAME>` собственными. `<MSI NAME>` будет свойством `name` назначаемого пользователем MSI, как указано в команде `az identity create` (см. примеры в предыдущих разделах):

   ```azurecli-interactive
   az vm remove-identity -g <RESOURCE GROUP> -n <VM NAME> --identities <MSI NAME>
   ```

## <a name="next-steps"></a>Дополнительная информация

- [Управляемое удостоверение службы (MSI) для Azure Active Directory](msi-overview.md)
- Ниже приведены комплексные краткие руководства по созданию виртуальных машин Azure: 

  - [Создание виртуальной машины Windows с помощью Azure CLI](~/articles/virtual-machines/windows/quick-create-cli.md)  
  - [Создание виртуальной машины Linux с помощью Azure CLI](~/articles/virtual-machines/linux/quick-create-cli.md) 

Оставляйте свои замечания и пожелания в разделе ниже. Они помогают нам улучшать содержимое веб-сайта.
















