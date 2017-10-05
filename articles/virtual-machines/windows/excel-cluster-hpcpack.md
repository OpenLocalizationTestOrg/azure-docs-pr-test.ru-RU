---
title: "Кластер пакета HPC для Excel и SOA | Документация Майкрософт"
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
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="2e2f1-103">Приступая к работе с рабочими нагрузками Excel и SOA в кластере пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="2e2f1-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="2e2f1-104">В этой статье показано, как развернуть кластер пакета Microsoft HPC 2012 R2 на виртуальных машинах Azure с помощью шаблона быстрого запуска Azure или сценария развертывания Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="2e2f1-105">В кластере используются образы виртуальных машин из Azure Marketplace, разработанные для выполнения рабочих нагрузок Microsoft Excel или сервисноориентированной архитектуры (SOA) с помощью пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="2e2f1-106">Кластер можно использовать для запуска служб HPC Excel и SOA на локальном клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="2e2f1-107">Службы Excel HPC включают функцию разгрузки книг и пользовательские функции Excel (или UDF).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2e2f1-108">В этой статье используются функции, шаблоны и сценарии для пакета HPC 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="2e2f1-109">Этот сценарий пока не поддерживается для пакета HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="2e2f1-110">На приведенной ниже схеме в общем показан создаваемый кластер пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Кластер HPC с узлами, выполняющими рабочие нагрузки Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="2e2f1-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2e2f1-112">Prerequisites</span></span>
* <span data-ttu-id="2e2f1-113">**Клиентский компьютер.** Необходим клиентский компьютер на основе Windows для отправки примеров заданий Excel и SOA в кластер.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="2e2f1-114">Кроме того, нужен компьютер Windows для выполнения сценария развертывания кластера Azure PowerShell (если выбран этот метод развертывания).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="2e2f1-115">**Подписка Azure.** Если ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="2e2f1-116">**Квота ядер.** Возможно, вам потребуется увеличить квоту на число ядер, особенно при развертывании нескольких узлов кластера с многоядерными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="2e2f1-117">Если вы используете шаблон быстрого запуска Azure, то квота ядер в Resource Manager выделяется на регион Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="2e2f1-118">В этом случае может потребоваться увеличить квоту в определенном регионе.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="2e2f1-119">Ознакомьтесь со статьей [Пределы, квоты и ограничения подписок на Azure](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="2e2f1-120">Чтобы увеличить квоту, бесплатно [отправьте запрос в службу поддержки](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) .</span><span class="sxs-lookup"><span data-stu-id="2e2f1-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="2e2f1-121">**Лицензия Microsoft Office.** В случае развертывания вычислительных узлов с помощью образа виртуальной машины пакета HPC 2012 R2 с Microsoft Excel из Marketplace будет установлена 30-дневная ознакомительная версия Microsoft Excel профессиональный плюс 2013.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="2e2f1-122">После завершения ознакомительного периода необходимо будет предоставить действительную лицензию Microsoft Office, чтобы активировать Excel и продолжить выполнение рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="2e2f1-123">Ознакомьтесь с разделом [Активация Excel](#excel-activation) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="2e2f1-124">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-124">Step 1.</span></span> <span data-ttu-id="2e2f1-125">Настройка кластера пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="2e2f1-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="2e2f1-126">Мы покажем вам два варианта настройки кластера пакета HPC 2012 R2: во-первых, с помощью шаблона быстрого запуска Azure и портала Azure, а во-вторых, с помощью сценария развертывания Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="2e2f1-127">Вариант 1.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-127">Option 1.</span></span> <span data-ttu-id="2e2f1-128">Использование шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="2e2f1-128">Use a quickstart template</span></span>
<span data-ttu-id="2e2f1-129">Шаблон быстрого запуска Azure позволяет быстро развернуть кластер пакета HPC на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="2e2f1-130">Открыв шаблон на портале, вы увидите простой пользовательский интерфейс, где вводятся параметры кластера.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="2e2f1-131">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="2e2f1-132">При необходимости используйте [шаблон Azure Markeplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) , который создает аналогичный кластер специально для рабочих нагрузок Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="2e2f1-133">Действия немного отличаются от следующих.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="2e2f1-134">Посетите [страницу шаблона создания кластера HPC на сайте GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="2e2f1-135">При необходимости просмотрите сведения о шаблоне и исходном коде.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="2e2f1-136">Щелкните **Развернуть в Azure** , чтобы начать развертывание шаблона на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Развертывание шаблона в Azure][github]
3. <span data-ttu-id="2e2f1-138">Выполните на портале следующие действия, чтобы ввести параметры шаблона кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="2e2f1-139">а.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-139">a.</span></span> <span data-ttu-id="2e2f1-140">На странице **Параметры** введите или измените значения параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="2e2f1-141">(щелкнув значок рядом с любым параметром, можно получить справочные сведения). Примеры значений показаны на следующем экране.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="2e2f1-142">Этот пример создает кластер *hpc01* в домене *hpc.local*, состоящий из головного узла и 2 вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="2e2f1-143">Вычислительные узлы создаются из образа виртуальной машины пакета HPC, включающего в себя Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Ввод параметров][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="2e2f1-145">Виртуальная машина головного узла создается автоматически из [последней версии образа Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) на основе пакета HPC 2012 R2 и Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="2e2f1-146">В настоящий момент образ основан на пакете HPC 2012 R2 с обновлением 3.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="2e2f1-147">Вычислительные узлы создаются из последней версии образа выбранного семейства вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="2e2f1-148">Выберите параметр **ComputeNodeWithExcel** для последней версии образа вычислительного узла пакета HPC, который включает ознакомительную версию Microsoft Excel профессиональный плюс 2013.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="2e2f1-149">Чтобы развернуть кластер для общих сеансов SOA или разгрузки определяемых пользователем функций Excel, выберите параметр **ComputeNode** (без установленного приложения Excel).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="2e2f1-150">b.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-150">b.</span></span> <span data-ttu-id="2e2f1-151">Выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="2e2f1-152">c.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-152">c.</span></span> <span data-ttu-id="2e2f1-153">Создайте группу ресурсов для кластера, например *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="2e2f1-154">d.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-154">d.</span></span> <span data-ttu-id="2e2f1-155">Выберите расположение группы ресурсов, например Центральная часть США.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="2e2f1-156">д.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-156">e.</span></span> <span data-ttu-id="2e2f1-157">Просмотрите условия на странице **Условия использования** .</span><span class="sxs-lookup"><span data-stu-id="2e2f1-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="2e2f1-158">Если вы согласны с ними, щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="2e2f1-159">Завершив настройку значений для шаблона, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="2e2f1-160">По завершении развертывания (как правило, это занимает около 30 минут) экспортируйте файл сертификата кластера с головного узла.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="2e2f1-161">На последующем шаге этот общедоступный сертификат будет импортирован на клиентский компьютер. Это обеспечит аутентификацию на стороне сервера для безопасной привязки HTTP.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="2e2f1-162">а.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-162">a.</span></span> <span data-ttu-id="2e2f1-163">Чтобы подключиться с помощью удаленного рабочего стола, на портале Azure перейдите к панели мониторинга, выберите головной узел и щелкните **Подключиться** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="2e2f1-164">b.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-164">b.</span></span> <span data-ttu-id="2e2f1-165">Используйте стандартные процедуры для экспорта сертификата головного узла (расположенного в папке Cert:\LocalMachine\My) без закрытого ключа с помощью диспетчера сертификатов.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="2e2f1-166">В этом примере экспортируйте *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Экспорт сертификата][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="2e2f1-168">Вариант 2.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-168">Option 2.</span></span> <span data-ttu-id="2e2f1-169">Использование сценария развертывания IaaS пакета HPC</span><span class="sxs-lookup"><span data-stu-id="2e2f1-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="2e2f1-170">Сценарий развертывания IaaS пакета HPC обеспечивает еще один способ гибкого развертывания кластера пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="2e2f1-171">Он создает кластер в классической модели развертывания, тогда как в шаблоне используется модель развертывания диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2e2f1-172">Кроме того, сценарий совместим с подпиской на службу Azure Global или Azure China.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="2e2f1-173">**Дополнительные требования**</span><span class="sxs-lookup"><span data-stu-id="2e2f1-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="2e2f1-174">**Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="2e2f1-175">**Сценарий развертывания IaaS из пакета HPC** — скачайте и распакуйте последнюю версию сценария из [Центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="2e2f1-176">Проверьте версию сценария, запустив `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="2e2f1-177">Эта статья основана на сценарии версии 4.5.0 или выше.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="2e2f1-178">**Создание файла конфигурации**</span><span class="sxs-lookup"><span data-stu-id="2e2f1-178">**Create the configuration file**</span></span>

 <span data-ttu-id="2e2f1-179">Сценарий развертывания IaaS из пакета HPC использует входной XML-файл конфигурации, описывающий инфраструктуру кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="2e2f1-180">Чтобы развернуть кластер, состоящий из головного узла и 18 вычислительных узлов, созданных из образа вычислительного узла, который включает Microsoft Excel, вставьте значения для вашей среды в следующий образец файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="2e2f1-181">Дополнительные сведения о файле конфигурации см. в файле Manual.rtf в папке сценария или статье [Создание кластера HPC с помощью сценария развертывания IaaS пакета HPC](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="2e2f1-182">**Примечания по файлу конфигурации**</span><span class="sxs-lookup"><span data-stu-id="2e2f1-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="2e2f1-183">Параметр **VMName** головного узла **ДОЛЖЕН** точно совпадать с параметром **ServiceName**, иначе запуск задания SOA завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="2e2f1-184">Обязательно укажите параметр **EnableWebPortal** , чтобы сертификат головного узла был создан и экспортирован.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="2e2f1-185">В этом файле указывается сценарий PostConfig.ps1, выполняемый на головном узле после настройки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="2e2f1-186">Приведенный ниже пример сценария настраивает строки подключения к службе хранилища Azure, удаляет роль вычислительного узла с головного узла и подключает все узлы к сети после развертывания.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
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

<span data-ttu-id="2e2f1-187">**Запуск сценария**</span><span class="sxs-lookup"><span data-stu-id="2e2f1-187">**Run the script**</span></span>

1. <span data-ttu-id="2e2f1-188">Откройте консоль PowerShell на клиентском компьютере от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="2e2f1-189">Измените каталог на папку сценария (E:\IaaSClusterScript в этом примере).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="2e2f1-190">Выполните следующую команду, чтобы развернуть кластер пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="2e2f1-191">В этом примере предполагается, что путь к файлу конфигурации — E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="2e2f1-192">Для выполнения сценария развертывания пакета HPC потребуется некоторое время.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="2e2f1-193">Одна из функций сценария — экспорт и скачивание сертификата кластера и его сохранение в папке документов текущего пользователя на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="2e2f1-194">Сценарий создаст сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="2e2f1-195">На следующем шаге вы импортируете сертификат в соответствующее хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="2e2f1-196">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-196">Step 2.</span></span> <span data-ttu-id="2e2f1-197">Разгрузка книг Excel и выполнение пользовательских функций из локального клиента</span><span class="sxs-lookup"><span data-stu-id="2e2f1-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="2e2f1-198">Активация Excel</span><span class="sxs-lookup"><span data-stu-id="2e2f1-198">Excel activation</span></span>
<span data-ttu-id="2e2f1-199">При использовании образа виртуальной машины ComputeNodeWithExcel для рабочих нагрузок в рабочей среде потребуется указать действительный лицензионный ключ Microsoft Office, чтобы активировать Excel на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="2e2f1-200">В противном случае срок действия ознакомительной версии Excel истечет через 30 дней, после чего выполнение книг Excel будет завершаться ошибкой COMExeption (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="2e2f1-201">Вы можете вернуться к исходному состоянию активации 30-дневной ознакомительной версии Excel. Для этого войдите на головной узел и выполните clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` во всех вычислительных узлах Excel через диспетчер кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="2e2f1-202">Возвращаться к исходному состоянию активации можно не более двух раз.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="2e2f1-203">После этого необходимо будет указать действительный лицензионный ключ Office.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="2e2f1-204">В образе виртуальной машины установлен корпоративный выпуск Office профессиональный плюс 2013 с универсальным ключом многократной установки (GVLK).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="2e2f1-205">Вы можете активировать его, воспользовавшись службой управления ключами (KMS), активацией с помощью Active Directory (AD-BA) или ключом многократной активации (MAK).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="2e2f1-206">Чтобы воспользоваться службой управления ключами (KMS) или активацией с помощью Active Directory, используйте существующий сервер службы KMS или настройте новый с помощью корпоративного пакета лицензий Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="2e2f1-207">При необходимости настройте сервер на головном узле. Затем активируйте ключ узла KMS через Интернет или по телефону.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="2e2f1-208">Затем выполните команду clusrun с файлом `ospp.vbs` для указания сервера и порта службы KMS и активации Office на всех вычислительных узлах Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="2e2f1-209">Для использования MAK сначала выполните команду clusrun с файлом `ospp.vbs` для ввода ключа, а затем активируйте все вычислительные узлы Excel через Интернет или по телефону.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="2e2f1-210">Розничные ключи продукта для Office профессиональный плюс 2013 невозможно использовать с этим образом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="2e2f1-211">Если у вас имеются действительные ключи и установочный носитель для выпусков Office или Excel, отличных от этого корпоративного выпуска Office профессиональный плюс 2013, то вы можете использовать имеющиеся выпуски.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="2e2f1-212">Сначала удалите данный корпоративный выпуск, после чего установите имеющийся выпуск.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="2e2f1-213">Повторно установленный вычислительный узел Excel можно захватывать в качестве настраиваемого образа виртуальной машины и использовать при развертывании в масштабе.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="2e2f1-214">Разгрузка книг Excel</span><span class="sxs-lookup"><span data-stu-id="2e2f1-214">Offload Excel workbooks</span></span>
<span data-ttu-id="2e2f1-215">Выполните следующие действия, чтобы выгрузить книгу Excel для выполнения в кластере пакета HPC в Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="2e2f1-216">Для этого на клиентском компьютере уже должен быть установлен Excel 2010 или 2013.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="2e2f1-217">Используйте один из вариантов шага 1 для развертывания образа вычислительного узла кластера пакета HPC с Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="2e2f1-218">Получите файл сертификата кластера (.cer), а также имя пользователя и пароль для кластера.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="2e2f1-219">На клиентском компьютере импортируйте сертификат кластера в папку Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="2e2f1-220">Убедитесь, что установлен Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-220">Make sure Excel is installed.</span></span> <span data-ttu-id="2e2f1-221">Создайте файл Excel.exe.config со следующим содержимым в одной папке с файлом Excel.exe на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="2e2f1-222">Это гарантирует успешную загрузку надстройки COM пакета HPC 2012 R2 для Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="2e2f1-223">Настройте клиент для отправки заданий в кластер пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="2e2f1-224">Один из вариантов — скачать полный установщик [пакета HPC 2012 R2 с обновлением 3](http://www.microsoft.com/download/details.aspx?id=49922) и установить клиент пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="2e2f1-225">Либо скачайте и установите [клиентские служебные программы пакета HPC 2012 R2 с обновлением 3](https://www.microsoft.com/download/details.aspx?id=49923) и соответствующий распространяемый компонент Visual C++ 2010 для своего компьютера (версию [x64](http://www.microsoft.com/download/details.aspx?id=14632) или [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="2e2f1-226">В этом примере мы используем пример книги Excel — ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="2e2f1-227">Его можно скачать [здесь](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="2e2f1-228">Скопируйте книгу Excel в рабочую папку, например D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="2e2f1-229">Откройте книгу Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-229">Open the Excel workbook.</span></span> <span data-ttu-id="2e2f1-230">На вкладке ленты **Разработка** щелкните **Надстройки COM** и убедитесь, что надстройка COM пакета HPC для Excel успешно загружена.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Надстройка Excel для пакета HPC][addin]
8. <span data-ttu-id="2e2f1-232">Отредактируйте макрос VBA HPCControlMacros в Excel, изменив закомментированные строки, как показано в следующем сценарии.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="2e2f1-233">Подставьте соответствующие значения для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="2e2f1-235">Скопируйте книгу Excel в каталог для передаваемых файлов, например D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="2e2f1-236">Этот каталог задается в константе HPC_DependsFiles в макросе VBA.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="2e2f1-237">Нажмите кнопку **Кластер** на листе, чтобы запустить книгу в кластере в Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="2e2f1-238">Выполнение пользовательских функций Excel</span><span class="sxs-lookup"><span data-stu-id="2e2f1-238">Run Excel UDFs</span></span>
<span data-ttu-id="2e2f1-239">Для выполнения пользовательских функций Excel выполните предыдущие этапы 1–3, чтобы настроить клиентский компьютер.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="2e2f1-240">Для использования определяемых пользователем функций Excel не нужно устанавливать приложение Excel на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="2e2f1-241">То есть при создании вычислительных узлов кластера можно выбрать обычный образ вычислительного узла, а не образ вычислительного узла с Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="2e2f1-242">В диалоговом окне соединителя кластера Excel 2010 и 2013 действует ограничение в 34 знака.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="2e2f1-243">Используйте это диалоговое окно, чтобы указать кластер, который выполняет определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="2e2f1-244">Если полное имя кластера имеет большую длину (например, hpcexcelhn01.southeastasia.cloudapp.azure.com), то оно не поместится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="2e2f1-245">Чтобы обойти эту проблему, задайте переменную уровня компьютера, например *CCP_IAASHN*, и присвойте ей значение полного имени кластера.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="2e2f1-246">Затем в диалоговом окне в поле имени головного узла кластера введите *%CCP_IAASHN%*.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="2e2f1-247">После успешного развертывания кластера выполните следующие действия, чтобы запустить встроенные образцы пользовательских функций Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="2e2f1-248">Для собственных пользовательских функций Excel см. эти [ресурсы](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx), чтобы создать XLL-файлы и развернуть их в кластере IaaS.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="2e2f1-249">Откройте новую книгу Excel.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-249">Open a new Excel workbook.</span></span> <span data-ttu-id="2e2f1-250">На вкладке ленты **Разработка** щелкните **Надстройки**.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="2e2f1-251">Затем в диалоговом окне нажмите кнопку **Обзор**, перейдите в папку %CCP_HOME%Bin\XLL32 и выберите пример ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="2e2f1-252">Если ClusterUDF32.xll не существует на клиентском компьютере, то скопируйте его из папки %CCP_HOME%Bin\XLL32 на головном узле.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![Выбор пользовательской функции][udf]
2. <span data-ttu-id="2e2f1-254">Щелкните **Файл** > **Параметры** > **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="2e2f1-255">В разделе **Формулы** установите флажок **Allow user-defined XLL functions to run a compute cluster** (Разрешить использование вычислительных кластеров для расчета определяемых пользователем функций XLL).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="2e2f1-256">Затем щелкните **Параметры** и введите полное имя кластера в поле **Cluster head node name** (Имя головного узла кластера).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="2e2f1-257">(Как упоминалось ранее, длина этого поля ограничена 34 символами, поэтому длинное имя кластера может не поместиться.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="2e2f1-258">Здесь для длинного имени кластера можно использовать переменную уровня компьютера.)</span><span class="sxs-lookup"><span data-stu-id="2e2f1-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Настройка пользовательской функции][options]
3. <span data-ttu-id="2e2f1-260">Щелкните ячейку со значением ==XllGetComputerNameC() и нажмите клавишу ВВОД, чтобы выполнить вычисление определяемой пользователем функции в кластере.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="2e2f1-261">Функция просто получает имя вычислительного узла, на котором выполняется определяемая пользователем функция.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="2e2f1-262">При первом выполнении в диалоговом окне учетных данных будет предложено ввести имя пользователя и пароль для подключения к кластеру IaaS.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![Запуск пользовательской функции][run]
   
   <span data-ttu-id="2e2f1-264">Если требуется вычислить много ячеек, нажмите клавиши Alt + Shift + Ctrl + F9, чтобы вычислить все ячейки.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="2e2f1-265">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-265">Step 3.</span></span> <span data-ttu-id="2e2f1-266">Запуск рабочей нагрузки SOA из локального клиента</span><span class="sxs-lookup"><span data-stu-id="2e2f1-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="2e2f1-267">Чтобы выполнять универсальные приложения SOA в кластере IaaS пакета HPC, сначала используйте один из методов шага 1, чтобы развернуть этот кластер.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="2e2f1-268">В этом случае укажите универсальный образ вычислительного узла, так как наличие Excel на вычислительных узлах не требуется.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="2e2f1-269">Затем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-269">Then follow these steps.</span></span>

1. <span data-ttu-id="2e2f1-270">После получения сертификата кластера импортируйте его на клиентский компьютер в папку Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="2e2f1-271">Установите [пакет SDK для пакета HPC 2012 R2 с обновлением 3](http://www.microsoft.com/download/details.aspx?id=49921) и [клиентские служебные программы пакета HPC 2012 R2 с обновлением 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="2e2f1-272">Эти инструменты позволяют разрабатывать и выполнять клиентские приложения SOA.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="2e2f1-273">Скачайте [пример кода](https://www.microsoft.com/download/details.aspx?id=41633)HelloWorldR2.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="2e2f1-274">Откройте файл HelloWorldR2.sln в Visual Studio 2010 или 2012.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="2e2f1-275">(В настоящее время этот пример несовместим с более поздними версиями Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="2e2f1-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="2e2f1-276">Сначала выполните сборку проекта EchoService.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-276">Build the EchoService project first.</span></span> <span data-ttu-id="2e2f1-277">Затем разверните службу в кластере IaaS так же, как и в локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="2e2f1-278">Подробные указания см. в файле Readme.doc примера HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="2e2f1-279">Измените HelloWorldR2 и другие проекты, после чего выполните их сборку, как описано в следующем разделе, чтобы создать клиентские приложения SOA, выполняемые в кластере IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="2e2f1-280">Использование привязки HTTP с очередью хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="2e2f1-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="2e2f1-281">Чтобы использовать привязку HTTP с очередью хранилища Azure, внесите несколько изменений в пример кода.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="2e2f1-282">Измените имя кластера.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="2e2f1-283">При необходимости используйте стандартную схему TransportScheme в SessionStartInfo или явно задайте значение Http.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="2e2f1-284">Используйте привязку по умолчанию для BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="2e2f1-285">Либо явно задайте значение basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="2e2f1-286">При необходимости задайте для флага UseAzureQueue значение true в SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="2e2f1-287">Если он не установлен, значение true будет задано по умолчанию, если имя кластера содержит суффиксы домена Azure, а параметр TransportScheme имеет значение Http.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="2e2f1-288">Использование привязки HTTP без очереди хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="2e2f1-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="2e2f1-289">Чтобы использовать привязку Http без очереди службы хранилища Azure, в SessionStartInfo явно задайте значение false для флага UseAzureQueue.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="2e2f1-290">Использование привязки NetTcp</span><span class="sxs-lookup"><span data-stu-id="2e2f1-290">Use NetTcp binding</span></span>
<span data-ttu-id="2e2f1-291">Настройка привязки NetTcp аналогична подключению к локальному кластеру.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="2e2f1-292">На виртуальной машине головного узла требуется открыть несколько конечных точек.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="2e2f1-293">Если вы использовали сценарий развертывания IaaS пакета HPC, например для создания кластера, то задайте конечные точки на портале Azure, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="2e2f1-294">Остановите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-294">Stop the VM.</span></span>
2. <span data-ttu-id="2e2f1-295">Добавьте TCP-порты 9090, 9087, 9091, 9094 для сеансов, брокера, рабочей роли брокера и служб данных, соответственно.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Настройка конечных точек][endpoint-new-portal]
3. <span data-ttu-id="2e2f1-297">Запустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-297">Start the VM.</span></span>

<span data-ttu-id="2e2f1-298">Клиентское приложение SOA не требует изменений, за исключением замены имени головного узла на полное имя кластера IaaS.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e2f1-299">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e2f1-299">Next steps</span></span>
* <span data-ttu-id="2e2f1-300">Дополнительные сведения о запуске рабочих нагрузок Excel с помощью пакета HPC см. в [этих ресурсах](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="2e2f1-301">Дополнительные сведения о развертывании служб SOA и управлении ими с помощью пакета HPC см. в статье [Управление службами SOA в пакете Microsoft HPC](https://technet.microsoft.com/library/ff919412.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
