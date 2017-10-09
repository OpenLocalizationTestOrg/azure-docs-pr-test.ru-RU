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
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="9da4a-103">Развертывание частного шаблона Resource Manager с использованием токена SAS и Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9da4a-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="9da4a-104">Если шаблон находится в учетной записи хранилища, вы можете ограничить доступ toohello шаблон и предоставить маркер подписи общего доступа во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="9da4a-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="9da4a-105">В этом разделе объясняется, как toouse Azure PowerShell с помощью шаблонов диспетчера ресурсов tooprovide маркер SAS во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="9da4a-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="9da4a-106">Добавьте учетную запись toostorage закрытый шаблона</span><span class="sxs-lookup"><span data-stu-id="9da4a-106">Add private template toostorage account</span></span>

<span data-ttu-id="9da4a-107">Можно добавить учетную запись хранилища tooa шаблоны и связывать toothem во время развертывания с помощью токена SAS.</span><span class="sxs-lookup"><span data-stu-id="9da4a-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9da4a-108">Перечисленные ниже действия hello, hello BLOB-объект, содержащий шаблон hello является владельцем учетной записи доступны tooonly hello.</span><span class="sxs-lookup"><span data-stu-id="9da4a-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="9da4a-109">Тем не менее при создании маркера SAS для большого двоичного объекта hello hello большой двоичный объект является доступного tooanyone с URI.</span><span class="sxs-lookup"><span data-stu-id="9da4a-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="9da4a-110">Если другой пользователь перехватывает hello URI, этот пользователь — шаблон может tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="9da4a-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="9da4a-111">С помощью маркера SAS является удобным способом ограничения доступа tooyour шаблоны, но не следует включать конфиденциальные данные, такие как пароли непосредственно в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="9da4a-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="9da4a-112">Hello следующий пример устанавливает контейнер частного хранилища учетной записи и отправка шаблона:</span><span class="sxs-lookup"><span data-stu-id="9da4a-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="9da4a-113">Предоставление маркера SAS во время развертывания</span><span class="sxs-lookup"><span data-stu-id="9da4a-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="9da4a-114">toodeploy закрытый шаблона в учетную запись хранилища, создать токен SAS и включите его в hello URI для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="9da4a-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="9da4a-115">Задайте tooallow время истечения срока действия hello достаточно времени toocomplete hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="9da4a-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="9da4a-116">Пример использования маркера SAS со связанными шаблонами см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9da4a-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9da4a-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9da4a-117">Next steps</span></span>
* <span data-ttu-id="9da4a-118">Шаблоны toodeploying введение в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9da4a-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="9da4a-119">Полный пример сценария, развертывающего шаблон, см. в статье [Сценарий для развертывания шаблона Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9da4a-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="9da4a-120">toodefine параметры в шаблоне, в разделе [разработки шаблонов](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="9da4a-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="9da4a-121">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9da4a-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

