---
title: "Диагностика сбоев артефактов на виртуальной машине Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как устранять неполадки при сбоях артефактов в DevTest Labs."
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
ms.openlocfilehash: e4f2946d0ba0756f36622aded0e8594acabb9527
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="diagnose-artifact-failures-in-the-lab"></a><span data-ttu-id="c7673-103">Диагностика сбоев артефактов в лаборатории</span><span class="sxs-lookup"><span data-stu-id="c7673-103">Diagnose artifact failures in the lab</span></span> 
<span data-ttu-id="c7673-104">После создания артефакта можно проверить, успешно ли он работает.</span><span class="sxs-lookup"><span data-stu-id="c7673-104">After you have created an artifact, you can check to see if it succeeded or failed.</span></span> <span data-ttu-id="c7673-105">Журналы артефактов в DevTest Labs предоставляют сведения, которые можно использовать для диагностики сбоя артефакта.</span><span class="sxs-lookup"><span data-stu-id="c7673-105">Artifact logs in DevTest Labs provide information you can use to diagnose an artifact failure.</span></span> <span data-ttu-id="c7673-106">Существует несколько способов просмотреть сведения журнала артефактов для виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="c7673-106">There are a couple different ways you can view the artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c7673-107">Чтобы можно было правильно идентифицировать и объяснить сбой, важно правильно структурировать артефакт.</span><span class="sxs-lookup"><span data-stu-id="c7673-107">To ensure that failures are correctly identified and explained, it is important that the artifact is properly structured.</span></span> <span data-ttu-id="c7673-108">Сведения о том, как правильно создать артефакт, см. в статье [Создание пользовательских артефактов для виртуальной машины DevTest Labs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="c7673-108">For information about how to correctly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="c7673-109">Правильно структурированный артефакт можно изучить на примере этого артефакта [тестовых типов параметров](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes).</span><span class="sxs-lookup"><span data-stu-id="c7673-109">And to see an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-the-azure-portal"></a><span data-ttu-id="c7673-110">Устранение неполадок при сбоях артефактов с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="c7673-110">Troubleshoot artifact failures using the Azure portal</span></span>
<span data-ttu-id="c7673-111">Чтобы использовать портал Azure для диагностики неполадок при создании артефактов, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c7673-111">To use the Azure portal to diagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="c7673-112">В списке ресурсов выберите свою лабораторию.</span><span class="sxs-lookup"><span data-stu-id="c7673-112">From the list of resources, select your lab.</span></span>

2. <span data-ttu-id="c7673-113">Выберите виртуальную машину Windows, которая содержит анализируемый артефакт.</span><span class="sxs-lookup"><span data-stu-id="c7673-113">Choose the Windows VM that includes the artifact you want to investigate.</span></span>

3. <span data-ttu-id="c7673-114">На левой панели в разделе **ОБЩИЕ** выберите **Артефакты**.</span><span class="sxs-lookup"><span data-stu-id="c7673-114">In the left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="c7673-115">Отобразится список артефактов, связанных с этой виртуальной машиной, в котором указывается имя артефакта и его состояние.</span><span class="sxs-lookup"><span data-stu-id="c7673-115">A list of artifacts associated with that VM appears, indicating the name of the artifact and its status.</span></span>

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="c7673-117">Выберите артефакт, для которого отображается состояние **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="c7673-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="c7673-118">Артефакт откроется и отобразится сообщение расширения, содержащее сведения о сбое артефакта.</span><span class="sxs-lookup"><span data-stu-id="c7673-118">The artifact opens and shows an extension message that includes details about the failure of the artifact.</span></span>

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-the-vm"></a><span data-ttu-id="c7673-120">Устранение неполадок при сбоях артефактов из виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c7673-120">Troubleshoot artifact failures from within the VM</span></span>
<span data-ttu-id="c7673-121">Чтобы просмотреть журналы артефактов из виртуальной машины, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c7673-121">To view the artifact logs from within the virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="c7673-122">Войдите в виртуальную машину, содержащую артефакт, для которого требуется выполнить диагностику.</span><span class="sxs-lookup"><span data-stu-id="c7673-122">Log in to the VM that contains the artifact you want to diagnose.</span></span>

2. <span data-ttu-id="c7673-123">Перейдите к расположению C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status, где 1.9 — это номер версии CSE.</span><span class="sxs-lookup"><span data-stu-id="c7673-123">Navigate to C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is the CSE version number.</span></span>

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="c7673-125">Откройте файл **status**, чтобы просмотреть сведения, которые помогут диагностировать сбои артефактов для данной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c7673-125">Open the **status** file to view information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="c7673-126">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="c7673-126">Related blog posts</span></span>
* <span data-ttu-id="c7673-127">[Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (Присоединение виртуальной машины к существующему домену AD с помощью шаблона ARM в Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="c7673-127">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7673-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7673-128">Next steps</span></span>
* <span data-ttu-id="c7673-129">Узнайте, как [добавить в лабораторию репозиторий Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="c7673-129">Learn how to [add a Git repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

