---
title: "Выделение ресурсов для обработки заданий службы пакетного выполнения машинного обучения | Документация Майкрософт"
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
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="7f3b4-103">Пакетные службы Azure для обработки заданий машинного обучения</span><span class="sxs-lookup"><span data-stu-id="7f3b4-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="7f3b4-104">Обработка в пуле пакетной службы машинного обучения предоставляет пользователям управление масштабированием службы выполнения пакетов машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="7f3b4-105">Классическая пакетная обработка для машинного обучения выполняется в мультитенантной среде. Это связано с определенными ограничениями числа одновременно отправляемых заданий, которые при этом помещаются в очередь по принципу FIFO.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="7f3b4-106">Эта неопределенность, в свою очередь, означает, что время запуска задания предсказать невозможно.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="7f3b4-107">Обработка в пуле пакетной службы связана с возможностью создавать пулы, куда можно отправлять соответствующие задания.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="7f3b4-108">Вы управляете размером пула и определяете, в какой пул будет отправлено то или иное задание.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="7f3b4-109">Задание BES выполняется в отдельной области обработки, обеспечивая прогнозируемую производительность и возможность создавать пулы ресурсов, которые соответствуют отправляемой вычислительной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="7f3b4-110">Как выполняется обработка в пуле пакетной службы</span><span class="sxs-lookup"><span data-stu-id="7f3b4-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="7f3b4-111">Сейчас настройка обработки в пуле пакетной службы на портале Azure недоступна.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="7f3b4-112">Для выполнения обработки в пуле пакетной службы вам понадобится:</span><span class="sxs-lookup"><span data-stu-id="7f3b4-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="7f3b4-113">вызвать CSS, чтобы создать учетную запись пула пакетной службы и получить URL-адрес службы пула и ключ авторизации;</span><span class="sxs-lookup"><span data-stu-id="7f3b4-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="7f3b4-114">создать веб-службу и план выставления счетов на основе новой версии Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="7f3b4-115">Чтобы создать учетную запись, обратитесь в служба поддержки пользователей Майкрософт (CSS) и предоставьте свой идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="7f3b4-116">Служба CSS поможет вам определить ресурсы, соответствующие вашему сценарию.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="7f3b4-117">Затем служба CSS определит для вашей учетной записи максимальное число пулов, которые вы можете создать, а также максимальное число виртуальных машин, которые можно включить в каждый пул.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="7f3b4-118">Когда ваша учетная запись будет настроена, вам будет назначен URL-адрес службы пула и ключ авторизации,</span><span class="sxs-lookup"><span data-stu-id="7f3b4-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="7f3b4-119">которые будут использоваться для выполнения операций управления пулом в пуле пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Архитектура пула пакетной службы](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="7f3b4-121">Вы можете создавать пулы, вызывая операцию "Создание пула" и используя URL-адрес службы пула, предоставленный службой CSS.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="7f3b4-122">Создавая пул, укажите число виртуальных машин и URL-адрес веб-службы машинного обучения на основе новой версии Resource Manager (файл swagger.json).</span><span class="sxs-lookup"><span data-stu-id="7f3b4-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="7f3b4-123">Эта веб-служба позволяет установить связь с конфигурацией для выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="7f3b4-124">Пул пакетной службы использует файл swagger.json для связывания пула с планом выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="7f3b4-125">Вы можете запустить любую веб-службу BES (на основе новой версии Resource Manager или классическую) из пула.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="7f3b4-126">Вы можете использовать любую веб-службу на основе новой версии Resource Manager, но помните, что тарификация обработки заданий производится на основе плана выставления счетов, связанного с этой службой.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="7f3b4-127">Вы также можете создать веб-службу и план выставления счетов специально для запуска заданий пула пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="7f3b4-128">См. дополнительные сведения о [развертывании веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7f3b4-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="7f3b4-129">Создав пул, вы можете отправить задание BES, используя URL-адрес запросов пакетной службы для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="7f3b4-130">Задание можно отправить для классической пакетной обработки или обработки в пуле.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="7f3b4-131">Чтобы отправить задание для обработки в пуле пакетной службы, добавьте следующий параметр в текст запроса на отправку задания:</span><span class="sxs-lookup"><span data-stu-id="7f3b4-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="7f3b4-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="7f3b4-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="7f3b4-133">Если вы не добавите этот параметр, задание запустится в среде для классической пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="7f3b4-134">Если у пула есть доступные ресурсы, задание запустится немедленно.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="7f3b4-135">Если у пула нет свободных ресурсов, задание будет помещено в очередь, пока ресурсы не станут доступными.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="7f3b4-136">Если вы регулярно расходуете ресурсы, выделяемые для пулов, и вам нужно увеличить их объем, обратитесь в службу CSS. Ее сотрудники помогут вам увеличить квоты.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="7f3b4-137">Пример запроса:</span><span class="sxs-lookup"><span data-stu-id="7f3b4-137">Example Request:</span></span>

<span data-ttu-id="7f3b4-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="7f3b4-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="7f3b4-139">Рекомендации по обработке в пуле пакетной службы</span><span class="sxs-lookup"><span data-stu-id="7f3b4-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="7f3b4-140">Обработка в пуле пакетной службы предусматривает непрерывную тарификацию. Эту конфигурацию необходимо связать с планом выставления счетов на основе Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="7f3b4-141">Плата взимается только за часы вычислений (работы пула) — независимо от числа заданий, выполняемых в это время.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="7f3b4-142">Создав пул, вы оплачиваете часы вычислений для каждой виртуальной машины в пуле до удаления пула, даже если в пуле нет запущенных заданий пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="7f3b4-143">Выставление счетов для виртуальных машин начинается после завершения их подготовки и останавливается при их удалении.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="7f3b4-144">Можно использовать любой план из перечисленных на [странице с ценами на машинное обучение](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="7f3b4-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="7f3b4-145">Пример выставления счетов</span><span class="sxs-lookup"><span data-stu-id="7f3b4-145">Billing example:</span></span>

<span data-ttu-id="7f3b4-146">Если вы создадите пул пакетной службы с двумя виртуальными машинами, а спустя 24 часа удалите его, согласно плану выставления счетов оплата будет начислена за 48 часов вычислений, независимо от того, сколько заданий выполнялось в это время.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="7f3b4-147">Если вы создадите пул пакетной службы с четырьмя виртуальными машинами, а спустя 12 часов удалите его, согласно плану выставления счетов оплата также будет начислена за 48 часов вычислений.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="7f3b4-148">Мы рекомендуем выполнять опрос состояния заданий, чтобы определять время их завершения.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="7f3b4-149">Когда все задания будут выполнены, вызовите операцию "Изменение размера пула", чтобы изменить число виртуальных машин в пуле, указав значение 0.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="7f3b4-150">Если вам не хватает ресурсов для пула и нужно создать другой пул (например, для тарификации в соответствии с другим планом выставления счетов), вы можете просто удалить пул после выполнения всех заданий.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="7f3b4-151">**Используйте обработку, выполняемую пулом пакетной службы в таких случаях**</span><span class="sxs-lookup"><span data-stu-id="7f3b4-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="7f3b4-152">**Используйте классическую пакетную обработку в таких случаях**</span><span class="sxs-lookup"><span data-stu-id="7f3b4-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="7f3b4-153">Необходимо выполнить большое число заданий.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="7f3b4-154">Или</span><span class="sxs-lookup"><span data-stu-id="7f3b4-154">Or</span></span><br/><span data-ttu-id="7f3b4-155">Необходимо запускать задания немедленно.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="7f3b4-156">Или</span><span class="sxs-lookup"><span data-stu-id="7f3b4-156">Or</span></span><br/><span data-ttu-id="7f3b4-157">Требуется гарантированная пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-157">You need guaranteed throughput.</span></span> <span data-ttu-id="7f3b4-158">Например, за определенное время вам нужно выполнить ряд заданий, и вы хотите масштабировать требуемые вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="7f3b4-159">Вы выполняете несколько заданий.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-159">You are running just a few jobs</span></span><br/><span data-ttu-id="7f3b4-160">и</span><span class="sxs-lookup"><span data-stu-id="7f3b4-160">And</span></span><br/> <span data-ttu-id="7f3b4-161">Вам не нужно немедленно запускать эти задания.</span><span class="sxs-lookup"><span data-stu-id="7f3b4-161">You don’t need the jobs to run immediately</span></span> |
