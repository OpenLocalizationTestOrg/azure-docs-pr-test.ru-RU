---
title: "aaaSet копию ключа хранилища для виртуальных машин Windows в диспетчере ресурсов Azure | Документы Microsoft"
description: "Как tooset копии хранилища ключей для использования в виртуальной машине Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Настройка хранилища ключей для виртуальных машин в Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

В стеке диспетчера ресурсов Azure секреты или сертификаты моделируются в виде ресурсов, которые предоставляются поставщиком ресурсов hello хранилища ключей. toolearn Дополнительные сведения о хранилище ключей. в разделе [что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Чтобы использовать с виртуальными машинами Azure Resource Manager toobe хранилище ключей, hello **EnabledForDeployment** свойства хранилища ключей должен быть указан tootrue. Это можно сделать на различных клиентах.
> 2. потребности Hello хранилище ключей toobe, созданного в hello же подписке и расположении как hello виртуальной машины.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Используйте PowerShell tooset копии хранилища ключей
toocreate хранилища ключей с помощью PowerShell см. в разделе [приступить к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md#vault).

Для новых хранилищ ключей можно использовать этот командлет PowerShell:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Для существующих хранилищ ключей можно использовать этот командлет PowerShell:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Нам CLI tooset копии хранилища ключей
toocreate хранилища ключей с помощью hello командной строки (CLI), в разделе [управление хранилище ключей с помощью CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Для CLI у вас есть хранилища ключей toocreate hello перед назначением hello развертывания политики. Это можно сделать с помощью hello следующую команду:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Используйте шаблоны tooset копии хранилища ключей
При использовании шаблона требуется tooset hello `enabledForDeployment` свойство слишком`true` для hello ресурса хранилища ключей.

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
