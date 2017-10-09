---
title: "шаблоны aaaDevelop для стека Azure | Документы Microsoft"
description: "Ознакомьтесь с рекомендациями по использованию шаблона Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="d4721-103">Рекомендации по использованию шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d4721-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="d4721-104">При разработке приложения, он является переносимость шаблона важные tooensure между Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d4721-104">As you develop your application, it is important tooensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="d4721-105">Этот раздел содержит рекомендации по разработке диспетчера ресурсов Azure [шаблоны](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), поэтому можно прототип приложения и тестов развертывания в Azure без среды стека Azure tooan доступа.</span><span class="sxs-lookup"><span data-stu-id="d4721-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access tooan Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="d4721-106">Общедоступные пространства имен</span><span class="sxs-lookup"><span data-stu-id="d4721-106">Public namespaces</span></span>
<span data-ttu-id="d4721-107">Поскольку стек Azure размещается в центре обработки данных, она имеет другую службу пространств имен конечных точек, чем hello общедоступное облако Azure.</span><span class="sxs-lookup"><span data-stu-id="d4721-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than hello Azure public cloud.</span></span> <span data-ttu-id="d4721-108">В результате жестко закодировано общедоступные конечные точки в шаблоны диспетчера ресурсов ошибкой при попытке toodeploy их tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="d4721-108">As a result, hardcoded public endpoints in Resource Manager templates fail when you try toodeploy them tooAzure Stack.</span></span> <span data-ttu-id="d4721-109">Вместо этого можно использовать hello *ссылки* и *объединение* toodynamically функция сборки hello конечной точки службы в зависимости от значения, полученные от поставщика ресурсов hello во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="d4721-109">Instead, you can use hello *reference* and *concatenate* function toodynamically build hello service endpoint based on values retrieved from hello resource provider during deployment.</span></span> <span data-ttu-id="d4721-110">Например, вместо того чтобы задавать *blob.core.windows.net* в шаблоне, получить hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically задать hello *osDisk.URI* Конечная точка:</span><span class="sxs-lookup"><span data-stu-id="d4721-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically set hello *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="d4721-111">Управление версиями API</span><span class="sxs-lookup"><span data-stu-id="d4721-111">API versioning</span></span>
<span data-ttu-id="d4721-112">В Azure и Azure Stack могут быть разные версии служб Azure.</span><span class="sxs-lookup"><span data-stu-id="d4721-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="d4721-113">Каждый ресурс требует hello apiVersion атрибут, определяющий возможности hello.</span><span class="sxs-lookup"><span data-stu-id="d4721-113">Each resource requires hello apiVersion attribute, which defines hello capabilities offered.</span></span> <span data-ttu-id="d4721-114">совместимость версий tooensure API в Azure стек, выполнив hello приведены допустимые версии API для каждого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4721-114">tooensure API version compatibility in Azure Stack, hello following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="d4721-115">Поставщик ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4721-115">Resource Provider</span></span> | <span data-ttu-id="d4721-116">версия_API</span><span class="sxs-lookup"><span data-stu-id="d4721-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="d4721-117">Среда выполнения приложений</span><span class="sxs-lookup"><span data-stu-id="d4721-117">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="d4721-118">Сеть</span><span class="sxs-lookup"><span data-stu-id="d4721-118">Network</span></span> |<span data-ttu-id="d4721-119">`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="d4721-119">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="d4721-120">Хранилище</span><span class="sxs-lookup"><span data-stu-id="d4721-120">Storage</span></span> |<span data-ttu-id="d4721-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="d4721-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="d4721-122">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="d4721-122">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="d4721-123">Служба приложений</span><span class="sxs-lookup"><span data-stu-id="d4721-123">App Service</span></span> |`'2015-08-01'` |
| <span data-ttu-id="d4721-124">MySQL</span><span class="sxs-lookup"><span data-stu-id="d4721-124">MySQL</span></span> |`'2015-09-01'` |
| <span data-ttu-id="d4721-125">SQL</span><span class="sxs-lookup"><span data-stu-id="d4721-125">SQL</span></span> |`'2014-04-01-preview'` |

## <a name="template-functions"></a><span data-ttu-id="d4721-126">Функции шаблонов</span><span class="sxs-lookup"><span data-stu-id="d4721-126">Template functions</span></span>
<span data-ttu-id="d4721-127">Диспетчер ресурсов [функции](../azure-resource-manager/resource-group-template-functions.md) предоставляют необходимые toobuild возможности динамических шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d4721-127">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required toobuild dynamic templates.</span></span> <span data-ttu-id="d4721-128">Например, можно использовать функции для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="d4721-128">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="d4721-129">Объединение или обрезание строк.</span><span class="sxs-lookup"><span data-stu-id="d4721-129">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="d4721-130">Создание ссылок на значения других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4721-130">Reference values from other resources</span></span>
* <span data-ttu-id="d4721-131">Итерации по toodeploy ресурсы нескольких экземпляров</span><span class="sxs-lookup"><span data-stu-id="d4721-131">Iterating on resources toodeploy multiple instances</span></span> 

<span data-ttu-id="d4721-132">При создании шаблонов, некоторые функции недоступны в пакете средств разработки Azure стека и не должны использоваться.</span><span class="sxs-lookup"><span data-stu-id="d4721-132">As you build your templates, some functions are not available in Azure Stack Development Kit, and should not be used.</span></span> <span data-ttu-id="d4721-133">Это следующие функции:</span><span class="sxs-lookup"><span data-stu-id="d4721-133">These functions are:</span></span>

* <span data-ttu-id="d4721-134">Skip</span><span class="sxs-lookup"><span data-stu-id="d4721-134">Skip</span></span>
* <span data-ttu-id="d4721-135">Take</span><span class="sxs-lookup"><span data-stu-id="d4721-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="d4721-136">Расположение ресурса</span><span class="sxs-lookup"><span data-stu-id="d4721-136">Resource location</span></span>
<span data-ttu-id="d4721-137">Шаблоны диспетчера ресурсов использовать расположение атрибута tooplace ресурсы во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="d4721-137">Resource Manager templates use a location attribute tooplace resources during deployment.</span></span> <span data-ttu-id="d4721-138">В Azure расположения ссылаться области tooa как Запад США или Южной Америке.</span><span class="sxs-lookup"><span data-stu-id="d4721-138">In Azure, locations refer tooa region like West US or South America.</span></span> <span data-ttu-id="d4721-139">В Azure Stack используются другие расположения, так как Azure Stack находится в вашем центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d4721-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="d4721-140">шаблоны tooensure переносимые между Azure и Azure стека, должно указывать расположение группы ресурсов hello при развертывании отдельных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4721-140">tooensure templates are transferrable between Azure and Azure Stack, you should reference hello resource group location as you deploy individual resources.</span></span> <span data-ttu-id="d4721-141">Это можно сделать с помощью `[resourceGroup().Location]` tooensure наследуют все ресурсы hello расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4721-141">You can do this using `[resourceGroup().Location]` tooensure all resources inherit hello resource group location.</span></span>  <span data-ttu-id="d4721-142">Hello следующий фрагмент шаблона диспетчера ресурсов приведен пример использования этой функции при развертывании учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d4721-142">hello following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a><span data-ttu-id="d4721-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4721-143">Next steps</span></span>
* [<span data-ttu-id="d4721-144">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4721-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="d4721-145">Развертывание шаблонов с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d4721-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="d4721-146">Развертывание шаблонов с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4721-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

