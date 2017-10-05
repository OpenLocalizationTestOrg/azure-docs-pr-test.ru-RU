---
title: "Создание шаблонов с помощью расширений виртуальной машины Windows | Документация Майкрософт"
description: "Узнайте о разработке шаблонов Azure Resource Manager с расширениями для виртуальных машин Windows."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 338668df33783d8ef62c6710f4d96ce805296fe5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="c1276-103">Authoring Azure Resource Manager templates with Windows VM extensions</span><span class="sxs-lookup"><span data-stu-id="c1276-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="c1276-104">Выполните следующий командлет в Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c1276-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="c1276-105">Данный командлет возвращает имя издателя, имя расширения и версию в следующем виде.</span><span class="sxs-lookup"><span data-stu-id="c1276-105">This cmdlet returns the publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="c1276-106">Эти три свойства сопоставляются со значениями publisher, type и typeHandlerVersion в приведенном выше фрагменте шаблона.</span><span class="sxs-lookup"><span data-stu-id="c1276-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="c1276-107">Рекомендуется всегда использовать самую последнюю версию расширения для обеспечения максимальной функциональности.</span><span class="sxs-lookup"><span data-stu-id="c1276-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="c1276-108">Определение схемы для параметров конфигурации расширения</span><span class="sxs-lookup"><span data-stu-id="c1276-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="c1276-109">Следующий шаг при создании шаблона расширения заключается в определении формата для предоставления параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c1276-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="c1276-110">Каждое расширение поддерживает собственный набор параметров.</span><span class="sxs-lookup"><span data-stu-id="c1276-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="c1276-111">Чтобы ознакомиться с примером конфигурации для расширений Windows, см. [примеры расширений Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1276-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c1276-112">Ознакомьтесь со следующими разделами, чтобы получить полноценный шаблон с расширениями виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c1276-112">Please refer to the following to get a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="c1276-113">Расширение Custom Script на виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="c1276-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="c1276-114">После разработки шаблон можно развернуть с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1276-114">After authoring the template, you can deploy it using Azure PowerShell.</span></span>

