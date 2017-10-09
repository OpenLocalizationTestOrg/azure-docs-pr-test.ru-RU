---
title: "шаблоны aaaAuthoring с расширениями виртуальных Машин Linux | Документы Microsoft"
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
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="05ee3-103">Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="05ee3-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="05ee3-104">В Azure CLI выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="05ee3-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="05ee3-105">Это имя издателя hello Возвращает команды, имя и версия модуля следующим образом:</span><span class="sxs-lookup"><span data-stu-id="05ee3-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="05ee3-106">Эти три свойства сопоставляются слишком «издатель», «тип» и «typeHandlerVersion» соответственно в hello выше фрагмента шаблона.</span><span class="sxs-lookup"><span data-stu-id="05ee3-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="05ee3-107">Это всегда рекомендуется toouse hello последнюю версию tooget hello Большинство обновленных функциональных возможностей расширения.</span><span class="sxs-lookup"><span data-stu-id="05ee3-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="05ee3-108">Определение схемы hello для параметров конфигурации модуля hello</span><span class="sxs-lookup"><span data-stu-id="05ee3-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="05ee3-109">следующим шагом Hello разработки шаблоном расширения является формат hello tooidentify для предоставления параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="05ee3-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="05ee3-110">Каждое расширение поддерживает собственный набор параметров.</span><span class="sxs-lookup"><span data-stu-id="05ee3-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="05ee3-111">toolook в образце конфигурации для расширения Linux щелкните hello документации см. в разделе [eExtensions образцы Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05ee3-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="05ee3-112">После полного выполнения шаблона с расширениями ВМ tooget toohello см.</span><span class="sxs-lookup"><span data-stu-id="05ee3-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="05ee3-113">Расширение пользовательских сценариев на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="05ee3-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="05ee3-114">После создания шаблона hello, можно развернуть его с помощью Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="05ee3-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

