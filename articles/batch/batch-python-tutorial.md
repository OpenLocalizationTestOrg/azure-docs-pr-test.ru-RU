---
title: "aaaTutorial - использование hello Azure пакета SDK для Python | Документы Microsoft"
description: "Изучите основные понятия hello пакетной службы Azure и создайте простое решение, с помощью Python."
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
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="9afea-103">Начало работы с hello пакета SDK для Python</span><span class="sxs-lookup"><span data-stu-id="9afea-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9afea-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9afea-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="9afea-105">Python</span><span class="sxs-lookup"><span data-stu-id="9afea-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="9afea-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="9afea-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="9afea-107">Основы hello объекта [пакетной службы Azure] [ azure_batch] и hello [пакета Python] [ py_azure_sdk] клиента в обсуждении небольшой пакет приложения, написанного на Python.</span><span class="sxs-lookup"><span data-stu-id="9afea-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="9afea-108">Рассматривается, как эти два примера скриптов используйте hello пакетной службы tooprocess параллельной рабочей нагрузки на виртуальных машинах Linux в облаке hello и их взаимодействие с [хранилища Azure](../storage/common/storage-introduction.md) для файла промежуточного хранения и извлечения.</span><span class="sxs-lookup"><span data-stu-id="9afea-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="9afea-109">Будет узнать общий рабочий процесс приложения пакета и получить представление о базовых hello основных компонентов пакета, например заданий, задач, пулы и вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9afea-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="9afea-110">![Рабочий процесс решения пакетной службы (основной)][11]</span><span class="sxs-lookup"><span data-stu-id="9afea-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="9afea-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9afea-111">Prerequisites</span></span>
<span data-ttu-id="9afea-112">В этой статье предполагается, что вы уже работали с Python и знаете, как работать в Linux.</span><span class="sxs-lookup"><span data-stu-id="9afea-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="9afea-113">Также предполагается, что вы будете требования к создания может toosatisfy hello учетной записи, указанные ниже для Azure и пакета hello и служб хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afea-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="9afea-114">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="9afea-114">Accounts</span></span>
* <span data-ttu-id="9afea-115">**Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="9afea-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="9afea-116">**Учетная запись пакетной службы**. Если у вас есть подписка Azure, [создайте учетную запись пакетной службы Azure](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="9afea-117">**Учетная запись хранения**. См. раздел [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="9afea-118">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9afea-118">Code sample</span></span>
<span data-ttu-id="9afea-119">Учебник Python Hello [образец кода] [ github_article_samples] является одним из hello найти множество образцов кода пакета в hello [образцы azure пакета] [ github_samples] репозитория на GitHub.</span><span class="sxs-lookup"><span data-stu-id="9afea-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="9afea-120">Можно загрузить все образцы hello, щелкнув **клон или загрузки > загрузить ZIP** на домашней странице hello репозитория или щелкнув hello [azure пакета образцы master.zip] [ github_samples_zip]прямой ссылкой скачивания.</span><span class="sxs-lookup"><span data-stu-id="9afea-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="9afea-121">Как только вы извлекли содержимое hello hello ZIP-файл, hello двух сценариев в этом учебнике можно найти на hello `article_samples` каталога:</span><span class="sxs-lookup"><span data-stu-id="9afea-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="9afea-122">Среда Python</span><span class="sxs-lookup"><span data-stu-id="9afea-122">Python environment</span></span>
<span data-ttu-id="9afea-123">toorun hello *python_tutorial_client.py* образец скрипта на локальной рабочей станции, необходимо **интерпретатор Python** совместим с версией **2.7** или **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="9afea-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="9afea-124">Hello сценарий протестирован на Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="9afea-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="9afea-125">Зависимости шифрования</span><span class="sxs-lookup"><span data-stu-id="9afea-125">cryptography dependencies</span></span>
<span data-ttu-id="9afea-126">Необходимо установить зависимости hello для hello [криптографии] [ crypto] библиотеки, необходимые для hello `azure-batch` и `azure-storage` пакеты Python.</span><span class="sxs-lookup"><span data-stu-id="9afea-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="9afea-127">Выполните одно из следующих операций, подходящих для вашей платформы hello, или ссылается toohello [установки криптографии] [ crypto_install] Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="9afea-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="9afea-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9afea-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="9afea-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="9afea-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="9afea-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="9afea-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="9afea-131">Windows</span><span class="sxs-lookup"><span data-stu-id="9afea-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="9afea-132">При установке для Python 3.3 + в Linux, используйте hello python3 эквиваленты для hello Python зависимостей.</span><span class="sxs-lookup"><span data-stu-id="9afea-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="9afea-133">Например, в Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="9afea-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="9afea-134">Пакеты Azure</span><span class="sxs-lookup"><span data-stu-id="9afea-134">Azure packages</span></span>
<span data-ttu-id="9afea-135">После этого установите hello **пакетной службы Azure** и **хранилища Azure** пакеты Python.</span><span class="sxs-lookup"><span data-stu-id="9afea-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="9afea-136">Можно установить оба пакета с помощью **pip** и hello *requirements.txt* по следующему адресу:</span><span class="sxs-lookup"><span data-stu-id="9afea-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="9afea-137">Следующие проблемы **pip** команды tooinstall hello пакета и хранения пакетов:</span><span class="sxs-lookup"><span data-stu-id="9afea-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="9afea-138">Кроме того, можно установить hello [пакета azure] [ pypi_batch] и [хранилища azure] [ pypi_storage] Python пакетов вручную:</span><span class="sxs-lookup"><span data-stu-id="9afea-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="9afea-139">Если вы используете непривилегированной учетной записи, может потребоваться tooprefix команды с `sudo`.</span><span class="sxs-lookup"><span data-stu-id="9afea-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="9afea-140">Например, `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="9afea-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="9afea-141">Дополнительные сведения об установке пакетов Python см. в статье [Installing Packages][pypi_install] (Установка пакетов) на сайте python.org.</span><span class="sxs-lookup"><span data-stu-id="9afea-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="9afea-142">Пример кода Python для руководства по пакетной службе</span><span class="sxs-lookup"><span data-stu-id="9afea-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="9afea-143">Образец учебника код пакета Python Hello состоит из двух сценариев Python и несколько файлов данных.</span><span class="sxs-lookup"><span data-stu-id="9afea-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="9afea-144">**python_tutorial_client.py**: взаимодействует с tooexecute hello пакета и хранилище служб параллельной рабочей нагрузки на вычислительных узлов (виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="9afea-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="9afea-145">Hello *python_tutorial_client.py* сценарий выполняется на локальной рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="9afea-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="9afea-146">**python_tutorial_task.py**: hello сценарий, запускаемый на вычислительных узлов в Azure tooperform hello фактическую работу.</span><span class="sxs-lookup"><span data-stu-id="9afea-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="9afea-147">В образце hello *python_tutorial_task.py* анализирует hello текст в файл, загруженный из хранилища Azure (hello входного файла).</span><span class="sxs-lookup"><span data-stu-id="9afea-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="9afea-148">Затем он создает текстовый файл (hello выходной файл), содержащий список hello первых трех слов, которые содержатся во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="9afea-149">После создания выходного файла hello, *python_tutorial_task.py* передач hello tooAzure файла хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afea-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="9afea-150">Это делает доступными для загрузки toohello клиента скрипт, выполняемый на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="9afea-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="9afea-151">Hello *python_tutorial_task.py* сценарий выполняется параллельно на нескольких вычислительных узлов в hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="9afea-152">**./Data/taskdata\*.txt**: эти три текстовых файлов ввода hello для hello задач, выполняемых на hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9afea-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="9afea-153">Привет, следующая схема иллюстрирует hello основных операций, выполняемых скриптов клиента "и" задача hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="9afea-154">Этот основной рабочий процесс является типичным для многих вычислительных решений, созданных с помощью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="9afea-155">Хотя здесь не показаны каждый компонент, доступный в hello пакетная служба, практически все пакета сценарий включает некоторые части этого рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="9afea-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="9afea-156">![Пример рабочего процесса пакетной службы][8]</span><span class="sxs-lookup"><span data-stu-id="9afea-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="9afea-157">**Шаг 1.**</span><span class="sxs-lookup"><span data-stu-id="9afea-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="9afea-158">Создайте **контейнеры** в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="9afea-159">
[**Шаг 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="9afea-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="9afea-160">Отправьте toocontainers задачи скрипта и входные файлы.</span><span class="sxs-lookup"><span data-stu-id="9afea-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="9afea-161">
[**Шаг 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="9afea-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="9afea-162">Создайте **пул** пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="9afea-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="9afea-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="9afea-164">Здравствуйте, пул **StartTask** загрузки hello toonodes Задача сценария (python_tutorial_task.py), которые они присоединиться к пулу hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="9afea-165">
[**Шаг 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="9afea-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="9afea-166">Создайте **задание** пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="9afea-167">
[**Шаг 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="9afea-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="9afea-168">Добавить **задачи** toohello задания.</span><span class="sxs-lookup"><span data-stu-id="9afea-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="9afea-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="9afea-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="9afea-170">Hello задачи, запланированные tooexecute на узлах.</span><span class="sxs-lookup"><span data-stu-id="9afea-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="9afea-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="9afea-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="9afea-172">Каждая задача скачивает свои входные данные из службы хранилища Azure, а затем начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="9afea-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="9afea-173">
[**Шаг 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="9afea-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="9afea-174">Мониторинг задач.</span><span class="sxs-lookup"><span data-stu-id="9afea-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="9afea-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="9afea-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="9afea-176">Как выполнить действия, они отправляют их вывода данных tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afea-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="9afea-177">
[**Шаг 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="9afea-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="9afea-178">Скачайте выходные данные задачи из службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afea-178">Download task output from Storage.</span></span>

<span data-ttu-id="9afea-179">Как уже упоминалось, не каждое решение пакетной службы будет выполнять именно эти шаги. Некоторые решения могут выполнять больше действий, но этот пример демонстрирует общие процессы в решении пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="9afea-180">Подготовка сценария клиента</span><span class="sxs-lookup"><span data-stu-id="9afea-180">Prepare client script</span></span>
<span data-ttu-id="9afea-181">Перед запуском образца hello, необходимо добавить учетные данные учетной записи пакета и хранилища слишком*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="9afea-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="9afea-182">Если вы еще не сделали этого, откройте файл hello в вашей избранные редактор и обновление hello следующие строки с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="9afea-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="9afea-183">Пакет и хранения учетные данные учетной записи в колонке hello учетной записи каждой службы можно найти в hello [портал Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="9afea-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="9afea-184">![Пакетное учетные данные на портале hello][9]
![учетные данные хранилища на портале hello][10]</span><span class="sxs-lookup"><span data-stu-id="9afea-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="9afea-185">В следующих разделах hello, анализируются hello шагов, используемых hello скрипты tooprocess рабочую нагрузку в hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="9afea-186">Мы рекомендуем вам регулярно toorefer toohello сценариев в редакторе, используемом во время продвигайтесь hello оставшейся части статьи hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="9afea-187">Перейдите следующей строкой в toohello **python_tutorial_client.py** toostart с шага 1:</span><span class="sxs-lookup"><span data-stu-id="9afea-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="9afea-188">Шаг 1. Создание контейнеров службы хранилища</span><span class="sxs-lookup"><span data-stu-id="9afea-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="9afea-189">![Создание контейнеров в службе хранилища Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="9afea-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="9afea-190">Пакетная служба включает встроенную поддержку для взаимодействия со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="9afea-191">Контейнеры в учетной записи хранилища обеспечивают hello файлов, необходимых hello задач, которые выполняются в вашей учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="9afea-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="9afea-192">контейнеры Hello также обеспечивают месте toostore hello выходные данные задачи hello выдавать.</span><span class="sxs-lookup"><span data-stu-id="9afea-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="9afea-193">Здравствуйте, первое, что hello *python_tutorial_client.py* сценарий выполняет создают три контейнера в [хранилища больших двоичных объектов](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="9afea-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="9afea-194">**приложение**: этот контейнер будет хранить hello Python сценариев, запускаемых задач hello *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="9afea-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="9afea-195">**входной**: задачи будут загружены файлы tooprocess hello данных с hello *ввода* контейнера.</span><span class="sxs-lookup"><span data-stu-id="9afea-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="9afea-196">**выходные данные**: после завершения выполнения задач обработки входных файлов они загрузит hello результаты toohello *вывода* контейнера.</span><span class="sxs-lookup"><span data-stu-id="9afea-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="9afea-197">В порядке toointeract с хранилищем учетной записи и создавать контейнеры, мы используем hello [хранилища azure] [ pypi_storage] пакета toocreate [BlockBlobService] [ py_blockblobservice] объект — hello «большой двоичный объект клиент».</span><span class="sxs-lookup"><span data-stu-id="9afea-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="9afea-198">Затем создадим три контейнера в учетной записи хранения hello, с помощью клиента hello BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="9afea-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="9afea-199">После создания контейнеров hello приложения hello, теперь можно отправить hello файлы, которые будут использоваться задачами hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="9afea-200">[Как toouse хранилища больших двоичных объектов Azure в Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) хороший Обзор работы с контейнеров хранилища Azure и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9afea-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="9afea-201">В начале работы с использованием пакета должно быть hello верхней части списка для чтения.</span><span class="sxs-lookup"><span data-stu-id="9afea-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="9afea-202">Шаг 2. Отправка сценария задач и файлов данных</span><span class="sxs-lookup"><span data-stu-id="9afea-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="9afea-203">![Задача передачи приложения и ввода (данных) файлы toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="9afea-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="9afea-204">В файле hello операции, передачи *python_tutorial_client.py* сначала определяет коллекции **приложения** и **ввода** пути к файлам, в котором они хранятся на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="9afea-205">Затем он передает эти контейнеры toohello файлы, созданные на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="9afea-206">Здравствуйте, используя охватом списка, `upload_file_to_container` функция вызывается для каждого файла в hello коллекций и двух [ResourceFile] [ py_resource_file] заполняются коллекций.</span><span class="sxs-lookup"><span data-stu-id="9afea-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="9afea-207">Hello `upload_file_to_container` функция появляется ниже:</span><span class="sxs-lookup"><span data-stu-id="9afea-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
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

### <a name="resourcefiles"></a><span data-ttu-id="9afea-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="9afea-208">ResourceFiles</span></span>
<span data-ttu-id="9afea-209">Объект [ResourceFile] [ py_resource_file] предоставляет задачи в пакете с файлом tooa hello URL-адрес в службе хранилища Azure, загруженные tooa вычислительный узел перед запуском этой задачи.</span><span class="sxs-lookup"><span data-stu-id="9afea-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="9afea-210">Hello [ResourceFile][py_resource_file]. **blob_source** свойство указывает hello полный URL-адрес файла hello, которое существовало в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="9afea-211">Hello URL-адрес может также включать подписанного URL-адреса (SAS), предоставляющий безопасный доступ toohello файла.</span><span class="sxs-lookup"><span data-stu-id="9afea-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="9afea-212">Большинство типов задач в пакетной службе, в том числе перечисленные ниже, содержат свойство *ResourceFiles* .</span><span class="sxs-lookup"><span data-stu-id="9afea-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="9afea-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="9afea-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="9afea-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="9afea-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="9afea-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="9afea-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="9afea-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="9afea-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="9afea-217">Этот образец не использует hello JobPreparationTask или JobReleaseTask типы задач, но вы можете прочитать больше о них в [выполнения задания Подготовка и выполнение задач в пакете Azure вычислительные узлы](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="9afea-218">Подписанный URL-адрес (SAS)</span><span class="sxs-lookup"><span data-stu-id="9afea-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="9afea-219">Подписи общего доступа являются строки, которые обеспечивают безопасный доступ toocontainers и больших двоичных объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="9afea-220">Hello *python_tutorial_client.py* скрипт использует оба большого двоичного объекта и контейнера подписи коллективного доступа, а также показано, как эти общие tooobtain доступ к строки подписи из hello службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afea-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="9afea-221">**BLOB-объектов подписи коллективного доступа**: hello пула StartTask использует BLOB-объектов подписи коллективного доступа при загрузке hello задачи скрипта и входные файлы данных из хранилища (в разделе [шаг 3](#step-3-create-batch-pool) ниже).</span><span class="sxs-lookup"><span data-stu-id="9afea-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="9afea-222">Hello `upload_file_to_container` функционировать в *python_tutorial_client.py* содержит hello код, который получает подпись общего доступа для каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9afea-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="9afea-223">Это достигается путем вызова [BlockBlobService.make_blob_url] [ py_make_blob_url] в модуле хранения hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="9afea-224">**Подписанный URL-адрес контейнера**: как каждая задача завершит свою работу на вычислительном узле hello, передает его выходной файл toohello *вывода* контейнера в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="9afea-225">toodo таким образом, *python_tutorial_task.py* используется подпись общего доступа контейнера, которая предоставляет доступ на запись toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="9afea-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="9afea-226">Hello `get_container_sas_token` функционировать в *python_tutorial_client.py* получает hello контейнер подписанный URL-адрес, который затем передается как аргумент командной строки toohello задачи.</span><span class="sxs-lookup"><span data-stu-id="9afea-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="9afea-227">Шаг #5 [добавить задачи tooa задания](#step-5-add-tasks-to-job), рассматривается использование hello hello SAS контейнера.</span><span class="sxs-lookup"><span data-stu-id="9afea-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="9afea-228">Извлечение серии из двух частей hello подписей общего доступа [часть 1: Общие сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) и [часть 2: создать и использовать SAS с hello службы BLOB-объектов](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn Дополнительные сведения о предоставления безопасного доступа toodata вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afea-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="9afea-229">Шаг 3. Создание пула пакетной службы</span><span class="sxs-lookup"><span data-stu-id="9afea-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="9afea-230">![Создание пула пакетной службы][3]
</span><span class="sxs-lookup"><span data-stu-id="9afea-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="9afea-231">**Пул** пакетной службы — это коллекция вычислительных узлов (виртуальных машин), на которых пакетная служба выполняет задачи задания.</span><span class="sxs-lookup"><span data-stu-id="9afea-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="9afea-232">После передает hello задач сценариев и данных файлов toohello учетной записи хранилища, *python_tutorial_client.py* запускает его взаимодействия с hello пакетной службы с помощью модуля hello пакета Python.</span><span class="sxs-lookup"><span data-stu-id="9afea-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="9afea-233">toodo таким образом, [BatchServiceClient] [ py_batchserviceclient] создается:</span><span class="sxs-lookup"><span data-stu-id="9afea-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="9afea-234">Далее пул вычислительных узлов создается в hello пакетной учетной записи с помощью вызова слишком`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="9afea-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
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

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
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

<span data-ttu-id="9afea-235">При создании пула определяется [PoolAddParameter] [ py_pooladdparam] , указывающий несколько свойств пула hello:</span><span class="sxs-lookup"><span data-stu-id="9afea-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="9afea-236">**Идентификатор** hello пула (*идентификатор* — требуется)</span><span class="sxs-lookup"><span data-stu-id="9afea-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="9afea-237">Как и у большинства сущностей в пакетной службе, у нового пула должен быть идентификатор, уникальный в учетной записи этой службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="9afea-238">Ваш код ссылается с помощью его идентификатора пула toothis, и именно вы идентифицируете пула hello в hello Azure [портала][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="9afea-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="9afea-239">**Количество вычислительных узлов** (*target_dedicated*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9afea-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="9afea-240">Это свойство определяет, сколько виртуальных машин должны развертываться в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="9afea-241">Является важным toonote, что все учетные записи пакетного имеют значение по умолчанию **квоты** hello, ограничения числа **ядер** (и, таким образом, вычислительных узлов) в учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="9afea-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="9afea-242">Можно найти квот по умолчанию hello и инструкции о том, как слишком[увеличить квоту](batch-quota-limit.md#increase-a-quota) (таких как максимальное количество ядер в вашей учетной записи пакетного hello) в [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="9afea-243">Если возник вопрос о том, почему пул не использует больше определенного количества узлов,</span><span class="sxs-lookup"><span data-stu-id="9afea-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="9afea-244">Эта квота ядра может быть причиной hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="9afea-245">**Операционная система** для узлов (*virtual_machine_configuration* **или** *cloud_service_configuration*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9afea-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="9afea-246">В *python_tutorial_client.py* мы создаем пул узлов Linux с использованием [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="9afea-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="9afea-247">Hello `select_latest_verified_vm_image_with_node_agent_sku` функционировать в `common.helpers` упрощает работу с [виртуальных машин Azure Marketplace] [ vm_marketplace] изображения.</span><span class="sxs-lookup"><span data-stu-id="9afea-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="9afea-248">Дополнительные сведения об использовании образов из магазина см. в статье [Подготовка вычислительных узлов Linux в пулах пакетной службы Azure](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="9afea-249">**Размер вычислительных узлов** (*vm_size*, обязательное).</span><span class="sxs-lookup"><span data-stu-id="9afea-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="9afea-250">Так как мы указываем узлы Linux для [VirtualMachineConfiguration][py_vm_config], необходимо указать их размер (в этом примере — `STANDARD_A1`), как описано в статье [Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9afea-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9afea-251">Дополнительные сведения см. в статье [Подготовка вычислительных узлов Linux в пулах пакетной службы Azure](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="9afea-252">**Задача запуска** (*start_task*, не обязательное).</span><span class="sxs-lookup"><span data-stu-id="9afea-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="9afea-253">Вместе с hello выше свойства физического узла, можно также указать [StartTask] [ py_starttask] для пула hello (не требуется).</span><span class="sxs-lookup"><span data-stu-id="9afea-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="9afea-254">Hello StartTask выполняет на каждом узле, как этот узел соединяет hello пул, и каждый раз при перезапуске узла.</span><span class="sxs-lookup"><span data-stu-id="9afea-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="9afea-255">Hello StartTask особенно полезна для подготовки вычислительных узлов для выполнения задач, таких как установка приложения hello, выполняющиеся задачи hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="9afea-256">В этом образце приложения hello StartTask копирует hello файлы, загружаемые из хранилища (которые указываются с помощью hello StartTask **resource_files** свойство) из hello StartTask *рабочий каталог* toohello *общего* каталог, в котором доступны все задачи, выполняемые на узле hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="9afea-257">По сути, это копирует `python_tutorial_task.py` toohello каталог общих на каждый узел при присоединении узла hello пула hello доступа к ней все задачи, выполняемых в узле hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="9afea-258">Вы можете заметить hello вызовов toohello `wrap_commands_in_shell` вспомогательную функцию.</span><span class="sxs-lookup"><span data-stu-id="9afea-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="9afea-259">Она использует коллекцию отдельных команд и создает одну соответствующую командную строку для свойства командной строки задачи.</span><span class="sxs-lookup"><span data-stu-id="9afea-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="9afea-260">Также значительным в приведенном выше фрагменте кода hello используется hello двух переменных среды в hello **командная_строка** свойство hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` и `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="9afea-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="9afea-261">Несколько переменных среды, которые являются определенной tooBatch автоматически настраивается каждом вычислительном узле в пуле пакета.</span><span class="sxs-lookup"><span data-stu-id="9afea-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="9afea-262">Любой процесс, выполняемый задачей имеет доступ к переменным среды toothese.</span><span class="sxs-lookup"><span data-stu-id="9afea-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="9afea-263">toofind Дополнительные сведения о переменных среды hello, доступные на вычислительных узлах пула, а также сведения о задаче рабочие каталоги, в разделе **параметры среды для задачи** и **файлов и каталогов**  в hello [Обзор возможностей пакетной службы Azure](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="9afea-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="9afea-264">Шаг 4. Создание задания пакетной службы</span><span class="sxs-lookup"><span data-stu-id="9afea-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="9afea-265">![Создание задания пакетной службы][4]</span><span class="sxs-lookup"><span data-stu-id="9afea-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="9afea-266">**Задание** пакетной службы — это коллекция задач, связанных с пулом вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9afea-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="9afea-267">Hello задачи в задании, выполняются в hello связанный пул вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9afea-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="9afea-268">Задания можно использовать не только для упорядочивания и отслеживания задач в связанных рабочих нагрузок, но также и для налагающий определенные ограничения, например hello максимального времени для задания hello (и по расширению, его задачи) и приоритет задания в заданиях tooother отношения в hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9afea-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="9afea-269">В этом примере задание hello связаны только с пулом hello, который был создан на шаге #3.</span><span class="sxs-lookup"><span data-stu-id="9afea-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="9afea-270">Дополнительные свойства не настроены.</span><span class="sxs-lookup"><span data-stu-id="9afea-270">No additional properties are configured.</span></span>

<span data-ttu-id="9afea-271">Все задания пакетной службы связаны с конкретным пулом.</span><span class="sxs-lookup"><span data-stu-id="9afea-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="9afea-272">Эта связь указывает, какие задачи hello задания выполняются в узлы.</span><span class="sxs-lookup"><span data-stu-id="9afea-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="9afea-273">Укажите hello пула с помощью hello [PoolInformation] [ py_poolinfo] свойства, как показано в приведенном ниже фрагменте кода hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
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

<span data-ttu-id="9afea-274">После создания задания задачи добавляются рабочие tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="9afea-275">Шаг 5: Добавление toojob задачи</span><span class="sxs-lookup"><span data-stu-id="9afea-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="9afea-276">![Добавление задачи toojob][5]</span><span class="sxs-lookup"><span data-stu-id="9afea-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="9afea-277">
*(1) задачи добавляются toohello задания, (2) hello задачи, запланированные toorun на узлах и (3) hello задачи загрузки tooprocess файлы данных hello*</span><span class="sxs-lookup"><span data-stu-id="9afea-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="9afea-278">Пакет **задачи** являются hello отдельных рабочих элементов, выполните на hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9afea-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="9afea-279">Задача имеет командную строку и выполняется hello сценарии или исполняемые файлы, укажите в этой командной строке.</span><span class="sxs-lookup"><span data-stu-id="9afea-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="9afea-280">tooactually выполнения работы, задачи должны быть добавлены tooa задания.</span><span class="sxs-lookup"><span data-stu-id="9afea-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="9afea-281">Каждый [CloudTask] [ py_task] настраивается с помощью свойства командной строки и [ResourceFiles] [ py_resource_file] (как в случае с StartTask hello пула), hello Задача загружает toohello узла перед его командной строки выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="9afea-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="9afea-282">В образце hello каждая задача обрабатывает только один файл.</span><span class="sxs-lookup"><span data-stu-id="9afea-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="9afea-283">Поэтому его коллекция ResourceFiles содержит один элемент.</span><span class="sxs-lookup"><span data-stu-id="9afea-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

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
> <span data-ttu-id="9afea-284">При доступе переменные среды, такие как `$AZ_BATCH_NODE_SHARED_DIR` или выполнить приложение не найдено в узле hello `PATH`, задача командные строки необходимо вызвать hello оболочки явно, такие как с `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="9afea-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="9afea-285">Это требование не требуется, если задачи Выполнение приложения в узле hello `PATH` и не ссылаться на переменные среды.</span><span class="sxs-lookup"><span data-stu-id="9afea-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="9afea-286">В рамках hello `for` цикла в приведенном выше фрагменте кода hello, можно увидеть, что hello командной строки для задачи «hello» создается пять аргументов командной строки, которые передаются слишком*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="9afea-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="9afea-287">**FILEPATH**: это файл toohello hello локальный путь, поскольку она существует на узле hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="9afea-288">Когда hello объекта ResourceFile в `upload_file_to_container` был создан на шаге 2 выше, имя файла hello был использован для этого свойства (hello `file_path` параметра в конструктор ResourceFile hello).</span><span class="sxs-lookup"><span data-stu-id="9afea-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="9afea-289">Это означает, что этот файл hello можно найти в hello же каталог на узле hello в виде *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="9afea-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="9afea-290">**NUMWORDS**: hello верхней *N* слова должны быть написаны toohello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="9afea-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="9afea-291">**storageaccount**: hello имя учетной записи хранилища, которому принадлежит выходные данные задачи hello контейнера toowhich hello hello должна быть загружена.</span><span class="sxs-lookup"><span data-stu-id="9afea-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="9afea-292">**storagecontainer**: hello имя контейнера toowhich hello хранилища hello вывода файлов должна быть загружена.</span><span class="sxs-lookup"><span data-stu-id="9afea-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="9afea-293">**sastoken**: hello подписанного URL-адреса (SAS), предоставляющий доступ на запись toohello **вывода** контейнера в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="9afea-294">Hello *python_tutorial_task.py* скрипт использует подписанный URL-адрес при создает его BlockBlobService ссылку.</span><span class="sxs-lookup"><span data-stu-id="9afea-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="9afea-295">Это обеспечивает доступ для записи toohello контейнера без использования клавиши доступа для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="9afea-296">Шаг 6. Мониторинг задач</span><span class="sxs-lookup"><span data-stu-id="9afea-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="9afea-297">![Мониторинг задач][6]</span><span class="sxs-lookup"><span data-stu-id="9afea-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="9afea-298">
*Здравствуйте, (1) мониторы hello задачи состояние завершения, а задачи hello (2) добавьте tooAzure результат данных хранилища*</span><span class="sxs-lookup"><span data-stu-id="9afea-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="9afea-299">При добавлении задачи задания tooa они автоматически в очередь и запланировать выполнение на вычислительных узлах пула hello, связанный с заданием hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="9afea-300">В зависимости от настройки hello пакета обрабатывает все очереди задач, планирования, повтор и другие задачи администрирования обязанностей.</span><span class="sxs-lookup"><span data-stu-id="9afea-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="9afea-301">Существует множество подходов toomonitoring выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="9afea-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="9afea-302">Hello `wait_for_tasks_to_complete` функционировать в *python_tutorial_client.py* предоставляет простой пример задач наблюдения для определенного состояния, в данном случае hello [завершения] [ py_taskstate] состояние.</span><span class="sxs-lookup"><span data-stu-id="9afea-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
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

## <a name="step-7-download-task-output"></a><span data-ttu-id="9afea-303">Шаг 7. Загрузка выходных данных задачи</span><span class="sxs-lookup"><span data-stu-id="9afea-303">Step 7: Download task output</span></span>
<span data-ttu-id="9afea-304">![Загрузка выходных данных задачи из службы хранилища][7]</span><span class="sxs-lookup"><span data-stu-id="9afea-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="9afea-305">Теперь, когда hello работа завершена, hello выходные данные задач hello можно загрузить из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9afea-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="9afea-306">Это делается с помощью вызова слишком`download_blobs_from_container` в *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="9afea-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="9afea-307">Здравствуйте вызов слишком`download_blobs_from_container` в *python_tutorial_client.py* указывает, hello файлы должны быть загруженного tooyour домашнего каталога.</span><span class="sxs-lookup"><span data-stu-id="9afea-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="9afea-308">Свободное toomodify считаете это расположение выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9afea-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="9afea-309">Шаг 8. Удаление контейнеров</span><span class="sxs-lookup"><span data-stu-id="9afea-309">Step 8: Delete containers</span></span>
<span data-ttu-id="9afea-310">Поскольку плата взимается для данных, которые хранятся в хранилище Azure, это всегда tooremove рекомендуется, когда все большие двоичные объекты, которые больше не нужен для пакетных заданий.</span><span class="sxs-lookup"><span data-stu-id="9afea-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="9afea-311">В *python_tutorial_client.py*, это делается с помощью трех вызовов слишком[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="9afea-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="9afea-312">Шаг 9: Удалить задание hello и hello пула</span><span class="sxs-lookup"><span data-stu-id="9afea-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="9afea-313">В последнем шаге hello, запрашиваемые toodelete hello задания и hello пула, созданных по hello *python_tutorial_client.py* сценария.</span><span class="sxs-lookup"><span data-stu-id="9afea-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="9afea-314">Хотя вы и не платите за задания и задачи, *взимается* плата за используемые вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="9afea-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="9afea-315">Поэтому рекомендуется выделять узлы только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9afea-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="9afea-316">Удаление неиспользуемых пулов может быть частью процесса обслуживания.</span><span class="sxs-lookup"><span data-stu-id="9afea-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="9afea-317">Hello BatchServiceClient [JobOperations] [ py_job] и [PoolOperations] [ py_pool] имеют соответствующих методов удаления, которые являются вызывается, если подтверждение удаления:</span><span class="sxs-lookup"><span data-stu-id="9afea-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="9afea-318">Помните, что вы платите за использование вычислительных ресурсов, поэтому удаление неиспользуемых пулов позволит сократить затраты.</span><span class="sxs-lookup"><span data-stu-id="9afea-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="9afea-319">Кроме того помните, что при удалении пула удаляются все вычислительные узлы этого пула, и все данные на узлах hello будет неустранимой после удаления пула hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="9afea-320">Запустите сценарий образец hello</span><span class="sxs-lookup"><span data-stu-id="9afea-320">Run hello sample script</span></span>
<span data-ttu-id="9afea-321">При запуске hello *python_tutorial_client.py* сценарий из учебника hello [образец кода][github_article_samples], вывод на консоль hello — примерно следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="9afea-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="9afea-322">Нет приостановит `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` пока hello пула вычислительные узлы создаются, запущена, и выполняются команды hello в задачу запуска пула hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="9afea-323">Используйте hello [портал Azure] [ azure_portal] toomonitor пула, вычислительные узлы, заданий и задач во время и после выполнения.</span><span class="sxs-lookup"><span data-stu-id="9afea-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="9afea-324">Используйте hello [портал Azure] [ azure_portal] или hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview ресурсов хранилища hello (контейнеров и больших двоичных объектов) созданные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="9afea-325">Запустите hello *python_tutorial_client.py* сценарий из внутри hello `azure-batch-samples/Python/Batch/article_samples` каталога.</span><span class="sxs-lookup"><span data-stu-id="9afea-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="9afea-326">Он использует относительный путь для hello `common.helpers` импорт модуля, чтобы можно было увидеть `ImportError: No module named 'common'` Если не выполнить скрипт hello из этого каталога.</span><span class="sxs-lookup"><span data-stu-id="9afea-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="9afea-327">Обычно время выполнения равно **приблизительно 5 – 7 минут** при запуске образца hello в конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9afea-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="9afea-328">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9afea-328">Next steps</span></span>
<span data-ttu-id="9afea-329">Чувствовать себя свободного toomake изменения слишком*python_tutorial_client.py* и *python_tutorial_task.py* tooexperiment с различными вычислений сценариев.</span><span class="sxs-lookup"><span data-stu-id="9afea-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="9afea-330">Например, попробуйте добавить задержки выполнения слишком*python_tutorial_task.py* toosimulate длительные задачи, а также отслеживать их на портале hello.</span><span class="sxs-lookup"><span data-stu-id="9afea-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="9afea-331">Попробуйте установить дополнительные задачи или изменить hello количество вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9afea-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="9afea-332">Добавьте toocheck логику для и разрешить использование hello существующих времени выполнения toospeed пула.</span><span class="sxs-lookup"><span data-stu-id="9afea-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="9afea-333">Теперь, когда вы знакомы с hello базовый рабочий процесс пакета решения, это время toodig в дополнительные возможности toohello hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afea-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="9afea-334">Просмотрите hello [возможности пакетной обработки Обзор Azure](batch-api-basics.md) статьи, которая рекомендуется, если вы новую службу toohello.</span><span class="sxs-lookup"><span data-stu-id="9afea-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="9afea-335">Здравствуйте, запуска на другие статьи по разработке пакета в списке **разработки подробные** в hello [план обучения пакета][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="9afea-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="9afea-336">Извлечение другой реализации обработки hello «N основных слова» рабочей нагрузки с использованием пакета в hello [TopNWords] [ github_topnwords] образца.</span><span class="sxs-lookup"><span data-stu-id="9afea-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

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
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Задача передачи приложения и ввода (данных) файлы toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Создание пула пакетной службы"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Создание задания пакетной службы"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Добавление задачи toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Мониторинг задач"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Скачивание выходных данных задачи из службы хранилища"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Рабочий процесс решения пакетной службы (полная схема)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Учетные данные пакетной службы на портале"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Учетные данные службы хранилища на портале"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Рабочий процесс решения пакетной службы (сокращенная схема)"
