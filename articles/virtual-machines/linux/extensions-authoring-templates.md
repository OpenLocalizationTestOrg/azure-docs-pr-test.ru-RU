---
title: "Разработка шаблонов с расширениями виртуальной машины Linux | Документация Майкрософт"
description: "Узнайте о разработке шаблонов Azure Resource Manager с расширениями для виртуальных машин Linux."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="27560-103">Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="27560-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="27560-104">В Azure CLI выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="27560-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="27560-105">Эта команда возвращает имя издателя, имя расширения и версию в следующем виде.</span><span class="sxs-lookup"><span data-stu-id="27560-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="27560-106">Эти три свойства сопоставляются со значениями publisher, type и typeHandlerVersion в приведенном выше фрагменте шаблона.</span><span class="sxs-lookup"><span data-stu-id="27560-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="27560-107">Рекомендуется всегда использовать самую последнюю версию расширения для обеспечения максимальной функциональности.</span><span class="sxs-lookup"><span data-stu-id="27560-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="27560-108">Определение схемы для параметров конфигурации расширения</span><span class="sxs-lookup"><span data-stu-id="27560-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="27560-109">Следующий шаг при создании шаблона расширения заключается в определении формата для предоставления параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="27560-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="27560-110">Каждое расширение поддерживает собственный набор параметров.</span><span class="sxs-lookup"><span data-stu-id="27560-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="27560-111">Чтобы ознакомиться с примерами конфигураций для расширений Linux, откройте документацию [с примерами расширений Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27560-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="27560-112">Ознакомьтесь со следующими разделами, чтобы получить полноценный шаблон с расширениями виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27560-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="27560-113">Расширение пользовательских сценариев на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="27560-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="27560-114">После разработки шаблон можно развернуть с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="27560-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

