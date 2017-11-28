---
title: "Azure управляемые диск для резервного копирования aaaCopy | Документы Microsoft"
description: "Узнайте, как toocreate копию toouse Azure управляемого диска для диска обратно вверх или устранения неполадок проблемы."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="11d5a-103">Создание копии виртуального жесткого диска, хранящегося в виде управляемого диска Azure, с помощью управляемых моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="11d5a-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="11d5a-104">Снимок управляемые диск для резервного копирования или создать диск управляемых из моментального снимка hello и присоединить ее tootroubleshoot виртуальной машины для теста tooa.</span><span class="sxs-lookup"><span data-stu-id="11d5a-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="11d5a-105">Управляемый моментальный снимок — это полная копия управляемого диска виртуальной машины на определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="11d5a-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="11d5a-106">Он создает копию виртуального жесткого диска только для чтения и по умолчанию сохраняет ее в качестве управляемого диска уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="11d5a-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="11d5a-107">Дополнительные сведения о ценах см. на странице [с ценами на службу хранилища Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="11d5a-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="11d5a-108">Используйте либо hello Azure portal или hello Azure CLI 2.0 tootake моментальный снимок hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="11d5a-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="11d5a-109">Использование Azure CLI 2.0 tootake моментального снимка</span><span class="sxs-lookup"><span data-stu-id="11d5a-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="11d5a-110">Hello следующий пример требует hello Azure CLI 2.0 установлена и выполнил вход в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="11d5a-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="11d5a-111">Hello следующие шаги показывают, как tooobtain и сделайте снимок управляемого ОС диска при использовании hello `az snapshot create` с hello `--source-disk` параметра.</span><span class="sxs-lookup"><span data-stu-id="11d5a-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="11d5a-112">Hello в примере предполагается наличие виртуальной Машины, которая называется `myVM` создан с использованием управляемого диска ОС в hello `myResourceGroup` группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11d5a-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="11d5a-113">Hello вывод должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="11d5a-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="11d5a-114">Использование Azure портала tootake моментального снимка</span><span class="sxs-lookup"><span data-stu-id="11d5a-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="11d5a-115">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11d5a-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="11d5a-116">Начиная с левого верхнего hello, нажмите кнопку **New** и выполните поиск **моментального снимка**.</span><span class="sxs-lookup"><span data-stu-id="11d5a-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="11d5a-117">В колонке hello моментального снимка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="11d5a-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="11d5a-118">Введите **имя** для hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="11d5a-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="11d5a-119">Выберите существующую [группы ресурсов](../../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую.</span><span class="sxs-lookup"><span data-stu-id="11d5a-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="11d5a-120">Выберите расположение центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="11d5a-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="11d5a-121">Для **исходный диск**, выберите hello toosnapshot управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="11d5a-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="11d5a-122">Выберите hello **тип счета** toouse toostore hello снимка.</span><span class="sxs-lookup"><span data-stu-id="11d5a-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="11d5a-123">Мы рекомендуем тип **Standard_LRS**, если вам не требуется хранить моментальный снимок на высокопроизводительном диске.</span><span class="sxs-lookup"><span data-stu-id="11d5a-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="11d5a-124">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="11d5a-124">Click **Create**.</span></span>

<span data-ttu-id="11d5a-125">Если план toouse hello моментального снимка toocreate диск управляемых и присоединить ее к виртуальной Машине, должен toobe высокопроизводительной, используйте параметр hello `--sku Premium_LRS` с hello `az snapshot create` команды.</span><span class="sxs-lookup"><span data-stu-id="11d5a-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="11d5a-126">Это создает hello моментального снимка, он сохранится как диск управляемых Premium.</span><span class="sxs-lookup"><span data-stu-id="11d5a-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="11d5a-127">Управляемые диски уровня "Премиум" работают быстрее, так как это твердотельные накопители (SSD), однако их использование обойдется дороже, чем диски уровня "Стандартный" (жесткие диски).</span><span class="sxs-lookup"><span data-stu-id="11d5a-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


