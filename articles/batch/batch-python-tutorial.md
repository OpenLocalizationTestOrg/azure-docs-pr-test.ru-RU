---
title: "Руководство по использованию пакета SDK пакетной службы Azure для Python | Документация Майкрософт"
description: "Изучите основные принципы работы пакетной службы Azure и создайте простое решения с использованием Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd5a977c10d3955639beb893cd7a37581b14f7c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-batch-sdk-for-python"></a><span data-ttu-id="9243a-103">Приступая к работе с пакетом SDK пакетной службы для Python</span><span class="sxs-lookup"><span data-stu-id="9243a-103">Get started with the Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9243a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9243a-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="9243a-105">Python</span><span class="sxs-lookup"><span data-stu-id="9243a-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="9243a-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="9243a-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="9243a-107">Здесь представлены основные сведения о [пакетной службе Azure][azure_batch] и клиенте [Python пакетной службы][py_azure_sdk] в рамках обсуждения небольшого приложения пакетной службы Azure, написанного на языке Python.</span><span class="sxs-lookup"><span data-stu-id="9243a-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="9243a-108">Мы рассмотрим, как в двух примерах скрипта используется пакетная служба для обработки параллельной рабочей нагрузки на виртуальных машинах Linux в облаке и происходит взаимодействие со [службой хранилища Azure](../storage/common/storage-introduction.md) при промежуточном хранении и извлечении файлов.</span><span class="sxs-lookup"><span data-stu-id="9243a-108">We look at how two sample scripts use the Batch service to process a parallel workload on Linux virtual machines in the cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="9243a-109">Вы узнаете об общем рабочем процессе приложения пакетной службы и получите базовые знания о главных компонентах пакетной службы, например заданиях, задачах, пулах и вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="9243a-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="9243a-110">![Рабочий процесс решения пакетной службы (основной)][11]</span><span class="sxs-lookup"><span data-stu-id="9243a-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="9243a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9243a-111">Prerequisites</span></span>
<span data-ttu-id="9243a-112">В этой статье предполагается, что вы уже работали с Python и знаете, как работать в Linux.</span><span class="sxs-lookup"><span data-stu-id="9243a-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="9243a-113">Также предполагается, что вы можете выполнить требования к созданию учетной записи для службы хранилища и пакетной службы Azure. Эти требования перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="9243a-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="9243a-114">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="9243a-114">Accounts</span></span>
* <span data-ttu-id="9243a-115">**Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="9243a-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="9243a-116">**Учетная запись пакетной службы**. Если у вас есть подписка Azure, [создайте учетную запись пакетной службы Azure](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="9243a-117">**Учетная запись хранения**. См. раздел [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="9243a-118">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9243a-118">Code sample</span></span>
<span data-ttu-id="9243a-119">[Пример кода][github_article_samples] Python для руководства — это один из многих примеров кода пакетной службы в репозитории [azure-batch-samples][github_samples] на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="9243a-119">The Python tutorial [code sample][github_article_samples] is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="9243a-120">Чтобы скачать все примеры, на домашней странице репозитория щелкните **Clone or download > Download ZIP** (Клонировать или скачать > Скачать ZIP-файл) или щелкните ссылку [azure-batch-samples-master.zip][github_samples_zip] и скачайте их напрямую.</span><span class="sxs-lookup"><span data-stu-id="9243a-120">You can download all the samples by clicking **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="9243a-121">После извлечения содержимого ZIP-файла оба сценария для этого руководства будут находиться в каталоге `article_samples` :</span><span class="sxs-lookup"><span data-stu-id="9243a-121">Once you've extracted the contents of the ZIP file, the two scripts for this tutorial are found in the `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="9243a-122">Среда Python</span><span class="sxs-lookup"><span data-stu-id="9243a-122">Python environment</span></span>
<span data-ttu-id="9243a-123">Чтобы запустить пример скрипта *python_tutorial_client.py* на локальной рабочей станции, необходим **интерпретатор Python**, совместимый с версией **2.7** или **3.3+**.</span><span class="sxs-lookup"><span data-stu-id="9243a-123">To run the *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="9243a-124">Сценарий прошел испытания в Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="9243a-124">The script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="9243a-125">Зависимости шифрования</span><span class="sxs-lookup"><span data-stu-id="9243a-125">cryptography dependencies</span></span>
<span data-ttu-id="9243a-126">Для библиотеки [шифрования][crypto], которая требуется пакетам Python `azure-batch` и `azure-storage`, необходимо установить зависимости.</span><span class="sxs-lookup"><span data-stu-id="9243a-126">You must install the dependencies for the [cryptography][crypto] library, required by the `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="9243a-127">Выполните одну из следующих операций, подходящих для вашей платформы, или ознакомьтесь с дополнительными сведениями об [установке шифрования][crypto_install]:</span><span class="sxs-lookup"><span data-stu-id="9243a-127">Perform one of the following operations appropriate for your platform, or refer to the [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="9243a-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9243a-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="9243a-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="9243a-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="9243a-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="9243a-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="9243a-131">Windows</span><span class="sxs-lookup"><span data-stu-id="9243a-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="9243a-132">При установке для версии Python 3.3+ в Linux используйте эквиваленты python3 для зависимостей Python.</span><span class="sxs-lookup"><span data-stu-id="9243a-132">If installing for Python 3.3+ on Linux, use the python3 equivalents for the Python dependencies.</span></span> <span data-ttu-id="9243a-133">Например, в Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="9243a-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="9243a-134">Пакеты Azure</span><span class="sxs-lookup"><span data-stu-id="9243a-134">Azure packages</span></span>
<span data-ttu-id="9243a-135">Далее установите пакеты Python **пакетной службы Azure** и **службы хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="9243a-135">Next, install the **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="9243a-136">Оба пакета можно установить, используя **pip** и *requirements.txt*, доступные здесь:</span><span class="sxs-lookup"><span data-stu-id="9243a-136">You can install both packages by using **pip** and the *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="9243a-137">Выполните команду **pip** , чтобы установить пакеты службы хранения и пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-137">Issue following **pip** command to install the Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="9243a-138">Кроме того, пакеты Python [azure-batch][pypi_batch] и [azure-storage][pypi_storage] можно установить вручную.</span><span class="sxs-lookup"><span data-stu-id="9243a-138">Or, you can install the [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="9243a-139">Если вы используете непривилегированную учетную запись, может понадобиться добавить к команде префикс `sudo`.</span><span class="sxs-lookup"><span data-stu-id="9243a-139">If you are using an unprivileged account, you may need to prefix your commands with `sudo`.</span></span> <span data-ttu-id="9243a-140">Например, `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="9243a-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="9243a-141">Дополнительные сведения об установке пакетов Python см. в статье [Installing Packages][pypi_install] (Установка пакетов) на сайте python.org.</span><span class="sxs-lookup"><span data-stu-id="9243a-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="9243a-142">Пример кода Python для руководства по пакетной службе</span><span class="sxs-lookup"><span data-stu-id="9243a-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="9243a-143">Пример кода Python для руководства по пакетной службе состоит из двух сценариев Python и нескольких файлов данных:</span><span class="sxs-lookup"><span data-stu-id="9243a-143">The Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="9243a-144">**python_tutorial_client.py** взаимодействует с пакетной службой и службой хранилища, чтобы выполнять параллельную рабочую нагрузку на вычислительных узлах (виртуальных машинах).</span><span class="sxs-lookup"><span data-stu-id="9243a-144">**python_tutorial_client.py**: Interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="9243a-145">Скрипт *python_tutorial_client.py* выполняется на локальной рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="9243a-145">The *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="9243a-146">**python_tutorial_task.py** — это скрипт, который запускается на вычислительных узлах в Azure, чтобы выполнять фактическую работу.</span><span class="sxs-lookup"><span data-stu-id="9243a-146">**python_tutorial_task.py**: The script that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="9243a-147">В этом примере *python_tutorial_task.py* анализирует текст во входном файле, скачанном из службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-147">In the sample, *python_tutorial_task.py* parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="9243a-148">Затем он создает текстовый файл (выходной файл), который содержит список из трех наиболее часто употребляемых слов во входном файле.</span><span class="sxs-lookup"><span data-stu-id="9243a-148">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="9243a-149">После создания выходного файла *python_tutorial_task.py* отправляет его в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-149">After it creates the output file, *python_tutorial_task.py* uploads the file to Azure Storage.</span></span> <span data-ttu-id="9243a-150">После этого он станет доступен для скачивания в сценарий клиента, запущенного на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="9243a-150">This makes it available for download to the client script running on your workstation.</span></span> <span data-ttu-id="9243a-151">Скрипт *python_tutorial_task.py* выполняется параллельно на нескольких вычислительных узлах в пакетной службе.</span><span class="sxs-lookup"><span data-stu-id="9243a-151">The *python_tutorial_task.py* script runs in parallel on multiple compute nodes in the Batch service.</span></span>
* <span data-ttu-id="9243a-152">Три текстовых файла **./data/taskdata\*.txt** обеспечивают ввод данных для задач, которые выполняются на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="9243a-152">**./data/taskdata\*.txt**: These three text files provide the input for the tasks that run on the compute nodes.</span></span>

<span data-ttu-id="9243a-153">На следующей схеме показаны основные операции, выполняемые с помощью сценариев клиента и задач.</span><span class="sxs-lookup"><span data-stu-id="9243a-153">The following diagram illustrates the primary operations that are performed by the client and task scripts.</span></span> <span data-ttu-id="9243a-154">Этот основной рабочий процесс является типичным для многих вычислительных решений, созданных с помощью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="9243a-155">Хотя он не демонстрирует все возможности, доступные в пакетной службе, почти все ее сценарии включают в себя части этого рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="9243a-155">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="9243a-156">![Пример рабочего процесса пакетной службы][8]</span><span class="sxs-lookup"><span data-stu-id="9243a-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="9243a-157">**Шаг 1.**</span><span class="sxs-lookup"><span data-stu-id="9243a-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="9243a-158">Создайте **контейнеры** в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="9243a-159">
[**Шаг 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="9243a-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="9243a-160">Отправьте скрипт задач и входные файлы в контейнеры.</span><span class="sxs-lookup"><span data-stu-id="9243a-160">Upload task script and input files to containers.</span></span><br/><span data-ttu-id="9243a-161">
[**Шаг 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="9243a-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="9243a-162">Создайте **пул** пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="9243a-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="9243a-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="9243a-164">Задача **StartTask** пула скачивает скрипт задач (python_tutorial_task.py) на узлы во время их присоединения к пулу.</span><span class="sxs-lookup"><span data-stu-id="9243a-164">The pool **StartTask** downloads the task script (python_tutorial_task.py) to nodes as they join the pool.</span></span><br/><span data-ttu-id="9243a-165">
[**Шаг 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="9243a-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="9243a-166">Создайте **задание** пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="9243a-167">
[**Шаг 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="9243a-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="9243a-168">Добавьте **задачи** в задание.</span><span class="sxs-lookup"><span data-stu-id="9243a-168">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="9243a-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="9243a-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="9243a-170">Планируется выполнение задач на узлах.</span><span class="sxs-lookup"><span data-stu-id="9243a-170">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="9243a-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="9243a-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="9243a-172">Каждая задача скачивает свои входные данные из службы хранилища Azure, а затем начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="9243a-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="9243a-173">
[**Шаг 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="9243a-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="9243a-174">Мониторинг задач.</span><span class="sxs-lookup"><span data-stu-id="9243a-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="9243a-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="9243a-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="9243a-176">Когда задачи выполнены, их выходные данные отправляются в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-176">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="9243a-177">
[**Шаг 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="9243a-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="9243a-178">Скачайте выходные данные задачи из службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="9243a-178">Download task output from Storage.</span></span>

<span data-ttu-id="9243a-179">Как уже упоминалось, не каждое решение пакетной службы будет выполнять именно эти шаги. Некоторые решения могут выполнять больше действий, но этот пример демонстрирует общие процессы в решении пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="9243a-180">Подготовка сценария клиента</span><span class="sxs-lookup"><span data-stu-id="9243a-180">Prepare client script</span></span>
<span data-ttu-id="9243a-181">Прежде чем запустить пример, добавьте учетные данные учетных записей пакетной службы и службы хранилища в скрипт *python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="9243a-181">Before you run the sample, add your Batch and Storage account credentials to *python_tutorial_client.py*.</span></span> <span data-ttu-id="9243a-182">Откройте файл в своем редакторе и обновите следующие строки, используя учетные данные, если еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="9243a-182">If you have not done so already, open the file in your favorite editor and update the following lines with your credentials.</span></span>

```python
# Update the Batch and Storage account credential strings below with the values
# unique to your accounts. These are used when constructing connection strings
# for the Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="9243a-183">Учетные данные учетных записей пакетной службы и службы хранилища можно найти в колонке учетной записи каждой службы на [портале Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="9243a-183">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="9243a-184">![Учетные данные пакетной службы на портале][9]
![Учетные данные службы хранилища на портале][10]</span><span class="sxs-lookup"><span data-stu-id="9243a-184">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="9243a-185">В следующих разделах мы проанализируем шаги, выполняемые в скриптах для обработки рабочей нагрузки в пакетной службе.</span><span class="sxs-lookup"><span data-stu-id="9243a-185">In the following sections, we analyze the steps used by the scripts to process a workload in the Batch service.</span></span> <span data-ttu-id="9243a-186">Во время работы с оставшейся частью статьи рекомендуем регулярно просматривать сценарии в редакторе.</span><span class="sxs-lookup"><span data-stu-id="9243a-186">We encourage you to refer regularly to the scripts in your editor while you work your way through the rest of the article.</span></span>

<span data-ttu-id="9243a-187">Перейдите на следующую строку в скрипте **python_tutorial_client.py**, чтобы выполнить шаг 1:</span><span class="sxs-lookup"><span data-stu-id="9243a-187">Navigate to the following line in **python_tutorial_client.py** to start with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="9243a-188">Шаг 1. Создание контейнеров службы хранилища</span><span class="sxs-lookup"><span data-stu-id="9243a-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="9243a-189">![Создание контейнеров в службе хранилища Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="9243a-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="9243a-190">Пакетная служба включает встроенную поддержку для взаимодействия со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="9243a-191">Контейнеры в учетной записи хранения предоставляют файлы, которые нужны для выполнения задач, запускаемых в вашей учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-191">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="9243a-192">Контейнеры также предоставляют место для хранения выходных данных, создаваемых задачами.</span><span class="sxs-lookup"><span data-stu-id="9243a-192">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="9243a-193">Сначала скрипт *python_tutorial_client.py* создает три контейнера в [хранилище BLOB-объектов Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="9243a-193">The first thing the *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="9243a-194">**application**. В этом контейнере будет храниться скрипт Python *python_tutorial_task.py*, выполняемый задачами.</span><span class="sxs-lookup"><span data-stu-id="9243a-194">**application**: This container will store the Python script run by the tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="9243a-195">**input**— задачи будут скачивать файлы данных, которые они должны обрабатывать, из контейнера *input* .</span><span class="sxs-lookup"><span data-stu-id="9243a-195">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="9243a-196">**output**— после завершения обработки входных файлов задачи будут отправлять результаты обработки в контейнер *output* .</span><span class="sxs-lookup"><span data-stu-id="9243a-196">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="9243a-197">Чтобы скрипт мог взаимодействовать с учетной записью службы хранилища и создавать контейнеры, мы используем пакет [azure-storage][pypi_storage] для создания объекта [BlockBlobService][py_blockblobservice], клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="9243a-197">In order to interact with a Storage account and create containers, we use the [azure-storage][pypi_storage] package to create a [BlockBlobService][py_blockblobservice] object--the "blob client."</span></span> <span data-ttu-id="9243a-198">Затем с помощью клиента BLOB-объектов мы создадим три контейнера в учетной записи службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="9243a-198">We then create three containers in the Storage account using the blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create the blob client, for use in obtaining references to
# blob storage containers and uploading files to containers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use the blob client to create the containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="9243a-199">Когда контейнеры будут созданы, приложение сможет отправлять файлы, которые будут использоваться задачами.</span><span class="sxs-lookup"><span data-stu-id="9243a-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="9243a-200">Статья [Использование хранилища больших двоичных объектов Azure из Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) содержит хороший обзор работы с контейнерами службы хранилища Azure и большими двоичными объектами.</span><span class="sxs-lookup"><span data-stu-id="9243a-200">[How to use Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="9243a-201">Вы должны ознакомиться с этой статьей, прежде чем приступать к работе с пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="9243a-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="9243a-202">Шаг 2. Отправка сценария задач и файлов данных</span><span class="sxs-lookup"><span data-stu-id="9243a-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="9243a-203">![Отправка файлов приложения и входных данных в контейнеры][2]
</span><span class="sxs-lookup"><span data-stu-id="9243a-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="9243a-204">Во время отправки файлов скрипт *python_tutorial_client.py* сначала определяет коллекции путей к файлам **application** и **input** на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9243a-204">In the file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="9243a-205">Затем оно отправляет эти файлы в контейнеры, созданные в рамках предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="9243a-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```python
# Paths to the task script. This script will be executed by the tasks that
# run on the compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# The collection of data files that are to be processed by the tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload the application script to Azure Storage. This is the script that
# will process the data files, and is executed by each of the tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload the data files. This is the data that will be processed by each of
# the tasks executed on the compute nodes in the pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="9243a-206">Списковое выражение вызывает функцию `upload_file_to_container` для каждого файла в коллекциях, а затем заполняются две коллекции [ResourceFile][py_resource_file].</span><span class="sxs-lookup"><span data-stu-id="9243a-206">Using list comprehension, the `upload_file_to_container` function is called for each file in the collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="9243a-207">Функция `upload_file_to_container` показана ниже.</span><span class="sxs-lookup"><span data-stu-id="9243a-207">The `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file to an Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: The name of the Azure Blob storage container.
    :param str file_path: The local path to the file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} to container [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="9243a-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="9243a-208">ResourceFiles</span></span>
<span data-ttu-id="9243a-209">Объект [ResourceFile][py_resource_file] передает задачи в пакетную службу с URL-адресом файла в службе хранилища Azure, который будет скачан на вычислительный узел перед выполнением этой задачи.</span><span class="sxs-lookup"><span data-stu-id="9243a-209">A [ResourceFile][py_resource_file] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="9243a-210">Свойство [ResourceFile][py_resource_file].**blob_source** указывает полный URL-адрес файла, по которому его можно найти в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-210">The [ResourceFile][py_resource_file].**blob_source** property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="9243a-211">URL-адрес может также включать подписанный URL-адрес (SAS), который обеспечивает безопасный доступ к файлу.</span><span class="sxs-lookup"><span data-stu-id="9243a-211">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="9243a-212">Большинство типов задач в пакетной службе, в том числе перечисленные ниже, содержат свойство *ResourceFiles* .</span><span class="sxs-lookup"><span data-stu-id="9243a-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="9243a-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="9243a-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="9243a-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="9243a-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="9243a-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="9243a-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="9243a-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="9243a-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="9243a-217">В этом примере не используются типы задач JobPreparationTask или JobReleaseTask, но о них можно узнать больше из статьи [Выполнение задач подготовки и завершения заданий на вычислительных узлах пакетной службы Azure](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-217">This sample does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="9243a-218">Подписанный URL-адрес (SAS)</span><span class="sxs-lookup"><span data-stu-id="9243a-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="9243a-219">Подписанные URL-адреса — это строки, которые предоставляют безопасный доступ к контейнерам и большим двоичным объектам в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-219">Shared access signatures are strings that provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="9243a-220">Скрипт *python_tutorial_client.py* использует подписанные URL-адреса как контейнеров, так и больших двоичных объектов. Он демонстрирует, как получить эти строки подписанных URL-адресов из службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="9243a-220">The *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="9243a-221">**Подписанные URL-адреса больших двоичных объектов**. Задача StartTask пула использует подписанные URL-адреса больших двоичных объектов во время скачивания скрипта заданий и файлов входных данных из службы хранилища (см. [шаг 3](#step-3-create-batch-pool) ниже).</span><span class="sxs-lookup"><span data-stu-id="9243a-221">**Blob shared access signatures**: The pool's StartTask uses blob shared access signatures when it downloads the task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="9243a-222">Функция `upload_file_to_container` в *python_tutorial_client.py* содержит код, который получает подписанный URL-адрес каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9243a-222">The `upload_file_to_container` function in *python_tutorial_client.py* contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="9243a-223">Для этого в модуле службы хранилища вызывается [BlockBlobService.make_blob_url][py_make_blob_url].</span><span class="sxs-lookup"><span data-stu-id="9243a-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in the Storage module.</span></span>
* <span data-ttu-id="9243a-224">**Подписанный URL-адрес контейнера**. Когда каждая задача завершает работу на вычислительном узле, она отправляет свой выходной файл в контейнер *output* в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-224">**Container shared access signature**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="9243a-225">Для этого *python_tutorial_task.py* использует подписанный URL-адрес контейнера, который предоставляет доступ на запись в контейнер.</span><span class="sxs-lookup"><span data-stu-id="9243a-225">To do so, *python_tutorial_task.py* uses a container shared access signature that provides write access to the container.</span></span> <span data-ttu-id="9243a-226">Функция `get_container_sas_token` в *python_tutorial_client.py* получает подписанный URL-адрес контейнера, который затем передается в задачи в качестве аргумента командной строки.</span><span class="sxs-lookup"><span data-stu-id="9243a-226">The `get_container_sas_token` function in *python_tutorial_client.py* obtains the container's shared access signature, which is then passed as a command-line argument to the tasks.</span></span> <span data-ttu-id="9243a-227">На шаге 5 [Добавление задач в задание](#step-5-add-tasks-to-job) описывается использование SAS контейнера.</span><span class="sxs-lookup"><span data-stu-id="9243a-227">Step #5, [Add tasks to a job](#step-5-add-tasks-to-job), discusses the usage of the container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="9243a-228">Дополнительные сведения о предоставлении безопасного доступа к данным в своей учетной записи службы хранилища см. в серии из двух статей о подписанных URL-адресах: [Часть 1: общие сведения о модели SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) и [Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-228">Check out the two-part series on shared access signatures, [Part 1: Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with the Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="9243a-229">Шаг 3. Создание пула пакетной службы</span><span class="sxs-lookup"><span data-stu-id="9243a-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="9243a-230">![Создание пула пакетной службы][3]
</span><span class="sxs-lookup"><span data-stu-id="9243a-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="9243a-231">**Пул** пакетной службы — это коллекция вычислительных узлов (виртуальных машин), на которых пакетная служба выполняет задачи задания.</span><span class="sxs-lookup"><span data-stu-id="9243a-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="9243a-232">После отправки скрипта задач и файлов данных в учетную запись службы хранилища *python_tutorial_client.py* начинает взаимодействие с пакетной службой, используя ее модуль Python.</span><span class="sxs-lookup"><span data-stu-id="9243a-232">After it uploads the task script and data files to the Storage account, *python_tutorial_client.py* starts its interaction with the Batch service by using the Batch Python module.</span></span> <span data-ttu-id="9243a-233">Для этого создается [BatchServiceClient][py_batchserviceclient].</span><span class="sxs-lookup"><span data-stu-id="9243a-233">To do so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with the Batch
# service in addition to Storage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="9243a-234">Затем в учетной записи пакетной службы создается пул вычислительных узлов с помощью вызова `create_pool`.</span><span class="sxs-lookup"><span data-stu-id="9243a-234">Next, a pool of compute nodes is created in the Batch account with a call to `create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with the specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for the new pool.
    :param list resource_files: A collection of resource files for the pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify the commands for the pool's start task. The start task is run
    # on each node as it joins the pool, and when it's rebooted or re-imaged.
    # We use the start task to prep the node for running our task script.
    task_commands = [
        # Copy the python_tutorial_task.py script to the "shared" directory
        # that all tasks that run on the node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and the dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install the azure-storage module so that the task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get the node agent SKU and image reference for the virtual machine
    # configuration.
    # For more information about the virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="9243a-235">Во время создания пула необходимо определить [PoolAddParameter][py_pooladdparam], который указывает несколько свойств пула:</span><span class="sxs-lookup"><span data-stu-id="9243a-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for the pool:</span></span>

* <span data-ttu-id="9243a-236">**Идентификатор** пула (*id*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9243a-236">**ID** of the pool (*id* - required)</span></span><p/><span data-ttu-id="9243a-237">Как и у большинства сущностей в пакетной службе, у нового пула должен быть идентификатор, уникальный в учетной записи этой службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="9243a-238">Код ссылается на этот пул, используя его идентификатор, по которому пул также можно найти на [портале Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="9243a-238">Your code refers to this pool using its ID, and it's how you identify the pool in the Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="9243a-239">**Количество вычислительных узлов** (*target_dedicated*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9243a-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="9243a-240">Указывает, сколько виртуальных машин следует развернуть в пуле.</span><span class="sxs-lookup"><span data-stu-id="9243a-240">This property specifies how many VMs should be deployed in the pool.</span></span> <span data-ttu-id="9243a-241">Стоит отметить, что для всех учетных записей пакетной службы установлена **квота** по умолчанию, которая ограничивает количество **ядер** (и, следовательно, вычислительных узлов) в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9243a-241">It is important to note that all Batch accounts have a default **quota** that limits the number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="9243a-242">Дополнительные сведения о квотах по умолчанию и инструкцию по [увеличению квоты](batch-quota-limit.md#increase-a-quota) (например, максимального количества ядер в учетной записи пакетной службы) см. в статье [Квоты и ограничения пакетной службы Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-242">You can find the default quotas and instructions on how to [increase a quota](batch-quota-limit.md#increase-a-quota) (such as the maximum number of cores in your Batch account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="9243a-243">Если возник вопрос о том, почему пул не использует больше определенного количества узлов,</span><span class="sxs-lookup"><span data-stu-id="9243a-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="9243a-244">Если возник вопрос о том, почему пул не использует больше определенного количества узлов, причиной может быть квота на ядра.</span><span class="sxs-lookup"><span data-stu-id="9243a-244">this core quota may be the cause.</span></span>
* <span data-ttu-id="9243a-245">**Операционная система** для узлов (*virtual_machine_configuration* **или** *cloud_service_configuration*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9243a-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="9243a-246">В *python_tutorial_client.py* мы создаем пул узлов Linux с использованием [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="9243a-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="9243a-247">Функция `select_latest_verified_vm_image_with_node_agent_sku` в `common.helpers` упрощает работу с образами из [магазина виртуальных машин Azure][vm_marketplace].</span><span class="sxs-lookup"><span data-stu-id="9243a-247">The `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="9243a-248">Дополнительные сведения об использовании образов из магазина см. в статье [Подготовка вычислительных узлов Linux в пулах пакетной службы Azure](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="9243a-249">**Размер вычислительных узлов** (*vm_size*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9243a-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="9243a-250">Так как мы указываем узлы Linux для [VirtualMachineConfiguration][py_vm_config], необходимо указать их размер (в этом примере — `STANDARD_A1`), как описано в статье [Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9243a-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9243a-251">Дополнительные сведения см. в статье [Подготовка вычислительных узлов Linux в пулах пакетной службы Azure](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="9243a-252">**Задача запуска** (*start_task*, не обязательное).</span><span class="sxs-lookup"><span data-stu-id="9243a-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="9243a-253">Вместе со свойствами физических узлов выше можно также указать [StartTask][py_starttask] для пула (необязательно).</span><span class="sxs-lookup"><span data-stu-id="9243a-253">Along with the above physical node properties, you may also specify a [StartTask][py_starttask] for the pool (it is not required).</span></span> <span data-ttu-id="9243a-254">Задача StartTask выполняется на каждом узле по мере его присоединения к пулу, а также при каждом перезапуске узла.</span><span class="sxs-lookup"><span data-stu-id="9243a-254">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="9243a-255">Она особенно полезна для подготовки вычислительных узлов к выполнению таких операций, как установка приложений, которые будут использовать задачи.</span><span class="sxs-lookup"><span data-stu-id="9243a-255">The StartTask is especially useful for preparing compute nodes for the execution of tasks, such as installing the applications that your tasks run.</span></span><p/><span data-ttu-id="9243a-256">В этом примере приложения задача StartTask копирует файлы, которые она загружает из рабочего каталога StartTask службы хранилища (эти файлы указаны в свойстве **resource_files** задачи *StartTask*) в *общий* каталог, к которому имеют доступ все задачи, выполняемые на узле.</span><span class="sxs-lookup"><span data-stu-id="9243a-256">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the StartTask's **resource_files** property) from the StartTask *working directory* to the *shared* directory that all tasks running on the node can access.</span></span> <span data-ttu-id="9243a-257">По сути, это обеспечивает копирование `python_tutorial_task.py` в общий каталог на каждом узле, когда узел присоединяется к пулу, чтобы к нему был доступ у всех задач, запускаемых на узле.</span><span class="sxs-lookup"><span data-stu-id="9243a-257">Essentially, this copies `python_tutorial_task.py` to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

<span data-ttu-id="9243a-258">Вы могли заметить вызов вспомогательной функции `wrap_commands_in_shell` .</span><span class="sxs-lookup"><span data-stu-id="9243a-258">You may notice the call to the `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="9243a-259">Она использует коллекцию отдельных команд и создает одну соответствующую командную строку для свойства командной строки задачи.</span><span class="sxs-lookup"><span data-stu-id="9243a-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="9243a-260">Обратите также внимание, что во фрагменте кода выше в свойстве **command_line** задачи StartTask используются две переменные среды: `AZ_BATCH_TASK_WORKING_DIR` и `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="9243a-260">Also notable in the code snippet above is the use of two environment variables in the **command_line** property of the StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="9243a-261">На каждом вычислительном узле в пуле пакетной службы автоматически настраивается несколько переменных среды, характерных для пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="9243a-262">Любой процесс, выполняемый задачей, имеет доступ к этим переменным среды.</span><span class="sxs-lookup"><span data-stu-id="9243a-262">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="9243a-263">Дополнительные сведения о переменных среды, доступных на вычислительных узлах в пуле пакетной службы, а также сведения о рабочих каталогах задач см. в разделах **Параметры среды для задач** и **Файлы и каталоги** статьи с [обзором функций пакетной службы Azure](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="9243a-263">To find out more about the environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in the [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="9243a-264">Шаг 4. Создание задания пакетной службы</span><span class="sxs-lookup"><span data-stu-id="9243a-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="9243a-265">![Создание задания пакетной службы][4]</span><span class="sxs-lookup"><span data-stu-id="9243a-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="9243a-266">**Задание** пакетной службы — это коллекция задач, связанных с пулом вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9243a-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="9243a-267">Задачи задания выполняются на вычислительных узлах связанного пула.</span><span class="sxs-lookup"><span data-stu-id="9243a-267">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="9243a-268">Вы можете использовать задание не только для упорядочивания и отслеживания задач в соответствующих рабочих нагрузках, но и для установления определенных ограничений, включая максимальное время выполнения задания (а следовательно, и его задач). При этом назначается приоритет задания относительно других заданий в учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) and job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="9243a-269">Но в этом примере задание связано только с пулом, который был создан на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="9243a-269">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="9243a-270">Дополнительные свойства не настроены.</span><span class="sxs-lookup"><span data-stu-id="9243a-270">No additional properties are configured.</span></span>

<span data-ttu-id="9243a-271">Все задания пакетной службы связаны с конкретным пулом.</span><span class="sxs-lookup"><span data-stu-id="9243a-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="9243a-272">Эта связь указывает, в каких узлах выполняются задачи задания.</span><span class="sxs-lookup"><span data-stu-id="9243a-272">This association indicates which nodes the job's tasks execute on.</span></span> <span data-ttu-id="9243a-273">Вам необходимо указать пул, используя свойство [PoolInformation][py_poolinfo], как показано в следующем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="9243a-273">You specify the pool by using the [PoolInformation][py_poolinfo] property, as shown in the code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with the specified ID, associated with the specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID for the job.
    :param str pool_id: The ID for the pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="9243a-274">В созданное задание добавляются задачи для выполнения работы.</span><span class="sxs-lookup"><span data-stu-id="9243a-274">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="9243a-275">Шаг 5. Добавление задач в задание</span><span class="sxs-lookup"><span data-stu-id="9243a-275">Step 5: Add tasks to job</span></span>
<span data-ttu-id="9243a-276">![Добавление задач в задание][5]</span><span class="sxs-lookup"><span data-stu-id="9243a-276">![Add tasks to job][5]</span></span><br/><span data-ttu-id="9243a-277">
*(1) Задачи добавляются в задание, (2) планируется запуск задач на узлах, (3) задачи скачивают файлы данных для обработки*</span><span class="sxs-lookup"><span data-stu-id="9243a-277">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="9243a-278">**Задачи** пакетной службы представляют собой отдельные рабочие единицы, выполняемые на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="9243a-278">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="9243a-279">У задачи есть командная строка, она запускает сценарии или исполняемые файлы, указанные в этой строке.</span><span class="sxs-lookup"><span data-stu-id="9243a-279">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="9243a-280">Для фактического выполнения работы необходимо добавить задачи в задание.</span><span class="sxs-lookup"><span data-stu-id="9243a-280">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="9243a-281">Каждая задача [CloudTask][py_task] (как и задача StartTask пула) настраивается с помощью свойства командной строки и объекта [ResourceFiles][py_resource_file], который она скачивает на узел до автоматического выполнения ее командной строки.</span><span class="sxs-lookup"><span data-stu-id="9243a-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="9243a-282">В этом примере каждая задача обрабатывает только один файл.</span><span class="sxs-lookup"><span data-stu-id="9243a-282">In the sample, each task processes only one file.</span></span> <span data-ttu-id="9243a-283">Поэтому его коллекция ResourceFiles содержит один элемент.</span><span class="sxs-lookup"><span data-stu-id="9243a-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in the collection to the specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID of the job to which to add the tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: The ID of an Azure Blob storage container to
    which the tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    the specified Azure Blob storage container.
    """

    print('Adding {} tasks to job [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="9243a-284">При получении доступа к переменным среды, таким как `$AZ_BATCH_NODE_SHARED_DIR`, или выполнении приложения, которое не находится в `PATH` на узле, командные строки задачи должны явным образом вызвать оболочку, например с помощью `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="9243a-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in the node's `PATH`, task command lines must invoke the shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="9243a-285">Это требование не является обязательным, если задачи выполняют приложение в `PATH` и не ссылаются на переменные среды.</span><span class="sxs-lookup"><span data-stu-id="9243a-285">This requirement is unnecessary if your tasks execute an application in the node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="9243a-286">В пределах цикла `for` в приведенном выше фрагменте кода видно, что командная строка задачи построена с использованием пяти аргументов командной строки, передаваемых в *python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="9243a-286">Within the `for` loop in the code snippet above, you can see that the command line for the task is constructed with five command-line arguments that are passed to *python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="9243a-287">**filepath**— это локальный путь к файлу, по которому его можно найти на узле.</span><span class="sxs-lookup"><span data-stu-id="9243a-287">**filepath**: This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="9243a-288">Когда объект ResourceFile создавался в `upload_file_to_container` на шаге 2 выше, для этого свойства использовалось имя файла (в конструкторе ResourceFile в параметре `file_path`).</span><span class="sxs-lookup"><span data-stu-id="9243a-288">When the ResourceFile object in `upload_file_to_container` was created in Step 2 above, the file name was used for this property (the `file_path` parameter in the ResourceFile constructor).</span></span> <span data-ttu-id="9243a-289">Это значит, что файл находится в том же каталоге на узле, что и *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="9243a-289">This indicates that the file can be found in the same directory on the node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="9243a-290">**numwords**указывает *N* наиболее часто используемых слов, которые должны быть записаны в выходной файл.</span><span class="sxs-lookup"><span data-stu-id="9243a-290">**numwords**: The top *N* words should be written to the output file.</span></span>
3. <span data-ttu-id="9243a-291">**storageaccount**— имя учетной записи службы хранилища, которой принадлежит контейнер, куда следует передать выходные данные задач.</span><span class="sxs-lookup"><span data-stu-id="9243a-291">**storageaccount**: The name of the Storage account that owns the container to which the task output should be uploaded.</span></span>
4. <span data-ttu-id="9243a-292">**storagecontainer**— имя контейнера службы хранилища, в который следует передать выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="9243a-292">**storagecontainer**: The name of the Storage container to which the output files should be uploaded.</span></span>
5. <span data-ttu-id="9243a-293">**sastoken** — это подписанный URL-адрес (SAS), который предоставляет доступ на запись в контейнер **output** в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-293">**sastoken**: The shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="9243a-294">Скрипт *python_tutorial_task.py* использует подписанный URL-адрес при создании ссылки на BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="9243a-294">The *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="9243a-295">Это обеспечивает доступ на запись в контейнер без ключа доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9243a-295">This provides write access to the container without requiring an access key for the storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create the blob client using the container's SAS token.
# This allows us to create a client that provides write
# access only to the container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="9243a-296">Шаг 6. Мониторинг задач</span><span class="sxs-lookup"><span data-stu-id="9243a-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="9243a-297">![Мониторинг задач][6]</span><span class="sxs-lookup"><span data-stu-id="9243a-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="9243a-298">
*Скрипт (1) выполняет мониторинг задач и состояния их выполнения, а задачи (2) отправляют данные результатов в службу хранилища Azure*</span><span class="sxs-lookup"><span data-stu-id="9243a-298">
*The script (1) monitors the tasks for completion status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="9243a-299">Добавленные в задание задачи автоматически выстраиваются в очередь и планируются для выполнения на вычислительных узлах пула, связанного с заданием.</span><span class="sxs-lookup"><span data-stu-id="9243a-299">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="9243a-300">Пакетная служба обрабатывает постановку задач в очередь, их планирование извлечение и другие задачи администрирования с учетом указанных вами параметров.</span><span class="sxs-lookup"><span data-stu-id="9243a-300">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="9243a-301">Есть несколько подходов к отслеживанию выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="9243a-301">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="9243a-302">Функция `wait_for_tasks_to_complete` в *python_tutorial_client.py* является простым примером мониторинга определенного состояния задач, в этом случае — [выполненного][py_taskstate] состояния.</span><span class="sxs-lookup"><span data-stu-id="9243a-302">The `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, the [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in the specified job reach the Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The id of the job whose tasks should be to monitored.
    :param timedelta timeout: The duration to wait for task completion. If all
    tasks in the specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="9243a-303">Шаг 7. Загрузка выходных данных задачи</span><span class="sxs-lookup"><span data-stu-id="9243a-303">Step 7: Download task output</span></span>
<span data-ttu-id="9243a-304">![Загрузка выходных данных задачи из службы хранилища][7]</span><span class="sxs-lookup"><span data-stu-id="9243a-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="9243a-305">Теперь, когда задание выполнено, можно загрузить выходные данные задач из службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9243a-305">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="9243a-306">Для этого нужно вызвать `download_blobs_from_container` в *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="9243a-306">This is done with a call to `download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from the specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: The Azure Blob storage container from which to
     download files.
    :param directory_path: The local directory to which to download the files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] to {}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="9243a-307">При вызове `download_blobs_from_container` в *python_tutorial_client.py* указывается, что файлы необходимо скачивать в корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="9243a-307">The call to `download_blobs_from_container` in *python_tutorial_client.py* specifies that the files should be downloaded to your home directory.</span></span> <span data-ttu-id="9243a-308">Вы можете изменить это расположение выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9243a-308">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="9243a-309">Шаг 8. Удаление контейнеров</span><span class="sxs-lookup"><span data-stu-id="9243a-309">Step 8: Delete containers</span></span>
<span data-ttu-id="9243a-310">Так как вы платите за данные, которые находятся в службе хранилища Azure, рекомендуется всегда удалять все большие двоичные объекты, которые больше не нужны для выполнения заданий пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-310">Because you are charged for data that resides in Azure Storage, it is always a good idea to remove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="9243a-311">В *python_tutorial_client.py* это можно сделать, вызвав [BlockBlobService.delete_container][py_delete_container] трижды:</span><span class="sxs-lookup"><span data-stu-id="9243a-311">In *python_tutorial_client.py*, this is done with three calls to [BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="9243a-312">Шаг 9. Удаление задания и пула</span><span class="sxs-lookup"><span data-stu-id="9243a-312">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="9243a-313">На последнем шаге появляется запрос на удаление пула и задания, созданных скриптом *python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="9243a-313">In the final step, you are prompted to delete the job and the pool that were created by the *python_tutorial_client.py* script.</span></span> <span data-ttu-id="9243a-314">Хотя вы и не платите за задания и задачи, *взимается* плата за используемые вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="9243a-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="9243a-315">Поэтому рекомендуется выделять узлы только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9243a-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="9243a-316">Удаление неиспользуемых пулов может быть частью процесса обслуживания.</span><span class="sxs-lookup"><span data-stu-id="9243a-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="9243a-317">Свойства [JobOperations][py_job] и [PoolOperations BatchServiceClient][py_pool] предусматривают соответствующие методы удаления, которые вызываются, если подтвердить удаление.</span><span class="sxs-lookup"><span data-stu-id="9243a-317">The BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if the user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="9243a-318">Помните, что вы платите за использование вычислительных ресурсов, поэтому удаление неиспользуемых пулов позволит сократить затраты.</span><span class="sxs-lookup"><span data-stu-id="9243a-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="9243a-319">Также не забывайте, что при удалении пула удаляются все вычислительные узлы этого пула, после чего все данные на узлах уже нельзя будет восстановить.</span><span class="sxs-lookup"><span data-stu-id="9243a-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-sample-script"></a><span data-ttu-id="9243a-320">Запуск примера сценария</span><span class="sxs-lookup"><span data-stu-id="9243a-320">Run the sample script</span></span>
<span data-ttu-id="9243a-321">При запуске скрипта *python_tutorial_client.py* из [примера кода][github_article_samples] в руководстве консоль будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9243a-321">When you run the *python_tutorial_client.py* script from the tutorial [code sample][github_article_samples], the console output is similar to the following.</span></span> <span data-ttu-id="9243a-322">Во время создания и запуска вычислительных узлов пула, а также выполнения команд в рамках его задачи запуска выполнение приостанавливается на `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` .</span><span class="sxs-lookup"><span data-stu-id="9243a-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while the pool's compute nodes are created, started, and the commands in the pool's start task are executed.</span></span> <span data-ttu-id="9243a-323">Используйте [портал Azure][azure_portal] для мониторинга пула, вычислительных узлов, заданий и задач во время и после выполнения.</span><span class="sxs-lookup"><span data-stu-id="9243a-323">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="9243a-324">Используйте [портал Azure][azure_portal] или [обозреватель службы хранилища Microsoft Azure][storage_explorer], чтобы просматривать ресурсы службы хранилища (контейнеры и большие двоичные объекты), созданные приложением.</span><span class="sxs-lookup"><span data-stu-id="9243a-324">Use the [Azure portal][azure_portal] or the [Microsoft Azure Storage Explorer][storage_explorer] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

> [!TIP]
> <span data-ttu-id="9243a-325">Выполните скрипт *python_tutorial_client.py* в каталоге `azure-batch-samples/Python/Batch/article_samples`.</span><span class="sxs-lookup"><span data-stu-id="9243a-325">Run the *python_tutorial_client.py* script from within the `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="9243a-326">Он использует относительный путь для импорта модуля `common.helpers`, поэтому, если не выполнить скрипт в этом каталоге, может возникнуть ошибка `ImportError: No module named 'common'`.</span><span class="sxs-lookup"><span data-stu-id="9243a-326">It uses a relative path for the `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run the script from within this directory.</span></span>
>
>

<span data-ttu-id="9243a-327">Обычное время выполнения — **примерно 5–7 минут** , если для примера задана конфигурация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9243a-327">Typical execution time is **approximately 5-7 minutes** when you run the sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py to container [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt to container [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks to job [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached the 'Completed' state within the specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] to /home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] to /home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] to /home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="9243a-328">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9243a-328">Next steps</span></span>
<span data-ttu-id="9243a-329">Вы можете внести изменения в *python_tutorial_client.py* и *python_tutorial_task.py*, чтобы поэкспериментировать с различными вычислительными сценариями.</span><span class="sxs-lookup"><span data-stu-id="9243a-329">Feel free to make changes to *python_tutorial_client.py* and *python_tutorial_task.py* to experiment with different compute scenarios.</span></span> <span data-ttu-id="9243a-330">Например, попробуйте добавить задержку выполнения в *python_tutorial_task.py*, чтобы сымитировать длительно выполняемые задачи и следить за ними на портале.</span><span class="sxs-lookup"><span data-stu-id="9243a-330">For example, try adding an execution delay to *python_tutorial_task.py* to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="9243a-331">Попробуйте добавить дополнительные задачи или изменить количество вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9243a-331">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="9243a-332">Добавьте логику для проверки и разрешите использование существующего пула, чтобы сократить время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9243a-332">Add logic to check for and allow the use of an existing pool to speed execution time.</span></span>

<span data-ttu-id="9243a-333">Теперь, когда вы знакомы с основным рабочим процессом решения пакетной службы, пришло время подробно изучить дополнительные возможности пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9243a-333">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="9243a-334">Если вы недавно используете пакетную службу, рекомендуем прочитать статью [с обзором функций пакетной службы Azure](batch-api-basics.md) .</span><span class="sxs-lookup"><span data-stu-id="9243a-334">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="9243a-335">Ознакомьтесь с другими статьями на тему разработки в пакетной службе в разделе **Подробные сведения о разработке** на [схеме обучения "Пакетная служба"][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="9243a-335">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="9243a-336">Ознакомьтесь с другими способами обработки рабочей нагрузки "N часто употребляемых слов" с помощью пакетной службы на примере [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="9243a-336">Check out a different implementation of processing the "top N words" workload with Batch in the [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Создание контейнеров в службе хранилища Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Отправка файлов приложения и входных данных в контейнеры"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Создание пула пакетной службы"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Создание задания пакетной службы"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Добавление задач в задание"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Мониторинг задач"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Скачивание выходных данных задачи из службы хранилища"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Рабочий процесс решения пакетной службы (полная схема)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Учетные данные пакетной службы на портале"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Учетные данные службы хранилища на портале"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Рабочий процесс решения пакетной службы (сокращенная схема)"
