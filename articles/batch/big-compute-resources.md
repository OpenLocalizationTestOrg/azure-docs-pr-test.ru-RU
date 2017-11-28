---
title: "Ресурсы для пакетных и высокопроизводительных вычислений (HPC) в облаке Azure | Документация Майкрософт"
description: "В этой статье приведены технические ресурсы, которые помогут вам выполнять крупномасштабные параллельные, пакетные и высокопроизводительные вычисления (HPC) в Azure."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="aa499-103">Большие вычисления в Azure: технические ресурсы для пакетных и высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="aa499-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="aa499-104">Это руководство по техническим ресурсам, которые помогут вам выполнять крупномасштабные параллельные, пакетные и высокопроизводительные вычисления (HPC) в Azure.</span><span class="sxs-lookup"><span data-stu-id="aa499-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="aa499-105">Перенесите свои текущие пакетные рабочие нагрузки или рабочие нагрузки HPC в облако Azure или создайте новые решения для больших вычислений с помощью набора служб Azure.</span><span class="sxs-lookup"><span data-stu-id="aa499-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="aa499-106">Варианты решений</span><span class="sxs-lookup"><span data-stu-id="aa499-106">Solutions options</span></span>
<span data-ttu-id="aa499-107">Узнайте, какие решения для больших вычислений существуют в Azure, и выберите вариант, который подходит для рабочих нагрузок и потребностей вашей организации.</span><span class="sxs-lookup"><span data-stu-id="aa499-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="aa499-108">Пакетные и высокопроизводительные вычислительные решения</span><span class="sxs-lookup"><span data-stu-id="aa499-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="aa499-109">Большие вычисления в облаке с помощью Azure и HPC (видео)</span><span class="sxs-lookup"><span data-stu-id="aa499-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="aa499-110">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="aa499-110">Azure Batch</span></span>
<span data-ttu-id="aa499-111">[Пакетная служба](https://azure.microsoft.com/services/batch/) — это платформа как услуга, которая позволяет легко переводить приложения Linux и Windows в облако и выполнять задания без настройки кластера или планировщика и управления ими.</span><span class="sxs-lookup"><span data-stu-id="aa499-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="aa499-112">С помощью пакета SDK вы можете интегрировать клиентские приложения в Пакетную службу Azure, используя различные языки, размещать данные в Azure и создавать конвейеры выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="aa499-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="aa499-113">Документация</span><span class="sxs-lookup"><span data-stu-id="aa499-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="aa499-114">Справочник по API [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) и [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa499-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="aa499-115">[библиотеке .NET для управления пакетной службой](https://msdn.microsoft.com/library/mt463120.aspx) </span><span class="sxs-lookup"><span data-stu-id="aa499-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="aa499-116">Руководcтва по началу работы с [библиотекой пакетной службы Azure для .NET](batch-dotnet-get-started.md) и [клиентом Python пакетной службы Azure](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="aa499-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="aa499-117">Форум по Пакетной службе</span><span class="sxs-lookup"><span data-stu-id="aa499-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="aa499-118">Видеоролики о Пакетной службе</span><span class="sxs-lookup"><span data-stu-id="aa499-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="aa499-119">Кластерные решения HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-119">HPC cluster solutions</span></span>
<span data-ttu-id="aa499-120">Разверните или расширьте свой существующий кластер HPC под управлением Windows или Linux в службу Azure и выполняйте ресурсоемкие вычислительные рабочие нагрузки в облаке.</span><span class="sxs-lookup"><span data-stu-id="aa499-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="aa499-121">Пакет Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="aa499-122">HPC Pack — это бесплатное решение HPC корпорации Майкрософт, созданное на основе технологий Microsoft Azure и Windows Server и поддерживающее рабочие нагрузки HPC как в Windows, так и в Linux.</span><span class="sxs-lookup"><span data-stu-id="aa499-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="aa499-123">Скачать пакет HPC 2016</span><span class="sxs-lookup"><span data-stu-id="aa499-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="aa499-124">Загрузить пакет HPC 2012 R2 с обновлением 3</span><span class="sxs-lookup"><span data-stu-id="aa499-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="aa499-125">Документация</span><span class="sxs-lookup"><span data-stu-id="aa499-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="aa499-126">Варианты кластера пакета HPC в Azure: под управлением [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) и [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="aa499-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="aa499-127">Ускорение в рабочие экземпляры Azure с помощью пакета HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="aa499-128">Ускорение в пакетную службу Azure с помощью пакета HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="aa499-129">Форумы по Windows HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="aa499-130">Кластерные решения Linux и OSS</span><span class="sxs-lookup"><span data-stu-id="aa499-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="aa499-131">Используйте эти шаблоны Azure для развертывания кластеров HPC под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="aa499-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="aa499-132">[Шаблон развертывания кластера SLURM](https://azure.microsoft.com/documentation/templates/slurm/) и [запись блога](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa499-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="aa499-133">Шаблон Spin up a Torque cluster</span><span class="sxs-lookup"><span data-stu-id="aa499-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="aa499-134">Вычисления шаблонов сетки с помощью PBS Professional</span><span class="sxs-lookup"><span data-stu-id="aa499-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="aa499-135">Хранилище HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-135">HPC storage</span></span>
* [<span data-ttu-id="aa499-136">Параллельные файловые системы для хранилища HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="aa499-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="aa499-137">Intel Cloud Edition для Lustre Software — пробная версия</span><span class="sxs-lookup"><span data-stu-id="aa499-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="aa499-138">Шаблон BeeGFS на платформе CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="aa499-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="aa499-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="aa499-139">Microsoft MPI</span></span>
<span data-ttu-id="aa499-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) — это реализация стандарта MPI (Message Passing Interface — интерфейс передачи сообщений) от Майкрософт, предназначенная для разработки и запуска параллельных приложений на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="aa499-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="aa499-141">Скачать MS-MPI</span><span class="sxs-lookup"><span data-stu-id="aa499-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="aa499-142">Справочник по MS-MPI</span><span class="sxs-lookup"><span data-stu-id="aa499-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="aa499-143">Форум по MPI</span><span class="sxs-lookup"><span data-stu-id="aa499-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="aa499-144">Экземпляры для ресурсоемких вычислений</span><span class="sxs-lookup"><span data-stu-id="aa499-144">Compute-intensive instances</span></span>
<span data-ttu-id="aa499-145">В Azure доступны [разные размеры виртуальных машин](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), включая экземпляры [для ресурсоемких вычислений серии H](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), поддерживающие подключение к внутренней сети RDMA для выполнения рабочих нагрузок HPC в Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="aa499-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="aa499-146">Настройка кластера Linux RDMA для выполнения приложений MPI</span><span class="sxs-lookup"><span data-stu-id="aa499-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="aa499-147">Настройка кластера RDMA в Windows с помощью пакета HPC для запуска приложений MPI</span><span class="sxs-lookup"><span data-stu-id="aa499-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="aa499-148">Для рабочих нагрузок, интенсивно использующих GPU, ознакомьтесь с [размерами NC и NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="aa499-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="aa499-149">Примеры и образцы</span><span class="sxs-lookup"><span data-stu-id="aa499-149">Samples and demos</span></span>
* [<span data-ttu-id="aa499-150">Примеры кода для пакетной службы Azure на C# и Python</span><span class="sxs-lookup"><span data-stu-id="aa499-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="aa499-151">Набор средств [Batch Shipyard](https://azure.github.io/batch-shipyard/) для удобного развертывания пакетных рабочих нагрузок Docker в пакетную службу Azure</span><span class="sxs-lookup"><span data-stu-id="aa499-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="aa499-152">Пакет R [doAzureParallel](http://www.github.com/Azure/doAzureParallel), созданный на основе пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="aa499-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="aa499-153">Пробная установка сервера SUSE Linux Enterprise Server для HPC</span><span class="sxs-lookup"><span data-stu-id="aa499-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="aa499-154">Связанные службы Azure</span><span class="sxs-lookup"><span data-stu-id="aa499-154">Related Azure services</span></span>
* [<span data-ttu-id="aa499-155">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="aa499-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="aa499-156">Машинное обучение</span><span class="sxs-lookup"><span data-stu-id="aa499-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="aa499-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa499-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="aa499-158">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="aa499-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="aa499-159">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="aa499-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="aa499-160">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="aa499-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="aa499-161">Служба приложений</span><span class="sxs-lookup"><span data-stu-id="aa499-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="aa499-162">Службы мультимедиа</span><span class="sxs-lookup"><span data-stu-id="aa499-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="aa499-163">Функции</span><span class="sxs-lookup"><span data-stu-id="aa499-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="aa499-164">Проекты архитектуры</span><span class="sxs-lookup"><span data-stu-id="aa499-164">Architecture blueprints</span></span>
* <span data-ttu-id="aa499-165">[Управление данными и высокопроизводительными вычислениями с помощью пакетной службы и фабрики данных Azure](http://go.microsoft.com/fwlink/?linkid=717686) (PDF-файл) и [статья](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="aa499-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="aa499-166">Отраслевые решения</span><span class="sxs-lookup"><span data-stu-id="aa499-166">Industry solutions</span></span>
* [<span data-ttu-id="aa499-167">Банки и рынки ценных бумаг</span><span class="sxs-lookup"><span data-stu-id="aa499-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="aa499-168">Инженерное моделирование</span><span class="sxs-lookup"><span data-stu-id="aa499-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="aa499-169">Истории клиентов</span><span class="sxs-lookup"><span data-stu-id="aa499-169">Customer stories</span></span>
* [<span data-ttu-id="aa499-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="aa499-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="aa499-171">d3View</span><span class="sxs-lookup"><span data-stu-id="aa499-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="aa499-172">Институт исследования рака Людвига</span><span class="sxs-lookup"><span data-stu-id="aa499-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="aa499-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="aa499-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="aa499-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="aa499-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="aa499-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="aa499-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="aa499-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="aa499-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="aa499-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="aa499-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="aa499-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="aa499-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="aa499-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa499-179">Next steps</span></span>
* <span data-ttu-id="aa499-180">Последние объявления см. в [блоге группы Microsoft HPC и пакетной службы](http://blogs.technet.com/b/windowshpc/), а также в [блоге Azure](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="aa499-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="aa499-181">Следите также за лентой [новостей о пакетной службе](https://azure.microsoft.com/updates/?service=batch) или подпишитесь на [RSS-канал](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="aa499-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

