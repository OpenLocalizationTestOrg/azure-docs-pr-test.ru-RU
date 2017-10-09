---
title: "вопросы и ответы для стека Azure aaaFrequently | Документы Microsoft"
description: "Стек Azure часто задаваемые вопросы."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a><span data-ttu-id="c44f8-103">Часто задаваемые вопросы про Azure стека</span><span class="sxs-lookup"><span data-stu-id="c44f8-103">Frequently asked questions for Azure Stack</span></span>
## <a name="deployment"></a><span data-ttu-id="c44f8-104">Развертывание</span><span class="sxs-lookup"><span data-stu-id="c44f8-104">Deployment</span></span>
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a><span data-ttu-id="c44f8-105">Нужен ли мне tooformat диски с данными до запуска или перезапуска установки?</span><span class="sxs-lookup"><span data-stu-id="c44f8-105">Do I need tooformat my data disks before starting or restarting an installation?</span></span>
<span data-ttu-id="c44f8-106">Диски должны находиться в необработанном формате.</span><span class="sxs-lookup"><span data-stu-id="c44f8-106">Disks should be in raw format.</span></span> <span data-ttu-id="c44f8-107">При переустановке операционной системы hello может требуется toocheck, если пул носителей старого hello по-прежнему присутствует и удаления с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c44f8-107">If you reinstall hello operating system, you may need toocheck if hello old storage pool is still present and delete using hello following steps:</span></span>

1. <span data-ttu-id="c44f8-108">Откройте диспетчер сервера.</span><span class="sxs-lookup"><span data-stu-id="c44f8-108">Open Server Manager.</span></span>
2. <span data-ttu-id="c44f8-109">Выберите пулы носителей.</span><span class="sxs-lookup"><span data-stu-id="c44f8-109">Select Storage Pools.</span></span>
3. <span data-ttu-id="c44f8-110">Если пул носителей отображается в разделе.</span><span class="sxs-lookup"><span data-stu-id="c44f8-110">See if a storage pool is listed.</span></span>
4. <span data-ttu-id="c44f8-111">Щелкните правой кнопкой мыши **пула носителей** Если в списке и включить чтения / записи.</span><span class="sxs-lookup"><span data-stu-id="c44f8-111">Right-click **storage pool** if listed and enable read / write.</span></span>
5. <span data-ttu-id="c44f8-112">Щелкните правой кнопкой мыши **виртуальный жесткий диск** (нижнем левом углу) и выберите Удалить.</span><span class="sxs-lookup"><span data-stu-id="c44f8-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span></span>
6. <span data-ttu-id="c44f8-113">Щелкните правой кнопкой мыши **пула носителей** и нажмите кнопку Удалить.</span><span class="sxs-lookup"><span data-stu-id="c44f8-113">Right-click **Storage Pool** and click delete.</span></span>
7. <span data-ttu-id="c44f8-114">Перед повторным запуском сценария Azure стека и проверьте, проходит проверку диска hello.</span><span class="sxs-lookup"><span data-stu-id="c44f8-114">Launch Azure Stack script again and verify that hello disk verification passes.</span></span>

<span data-ttu-id="c44f8-115">При необходимости можно использовать следующий скрипт hello:</span><span class="sxs-lookup"><span data-stu-id="c44f8-115">Optionally, hello following script can be used:</span></span>

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a><span data-ttu-id="c44f8-116">Можно использовать все диски SSD в пуле носителей hello в hello подтверждения Концепции установки?</span><span class="sxs-lookup"><span data-stu-id="c44f8-116">Can I use all SSD disks for hello storage pool in hello POC installation?</span></span>
<span data-ttu-id="c44f8-117">Дополнительные сведения о конфигурации хранилища см. в разделе hello [руководство по требованиям к](azure-stack-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c44f8-117">For more information on storage configurations, see hello [requirements guide](azure-stack-deploy.md).</span></span>

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="c44f8-118">Можно использовать диски данных NVMe для hello эта стека Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="c44f8-118">Can I use NVMe data disks for hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="c44f8-119">Хотя Storage Spaces Direct поддерживает NVMe дисков, стек Azure поддерживает только подмножество типов возможных дисков hello и возможных сочетаний для дисковых пространств.</span><span class="sxs-lookup"><span data-stu-id="c44f8-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of hello possible drive types and combinations possible for Storage Spaces Direct.</span></span>  <span data-ttu-id="c44f8-120">В разделе hello [руководство по требованиям к](azure-stack-deploy.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="c44f8-120">See hello [requirements guide](azure-stack-deploy.md) for more information.</span></span> 

### <a name="how-can-i-reinstall-azure-stack"></a><span data-ttu-id="c44f8-121">Как можно переустановить стек Azure</span><span class="sxs-lookup"><span data-stu-id="c44f8-121">How can I reinstall Azure Stack?</span></span>
<span data-ttu-id="c44f8-122">Выполните действия hello в hello [руководство повторного развертывания](azure-stack-redeploy.md).</span><span class="sxs-lookup"><span data-stu-id="c44f8-122">You can follow hello steps in hello [redeployment guide](azure-stack-redeploy.md).</span></span>  

## <a name="tenant"></a><span data-ttu-id="c44f8-123">Клиент</span><span class="sxs-lookup"><span data-stu-id="c44f8-123">Tenant</span></span>
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a><span data-ttu-id="c44f8-124">Можно развернуть собственный изображения как клиента</span><span class="sxs-lookup"><span data-stu-id="c44f8-124">Can I deploy my own images as a tenant?</span></span>
<span data-ttu-id="c44f8-125">Да, так же, как в Azure, клиент может отправить изображений в стек Azure, кроме администратора службы toousing hello изображений из hello.</span><span class="sxs-lookup"><span data-stu-id="c44f8-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition toousing hello images from hello service administrator.</span></span> <span data-ttu-id="c44f8-126">Общие сведения см. в разделе hello [Добавление образа виртуальной Машины](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="c44f8-126">For an overview, see hello [Adding a VM Image](azure-stack-add-vm-image.md).</span></span> 

## <a name="testing"></a><span data-ttu-id="c44f8-127">Тестирование</span><span class="sxs-lookup"><span data-stu-id="c44f8-127">Testing</span></span>
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="c44f8-128">Можно использовать hello tootest вложенной виртуализации эта стека Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="c44f8-128">Can I use Nested Virtualization tootest hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="c44f8-129">Вложенная виртуализация не поддерживается и не протестированы с Azure стека Technical Preview 3.</span><span class="sxs-lookup"><span data-stu-id="c44f8-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="c44f8-130">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="c44f8-130">Virtual machines</span></span>
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a><span data-ttu-id="c44f8-131">Стек Azure поддерживает динамические диски для виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="c44f8-131">Does Azure Stack support dynamic disks for virtual machines?</span></span>
<span data-ttu-id="c44f8-132">Стек Azure не поддерживает динамические диски.</span><span class="sxs-lookup"><span data-stu-id="c44f8-132">Azure Stack does not support dynamic disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c44f8-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c44f8-133">Next steps</span></span>
[<span data-ttu-id="c44f8-134">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c44f8-134">Troubleshooting</span></span>](azure-stack-troubleshooting.md)

