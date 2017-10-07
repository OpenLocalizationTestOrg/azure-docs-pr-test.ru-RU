---
title: "пакеты приложений aaaInstall на вычислительных узлах - пакетной службы Azure | Документы Microsoft"
description: "Использовать приложение hello пакеты возможность пакетной службы Azure tooeasily управлять несколькими приложениями и версии для установки пакета вычислительных узлов."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="78f3a-103">Развертывание приложений toocompute узлов с пакетами приложения пакета</span><span class="sxs-lookup"><span data-stu-id="78f3a-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="78f3a-104">компонент пакеты приложения Hello пакетной службы Azure предоставляет удобное управление задач приложений и их развертывания toohello вычислительных узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="78f3a-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="78f3a-105">С помощью пакетов приложений можно загрузить и управления несколькими версиями приложения hello запуска задач, включая их вспомогательные файлы.</span><span class="sxs-lookup"><span data-stu-id="78f3a-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="78f3a-106">Затем можно автоматически развернуть один или несколько из этих приложений toohello вычислительных узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="78f3a-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="78f3a-107">В этой статье вы узнаете, как tooupload пакетов приложений в hello портал Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="78f3a-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="78f3a-108">Затем будет рассмотрено, каким образом tooinstall их в пуле вычислительных узлов с hello [пакета .NET] [ api_net] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="78f3a-109">Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="78f3a-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="78f3a-110">Они поддерживаются в пулах пакета, созданные между 10 марта 2016 г. и 5 июля 2017 г., только в том случае, если пул hello был создан с помощью конфигурации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="78f3a-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="78f3a-111">Пакеты приложений не поддерживают пулы пакета, созданные предыдущей too10 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="78f3a-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="78f3a-112">Hello API-интерфейсы для создания и управления пакетами приложения являются частью hello [пакет управления .NET] [[api_net_mgmt]] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="78f3a-113">Hello API-интерфейсы для установки пакетов приложений в вычислительном узле являются частью hello [пакета .NET] [ api_net] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="78f3a-114">функция пакеты приложения Hello, описанные здесь заменяет функции hello пакет приложений, доступны в предыдущих версиях службы hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="78f3a-115">Требования к пакетам приложений</span><span class="sxs-lookup"><span data-stu-id="78f3a-115">Application package requirements</span></span>
<span data-ttu-id="78f3a-116">пакеты приложений toouse, требуется слишком[связать учетную запись хранилища Azure](#link-a-storage-account) tooyour пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="78f3a-117">Эта функция появилась в [API REST пакета] [ api_rest] версии 2015-12-01.2.2 и соответствующий hello [пакета .NET] [ api_net] версия библиотеки 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="78f3a-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="78f3a-118">Рекомендуется всегда использовать последнюю версию API hello при работе с использованием пакета.</span><span class="sxs-lookup"><span data-stu-id="78f3a-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="78f3a-119">Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="78f3a-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="78f3a-120">Они поддерживаются в пулах пакета, созданные между 10 марта 2016 г. и 5 июля 2017 г., только в том случае, если пул hello был создан с помощью конфигурации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="78f3a-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="78f3a-121">Пакеты приложений не поддерживают пулы пакета, созданные предыдущей too10 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="78f3a-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="78f3a-122">О приложениях и пакетах приложений</span><span class="sxs-lookup"><span data-stu-id="78f3a-122">About applications and application packages</span></span>
<span data-ttu-id="78f3a-123">В пакете Azure *приложения* ссылается набор tooa версии двоичных файлов, которые могут быть автоматически загружаемые toohello вычислительных узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="78f3a-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="78f3a-124">*Пакета приложения* ссылается tooa *определенный набор* этих двоичных файлов и представляет данного *версии* приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="78f3a-125">![Обзорная схема: приложения и пакеты приложений][1]</span><span class="sxs-lookup"><span data-stu-id="78f3a-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="78f3a-126">Приложения</span><span class="sxs-lookup"><span data-stu-id="78f3a-126">Applications</span></span>
<span data-ttu-id="78f3a-127">Приложения в пакете содержит один или несколько приложений, пакеты и задает параметры конфигурации для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="78f3a-128">Например приложение может указать tooinstall к версии пакета приложения hello по умолчанию на вычислительные узлы и ли его пакетов могут быть обновлены или удалены.</span><span class="sxs-lookup"><span data-stu-id="78f3a-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="78f3a-129">Пакеты приложений</span><span class="sxs-lookup"><span data-stu-id="78f3a-129">Application packages</span></span>
<span data-ttu-id="78f3a-130">Пакет приложения является ZIP-файл, содержащий двоичные файлы приложения hello и вспомогательные файлы, которые требуются для приложения hello toorun задачи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="78f3a-131">Каждый пакет приложения представляет конкретную версию приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="78f3a-132">Можно указать пакетов приложений на уровнях hello пула и задач.</span><span class="sxs-lookup"><span data-stu-id="78f3a-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="78f3a-133">При создании пула или задачи можно указать один или несколько таких пакетов и (при необходимости) версию.</span><span class="sxs-lookup"><span data-stu-id="78f3a-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="78f3a-134">**Пул пакетов приложений** развертываются слишком*каждого* узла в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="78f3a-135">Развертывание приложений осуществляется во время присоединения узла к пулу, а также когда узел перезагружается или для него пересоздается образ.</span><span class="sxs-lookup"><span data-stu-id="78f3a-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="78f3a-136">Если все узлы в пуле выполняют задачи задания, пакеты приложения уровня пула считаются пригодными.</span><span class="sxs-lookup"><span data-stu-id="78f3a-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="78f3a-137">При создании пула можно указать один или несколько пакетов приложений, а также добавить или обновить имеющиеся в пуле пакеты.</span><span class="sxs-lookup"><span data-stu-id="78f3a-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="78f3a-138">При обновлении пакетов существующий пул приложений, необходимо перезапустить его tooinstall узлы hello новый пакет.</span><span class="sxs-lookup"><span data-stu-id="78f3a-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="78f3a-139">**Задача пакетов приложений** развертываются только tooa вычислительном узле запланированные задачи, toorun непосредственно перед запуском задачу hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="78f3a-140">Если указан hello пакета приложения и версии уже находится на узле hello, не развертывается и используется hello существующий пакет.</span><span class="sxs-lookup"><span data-stu-id="78f3a-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="78f3a-141">Пакеты приложений задачи полезны в общий пул средах, где различные задания выполняются на один пул и пул hello не удаляется при завершении задания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="78f3a-142">Если в задании содержится меньшее количество задач, чем узлы в пуле hello, пакеты приложения задач можно свести к минимуму передачи данных так, как приложение будет развернутой toohello только узлы, выполнять задачи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="78f3a-143">Мы также рекомендуем использовать пакеты приложений уровня задач для выполнения небольшого количества задач в сценариях с большими приложениями.</span><span class="sxs-lookup"><span data-stu-id="78f3a-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="78f3a-144">Например стадии предварительной обработки или задача слияния, где приложение hello предварительной обработки или слияния является высокой плотности, могут использовать преимущества пакеты задач приложения.</span><span class="sxs-lookup"><span data-stu-id="78f3a-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78f3a-145">Существуют ограничения на количество hello приложений и пакетов приложений внутри пакета учетной записи и на размер пакета максимальное приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="78f3a-146">В разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md) подробные сведения об этих ограничениях.</span><span class="sxs-lookup"><span data-stu-id="78f3a-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="78f3a-147">Преимущества пакетов приложений</span><span class="sxs-lookup"><span data-stu-id="78f3a-147">Benefits of application packages</span></span>
<span data-ttu-id="78f3a-148">Пакеты приложений можно упростить код hello в пакет решения и нижней hello служебных данных требуется toomanage hello работающих приложений ваших задач.</span><span class="sxs-lookup"><span data-stu-id="78f3a-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="78f3a-149">С пакетами приложения задачи запуска в пуле нет toospecify длинный список отдельных ресурсов tooinstall файлы на узлах hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="78f3a-150">У вас нет toomanually управления несколькими версиями файлов приложения в службе хранилища Azure или на узлах.</span><span class="sxs-lookup"><span data-stu-id="78f3a-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="78f3a-151">И нет необходимости tooworry о создании [URL-адреса SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide доступ к файлам toohello вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="78f3a-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="78f3a-152">Пакетный работает в фоновом режиме hello пакетов приложений toostore хранилища Azure и развертывать их toocompute узлов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="78f3a-153">Hello общий размер задачи запуска должен быть меньше или равно too32768 символов, включая файлы ресурсов и переменные среды.</span><span class="sxs-lookup"><span data-stu-id="78f3a-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="78f3a-154">Если задача запуска превышает это ограничение, то можно воспользоваться пакетами приложений.</span><span class="sxs-lookup"><span data-stu-id="78f3a-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="78f3a-155">Можно также создать ZIP-архив, содержащий файлы ресурсов, передать его как tooAzure BLOB-объекта хранилища и затем распакуйте его из командной строки hello вашей задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="78f3a-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="78f3a-156">Передача приложений и управление ими</span><span class="sxs-lookup"><span data-stu-id="78f3a-156">Upload and manage applications</span></span>
<span data-ttu-id="78f3a-157">Можно использовать hello [портал Azure] [ portal] или hello [пакета управления .NET](batch-management-dotnet.md) пакетов приложений библиотеки toomanage hello в вашей учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="78f3a-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="78f3a-158">Здравствуйте рядом в нескольких разделах, сначала отобразить как toolink учетную запись хранилища, затем приводятся добавления приложений и пакетов и управления ими с помощью hello портала.</span><span class="sxs-lookup"><span data-stu-id="78f3a-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="78f3a-159">Связывание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="78f3a-159">Link a Storage account</span></span>
<span data-ttu-id="78f3a-160">toouse пакетов приложений, необходимо сначала связать tooyour учетной записи хранилища Azure пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="78f3a-161">Если учетная запись хранения еще не настроен, hello Azure портал отображает hello предупреждение первом нажатии hello **приложений** плитки в hello **учетная запись пакетной службы** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78f3a-162">В настоящее время пакета поддерживает *только* hello **общего назначения** тип учетной записи хранения, как описано в шаге 5, [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account)в [о Azure учетные записи хранения](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="78f3a-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="78f3a-163">При связывании tooyour учетной записи хранилища Azure пакетной учетной записи, связать *только* **общего назначения** учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="78f3a-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="78f3a-164">![Предупреждение "Нет настроенной учетной записи хранения" на портале Azure][9]</span><span class="sxs-lookup"><span data-stu-id="78f3a-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="78f3a-165">Hello пакетной службы использует hello связанные toostore учетной записи хранилища пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="78f3a-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="78f3a-166">После привязки hello две учетные записи, пакет можно автоматически развертывать hello пакеты, хранимые в связанной hello хранилища учетной записи tooyour вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="78f3a-167">toolink tooyour учетной записи хранилища пакетной учетной записи, нажмите кнопку **параметры учетной записи хранилища** на hello **предупреждение** и, при необходимости нажмите кнопку **учетной записи хранилища** на hello **Учетной записи хранилища** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="78f3a-168">![Выбор колонки учетной записи хранения на портале Azure][10]</span><span class="sxs-lookup"><span data-stu-id="78f3a-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="78f3a-169">Мы рекомендуем создать учетную запись хранения *специально* для учетной записи пакетной службы и выбрать ее здесь.</span><span class="sxs-lookup"><span data-stu-id="78f3a-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="78f3a-170">Дополнительные сведения о том, как toocreate учетную запись хранилища, в разделе «Создание учетной записи хранения» в [учетные записи о хранилище Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="78f3a-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="78f3a-171">После создания учетной записи хранилища, можно затем связать его tooyour пакетной учетной записи с помощью hello **учетной записи хранилища** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="78f3a-172">Hello пакетная служба использует toostore хранилища Azure пакеты приложения в качестве блочных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="78f3a-173">Вы являетесь [взимается плата в обычном режиме] [ storage_pricing] для данных большого двоичного объекта блока hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="78f3a-174">Убедиться, что размер tooconsider hello и количество пакетов приложения и периодически удалять устаревшие пакеты toominimize затраты.</span><span class="sxs-lookup"><span data-stu-id="78f3a-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="78f3a-175">Просмотр текущих приложений</span><span class="sxs-lookup"><span data-stu-id="78f3a-175">View current applications</span></span>
<span data-ttu-id="78f3a-176">tooview приложения hello в учетной записи пакета щелкните hello **приложений** пункта меню в левом меню hello во время просмотра hello **учетная запись пакетной службы** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="78f3a-177">![Элемент "Приложения"][2]</span><span class="sxs-lookup"><span data-stu-id="78f3a-177">![Applications tile][2]</span></span>

<span data-ttu-id="78f3a-178">При выборе этого параметра меню открывается hello **приложений** колонки:</span><span class="sxs-lookup"><span data-stu-id="78f3a-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="78f3a-179">![Список приложений][3]</span><span class="sxs-lookup"><span data-stu-id="78f3a-179">![List applications][3]</span></span>

<span data-ttu-id="78f3a-180">Hello **приложений** колонке отображает hello идентификатор каждого приложения в вашей учетной записи и hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="78f3a-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="78f3a-181">**Пакеты**: hello номер версии, связанные с этим приложением.</span><span class="sxs-lookup"><span data-stu-id="78f3a-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="78f3a-182">**Версия по умолчанию**: версия приложения hello установлены, если версия не указана при указании приложения hello в пуле.</span><span class="sxs-lookup"><span data-stu-id="78f3a-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="78f3a-183">Это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="78f3a-183">This setting is optional.</span></span>
* <span data-ttu-id="78f3a-184">**Разрешить обновления**: hello значение, указывающее, является ли пакет обновления, удаления и дополнения разрешены.</span><span class="sxs-lookup"><span data-stu-id="78f3a-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="78f3a-185">Если это значение задано слишком**нет**, пакет обновления и удаления для приложения hello отключены.</span><span class="sxs-lookup"><span data-stu-id="78f3a-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="78f3a-186">Вы сможете только добавлять новые версии пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="78f3a-186">Only new application package versions can be added.</span></span> <span data-ttu-id="78f3a-187">по умолчанию Hello — **Да**.</span><span class="sxs-lookup"><span data-stu-id="78f3a-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="78f3a-188">Просмотр сведений о приложении</span><span class="sxs-lookup"><span data-stu-id="78f3a-188">View application details</span></span>
<span data-ttu-id="78f3a-189">tooopen hello колонки, включая данные о hello для приложения hello приложения, выберите в hello **приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="78f3a-190">![Сведения о приложении][4]</span><span class="sxs-lookup"><span data-stu-id="78f3a-190">![Application details][4]</span></span>

<span data-ttu-id="78f3a-191">В колонке сведений приложения hello можно настроить следующие параметры для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="78f3a-192">**Разрешить обновления**: возможность обновления и удаления пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="78f3a-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="78f3a-193">См. раздел "Обновление или удаление пакета приложения" ниже.</span><span class="sxs-lookup"><span data-stu-id="78f3a-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="78f3a-194">**Версия по умолчанию**: укажите toocompute узлы toodeploy пакета по умолчанию приложения.</span><span class="sxs-lookup"><span data-stu-id="78f3a-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="78f3a-195">**Отображаемое имя**: укажите понятное имя, которое пакет решения можно использовать при отображении сведений о приложении hello, например, в hello пользовательского интерфейса, которые предоставляют tooyour клиентов с помощью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="78f3a-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="78f3a-196">Добавление нового приложения</span><span class="sxs-lookup"><span data-stu-id="78f3a-196">Add a new application</span></span>
<span data-ttu-id="78f3a-197">toocreate нового приложения, добавьте пакет приложения и укажите приложения новый, уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="78f3a-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="78f3a-198">Hello первого приложения пакета, добавлении с новым Идентификатором приложения hello также создает новое приложение hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="78f3a-199">Нажмите кнопку **добавить** на hello **приложений** hello колонке tooopen **новое приложение** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="78f3a-200">![Колонка "Новое приложение" на портале Azure][5]</span><span class="sxs-lookup"><span data-stu-id="78f3a-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="78f3a-201">Hello **новое приложение** колонке предоставляет следующие hello полей параметры hello toospecify новое приложение и пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="78f3a-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="78f3a-202">**Идентификатор приложения**</span><span class="sxs-lookup"><span data-stu-id="78f3a-202">**Application id**</span></span>

<span data-ttu-id="78f3a-203">Это поле указывает идентификатор hello нового приложения, являющегося правила проверки стандартный идентификатор пакета Azure toohello субъекта.</span><span class="sxs-lookup"><span data-stu-id="78f3a-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="78f3a-204">Ниже приведены правила Hello для предоставления идентификатора приложения:</span><span class="sxs-lookup"><span data-stu-id="78f3a-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="78f3a-205">На узлах Windows hello идентификатор может содержать любое сочетание буквенно-цифровые символы, дефисы и знаки подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="78f3a-206">На узлах Linux допускаются только буквенно-цифровые знаки и символы подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="78f3a-207">Не может содержать более 64 символов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="78f3a-208">Должно быть уникальным в пределах hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="78f3a-209">Не меняет и не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="78f3a-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="78f3a-210">**Версия**</span><span class="sxs-lookup"><span data-stu-id="78f3a-210">**Version**</span></span>

<span data-ttu-id="78f3a-211">Это поле указывает hello версии пакета приложения hello, которые вы отправляете.</span><span class="sxs-lookup"><span data-stu-id="78f3a-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="78f3a-212">Строки версии приведены toohello субъекта правилам проверки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="78f3a-213">На узлах Windows hello версии строка может содержать любое сочетание буквенно-цифровые символы, дефисы, подчеркивания и точки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="78f3a-214">На узлах Linux hello версии строка может содержать только буквы, цифры и знаки подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="78f3a-215">Не может содержать более 64 символов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="78f3a-216">Должно быть уникальным в пределах приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="78f3a-217">Не меняет и не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="78f3a-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="78f3a-218">**Пакет приложения**</span><span class="sxs-lookup"><span data-stu-id="78f3a-218">**Application package**</span></span>

<span data-ttu-id="78f3a-219">Это поле указывает hello ZIP-файл, содержащий двоичные файлы приложения hello и вспомогательные файлы, необходимые tooexecute приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="78f3a-220">Нажмите кнопку hello **выберите файл** поле или hello tooand toobrowse значок папки выберите ZIP-файл, содержащий файлы приложения.</span><span class="sxs-lookup"><span data-stu-id="78f3a-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="78f3a-221">После выбора файла, нажмите кнопку **ОК** toobegin hello передачи tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="78f3a-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="78f3a-222">После завершения операции отправки hello hello портал отображает уведомление и закрывает hello колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="78f3a-223">В зависимости от размера hello файла hello, отправка и hello скорость сетевого подключения эта операция может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="78f3a-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="78f3a-224">Не закрывайте hello **новое приложение** колонке до завершения операции отправки hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="78f3a-225">Это останавливает процесс передачи hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="78f3a-226">Добавление нового пакета приложения</span><span class="sxs-lookup"><span data-stu-id="78f3a-226">Add a new application package</span></span>
<span data-ttu-id="78f3a-227">tooadd новой версии пакета приложения для существующего приложения, откройте приложение в hello **приложений** колонка, щелкните **пакетов**, нажмите кнопку **добавить** tooopen Hello **добавить пакет** колонку.</span><span class="sxs-lookup"><span data-stu-id="78f3a-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="78f3a-228">![Колонка "Добавление пакета приложения" на портале Azure][8]</span><span class="sxs-lookup"><span data-stu-id="78f3a-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="78f3a-229">Как видите, hello полей совпадают с hello **новое приложение** колонки, но hello **идентификатор приложения** поле отключено.</span><span class="sxs-lookup"><span data-stu-id="78f3a-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="78f3a-230">Как и для нового приложения hello, укажите hello **версии** для нового пакета, Обзор tooyour **пакета приложения** .zip файла, после чего нажмите кнопку **ОК** tooupload hello пакет.</span><span class="sxs-lookup"><span data-stu-id="78f3a-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="78f3a-231">Обновление или удаление пакета приложения</span><span class="sxs-lookup"><span data-stu-id="78f3a-231">Update or delete an application package</span></span>
<span data-ttu-id="78f3a-232">tooupdate или удалить существующий пакет приложения, откройте hello колонке сведения для приложения hello, нажмите кнопку **пакетов** tooopen hello **пакетов** колонке щелкните hello **многоточие**в строке приветствия пакета приложения hello, toomodify и выберите требуемый tooperform действие hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="78f3a-233">![Обновление или удаление пакета на портале Azure][7]</span><span class="sxs-lookup"><span data-stu-id="78f3a-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="78f3a-234">**Блокировка изменений**</span><span class="sxs-lookup"><span data-stu-id="78f3a-234">**Update**</span></span>

<span data-ttu-id="78f3a-235">При нажатии кнопки **обновление**, hello *обновление* колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="78f3a-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="78f3a-236">Эта колонка находится аналогичные toohello *новый пакет приложения* колонки, однако только поле выбора пакета hello включен, позволяя toospecify новый tooupload файла ZIP.</span><span class="sxs-lookup"><span data-stu-id="78f3a-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="78f3a-237">![Колонка "Обновление пакета" на портале Azure][11]</span><span class="sxs-lookup"><span data-stu-id="78f3a-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="78f3a-238">**Удалить**</span><span class="sxs-lookup"><span data-stu-id="78f3a-238">**Delete**</span></span>

<span data-ttu-id="78f3a-239">При нажатии кнопки **удалить**, будет предложено удаление hello tooconfirm версия пакета hello и пакетные удаления hello пакет из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="78f3a-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="78f3a-240">При удалении версии по умолчанию hello приложения hello **версия по умолчанию** удалить параметр для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="78f3a-241">![Удаление приложения][12]</span><span class="sxs-lookup"><span data-stu-id="78f3a-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="78f3a-242">Установка приложений на вычислительных узлах</span><span class="sxs-lookup"><span data-stu-id="78f3a-242">Install applications on compute nodes</span></span>
<span data-ttu-id="78f3a-243">Теперь, когда вы узнали, как приложение toomanage пакетов с hello портал Azure, рассмотрим, как toodeploy их toocompute узлов и запускать их с пакетные задачи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="78f3a-244">Установка пакетов приложений уровня пула</span><span class="sxs-lookup"><span data-stu-id="78f3a-244">Install pool application packages</span></span>
<span data-ttu-id="78f3a-245">tooinstall пакета приложения на всех вычислительных узлов в пуле, укажите один или несколько пакетов приложений *ссылки* hello в пуле.</span><span class="sxs-lookup"><span data-stu-id="78f3a-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="78f3a-246">пакеты приложения Hello, указываемые в пуле устанавливаются на каждом вычислительном узле, когда этот узел будет присоединен пула hello и при узел hello перезагрузки или повторного создания образа.</span><span class="sxs-lookup"><span data-stu-id="78f3a-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="78f3a-247">В .NET пакетной службы укажите одно или несколько свойств [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] для нового пула во время создания или для имеющегося пула.</span><span class="sxs-lookup"><span data-stu-id="78f3a-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="78f3a-248">Hello [ApplicationPackageReference] [ net_pkgref] класс указывает идентификатор приложения и версии tooinstall в пуле вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="78f3a-249">Если какой-либо причине произошел сбой развертывания пакета приложения, знаков обслуживания пакетного hello hello узел [непригодным для использования][net_nodestate], и никакие задачи, планируются на выполнение на этом узле.</span><span class="sxs-lookup"><span data-stu-id="78f3a-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="78f3a-250">В этом случае следует **перезапустите** hello узел tooreinitiate hello пакета развертывания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="78f3a-251">Перезапускать hello узла также позволяет повторно планированием задач на узле hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="78f3a-252">Установка пакетов приложений уровня задач</span><span class="sxs-lookup"><span data-stu-id="78f3a-252">Install task application packages</span></span>
<span data-ttu-id="78f3a-253">Аналогичные tooa пула, укажите пакет приложения *ссылки* для задачи.</span><span class="sxs-lookup"><span data-stu-id="78f3a-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="78f3a-254">Если задача становится запланированных toorun на узле, пакет hello загрузку и извлечение непосредственно перед выполнением задачи hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="78f3a-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="78f3a-255">Если указанный пакет и версию уже установлен на узле hello, hello пакет не загружается и используется существующий пакет hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="78f3a-256">tooinstall задач пакета приложения, настроить задачу hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] свойства:</span><span class="sxs-lookup"><span data-stu-id="78f3a-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="78f3a-257">Выполнение приложений установлены hello</span><span class="sxs-lookup"><span data-stu-id="78f3a-257">Execute hello installed applications</span></span>
<span data-ttu-id="78f3a-258">Hello пакеты, которые вы указали для пула или задачи загрузили и извлекли tooa с именем каталога в hello `AZ_BATCH_ROOT_DIR` hello узла.</span><span class="sxs-lookup"><span data-stu-id="78f3a-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="78f3a-259">Пакет также создается переменная среды, которая содержит каталог с именем toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="78f3a-260">Командные строки вашей задачи использовать эту переменную среды, при ссылке на приложение hello на узле hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="78f3a-261">На узлах Windows hello переменная будет попадать в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="78f3a-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="78f3a-262">На узлах Linux формат hello немного отличается.</span><span class="sxs-lookup"><span data-stu-id="78f3a-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="78f3a-263">Точки (.), дефисы (-) и символом решетки (#) — это плоский toounderscores в переменной среды hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="78f3a-264">Например:</span><span class="sxs-lookup"><span data-stu-id="78f3a-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="78f3a-265">`APPLICATIONID`и `version` — это значения, которые соответствуют toohello приложения и версия пакета, указанного для развертывания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="78f3a-266">Например, если указано, версии 2.7 приложения *blender* должен быть установлен на узлах Windows вашей задачи командные строки использовать этот tooaccess переменной среды ее файлы:</span><span class="sxs-lookup"><span data-stu-id="78f3a-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="78f3a-267">На узлах Linux Укажите переменную среды hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="78f3a-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="78f3a-268">При передаче пакета приложения, можно указать, по умолчанию версии toodeploy tooyour вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="78f3a-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="78f3a-269">Если указана версия по умолчанию для приложения, можно опустить суффикса версии hello при ссылке на приложение hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="78f3a-270">Можно указать версию приложения по умолчанию hello в hello портал Azure, в колонке приложения hello, как показано в [отправка и управление приложениями](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="78f3a-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="78f3a-271">Например, если указать «2.7» hello версия по умолчанию для приложения *blender*, задачам ссылаться hello следующая переменная среды, затем узлы Windows будет выполняться версии 2.7:</span><span class="sxs-lookup"><span data-stu-id="78f3a-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="78f3a-272">Hello следующий фрагмент кода показывает пример задачи командной строки, запускающей версия по умолчанию hello hello *blender* приложения:</span><span class="sxs-lookup"><span data-stu-id="78f3a-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="78f3a-273">В разделе [параметры среды для задачи](batch-api-basics.md#environment-settings-for-tasks) в hello [Обзор возможностей пакетной](batch-api-basics.md) Дополнительные сведения о параметрах среды вычислительного узла.</span><span class="sxs-lookup"><span data-stu-id="78f3a-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="78f3a-274">Обновление пакетов приложений пула</span><span class="sxs-lookup"><span data-stu-id="78f3a-274">Update a pool's application packages</span></span>
<span data-ttu-id="78f3a-275">Если существующий пул уже был настроен с помощью пакета приложения, можно указать новый пакет для пула hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="78f3a-276">При указании новую ссылку пакета для пула применяются следующие hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="78f3a-277">Hello пакетная служба устанавливает hello вновь указанного пакета на всех новых узлов, которые присоединиться к пулу hello и на любой существующий узел, перезагрузки или повторного создания образа.</span><span class="sxs-lookup"><span data-stu-id="78f3a-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="78f3a-278">Вычислительные узлы, которые уже находятся в пуле hello при обновлении ссылки на пакет hello не устанавливают новый пакет приложения hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="78f3a-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="78f3a-279">Эти вычисляемые узлов должны быть перезагружены или Модернизированные tooreceive hello новый пакет.</span><span class="sxs-lookup"><span data-stu-id="78f3a-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="78f3a-280">При развертывании нового пакета hello создать переменные среды отражают hello новые ссылки пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="78f3a-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="78f3a-281">В этом примере hello существующий пул имеет версию 2.7 hello *blender* приложения, настроенного как один из его [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="78f3a-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="78f3a-282">узлы tooupdate hello пул с версией 2.76b, укажите новое [ApplicationPackageReference] [ net_pkgref] с новой версией hello и фиксации изменений hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="78f3a-283">Теперь, когда hello новой версии будет настроена, hello пакетная служба устанавливает версию 2.76b tooany *новый* узел присоединяется hello пула.</span><span class="sxs-lookup"><span data-stu-id="78f3a-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="78f3a-284">tooinstall 2.76b на узлах hello, *уже* в пуле hello перезагрузки или повторного создания образа их.</span><span class="sxs-lookup"><span data-stu-id="78f3a-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="78f3a-285">Обратите внимание, что перезагруженный узлы сохраняют hello файлы из предыдущего пакета развертывания.</span><span class="sxs-lookup"><span data-stu-id="78f3a-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="78f3a-286">Список приложений hello в пакетную учетную запись</span><span class="sxs-lookup"><span data-stu-id="78f3a-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="78f3a-287">Список приложений hello и их пакетов в пакетную учетную запись можно с помощью hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] метод.</span><span class="sxs-lookup"><span data-stu-id="78f3a-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="78f3a-288">Заключение</span><span class="sxs-lookup"><span data-stu-id="78f3a-288">Wrap up</span></span>
<span data-ttu-id="78f3a-289">Пакеты приложений, которые могут пригодиться клиентов выберите приложения hello для своей работы и указать точную версию toouse hello при обработке задания с активированным пакетным режимом службы.</span><span class="sxs-lookup"><span data-stu-id="78f3a-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="78f3a-290">Может также предоставляют возможность hello для вашего tooupload клиентов и отслеживать своих приложений в службе.</span><span class="sxs-lookup"><span data-stu-id="78f3a-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78f3a-291">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78f3a-291">Next steps</span></span>
* <span data-ttu-id="78f3a-292">Hello [API REST пакета] [ api_rest] также обеспечивает поддержку toowork пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="78f3a-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="78f3a-293">Пример в статье hello [applicationPackageReferences] [ rest_add_pool_with_packages] элемент в [добавить учетную запись пула tooan] [ rest_add_pool] сведения о том, как toospecify tooinstall пакетов с помощью API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="78f3a-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="78f3a-294">В разделе [приложений] [ rest_applications] для получения сведений об как tooobtain сведений о приложении с помощью hello API REST пакета.</span><span class="sxs-lookup"><span data-stu-id="78f3a-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="78f3a-295">Узнайте, как tooprogrammatically [управление учетными записями пакетной службы Azure и квоты, с помощью пакета управления .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="78f3a-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="78f3a-296">Hello [пакета управления .NET][api_net_mgmt] библиотеки можно включить функции создания и удаления учетной записи для пакета приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="78f3a-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Общая схема: пакеты приложений"
[2]: ./media/batch-application-packages/app_pkg_02.png "Элемент "Приложения" на портале Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Колонка "Приложения" на портале Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Параметры в колонке "Сведения о приложении" на портале Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Колонка "Новое приложение" на портале Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Пункты "Обновить" и "Удалить" для пакетов на портале Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Колонка "Новый пакет приложения" на портале Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Предупреждение об отсутствии связанной учетной записи хранения"
[10]: ./media/batch-application-packages/app_pkg_10.png "Выбор колонки учетной записи хранения на портале Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Колонка "Обновление пакета" на портале Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Диалоговое окно для подтверждения удаления пакета на портале Azure"
