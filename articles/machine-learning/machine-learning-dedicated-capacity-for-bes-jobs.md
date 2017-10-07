---
title: "aaaDedicated емкости для машины обучения пакетного выполнения службы заданий | Документы Microsoft"
description: "Обзор пакетных служб Azure для обработки заданий машинного обучения"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="a4fb9-103">Пакетные службы Azure для обработки заданий машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a4fb9-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="a4fb9-104">Машины обучения пула обработки обеспечивает масштаб с управлением клиентом hello службы Azure Machine Learning пакетного выполнения.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="a4fb9-105">Классический пакетной обработки для машинного обучения выполняется в многопользовательской среде, какие ограничения hello количество одновременно выполняемых заданий можно отправить и задания помещаются в очередь на основе первым пришел первым вышел.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="a4fb9-106">Эта неопределенность, в свою очередь, означает, что время запуска задания предсказать невозможно.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="a4fb9-107">Пакетная обработка пула позволяет toocreate пулы, на которых вы можете отправить пакетных заданий.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="a4fb9-108">Управлять hello размер пула hello и отправке задания hello toowhich пула.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="a4fb9-109">Задание BES выполняется в собственную обработку предоставления пространства производительность обработки прогнозируемого и hello возможность toocreate пулы ресурсов, которые соответствуют toohello нагрузку, которую можно отправить.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="a4fb9-110">Как toouse пула пакетной обработки</span><span class="sxs-lookup"><span data-stu-id="a4fb9-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="a4fb9-111">Конфигурацию пула Пакетная обработка в настоящее время недоступен через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="a4fb9-112">toouse пула пакетной обработки, необходимо:</span><span class="sxs-lookup"><span data-stu-id="a4fb9-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="a4fb9-113">Вызовите CSS toocreate пакетную учетную запись пула и получения URL-адрес пула службы и ключ авторизации</span><span class="sxs-lookup"><span data-stu-id="a4fb9-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="a4fb9-114">создать веб-службу и план выставления счетов на основе новой версии Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="a4fb9-115">toocreate вашей учетной записи, вызовите службу технической поддержки и поддержки (CSS) и укажите идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="a4fb9-116">CSS будут работать с вы toodetermine hello соответствующие емкости для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="a4fb9-117">Затем CSS настройку учетной записи с hello максимальное число пулов, можно создать и hello максимальное число виртуальных машин (ВМ), которые можно размещать в каждом пуле.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="a4fb9-118">Когда ваша учетная запись будет настроена, вам будет назначен URL-адрес службы пула и ключ авторизации,</span><span class="sxs-lookup"><span data-stu-id="a4fb9-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="a4fb9-119">После создания учетной записи используется hello URL-адрес службы пула и авторизации ключа tooperform пула операций управления в пуле пакета.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Архитектура пула пакетной службы](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="a4fb9-121">Пулы создается путем вызова операции создания пула hello на URL-адрес службы пула hello tooyou, предоставляемые CSS.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="a4fb9-122">При создании пула указывайте hello количества виртуальных машин и URL-адрес hello swagger.json hello объекта новый диспетчер ресурсов на основе веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="a4fb9-123">Эта веб-служба предоставляется tooestablish hello выставления счетов ассоциации.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="a4fb9-124">Hello пула службы использует hello swagger.json tooassociate hello пул с план выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="a4fb9-125">Можно выполнять любые BES обоих новый диспетчер ресурсов на основе веб-службы и классический, выбранная на пул hello.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="a4fb9-126">Можно использовать любую веб-службу на основе нового диспетчера ресурсов, но имейте в виду, что hello выставления счетов для заданий hello вычитается hello план выставления счетов, связанных с этой службой.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="a4fb9-127">Можно специально для выполнения заданий пула toocreate веб-службы и выставление счетов новый план.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="a4fb9-128">См. дополнительные сведения о [развертывании веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="a4fb9-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="a4fb9-129">После создания пула hello BES отправки задания с помощью hello URL-адрес пакета запросов для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="a4fb9-130">Вы можете toosubmit его tooa пула или tooclassic пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="a4fb9-131">toosubmit tooBatch пула задания обработки, добавьте следующий текст запроса отправки задания toohello параметр hello:</span><span class="sxs-lookup"><span data-stu-id="a4fb9-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="a4fb9-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="a4fb9-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="a4fb9-133">Если не добавить параметр hello, hello задание выполняется в среде процесса hello классический пакета.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="a4fb9-134">Если пул hello имеются доступные ресурсы, задание hello запустится немедленно.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="a4fb9-135">Если пул hello не имеет свободных ресурсов, задания помещается в очередь, пока не будет доступен ресурс.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="a4fb9-136">Если регулярно достигнете hello емкости пулов, которое требуется больший объем, можно вызвать CSS и работать с репрезентативной tooincrease квот.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="a4fb9-137">Пример запроса:</span><span class="sxs-lookup"><span data-stu-id="a4fb9-137">Example Request:</span></span>

<span data-ttu-id="a4fb9-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="a4fb9-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="a4fb9-139">Рекомендации по обработке в пуле пакетной службы</span><span class="sxs-lookup"><span data-stu-id="a4fb9-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="a4fb9-140">Пакетная обработка пул — это всегда на оплачиваемых служба и, требует tooassociate его с помощью диспетчера ресурсов на основе план выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="a4fb9-141">Только выставляется hello количества часов вычислений, выполняемых hello пула; независимо от того, количество заданий, выполняющихся во время этого пула время hello.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="a4fb9-142">При создании пула вас взимается плата за часы hello вычислений для всех виртуальных машин в пуле hello до удаления пула hello, даже если не пакетных заданий, запущенных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="a4fb9-143">Выставление счетов для виртуальных машин hello запускается после завершения подготовки и останавливается, если они были удалены.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="a4fb9-144">Можно использовать любой из планов hello, найденных на hello [цены обучения машины](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="a4fb9-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="a4fb9-145">Пример выставления счетов</span><span class="sxs-lookup"><span data-stu-id="a4fb9-145">Billing example:</span></span>

<span data-ttu-id="a4fb9-146">Если вы создадите пул пакетной службы с двумя виртуальными машинами, а спустя 24 часа удалите его, согласно плану выставления счетов оплата будет начислена за 48 часов вычислений, независимо от того, сколько заданий выполнялось в это время.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="a4fb9-147">Если вы создадите пул пакетной службы с четырьмя виртуальными машинами, а спустя 12 часов удалите его, согласно плану выставления счетов оплата также будет начислена за 48 часов вычислений.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="a4fb9-148">Корпорация Майкрософт рекомендует опроса состояния toodetermine hello задания после завершения выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="a4fb9-149">После завершения выполнения всех заданий вызов hello изменения размера пула операции tooset hello количество виртуальных машин в пул toozero hello.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="a4fb9-150">Если вам не хватает ресурсов пула и необходимо, чтобы toocreate пула, например toobill от другой план выставления счетов hello пул можно удалить вместо этого после завершения работы всех заданий.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="a4fb9-151">**Используйте обработку, выполняемую пулом пакетной службы в таких случаях**</span><span class="sxs-lookup"><span data-stu-id="a4fb9-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="a4fb9-152">**Используйте классическую пакетную обработку в таких случаях**</span><span class="sxs-lookup"><span data-stu-id="a4fb9-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="a4fb9-153">Требуется toorun большое количество заданий</span><span class="sxs-lookup"><span data-stu-id="a4fb9-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="a4fb9-154">Или</span><span class="sxs-lookup"><span data-stu-id="a4fb9-154">Or</span></span><br/><span data-ttu-id="a4fb9-155">Требуется tooknow, немедленно запустить заданиям</span><span class="sxs-lookup"><span data-stu-id="a4fb9-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="a4fb9-156">Или</span><span class="sxs-lookup"><span data-stu-id="a4fb9-156">Or</span></span><br/><span data-ttu-id="a4fb9-157">Требуется гарантированная пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-157">You need guaranteed throughput.</span></span> <span data-ttu-id="a4fb9-158">Например требуется toorun число заданий в заданный период времени и необходимости tooscale out вашей toomeet вычислительные ресурсы вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="a4fb9-159">Вы выполняете несколько заданий.</span><span class="sxs-lookup"><span data-stu-id="a4fb9-159">You are running just a few jobs</span></span><br/><span data-ttu-id="a4fb9-160">и</span><span class="sxs-lookup"><span data-stu-id="a4fb9-160">And</span></span><br/> <span data-ttu-id="a4fb9-161">Не требуется toorun заданий hello немедленно</span><span class="sxs-lookup"><span data-stu-id="a4fb9-161">You don’t need hello jobs toorun immediately</span></span> |
