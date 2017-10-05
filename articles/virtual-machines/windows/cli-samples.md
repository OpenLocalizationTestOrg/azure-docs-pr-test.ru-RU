---
title: "Примеры Azure CLI для Windows | Документация Майкрософт"
description: "Примеры Azure CLI для Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f4b2e8a5583855df7472af3fbef01ac641caf6bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="bc1ff-103">Примеры Azure CLI для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="bc1ff-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="bc1ff-104">В следующей таблице содержатся ссылки на скрипты Bash, созданные с помощью Azure CLI, которые развертывают виртуальные машины Windows.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-104">The following table includes links to bash scripts built using the Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="bc1ff-105">**Создание виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="bc1ff-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="bc1ff-106">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bc1ff-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-107">Создает виртуальную машину Windows с минимальной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="bc1ff-108">Создание полностью настроенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bc1ff-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-109">Создает группу ресурсов, виртуальную машину и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="bc1ff-110">Создание высокодоступной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bc1ff-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-111">Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="bc1ff-112">Создание виртуальной машины с помощью NGINX</span><span class="sxs-lookup"><span data-stu-id="bc1ff-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-113">Создает виртуальную машину и использует расширение пользовательских скриптов Azure для установки IIS.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-113">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="bc1ff-114">Создание виртуальной машины с IIS с помощью DSC</span><span class="sxs-lookup"><span data-stu-id="bc1ff-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-115">Создает виртуальную машину и использует расширение настройки требуемого состояния (DSC) для установки IIS.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-115">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
|<span data-ttu-id="bc1ff-116">**Сети виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="bc1ff-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="bc1ff-117">Защита сетевого трафика между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="bc1ff-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-118">Создает две виртуальные машины, все связанные ресурсы, а также внешние и внутренние группы безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="bc1ff-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="bc1ff-119">**Защита виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="bc1ff-119">**Secure virtual machines**</span></span>||
| <span data-ttu-id="bc1ff-120">[Encrypt a Windows virtual machine with Azure PowerShell](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) (Шифрование виртуальной машины Windows с помощью Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="bc1ff-120">[Encrypt a VM and data disks](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json)</span></span> | <span data-ttu-id="bc1ff-121">Создание Azure Key Vault, ключа шифрования и субъекта-службы. Шифрование виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="bc1ff-122">**Мониторинг виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="bc1ff-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="bc1ff-123">Мониторинг виртуальной машины с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="bc1ff-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="bc1ff-124">Создает виртуальную машину, устанавливает агент Operations Management Suite и регистрирует виртуальную машину в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="bc1ff-124">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |
