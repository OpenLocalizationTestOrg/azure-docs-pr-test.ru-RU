---
title: "Устранение неполадок при развертывании виртуальных машин Linux в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="eb8fa-103">Устранение неполадок при развертывании виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="eb8fa-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="eb8fa-104">Для устранения неполадок, связанных с развертыванием виртуальных машин в Azure, ознакомьтесь с разделом [Наиболее важные проблемы](#top-issues), где описаны распространенные ошибки и способы их разрешения.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="eb8fa-105">Если в любой момент при изучении этой статьи вам потребуется дополнительная помощь, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="eb8fa-106">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="eb8fa-107">Перейдите на [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и щелкните **Получить поддержку**.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="eb8fa-108">Наиболее важные проблемы</span><span class="sxs-lookup"><span data-stu-id="eb8fa-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="eb8fa-109">Кластер не поддерживает запрошенный размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="eb8fa-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="eb8fa-110">Повторите запрос с указанием меньшего размера виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="eb8fa-111">Если нельзя изменить размер запрошенной виртуальной машины,</span><span class="sxs-lookup"><span data-stu-id="eb8fa-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="eb8fa-112">остановите все виртуальные машины в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="eb8fa-113">Выберите **Группы ресурсов** > имя вашей группы ресурсов > **Ресурсы** > имя вашей группы доступности > **Виртуальные машины** > имя вашей виртуальной машины > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="eb8fa-114">После остановки всех виртуальных машин создайте виртуальную машину необходимого размера.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="eb8fa-115">Сначала запустите новую виртуальную машину, а затем выберите каждую из остановленных виртуальных машин и нажмите кнопку "Запустить".</span><span class="sxs-lookup"><span data-stu-id="eb8fa-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="eb8fa-116">В кластере нет свободных ресурсов</span><span class="sxs-lookup"><span data-stu-id="eb8fa-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="eb8fa-117">Повторите запрос позже.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-117">Retry the request later.</span></span>
- <span data-ttu-id="eb8fa-118">Если новая виртуальная машина должна быть частью другой группы доступности:</span><span class="sxs-lookup"><span data-stu-id="eb8fa-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="eb8fa-119">создайте виртуальную машину в другой группе доступности (в том же регионе);</span><span class="sxs-lookup"><span data-stu-id="eb8fa-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="eb8fa-120">добавьте новую виртуальную машину в ту же виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="eb8fa-121">Как активировать мой ежемесячный кредит для Visual Studio Enterprise (BizSpark)?</span><span class="sxs-lookup"><span data-stu-id="eb8fa-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="eb8fa-122">Чтобы активировать ежемесячный кредит, см. эту [статью](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="eb8fa-123">Почему не удается установить драйвер графического процессора (GPU) для виртуальной машины Ubuntu NV?</span><span class="sxs-lookup"><span data-stu-id="eb8fa-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="eb8fa-124">В настоящее время поддержка Linux GPU доступна только на виртуальных машинах Azure серии NC под управлением Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="eb8fa-125">Дополнительные сведения см. в статье [Установка драйверов GPU для виртуальных машин серии N под управлением Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="eb8fa-126">Для моей виртуальной машины Linux серии N отсутствуют драйверы</span><span class="sxs-lookup"><span data-stu-id="eb8fa-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="eb8fa-127">Драйверы для виртуальных машин под управлением Linux доступны [здесь](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="eb8fa-128">Не удается найти экземпляр графического процессора (GPU) на виртуальной машине серии N</span><span class="sxs-lookup"><span data-stu-id="eb8fa-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="eb8fa-129">Чтобы воспользоваться преимуществами возможностей GPU виртуальных машин Azure серии N под управлением Windows Server 2016 или Windows Server 2012 R2, необходимо установить графические драйверы NVIDIA на каждую виртуальную машину после развертывания.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="eb8fa-130">Сведения об установке драйверов доступны для [виртуальных машин Windows](../windows/n-series-driver-setup.md) и [виртуальных машин Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="eb8fa-131">Доступны ли виртуальные машины серии N в моем регионе?</span><span class="sxs-lookup"><span data-stu-id="eb8fa-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="eb8fa-132">Доступность можно проверить в [таблице "Доступность продуктов по регионам"](https://azure.microsoft.com/regions/services), а цену можно узнать [здесь](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="eb8fa-133">При изменении размера виртуальной машины не отображается необходимое семейство размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="eb8fa-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="eb8fa-134">Когда виртуальная машина запущена, она развертывается на физический сервер.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="eb8fa-135">Физические серверы в регионах Azure группируются в кластеры общего физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="eb8fa-136">Изменение размера виртуальной машины, для которого требуется переместить виртуальную машину в другой кластер оборудования, отличается в зависимости от того, какая модель развертывания использовалась для развертывания данной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="eb8fa-137">На виртуальных машинах, развернутых с помощью классической модели, необходимо удалить развертывание облачной службы и развернуть ее повторно, выбрав для виртуальных машин размер из другого семейства размеров.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="eb8fa-138">На виртуальных машинах, развернутых с помощью модели Resource Manager, необходимо остановить все виртуальные машины в группе доступности, прежде чем изменять размер любой виртуальной машины в этой группе доступности.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="eb8fa-139">Указанный размер виртуальной машины не поддерживается при развертывании в группе доступности</span><span class="sxs-lookup"><span data-stu-id="eb8fa-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="eb8fa-140">Выберите размер, который поддерживается в кластере группы доступности.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="eb8fa-141">При создании группы доступности рекомендуется выбрать самый большой размер виртуальной машины, который может понадобиться, и использовать его в качестве первого развертывания в этой группе доступности.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="eb8fa-142">Какие дистрибутивы или версии Linux поддерживаются в Azure?</span><span class="sxs-lookup"><span data-stu-id="eb8fa-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="eb8fa-143">Список для Linux приводится в статье [Linux в Azure — рекомендованные дистрибутивы](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="eb8fa-144">Можно ли добавить существующую классическую виртуальную машину в группу доступности?</span><span class="sxs-lookup"><span data-stu-id="eb8fa-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="eb8fa-145">Да.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-145">Yes.</span></span> <span data-ttu-id="eb8fa-146">Существующую классическую виртуальную машину можно добавить в новую или существующую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="eb8fa-147">Дополнительные сведения см. в разделе [Добавление существующей виртуальной машины к группе доступности](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="eb8fa-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb8fa-148">Next steps</span></span>
<span data-ttu-id="eb8fa-149">Если в любой момент при изучении этой статьи вам потребуется дополнительная помощь, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="eb8fa-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="eb8fa-150">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="eb8fa-151">Перейдите на [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и щелкните **Получить поддержку**.</span><span class="sxs-lookup"><span data-stu-id="eb8fa-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
