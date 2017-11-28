---
title: "aaaAzure образец скрипта CLI - Создание управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке | Документы Microsoft"
description: "Сценарий Azure CLI пример — создание управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="868aa-103">Создание управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке с CLI</span><span class="sxs-lookup"><span data-stu-id="868aa-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="868aa-104">Этот скрипт создает управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="868aa-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="868aa-105">Используйте этот скрипт tooimport специальных (не обобщенный или командой Sysprep) виртуального жесткого диска toomanaged ОС диска toocreate виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="868aa-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="868aa-106">Или использовать его tooimport диск данных виртуального жесткого диска toomanaged данных.</span><span class="sxs-lookup"><span data-stu-id="868aa-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="868aa-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="868aa-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="868aa-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="868aa-108">Script explanation</span></span>

<span data-ttu-id="868aa-109">Этот скрипт использует следующие команды toocreate управляемого диска с виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="868aa-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="868aa-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="868aa-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="868aa-111">Команда</span><span class="sxs-lookup"><span data-stu-id="868aa-111">Command</span></span> | <span data-ttu-id="868aa-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="868aa-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="868aa-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="868aa-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="868aa-114">Создает управляемый диска с использованием URI виртуального жесткого диска в учетной записи хранения в hello одной подписке</span><span class="sxs-lookup"><span data-stu-id="868aa-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="868aa-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="868aa-115">Next steps</span></span>

[<span data-ttu-id="868aa-116">Создание виртуальной машины путем подключения управляемого диска как диска ОС</span><span class="sxs-lookup"><span data-stu-id="868aa-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="868aa-117">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="868aa-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="868aa-118">Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="868aa-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
