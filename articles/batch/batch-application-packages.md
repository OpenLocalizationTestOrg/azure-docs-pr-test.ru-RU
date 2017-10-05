---
title: "Установка пакетов приложений на вычислительных узлах (пакетная служба Azure) | Документация Майкрософт"
description: "Пакеты приложений пакетной службы Azure позволяют легко управлять несколькими приложениями и их версиями для установки на вычислительные узлы пакетной службы."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="5fe3d-103">Развертывание приложений на вычислительных узлах с помощью пакетов приложений пакетной службы</span><span class="sxs-lookup"><span data-stu-id="5fe3d-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="5fe3d-104">Использование пакетов приложений пакетной службы Azure обеспечивает простое управление приложениями задач и их развертывание на вычислительных узлах в пуле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="5fe3d-105">С помощью пакетов приложений вы можете передать несколько версий приложений, выполняемых вашими задачами (в том числе вспомогательные файлы), а также управлять ими,</span><span class="sxs-lookup"><span data-stu-id="5fe3d-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="5fe3d-106">а затем автоматически развернуть одно или несколько таких приложений на вычислительных узлах в пуле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="5fe3d-107">Из этой статьи вы узнаете, как передать пакеты приложений на портале Azure, а также управлять ими,</span><span class="sxs-lookup"><span data-stu-id="5fe3d-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="5fe3d-108">а затем установить их на вычислительных узлах пула с помощью библиотеки [.NET для пакетной службы][api_net].</span><span class="sxs-lookup"><span data-stu-id="5fe3d-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="5fe3d-109">Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="5fe3d-110">Если пул создан с помощью конфигурации облачной службы, пакеты приложений также поддерживаются в пулах пакетной службы, созданных между 10 марта 2016 г. и 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="5fe3d-111">Пулы пакетной службы, созданные до 10 марта 2016 г., не поддерживают пакеты приложений.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="5fe3d-112">API-интерфейсы для создания пакетов приложений и управления ими входят в библиотеку [.NET для управления пакетной службой] [[api_net_mgmt]].</span><span class="sxs-lookup"><span data-stu-id="5fe3d-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="5fe3d-113">API-интерфейсы для установки пакетов приложений в вычислительном узле входят в библиотеку [.NET для пакетной службы][api_net].</span><span class="sxs-lookup"><span data-stu-id="5fe3d-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="5fe3d-114">Компонент "Пакеты приложений", описываемый в этой статье, заменяет компонент "Приложения пакетной службы", доступный в предыдущих версиях службы.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="5fe3d-115">Требования к пакетам приложений</span><span class="sxs-lookup"><span data-stu-id="5fe3d-115">Application package requirements</span></span>
<span data-ttu-id="5fe3d-116">Чтобы использовать пакеты приложений, необходимо [связать учетную запись хранения Azure](#link-a-storage-account) с учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="5fe3d-117">Этот компонент появился в [REST API пакетной службы][api_rest] версии 2015-12-01.2.2 и соответствующей библиотеке [.NET для пакетной службы][api_net] версии 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="5fe3d-118">Мы рекомендуем всегда использовать при работе с пакетной службой последнюю версию API.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="5fe3d-119">Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="5fe3d-120">Если пул создан с помощью конфигурации облачной службы, пакеты приложений также поддерживаются в пулах пакетной службы, созданных между 10 марта 2016 г. и 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="5fe3d-121">Пулы пакетной службы, созданные до 10 марта 2016 г., не поддерживают пакеты приложений.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="5fe3d-122">О приложениях и пакетах приложений</span><span class="sxs-lookup"><span data-stu-id="5fe3d-122">About applications and application packages</span></span>
<span data-ttu-id="5fe3d-123">В пакетной службе Azure *приложение* ссылается на набор двоичных файлов с возможностью управления версиями, которые могут автоматически скачиваться на вычислительные узлы в пуле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="5fe3d-124">*Пакет приложения* ссылается на *определенный набор* таких двоичных файлов, представляя конкретную *версию* приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="5fe3d-125">![Обзорная схема: приложения и пакеты приложений][1]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="5fe3d-126">Приложения</span><span class="sxs-lookup"><span data-stu-id="5fe3d-126">Applications</span></span>
<span data-ttu-id="5fe3d-127">Приложение в пакетной службе содержит один или несколько пакетов приложений и задает параметры конфигурации для приложения,</span><span class="sxs-lookup"><span data-stu-id="5fe3d-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="5fe3d-128">Например, приложение может указать версию пакета приложения по умолчанию для установки на вычислительных узлах, а также определяет необходимость обновления или удаления пакетов.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="5fe3d-129">Пакеты приложений</span><span class="sxs-lookup"><span data-stu-id="5fe3d-129">Application packages</span></span>
<span data-ttu-id="5fe3d-130">Пакет приложения — это ZIP-файл, содержащий двоичные файлы приложения и вспомогательные файлы, которые необходимы задачам для выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="5fe3d-131">Каждый пакет приложения представляет определенную версию приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="5fe3d-132">Пакеты приложений можно указывать на уровне пула и задачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="5fe3d-133">При создании пула или задачи можно указать один или несколько таких пакетов и (при необходимости) версию.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="5fe3d-134">**Пакеты приложений уровня пула** развертываются на *каждом* узле в пуле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="5fe3d-135">Развертывание приложений осуществляется во время присоединения узла к пулу, а также когда узел перезагружается или для него пересоздается образ.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="5fe3d-136">Если все узлы в пуле выполняют задачи задания, пакеты приложения уровня пула считаются пригодными.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="5fe3d-137">При создании пула можно указать один или несколько пакетов приложений, а также добавить или обновить имеющиеся в пуле пакеты.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="5fe3d-138">Чтобы обновить имеющиеся пакеты приложений, следует перезапустить узлы пула. Это позволит установить новый пакет.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="5fe3d-139">**Пакеты приложений уровня задач** развертываются только на вычислительных узлах, на которых запланировано выполнение задач. Развертывание осуществляется перед выполнением командной строки задачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="5fe3d-140">Если в узле уже развернут указанный пакет приложений и настроена версия, повторное развертывание не инициируется и используется имеющийся пакет.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="5fe3d-141">Пакеты приложений уровня задач полезны в средах с общим пулом, где различные задания выполняются в одном пуле, который не удаляется по завершении задания.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="5fe3d-142">Если задание содержит меньше задач, чем число узлов в пуле, пакеты приложений задач помогут минимизировать объем передаваемых данных, так как приложение развертывается только на узлах, на которых выполняются задачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="5fe3d-143">Мы также рекомендуем использовать пакеты приложений уровня задач для выполнения небольшого количества задач в сценариях с большими приложениями.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="5fe3d-144">Например, для выполнения задачи предварительной обработки или объединения с помощью соответствующих ресурсоемких приложений.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fe3d-145">Существуют ограничения на количество приложений и пакетов приложений в учетной записи пакетной службы, а также на максимальный размер пакета.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="5fe3d-146">Дополнительные сведения см. в статье [Квоты и ограничения пакетной службы Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="5fe3d-147">Преимущества пакетов приложений</span><span class="sxs-lookup"><span data-stu-id="5fe3d-147">Benefits of application packages</span></span>
<span data-ttu-id="5fe3d-148">Пакеты приложений позволяют упростить код в решении пакетной службы, а также сократить расходы на управление приложениями, выполняемыми задачами.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="5fe3d-149">При использовании пакетов приложений задача запуска пула не должна указывать длинный список отдельных файлов ресурсов для установки на узлах.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="5fe3d-150">Кроме того, вам не нужно вручную управлять несколькими версиями этих файлов приложения в службе хранилища Azure или на узлах,</span><span class="sxs-lookup"><span data-stu-id="5fe3d-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="5fe3d-151">а также создавать [URL-адреса SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md), чтобы предоставить доступ к файлам в своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="5fe3d-152">Пакетная служба работает со службой хранилища Azure в фоновом режиме, обеспечивая хранение пакетов приложений и их развертывание на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="5fe3d-153">Общий размер задачи запуска не должен превышать 32 768 символов, включая файлы ресурсов и переменные среды.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="5fe3d-154">Если задача запуска превышает это ограничение, то можно воспользоваться пакетами приложений.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="5fe3d-155">Также можно создать ZIP-архив, содержащий файлы ресурсов, передать его в виде большого двоичного объекта в службу хранилища Azure, а затем распаковать его из командной строки задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="5fe3d-156">Передача приложений и управление ими</span><span class="sxs-lookup"><span data-stu-id="5fe3d-156">Upload and manage applications</span></span>
<span data-ttu-id="5fe3d-157">Управление пакетами приложений в учетной записи пакетной службы осуществляется на [портале Azure][portal] или с помощью библиотеки [.NET для управления пакетной службой](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="5fe3d-158">В следующих разделах мы сначала покажем, как связать учетную запись хранения, а затем ознакомимся с добавлением приложений и пакетов, а также с управлением ими на портале.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="5fe3d-159">Связывание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="5fe3d-159">Link a Storage account</span></span>
<span data-ttu-id="5fe3d-160">Чтобы использовать пакеты приложений, вам сначала нужно связать учетную запись хранения Azure со своей учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="5fe3d-161">Если вы еще не настроили учетную запись хранения, то на портале Azure отобразится предупреждение, когда вы в первый раз щелкнете элемент **Приложения** в колонке **Учетная запись пакетной службы**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fe3d-162">Сейчас пакетная служба поддерживает *только* учетные записи хранения **общего назначения**, как описано на шаге 5 раздела о [создании учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="5fe3d-163">При связывании учетной записи службы хранилища Azure с учетной записью пакетной службы используйте *только* учетные записи хранения **общего назначения**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="5fe3d-164">![Предупреждение "Нет настроенной учетной записи хранения" на портале Azure][9]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="5fe3d-165">Пакетная служба использует связанную учетную запись хранения для хранения пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="5fe3d-166">Когда вы свяжете две учетные записи, пакетная служба сможет автоматически развертывать на вычислительных узлах пакеты, хранимые в связанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="5fe3d-167">Щелкните **Параметры учетной записи хранения** в колонке **Предупреждение**, а затем выберите **Учетная запись хранения** в колонке **Учетная запись хранения**, чтобы связать учетную запись хранения с учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="5fe3d-168">![Выбор колонки учетной записи хранения на портале Azure][10]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="5fe3d-169">Мы рекомендуем создать учетную запись хранения *специально* для учетной записи пакетной службы и выбрать ее здесь.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="5fe3d-170">Дополнительные сведения о создании учетной записи хранения см. в соответствующем разделе статьи [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="5fe3d-171">Созданную учетную запись хранения затем можно связать с учетной записью пакетной службы в колонке **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="5fe3d-172">Пакетная служба использует службу хранилища Azure для хранения пакетов приложений в виде блочных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="5fe3d-173">За использование данных блочных BLOB-объектов [взимается обычная плата][storage_pricing].</span><span class="sxs-lookup"><span data-stu-id="5fe3d-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="5fe3d-174">Вам обязательно следует учитывать размер и количество пакетов приложений, периодически удаляя устаревшие пакеты для минимизации расходов.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="5fe3d-175">Просмотр текущих приложений</span><span class="sxs-lookup"><span data-stu-id="5fe3d-175">View current applications</span></span>
<span data-ttu-id="5fe3d-176">Чтобы просмотреть приложения в учетной записи пакетной службы, щелкните пункт меню слева **Приложения** в колонке **Учетная запись пакетной службы**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="5fe3d-177">![Элемент "Приложения"][2]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-177">![Applications tile][2]</span></span>

<span data-ttu-id="5fe3d-178">Если выбрать этот пункт меню, то откроется колонка **Приложения**:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="5fe3d-179">![Список приложений][3]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-179">![List applications][3]</span></span>

<span data-ttu-id="5fe3d-180">В колонке **Приложения** отображается идентификатор каждого приложения в вашей учетной записи, а также следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="5fe3d-181">**Пакеты**: количество версий, связанных с этим приложением.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="5fe3d-182">**Версия по умолчанию**: версия приложения, которая будет установлена, если не указать версию при указании приложения для пула.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="5fe3d-183">Это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-183">This setting is optional.</span></span>
* <span data-ttu-id="5fe3d-184">**Разрешить обновления**: значение, которое определяет возможность обновления, удаления и дополнения пакетов.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="5fe3d-185">Если для этого параметра задано значение **Нет**, возможность обновления и удаления пакетов будет отключена для приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="5fe3d-186">Вы сможете только добавлять новые версии пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-186">Only new application package versions can be added.</span></span> <span data-ttu-id="5fe3d-187">По умолчанию используется значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="5fe3d-188">Просмотр сведений о приложении</span><span class="sxs-lookup"><span data-stu-id="5fe3d-188">View application details</span></span>
<span data-ttu-id="5fe3d-189">Чтобы открыть колонку со сведениями о приложении, выберите приложение в колонке **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="5fe3d-190">![Сведения о приложении][4]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-190">![Application details][4]</span></span>

<span data-ttu-id="5fe3d-191">В колонке сведений о приложении можно настроить следующие параметры для приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="5fe3d-192">**Разрешить обновления**: возможность обновления и удаления пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="5fe3d-193">См. раздел "Обновление или удаление пакета приложения" ниже.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="5fe3d-194">**Версия по умолчанию**: выбор пакета приложения по умолчанию для развертывания на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="5fe3d-195">**Отображаемое имя**: понятное имя, которое решение пакетной службы может использовать при отображении сведений о приложении, например в пользовательском интерфейсе службы, предоставляемой пользователям через пакетную службу.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="5fe3d-196">Добавление нового приложения</span><span class="sxs-lookup"><span data-stu-id="5fe3d-196">Add a new application</span></span>
<span data-ttu-id="5fe3d-197">Чтобы создать приложение, добавьте пакет приложения и укажите новый уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="5fe3d-198">Первый пакет приложения, добавленный с помощью идентификатора нового приложения, в свою очередь создает приложение.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="5fe3d-199">Щелкните **Добавить** в колонке **Приложения**, чтобы открыть колонку **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="5fe3d-200">![Колонка "Новое приложение" на портале Azure][5]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="5fe3d-201">Колонка **Новое приложение** содержит следующие поля для настройки параметров нового приложения и пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="5fe3d-202">**Идентификатор приложения**</span><span class="sxs-lookup"><span data-stu-id="5fe3d-202">**Application id**</span></span>

<span data-ttu-id="5fe3d-203">Это поле указывает идентификатор нового приложения, на который распространяются стандартные правила проверки идентификатора пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="5fe3d-204">Ниже приводятся правила предоставления идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="5fe3d-205">На узлах Windows идентификатор может содержать любое сочетание буквенно-цифровых знаков, дефисов и символов подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="5fe3d-206">На узлах Linux допускаются только буквенно-цифровые знаки и символы подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="5fe3d-207">Не может содержать более 64 символов.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="5fe3d-208">Должен быть уникальным в рамках учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="5fe3d-209">Не меняет и не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="5fe3d-210">**Версия**</span><span class="sxs-lookup"><span data-stu-id="5fe3d-210">**Version**</span></span>

<span data-ttu-id="5fe3d-211">Это поле указывает версию пакета приложения, который вы передаете.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="5fe3d-212">На строки версии распространяются следующие правила проверки.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="5fe3d-213">На узлах Windows строка версии может содержать любое сочетание буквенно-цифровых знаков, дефисов, символов подчеркивания и точек.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="5fe3d-214">На узлах Linux строка версии может содержать только буквенно-цифровые знаки и символы подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="5fe3d-215">Не может содержать более 64 символов.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="5fe3d-216">Должны быть уникальными в рамках приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-216">Must be unique within the application.</span></span>
* <span data-ttu-id="5fe3d-217">Не меняет и не учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="5fe3d-218">**Пакет приложения**</span><span class="sxs-lookup"><span data-stu-id="5fe3d-218">**Application package**</span></span>

<span data-ttu-id="5fe3d-219">Это поле указывает ZIP-файл, содержащий двоичные файлы приложения и вспомогательные файлы, необходимые для выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="5fe3d-220">Щелкните текстовое поле **Выбор файла** или значок папки, чтобы выбрать ZIP-файл, содержащий файлы приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="5fe3d-221">Выбрав файл, нажмите кнопку **ОК** , чтобы передать файл в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="5fe3d-222">По завершении операции передачи портал отображает уведомление и закрывает колонку.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="5fe3d-223">Скорость выполнения этой операции зависит от размера передаваемого файла и возможностей сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="5fe3d-224">Не закрывайте колонку **Новое приложение** до завершения операции.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="5fe3d-225">Иначе вы остановите процесс передачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="5fe3d-226">Добавление нового пакета приложения</span><span class="sxs-lookup"><span data-stu-id="5fe3d-226">Add a new application package</span></span>
<span data-ttu-id="5fe3d-227">Чтобы добавить новую версию пакета приложения для имеющегося приложения, выберите это приложение в колонке **Приложения**, щелкните **Пакеты**, а затем — **Добавить**, чтобы открыть колонку **Add package** (Добавление пакета).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="5fe3d-228">![Колонка "Добавление пакета приложения" на портале Azure][8]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="5fe3d-229">Как видите, эти поля совпадают с полями в колонке **Новое приложение**, за исключением неактивного текстового поля **Идентификатор приложения**.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="5fe3d-230">Как и для нового приложения, укажите **версию** нового пакета, выберите ZIP-файл **пакета приложения**, а затем нажмите кнопку **OК**, чтобы передать пакет.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="5fe3d-231">Обновление или удаление пакета приложения</span><span class="sxs-lookup"><span data-stu-id="5fe3d-231">Update or delete an application package</span></span>
<span data-ttu-id="5fe3d-232">Чтобы обновить или удалить имеющийся пакет приложения, откройте колонку со сведениями о приложении, щелкните **Пакеты**, чтобы открыть колонку **Пакеты**, а затем щелкните **многоточие** в строке пакета приложения, который вы хотите изменить, и выберите нужное действие.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="5fe3d-233">![Обновление или удаление пакета на портале Azure][7]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="5fe3d-234">**Блокировка изменений**</span><span class="sxs-lookup"><span data-stu-id="5fe3d-234">**Update**</span></span>

<span data-ttu-id="5fe3d-235">Если щелкнуть **Обновить**, отобразится колонка *Обновление пакета* .</span><span class="sxs-lookup"><span data-stu-id="5fe3d-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="5fe3d-236">Эта колонка аналогична колонке *New application package* (Новый пакет приложения), но в ней активно только поле выбора пакета, с помощью которого вы можете указать новый ZIP-файл для передачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="5fe3d-237">![Колонка "Обновление пакета" на портале Azure][11]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="5fe3d-238">**Удалить**</span><span class="sxs-lookup"><span data-stu-id="5fe3d-238">**Delete**</span></span>

<span data-ttu-id="5fe3d-239">Если щелкнуть **Удалить**, вам будет предложено подтвердить удаление версии пакета. Затем пакетная служба удалит пакет из службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="5fe3d-240">Удалив версию приложения по умолчанию, вы удалите настройку **версии по умолчанию** для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="5fe3d-241">![Удаление приложения][12]</span><span class="sxs-lookup"><span data-stu-id="5fe3d-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="5fe3d-242">Установка приложений на вычислительных узлах</span><span class="sxs-lookup"><span data-stu-id="5fe3d-242">Install applications on compute nodes</span></span>
<span data-ttu-id="5fe3d-243">Мы узнали об управлении пакетами приложений с помощью портала Azure. Теперь можно перейти к их развертыванию на вычислительных узлах, а также их выполнению с помощью задач пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="5fe3d-244">Установка пакетов приложений уровня пула</span><span class="sxs-lookup"><span data-stu-id="5fe3d-244">Install pool application packages</span></span>
<span data-ttu-id="5fe3d-245">Чтобы установить пакет приложения на все вычислительные узлы в пуле, укажите *ссылки* на один или несколько пакетов приложений для пула.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="5fe3d-246">Пакеты приложения, которые указываются для пула, устанавливаются на каждый вычислительный узел, когда он присоединяется к пулу, а также когда он перезагружается или для него пересоздается образ.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="5fe3d-247">В .NET пакетной службы укажите одно или несколько свойств [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] для нового пула во время создания или для имеющегося пула.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="5fe3d-248">Класс [ApplicationPackageReference][net_pkgref] определяет идентификатор приложения и версию для установки на вычислительные узлы пула.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="5fe3d-249">Если по какой-либо причине произошел сбой развертывания пакета приложения, то пакетная служба помечает узел как [непригодный][net_nodestate], и на этом узле не планируется выполнение каких-либо задач.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="5fe3d-250">В этом случае следует **перезапустить** этот узел, чтобы повторно инициировать развертывание пакета.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="5fe3d-251">Перезапуск узла также возобновляет планирование задач на узле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="5fe3d-252">Установка пакетов приложений уровня задач</span><span class="sxs-lookup"><span data-stu-id="5fe3d-252">Install task application packages</span></span>
<span data-ttu-id="5fe3d-253">Как и для пакетов уровня пула, укажите *ссылки* на один или несколько пакетов приложений для задачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="5fe3d-254">Если на узле запланировано выполнение задачи, скачивание и извлечение пакета осуществляется непосредственно перед выполнением командной строки задачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="5fe3d-255">Если в пуле уже установлен указанный пакет и настроена версия, скачивание не инициируется и используется имеющийся пакет.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="5fe3d-256">Чтобы установить пакет приложений уровня задач, настройте свойство [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] задачи.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="5fe3d-257">Выполнение установленных приложений</span><span class="sxs-lookup"><span data-stu-id="5fe3d-257">Execute the installed applications</span></span>
<span data-ttu-id="5fe3d-258">Пакеты, указанные для уровня пула или задач, скачиваются и извлекаются в указанный каталог `AZ_BATCH_ROOT_DIR` на узле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="5fe3d-259">Пакетная служба также создает переменную среды, содержащую путь к указанному каталогу.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="5fe3d-260">Командные строки задачи будут использовать эту переменную среды, ссылаясь на приложение в узле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="5fe3d-261">На узлах Windows переменная имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="5fe3d-262">На узлах Linux формат немного отличается.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="5fe3d-263">Точки (.), дефисы (-) и символы решетки (#) в переменной среды преобразовываются в символы подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="5fe3d-264">Например:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="5fe3d-265">Свойства `APPLICATIONID` и `version` — это значения, соответствующие версии пакета и приложения, указанных при развертывании.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="5fe3d-266">Например, если вы выбираете установку приложения *blender* версии 2.7 на узлах Windows, то командные строки задачи будут использовать переменную среды для получения доступа к его файлам:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="5fe3d-267">На узлах Linux укажите переменную среды в таком формате:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="5fe3d-268">При передаче пакета приложения можно указать версию по умолчанию для развертывания на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="5fe3d-269">Если для приложения указана версия по умолчанию, то на это приложение можно ссылаться без суффикса версии.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="5fe3d-270">Версию приложения по умолчанию можно указать на портале Azure в колонке "Приложения", как показано в разделе [Передача приложений и управление ими](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="5fe3d-271">Например, если для приложения *blender* в качестве версии по умолчанию указана версия 2.7 и задачи ссылаются на следующую переменную среды, то узлы Windows будут выполнять версию 2.7:</span><span class="sxs-lookup"><span data-stu-id="5fe3d-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="5fe3d-272">В следующем фрагменте кода показан образец командной строки задачи, используемый для запуска версии приложения *blender* по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="5fe3d-273">Дополнительные сведения о параметрах среды вычислительных узлов см. в разделе [Параметры среды для задач](batch-api-basics.md#environment-settings-for-tasks) статьи [Обзор функций пакетной службы для разработчиков](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="5fe3d-274">Обновление пакетов приложений пула</span><span class="sxs-lookup"><span data-stu-id="5fe3d-274">Update a pool's application packages</span></span>
<span data-ttu-id="5fe3d-275">Если для существующего пула уже выполнена настройка пакета приложения, вы можете указать новый пакет для пула.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="5fe3d-276">Если указывается ссылка на новый пакет для пула, действует следующее.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="5fe3d-277">Пакетная служба устанавливает новый указанный пакет на все новые узлы, присоединенные к пулу, и на все имеющиеся узлы, которые были перезагружены или для которых был повторно создан образ.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="5fe3d-278">Новый пакет приложения не будет автоматически установлен на вычислительные узлы, которые во время обновления ссылки на пакет уже существовали в пуле.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="5fe3d-279">Для получения нового пакета их необходимо перезагрузить либо заново создать для них образ.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="5fe3d-280">Переменные среды, создаваемые при развертывании нового пакета, отражают новые ссылки на пакеты приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="5fe3d-281">В нашем примере для имеющегося пула настроена версия 2.7 приложения *blender* (в качестве одного из свойств [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="5fe3d-282">Чтобы обновить узлы в пуле, используя версию 2.76b, укажите новое свойство [ApplicationPackageReference][net_pkgref] с новой версией, а затем подтвердите изменения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="5fe3d-283">После настройки новой версии пакетная служба устанавливает версию 2.76b на всех *новых* узлах, присоединенных к пулу.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="5fe3d-284">Чтобы установить версию 2.76b на все узлы, *уже* имеющиеся в пуле, перезагрузите их или создайте для них новый образ.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="5fe3d-285">Обратите внимание: после перезагрузки на узлах остаются файлы предыдущих развертываний пакета.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="5fe3d-286">Список приложений в учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="5fe3d-286">List the applications in a Batch account</span></span>
<span data-ttu-id="5fe3d-287">Вы можете вывести список приложений и их пакетов, входящих в учетную запись пакетной службы, с помощью метода [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries].</span><span class="sxs-lookup"><span data-stu-id="5fe3d-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="5fe3d-288">Заключение</span><span class="sxs-lookup"><span data-stu-id="5fe3d-288">Wrap up</span></span>
<span data-ttu-id="5fe3d-289">С помощью пакетов приложений вы можете предоставлять пользователям возможность выбирать приложения для своих заданий и указывать точную версию для использования при обработке заданий в пакетной службе.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="5fe3d-290">Вы также можете предоставить пользователям возможность передавать и отслеживать свои приложения в вашей службе.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fe3d-291">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fe3d-291">Next steps</span></span>
* <span data-ttu-id="5fe3d-292">[REST API пакетной службы][api_rest] также поддерживает работу с пакетами приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="5fe3d-293">В качестве примера изучите элемент [applicationPackageReferences][rest_add_pool_with_packages] в статье [Добавление учетной записи пула][rest_add_pool]. Сведения, описанные в этой статье, помогут вам определить пакеты для установки с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="5fe3d-294">Дополнительные сведения о получении сведений о приложении с помощью REST API пакетной службы см. в статье [Приложения][rest_applications].</span><span class="sxs-lookup"><span data-stu-id="5fe3d-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="5fe3d-295">Узнайте больше о программном [управлении квотами и учетными записями пакетной службы Azure с помощью библиотеки .NET для управления пакетной службой](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5fe3d-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="5fe3d-296">С помощью библиотеки [.NET для управления пакетной службой][api_net_mgmt] можно включить функции создания и удаления учетной записи для пакетной службы или приложения.</span><span class="sxs-lookup"><span data-stu-id="5fe3d-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
