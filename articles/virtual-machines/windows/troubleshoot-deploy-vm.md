---
title: "развертывание Windows виртуальной машины проблемы в Azure aaaTroubleshoot | Документы Microsoft"
description: "Устранение неполадок при развертывании виртуальных машин Windows в Azure (модель развертывания с помощью Resource Manager)."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="0c6a9-103">Устранение неполадок при развертывании виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="0c6a9-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="0c6a9-104">tootroubleshoot проблемы развертывания виртуальной машины (VM) в Azure, просмотрите hello [основных проблем](#top-issues) распространенных ошибок и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="0c6a9-105">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="0c6a9-106">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="0c6a9-107">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="0c6a9-108">Наиболее важные проблемы</span><span class="sxs-lookup"><span data-stu-id="0c6a9-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="0c6a9-109">не поддерживает кластера Hello hello запрошенный размер виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="0c6a9-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="0c6a9-110">Повторите запрос hello, с использованием меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="0c6a9-111">Если hello запрошенный размер hello, что виртуальная машина нельзя изменить:</span><span class="sxs-lookup"><span data-stu-id="0c6a9-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="0c6a9-112">Остановите все виртуальные машины hello в наборе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="0c6a9-113">Выберите **Группы ресурсов** > имя вашей группы ресурсов > **Ресурсы** > имя вашей группы доступности > **Виртуальные машины** > имя вашей виртуальной машины > **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="0c6a9-114">После того как все hello остановка виртуальных машин, создайте hello ВМ hello требуемого размера.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="0c6a9-115">Запустить сначала hello новой виртуальной Машины, а затем выберите каждый hello остановлен, виртуальные машины и нажмите кнопку Пуск.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="0c6a9-116">Hello кластер не имеет свободных ресурсов</span><span class="sxs-lookup"><span data-stu-id="0c6a9-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="0c6a9-117">Повторите запрос hello позже.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-117">Retry hello request later.</span></span>
- <span data-ttu-id="0c6a9-118">Если hello новой виртуальной Машины можно указать различные доступности</span><span class="sxs-lookup"><span data-stu-id="0c6a9-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="0c6a9-119">Создайте виртуальную Машину в наборе доступности на другой (в hello одного региона).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="0c6a9-120">Добавление новой виртуальной Машины toohello hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="0c6a9-121">Как использовать и развернуть образ клиента Windows в Azure?</span><span class="sxs-lookup"><span data-stu-id="0c6a9-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="0c6a9-122">В сценариях разработки и тестирования Azure можно использовать Windows 7, Windows 8 или Windows 10, если у вас есть соответствующая подписка Visual Studio (прежнее название — MSDN).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="0c6a9-123">Это [статьи](client-images.md) контуров hello требования для запуска клиента Windows в Azure, а также способы использования hello образов коллекции Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="0c6a9-124">Развертывание виртуальной машины при помощи hello преимущество использования гибридной (КОНЦЕНТРАТОР)</span><span class="sxs-lookup"><span data-stu-id="0c6a9-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="0c6a9-125">Существует несколько способов toodeploy Windows виртуальных машин с hello преимущество использования гибридной Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="0c6a9-126">Для подписки с соглашением Enterprise:</span><span class="sxs-lookup"><span data-stu-id="0c6a9-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="0c6a9-127">•   можно развернуть виртуальные машины на основе специальных образов из Marketplace, предварительно настроенных для применения программы преимуществ гибридного использования Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="0c6a9-128">Для соглашения Enterprise:</span><span class="sxs-lookup"><span data-stu-id="0c6a9-128">For Enterprise agreement:</span></span>

<span data-ttu-id="0c6a9-129">•   можно передать настраиваемую виртуальную машину и развернуть ее с помощью шаблона Resource Manager или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="0c6a9-130">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="0c6a9-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="0c6a9-131">Обзор программы преимуществ гибридного использования Azure</span><span class="sxs-lookup"><span data-stu-id="0c6a9-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="0c6a9-132">Скачиваемый файл с часто задаваемыми вопросами</span><span class="sxs-lookup"><span data-stu-id="0c6a9-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="0c6a9-133">[Преимущества гибридного использования Azure для сервера Windows Server и клиента Windows](hybrid-use-benefit-licensing.md)</span><span class="sxs-lookup"><span data-stu-id="0c6a9-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="0c6a9-134">Как использовать hello гибридного использовать преимущества Azure</span><span class="sxs-lookup"><span data-stu-id="0c6a9-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="0c6a9-135">Как активировать мой ежемесячный кредит для Visual Studio Enterprise (BizSpark)?</span><span class="sxs-lookup"><span data-stu-id="0c6a9-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="0c6a9-136">tooactivate кредита вашей ежемесячно, см. в этом [статьи](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="0c6a9-137">Как tooadd Enterprise разработки и тестирования toomy Enterprise Agreement (EA) tooget доступ к tooWindow образов клиента?</span><span class="sxs-lookup"><span data-stu-id="0c6a9-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="0c6a9-138">предложить Hello возможность toocreate подписки, основанные на hello Enterprise разработки и тестирования является ограниченным tooAccount владельцев, которые были присвоены разрешения toodo так администратором предприятия.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="0c6a9-139">Hello владелец учетной записи создает подписки через портал учетных записей Azure hello и затем следует добавить действующими подписками Visual Studio в список администраторов.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="0c6a9-140">Чтобы они смогут управлять и использовать ресурсы hello, необходимые для разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="0c6a9-141">Дополнительные сведения см. в статье [Разработка и тестирование Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="0c6a9-142">Для моей виртуальной машины Windows серии N отсутствуют драйверы</span><span class="sxs-lookup"><span data-stu-id="0c6a9-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="0c6a9-143">Драйверы для виртуальных машин под управлением Windows доступны [здесь](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="0c6a9-144">Не удается найти экземпляр графического процессора (GPU) на виртуальной машине серии N</span><span class="sxs-lookup"><span data-stu-id="0c6a9-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="0c6a9-145">tootake преимущества возможностей GPU hello Azure N-й серии виртуальных машин под управлением Windows Server 2016 или Windows Server 2012 R2, необходимо установить NVIDIA графические драйверы на каждую виртуальную Машину после развертывания.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="0c6a9-146">Сведения об установке драйверов доступны для [виртуальных машин Windows](n-series-driver-setup.md) и [виртуальных машин Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="0c6a9-147">Поддерживаются ли образы клиентов для серии N?</span><span class="sxs-lookup"><span data-stu-id="0c6a9-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="0c6a9-148">В настоящее время Azure поддерживает образы клиентов только на виртуальных машинах серии N под управлением операционных систем Windows Server и Linux.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="0c6a9-149">Доступны ли виртуальные машины серии N в моем регионе?</span><span class="sxs-lookup"><span data-stu-id="0c6a9-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="0c6a9-150">Можно проверить доступность hello из hello [продукты, доступные по таблицы region](https://azure.microsoft.com/regions/services)и ценах [здесь](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="0c6a9-151">Какие клиентские образы можно ли использовать и развертывать в Azure, а также как получить tooI их?</span><span class="sxs-lookup"><span data-stu-id="0c6a9-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="0c6a9-152">В сценариях разработки и тестирования Azure можно использовать Windows 7, Windows 8 или Windows 10 при условии, что у вас есть соответствующая подписка Visual Studio (прежнее название — MSDN).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="0c6a9-153">Образы Windows 10 можно получить из коллекции Azure hello в [предлагает подходящие для разработки и тестирования](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="0c6a9-154">Visual Studio, использующих любого типа предложения можно также [адекватно подготовки и создания](prepare-for-upload-vhd-image.md) 64-разрядный образ Windows 7, Windows 8 или Windows 10 и затем [отправить tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="0c6a9-155">Использование Hello остается ограниченной toodev и тестирования с действующими подписками Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="0c6a9-156">Это [статьи](client-images.md) контуров hello требования для запуска клиента Windows Azure и использование hello образов коллекции Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="0c6a9-157">Я не семейство может toosee размер виртуальной Машины, которое требуется при изменении размера ВМ.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="0c6a9-158">При запуске виртуальной Машины, это развернутой tooa физического сервера.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="0c6a9-159">Hello физические серверы в регионах Azure, группируются в кластеры общих физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="0c6a9-160">Изменение размера виртуальной Машины, которая требует hello виртуальная машина перемещена toobe toodifferent аппаратных кластеров отличается в зависимости от того, какая модель развертывания было используется toodeploy hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="0c6a9-161">Виртуальные машины, развернутые в классической модели развертывания, hello развертывания облачной службы необходимо удалить и повторного развертывания размер tooa toochange hello виртуальные машины в другую семью размер.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="0c6a9-162">Виртуальных машин, развернутых в модели развертывания диспетчера ресурсов, необходимо остановить все виртуальные машины в группе перед изменением размера hello любой виртуальной Машины в наборе доступности hello доступности hello.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="0c6a9-163">Hello перечисленных размер виртуальной Машины не поддерживается при развертывании в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="0c6a9-164">Выберите размер, который поддерживается в наборе доступности hello кластера.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="0c6a9-165">Рекомендуется при создании набора доступности toochoose hello наибольший размер виртуальной Машины, предполагается, что необходимо, а также иметь ее вашего первого развертывания toohello набора доступности.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="0c6a9-166">Можно добавить существующую группу доступности tooan классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="0c6a9-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="0c6a9-167">Да.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-167">Yes.</span></span> <span data-ttu-id="0c6a9-168">Можно добавить существующие классические ВМ tooa новый или существующий набор доступности.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="0c6a9-169">Дополнительные сведения см. [добавить существующую группу доступности виртуальной машины tooan](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0c6a9-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c6a9-170">Next steps</span></span>
<span data-ttu-id="0c6a9-171">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="0c6a9-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="0c6a9-172">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="0c6a9-173">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.</span><span class="sxs-lookup"><span data-stu-id="0c6a9-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
