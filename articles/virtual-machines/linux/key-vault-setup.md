---
title: "aaaSet копирование хранилища ключей Azure для виртуальных машин Linux | Документы Microsoft"
description: "Как tooset копии хранилища ключей для использования в виртуальной машине Azure Resource Manager с hello CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Как tooset копию ключа хранилища для виртуальных машин с hello Azure CLI 2.0

В стеке диспетчера ресурсов Azure hello секреты или сертификаты моделируются в виде ресурсов, предоставляемых хранилищем ключей. toolearn Дополнительные сведения о хранилище ключей Azure, в разделе [что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md) Чтобы использовать с виртуальными машинами Azure Resource Manager toobe хранилище ключей, hello *EnabledForDeployment* свойства хранилища ключей должен быть указан tootrue. В этой статье рассказывается, как tooset копии хранилища ключей для использования с виртуальными машинами Azure (ВМ) с помощью hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform эти шаги, необходимые hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

## <a name="create-a-key-vault"></a>создать хранилище ключей;
Создание хранилища ключей и назначение политики развертывания hello с [az keyvault создать](/cli/azure/keyvault#create). Hello следующий пример создает хранилища ключей с именем `myKeyVault` в hello `myResourceGroup` группа ресурсов:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Обновление Key Vault для использования с виртуальными машинами
Задать политику развертывания hello в существующем хранилище ключей с [обновление keyvault az](/cli/azure/keyvault#update). Hello следующие обновления hello хранилища ключей с именем `myKeyVault` в hello `myResourceGroup` группа ресурсов:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Используйте шаблоны tooset копии хранилища ключей
При использовании шаблона необходимо tooset hello `enabledForDeployment` свойство слишком`true` для ресурса хранилища ключей hello следующим образом:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других параметрах, которые можно настроить при создании Key Vault с помощью шаблонов, см. в разделе [Create a Key Vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/) (Создание Key Vault).
