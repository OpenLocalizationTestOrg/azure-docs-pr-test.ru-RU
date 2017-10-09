---
title: "aaaDeploy шаблон Azure с маркер SAS и PowerShell | Документы Microsoft"
description: "Используйте диспетчер ресурсов Azure и Azure PowerShell tooAzure toodeploy ресурсы из шаблона, который защищен с маркер SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell

Если шаблон находится в учетной записи хранилища, вы можете ограничить доступ toohello шаблон и предоставить маркер подписи общего доступа во время развертывания. В этом разделе объясняется, как toouse Azure PowerShell с помощью шаблонов диспетчера ресурсов tooprovide маркер SAS во время развертывания. 

## <a name="add-private-template-toostorage-account"></a>Добавьте учетную запись toostorage закрытый шаблона

Можно добавить учетную запись хранилища tooa шаблоны и связывать toothem во время развертывания с помощью токена SAS.

> [!IMPORTANT]
> Перечисленные ниже действия hello, hello BLOB-объект, содержащий шаблон hello является владельцем учетной записи доступны tooonly hello. Тем не менее при создании маркера SAS для большого двоичного объекта hello hello большой двоичный объект является доступного tooanyone с URI. Если другой пользователь перехватывает hello URI, этот пользователь — шаблон может tooaccess hello. С помощью маркера SAS является удобным способом ограничения доступа tooyour шаблоны, но не следует включать конфиденциальные данные, такие как пароли непосредственно в шаблоне hello.
> 
> 

Hello следующий пример устанавливает контейнер частного хранилища учетной записи и отправка шаблона:
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>Предоставление маркера SAS во время развертывания
toodeploy закрытый шаблона в учетную запись хранилища, создать токен SAS и включите его в hello URI для шаблона hello. Задайте tooallow время истечения срока действия hello достаточно времени toocomplete hello развертывания.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Пример использования маркера SAS со связанными шаблонами см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).


## <a name="next-steps"></a>Дальнейшие действия
* Шаблоны toodeploying введение в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](resource-group-template-deploy.md).
* Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-powershell-deploy.md).
* toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

