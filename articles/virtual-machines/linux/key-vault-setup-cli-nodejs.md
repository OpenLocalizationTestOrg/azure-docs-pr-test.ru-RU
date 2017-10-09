---
title: "aaaSet копирование хранилища ключей для виртуальных машин Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Как tooset копии хранилища ключей для использования в виртуальной машине Azure Resource Manager с hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Настройка хранилища ключей для виртуальных машин диспетчера ресурсов Azure с hello Azure CLI 1.0
В стеке диспетчера ресурсов Azure hello секреты или сертификаты моделируются в виде ресурсов, которые предоставляются поставщиком ресурсов hello хранилища ключей. toolearn Дополнительные сведения о хранилище ключей Azure, в разделе [что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md) Чтобы использовать с виртуальными машинами Azure Resource Manager toobe хранилище ключей, hello *EnabledForDeployment* свойства хранилища ключей должен быть указан tootrue. Это можно сделать на различных клиентах. В этой статье показано, как tooset копии хранилища ключей для использования с виртуальными машинами Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="use-cli-10-tooset-up-key-vault"></a>Использовать tooset CLI 1.0 копии хранилища ключей
toocreate хранилища ключей с помощью hello командной строки (CLI), в разделе [управление хранилище ключей с помощью CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

1.0 CLI у вас есть хранилища ключей hello toocreate перед назначением hello развертывания политики. Вы можете назначить hello политики с помощью hello следующую команду:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Используйте шаблоны tooset копии хранилища ключей
При использовании шаблона необходимо tooset hello `enabledForDeployment` свойство слишком`true` для hello ресурса хранилища ключей.

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

Сведения о других параметрах, которые можно настроить при создании хранилища ключей с помощью шаблонов, см. в статье [Создание хранилища ключей](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
