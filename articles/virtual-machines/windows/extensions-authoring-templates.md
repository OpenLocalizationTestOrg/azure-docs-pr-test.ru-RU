---
title: "aaaAuthoring шаблоны с расширениями ВМ Windows | Документы Microsoft"
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
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="08aa8-103">Authoring Azure Resource Manager templates with Windows VM extensions</span><span class="sxs-lookup"><span data-stu-id="08aa8-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="08aa8-104">В Azure PowerShell выполните hello, выполнив командлет Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08aa8-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="08aa8-105">Этот командлет возвращает hello имя издателя, имя и версия модуля следующим образом:</span><span class="sxs-lookup"><span data-stu-id="08aa8-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="08aa8-106">Эти три свойства сопоставляются слишком «издатель», «тип» и «typeHandlerVersion» соответственно в hello выше фрагмента шаблона.</span><span class="sxs-lookup"><span data-stu-id="08aa8-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa8-107">Это всегда рекомендуется toouse hello последнюю версию tooget hello Большинство обновленных функциональных возможностей расширения.</span><span class="sxs-lookup"><span data-stu-id="08aa8-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="08aa8-108">Определение схемы hello для параметров конфигурации модуля hello</span><span class="sxs-lookup"><span data-stu-id="08aa8-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="08aa8-109">следующим шагом Hello разработки шаблоном расширения является формат hello tooidentify для предоставления параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="08aa8-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="08aa8-110">Каждое расширение поддерживает собственный набор параметров.</span><span class="sxs-lookup"><span data-stu-id="08aa8-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="08aa8-111">toolook в образце конфигурации для расширения Windows, в разделе [примеры расширений Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08aa8-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="08aa8-112">После полного выполнения шаблона с расширениями ВМ tooget toohello см.</span><span class="sxs-lookup"><span data-stu-id="08aa8-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="08aa8-113">Расширение Custom Script на виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="08aa8-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="08aa8-114">После создания шаблона hello, можно развернуть с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08aa8-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

