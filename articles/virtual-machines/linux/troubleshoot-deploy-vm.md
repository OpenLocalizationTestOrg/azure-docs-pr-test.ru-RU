---
title: "aaaTroubleshoot развертывание проблемы виртуальной машины Linux в Azure | Документы Microsoft"
description: "Устранение неполадок при развертывании виртуальных машин Linux в Azure (модель развертывания с помощью Resource Manager)."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="e0e8d-103">Устранение неполадок при развертывании виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="e0e8d-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="e0e8d-104">tootroubleshoot проблемы развертывания виртуальной машины (VM) в Azure, просмотрите hello [основных проблем](#top-issues) распространенных ошибок и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="e0e8d-105">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e0e8d-106">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e0e8d-107">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="e0e8d-108">Наиболее важные проблемы</span><span class="sxs-lookup"><span data-stu-id="e0e8d-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="e0e8d-109">не поддерживает кластера Hello hello запрошенный размер виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="e0e8d-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="e0e8d-110">Повторите запрос hello, с использованием меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="e0e8d-111">Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:</span><span class="sxs-lookup"><span data-stu-id="e0e8d-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="e0e8d-112">Остановите все виртуальные машины hello в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="e0e8d-113">Выберите **Группы ресурсов** > имя вашей группы ресурсов > **Ресурсы** > имя вашей группы доступности > **Виртуальные машины** > имя вашей виртуальной машины > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="e0e8d-114">После того как все hello остановка виртуальных машин, создайте hello ВМ hello требуемого размера.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="e0e8d-115">Запустить сначала hello новой виртуальной Машины, а затем выберите каждый hello остановлен, виртуальные машины и нажмите кнопку Пуск.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="e0e8d-116">Hello кластер не имеет свободных ресурсов</span><span class="sxs-lookup"><span data-stu-id="e0e8d-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="e0e8d-117">Повторите запрос hello позже.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-117">Retry hello request later.</span></span>
- <span data-ttu-id="e0e8d-118">Если hello новой виртуальной Машины можно указать различные доступности</span><span class="sxs-lookup"><span data-stu-id="e0e8d-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="e0e8d-119">Создайте виртуальную Машину в наборе доступности на другой (в hello одного региона).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="e0e8d-120">Добавление новой виртуальной Машины toohello hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="e0e8d-121">Как активировать мой ежемесячный кредит для Visual Studio Enterprise (BizSpark)?</span><span class="sxs-lookup"><span data-stu-id="e0e8d-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="e0e8d-122">tooactivate кредита вашей ежемесячно, см. в этом [статьи](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="e0e8d-123">Почему не установить драйвер графического Процессора hello для Виртуальной машине Ubuntu NV?</span><span class="sxs-lookup"><span data-stu-id="e0e8d-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="e0e8d-124">В настоящее время поддержка Linux GPU доступна только на виртуальных машинах Azure серии NC под управлением Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="e0e8d-125">Дополнительные сведения см. в статье [Установка драйверов GPU для виртуальных машин серии N под управлением Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="e0e8d-126">Для моей виртуальной машины Linux серии N отсутствуют драйверы</span><span class="sxs-lookup"><span data-stu-id="e0e8d-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="e0e8d-127">Драйверы для виртуальных машин под управлением Linux доступны [здесь](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="e0e8d-128">Не удается найти экземпляр графического процессора (GPU) на виртуальной машине серии N</span><span class="sxs-lookup"><span data-stu-id="e0e8d-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="e0e8d-129">tootake преимущества возможностей GPU hello Azure N-й серии виртуальных машин под управлением Windows Server 2016 или Windows Server 2012 R2, необходимо установить NVIDIA графические драйверы на каждую виртуальную Машину после развертывания.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="e0e8d-130">Сведения об установке драйверов доступны для [виртуальных машин Windows](../windows/n-series-driver-setup.md) и [виртуальных машин Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="e0e8d-131">Доступны ли виртуальные машины серии N в моем регионе?</span><span class="sxs-lookup"><span data-stu-id="e0e8d-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="e0e8d-132">Можно проверить доступность hello из hello [продукты, доступные по таблицы region](https://azure.microsoft.com/regions/services)и ценах [здесь](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="e0e8d-133">Я не семейство может toosee размер виртуальной Машины, которое требуется при изменении размера ВМ.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="e0e8d-134">При запуске виртуальной Машины, это развернутой tooa физического сервера.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="e0e8d-135">Hello физические серверы в регионах Azure, группируются в кластеры общих физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="e0e8d-136">Изменение размера виртуальной Машины, которая требует hello виртуальная машина перемещена toobe toodifferent аппаратных кластеров отличается в зависимости от того, какая модель развертывания было используется toodeploy hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="e0e8d-137">Виртуальные машины, развернутые в классической модели развертывания, hello развертывания облачной службы необходимо удалить и повторного развертывания размер tooa toochange hello виртуальные машины в другую семью размер.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="e0e8d-138">Виртуальных машин, развернутых в модели развертывания диспетчера ресурсов, необходимо остановить все виртуальные машины в группе перед изменением размера hello любой виртуальной Машины в наборе доступности hello доступности hello.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="e0e8d-139">Hello перечисленных размер виртуальной Машины не поддерживается при развертывании в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="e0e8d-140">Выберите размер, который поддерживается в наборе доступности hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="e0e8d-141">Рекомендуется при создании набора доступности toochoose hello наибольший размер виртуальной Машины, предполагается, что необходимо, а также иметь ее вашего первого развертывания toohello набора доступности.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="e0e8d-142">Какие дистрибутивы или версии Linux поддерживаются в Azure?</span><span class="sxs-lookup"><span data-stu-id="e0e8d-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="e0e8d-143">Список hello в Linux можно найти на [Azure-Endorsed распределения](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="e0e8d-144">Можно добавить существующую группу доступности tooan классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="e0e8d-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="e0e8d-145">Да.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-145">Yes.</span></span> <span data-ttu-id="e0e8d-146">Можно добавить существующие классические ВМ tooa новый или существующий набор доступности.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="e0e8d-147">Дополнительные сведения см. [добавить существующую группу доступности виртуальной машины tooan](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0e8d-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0e8d-148">Next steps</span></span>
<span data-ttu-id="e0e8d-149">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e0e8d-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="e0e8d-150">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e0e8d-151">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.</span><span class="sxs-lookup"><span data-stu-id="e0e8d-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
