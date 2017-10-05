---
title: "Понимание и устранение ошибок WebHCat в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте о наиболее распространенных ошибках, возвращаемых WebHCat в HDInsight, и о способах их устранения."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="34c25-103">Понимание и устранение ошибок, полученных из WebHCat в HDInsight</span><span class="sxs-lookup"><span data-stu-id="34c25-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="34c25-104">Дополнительные сведения об ошибках, возникающих при использовании WebHCat в HDInsight, а также способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="34c25-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="34c25-105">WebHCat используется во внутренних процессах таких клиентских инструментов, как Azure PowerShell и средства Azure Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34c25-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="34c25-106">Что такое WebHCat</span><span class="sxs-lookup"><span data-stu-id="34c25-106">What is WebHCat</span></span>

<span data-ttu-id="34c25-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) — это REST API для [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), уровень управления таблицами и хранилищем данных для Hadoop.</span><span class="sxs-lookup"><span data-stu-id="34c25-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="34c25-108">WebHCat активирован по умолчанию в кластерах HDInsight и используется различными средствами для отправки заданий, получения состояния задания и т. д. без входа в кластер.</span><span class="sxs-lookup"><span data-stu-id="34c25-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="34c25-109">Изменение конфигурации</span><span class="sxs-lookup"><span data-stu-id="34c25-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34c25-110">Некоторые из ошибок, приведенных в этом документе, возникают из-за превышения установленного максимума.</span><span class="sxs-lookup"><span data-stu-id="34c25-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="34c25-111">Если на этапе разрешения ошибки упоминается, что можно изменить значение, необходимо сделать одно из следующих действий для внесения изменений:</span><span class="sxs-lookup"><span data-stu-id="34c25-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="34c25-112">Для кластеров на основе **Windows** : используйте Action Script, чтобы настроить значение во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="34c25-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="34c25-113">Для получения дополнительных сведений обратитесь к разделу [Разработка сценариев Action Script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="34c25-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="34c25-114">Для кластеров на основе **Linux** : используйте Ambari (онлайн версию или API-Интерфейс REST) для изменения значения.</span><span class="sxs-lookup"><span data-stu-id="34c25-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="34c25-115">Для получения дополнительных сведений обратитесь к разделу [Управления HDInsight с помощью Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="34c25-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34c25-116">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="34c25-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="34c25-117">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="34c25-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="34c25-118">Конфигурация по умолчанию</span><span class="sxs-lookup"><span data-stu-id="34c25-118">Default configuration</span></span>

<span data-ttu-id="34c25-119">При превышении следующих значений по умолчанию может снизиться производительность WebHCat или могут возникнуть ошибки.</span><span class="sxs-lookup"><span data-stu-id="34c25-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="34c25-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="34c25-120">Setting</span></span> | <span data-ttu-id="34c25-121">Действие</span><span class="sxs-lookup"><span data-stu-id="34c25-121">What it does</span></span> | <span data-ttu-id="34c25-122">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="34c25-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34c25-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="34c25-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="34c25-124">Максимальное количество заданий, которые могут быть активны одновременно (в состоянии ожидания или выполнения)</span><span class="sxs-lookup"><span data-stu-id="34c25-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="34c25-125">10 000</span><span class="sxs-lookup"><span data-stu-id="34c25-125">10,000</span></span> |
| <span data-ttu-id="34c25-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="34c25-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="34c25-127">Максимальное число запросов, которые могут обрабатываться параллельно</span><span class="sxs-lookup"><span data-stu-id="34c25-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="34c25-128">20</span><span class="sxs-lookup"><span data-stu-id="34c25-128">20</span></span> |
| <span data-ttu-id="34c25-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="34c25-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="34c25-130">Число дней, в течение которых хранится журнал заданий.</span><span class="sxs-lookup"><span data-stu-id="34c25-130">The number of days that job history are retained</span></span> |<span data-ttu-id="34c25-131">7 дней</span><span class="sxs-lookup"><span data-stu-id="34c25-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="34c25-132">Слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="34c25-132">Too many requests</span></span>

<span data-ttu-id="34c25-133">**Код состояния HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="34c25-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="34c25-134">Причина:</span><span class="sxs-lookup"><span data-stu-id="34c25-134">Cause</span></span> | <span data-ttu-id="34c25-135">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="34c25-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="34c25-136">Превышено максимальное число одновременных запросов, обслуживаемых WebHCat в минуту (по умолчанию 20)</span><span class="sxs-lookup"><span data-stu-id="34c25-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="34c25-137">Уменьшить рабочую нагрузку, чтобы убедиться, что не будет отправлено больше, чем максимальное количество параллельных запросов, или увеличить количество одновременных запросов путем изменения `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="34c25-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="34c25-138">Для получения дополнительных сведений ознакомьтесь с разделом [Изменение конфигурации](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="34c25-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="34c25-139">Сервер недоступен</span><span class="sxs-lookup"><span data-stu-id="34c25-139">Server unavailable</span></span>

<span data-ttu-id="34c25-140">**Код состояния HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="34c25-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="34c25-141">Причина:</span><span class="sxs-lookup"><span data-stu-id="34c25-141">Cause</span></span> | <span data-ttu-id="34c25-142">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="34c25-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="34c25-143">Обычно этот код состояния отображается во время обработки отказа между первичным и вторичным головным узлом кластера.</span><span class="sxs-lookup"><span data-stu-id="34c25-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="34c25-144">Подождите две минуты, а затем повторите операцию</span><span class="sxs-lookup"><span data-stu-id="34c25-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="34c25-145">Неправильный запрос содержимого: не удалось найти задание</span><span class="sxs-lookup"><span data-stu-id="34c25-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="34c25-146">**Код состояния HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="34c25-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="34c25-147">Причина:</span><span class="sxs-lookup"><span data-stu-id="34c25-147">Cause</span></span> | <span data-ttu-id="34c25-148">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="34c25-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="34c25-149">Сведения о задании были удалены утилитой очистки журнала заданий</span><span class="sxs-lookup"><span data-stu-id="34c25-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="34c25-150">Срок хранения по умолчанию для журнала заданий составляет 7 дней.</span><span class="sxs-lookup"><span data-stu-id="34c25-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="34c25-151">Его можно изменить, внеся изменения в `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="34c25-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="34c25-152">Для получения дополнительных сведений ознакомьтесь с разделом [Изменение конфигурации](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="34c25-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="34c25-153">Задание был прекращено из-за отработки отказа</span><span class="sxs-lookup"><span data-stu-id="34c25-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="34c25-154">Повторить попытку отправки задания через две минуты.</span><span class="sxs-lookup"><span data-stu-id="34c25-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="34c25-155">Был использован недопустимый идентификатор задания</span><span class="sxs-lookup"><span data-stu-id="34c25-155">An Invalid job id was used</span></span> |<span data-ttu-id="34c25-156">Проверьте правильность идентификатора задания</span><span class="sxs-lookup"><span data-stu-id="34c25-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="34c25-157">Недопустимый шлюз</span><span class="sxs-lookup"><span data-stu-id="34c25-157">Bad gateway</span></span>

<span data-ttu-id="34c25-158">**Код состояния HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="34c25-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="34c25-159">Причина:</span><span class="sxs-lookup"><span data-stu-id="34c25-159">Cause</span></span> | <span data-ttu-id="34c25-160">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="34c25-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="34c25-161">Внутренний сбор мусора происходит в процессе WebHCat</span><span class="sxs-lookup"><span data-stu-id="34c25-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="34c25-162">Дождитесь завершения процесса сбора мусора или перезапустите службу WebHCat</span><span class="sxs-lookup"><span data-stu-id="34c25-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="34c25-163">Превышено время ожидания ответа от службы Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="34c25-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="34c25-164">Эта ошибка может произойти, когда число активных приложений становится выше заданного максимума (по умолчанию 10 000).</span><span class="sxs-lookup"><span data-stu-id="34c25-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="34c25-165">Дождитесь завершения выполняемых заданий или увеличьте ограничение на количество одновременно выполняемых заданий, изменив `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="34c25-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="34c25-166">Дополнительные сведения см. в разделе [Изменение конфигурации](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="34c25-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="34c25-167">Выполнена попытка получить все задания вызовом [GET /Jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) при `Fields` со значением `*`.</span><span class="sxs-lookup"><span data-stu-id="34c25-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="34c25-168">Не пытайтесь получить сведения о *всех* заданиях.</span><span class="sxs-lookup"><span data-stu-id="34c25-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="34c25-169">Вместо этого используйте `jobid` для получения сведений только о тех заданиях, идентификатор которых больше определенного значения.</span><span class="sxs-lookup"><span data-stu-id="34c25-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="34c25-170">Или не используйте `Fields`</span><span class="sxs-lookup"><span data-stu-id="34c25-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="34c25-171">Служба WebHCat не работает во время отработки отказа узла HeadNode</span><span class="sxs-lookup"><span data-stu-id="34c25-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="34c25-172">Подождите 2 минуты и повторите попытку</span><span class="sxs-lookup"><span data-stu-id="34c25-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="34c25-173">В настоящий момент более 500 заданий, отправленных через WebHCat, находятся в режиме ожидания</span><span class="sxs-lookup"><span data-stu-id="34c25-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="34c25-174">Дождитесь завершения текущих заданий, находящихся в режиме ожидания, перед отправкой новых заданий</span><span class="sxs-lookup"><span data-stu-id="34c25-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
