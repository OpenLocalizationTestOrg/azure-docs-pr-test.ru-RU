---
title: "Сравнение пользовательских образов и формул в DevTest Labs | Документация Майкрософт"
description: "Узнайте о различиях между пользовательскими образами и формулами при использовании в качестве основы для создания виртуальных машин, чтобы выбрать наиболее подходящее средство для своей среды."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="6f7aa-103">Сравнение пользовательских образов и формул в DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6f7aa-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="6f7aa-104">В качестве основы для [создания виртуальных машин](devtest-lab-add-vm-with-artifacts.md) можно использовать как [пользовательские образы](devtest-lab-create-template.md), так и [формулы](devtest-lab-manage-formulas.md).</span><span class="sxs-lookup"><span data-stu-id="6f7aa-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="6f7aa-105">Но основное различие между пользовательскими образами и формулами заключается в том, что пользовательский образ — это просто образ на основе виртуального жесткого диска, а формула — это образ на основе виртуального жесткого диска *с дополнительными* предварительно настроенными параметрами, такими как размер виртуальной машины, виртуальная сеть, подсеть и артефакты.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="6f7aa-106">Для этих предварительно настроенных параметров задаются значения по умолчанию, которые можно переопределить при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="6f7aa-107">В этой статье описываются некоторые преимущества и недостатки использования пользовательских образов и формул.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="6f7aa-108">Преимущества и недостатки пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="6f7aa-108">Custom image pros and cons</span></span>
<span data-ttu-id="6f7aa-109">Пользовательские образы обеспечивают статичный способ создания виртуальных машин на основе требуемой среды.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="6f7aa-110">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="6f7aa-110">**Pros**</span></span>

* <span data-ttu-id="6f7aa-111">Подготовка виртуальной машины из пользовательского образа происходит быстро, так как после развертывания виртуальной машины из образа ничего не меняется.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="6f7aa-112">Иными словами, параметры не применяются, так как пользовательский образ не содержит их.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="6f7aa-113">Виртуальные машины, создаваемые на основе одного и того же пользовательского образа, идентичны.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="6f7aa-114">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="6f7aa-114">**Cons**</span></span>

* <span data-ttu-id="6f7aa-115">Если требуется изменить некоторые аспекты пользовательского образа, его необходимо создать заново.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="6f7aa-116">Преимущества и недостатки формул</span><span class="sxs-lookup"><span data-stu-id="6f7aa-116">Formula pros and cons</span></span>
<span data-ttu-id="6f7aa-117">Формулы позволяют динамически создавать виртуальные машины на основе нужной конфигурации и параметров.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="6f7aa-118">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="6f7aa-118">**Pros**</span></span>

* <span data-ttu-id="6f7aa-119">Изменения в среде можно фиксировать в режиме реального времени с помощью артефактов.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="6f7aa-120">Например, если нужно установить виртуальную машину с последними обновлениями из конвейера выпуска или включить последний код из репозитория, то можно просто указать в формуле артефакт, который развертывает последние обновления или включает последний код, вместе с целевым базовым образом.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="6f7aa-121">При каждом использовании этой формулы для создания виртуальных машин в них будут развертываться последние обновления и включаться последний код.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="6f7aa-122">В формулах можно определять параметры по умолчанию, например размер виртуальной машины и параметры виртуальной сети, что невозможно в случае с пользовательскими образами.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="6f7aa-123">Параметры, сохраненные в формуле, отображаются как значения по умолчанию, но их можно изменить при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="6f7aa-124">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="6f7aa-124">**Cons**</span></span>

* <span data-ttu-id="6f7aa-125">Создание виртуальной машины на основе формулы может занимать больше времени, чем ее создание из пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="6f7aa-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="6f7aa-126">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="6f7aa-126">Related blog posts</span></span>
* [<span data-ttu-id="6f7aa-127">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="6f7aa-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="6f7aa-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f7aa-128">Next steps</span></span>
- [<span data-ttu-id="6f7aa-129">Часто задаваемые вопросы о DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6f7aa-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)