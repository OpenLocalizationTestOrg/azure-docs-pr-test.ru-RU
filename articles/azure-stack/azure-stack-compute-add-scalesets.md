---
title: "масштабирования виртуальных машин aaaMake наборов, доступных в стек Azure"
description: "Узнайте, как добавить администратора облака toohello масштабирования виртуальной машины Azure Marketplace стека"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a><span data-ttu-id="f86d2-103">Открытие набора масштабирования виртуальной машины в стек Azure</span><span class="sxs-lookup"><span data-stu-id="f86d2-103">Make virtual machine scale sets available in Azure Stack</span></span>
<span data-ttu-id="f86d2-104">Наборы масштабирования виртуальной машины — это ресурс Azure стека вычислений.</span><span class="sxs-lookup"><span data-stu-id="f86d2-104">Virtual machine scale sets are an Azure Stack compute resource.</span></span> <span data-ttu-id="f86d2-105">Можно использовать их toodeploy и управление набором одинаковые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="f86d2-105">You can use them toodeploy and manage a set of identical virtual machines.</span></span> <span data-ttu-id="f86d2-106">Здравствуйте, же со всех виртуальных машин, наборы масштабирования не требуется предварительно подготовку виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f86d2-106">With all virtual machines configured hello same, scale sets don’t require pre-provisioning of virtual machines.</span></span> <span data-ttu-id="f86d2-107">Это упрощает toobuild крупномасштабных служб, предназначенных для больших вычислений, большие наборы данных и контейнерах рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="f86d2-107">It's easier toobuild large-scale services that target big compute, big data, and containerized workloads.</span></span>

<span data-ttu-id="f86d2-108">В этом разделе поможет hello процесса toomake наборы масштабирования в Azure Marketplace стека hello.</span><span class="sxs-lookup"><span data-stu-id="f86d2-108">This topic guides you through hello process toomake scale sets available in hello Azure Stack Marketplace.</span></span> <span data-ttu-id="f86d2-109">После завершения этой процедуры, пользователи могут добавлять подписки tootheir наборов масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f86d2-109">After you complete this procedure, your users can add virtual machine scale sets tootheir subscriptions.</span></span>

<span data-ttu-id="f86d2-110">Наборы масштабирования виртуальных машин Azure стеке похожи на наборы масштабирования виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="f86d2-110">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span></span> <span data-ttu-id="f86d2-111">Дополнительные сведения см. в разделе hello следующие видео:</span><span class="sxs-lookup"><span data-stu-id="f86d2-111">For more information, see hello following videos:</span></span>
* [<span data-ttu-id="f86d2-112">Марк Руссинович (Mark Russinovich) рассказывает о масштабируемых наборах Azure.</span><span class="sxs-lookup"><span data-stu-id="f86d2-112">Mark Russinovich talks Azure scale sets</span></span>](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [<span data-ttu-id="f86d2-113">Масштабируемые наборы виртуальных машин с Гаем Бауэрманом (Guy Bowerman).</span><span class="sxs-lookup"><span data-stu-id="f86d2-113">Virtual Machine Scale Sets with Guy Bowerman</span></span>](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

<span data-ttu-id="f86d2-114">Стек Azure наборы масштабирования виртуальных машин не поддерживают автоматическое масштабирование.</span><span class="sxs-lookup"><span data-stu-id="f86d2-114">On Azure Stack, Virtual Machine Scale Sets do not support auto-scale.</span></span> <span data-ttu-id="f86d2-115">Можно добавить дополнительные экземпляры tooa масштабирования, заданные с помощью портала Azure стека hello, шаблоны диспетчера ресурсов или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f86d2-115">You can add more instances tooa scale set using hello Azure Stack portal, Resource Manager templates, or PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f86d2-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f86d2-116">Prerequisites</span></span>
* <span data-ttu-id="f86d2-117">**PowerShell и средства**</span><span class="sxs-lookup"><span data-stu-id="f86d2-117">**Powershell and tools**</span></span>

   <span data-ttu-id="f86d2-118">Установка и настроенный PowerShell для Azure стека и средства Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="f86d2-118">Install and configured PowerShell for Azure Stack and hello Azure Stack tools.</span></span> <span data-ttu-id="f86d2-119">В разделе [приступить к работе с PowerShell Azure стека](azure-stack-powershell-configure-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="f86d2-119">See [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md).</span></span>

   <span data-ttu-id="f86d2-120">После установки средств Azure стека hello, убедитесь, что импорт hello следующий модуль PowerShell (toohello относительный путь. \ComputeAdmin папки в папке hello AzureStack средства главным):</span><span class="sxs-lookup"><span data-stu-id="f86d2-120">After you install hello Azure Stack tools, make sure you import hello following PowerShell module (path relative toohello .\ComputeAdmin folder in hello AzureStack-Tools-master folder):</span></span>

        Import-Module .\AzureStack.ComputeAdmin.psm1

* <span data-ttu-id="f86d2-121">**Образ операционной системы**</span><span class="sxs-lookup"><span data-stu-id="f86d2-121">**Operating system image**</span></span>

   <span data-ttu-id="f86d2-122">Если вы не добавляли tooyour образа операционной системы Azure Marketplace стека, см. раздел [добавить hello виртуальной Машины Windows Server 2016 изображения toohello стека Azure marketplace](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="f86d2-122">If you haven’t added an operating system image tooyour Azure Stack Marketplace, see [Add hello Windows Server 2016 VM image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>

   <span data-ttu-id="f86d2-123">Поддержка Linux загрузить Ubuntu Server 16.04 и добавить его с помощью ```Add-AzsVMImage``` с hello следующие параметры: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span><span class="sxs-lookup"><span data-stu-id="f86d2-123">For Linux support, download Ubuntu Server 16.04 and add it using ```Add-AzsVMImage``` with hello following parameters: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span></span>

## <a name="add-hello-virtual-machine-scale-set"></a><span data-ttu-id="f86d2-124">Добавление набора масштабирования виртуальных машин hello</span><span class="sxs-lookup"><span data-stu-id="f86d2-124">Add hello virtual machine scale set</span></span>

<span data-ttu-id="f86d2-125">Измените hello следующие команды PowerShell, скрипт для вашей среды, а затем запустите ее tooadd tooyour набор масштабирования виртуальной машины Azure Marketplace стека.</span><span class="sxs-lookup"><span data-stu-id="f86d2-125">Edit hello following PowerShell script for your environment and then run it tooadd a virtual machine scale set tooyour Azure Stack Marketplace.</span></span> 

<span data-ttu-id="f86d2-126">``$User``— Учетная запись hello, портал администратора hello tooconnect использовать.</span><span class="sxs-lookup"><span data-stu-id="f86d2-126">``$User`` is hello account you use tooconnect hello administrator portal.</span></span> <span data-ttu-id="f86d2-127">Например, serviceadmin@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f86d2-127">For example, serviceadmin@contoso.onmicrosoft.com.</span></span>

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a><span data-ttu-id="f86d2-128">Удалить набор масштабирования виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f86d2-128">Remove a virtual machine scale set</span></span>

<span data-ttu-id="f86d2-129">tooremove элемент коллекции набора масштабирования виртуальных машин, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="f86d2-129">tooremove a virtual machine scale set gallery item, run hello following PowerShell command:</span></span>

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> <span data-ttu-id="f86d2-130">элемент коллекции Hello не может быть удалено непосредственно.</span><span class="sxs-lookup"><span data-stu-id="f86d2-130">hello gallery item may not be removed immediately.</span></span> <span data-ttu-id="f86d2-131">Может потребоваться несколько раз toorefresh hello портала, перед удалением из hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f86d2-131">You may need toorefresh hello portal several times before it is removed from hello Marketplace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f86d2-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f86d2-132">Next steps</span></span>
[<span data-ttu-id="f86d2-133">Часто задаваемые вопросы про Azure стека</span><span class="sxs-lookup"><span data-stu-id="f86d2-133">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

