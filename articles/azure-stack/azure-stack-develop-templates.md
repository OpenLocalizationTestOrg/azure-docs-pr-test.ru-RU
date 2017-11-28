---
title: "Разработка шаблонов для Azure Stack | Документация Майкрософт"
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
ms.openlocfilehash: a8468616f924aebb91447b379cea3f926c39de48
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="6f2bb-103">Рекомендации по использованию шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f2bb-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="6f2bb-104">При разработке приложения очень важно обеспечить мобильность шаблона в контексте взаимодействия Azure и Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-104">As you develop your application, it is important to ensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="6f2bb-105">Эта статья содержит рекомендации по разработке [шаблонов](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) Azure Resource Manager. С ее помощью вы сможете создать прототип приложения и протестировать развертывание в Azure без доступа к среде Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access to an Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="6f2bb-106">Общедоступные пространства имен</span><span class="sxs-lookup"><span data-stu-id="6f2bb-106">Public namespaces</span></span>
<span data-ttu-id="6f2bb-107">Так как среда Azure Stack размещена в центре обработки данных, она использует собственные пространства имен конечных точек службы, а не пространства общедоступного облака Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than the Azure public cloud.</span></span> <span data-ttu-id="6f2bb-108">В результате жестко закодировано общедоступные конечные точки в шаблоны диспетчера ресурсов ошибкой при попытке развернуть их на стек Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-108">As a result, hardcoded public endpoints in Resource Manager templates fail when you try to deploy them to Azure Stack.</span></span> <span data-ttu-id="6f2bb-109">Вместо этого можно использовать функцию *создания ссылки* и *объединения*, чтобы динамически создать конечную точку службы на основе значений, полученных от поставщика ресурсов во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-109">Instead, you can use the *reference* and *concatenate* function to dynamically build the service endpoint based on values retrieved from the resource provider during deployment.</span></span> <span data-ttu-id="6f2bb-110">Например, чтобы не указывать *blob.core.windows.net* в шаблоне, получите [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) для динамической настройки конечной точки *osDisk.URI*.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve the [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) to dynamically set the *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="6f2bb-111">Управление версиями API</span><span class="sxs-lookup"><span data-stu-id="6f2bb-111">API versioning</span></span>
<span data-ttu-id="6f2bb-112">В Azure и Azure Stack могут быть разные версии служб Azure.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="6f2bb-113">Для каждого ресурса требуется атрибут apiVersion, который определяет доступные возможности.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-113">Each resource requires the apiVersion attribute, which defines the capabilities offered.</span></span> <span data-ttu-id="6f2bb-114">Чтобы обеспечить совместимость версий API в стек Azure, ниже приведены допустимые версии API для каждого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-114">To ensure API version compatibility in Azure Stack, the following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="6f2bb-115">Поставщик ресурсов</span><span class="sxs-lookup"><span data-stu-id="6f2bb-115">Resource Provider</span></span> | <span data-ttu-id="6f2bb-116">версия_API</span><span class="sxs-lookup"><span data-stu-id="6f2bb-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="6f2bb-117">Среда выполнения приложений</span><span class="sxs-lookup"><span data-stu-id="6f2bb-117">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="6f2bb-118">Сеть</span><span class="sxs-lookup"><span data-stu-id="6f2bb-118">Network</span></span> |<span data-ttu-id="6f2bb-119">`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="6f2bb-119">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="6f2bb-120">Хранилище</span><span class="sxs-lookup"><span data-stu-id="6f2bb-120">Storage</span></span> |<span data-ttu-id="6f2bb-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="6f2bb-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="6f2bb-122">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="6f2bb-122">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="6f2bb-123">Служба приложений</span><span class="sxs-lookup"><span data-stu-id="6f2bb-123">App Service</span></span> |`'2015-08-01'` |
| <span data-ttu-id="6f2bb-124">MySQL</span><span class="sxs-lookup"><span data-stu-id="6f2bb-124">MySQL</span></span> |`'2015-09-01'` |
| <span data-ttu-id="6f2bb-125">SQL</span><span class="sxs-lookup"><span data-stu-id="6f2bb-125">SQL</span></span> |`'2014-04-01-preview'` |

## <a name="template-functions"></a><span data-ttu-id="6f2bb-126">Функции шаблонов</span><span class="sxs-lookup"><span data-stu-id="6f2bb-126">Template functions</span></span>
<span data-ttu-id="6f2bb-127">[Функции](../azure-resource-manager/resource-group-template-functions.md) Resource Manager позволяют создавать динамические шаблоны.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-127">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required to build dynamic templates.</span></span> <span data-ttu-id="6f2bb-128">Например, можно использовать функции для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-128">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="6f2bb-129">Объединение или обрезание строк.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-129">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="6f2bb-130">Создание ссылок на значения других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-130">Reference values from other resources</span></span>
* <span data-ttu-id="6f2bb-131">Итерация по ресурсам для развертывания нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-131">Iterating on resources to deploy multiple instances</span></span> 

<span data-ttu-id="6f2bb-132">При создании шаблонов, некоторые функции недоступны в пакете средств разработки Azure стека и не должны использоваться.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-132">As you build your templates, some functions are not available in Azure Stack Development Kit, and should not be used.</span></span> <span data-ttu-id="6f2bb-133">Это следующие функции:</span><span class="sxs-lookup"><span data-stu-id="6f2bb-133">These functions are:</span></span>

* <span data-ttu-id="6f2bb-134">Skip</span><span class="sxs-lookup"><span data-stu-id="6f2bb-134">Skip</span></span>
* <span data-ttu-id="6f2bb-135">Take</span><span class="sxs-lookup"><span data-stu-id="6f2bb-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="6f2bb-136">Расположение ресурса</span><span class="sxs-lookup"><span data-stu-id="6f2bb-136">Resource location</span></span>
<span data-ttu-id="6f2bb-137">Шаблоны Resource Manager используют атрибут расположения для размещения ресурсов во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-137">Resource Manager templates use a location attribute to place resources during deployment.</span></span> <span data-ttu-id="6f2bb-138">В Azure расположения называются регионами, например "западная часть США"или "Южная Америка".</span><span class="sxs-lookup"><span data-stu-id="6f2bb-138">In Azure, locations refer to a region like West US or South America.</span></span> <span data-ttu-id="6f2bb-139">В Azure Stack используются другие расположения, так как Azure Stack находится в вашем центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="6f2bb-140">Чтобы шаблоны можно было передавать между Azure и Azure Stack, необходимо указать расположение группы ресурсов при развертывании отдельных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-140">To ensure templates are transferrable between Azure and Azure Stack, you should reference the resource group location as you deploy individual resources.</span></span> <span data-ttu-id="6f2bb-141">Это можно сделать с помощью `[resourceGroup().Location]` для обеспечения всех ресурсов наследуют расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-141">You can do this using `[resourceGroup().Location]` to ensure all resources inherit the resource group location.</span></span>  <span data-ttu-id="6f2bb-142">В следующем фрагменте кода шаблона Resource Manager приведен пример использования этой функции при развертывании учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6f2bb-142">The following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used to store the VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a><span data-ttu-id="6f2bb-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f2bb-143">Next steps</span></span>
* [<span data-ttu-id="6f2bb-144">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f2bb-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="6f2bb-145">Развертывание шаблонов с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="6f2bb-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="6f2bb-146">Развертывание шаблонов с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f2bb-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

