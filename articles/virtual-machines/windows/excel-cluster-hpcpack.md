---
title: "aaaHPC пакет кластера для Excel и SOA | Документы Microsoft"
description: "Приступая к работе с крупномасштабными рабочими нагрузками Excel и SOA в кластере пакета HPC в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="66dd4-103">Приступая к работе с рабочими нагрузками Excel и SOA в кластере пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="66dd4-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="66dd4-104">В этой статье показано, как toodeploy Microsoft HPC Pack 2012 R2 кластера на виртуальных машинах Azure с использованием шаблоном краткого руководства Azure, или при необходимости развертывания сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66dd4-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="66dd4-105">Hello кластер использует toorun виртуальной Машины Azure Marketplace образов разработана Microsoft Excel или рабочих нагрузок сервисноориентированной архитектуре (SOA) с пакетом HPC.</span><span class="sxs-lookup"><span data-stu-id="66dd4-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="66dd4-106">Можно использовать toorun hello кластера HPC для Excel и служб SOA с клиентского компьютера в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="66dd4-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="66dd4-107">службы Excel HPC Hello включают разгрузки книги Excel и определяемые пользователем функции Excel или определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="66dd4-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="66dd4-108">В этой статье используются функции, шаблоны и сценарии для пакета HPC 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="66dd4-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="66dd4-109">Этот сценарий пока не поддерживается для пакета HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="66dd4-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="66dd4-110">На высоком уровне hello следующей диаграмме показан кластер HPC Pack hello создания.</span><span class="sxs-lookup"><span data-stu-id="66dd4-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Кластер HPC с узлами, выполняющими рабочие нагрузки Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="66dd4-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="66dd4-112">Prerequisites</span></span>
* <span data-ttu-id="66dd4-113">**Клиентский компьютер** -вам потребуется клиента на основе Windows компьютер toosubmit образец Excel и SOA задания toohello кластер.</span><span class="sxs-lookup"><span data-stu-id="66dd4-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="66dd4-114">Необходимо также hello toorun компьютера Windows Azure PowerShell сценария развертывания кластера (при выборе этого метода развертывания).</span><span class="sxs-lookup"><span data-stu-id="66dd4-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="66dd4-115">**Подписка Azure.** Если ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66dd4-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="66dd4-116">**Квота ядер** -может потребоваться tooincrease hello квоту ядер, особенно в том случае, если вы развертываете несколько узлов кластера с несколькими ядрами размеры виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="66dd4-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="66dd4-117">При использовании шаблона Azure краткое руководство по регионам Azure — hello квоту ядер в диспетчере ресурсов.</span><span class="sxs-lookup"><span data-stu-id="66dd4-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="66dd4-118">В этом случае может потребоваться Квота tooincrease hello в определенном регионе.</span><span class="sxs-lookup"><span data-stu-id="66dd4-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="66dd4-119">Ознакомьтесь со статьей [Пределы, квоты и ограничения подписок на Azure](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="66dd4-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="66dd4-120">квоты tooincrease [откройте запрос поддержки сети клиента](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="66dd4-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="66dd4-121">**Лицензия Microsoft Office.** В случае развертывания вычислительных узлов с помощью образа виртуальной машины пакета HPC 2012 R2 с Microsoft Excel из Marketplace будет установлена 30-дневная ознакомительная версия Microsoft Excel профессиональный плюс 2013.</span><span class="sxs-lookup"><span data-stu-id="66dd4-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="66dd4-122">После hello ознакомительного периода необходимо tooprovide допустимым Microsoft Office лицензии tooactivate Excel toocontinue toorun рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="66dd4-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="66dd4-123">Ознакомьтесь с разделом [Активация Excel](#excel-activation) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="66dd4-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="66dd4-124">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="66dd4-124">Step 1.</span></span> <span data-ttu-id="66dd4-125">Настройка кластера пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="66dd4-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="66dd4-126">Далее показано два tooset параметры кластера HPC Pack 2012 R2 hello: во-первых, с помощью шаблона Azure краткое руководство и hello портал Azure; Во-вторых, с помощью сценария развертывания Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66dd4-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="66dd4-127">Вариант 1.</span><span class="sxs-lookup"><span data-stu-id="66dd4-127">Option 1.</span></span> <span data-ttu-id="66dd4-128">Использование шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="66dd4-128">Use a quickstart template</span></span>
<span data-ttu-id="66dd4-129">Использование шаблона Azure краткое руководство tooquickly развертывание кластере HPC Pack в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="66dd4-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="66dd4-130">При открытии шаблона hello в портале hello, вы получаете простой пользовательский Интерфейс, куда вводится hello параметры для кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="66dd4-131">Ниже приведены шаги, hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="66dd4-132">При необходимости используйте [шаблон Azure Markeplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) , который создает аналогичный кластер специально для рабочих нагрузок Excel.</span><span class="sxs-lookup"><span data-stu-id="66dd4-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="66dd4-133">действия Hello немного отличаются от следующих hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="66dd4-134">Посетите hello [страницы шаблона создать кластер HPC на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="66dd4-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="66dd4-135">Если требуется, просмотрите сведения о шаблона hello и hello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="66dd4-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="66dd4-136">Нажмите кнопку **развертывание tooAzure** toostart развертывания с помощью шаблона hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="66dd4-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Развертывание шаблона tooAzure][github]
3. <span data-ttu-id="66dd4-138">На портале hello выполните эти шаги tooenter hello параметры для шаблона кластера HPC hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="66dd4-139">а.</span><span class="sxs-lookup"><span data-stu-id="66dd4-139">a.</span></span> <span data-ttu-id="66dd4-140">На hello **параметры** введите или измените значения для параметров шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="66dd4-141">(Щелкните значок Далее tooeach приветствия сведения справки.) В следующий экран приветствия будут показаны примеры значений.</span><span class="sxs-lookup"><span data-stu-id="66dd4-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="66dd4-142">В этом примере создается кластер с именем *hpc01* в hello *hpc.local* домен, состоящий из головного узла и 2 вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="66dd4-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="66dd4-143">Hello вычислительные узлы создаются из виртуальной Машины HPC Pack образ, включающий Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="66dd4-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Ввод параметров][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="66dd4-145">Hello головного узла виртуальной Машины автоматически создается на основе hello [последние образа Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC Pack 2012 R2 на Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="66dd4-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="66dd4-146">В настоящее время образ hello основан на HPC Pack 2012 R2 с обновлением 3.</span><span class="sxs-lookup"><span data-stu-id="66dd4-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="66dd4-147">ВМ вычислительных узлов создаются на основе hello последний образ hello выбран вычислительного узла семейства.</span><span class="sxs-lookup"><span data-stu-id="66dd4-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="66dd4-148">Выберите hello **ComputeNodeWithExcel** параметр для hello последнюю пакета HPC образ вычислительного узла, включающий ознакомительной версии Microsoft Excel профессиональный плюс 2013.</span><span class="sxs-lookup"><span data-stu-id="66dd4-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="66dd4-149">toodeploy кластера для общие SOA сеансов или Разгрузка Excel UDF, выберите hello **ComputeNode** параметр (без установки Excel).</span><span class="sxs-lookup"><span data-stu-id="66dd4-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="66dd4-150">b.</span><span class="sxs-lookup"><span data-stu-id="66dd4-150">b.</span></span> <span data-ttu-id="66dd4-151">Выберите подписку hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="66dd4-152">c.</span><span class="sxs-lookup"><span data-stu-id="66dd4-152">c.</span></span> <span data-ttu-id="66dd4-153">Создание группы ресурсов кластера hello, таких как *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="66dd4-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="66dd4-154">d.</span><span class="sxs-lookup"><span data-stu-id="66dd4-154">d.</span></span> <span data-ttu-id="66dd4-155">Выберите расположение для hello группы ресурсов, таких как центральной части США.</span><span class="sxs-lookup"><span data-stu-id="66dd4-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="66dd4-156">д.</span><span class="sxs-lookup"><span data-stu-id="66dd4-156">e.</span></span> <span data-ttu-id="66dd4-157">На hello **условия** Проверьте условия hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="66dd4-158">Если вы согласны с ними, щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="66dd4-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="66dd4-159">Когда вы закончите задание hello значений для параметров шаблона hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="66dd4-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="66dd4-160">После завершения развертывания hello (обычно занимает около 30 минут), экспортируйте файл сертификата hello кластера из головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="66dd4-161">В более позднем этапе вы импортируете сертификат открытого на hello tooprovide hello стороне сервера проверки подлинности клиентского компьютера для безопасной привязкой HTTP.</span><span class="sxs-lookup"><span data-stu-id="66dd4-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="66dd4-162">а.</span><span class="sxs-lookup"><span data-stu-id="66dd4-162">a.</span></span> <span data-ttu-id="66dd4-163">На hello портал Azure, перейдите toohello панели мониторинга, выберите hello головного узла и нажмите кнопку **Connect** вверху hello tooconnect страницы приветствия, с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="66dd4-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="66dd4-164">b.</span><span class="sxs-lookup"><span data-stu-id="66dd4-164">b.</span></span> <span data-ttu-id="66dd4-165">Используйте стандартные процедуры в диспетчер сертификатов tooexport hello головного узла сертификат (расположенный в Cert: \LocalMachine\My) без закрытого ключа hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="66dd4-166">В этом примере экспортируйте *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="66dd4-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Экспорт сертификата hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="66dd4-168">Вариант 2.</span><span class="sxs-lookup"><span data-stu-id="66dd4-168">Option 2.</span></span> <span data-ttu-id="66dd4-169">Использовать скрипт развертывания IaaS пакета HPC hello</span><span class="sxs-lookup"><span data-stu-id="66dd4-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="66dd4-170">Hello скрипт развертывания IaaS пакета HPC предоставляет другим универсальным способом toodeploy кластере HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="66dd4-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="66dd4-171">Он создает кластер hello классической модели развертывания, в то время как шаблон hello использует модель развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="66dd4-172">Кроме того сценарий hello совместим с подписки в hello Azure Global или Azure China службы.</span><span class="sxs-lookup"><span data-stu-id="66dd4-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="66dd4-173">**Дополнительные требования**</span><span class="sxs-lookup"><span data-stu-id="66dd4-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="66dd4-174">**Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="66dd4-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="66dd4-175">**Скрипт развертывания IaaS пакета HPC** — Загрузите и распакуйте hello последнюю версию скрипта hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="66dd4-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="66dd4-176">Проверьте версию hello hello сценария, выполнив команду `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="66dd4-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="66dd4-177">Эта статья основана на версии 4.5.0 или более поздней hello сценария.</span><span class="sxs-lookup"><span data-stu-id="66dd4-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="66dd4-178">**Создать файл конфигурации hello**</span><span class="sxs-lookup"><span data-stu-id="66dd4-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="66dd4-179">Hello скрипт развертывания IaaS пакета HPC использует файл конфигурации XML в качестве входных данных, описывающий hello инфраструктура кластера HPC hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="66dd4-180">в кластере, состоящем из головного узла и 18 вычислительные узлы, созданные на основе образ hello вычислительного узла, который включает Microsoft Excel toodeploy заменить значения для вашей среды в hello следующий образец файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="66dd4-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="66dd4-181">Дополнительные сведения о файле конфигурации hello см. в разделе файла Manual.rtf hello в папке скрипта hello и [создание кластера HPC с помощью скрипта развертывания IaaS пакета HPC hello](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66dd4-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="66dd4-182">**Примечания о файле конфигурации hello**</span><span class="sxs-lookup"><span data-stu-id="66dd4-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="66dd4-183">Hello **VMName** головного узла hello **должен** быть hello же, как hello **ServiceName**, или toorun сбой заданий SOA.</span><span class="sxs-lookup"><span data-stu-id="66dd4-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="66dd4-184">Убедитесь, что указан **EnableWebPortal** , чтобы hello головного узла сертификат создается и экспортировать.</span><span class="sxs-lookup"><span data-stu-id="66dd4-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="66dd4-185">файл Hello указывает сценарий PowerShell после конфигурации PostConfig.ps1, работающей на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="66dd4-186">Hello следующий образец скрипта настраивает hello строка подключения хранилища Azure, удаляет hello роли вычислительного узла из головного узла hello и переводит все узлы в оперативный режим, если они развернуты.</span><span class="sxs-lookup"><span data-stu-id="66dd4-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="66dd4-187">**Запустите сценарий hello**</span><span class="sxs-lookup"><span data-stu-id="66dd4-187">**Run hello script**</span></span>

1. <span data-ttu-id="66dd4-188">Откройте консоль PowerShell hello hello клиентского компьютера с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="66dd4-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="66dd4-189">Измените скрипт в папку toohello каталога (E:\IaaSClusterScript в этом примере).</span><span class="sxs-lookup"><span data-stu-id="66dd4-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="66dd4-190">hello HPC Pack toodeploy кластера, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="66dd4-191">В этом примере предполагается, что этот файл конфигурации hello находится в E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="66dd4-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="66dd4-192">сценарий развертывания пакета HPC Hello выполняется некоторое время.</span><span class="sxs-lookup"><span data-stu-id="66dd4-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="66dd4-193">Один сценарий hello самое делает — tooexport и загрузить сертификат кластера hello и сохраните его в папке "документы" hello текущего пользователя на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="66dd4-194">Hello сценарий создает сообщение аналогичные toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="66dd4-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="66dd4-195">На следующем шаге нужно импортировать сертификат hello в hello соответствующее хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="66dd4-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="66dd4-196">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="66dd4-196">Step 2.</span></span> <span data-ttu-id="66dd4-197">Разгрузка книг Excel и выполнение пользовательских функций из локального клиента</span><span class="sxs-lookup"><span data-stu-id="66dd4-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="66dd4-198">Активация Excel</span><span class="sxs-lookup"><span data-stu-id="66dd4-198">Excel activation</span></span>
<span data-ttu-id="66dd4-199">При использовании образа виртуальной Машины ComputeNodeWithExcel hello для рабочих нагрузок, необходимо tooprovide допустимым Microsoft Office лицензионного ключа tooactivate Excel на вычислительных узлах hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="66dd4-200">В противном случае hello ознакомительной версии Excel истекает через 30 дней, и запускать книги Excel будут завершаться hello COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="66dd4-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="66dd4-201">Excel может rearm еще на 30 дней оценки времени: вход toohello головного узла и clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` на все Excel вычислительных узлов через диспетчер кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="66dd4-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="66dd4-202">Возвращаться к исходному состоянию активации можно не более двух раз.</span><span class="sxs-lookup"><span data-stu-id="66dd4-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="66dd4-203">После этого необходимо будет указать действительный лицензионный ключ Office.</span><span class="sxs-lookup"><span data-stu-id="66dd4-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="66dd4-204">Hello Office профессиональный плюс 2013 установлен на hello образа виртуальной Машины представляет собой версию тома с универсальным тома лицензии ключ установки (GVLK).</span><span class="sxs-lookup"><span data-stu-id="66dd4-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="66dd4-205">Вы можете активировать его, воспользовавшись службой управления ключами (KMS), активацией с помощью Active Directory (AD-BA) или ключом многократной активации (MAK).</span><span class="sxs-lookup"><span data-stu-id="66dd4-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="66dd4-206">toouse KMS/AD-бизнес-Аналитики, использовать существующий сервер KMS, или настройте его с помощью hello пакет Microsoft Office 2013 корпоративного лицензирования.</span><span class="sxs-lookup"><span data-stu-id="66dd4-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="66dd4-207">(Если вы хотите задайте hello server на головном узле hello.) После этого активируйте ключ узла KMS hello через hello Интернет или по телефону.</span><span class="sxs-lookup"><span data-stu-id="66dd4-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="66dd4-208">Затем clusrun `ospp.vbs` tooset hello и порт сервера службы KMS и активировать Office на всех узлах вычисления Excel hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="66dd4-209">toouse MAK первый clusrun `ospp.vbs` tooinput hello ключ, а затем активировать все узлы вычислений Excel hello через hello Интернет или по телефону.</span><span class="sxs-lookup"><span data-stu-id="66dd4-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="66dd4-210">Розничные ключи продукта для Office профессиональный плюс 2013 невозможно использовать с этим образом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66dd4-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="66dd4-211">Если у вас имеются действительные ключи и установочный носитель для выпусков Office или Excel, отличных от этого корпоративного выпуска Office профессиональный плюс 2013, то вы можете использовать имеющиеся выпуски.</span><span class="sxs-lookup"><span data-stu-id="66dd4-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="66dd4-212">Сначала удалите этот том выпуск и установите hello от имеющегося выпуска.</span><span class="sxs-lookup"><span data-stu-id="66dd4-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="66dd4-213">Hello переустановлен Excel вычислительных узлов, можно захватить как настраиваемые toouse образ виртуальной Машины в развертывании в масштабе.</span><span class="sxs-lookup"><span data-stu-id="66dd4-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="66dd4-214">Разгрузка книг Excel</span><span class="sxs-lookup"><span data-stu-id="66dd4-214">Offload Excel workbooks</span></span>
<span data-ttu-id="66dd4-215">Выполните эти шаги toooffload книги Excel, чтобы он запускался на кластере HPC Pack hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="66dd4-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="66dd4-216">toodo это, необходимо иметь Excel 2010 или 2013, уже установлен на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="66dd4-217">С помощью одного из параметров hello в шаге 1 toodeploy кластере HPC Pack с hello Excel вычислений изображение узла.</span><span class="sxs-lookup"><span data-stu-id="66dd4-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="66dd4-218">Получите hello кластера файл сертификата (.cer) кластера имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="66dd4-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="66dd4-219">На клиентском компьютере hello импортируйте сертификат кластера hello в Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="66dd4-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="66dd4-220">Убедитесь, что установлен Excel.</span><span class="sxs-lookup"><span data-stu-id="66dd4-220">Make sure Excel is installed.</span></span> <span data-ttu-id="66dd4-221">Создайте файл Excel.exe.config с hello, следуя содержимое в hello же папке, что и Excel.exe на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="66dd4-222">Этот шаг гарантирует, что успешной загрузки этого hello HPC Pack 2012 R2 Excel надстройки.</span><span class="sxs-lookup"><span data-stu-id="66dd4-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="66dd4-223">Установка пакета HPC hello клиента toosubmit заданий toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="66dd4-224">Один из вариантов — полный hello toodownload [установки HPC Pack 2012 R2 с обновлением 3](http://www.microsoft.com/download/details.aspx?id=49922) и установить клиент HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="66dd4-225">Можно также загрузить и установить hello [HPC Pack 2012 R2 с обновлением 3 клиентские служебные программы](https://www.microsoft.com/download/details.aspx?id=49923) и hello соответствующие Visual C++ 2010 распространяемого пакета для компьютера ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="66dd4-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="66dd4-226">В этом примере мы используем пример книги Excel — ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="66dd4-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="66dd4-227">Его можно скачать [здесь](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="66dd4-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="66dd4-228">Скопируйте hello Excel книги tooa например D:\Excel\Run рабочей папки.</span><span class="sxs-lookup"><span data-stu-id="66dd4-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="66dd4-229">Откройте книгу Excel hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-229">Open hello Excel workbook.</span></span> <span data-ttu-id="66dd4-230">На hello **разработка** ленты, нажмите кнопку **надстройки COM** и подтвердите, hello HPC Pack Excel надстройка успешно загружается.</span><span class="sxs-lookup"><span data-stu-id="66dd4-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Надстройка Excel для пакета HPC][addin]
8. <span data-ttu-id="66dd4-232">Макрос VBA hello редактирования HPCControlMacros в Excel, изменив hello комментарии как показано в hello, выполнив сценарий.</span><span class="sxs-lookup"><span data-stu-id="66dd4-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="66dd4-233">Подставьте соответствующие значения для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="66dd4-233">Substitute appropriate values for your environment.</span></span>
   
   ![Макрос Excel для пакета HPC][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="66dd4-235">Скопируйте каталог hello Excel книги tooan передачи, например D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="66dd4-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="66dd4-236">Этот каталог задается в константа HPC_DependsFiles hello в макрос VBA hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="66dd4-237">Книга hello toorun hello кластере в Azure, щелкните hello **кластера** кнопку на листе hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="66dd4-238">Выполнение пользовательских функций Excel</span><span class="sxs-lookup"><span data-stu-id="66dd4-238">Run Excel UDFs</span></span>
<span data-ttu-id="66dd4-239">toorun UDF Excel следуйте hello предыдущих шагах 1 – 3 tooset копирование hello клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="66dd4-240">Для определяемых пользователем функций Excel не требуется на вычислительных узлах установлено приложение Excel toohave hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="66dd4-241">Поэтому при создании кластера вычислительных узлов, можно выбрать образ обычный вычислительного узла вместо hello вычислений изображение узла с помощью Excel.</span><span class="sxs-lookup"><span data-stu-id="66dd4-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="66dd4-242">Имеется 34 знаков в hello Excel 2010 и 2013 диалоговое окно соединитель кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="66dd4-243">Использовании этого диалогового окна поле toospecify hello кластера под управлением hello определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="66dd4-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="66dd4-244">Если длиннее hello полное имя кластера (например, hpcexcelhn01.southeastasia.cloudapp.azure.com), не помещается в диалоговое окно «hello».</span><span class="sxs-lookup"><span data-stu-id="66dd4-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="66dd4-245">Hello решение — tooset переменной компьютера, такие как *CCP_IAASHN* со значением hello hello кластера длинное имя.</span><span class="sxs-lookup"><span data-stu-id="66dd4-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="66dd4-246">Затем введите *% CCP_IAASHN %* в диалоговом окне приветствия как hello имя головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="66dd4-247">После успешно развернут кластер hello, выполните следующие шаги toorun hello встроенный образец определяемой пользователем функции в Excel.</span><span class="sxs-lookup"><span data-stu-id="66dd4-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="66dd4-248">Настраиваемые пользовательские функции Excel, просмотрите эти [ресурсов](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL и их развертывание в кластере IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="66dd4-249">Откройте новую книгу Excel.</span><span class="sxs-lookup"><span data-stu-id="66dd4-249">Open a new Excel workbook.</span></span> <span data-ttu-id="66dd4-250">На hello **разработка** ленты, нажмите кнопку **надстройки**. В диалоговом окне приветствия нажмите кнопку **Обзор**, перейдите в папку %CCP_HOME%Bin\XLL32 toohello и выберите образец hello ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="66dd4-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="66dd4-251">Если hello ClusterUDF32 не существует на компьютере клиента hello, скопируйте его из папки %CCP_HOME%Bin\XLL32 hello на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Выберите hello определяемой пользователем функции.][udf]
2. <span data-ttu-id="66dd4-253">Щелкните **Файл** > **Параметры** > **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="66dd4-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="66dd4-254">В разделе **формулы**, проверьте **разрешить определяемой пользователем функции toorun XLL вычислительного кластера**.</span><span class="sxs-lookup"><span data-stu-id="66dd4-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="66dd4-255">Нажмите кнопку **параметры** и введите hello полное имя кластера в **имя головного узла кластера**.</span><span class="sxs-lookup"><span data-stu-id="66dd4-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="66dd4-256">(Как отмечено выше ранее это поле является ограниченной too34 символов, так много имя_кластера может не поместиться.</span><span class="sxs-lookup"><span data-stu-id="66dd4-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="66dd4-257">Здесь для длинного имени кластера можно использовать переменную уровня компьютера.)</span><span class="sxs-lookup"><span data-stu-id="66dd4-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Настройка hello определяемой пользователем функции.][options]
3. <span data-ttu-id="66dd4-259">Щелкните ячейку hello с =XllGetComputerNameC() значение toorun hello вычисления определяемой пользователем функции в кластере hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="66dd4-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="66dd4-260">функция Hello просто получает имя hello hello вычислительных узлов, на какие hello определяемая пользователем Функция выполняется.</span><span class="sxs-lookup"><span data-stu-id="66dd4-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="66dd4-261">Диалоговое окно учетных данных для первого запуска hello, запрашивает hello имя пользователя и пароль tooconnect toohello IaaS кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Запуск пользовательской функции][run]
   
   <span data-ttu-id="66dd4-263">После многих toocalculate ячейки нажмите клавишу Alt, Shift, Ctrl + F9 toorun hello вычисления всех ячеек.</span><span class="sxs-lookup"><span data-stu-id="66dd4-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="66dd4-264">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="66dd4-264">Step 3.</span></span> <span data-ttu-id="66dd4-265">Запуск рабочей нагрузки SOA из локального клиента</span><span class="sxs-lookup"><span data-stu-id="66dd4-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="66dd4-266">Сначала toorun Общие приложения SOA в кластере IaaS пакета HPC hello, используйте один из методов hello в кластере hello toodeploy шаг 1.</span><span class="sxs-lookup"><span data-stu-id="66dd4-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="66dd4-267">В этом случае укажите образ универсального вычислительного узла, так как не требуется Excel на вычислительных узлах hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="66dd4-268">Затем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="66dd4-268">Then follow these steps.</span></span>

1. <span data-ttu-id="66dd4-269">После получения сертификата кластера hello, импортируйте его на клиентском компьютере hello в Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="66dd4-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="66dd4-270">Установка hello [HPC Pack 2012 R2 обновление 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) и [HPC Pack 2012 R2 с обновлением 3 клиентские служебные программы](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="66dd4-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="66dd4-271">Эти средства позволяют toodevelop и запустите SOA клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="66dd4-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="66dd4-272">Загрузите hello HelloWorldR2 [пример кода](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="66dd4-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="66dd4-273">Откройте hello HelloWorldR2.sln в Visual Studio 2010 или 2012.</span><span class="sxs-lookup"><span data-stu-id="66dd4-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="66dd4-274">(В настоящее время этот пример несовместим с более поздними версиями Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="66dd4-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="66dd4-275">Первая сборка проекта EchoService hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-275">Build hello EchoService project first.</span></span> <span data-ttu-id="66dd4-276">Разверните кластер IaaS toohello службы hello в hello так же, как tooan локального кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="66dd4-277">Подробные инструкции см. в разделе hello readme.doc для в HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="66dd4-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="66dd4-278">Изменение и выполнение сборки hello HellWorldR2 и в других проектах, как описано в следующий раздел toogenerate hello SOA клиентских приложений, работающих на кластере Azure IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="66dd4-279">Использование привязки HTTP с очередью хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66dd4-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="66dd4-280">Привязка Http toouse с очередь хранилища Azure внести некоторые изменения, toohello образец кода.</span><span class="sxs-lookup"><span data-stu-id="66dd4-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="66dd4-281">Обновите имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="66dd4-282">При необходимости использовать по умолчанию hello TransportScheme в SessionStartInfo или явно задать tooHttp.</span><span class="sxs-lookup"><span data-stu-id="66dd4-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="66dd4-283">Используйте привязку по умолчанию для hello BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="66dd4-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="66dd4-284">Или явно с помощью hello basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="66dd4-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="66dd4-285">При необходимости задайте tootrue флаг UseAzureQueue hello в SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="66dd4-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="66dd4-286">В противном случае набор, оно будет иметь значение tootrue по умолчанию при суффиксы доменов Azure имеет имя кластера hello и hello TransportScheme Http.</span><span class="sxs-lookup"><span data-stu-id="66dd4-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="66dd4-287">Использование привязки HTTP без очереди хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="66dd4-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="66dd4-288">Привязка Http toouse без очередь хранилища Azure, а явно набор hello UseAzureQueue флаг toofalse в hello SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="66dd4-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="66dd4-289">Использование привязки NetTcp</span><span class="sxs-lookup"><span data-stu-id="66dd4-289">Use NetTcp binding</span></span>
<span data-ttu-id="66dd4-290">toouse NetTcp hello конфигурации привязки, — примерно tooconnecting tooan локального кластера.</span><span class="sxs-lookup"><span data-stu-id="66dd4-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="66dd4-291">Необходимо tooopen несколько конечных точек на ВМ головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="66dd4-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="66dd4-292">Если используется кластер hello toocreate скрипт развертывания hello IaaS пакета HPC, например, установке конечных точек hello в hello портал Azure следующим образом.</span><span class="sxs-lookup"><span data-stu-id="66dd4-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="66dd4-293">Остановите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="66dd4-293">Stop hello VM.</span></span>
2. <span data-ttu-id="66dd4-294">Добавьте TCP-порты hello 9090, 9087, 9091, 9094 для сеанса, hello компонента Service Broker, соответственно брокера рабочего процесса и службы данных</span><span class="sxs-lookup"><span data-stu-id="66dd4-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Настройка конечных точек][endpoint-new-portal]
3. <span data-ttu-id="66dd4-296">Запустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="66dd4-296">Start hello VM.</span></span>

<span data-ttu-id="66dd4-297">Hello SOA клиентское приложение не требует изменений за исключением изменения hello головного toohello IaaS кластера полное имя.</span><span class="sxs-lookup"><span data-stu-id="66dd4-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66dd4-298">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66dd4-298">Next steps</span></span>
* <span data-ttu-id="66dd4-299">Дополнительные сведения о запуске рабочих нагрузок Excel с помощью пакета HPC см. в [этих ресурсах](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx).</span><span class="sxs-lookup"><span data-stu-id="66dd4-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="66dd4-300">Дополнительные сведения о развертывании служб SOA и управлении ими с помощью пакета HPC см. в статье [Управление службами SOA в пакете Microsoft HPC](https://technet.microsoft.com/library/ff919412.aspx).</span><span class="sxs-lookup"><span data-stu-id="66dd4-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
