---
title: "Пример сценария Azure CLI. Экспорт или копирование моментального снимка в виде VHD в учетную запись хранения в другом регионе | Документы Майкрософт"
description: "Пример сценария Azure CLI. Экспорт или копирование моментального снимка в виде VHD в учетную запись хранения в той же или другой подписке"
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
ms.openlocfilehash: a6ea65aba91641ece415db4df6ae9c17b42a0954
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="4da62-103">Экспорт или копирование управляемых моментальных снимков в виде VHD-файлов в учетную запись хранения в другом регионе с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="4da62-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="4da62-104">Этот сценарий экспортирует управляемый моментальный снимок в учетную запись хранения в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="4da62-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="4da62-105">Сначала он создает URI SAS для моментального снимка, а затем использует его для копирования в учетную запись хранения в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="4da62-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="4da62-106">Этот сценарий можно использовать для обеспечения резервной копии управляемых дисков в другом регионе в целях аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="4da62-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4da62-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4da62-107">Sample script</span></span>

<span data-ttu-id="4da62-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Копирование моментального снимка")]</span><span class="sxs-lookup"><span data-stu-id="4da62-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="4da62-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4da62-109">Script explanation</span></span>

<span data-ttu-id="4da62-110">Этот сценарий выполняет приведенные ниже команды для создания универсального кода ресурса (URI) SAS для управляемого моментального снимка и копирует моментальный снимок в учетную запись хранения, используя созданный универсальный код ресурса (URI) SAS.</span><span class="sxs-lookup"><span data-stu-id="4da62-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="4da62-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="4da62-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4da62-112">Команда</span><span class="sxs-lookup"><span data-stu-id="4da62-112">Command</span></span> | <span data-ttu-id="4da62-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="4da62-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4da62-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="4da62-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="4da62-115">Создает SAS только для чтения, который используется для копирования базового VHD-файла в учетную запись хранения или загрузки в локальную среду.</span><span class="sxs-lookup"><span data-stu-id="4da62-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="4da62-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="4da62-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="4da62-117">Асинхронно копирует большой двоичный объект из одной учетной записи хранения в другую.</span><span class="sxs-lookup"><span data-stu-id="4da62-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4da62-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4da62-118">Next steps</span></span>

[<span data-ttu-id="4da62-119">Создание управляемого диска на основе VHD</span><span class="sxs-lookup"><span data-stu-id="4da62-119">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="4da62-120">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="4da62-120">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="4da62-121">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4da62-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4da62-122">Дополнительные примеры сценариев интерфейса командной строки для виртуальных машин и управляемых дисков см. в [документации по виртуальным машинам Azure под управлением Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4da62-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
