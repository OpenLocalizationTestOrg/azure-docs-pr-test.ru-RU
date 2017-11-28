---
title: "сбои aaaDiagnose артефакта в виртуальной Машине Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tootroubleshoot сбоев артефакта в DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="aa2cb-103">Диагностику сбоев артефакта в лаборатории hello</span><span class="sxs-lookup"><span data-stu-id="aa2cb-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="aa2cb-104">После создания артефакта toosee можно проверить, если он успешно или неудачно.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="aa2cb-105">Журналы артефакта в DevTest Labs предоставляют сведения, которые можно использовать toodiagnose сбоя артефакта.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="aa2cb-106">Существует несколько способов, можно просмотреть сведения о журнале hello артефакта для виртуальной Машины Windows.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="aa2cb-107">tooensure, сбои идентифицируются и описано, очень важно, этим артефактом hello неправильно структурированы правильно.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="aa2cb-108">Сведения о как toocorrectly построить артефакта содержатся [создать пользовательские артефакты](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="aa2cb-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="aa2cb-109">И toosee пример правильно структурированного артефакта, ознакомьтесь с этой [типы параметров тестирования](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) артефакта.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="aa2cb-110">Устранение неполадок при неудачном артефакта, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="aa2cb-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="aa2cb-111">toouse hello Azure портала toodiagnose сбоев во время создания артефакта, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="aa2cb-112">Выберите из списка hello ресурсов лаборатории.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="aa2cb-113">Выберите hello виртуальной Машине Windows, включающий требуется tooinvestigate артефакта hello.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="aa2cb-114">Hello левой панели в разделе **Общие**, выберите **артефакты**.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="aa2cb-115">Отображается список артефакты, связанные с этой виртуальной Машины, является признаком того, имя hello hello артефактов и их состояния.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="aa2cb-117">Выберите артефакт, для которого отображается состояние **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="aa2cb-118">артефакт Hello открывается и отображается сообщение расширения, включающий сведения о сбое hello hello артефакта.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="aa2cb-120">Устранение неполадок при неудачном артефакта из внутри hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="aa2cb-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="aa2cb-121">tooview hello артефакта журналы hello виртуальной машине, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="aa2cb-122">Войдите в виртуальной Машине, которая содержит артефакт hello требуется toodiagnose toohello.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="aa2cb-123">Перейдите tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status где «1.9 — номер версии CSE hello.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="aa2cb-125">Откройте hello **состояние** файл tooview данные, что помогает диагностировать артефакта для этой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="aa2cb-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="aa2cb-126">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="aa2cb-126">Related blog posts</span></span>
* [<span data-ttu-id="aa2cb-127">Присоединение виртуальной Машины tooexisting домена AD, с помощью шаблона диспетчера ресурсов в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aa2cb-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="aa2cb-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa2cb-128">Next steps</span></span>
* <span data-ttu-id="aa2cb-129">Узнайте, каким образом слишком[добавьте лаборатории tooa репозитория Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="aa2cb-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

