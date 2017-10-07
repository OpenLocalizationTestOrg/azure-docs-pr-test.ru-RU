---
title: "способы aaaDifferent toocreate виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Список способов hello toocreate виртуальной машины Windows с помощью диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="dec6b-103">Различные способы toocreate виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="dec6b-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="dec6b-104">Azure предлагает toocreate различными способами виртуальной машины, так как виртуальные машины подходят для разных пользователей и целей.</span><span class="sxs-lookup"><span data-stu-id="dec6b-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="dec6b-105">Это означает, что вы должны toomake некоторые решения о hello виртуальной машины и как toocreate его.</span><span class="sxs-lookup"><span data-stu-id="dec6b-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="dec6b-106">В этой статье предоставляет сводку часть этих вариантов и связывает tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="dec6b-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="dec6b-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="dec6b-107">Azure portal</span></span>
<span data-ttu-id="dec6b-108">С помощью портала Azure hello является tootry простым способом ожидания виртуальной машины, особенно в том случае, если только вы начинаете работать с Azure.</span><span class="sxs-lookup"><span data-stu-id="dec6b-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="dec6b-109">Создание виртуальной машины под управлением Windows, с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="dec6b-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="dec6b-110">Шаблон</span><span class="sxs-lookup"><span data-stu-id="dec6b-110">Template</span></span>
<span data-ttu-id="dec6b-111">Для виртуальных машин требуется сочетание ресурсов (таких как группы доступности и учетные записи хранения).</span><span class="sxs-lookup"><span data-stu-id="dec6b-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="dec6b-112">Вместо того чтобы развертывание и управление каждого ресурса отдельно, можно создать шаблон диспетчера ресурсов Azure, которая развертывает и подготавливает все ресурсы hello в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="dec6b-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="dec6b-113">Создание виртуальной машины Windows с использованием шаблона диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="dec6b-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="dec6b-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dec6b-114">Azure PowerShell</span></span>
<span data-ttu-id="dec6b-115">Если вы предпочитаете работать в командной строке, можно использовать Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dec6b-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="dec6b-116">Создание виртуальной машины Windows с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="dec6b-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="dec6b-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dec6b-117">Visual Studio</span></span>
<span data-ttu-id="dec6b-118">Использовать toobuild Visual Studio, управление, развертывание виртуальных машин с помощью средств hello Azure для Visual Studio и hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="dec6b-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="dec6b-119">Инструменты Azure для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dec6b-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

