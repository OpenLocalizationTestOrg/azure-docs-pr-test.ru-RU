---
title: "Пример сценария CLI - Экспорт копирования моментальных снимков с учетной записью хранения tooa VHD в другом регионе aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI - Экспорт копирования моментальных снимков с учетной записью хранения tooa виртуального жесткого диска в тот же или другой подписке"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="39012-103">Экспорт» или «копировать управляемый снимки с учетной записью хранения tooa VHD в другом регионе с CLI</span><span class="sxs-lookup"><span data-stu-id="39012-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="39012-104">Этот сценарий экспортирует учетную запись хранения tooa управляемого моментального снимка в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="39012-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="39012-105">Сначала генерации hello универсальный код Ресурса SAS hello моментальных снимков и использует его toocopy его tooa учетной записи хранилища в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="39012-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="39012-106">Используйте эту резервную копию toomaintain сценария управляемого диски в другом регионе для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="39012-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="39012-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="39012-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="39012-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="39012-108">Script explanation</span></span>

<span data-ttu-id="39012-109">Этот скрипт использует следующую toogenerate команды универсальный код Ресурса SAS для управляемых hello моментального снимка и копий моментальных снимков tooa учетной записи хранилища с помощью универсального кода Ресурса SAS.</span><span class="sxs-lookup"><span data-stu-id="39012-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="39012-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="39012-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="39012-111">Команда</span><span class="sxs-lookup"><span data-stu-id="39012-111">Command</span></span> | <span data-ttu-id="39012-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="39012-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39012-113">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="39012-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="39012-114">Создает локальный tooon SAS только для чтения, используется toocopy основной учетной записи хранилища tooa файл виртуального жесткого диска или загрузите его</span><span class="sxs-lookup"><span data-stu-id="39012-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="39012-115">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="39012-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="39012-116">Асинхронно копирует большой двоичный объект из одного tooanother учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="39012-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39012-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39012-117">Next steps</span></span>

[<span data-ttu-id="39012-118">Создание управляемого диска на основе VHD</span><span class="sxs-lookup"><span data-stu-id="39012-118">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="39012-119">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="39012-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="39012-120">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="39012-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="39012-121">Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39012-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
