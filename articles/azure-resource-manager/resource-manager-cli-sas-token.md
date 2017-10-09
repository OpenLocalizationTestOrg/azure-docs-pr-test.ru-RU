---
title: "шаблон Azure с маркер SAS и Azure CLI aaaDeploy | Документы Microsoft"
description: "Используйте диспетчер ресурсов Azure и Azure CLI tooAzure toodeploy ресурсы из шаблона, который защищен с маркер SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure CLI

Если шаблон находится в учетной записи хранилища, вы можете ограничить доступ toohello шаблон и предоставить маркер подписи общего доступа во время развертывания. В этом разделе объясняется, как toouse Azure PowerShell с помощью шаблонов диспетчера ресурсов tooprovide маркер SAS во время развертывания. 

## <a name="add-private-template-toostorage-account"></a>Добавьте учетную запись toostorage закрытый шаблона

Можно добавить учетную запись хранилища tooa шаблоны и связывать toothem во время развертывания с помощью токена SAS.

> [!IMPORTANT]
> Перечисленные ниже действия hello, hello BLOB-объект, содержащий шаблон hello является владельцем учетной записи доступны tooonly hello. Тем не менее при создании маркера SAS для большого двоичного объекта hello hello большой двоичный объект является доступного tooanyone с URI. Если другой пользователь перехватывает hello URI, этот пользователь — шаблон может tooaccess hello. С помощью маркера SAS является удобным способом ограничения доступа tooyour шаблоны, но не следует включать конфиденциальные данные, такие как пароли непосредственно в шаблоне hello.
> 
> 

Hello следующий пример устанавливает контейнер частного хранилища учетной записи и отправка шаблона:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Предоставление маркера SAS во время развертывания
toodeploy закрытый шаблона в учетную запись хранилища, создать токен SAS и включите его в hello URI для шаблона hello. Задайте tooallow время истечения срока действия hello достаточно времени toocomplete hello развертывания.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Пример использования маркера SAS со связанными шаблонами см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Дальнейшие действия
* Шаблоны toodeploying введение в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](resource-group-template-deploy-cli.md).
* Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-cli-deploy.md).
* toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).
