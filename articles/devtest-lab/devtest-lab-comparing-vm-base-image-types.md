---
title: "aaaComparing пользовательских образов и формул в DevTest Labs | Документы Microsoft"
description: "Дополнительные сведения о hello различия между пользовательских образов и формулы, как виртуальная машина оснований, чтобы можно было решить, какой из них лучше всего подходит для вашей среды."
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
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="2f158-103">Сравнение пользовательских образов и формул в DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2f158-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="2f158-104">В качестве основы для [создания виртуальных машин](devtest-lab-add-vm-with-artifacts.md) можно использовать как [пользовательские образы](devtest-lab-create-template.md), так и [формулы](devtest-lab-manage-formulas.md).</span><span class="sxs-lookup"><span data-stu-id="2f158-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="2f158-105">Hello ключевое различие между пользовательских образов и формулы, то, что пользовательский образ является просто изображение, основываясь на виртуальный жесткий ДИСК, а формула является изображение, зависящее от виртуального жесткого диска *в дополнение к* заранее настроенные параметры — например размер виртуальной Машины, виртуальной сети подсеть и артефакты.</span><span class="sxs-lookup"><span data-stu-id="2f158-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="2f158-106">Эти заранее настроенные параметры настраиваются со значениями по умолчанию, которые могут быть изменены во время создания виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="2f158-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="2f158-107">В этой статье описываются некоторые из преимуществ hello (-специалистов) и недостатки пользовательских образов toousing (cons) и с помощью формул.</span><span class="sxs-lookup"><span data-stu-id="2f158-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="2f158-108">Преимущества и недостатки пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="2f158-108">Custom image pros and cons</span></span>
<span data-ttu-id="2f158-109">Пользовательские изображения предоставляют toocreate как статические, неизменяемый виртуальные машины с требуемой среде.</span><span class="sxs-lookup"><span data-stu-id="2f158-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="2f158-110">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="2f158-110">**Pros**</span></span>

* <span data-ttu-id="2f158-111">Подготовки с помощью пользовательского образа виртуальной Машины осуществляется быстрее, что ничего не изменилось после приветствия зацикливается виртуальной Машины из образа hello.</span><span class="sxs-lookup"><span data-stu-id="2f158-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="2f158-112">Другими словами нет tooapply без параметров, как hello пользовательские — это изображение без параметров.</span><span class="sxs-lookup"><span data-stu-id="2f158-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="2f158-113">Виртуальные машины, создаваемые на основе одного и того же пользовательского образа, идентичны.</span><span class="sxs-lookup"><span data-stu-id="2f158-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="2f158-114">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="2f158-114">**Cons**</span></span>

* <span data-ttu-id="2f158-115">При необходимости tooupdate некоторых аспектов пользовательского образа hello, необходимо повторно создать образ hello.</span><span class="sxs-lookup"><span data-stu-id="2f158-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="2f158-116">Преимущества и недостатки формул</span><span class="sxs-lookup"><span data-stu-id="2f158-116">Formula pros and cons</span></span>
<span data-ttu-id="2f158-117">Формулы предоставляют toocreate динамическое виртуальных машин из параметров конфигурации требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="2f158-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="2f158-118">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="2f158-118">**Pros**</span></span>

* <span data-ttu-id="2f158-119">Изменения в среде hello можно записать на лету hello через артефакты.</span><span class="sxs-lookup"><span data-stu-id="2f158-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="2f158-120">Например, если требуется виртуальная машина устанавливается вместе с последней биты hello из конвейера выпуска или прикрепить hello последнюю кода из репозитория, можно просто указать артефактом, который развертывает последнюю bits hello или присоединяет последнюю кода hello в формуле hello вместе с целевой базовый образ.</span><span class="sxs-lookup"><span data-stu-id="2f158-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="2f158-121">Всякий раз, когда эта формула используется toocreate виртуальные машины, последнюю hello бит/кода, развернуты прикрепления toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f158-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="2f158-122">В формулах можно определять параметры по умолчанию, например размер виртуальной машины и параметры виртуальной сети, что невозможно в случае с пользовательскими образами.</span><span class="sxs-lookup"><span data-stu-id="2f158-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="2f158-123">Hello параметры, сохраненные в формуле отображаются как значения по умолчанию, но можно изменить при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f158-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="2f158-124">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="2f158-124">**Cons**</span></span>

* <span data-ttu-id="2f158-125">Создание виртуальной машины на основе формулы может занимать больше времени, чем ее создание из пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="2f158-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="2f158-126">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="2f158-126">Related blog posts</span></span>
* [<span data-ttu-id="2f158-127">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="2f158-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="2f158-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f158-128">Next steps</span></span>
- [<span data-ttu-id="2f158-129">Часто задаваемые вопросы о DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2f158-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)