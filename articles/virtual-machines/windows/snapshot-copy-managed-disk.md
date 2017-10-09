---
title: "aaaCreate копию управляемых диска Azure для резервного копирования | Документы Microsoft"
description: "Узнайте, как toocreate копию toouse Azure управляемого диска для диска обратно вверх или устранения неполадок проблемы."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="4aa43-103">Создание копии виртуального жесткого диска, хранящегося в виде управляемого диска Azure, с помощью управляемых моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="4aa43-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="4aa43-104">Снимок управляемых диск для резервного копирования или создать диск управляемых из моментального снимка hello и присоединить ее tootroubleshoot виртуальной машины tooa теста.</span><span class="sxs-lookup"><span data-stu-id="4aa43-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="4aa43-105">Управляемый моментальный снимок — это полная копия управляемого диска виртуальной машины на определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="4aa43-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="4aa43-106">Он создает копию виртуального жесткого диска только для чтения и по умолчанию сохраняет ее в качестве управляемого диска уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="4aa43-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="4aa43-107">Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4aa43-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="4aa43-108">Дополнительные сведения о ценах см. на странице [с ценами на службу хранилища Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="4aa43-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4aa43-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4aa43-109">Before you begin</span></span>
<span data-ttu-id="4aa43-110">При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="4aa43-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="4aa43-111">Запустите hello следующие tooinstall команды.</span><span class="sxs-lookup"><span data-stu-id="4aa43-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="4aa43-112">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4aa43-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="4aa43-113">Скопируйте hello виртуального жесткого диска с помощью моментального снимка</span><span class="sxs-lookup"><span data-stu-id="4aa43-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="4aa43-114">Используйте hello портал Azure или tootake PowerShell моментальный снимок hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="4aa43-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="4aa43-115">Использование Azure портала tootake моментального снимка</span><span class="sxs-lookup"><span data-stu-id="4aa43-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="4aa43-116">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4aa43-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4aa43-117">Начиная с левого верхнего угла hello, нажмите кнопку **New** и выполните поиск **моментального снимка**.</span><span class="sxs-lookup"><span data-stu-id="4aa43-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="4aa43-118">В колонке hello моментального снимка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="4aa43-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="4aa43-119">Введите **имя** для hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="4aa43-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="4aa43-120">Выберите существующую [группы ресурсов](../../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую.</span><span class="sxs-lookup"><span data-stu-id="4aa43-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="4aa43-121">Выберите расположение центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa43-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="4aa43-122">Для **исходный диск**, выберите hello toosnapshot управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="4aa43-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="4aa43-123">Выберите hello **тип счета** toouse toostore hello снимка.</span><span class="sxs-lookup"><span data-stu-id="4aa43-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="4aa43-124">Мы рекомендуем тип **Standard_LRS**, если вам не требуется хранить моментальный снимок на высокопроизводительном диске.</span><span class="sxs-lookup"><span data-stu-id="4aa43-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="4aa43-125">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4aa43-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="4aa43-126">Используйте PowerShell tootake моментального снимка</span><span class="sxs-lookup"><span data-stu-id="4aa43-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="4aa43-127">Hello следующее показано, как tooget hello VHD на диске toobe копируются, создания hello конфигураций моментального снимка и снимок hello диска с помощью командлета New-AzureRmSnapshot hello<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="4aa43-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="4aa43-128">Задайте некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="4aa43-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="4aa43-129">Замените значения параметров hello:</span><span class="sxs-lookup"><span data-stu-id="4aa43-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="4aa43-130">«myResourceGroup» с группой ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="4aa43-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="4aa43-131">«southeastasia» с место снимок управляемых хранимых географическое расположение hello.</span><span class="sxs-lookup"><span data-stu-id="4aa43-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="4aa43-132">«ContosoMD_datadisk1» с именем hello, которые должны toocopy диска VHD hello.</span><span class="sxs-lookup"><span data-stu-id="4aa43-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="4aa43-133">«ContosoMD_datadisk1_snapshot1» с hello именем, вы должны toouse для hello новый моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="4aa43-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="4aa43-134">Получение hello VHD диск toobe копируются.</span><span class="sxs-lookup"><span data-stu-id="4aa43-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="4aa43-135">Создайте моментальный снимок конфигурации, hello.</span><span class="sxs-lookup"><span data-stu-id="4aa43-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="4aa43-136">Снимок "hello".</span><span class="sxs-lookup"><span data-stu-id="4aa43-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="4aa43-137">Если план toouse hello моментального снимка toocreate диск управляемых и присоединить ее к виртуальной Машине, должен toobe высокопроизводительной, используйте параметр hello `-AccountType Premium_LRS` с помощью команды New-AzureRmSnapshot hello.</span><span class="sxs-lookup"><span data-stu-id="4aa43-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="4aa43-138">параметр Hello создает hello моментальных снимков, чтобы оно хранится как диск управляемых Premium.</span><span class="sxs-lookup"><span data-stu-id="4aa43-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="4aa43-139">Управляемые диски уровня "Премиум" дороже, чем управляемые диски уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="4aa43-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="4aa43-140">Поэтому, прежде чем использовать этот параметр, убедитесь, что вам действительно необходим управляемый диск уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="4aa43-140">So be sure you really need Premium before using that parameter.</span></span>


