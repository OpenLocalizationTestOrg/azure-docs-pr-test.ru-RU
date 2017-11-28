---
title: "Создание образа виртуальной машины для Azure Marketplace | Документация Майкрософт"
description: "Подробные инструкции по созданию образа виртуальной машины для Azure Marketplace для приобретения другими пользователями."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 046ce7af40301014746c6aef07d08d81ab4adcc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="dd486-103">Руководство по созданию образа виртуальной машины для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="dd486-103">Guide to create a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="dd486-104">Эта статья ( **шаг 2**) содержит инструкции по подготовке виртуальных жестких дисков (VHD), развертываемых в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd486-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span></span> <span data-ttu-id="dd486-105">Виртуальные жесткие диски являются основой номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-105">Your VHDs are the foundation of your SKU.</span></span> <span data-ttu-id="dd486-106">Процесс подготовки будет отличаться в зависимости от типа номера SKU (на основе Linux или Windows).</span><span class="sxs-lookup"><span data-stu-id="dd486-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="dd486-107">В этой статье рассматриваются оба сценария.</span><span class="sxs-lookup"><span data-stu-id="dd486-107">This article covers both scenarios.</span></span> <span data-ttu-id="dd486-108">Описываемую процедуру можно выполнять параллельно с [созданием учетной записи разработчика Майкрософт][link-acct-creation].</span><span class="sxs-lookup"><span data-stu-id="dd486-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="dd486-109">1. Определение предложений и номеров SKU</span><span class="sxs-lookup"><span data-stu-id="dd486-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="dd486-110">В этом разделе вы узнаете, как определять предложения и соответствующие номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-110">In this section, you learn to define the offers and their associated SKUs.</span></span>

<span data-ttu-id="dd486-111">Предложение является «родительским» по отношению ко всем номерам SKU, из которых оно состоит.</span><span class="sxs-lookup"><span data-stu-id="dd486-111">An offer is a "parent" to all of its SKUs.</span></span> <span data-ttu-id="dd486-112">Вы можете создать несколько предложений.</span><span class="sxs-lookup"><span data-stu-id="dd486-112">You can have multiple offers.</span></span> <span data-ttu-id="dd486-113">Вы сами можете решить, как структурировать свои предложения.</span><span class="sxs-lookup"><span data-stu-id="dd486-113">How you decide to structure your offers is up to you.</span></span> <span data-ttu-id="dd486-114">Когда предложение переходит к стадии промежуточного хранения, вместе с ним переводятся все связанные с ним номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="dd486-115">Тщательно продумайте идентификаторы SKU, так как они будут видимы в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="dd486-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span></span>

* <span data-ttu-id="dd486-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{пространство_имен_партнера}/{идентификатор_заказа}-{идентификатор_SKU};</span><span class="sxs-lookup"><span data-stu-id="dd486-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="dd486-117">портал предварительной версии Azure: https://portal.azure.com/#gallery/{пространство_имен_издателя}.{идентификатор_заказа}{идентификатор_SKU}.</span><span class="sxs-lookup"><span data-stu-id="dd486-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="dd486-118">Номер SKU — это коммерческое название для образа виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="dd486-118">A SKU is the commercial name for a VM image.</span></span> <span data-ttu-id="dd486-119">Образ VM содержит один диск операционной системы и от нуля до нескольких дисков данных.</span><span class="sxs-lookup"><span data-stu-id="dd486-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="dd486-120">Он представляет собой полный профиль хранения для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-120">It is essentially the complete storage profile for a virtual machine.</span></span> <span data-ttu-id="dd486-121">Для одного диска требуется один VHD.</span><span class="sxs-lookup"><span data-stu-id="dd486-121">One VHD is needed per disk.</span></span> <span data-ttu-id="dd486-122">VHD необходимо создавать даже для пустых дисков данных.</span><span class="sxs-lookup"><span data-stu-id="dd486-122">Even blank data disks require a VHD to be created.</span></span>

<span data-ttu-id="dd486-123">Вне зависимости от используемой операционной системы добавляйте минимальное количество дисков данных, необходимое для номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span></span> <span data-ttu-id="dd486-124">Ваши клиенты не смогут удалить диски, которые являлись частью образа на стадии развертывания, однако при необходимости всегда смогут добавить новые диски во время или после развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd486-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd486-125">**Не изменяйте число дисков в новой версии образа.**</span><span class="sxs-lookup"><span data-stu-id="dd486-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="dd486-126">Если в образе необходимо перенастроить диски с данными, определите новый SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-126">If you must reconfigure Data disks in the image, define a new SKU.</span></span> <span data-ttu-id="dd486-127">Публикация новой версии образа с другим числом дисков может привести к ошибке нового развертывания на основе новой версии образа в случае автоматического масштабирования, автоматического развертывания решений с помощью шаблонов ARM и других сценариев.</span><span class="sxs-lookup"><span data-stu-id="dd486-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="dd486-128">1.1. Добавление предложения</span><span class="sxs-lookup"><span data-stu-id="dd486-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="dd486-129">Войдите на [портал публикации][link-pubportal], используя свою учетную запись продавца.</span><span class="sxs-lookup"><span data-stu-id="dd486-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="dd486-130">На портале публикации перейдите на вкладку **Виртуальные машины** .</span><span class="sxs-lookup"><span data-stu-id="dd486-130">Select the **Virtual Machines** tab of the Publishing Portal.</span></span> <span data-ttu-id="dd486-131">В поле для ввода укажите название предложения.</span><span class="sxs-lookup"><span data-stu-id="dd486-131">In the prompted entry field, enter your offer name.</span></span> <span data-ttu-id="dd486-132">Названием предложения обычно является название продукта (или службы), который вы планируете продавать в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd486-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span></span>
3. <span data-ttu-id="dd486-133">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd486-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="dd486-134">1.2. Определение номера SKU</span><span class="sxs-lookup"><span data-stu-id="dd486-134">1.2 Define a SKU</span></span>
<span data-ttu-id="dd486-135">Добавив предложение, следует определить (идентифицировать) номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-135">After you have added an offer, you need to define and identify your SKUs.</span></span> <span data-ttu-id="dd486-136">У вас может быть несколько предложений, и каждое из них может содержать несколько номеров SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="dd486-137">Когда предложение переходит к стадии промежуточного хранения, вместе с ним переводятся все связанные с ним номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="dd486-138">**Добавьте номер SKU.**</span><span class="sxs-lookup"><span data-stu-id="dd486-138">**Add a SKU.**</span></span> <span data-ttu-id="dd486-139">Для номера SKU необходим идентификатор, который используется в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="dd486-139">The SKU requires an identifier, which is used in the URL.</span></span> <span data-ttu-id="dd486-140">Идентификатор должен быть уникальным в вашем профиле публикации. При этом риск совпадения идентификаторов с другими издателями отсутствует.</span><span class="sxs-lookup"><span data-stu-id="dd486-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd486-141">Предложение и идентификатор SKU будут отображаться в URL-адресе предложения в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd486-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="dd486-142">**Добавьте сводное описание для номера SKU.**</span><span class="sxs-lookup"><span data-stu-id="dd486-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="dd486-143">Описания предназначены для клиентов, поэтому рекомендуем составить текст так, чтобы он легко читался.</span><span class="sxs-lookup"><span data-stu-id="dd486-143">Summary descriptions are visible to customers, so you should make them easily readable.</span></span> <span data-ttu-id="dd486-144">Эти сведения не должны блокироваться до стадии «Переход к промежуточному хранению».</span><span class="sxs-lookup"><span data-stu-id="dd486-144">This information does not need to be locked until the "Push to Staging" phase.</span></span> <span data-ttu-id="dd486-145">До этого момента вы сможете их редактировать.</span><span class="sxs-lookup"><span data-stu-id="dd486-145">Until then, you are free to edit it.</span></span>
3. <span data-ttu-id="dd486-146">Если вы используете номера SKU для Windows, используйте предложенные ссылки, чтобы приобрести утвержденные версии Windows Server.</span><span class="sxs-lookup"><span data-stu-id="dd486-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="dd486-147">2. Создание виртуального жесткого диска, совместимого с Azure (для Linux)</span><span class="sxs-lookup"><span data-stu-id="dd486-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="dd486-148">В следующем разделе приводятся рекомендации по созданию образа виртуальной машины Linux для Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd486-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span></span> <span data-ttu-id="dd486-149">Пошаговые инструкции см. в статье [Создание и передача виртуального жесткого диска с операционной системой Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd486-149">For a step-by-step walkthrough, refer to the following documentation: [Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="dd486-150">3. Создание виртуального жесткого диска, совместимого с Azure (на основе Windows)</span><span class="sxs-lookup"><span data-stu-id="dd486-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="dd486-151">Следующий раздел содержит шаги по созданию номера SKU на основе Windows Server для Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dd486-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-the-correct-base-vhds"></a><span data-ttu-id="dd486-152">3.1. Убедитесь, что вы используете подходящие базовые диски VHD</span><span class="sxs-lookup"><span data-stu-id="dd486-152">3.1 Ensure that you are using the correct base VHDs</span></span>
<span data-ttu-id="dd486-153">Виртуальный жесткий диск с ОС для вашего образа виртуальной машины должен быть основан на базовом образе, одобренном для Azure и содержащем Windows Server или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd486-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="dd486-154">Для начала создайте виртуальную машину из одного из следующих образов, расположенных на [портале Microsoft Azure][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="dd486-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="dd486-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2]);</span><span class="sxs-lookup"><span data-stu-id="dd486-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="dd486-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web]);</span><span class="sxs-lookup"><span data-stu-id="dd486-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="dd486-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web]).</span><span class="sxs-lookup"><span data-stu-id="dd486-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="dd486-158">Эти ссылки можно найти также на портале для публикаций на странице номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-158">These links can also be found in the Publishing Portal under the SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="dd486-159">Если вы используете текущую версию портала Azure или PowerShell, используйте образы Windows Server, опубликованные 8 сентября 2014 г. или позднее, одобренные для Azure.</span><span class="sxs-lookup"><span data-stu-id="dd486-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="dd486-160">3.2. Создайте виртуальную машину Windows</span><span class="sxs-lookup"><span data-stu-id="dd486-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="dd486-161">Используя портал Microsoft Azure, вы можете создать виртуальную машину на основе одобренного базового образа всего за несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="dd486-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="dd486-162">Ниже приведен обзор этого процесса.</span><span class="sxs-lookup"><span data-stu-id="dd486-162">The following is an overview of the process:</span></span>

1. <span data-ttu-id="dd486-163">На странице базового образа нажмите кнопку **Создать виртуальную машину**, чтобы перейти на новый [портал Microsoft Azure][link-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="dd486-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![рисунок][img-acom-1]
2. <span data-ttu-id="dd486-165">Войдите на портал, используя учетную запись Майкрософт и пароль подписки Azure, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="dd486-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span></span>
3. <span data-ttu-id="dd486-166">Следуйте инструкциям на экране, чтобы создать VM с помощью выбранного базового образа.</span><span class="sxs-lookup"><span data-stu-id="dd486-166">Follow the prompts to create a VM by using the base image you have selected.</span></span> <span data-ttu-id="dd486-167">Вам потребуется указать имя узла (компьютера), имя пользователя (зарегистрированного как администратор), а также пароль для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span></span>

    ![рисунок][img-portal-vm-create]
4. <span data-ttu-id="dd486-169">Выберите размер виртуальной машины для развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd486-169">Select the size of the VM to deploy:</span></span>

    <span data-ttu-id="dd486-170">а.</span><span class="sxs-lookup"><span data-stu-id="dd486-170">a.</span></span>    <span data-ttu-id="dd486-171">Если вы планируете локальную разработку VHD, размер не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="dd486-171">If you plan to develop the VHD on-premises, the size does not matter.</span></span> <span data-ttu-id="dd486-172">Мы рекомендуем использовать виртуальные машины небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="dd486-172">Consider using one of the smaller VMs.</span></span>

    <span data-ttu-id="dd486-173">b.</span><span class="sxs-lookup"><span data-stu-id="dd486-173">b.</span></span>    <span data-ttu-id="dd486-174">Если вы планируете разработку образа в среде Azure, лучше использовать один из рекомендуемых размеров виртуальной машины для выбранного образа.</span><span class="sxs-lookup"><span data-stu-id="dd486-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span></span>

    <span data-ttu-id="dd486-175">В.</span><span class="sxs-lookup"><span data-stu-id="dd486-175">c.</span></span>    <span data-ttu-id="dd486-176">С ценами можно ознакомиться в разделе **Рекомендуемые ценовые категории** на портале.</span><span class="sxs-lookup"><span data-stu-id="dd486-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span></span> <span data-ttu-id="dd486-177">В этом разделе можно найти три рекомендуемых размера, предоставленных издателем</span><span class="sxs-lookup"><span data-stu-id="dd486-177">It will provide the three recommended sizes provided by the publisher.</span></span> <span data-ttu-id="dd486-178">(в данном случае издателем является Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="dd486-178">(In this case, the publisher is Microsoft.)</span></span>

    ![рисунок][img-portal-vm-size]
5. <span data-ttu-id="dd486-180">Задайте свойства.</span><span class="sxs-lookup"><span data-stu-id="dd486-180">Set properties:</span></span>

    <span data-ttu-id="dd486-181">а.</span><span class="sxs-lookup"><span data-stu-id="dd486-181">a.</span></span>    <span data-ttu-id="dd486-182">Для быстроты развертывания можно оставить значения по умолчанию для свойств в разделе **Необязательная конфигурация** и **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="dd486-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="dd486-183">b.</span><span class="sxs-lookup"><span data-stu-id="dd486-183">b.</span></span>    <span data-ttu-id="dd486-184">Если нужно, в разделе **Учетная запись хранения**можно выбрать учетную запись хранения, в которой будет храниться VHD с операционной системой.</span><span class="sxs-lookup"><span data-stu-id="dd486-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span></span>

    <span data-ttu-id="dd486-185">c.</span><span class="sxs-lookup"><span data-stu-id="dd486-185">c.</span></span>    <span data-ttu-id="dd486-186">Если нужно, в разделе **Группа ресурсов**можно выбрать логическую группу, в которой будет размещена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="dd486-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span></span>
6. <span data-ttu-id="dd486-187">Выберите **расположение** для развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd486-187">Select the **Location** for deployment:</span></span>

    <span data-ttu-id="dd486-188">а.</span><span class="sxs-lookup"><span data-stu-id="dd486-188">a.</span></span>    <span data-ttu-id="dd486-189">Если вы планируете локальную разработку VHD, расположение не имеет значения, так как вы сможете загрузить образ в Azure позднее.</span><span class="sxs-lookup"><span data-stu-id="dd486-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span></span>

    <span data-ttu-id="dd486-190">b.</span><span class="sxs-lookup"><span data-stu-id="dd486-190">b.</span></span>    <span data-ttu-id="dd486-191">Если вы планируете разработку образа в Azure, рекомендуем с самого начала использовать один из регионов Microsoft Azure в США.</span><span class="sxs-lookup"><span data-stu-id="dd486-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span></span> <span data-ttu-id="dd486-192">Это позволит ускорить копирование VHD, которое выполняет корпорация Майкрософт от вашего имени при отправке образа для сертификации.</span><span class="sxs-lookup"><span data-stu-id="dd486-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![рисунок][img-portal-vm-location]
7. <span data-ttu-id="dd486-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd486-194">Click **Create**.</span></span> <span data-ttu-id="dd486-195">Начнется развертывание виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-195">The VM starts to deploy.</span></span> <span data-ttu-id="dd486-196">Всего через несколько минут у вас появится успешно развернутая виртуальная машина и вы сможете начать создание образа для номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-the-cloud"></a><span data-ttu-id="dd486-197">3.3. Разработка VHD в облаке</span><span class="sxs-lookup"><span data-stu-id="dd486-197">3.3 Develop your VHD in the cloud</span></span>
<span data-ttu-id="dd486-198">Мы настоятельно рекомендуем разрабатывать VHD в облаке, используя протокол удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="dd486-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="dd486-199">Подключение к удаленному рабочему столу будет осуществляться по протоколу RDP с именем пользователя и паролем, указанным при подготовке.</span><span class="sxs-lookup"><span data-stu-id="dd486-199">You connect to RDP with the user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd486-200">В случае локальной разработки виртуального жесткого диска (мы не рекомендуем) см. статью [Локальная разработка образа виртуальной машины для Azure Marketplace](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="dd486-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="dd486-201">Загрузка VHD при разработке в облаке не является обязательной.</span><span class="sxs-lookup"><span data-stu-id="dd486-201">Downloading your VHD is not necessary if you are developing in the cloud.</span></span>
>
>

<span data-ttu-id="dd486-202">**Подключение по протоколу RDP через [портал Microsoft Azure][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="dd486-202">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="dd486-203">Выберите **Обзор** > **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="dd486-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="dd486-204">Откроется колонка «Виртуальные машины».</span><span class="sxs-lookup"><span data-stu-id="dd486-204">The Virtual machines blade opens.</span></span> <span data-ttu-id="dd486-205">Убедитесь, что виртуальная машина, к которой вы хотите подключиться, запущена, и выберите ее из списка развернутых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dd486-205">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span></span>
3. <span data-ttu-id="dd486-206">Откроется колонка с описанием выбранной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-206">A blade opens that describes the selected VM.</span></span> <span data-ttu-id="dd486-207">Щелкните **Подключить**в верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="dd486-207">At the top, click **Connect**.</span></span>
4. <span data-ttu-id="dd486-208">Появится запрос на ввод имени пользователя и пароля, которые вы указали при подготовке.</span><span class="sxs-lookup"><span data-stu-id="dd486-208">You are prompted to enter the user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="dd486-209">**Подключение по протоколу RDP с помощью PowerShell**</span><span class="sxs-lookup"><span data-stu-id="dd486-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="dd486-210">Чтобы скачать файл удаленного рабочего стола на локальный компьютер, используйте [командлет Get-AzureRemoteDesktopFile][link-technet-2].</span><span class="sxs-lookup"><span data-stu-id="dd486-210">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="dd486-211">Чтобы использовать этот командлет, необходимо знать имя службы и имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-211">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span></span> <span data-ttu-id="dd486-212">Если вы создали виртуальную машину с помощью [портала Microsoft Azure][link-azure-portal], эти сведения можно найти в свойствах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-212">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="dd486-213">На портале Microsoft Azure выберите **Обзор** > **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="dd486-213">In the Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="dd486-214">Откроется колонка «Виртуальные машины».</span><span class="sxs-lookup"><span data-stu-id="dd486-214">The Virtual machines blade opens.</span></span> <span data-ttu-id="dd486-215">Выберите развернутую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="dd486-215">Select the VM that you deployed.</span></span>
3. <span data-ttu-id="dd486-216">Откроется колонка с описанием выбранной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-216">A blade opens that describes the selected VM.</span></span>
4. <span data-ttu-id="dd486-217">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="dd486-217">Click **Properties**.</span></span>
5. <span data-ttu-id="dd486-218">Первая часть доменного имени является именем службы.</span><span class="sxs-lookup"><span data-stu-id="dd486-218">The first portion of the domain name is the service name.</span></span> <span data-ttu-id="dd486-219">Имя узла представляет собой имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-219">The host name is the VM name.</span></span>

    ![рисунок][img-portal-vm-rdp]
6. <span data-ttu-id="dd486-221">Командлет для скачивания RDP-файла для созданной виртуальной машины на локальный компьютер администратора выглядит так:</span><span class="sxs-lookup"><span data-stu-id="dd486-221">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="dd486-222">Дополнительные сведения об RDP можно найти на сайте MSDN в статье [Подключение к виртуальной машине Azure с помощью RDP или SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd486-222">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="dd486-223">**Настройка виртуальной машины и создание номера SKU**</span><span class="sxs-lookup"><span data-stu-id="dd486-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="dd486-224">Скачав VHD с операционной системой, используйте клиент Hyper-V и настройте виртуальную машину, чтобы начать создание номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-224">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span></span> <span data-ttu-id="dd486-225">Подробные инструкции можно найти по следующей ссылке на сайт TechNet: [Установка Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd486-225">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-the-correct-vhd-size"></a><span data-ttu-id="dd486-226">3.4. Выбор правильного размера VHD</span><span class="sxs-lookup"><span data-stu-id="dd486-226">3.4 Choose the correct VHD size</span></span>
<span data-ttu-id="dd486-227">VHD с операционной системой Windows в образе виртуальной машины должен иметь фиксированный формат и размер 128 ГБ.</span><span class="sxs-lookup"><span data-stu-id="dd486-227">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="dd486-228">Если физический размер меньше 128 ГБ, VHD необходимо разбить на части.</span><span class="sxs-lookup"><span data-stu-id="dd486-228">If the physical size is less than 128 GB, the VHD should be sparse.</span></span> <span data-ttu-id="dd486-229">Предоставляемые базовые образы Windows и SQL Server уже соответствуют этим требованиям. Не меняйте формат и размер полученного виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="dd486-229">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span></span>  

<span data-ttu-id="dd486-230">Размер дисков данных может достигать 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="dd486-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="dd486-231">Выбирая размер диска, помните, что конечные пользователи не смогут изменить размер виртуальных жестких дисков в образе во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd486-231">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span></span> <span data-ttu-id="dd486-232">Виртуальные жесткие диски для дисков данных должны создаваться в фиксированном формате.</span><span class="sxs-lookup"><span data-stu-id="dd486-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="dd486-233">Тем не менее их также следует разбивать на части.</span><span class="sxs-lookup"><span data-stu-id="dd486-233">They should also be sparse.</span></span> <span data-ttu-id="dd486-234">Диски данных могут быть пустыми или содержать данные.</span><span class="sxs-lookup"><span data-stu-id="dd486-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-the-latest-windows-patches"></a><span data-ttu-id="dd486-235">3.5. Установка последних исправлений Windows</span><span class="sxs-lookup"><span data-stu-id="dd486-235">3.5 Install the latest Windows patches</span></span>
<span data-ttu-id="dd486-236">Базовые образы содержат последние исправления вплоть до даты публикации.</span><span class="sxs-lookup"><span data-stu-id="dd486-236">The base images contain the latest patches up to their published date.</span></span> <span data-ttu-id="dd486-237">Перед публикацией созданного VHD с операционной системой убедитесь, что Центр обновления Windows запущен и установлены последние критические и важные обновления безопасности.</span><span class="sxs-lookup"><span data-stu-id="dd486-237">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="dd486-238">3.6. Выполнение дополнительной настройки и задание расписания для выполнения задач по мере необходимости</span><span class="sxs-lookup"><span data-stu-id="dd486-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="dd486-239">Если необходима дополнительная настройка, попробуйте использовать запланированную задачу, которая сработает при запуске и внесет последние изменения в виртуальную машину сразу после ее развертывания.</span><span class="sxs-lookup"><span data-stu-id="dd486-239">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span></span>

* <span data-ttu-id="dd486-240">Лучше всего настроить самостоятельное удаление задачи после ее успешного выполнения.</span><span class="sxs-lookup"><span data-stu-id="dd486-240">It is a best practice to have the task delete itself upon successful execution.</span></span>
* <span data-ttu-id="dd486-241">Ни одна из конфигураций не должна использовать диски, отличные от C или D, так как это единственные два диска, наличие которых гарантировано.</span><span class="sxs-lookup"><span data-stu-id="dd486-241">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span></span> <span data-ttu-id="dd486-242">Диск C служит для размещения операционной системы, а диск D является временным локальным диском.</span><span class="sxs-lookup"><span data-stu-id="dd486-242">Drive C is the operating system disk, and drive D is the temporary local disk.</span></span>

### <a name="37-generalize-the-image"></a><span data-ttu-id="dd486-243">3.7. Подготовка образа</span><span class="sxs-lookup"><span data-stu-id="dd486-243">3.7 Generalize the image</span></span>
<span data-ttu-id="dd486-244">Все образы в Azure Marketplace должны быть доступны для повторного использования в первоначальном виде.</span><span class="sxs-lookup"><span data-stu-id="dd486-244">All images in the Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="dd486-245">Другими словами, VHD с операционной системой необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="dd486-245">In other words, the operating system VHD must be generalized:</span></span>

* <span data-ttu-id="dd486-246">Для Windows образ должен быть подготовлен таким образом, чтобы все конфигурации поддерживали команду **sysprep** .</span><span class="sxs-lookup"><span data-stu-id="dd486-246">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span></span>
* <span data-ttu-id="dd486-247">Вы можете запустить следующую команду из каталога %windir%\System32\Sysprep.</span><span class="sxs-lookup"><span data-stu-id="dd486-247">You can run the following command from the directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="dd486-248">Рекомендации по подготовке операционной системы к использованию команды sysprep приведены на шаге 1 статьи MSDN [Создание и передача виртуального жесткого диска Windows Server в Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd486-248">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="dd486-249">4. Развертывание виртуальной машины из дисков VHD</span><span class="sxs-lookup"><span data-stu-id="dd486-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="dd486-250">Передав виртуальные жесткие диски (подготовленный VHD с ОС и от нуля до нескольких VHD данных) в учетную запись хранения Azure, их можно зарегистрировать как пользовательский образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-250">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="dd486-251">Затем можно приступать к тестированию образа.</span><span class="sxs-lookup"><span data-stu-id="dd486-251">Then you can test that image.</span></span> <span data-ttu-id="dd486-252">Обратите внимание: так как VHD с ОС является подготовленным, вы не можете напрямую развертывать виртуальную машину, указав URL-адрес этого VHD.</span><span class="sxs-lookup"><span data-stu-id="dd486-252">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span></span>

<span data-ttu-id="dd486-253">Дополнительные сведения об образах виртуальных машин см. в следующих публикациях блога.</span><span class="sxs-lookup"><span data-stu-id="dd486-253">To learn more about VM images, review the following blog posts:</span></span>

* [<span data-ttu-id="dd486-254">Образ виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dd486-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="dd486-255">Способы использования PowerShell при работе с образами виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="dd486-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="dd486-256">Образы виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-the-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="dd486-257">Настройка необходимых средств, PowerShell и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd486-257">Set up the necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="dd486-258">Приступая к работе с командлетами Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd486-258">How to setup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="dd486-259">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd486-259">How to setup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="dd486-260">4.1. Создание пользовательского образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dd486-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="dd486-261">Запись виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dd486-261">Capture VM</span></span>
<span data-ttu-id="dd486-262">Рекомендации по записи виртуальной машины с помощью API, PowerShell или Azure CLI см. в следующих источниках.</span><span class="sxs-lookup"><span data-stu-id="dd486-262">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="dd486-263">API</span><span class="sxs-lookup"><span data-stu-id="dd486-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="dd486-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd486-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dd486-265">интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="dd486-266">Подготовка образа</span><span class="sxs-lookup"><span data-stu-id="dd486-266">Generalize Image</span></span>
<span data-ttu-id="dd486-267">Рекомендации по записи виртуальной машины с помощью API, PowerShell или Azure CLI см. в следующих источниках.</span><span class="sxs-lookup"><span data-stu-id="dd486-267">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="dd486-268">API</span><span class="sxs-lookup"><span data-stu-id="dd486-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="dd486-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd486-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="dd486-270">интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="dd486-271">4.2 Развертывание виртуальной машины из пользовательского образа VM</span><span class="sxs-lookup"><span data-stu-id="dd486-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="dd486-272">Чтобы развернуть виртуальную машину из пользовательского образа VM, можно использовать текущую версию [портала Azure](https://manage.windowsazure.com) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd486-272">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="dd486-273">**Развертывание виртуальной машины с помощью текущей версии портала Azure**</span><span class="sxs-lookup"><span data-stu-id="dd486-273">**Deploy a VM from the current Azure portal**</span></span>

1. <span data-ttu-id="dd486-274">Выберите **Создать** > **Среда выполнения приложений** > **Виртуальная машина** > **Из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="dd486-274">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![рисунок][img-manage-vm-new]
2. <span data-ttu-id="dd486-276">Перейдите в раздел **Мои образы**и выберите образ виртуальной машины, из которого следует выполнить развертывание виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd486-276">Go to **My images**, and then select the VM image from which to deploy a VM:</span></span>

   1. <span data-ttu-id="dd486-277">Обратите особое внимание на то, какой образ вы выбираете, так как представление **Мои образы** содержит как образы операционных систем, так и образы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dd486-277">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="dd486-278">Указанное количество дисков поможет определить тип развертываемого образа, так как большинство образов виртуальных машин будут иметь более одного диска.</span><span class="sxs-lookup"><span data-stu-id="dd486-278">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span></span> <span data-ttu-id="dd486-279">Кроме того, возможно использование образа виртуальной машины только с одним диском операционной системы. У такого образа параметр **Количество дисков** будет иметь значение 1.</span><span class="sxs-lookup"><span data-stu-id="dd486-279">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span></span>

      ![рисунок][img-manage-vm-select]
3. <span data-ttu-id="dd486-281">Следуйте инструкциям мастера создания VM и укажите имя виртуальной машины, ее размер, расположение, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dd486-281">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="dd486-282">**Развертывание виртуальной машины из PowerShell**</span><span class="sxs-lookup"><span data-stu-id="dd486-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="dd486-283">Чтобы развернуть большую виртуальную машину из только что созданного подготовленного образа VM, можно использовать следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="dd486-283">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="dd486-284">Дополнительные сведения см. в статье [Как устранить распространенные неполадки, возникающие в процессе создания виртуального жесткого диска].</span><span class="sxs-lookup"><span data-stu-id="dd486-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="dd486-285">5. Получение сертификата для образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dd486-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="dd486-286">Следующий шаг при подготовке образа виртуальной машины для Azure Marketplace — это сертификация.</span><span class="sxs-lookup"><span data-stu-id="dd486-286">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span></span>

<span data-ttu-id="dd486-287">Этот процесс включает запуск специального средства сертификации, передачу результатов проверки в контейнер Azure с вашими дисками VHD, добавление предложения, определение номера SKU и отправку образа виртуальной машины для сертификации.</span><span class="sxs-lookup"><span data-stu-id="dd486-287">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-the-certification-test-tool-for-azure-certified"></a><span data-ttu-id="dd486-288">5.1. Загрузка и запуск средства проверки сертификации Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-288">5.1 Download and run the Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="dd486-289">Средство сертификации будет работать на запущенной виртуальной машине, подготовленной на основе вашего пользовательского образа виртуальной машины. Оно позволит обеспечить совместимость образа виртуальной машины с Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dd486-289">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="dd486-290">Оно позволит обеспечить совместимость образа виртуальной машины с Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dd486-290">It will verify that the guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="dd486-291">Средство проверит соответствие рекомендациям и требованиям, предъявляемым к подготовке диска VHD, и выдаст отчет о совместимости, который нужно будет передать на портал публикации при запросе сертификации.</span><span class="sxs-lookup"><span data-stu-id="dd486-291">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="dd486-292">Средство сертификации можно использовать с виртуальными машинами Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="dd486-292">The certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="dd486-293">Оно подключается к виртуальным машинам Windows через PowerShell, а к виртуальным машинам Linux — через SSH.Net.</span><span class="sxs-lookup"><span data-stu-id="dd486-293">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="dd486-294">Сначала скачайте средство сертификации из [Центра загрузки Майкрософт][link-msft-download].</span><span class="sxs-lookup"><span data-stu-id="dd486-294">First, download the certification tool at the [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="dd486-295">Откройте средство сертификации и нажмите кнопку **Начать новый тест** .</span><span class="sxs-lookup"><span data-stu-id="dd486-295">Open the certification tool, and then click the **Start New Test** button.</span></span>
3. <span data-ttu-id="dd486-296">На экране **Сведения о проверке** введите имя для тестового запуска.</span><span class="sxs-lookup"><span data-stu-id="dd486-296">From the **Test Information** screen, enter a name for the test run.</span></span>
4. <span data-ttu-id="dd486-297">Выберите операционную систему для вашей виртуальной машины — Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="dd486-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="dd486-298">В зависимости от выбранного варианта выберите последующие параметры.</span><span class="sxs-lookup"><span data-stu-id="dd486-298">Depending on which you choose, select the subsequent options.</span></span>

### <a name="connect-the-certification-tool-to-a-linux-vm-image"></a><span data-ttu-id="dd486-299">**Подключение средства сертификации к образу виртуальной машины Linux**</span><span class="sxs-lookup"><span data-stu-id="dd486-299">**Connect the certification tool to a Linux VM image**</span></span>
1. <span data-ttu-id="dd486-300">Выберите режим проверки подлинности SSH: пароль или файл ключа.</span><span class="sxs-lookup"><span data-stu-id="dd486-300">Select the SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="dd486-301">При использовании проверки подлинности на основе пароля введите DNS-имя, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dd486-301">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="dd486-302">При использовании проверки подлинности с помощью файла ключа введите DNS-имя, имя пользователя и расположение закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="dd486-302">If using key file authentication, enter the DNS name, user name, and private key location.</span></span>

   ![Проверка пароля для образа виртуальной машины Linux][img-cert-vm-pswd-lnx]

   ![Проверка подлинности файла ключа для образа виртуальной машины Linux][img-cert-vm-key-lnx]

### <a name="connect-the-certification-tool-to-a-windows-based-vm-image"></a><span data-ttu-id="dd486-305">**Подключение средства сертификации к образу виртуальной машины Windows**</span><span class="sxs-lookup"><span data-stu-id="dd486-305">**Connect the certification tool to a Windows-based VM image**</span></span>
1. <span data-ttu-id="dd486-306">Введите полное доменное имя виртуальной машины (например, MyVMName.ClOudapp.net).</span><span class="sxs-lookup"><span data-stu-id="dd486-306">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="dd486-307">Введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dd486-307">Enter the user name and password.</span></span>

   ![Проверка пароля для образа виртуальной машины Windows][img-cert-vm-pswd-win]

<span data-ttu-id="dd486-309">Задав нужные параметры для образа виртуальной машины Linux или Windows, нажмите кнопку **Проверить подключение** , чтобы убедиться, что SSH.Net или PowerShell имеет допустимое подключение для тестирования.</span><span class="sxs-lookup"><span data-stu-id="dd486-309">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="dd486-310">Когда подключение будет установлено, нажмите кнопку **Далее** , чтобы начать проверку.</span><span class="sxs-lookup"><span data-stu-id="dd486-310">After a connection is established, select **Next** to start the test.</span></span>

<span data-ttu-id="dd486-311">После его завершения вы получите результаты («Пройден», «Не пройден» или «Предупреждение») для каждого проверяемого элемента.</span><span class="sxs-lookup"><span data-stu-id="dd486-311">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span></span>

![Тестовые случаи для образа виртуальной машины Linux][img-cert-vm-test-lnx]

![Тестовые случаи для образа виртуальной машины Windows][img-cert-vm-test-win]

<span data-ttu-id="dd486-314">Если хотя бы один из тестов не будет пройден, образ не будет сертифицирован.</span><span class="sxs-lookup"><span data-stu-id="dd486-314">If any of the tests fail, your image will not be certified.</span></span> <span data-ttu-id="dd486-315">В этом случае изучите требования и внесите необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="dd486-315">If this occurs, review the requirements and make any necessary changes.</span></span>

<span data-ttu-id="dd486-316">После автоматической проверки вам будет предложено указать дополнительные входные данные для образа виртуальной машины на экране анкеты.</span><span class="sxs-lookup"><span data-stu-id="dd486-316">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="dd486-317">Ответьте на вопросы и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dd486-317">Complete the questions, and then select **Next**.</span></span>

![Анкета средства сертификации][img-cert-vm-questionnaire]

![Анкета средства сертификации][img-cert-vm-questionnaire-2]

<span data-ttu-id="dd486-320">Заполнив анкету, можно указать дополнительные сведения, например данные для доступа по протоколу SSH для образа VM Linux, а также разъяснения для непройденных проверок.</span><span class="sxs-lookup"><span data-stu-id="dd486-320">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="dd486-321">Вы можете скачать результаты проверки и файлы журналов выполненных проверок, а также свои ответы на вопросы анкеты.</span><span class="sxs-lookup"><span data-stu-id="dd486-321">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span></span> <span data-ttu-id="dd486-322">Сохраните результаты в том же контейнере, что и диски VHD.</span><span class="sxs-lookup"><span data-stu-id="dd486-322">Save the results in the same container as your VHDs.</span></span>

![Сохранение результатов теста для сертификации][img-cert-vm-results]

### <a name="52-get-the-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="dd486-324">5.2. Получение URI подписанного URL-адреса для образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="dd486-324">5.2 Get the shared access signature URI for your VM images</span></span>
<span data-ttu-id="dd486-325">Во время публикации необходимо будет указать URI всех виртуальных жестких дисков, созданных для вашего номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-325">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span></span> <span data-ttu-id="dd486-326">Майкрософт понадобится доступ к этим дискам во время сертификации.</span><span class="sxs-lookup"><span data-stu-id="dd486-326">Microsoft needs access to these VHDs during the certification process.</span></span> <span data-ttu-id="dd486-327">Таким образом, вам потребуется создать URI подписанного URL-адреса для каждого виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="dd486-327">Therefore, you need to create a shared access signature URI for each VHD.</span></span> <span data-ttu-id="dd486-328">Этот URI необходимо ввести на вкладке **Образы** портала публикации.</span><span class="sxs-lookup"><span data-stu-id="dd486-328">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span></span>

<span data-ttu-id="dd486-329">Созданный URI подписанного URL-адреса должен соответствовать следующим требованиям.</span><span class="sxs-lookup"><span data-stu-id="dd486-329">The shared access signature URI created should adhere to the following requirements:</span></span>

* <span data-ttu-id="dd486-330">Для создания URI подписанного URL-адреса для виртуальных жестких дисков достаточно разрешений на создание списков и на чтение.</span><span class="sxs-lookup"><span data-stu-id="dd486-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="dd486-331">Не предоставляйте разрешения на запись или удаление.</span><span class="sxs-lookup"><span data-stu-id="dd486-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="dd486-332">Продолжительность предоставляемого доступа должна составлять минимум три (3) недели с момента создания URI подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="dd486-332">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span></span>
* <span data-ttu-id="dd486-333">Чтобы сохранить время в формате UTC, выберите дату начала за день до текущей даты.</span><span class="sxs-lookup"><span data-stu-id="dd486-333">To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="dd486-334">Например, если сегодня 6 октября 2014 г., выберите 05.10.2014.</span><span class="sxs-lookup"><span data-stu-id="dd486-334">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="dd486-335">Чтобы предоставить общий доступ к виртуальному жесткому диску в Azure Marketplace, URL-адрес SAS можно создать с помощью разных средств.</span><span class="sxs-lookup"><span data-stu-id="dd486-335">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="dd486-336">Рекомендуемые средства перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="dd486-336">Following are the 3 recommended tools:</span></span>

1.  <span data-ttu-id="dd486-337">Обозреватель хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="dd486-338">Обозреватель хранилищ Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="dd486-339">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="dd486-339">Azure CLI</span></span>

<span data-ttu-id="dd486-340">**Обозреватель хранилищ Azure (рекомендуется для пользователей Windows)**</span><span class="sxs-lookup"><span data-stu-id="dd486-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="dd486-341">Ниже перечислены шаги по созданию URL-адреса SAS с помощью обозревателя хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="dd486-341">Following are the steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="dd486-342">Скачайте [обозреватель хранилищ Azure версии 6 (предварительная версия 3)](https://azurestorageexplorer.codeplex.com/) на сайте CodePlex.</span><span class="sxs-lookup"><span data-stu-id="dd486-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="dd486-343">Найдите [обозреватель хранилищ Azure версии 6 (предварительная версия 3)](https://azurestorageexplorer.codeplex.com/) и нажмите кнопку **скачивания**.</span><span class="sxs-lookup"><span data-stu-id="dd486-343">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="dd486-345">Скачайте и распакуйте файл [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668), а затем установите его.</span><span class="sxs-lookup"><span data-stu-id="dd486-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="dd486-347">После установки откройте приложение.</span><span class="sxs-lookup"><span data-stu-id="dd486-347">After it is installed, open the application.</span></span>
4. <span data-ttu-id="dd486-348">Щелкните **Добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="dd486-348">Click **Add Account**.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="dd486-350">Укажите имя и ключ учетной записи хранения, а также домен конечных точек хранилища.</span><span class="sxs-lookup"><span data-stu-id="dd486-350">Specify the storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="dd486-351">Это учетная запись хранения в подписке Azure, где на портале Azure хранится виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="dd486-351">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="dd486-353">Когда обозреватель хранилищ Azure будет подключен к учетной записи хранения, в нем отобразится все содержимое, связанное с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="dd486-353">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span></span> <span data-ttu-id="dd486-354">Выберите контейнер, в который вы скопировали VHD-файл с диском операционной системы (а также диски данных, если они используются в вашем сценарии).</span><span class="sxs-lookup"><span data-stu-id="dd486-354">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="dd486-356">После выбора контейнера BLOB-объектов запустится обозреватель хранилищ Azure, в котором отобразятся файлы, содержащиеся в контейнере.</span><span class="sxs-lookup"><span data-stu-id="dd486-356">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span></span> <span data-ttu-id="dd486-357">Выберите файл образа (VHD), который необходимо отправить.</span><span class="sxs-lookup"><span data-stu-id="dd486-357">Select the image file (.vhd) that needs to be submitted.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="dd486-359">Выбрав VHD-файл в контейнере, перейдите на вкладку **Безопасность** .</span><span class="sxs-lookup"><span data-stu-id="dd486-359">After selecting the .vhd file in the container, click the **Security** tab.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="dd486-361">В диалоговом окне **Blob Container Security** (Безопасность контейнера больших двоичных объектов) на вкладке **Access Level** (Уровень доступа) оставьте значения по умолчанию и перейдите на вкладку **Shared Access Signatures** (Подписанные URL-адреса).</span><span class="sxs-lookup"><span data-stu-id="dd486-361">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="dd486-363">Выполните следующие действия, чтобы создать URI подписанного URL-адреса для VHD-образа.</span><span class="sxs-lookup"><span data-stu-id="dd486-363">Follow the steps below to generate a shared access signature URI for the .vhd image:</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="dd486-365">а.</span><span class="sxs-lookup"><span data-stu-id="dd486-365">a.</span></span> <span data-ttu-id="dd486-366">**Access permitted from** (Доступ разрешен с). Чтобы сохранить время в формате UTC, выберите дату начала за день до текущей даты.</span><span class="sxs-lookup"><span data-stu-id="dd486-366">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="dd486-367">Например, если сегодня 6 октября 2014 г., выберите 05.10.2014.</span><span class="sxs-lookup"><span data-stu-id="dd486-367">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="dd486-368">b.</span><span class="sxs-lookup"><span data-stu-id="dd486-368">b.</span></span> <span data-ttu-id="dd486-369">**Access permitted to** (Доступ разрешен до). Выберите дату, которая наступит через 3 недели после даты **Access permitted from** (Доступ разрешен с).</span><span class="sxs-lookup"><span data-stu-id="dd486-369">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span></span>

    <span data-ttu-id="dd486-370">c.</span><span class="sxs-lookup"><span data-stu-id="dd486-370">c.</span></span> <span data-ttu-id="dd486-371">**Actions permitted** (Разрешенные действия). Выберите разрешения на **создание списков** и **чтение**.</span><span class="sxs-lookup"><span data-stu-id="dd486-371">**Actions permitted:** Select the **List** and **Read** permissions.</span></span>

    <span data-ttu-id="dd486-372">d.</span><span class="sxs-lookup"><span data-stu-id="dd486-372">d.</span></span> <span data-ttu-id="dd486-373">Если VHD-файл выбран правильно, то ваш файл с расширением VHD отобразится рядом с **именем BLOB-объекта** .</span><span class="sxs-lookup"><span data-stu-id="dd486-373">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span></span>

    <span data-ttu-id="dd486-374">e.</span><span class="sxs-lookup"><span data-stu-id="dd486-374">e.</span></span> <span data-ttu-id="dd486-375">Щелкните **Создать подпись**.</span><span class="sxs-lookup"><span data-stu-id="dd486-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="dd486-376">f.</span><span class="sxs-lookup"><span data-stu-id="dd486-376">f.</span></span> <span data-ttu-id="dd486-377">Проверьте содержимое поля **Созданный URI подписанного URL-адреса для контейнера**согласно следующим условиям.</span><span class="sxs-lookup"><span data-stu-id="dd486-377">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span></span>

       - <span data-ttu-id="dd486-378">URI должен включать имя файла образа и расширение **.vhd**.</span><span class="sxs-lookup"><span data-stu-id="dd486-378">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
       - <span data-ttu-id="dd486-379">В конце подписи должны быть символы **=rl**.</span><span class="sxs-lookup"><span data-stu-id="dd486-379">At the end of the signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="dd486-380">Это показывает, что права на чтение и создание списков успешно предоставлены.</span><span class="sxs-lookup"><span data-stu-id="dd486-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="dd486-381">В середине подписи должны быть символы **sr=c**.</span><span class="sxs-lookup"><span data-stu-id="dd486-381">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="dd486-382">Это означает, что у вас есть доступ на уровне контейнера.</span><span class="sxs-lookup"><span data-stu-id="dd486-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="dd486-383">Чтобы проверить работу созданного URI подписанного URL-адреса, щелкните **Проверить в браузере**.</span><span class="sxs-lookup"><span data-stu-id="dd486-383">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="dd486-384">Должен начаться процесс загрузки.</span><span class="sxs-lookup"><span data-stu-id="dd486-384">It should start the download process.</span></span>

12. <span data-ttu-id="dd486-385">Скопируйте URI подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="dd486-385">Copy the shared access signature URI.</span></span> <span data-ttu-id="dd486-386">Этот код URI необходимо вставить на портал публикации.</span><span class="sxs-lookup"><span data-stu-id="dd486-386">This is the URI to paste into the Publishing Portal.</span></span>

13. <span data-ttu-id="dd486-387">Повторите шаги 6–10 для каждого виртуального жесткого диска в SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-387">Repeat steps 6-10 for each VHD in the SKU.</span></span>

<span data-ttu-id="dd486-388">**Обозреватель хранилищ Microsoft Azure (Windows/MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="dd486-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="dd486-389">Ниже перечислены шаги по созданию URL-адреса SAS с помощью обозревателя хранилищ Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dd486-389">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="dd486-390">Скачайте обозреватель хранилищ Microsoft Azure Storage Explorer на сайте [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="dd486-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="dd486-391">Найдите [обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/releasenotes.html) и нажмите кнопку **скачивания для Windows**.</span><span class="sxs-lookup"><span data-stu-id="dd486-391">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="dd486-393">После установки откройте приложение.</span><span class="sxs-lookup"><span data-stu-id="dd486-393">After it is installed, open the application.</span></span>

3.  <span data-ttu-id="dd486-394">Щелкните **Добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="dd486-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="dd486-395">Свяжите обозреватель хранилищ Microsoft Azure с подпиской, войдя в учетную запись.</span><span class="sxs-lookup"><span data-stu-id="dd486-395">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="dd486-397">Перейдите к учетной записи хранения и выберите контейнер.</span><span class="sxs-lookup"><span data-stu-id="dd486-397">Go to storage account and select the Container</span></span>

6.  <span data-ttu-id="dd486-398">Выберите **Get Shared Access Signature** (Получить подписанный URL-адрес),</span><span class="sxs-lookup"><span data-stu-id="dd486-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="dd486-399">щелкнув **контейнер** правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="dd486-399">by using Right Click of the **container**</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="dd486-401">Обновите время начала, время окончания срока действия и разрешения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="dd486-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="dd486-403">а.</span><span class="sxs-lookup"><span data-stu-id="dd486-403">a.</span></span>  <span data-ttu-id="dd486-404">**Start Time** (Время начала). Чтобы сохранить время в формате UTC, выберите дату начала за день до текущей даты.</span><span class="sxs-lookup"><span data-stu-id="dd486-404">**Start Time:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="dd486-405">Например, если сегодня 6 октября 2014 г., выберите 05.10.2014.</span><span class="sxs-lookup"><span data-stu-id="dd486-405">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="dd486-406">b.</span><span class="sxs-lookup"><span data-stu-id="dd486-406">b.</span></span>  <span data-ttu-id="dd486-407">**Expiry Time:** (Время окончания срока действия). Выберите дату, которая наступит через 3 недели после даты **Start Time** (Время начала).</span><span class="sxs-lookup"><span data-stu-id="dd486-407">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span></span>

    <span data-ttu-id="dd486-408">c.</span><span class="sxs-lookup"><span data-stu-id="dd486-408">c.</span></span>  <span data-ttu-id="dd486-409">**Permissions** (Разрешения). Выберите разрешения на **создание списков** и **чтение**.</span><span class="sxs-lookup"><span data-stu-id="dd486-409">**Permissions:** Select the **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="dd486-410">Скопируйте подписанный URL-адрес контейнера.</span><span class="sxs-lookup"><span data-stu-id="dd486-410">Copy Container shared access signature URI</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="dd486-412">URL-адрес SAS создается на уровне контейнера. Теперь нам нужно включить в него имя виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="dd486-412">Generated SAS URL is for container Level and now we need to add VHD name in it.</span></span>

    <span data-ttu-id="dd486-413">Формат URL-адреса SAS на уровне контейнера:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="dd486-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="dd486-414">Вставьте имя виртуального жесткого диска в URL-адрес SAS после имени контейнера, как показано ниже `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="dd486-414">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="dd486-415">Пример:</span><span class="sxs-lookup"><span data-stu-id="dd486-415">Example:</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="dd486-417">TestRGVM201631920152.vhd — это имя VHD, следовательно, URL-адрес SAS для VHD будет таким: `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="dd486-417">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="dd486-418">URI должен включать имя файла образа и расширение **.vhd**.</span><span class="sxs-lookup"><span data-stu-id="dd486-418">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
    - <span data-ttu-id="dd486-419">В середине подписи должны быть символы **sp=rl**.</span><span class="sxs-lookup"><span data-stu-id="dd486-419">In middle of the signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="dd486-420">Это показывает, что права на чтение и создание списков успешно предоставлены.</span><span class="sxs-lookup"><span data-stu-id="dd486-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="dd486-421">В середине подписи должны быть символы **sr=c**.</span><span class="sxs-lookup"><span data-stu-id="dd486-421">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="dd486-422">Это означает, что у вас есть доступ на уровне контейнера.</span><span class="sxs-lookup"><span data-stu-id="dd486-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="dd486-423">Проверьте работу созданного URI подписанного URL-адреса в браузере.</span><span class="sxs-lookup"><span data-stu-id="dd486-423">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="dd486-424">Должен начаться процесс скачивания.</span><span class="sxs-lookup"><span data-stu-id="dd486-424">It should start the download process</span></span>

10. <span data-ttu-id="dd486-425">Скопируйте URI подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="dd486-425">Copy the shared access signature URI.</span></span> <span data-ttu-id="dd486-426">Этот код URI необходимо вставить на портал публикации.</span><span class="sxs-lookup"><span data-stu-id="dd486-426">This is the URI to paste into the Publishing Portal.</span></span>

11. <span data-ttu-id="dd486-427">Повторите эти шаги для каждого виртуального жесткого диска в номере SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-427">Repeat these steps for each VHD in the SKU.</span></span>

<span data-ttu-id="dd486-428">**Azure CLI (рекомендуется для непрерывной интеграции и интеграции со сторонними решениями)**</span><span class="sxs-lookup"><span data-stu-id="dd486-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="dd486-429">Ниже перечислены шаги по созданию URL-адреса SAS с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="dd486-429">Following are the steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="dd486-430">Скачайте Microsoft Azure CLI [отсюда](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span><span class="sxs-lookup"><span data-stu-id="dd486-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="dd486-431">Также можно использовать ссылки для **[Windows](http://aka.ms/webpi-azure-cli)** и **[MAC OS](http://aka.ms/mac-azure-cli)**.</span><span class="sxs-lookup"><span data-stu-id="dd486-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="dd486-432">Установите скачанные файлы.</span><span class="sxs-lookup"><span data-stu-id="dd486-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="dd486-433">Создайте файл PowerShell, используя следующий код, а затем сохраните его в локальной переменной.</span><span class="sxs-lookup"><span data-stu-id="dd486-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="dd486-434">Обновите следующие параметры, упомянутые выше.</span><span class="sxs-lookup"><span data-stu-id="dd486-434">Update the following parameters in above</span></span>

    <span data-ttu-id="dd486-435">а.</span><span class="sxs-lookup"><span data-stu-id="dd486-435">a.</span></span> <span data-ttu-id="dd486-436">**`<StorageAccountName>`**: укажите имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="dd486-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="dd486-437">b.</span><span class="sxs-lookup"><span data-stu-id="dd486-437">b.</span></span> <span data-ttu-id="dd486-438">**`<Storage Account Key>`**: укажите ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="dd486-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="dd486-439">c.</span><span class="sxs-lookup"><span data-stu-id="dd486-439">c.</span></span> <span data-ttu-id="dd486-440">**`<Permission Start Date>`**: чтобы сохранить время в формате UTC, выберите дату начала за день до текущей даты.</span><span class="sxs-lookup"><span data-stu-id="dd486-440">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="dd486-441">Например, если сегодня 26 октября 2016 г., выберите значение 25.10.2016.</span><span class="sxs-lookup"><span data-stu-id="dd486-441">For example, if the current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="dd486-442">d.</span><span class="sxs-lookup"><span data-stu-id="dd486-442">d.</span></span> <span data-ttu-id="dd486-443">**`<Permission End Date>`**: выберите дату, которая наступит через 3 недели после даты **Start Time** (Время начала).</span><span class="sxs-lookup"><span data-stu-id="dd486-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span></span> <span data-ttu-id="dd486-444">Значение должно быть **02.11.2016**.</span><span class="sxs-lookup"><span data-stu-id="dd486-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="dd486-445">Ниже приведен пример кода после обновления нужных параметров.</span><span class="sxs-lookup"><span data-stu-id="dd486-445">Following is the example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="dd486-446">Запустите редактор Powershell от имени администратора, а затем откройте файл из шага 3.</span><span class="sxs-lookup"><span data-stu-id="dd486-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="dd486-447">Выполните скрипт. Вы получите URL-адрес SAS для доступа на уровне контейнера.</span><span class="sxs-lookup"><span data-stu-id="dd486-447">Run the script and it will provide you the SAS URL for container level access</span></span>

    <span data-ttu-id="dd486-448">Ниже представлены выходные данные подписи SAS. Скопируйте выделенную часть в блокнот.</span><span class="sxs-lookup"><span data-stu-id="dd486-448">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="dd486-450">Теперь, когда вы получили URL-адрес SAS уровня контейнера, нужно включить в него имя виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="dd486-450">Now you will get container level SAS URL and you need to add VHD name in it.</span></span>

    <span data-ttu-id="dd486-451">URL-адрес SAS уровня контейнера</span><span class="sxs-lookup"><span data-stu-id="dd486-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="dd486-452">Вставьте имя виртуального жесткого диска в URL-адрес SAS после имени контейнера, как показано ниже `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="dd486-452">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="dd486-453">Пример:</span><span class="sxs-lookup"><span data-stu-id="dd486-453">Example:</span></span>

    <span data-ttu-id="dd486-454">TestRGVM201631920152.vhd — это имя VHD, следовательно, URL-адрес SAS для VHD будет таким:</span><span class="sxs-lookup"><span data-stu-id="dd486-454">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="dd486-455">URI должен включать имя файла образа и расширение VHD.</span><span class="sxs-lookup"><span data-stu-id="dd486-455">Make sure that your image file name and ".vhd" are in the URI.</span></span>
    -   <span data-ttu-id="dd486-456">В середине подписи должны быть символы sp=rl.</span><span class="sxs-lookup"><span data-stu-id="dd486-456">In middle of the signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="dd486-457">Это показывает, что права на чтение и создание списков успешно предоставлены.</span><span class="sxs-lookup"><span data-stu-id="dd486-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="dd486-458">В середине подписи должны быть символы sr=c.</span><span class="sxs-lookup"><span data-stu-id="dd486-458">In middle of the signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="dd486-459">Это означает, что у вас есть доступ на уровне контейнера.</span><span class="sxs-lookup"><span data-stu-id="dd486-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="dd486-460">Проверьте работу созданного URI подписанного URL-адреса в браузере.</span><span class="sxs-lookup"><span data-stu-id="dd486-460">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="dd486-461">Должен начаться процесс скачивания.</span><span class="sxs-lookup"><span data-stu-id="dd486-461">It should start the download process</span></span>

9.  <span data-ttu-id="dd486-462">Скопируйте URI подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="dd486-462">Copy the shared access signature URI.</span></span> <span data-ttu-id="dd486-463">Этот код URI необходимо вставить на портал публикации.</span><span class="sxs-lookup"><span data-stu-id="dd486-463">This is the URI to paste into the Publishing Portal.</span></span>

10. <span data-ttu-id="dd486-464">Повторите эти шаги для каждого виртуального жесткого диска в номере SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-464">Repeat these steps for each VHD in the SKU.</span></span>


### <a name="53-provide-information-about-the-vm-image-and-request-certification-in-the-publishing-portal"></a><span data-ttu-id="dd486-465">5.3. Указание сведений об образе виртуальной машины и запросите сертификацию на портале публикации</span><span class="sxs-lookup"><span data-stu-id="dd486-465">5.3 Provide information about the VM image and request certification in the Publishing Portal</span></span>
<span data-ttu-id="dd486-466">Создав предложение и номер SKU, нужно ввести сведения об образе, связанные с этим номером SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-466">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span></span>

1. <span data-ttu-id="dd486-467">Перейдите на [портал публикации][link-pubportal] и выполните вход с использованием своей учетной записи продавца.</span><span class="sxs-lookup"><span data-stu-id="dd486-467">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="dd486-468">Выберите вкладку **Образы виртуальных машин** .</span><span class="sxs-lookup"><span data-stu-id="dd486-468">Select the **VM images** tab.</span></span>
3. <span data-ttu-id="dd486-469">Идентификатор вверху страницы является идентификатором предложения, а не идентификатором номера SKU.</span><span class="sxs-lookup"><span data-stu-id="dd486-469">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span></span>
4. <span data-ttu-id="dd486-470">Задайте свойства в разделе **номеров SKU** .</span><span class="sxs-lookup"><span data-stu-id="dd486-470">Fill out the properties under the **SKUs** section.</span></span>
5. <span data-ttu-id="dd486-471">В разделе **Семейство операционных систем**выберите тип операционной системы, связанный с VHD операционной системы.</span><span class="sxs-lookup"><span data-stu-id="dd486-471">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span></span>
6. <span data-ttu-id="dd486-472">В поле **Операционная система** введите описание операционной системы.</span><span class="sxs-lookup"><span data-stu-id="dd486-472">In the **Operating system** box, describe the operating system.</span></span> <span data-ttu-id="dd486-473">Рекомендуется использовать формат «Семейство ОС, тип, версия, обновления».</span><span class="sxs-lookup"><span data-stu-id="dd486-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="dd486-474">Например, Windows Server Datacenter 2014 R2.</span><span class="sxs-lookup"><span data-stu-id="dd486-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="dd486-475">Выберите до шести рекомендуемых размеров виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dd486-475">Select up to six recommended virtual machine sizes.</span></span> <span data-ttu-id="dd486-476">Эти рекомендации будут отображаться для клиентов в колонке "Ценовая категория" на портале Azure, когда они примут решение приобрести и развернуть ваш образ.</span><span class="sxs-lookup"><span data-stu-id="dd486-476">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span></span> <span data-ttu-id="dd486-477">**Это всего лишь рекомендации. Клиент может выбрать любой размер виртуальной машины, который соответствует дискам, указанным в образе.**</span><span class="sxs-lookup"><span data-stu-id="dd486-477">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span></span>
8. <span data-ttu-id="dd486-478">Введите версию.</span><span class="sxs-lookup"><span data-stu-id="dd486-478">Enter the version.</span></span> <span data-ttu-id="dd486-479">В поле «Версия» указана семантическая версия для идентификации продукта и его обновлений.</span><span class="sxs-lookup"><span data-stu-id="dd486-479">The version field encapsulates a semantic version to identify the product and its updates:</span></span>
   * <span data-ttu-id="dd486-480">Формат версии должен иметь вид X.Y.Z, где X, Y и Z являются целыми числами.</span><span class="sxs-lookup"><span data-stu-id="dd486-480">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="dd486-481">Образы в разных номерах SKU могут иметь различные основные и дополнительные версии.</span><span class="sxs-lookup"><span data-stu-id="dd486-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="dd486-482">Версии в номере SKU должны изменяться только пошагово, увеличивая версию исправления (Z из X.Y.Z).</span><span class="sxs-lookup"><span data-stu-id="dd486-482">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="dd486-483">В поле **URL-адрес VHD с ОС** введите URI подписанного URL-адреса, созданного для VHD с операционной системой.</span><span class="sxs-lookup"><span data-stu-id="dd486-483">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span></span>
10. <span data-ttu-id="dd486-484">Если с этим номером SKU связаны диски данных, выберите логический номер устройства (LUN), к которому должен подключаться этот диск при развертывании.</span><span class="sxs-lookup"><span data-stu-id="dd486-484">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span></span>
11. <span data-ttu-id="dd486-485">В поле **URL-адрес VHD LUN X** введите URI подписанного URL-адреса, созданного для первого VHD с данными.</span><span class="sxs-lookup"><span data-stu-id="dd486-485">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span></span>

    ![рисунок](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="dd486-487">Распространенные проблемы с URL-адресом SAS и способы их устранения</span><span class="sxs-lookup"><span data-stu-id="dd486-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="dd486-488">Проблема</span><span class="sxs-lookup"><span data-stu-id="dd486-488">Issue</span></span>|<span data-ttu-id="dd486-489">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="dd486-489">Failure Message</span></span>|<span data-ttu-id="dd486-490">Исправление</span><span class="sxs-lookup"><span data-stu-id="dd486-490">Fix</span></span>|<span data-ttu-id="dd486-491">Ссылка на документацию</span><span class="sxs-lookup"><span data-stu-id="dd486-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="dd486-492">Сбой при копировании образов: символ "?" не найден в URL-адресе SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="dd486-493">Ошибка: копирование образов.</span><span class="sxs-lookup"><span data-stu-id="dd486-493">Failure: Copying Images.</span></span> <span data-ttu-id="dd486-494">Не удалось скачать BLOB-объект с помощью указанного URI SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-494">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="dd486-495">Обновите URL-адрес SAS с помощью рекомендуемых средств.</span><span class="sxs-lookup"><span data-stu-id="dd486-495">Update the SAS Url using recommended tools</span></span>|[<span data-ttu-id="dd486-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="dd486-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="dd486-497">Сбой при копировании образов: параметры st и se отсутствуют в URL-адресе SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="dd486-498">Ошибка: копирование образов.</span><span class="sxs-lookup"><span data-stu-id="dd486-498">Failure: Copying Images.</span></span> <span data-ttu-id="dd486-499">Не удалось скачать BLOB-объект с помощью указанного URI SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-499">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="dd486-500">Обновите URL-адрес SAS, указав правильные даты начала и окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="dd486-500">Update the SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="dd486-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="dd486-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="dd486-502">Сбой при копировании образов: параметр sp=rl отсутствует в URL-адресе SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="dd486-503">Ошибка: копирование образов.</span><span class="sxs-lookup"><span data-stu-id="dd486-503">Failure: Copying Images.</span></span> <span data-ttu-id="dd486-504">Не удалось скачать BLOB-объект с помощью указанного URI SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-504">Not able to download blob using provided SAS Uri</span></span>|<span data-ttu-id="dd486-505">Обновите URL-адрес SAS, указав разрешения на чтение и создание списка.</span><span class="sxs-lookup"><span data-stu-id="dd486-505">Update the SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="dd486-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="dd486-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="dd486-507">Сбой при копировании образов: URL-адрес SAS в имени VHD-файла содержит пробелы.</span><span class="sxs-lookup"><span data-stu-id="dd486-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="dd486-508">Ошибка: копирование образов.</span><span class="sxs-lookup"><span data-stu-id="dd486-508">Failure: Copying Images.</span></span> <span data-ttu-id="dd486-509">Не удалось скачать BLOB-объект с помощью указанного URI SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-509">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="dd486-510">Обновите URL-адрес, удалив пробелы.</span><span class="sxs-lookup"><span data-stu-id="dd486-510">Update the SAS Url without white spaces</span></span>|[<span data-ttu-id="dd486-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="dd486-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="dd486-512">Сбой при копировании образов: ошибка авторизации URL-адреса SAS.</span><span class="sxs-lookup"><span data-stu-id="dd486-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="dd486-513">Ошибка: копирование образов.</span><span class="sxs-lookup"><span data-stu-id="dd486-513">Failure: Copying Images.</span></span> <span data-ttu-id="dd486-514">Не удалось скачать BLOB-объект из-за ошибки авторизации.</span><span class="sxs-lookup"><span data-stu-id="dd486-514">Not able to download blob due to authorization error</span></span>|<span data-ttu-id="dd486-515">Создайте URL-адрес SAS повторно.</span><span class="sxs-lookup"><span data-stu-id="dd486-515">Regenerate the SAS Url</span></span>|[<span data-ttu-id="dd486-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="dd486-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="dd486-517">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd486-517">Next step</span></span>
<span data-ttu-id="dd486-518">Закончив с настройкой данных SKU, перейдите к статье [Завершение создания предложения с маркетинговыми материалами][link-pushstaging].</span><span class="sxs-lookup"><span data-stu-id="dd486-518">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="dd486-519">На этом шаге публикации следует указать маркетинговые сведения, цены и другую информацию, которую необходимо предоставить до **тестирования предложения виртуальной машины в промежуточной среде (шаг 3 )**. На этом шаге вы можете протестировать предложение виртуальной машины при различных сценариях использования, прежде чем развертывать его в Azure Marketplace для общего доступа и приобретения.</span><span class="sxs-lookup"><span data-stu-id="dd486-519">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="dd486-520">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="dd486-520">See also</span></span>
* [<span data-ttu-id="dd486-521">Приступая к работе: как опубликовать предложение в Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="dd486-521">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
