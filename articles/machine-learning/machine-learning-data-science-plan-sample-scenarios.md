---
title: "Дополнительные сценарии анализа для машинного обучения Azure aaaIdentify | Документы Microsoft"
description: "Выберите подходящие сценарии hello это расширенный прогнозной аналитики с hello командного процесса обработки и анализа данных."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="179da-103">Сценарии для расширенной аналитики в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="179da-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="179da-104">В этой статье рассматриваются различные hello образцы источников данных и целевые сценарии, которые могут быть обработаны hello [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="179da-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="179da-105">Hello TDSP предоставляет систематический подход для toocollaborate команды на создание интеллектуальных приложений.</span><span class="sxs-lookup"><span data-stu-id="179da-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="179da-106">представленные сценарии Hello показаны параметры, доступные в рабочем процессе hello обработки данных, зависящих от целевой репозиториев в Azure, расположений и характеристики данных hello.</span><span class="sxs-lookup"><span data-stu-id="179da-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="179da-107">Hello **дерева принятия решений** для выбора hello примеры сценариев, подходящий для данных и цель представлены в последнем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="179da-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="179da-108">Каждого hello в следующих разделах представлен пример сценария.</span><span class="sxs-lookup"><span data-stu-id="179da-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="179da-109">Для каждого сценария перечислены возможные последовательности операций процесса обработки и анализа или расширенного анализа данных, а также вспомогательные ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="179da-110">**Все следующие сценарии hello необходимо:**
> </span><span class="sxs-lookup"><span data-stu-id="179da-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="179da-111">[создать учетную запись хранения](../storage/common/storage-create-storage-account.md)
>   ;</span><span class="sxs-lookup"><span data-stu-id="179da-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="179da-112">Создание рабочей области машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="179da-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="179da-113"><a name="smalllocal"></a>Сценарий \#1: небольшой toomedium набор табличных данных в локальных файлах</span><span class="sxs-lookup"><span data-stu-id="179da-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Небольшие toomedium локальные файлы][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="179da-115">Дополнительные ресурсы Azure: отсутствуют</span><span class="sxs-lookup"><span data-stu-id="179da-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="179da-116">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="179da-117">Отправьте набор данных.</span><span class="sxs-lookup"><span data-stu-id="179da-117">Upload a dataset.</span></span>
3. <span data-ttu-id="179da-118">Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с отправленных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="179da-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="179da-119"><a name="smalllocalprocess"></a>Сценарий \#2: набор данных небольшой toomedium локальных файлов, которые требуют обработки</span><span class="sxs-lookup"><span data-stu-id="179da-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Небольшие toomedium локальных файлов с обработкой][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="179da-121">Дополнительные ресурсы Azure: виртуальная машина Azure (сервер IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="179da-122">Создайте виртуальную машину Azure с IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="179da-123">Передача данных контейнер хранилища Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="179da-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="179da-124">Предварительно обработайте и очистите данные в IPython Notebook из контейнера хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="179da-125">Преобразование данных toocleaned, табличной форме.</span><span class="sxs-lookup"><span data-stu-id="179da-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="179da-126">Сохраните преобразованные данные в большие двоичные объекты Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="179da-127">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="179da-128">Чтение данных hello из больших двоичных объектов Azure с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="179da-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="179da-129">Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с принятых наборов данных.</span><span class="sxs-lookup"><span data-stu-id="179da-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="179da-130"><a name="largelocal"></a>Сценарий\# №3. Большой набор данных в локальных файлах, загружаемый в большие двоичные объекты Azure</span><span class="sxs-lookup"><span data-stu-id="179da-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Локальные файлы большого размера][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="179da-132">Дополнительные ресурсы Azure: виртуальная машина Azure (сервер IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="179da-133">Создайте виртуальную машину Azure с IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="179da-134">Передача данных контейнер хранилища Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="179da-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="179da-135">Предварительно обработайте и очистите данные в IPython Notebook из больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="179da-136">При необходимости, преобразовывать toocleaned данных, в табличной форме.</span><span class="sxs-lookup"><span data-stu-id="179da-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="179da-137">Просмотрите данные и при необходимости создайте компоненты.</span><span class="sxs-lookup"><span data-stu-id="179da-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="179da-138">Извлеките пример данных небольшого или среднего размера.</span><span class="sxs-lookup"><span data-stu-id="179da-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="179da-139">Сохраните данные выборки hello в больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="179da-140">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="179da-141">Чтение данных hello из больших двоичных объектов Azure с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="179da-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="179da-142">Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с принятых наборов данных.</span><span class="sxs-lookup"><span data-stu-id="179da-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="179da-143"><a name="smalllocaltodb"></a>Сценарий \#4: небольшой toomedium набора данных из локальных файлов, предназначенных для SQL Server в виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="179da-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Небольшие toomedium tooSQL локальные файлы базы данных в Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="179da-145">Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="179da-146">Создайте виртуальную машину Azure с SQL Server и IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="179da-147">Передача данных контейнер хранилища Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="179da-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="179da-148">Предварительно обработайте и очистите данные в контейнере хранилища Azure с помощью IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="179da-149">При необходимости, преобразовывать toocleaned данных, в табличной форме.</span><span class="sxs-lookup"><span data-stu-id="179da-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="179da-150">Сохранить tooVM локальных файлов данных (ноутбук IPython работает на виртуальной Машине см. в локальные диски tooVM дисков).</span><span class="sxs-lookup"><span data-stu-id="179da-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="179da-151">Загрузите данные tooSQL сервера базы данных, на Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="179da-152">Вариант \# №1. Использование SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="179da-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="179da-153">TooSQL входа в систему сервера виртуальных Машин</span><span class="sxs-lookup"><span data-stu-id="179da-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="179da-154">Запустите среду SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="179da-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="179da-155">Создайте базу данных и целевые таблицы.</span><span class="sxs-lookup"><span data-stu-id="179da-155">Create database and target tables.</span></span>
   * <span data-ttu-id="179da-156">Используйте одну из массового hello импортировать методы tooload hello данные из файлов локальной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="179da-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="179da-157">Вариант \# №2. Использование IPython Notebook (не рекомендуется использовать этот вариант для средних и больших наборов данных).</span><span class="sxs-lookup"><span data-stu-id="179da-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="179da-158">Используйте tooaccess строку соединения ODBC SQL Server на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="179da-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="179da-159">Создайте базу данных и целевые таблицы.</span><span class="sxs-lookup"><span data-stu-id="179da-159">Create database and target tables.</span></span>
   * <span data-ttu-id="179da-160">Используйте одну из массового hello импортировать методы tooload hello данные из файлов локальной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="179da-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="179da-161">Просмотрите данные и при необходимости создайте компоненты.</span><span class="sxs-lookup"><span data-stu-id="179da-161">Explore data, create features as needed.</span></span> <span data-ttu-id="179da-162">Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="179da-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="179da-163">Только Примечание hello необходимый запрос toocreate их.</span><span class="sxs-lookup"><span data-stu-id="179da-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="179da-164">При необходимости выберите размер примера данных.</span><span class="sxs-lookup"><span data-stu-id="179da-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="179da-165">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="179da-166">Hello чтения данных непосредственно из hello SQL Server с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="179da-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="179da-167">Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.</span><span class="sxs-lookup"><span data-stu-id="179da-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="179da-168">Создайте последовательность операций эксперимента Машинного обучения Azure, начиная с принятых наборов данных.</span><span class="sxs-lookup"><span data-stu-id="179da-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="179da-169"><a name="largelocaltodb"></a>Сценарий \#№5. Большой набор данных в локальных файлах, загружаемый на сервер SQL Server в виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="179da-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![TooSQL большие файлы локальной базы данных в Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="179da-171">Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="179da-172">Создайте виртуальную машину Azure с SQL Server и IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="179da-173">Передача данных контейнер хранилища Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="179da-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="179da-174">Предварительно обработайте и очистите данные (необязательно).</span><span class="sxs-lookup"><span data-stu-id="179da-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="179da-175">а.</span><span class="sxs-lookup"><span data-stu-id="179da-175">a.</span></span>  <span data-ttu-id="179da-176">Предварительно обработайте и очистите данные в IPython Notebook из Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="179da-177">b.</span><span class="sxs-lookup"><span data-stu-id="179da-177">b.</span></span>  <span data-ttu-id="179da-178">При необходимости, преобразовывать toocleaned данных, в табличной форме.</span><span class="sxs-lookup"><span data-stu-id="179da-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="179da-179">c.</span><span class="sxs-lookup"><span data-stu-id="179da-179">c.</span></span>  <span data-ttu-id="179da-180">Сохранить tooVM локальных файлов данных (ноутбук IPython работает на виртуальной Машине см. в локальные диски tooVM дисков).</span><span class="sxs-lookup"><span data-stu-id="179da-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="179da-181">Загрузите данные tooSQL сервера базы данных, на Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="179da-182">а.</span><span class="sxs-lookup"><span data-stu-id="179da-182">a.</span></span>  <span data-ttu-id="179da-183">TooSQL входа сервера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="179da-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="179da-184">b.</span><span class="sxs-lookup"><span data-stu-id="179da-184">b.</span></span>  <span data-ttu-id="179da-185">Если данные еще не сохранены, скачайте файлы данных из Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="179da-186">В.</span><span class="sxs-lookup"><span data-stu-id="179da-186">c.</span></span>  <span data-ttu-id="179da-187">Запустите среду SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="179da-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="179da-188">г)</span><span class="sxs-lookup"><span data-stu-id="179da-188">d.</span></span>  <span data-ttu-id="179da-189">Создайте базу данных и целевые таблицы.</span><span class="sxs-lookup"><span data-stu-id="179da-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="179da-190">д.</span><span class="sxs-lookup"><span data-stu-id="179da-190">e.</span></span>  <span data-ttu-id="179da-191">Используйте одну из hello массового импорта данных hello tooload методы.</span><span class="sxs-lookup"><span data-stu-id="179da-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="179da-192">f.</span><span class="sxs-lookup"><span data-stu-id="179da-192">f.</span></span>  <span data-ttu-id="179da-193">Если требуется соединение таблиц, создайте индексы tooexpedite соединения.</span><span class="sxs-lookup"><span data-stu-id="179da-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="179da-194">Быстрее загружать из размеров больших объемов данных, рекомендуется создавать секционированные таблицы и выполнить массовый импорт данных hello в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="179da-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="179da-195">Дополнительные сведения см. в разделе [параллельный импорт данных tooSQL секционированных таблиц](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="179da-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="179da-196">Просмотрите данные и при необходимости создайте компоненты.</span><span class="sxs-lookup"><span data-stu-id="179da-196">Explore data, create features as needed.</span></span> <span data-ttu-id="179da-197">Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="179da-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="179da-198">Только Примечание hello необходимый запрос toocreate их.</span><span class="sxs-lookup"><span data-stu-id="179da-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="179da-199">При необходимости выберите размер примера данных.</span><span class="sxs-lookup"><span data-stu-id="179da-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="179da-200">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="179da-201">Hello чтения данных непосредственно из hello SQL Server с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="179da-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="179da-202">Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.</span><span class="sxs-lookup"><span data-stu-id="179da-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="179da-203">Создайте простую последовательность операций эксперимента Машинного обучения Azure, начиная с отправленного набора данных.</span><span class="sxs-lookup"><span data-stu-id="179da-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="179da-204"><a name="largedbtodb"></a>Сценарий\# №6. Большой набор данных в локальной базе данных SQL Server, загружаемый на сервер SQL Server в виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="179da-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![В локальной среде tooSQL больших баз данных SQL Server DB в Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="179da-206">Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="179da-207">Создайте виртуальную машину Azure с SQL Server и IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="179da-208">Используйте одну из данных hello Экспорт данных hello tooexport методы toodump файлов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="179da-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="179da-209">Если вы решите toomove все данные из базы данных в локальной среде hello, альтернативный (быстрее) метод toomove hello полный экземпляр базы данных toothe SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="179da-210">Пропустите hello действия tooexport данных, создание базы данных и загрузки и импорта данных toohello целевую базу данных и выполните hello альтернативный метод.</span><span class="sxs-lookup"><span data-stu-id="179da-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="179da-211">Отправьте контейнер хранилища tooAzure файлов дампа.</span><span class="sxs-lookup"><span data-stu-id="179da-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="179da-212">Загрузить hello данных tooa базы данных SQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="179da-213">а.</span><span class="sxs-lookup"><span data-stu-id="179da-213">a.</span></span>  <span data-ttu-id="179da-214">Toohello входа в систему виртуальной Машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="179da-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="179da-215">b.</span><span class="sxs-lookup"><span data-stu-id="179da-215">b.</span></span>  <span data-ttu-id="179da-216">Загрузите файлы данных из папки локальной ВМ toohello контейнер хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="179da-217">c.</span><span class="sxs-lookup"><span data-stu-id="179da-217">c.</span></span>  <span data-ttu-id="179da-218">Запустите среду SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="179da-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="179da-219">г)</span><span class="sxs-lookup"><span data-stu-id="179da-219">d.</span></span>  <span data-ttu-id="179da-220">Создайте базу данных и целевые таблицы.</span><span class="sxs-lookup"><span data-stu-id="179da-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="179da-221">д.</span><span class="sxs-lookup"><span data-stu-id="179da-221">e.</span></span>  <span data-ttu-id="179da-222">Используйте одну из hello массового импорта данных hello tooload методы.</span><span class="sxs-lookup"><span data-stu-id="179da-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="179da-223">f.</span><span class="sxs-lookup"><span data-stu-id="179da-223">f.</span></span>  <span data-ttu-id="179da-224">Если требуется соединение таблиц, создайте индексы tooexpedite соединения.</span><span class="sxs-lookup"><span data-stu-id="179da-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="179da-225">Быстрее загружать большие объемы данных размеров параллельного создания секционированных таблиц и данных hello toobulk импорта.</span><span class="sxs-lookup"><span data-stu-id="179da-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="179da-226">Дополнительные сведения см. в разделе [параллельный импорт данных tooSQL секционированных таблиц](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="179da-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="179da-227">Просмотрите данные и при необходимости создайте компоненты.</span><span class="sxs-lookup"><span data-stu-id="179da-227">Explore data, create features as needed.</span></span> <span data-ttu-id="179da-228">Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="179da-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="179da-229">Только Примечание hello необходимый запрос toocreate их.</span><span class="sxs-lookup"><span data-stu-id="179da-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="179da-230">При необходимости выберите размер примера данных.</span><span class="sxs-lookup"><span data-stu-id="179da-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="179da-231">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="179da-232">Hello чтения данных непосредственно из hello SQL Server с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="179da-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="179da-233">Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.</span><span class="sxs-lookup"><span data-stu-id="179da-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="179da-234">Создайте простую последовательность операций эксперимента Машинного обучения Azure, начиная с отправленного набора данных.</span><span class="sxs-lookup"><span data-stu-id="179da-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="179da-235">Альтернативный способ toocopy всей базы данных из tooAzure SQL Server в локальной базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="179da-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Присоединение и отсоединение базы данных local DB tooSQL DB в Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="179da-237">Дополнительные ресурсы Azure: виртуальная машина Azure (сервер SQL Server и IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="179da-238">tooreplicate hello всей базы данных SQL Server на виртуальной машине SQL Server, следует скопировать базу данных из одного tooanother расположения и сервера, при условии, что hello базы данных можно было временно отключить.</span><span class="sxs-lookup"><span data-stu-id="179da-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="179da-239">Для этого в обозревателе объектов SQL Server Management Studio hello, или с помощью hello эквивалентные команды Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="179da-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="179da-240">Отсоединение базы данных hello в исходных папках hello.</span><span class="sxs-lookup"><span data-stu-id="179da-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="179da-241">Дополнительные сведения см. в статье [Отсоединение базы данных](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="179da-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="179da-242">В окне проводника Windows или командной строки Windows hello копирования отсоединенного файла базы данных или файлов и файла журнала или файлы toohello целевое расположение на виртуальной Машине SQL Server в Azure hello.</span><span class="sxs-lookup"><span data-stu-id="179da-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="179da-243">Присоедините hello копируются файлы toohello целевого экземпляра SQL Server.</span><span class="sxs-lookup"><span data-stu-id="179da-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="179da-244">Дополнительные сведения см. в статье [Присоединение базы данных](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="179da-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="179da-245">[Перенос базы данных путем отсоединения и присоединения (язык Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="179da-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="179da-246"><a name="largedbtohive"></a>Сценарий \# №7. Данные большого размера в локальных файлах, загружаемые в базу данных Hive в кластерах Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="179da-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Данные большого размера в локальных файлах для базы данных Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="179da-248">Дополнительные ресурсы Azure: кластер Azure HDInsight Hadoop и виртуальная машина Azure (сервер IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="179da-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="179da-249">Создайте виртуальную машину Azure с сервером IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="179da-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="179da-250">Создайте кластер Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="179da-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="179da-251">Предварительно обработайте и очистите данные (необязательно).</span><span class="sxs-lookup"><span data-stu-id="179da-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="179da-252">а.</span><span class="sxs-lookup"><span data-stu-id="179da-252">a.</span></span>  <span data-ttu-id="179da-253">Предварительно обработайте и очистите данные в IPython Notebook из Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="179da-254">b.</span><span class="sxs-lookup"><span data-stu-id="179da-254">b.</span></span>  <span data-ttu-id="179da-255">При необходимости, преобразовывать toocleaned данных, в табличной форме.</span><span class="sxs-lookup"><span data-stu-id="179da-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="179da-256">c.</span><span class="sxs-lookup"><span data-stu-id="179da-256">c.</span></span>  <span data-ttu-id="179da-257">Сохранить tooVM локальных файлов данных (ноутбук IPython работает на виртуальной Машине см. в локальные диски tooVM дисков).</span><span class="sxs-lookup"><span data-stu-id="179da-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="179da-258">Передача данных контейнер по умолчанию toohello hello кластера Hadoop, выбранного в шаге hello 2.</span><span class="sxs-lookup"><span data-stu-id="179da-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="179da-259">Загрузить tooHive база данных в кластере Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="179da-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="179da-260">а.</span><span class="sxs-lookup"><span data-stu-id="179da-260">a.</span></span>  <span data-ttu-id="179da-261">Войдите в toohello головного узла кластера Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="179da-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="179da-262">b.</span><span class="sxs-lookup"><span data-stu-id="179da-262">b.</span></span>  <span data-ttu-id="179da-263">Откройте hello командной строки Hadoop.</span><span class="sxs-lookup"><span data-stu-id="179da-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="179da-264">c.</span><span class="sxs-lookup"><span data-stu-id="179da-264">c.</span></span>  <span data-ttu-id="179da-265">Введите каталог корневого куста hello командой `cd %hive_home%\bin` в Hadoop командной строки.</span><span class="sxs-lookup"><span data-stu-id="179da-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="179da-266">d.</span><span class="sxs-lookup"><span data-stu-id="179da-266">d.</span></span>  <span data-ttu-id="179da-267">Выполнение hello запросы Hive toocreate к базе данных и таблиц и загрузки данных из таблиц tooHive хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="179da-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="179da-268">Если данные hello больших, пользователи могут создавать таблицу Hive hello с секциями.</span><span class="sxs-lookup"><span data-stu-id="179da-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="179da-269">После этого пользователи могут использовать `for` цикл в hello командной строки Hadoop на hello головного узла tooload данных в таблицу Hive hello секционированы по секциям.</span><span class="sxs-lookup"><span data-stu-id="179da-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="179da-270">Просмотрите данные и при необходимости создайте компоненты в командной строке Hadoop.</span><span class="sxs-lookup"><span data-stu-id="179da-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="179da-271">Обратите внимание, что функции hello не toobe материализуются в таблицах базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="179da-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="179da-272">Только Примечание hello необходимый запрос toocreate их.</span><span class="sxs-lookup"><span data-stu-id="179da-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="179da-273">а.</span><span class="sxs-lookup"><span data-stu-id="179da-273">a.</span></span>  <span data-ttu-id="179da-274">Войдите в toohello головного узла кластера Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="179da-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="179da-275">b.</span><span class="sxs-lookup"><span data-stu-id="179da-275">b.</span></span>  <span data-ttu-id="179da-276">Откройте hello командной строки Hadoop.</span><span class="sxs-lookup"><span data-stu-id="179da-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="179da-277">c.</span><span class="sxs-lookup"><span data-stu-id="179da-277">c.</span></span>  <span data-ttu-id="179da-278">Введите каталог корневого куста hello командой `cd %hive_home%\bin` в Hadoop командной строки.</span><span class="sxs-lookup"><span data-stu-id="179da-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="179da-279">d.</span><span class="sxs-lookup"><span data-stu-id="179da-279">d.</span></span>  <span data-ttu-id="179da-280">Выполнять запросы Hive hello в Hadoop командной строки на головном узле данных hello tooexplore кластера Hadoop hello hello и создавать компоненты при необходимости.</span><span class="sxs-lookup"><span data-stu-id="179da-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="179da-281">При необходимости или требуемого, образец hello toofit данных в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="179da-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="179da-282">Войдите в toohello [студии машинного обучения Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="179da-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="179da-283">Чтение данных hello непосредственно из hello `Hive Queries` с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="179da-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="179da-284">Необходимый запрос hello вставки, которая извлекает поля, создает компоненты и образцы данных, при необходимости непосредственно в hello [импорта данных] [ import-data] запроса.</span><span class="sxs-lookup"><span data-stu-id="179da-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="179da-285">Создайте простую последовательность операций эксперимента Машинного обучения Azure, начиная с отправленного набора данных.</span><span class="sxs-lookup"><span data-stu-id="179da-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="179da-286"><a name="decisiontree"></a>Дерево принятия решений для выбора сценариев</span><span class="sxs-lookup"><span data-stu-id="179da-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="179da-287">Hello следующей диаграмме показаны описанных выше сценариях hello и hello Advanced Analytics процесса и технологии выборов, сделанных использующие tooeach hello перечислено сценариев.</span><span class="sxs-lookup"><span data-stu-id="179da-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="179da-288">Обратите внимание, что может занять обработки данных, просмотра, конструируются и выборки поместите в одной или нескольких метод/среды--hello источника промежуточных данных, или целевых средах — и может выполняться последовательно по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="179da-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="179da-289">Схема Hello только служит в качестве иллюстрации того, некоторые из возможных потоков и не предоставляет полное перечисление.</span><span class="sxs-lookup"><span data-stu-id="179da-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Примеры сценариев с пошаговыми действиями процесса обработки и анализа данных][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="179da-291">Практические примеры расширенного анализа</span><span class="sxs-lookup"><span data-stu-id="179da-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="179da-292">Пошаговые руководства машинного обучения Azure начала до конца, в которых используются hello Advanced Analytics процесса и технологии использования общих наборов данных см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="179da-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="179da-293">[Процесс обработки и анализа данных группы на практике: использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="179da-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="179da-294">[Процесс обработки и анализа данных группы на практике: использование кластеров HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="179da-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
