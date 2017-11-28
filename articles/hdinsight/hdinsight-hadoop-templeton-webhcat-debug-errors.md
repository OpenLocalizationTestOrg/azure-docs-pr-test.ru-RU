---
title: "aaaUnderstand и устранение ошибок WebHCat на HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как распространенные ошибки tooabout возвращенных WebHCat на HDInsight и как tooresolve их."
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
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="0a89a-103">Понимание и устранение ошибок, полученных из WebHCat в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a89a-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="0a89a-104">Дополнительные сведения об ошибках, полученное при использовании WebHCat с HDInsight и о том, как tooresolve их.</span><span class="sxs-lookup"><span data-stu-id="0a89a-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="0a89a-105">WebHCat используется внутренне клиентские средства, такие как Azure PowerShell и hello Озера Data Tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a89a-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="0a89a-106">Что такое WebHCat</span><span class="sxs-lookup"><span data-stu-id="0a89a-106">What is WebHCat</span></span>

<span data-ttu-id="0a89a-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) — это REST API для [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), уровень управления таблицами и хранилищем данных для Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0a89a-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="0a89a-108">WebHCat включена по умолчанию в кластерах HDInsight и используется заданиями toosubmit различные средства, получить состояние задания, т. д., не входя в кластере toohello.</span><span class="sxs-lookup"><span data-stu-id="0a89a-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="0a89a-109">Изменение конфигурации</span><span class="sxs-lookup"><span data-stu-id="0a89a-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a89a-110">Некоторые из hello ошибок, перечисленных в этом документе возникают из-за превышения заданного максимума.</span><span class="sxs-lookup"><span data-stu-id="0a89a-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="0a89a-111">При шаг разрешение hello указывается, что можно изменить значение, необходимо использовать один hello после изменения hello tooperform:</span><span class="sxs-lookup"><span data-stu-id="0a89a-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="0a89a-112">Для **Windows** кластеров: используйте значение hello tooconfigure действие сценария во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="0a89a-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="0a89a-113">Для получения дополнительных сведений обратитесь к разделу [Разработка сценариев Action Script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="0a89a-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="0a89a-114">Для **Linux** кластеров: значение hello toomodify Ambari использования (веб- или REST API).</span><span class="sxs-lookup"><span data-stu-id="0a89a-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="0a89a-115">Для получения дополнительных сведений обратитесь к разделу [Управления HDInsight с помощью Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="0a89a-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a89a-116">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="0a89a-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0a89a-117">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0a89a-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="0a89a-118">Конфигурация по умолчанию</span><span class="sxs-lookup"><span data-stu-id="0a89a-118">Default configuration</span></span>

<span data-ttu-id="0a89a-119">При превышении следующие значения по умолчанию hello можно привести к снижению производительности WebHCat или привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="0a89a-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="0a89a-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="0a89a-120">Setting</span></span> | <span data-ttu-id="0a89a-121">Действие</span><span class="sxs-lookup"><span data-stu-id="0a89a-121">What it does</span></span> | <span data-ttu-id="0a89a-122">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="0a89a-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a89a-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="0a89a-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="0a89a-124">Здравствуйте, максимальное количество заданий, которые могут быть активными одновременно (ожидающие или выполняемые)</span><span class="sxs-lookup"><span data-stu-id="0a89a-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="0a89a-125">10 000</span><span class="sxs-lookup"><span data-stu-id="0a89a-125">10,000</span></span> |
| <span data-ttu-id="0a89a-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="0a89a-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="0a89a-127">Максимальное число запросов, которые могут обрабатываться параллельно Hello</span><span class="sxs-lookup"><span data-stu-id="0a89a-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="0a89a-128">20</span><span class="sxs-lookup"><span data-stu-id="0a89a-128">20</span></span> |
| <span data-ttu-id="0a89a-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="0a89a-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="0a89a-130">сохраняются Hello, сколько дней журнал заданий</span><span class="sxs-lookup"><span data-stu-id="0a89a-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="0a89a-131">7 дней</span><span class="sxs-lookup"><span data-stu-id="0a89a-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="0a89a-132">Слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="0a89a-132">Too many requests</span></span>

<span data-ttu-id="0a89a-133">**Код состояния HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="0a89a-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="0a89a-134">Причина:</span><span class="sxs-lookup"><span data-stu-id="0a89a-134">Cause</span></span> | <span data-ttu-id="0a89a-135">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="0a89a-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0a89a-136">Вы превысили hello максимальное число параллельных запросов обслуживается WebHCat в минуту (по умолчанию 20)</span><span class="sxs-lookup"><span data-stu-id="0a89a-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="0a89a-137">Уменьшить tooensure вашей рабочей нагрузки, не отправлять больше, чем hello максимальное число одновременных запросов или увеличить hello ограничение одновременных запросов на изменение `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="0a89a-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="0a89a-138">Для получения дополнительных сведений ознакомьтесь с разделом [Изменение конфигурации](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="0a89a-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="0a89a-139">Сервер недоступен</span><span class="sxs-lookup"><span data-stu-id="0a89a-139">Server unavailable</span></span>

<span data-ttu-id="0a89a-140">**Код состояния HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="0a89a-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="0a89a-141">Причина:</span><span class="sxs-lookup"><span data-stu-id="0a89a-141">Cause</span></span> | <span data-ttu-id="0a89a-142">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="0a89a-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0a89a-143">Этот код состояния обычно происходит во время отработки отказа между hello первичной и вторичной головному узлу кластера hello</span><span class="sxs-lookup"><span data-stu-id="0a89a-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="0a89a-144">Подождите две минуты, а затем повторите операцию hello</span><span class="sxs-lookup"><span data-stu-id="0a89a-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="0a89a-145">Неправильный запрос содержимого: не удалось найти задание</span><span class="sxs-lookup"><span data-stu-id="0a89a-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="0a89a-146">**Код состояния HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="0a89a-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="0a89a-147">Причина:</span><span class="sxs-lookup"><span data-stu-id="0a89a-147">Cause</span></span> | <span data-ttu-id="0a89a-148">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="0a89a-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0a89a-149">Сведения о заданиях, были очищены, журнал заданий hello очистки</span><span class="sxs-lookup"><span data-stu-id="0a89a-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="0a89a-150">срок хранения по умолчанию Hello для журнала заданий составляет 7 дней.</span><span class="sxs-lookup"><span data-stu-id="0a89a-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="0a89a-151">срок хранения по умолчанию Hello может быть изменен путем изменения `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="0a89a-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="0a89a-152">Для получения дополнительных сведений ознакомьтесь с разделом [Изменение конфигурации](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="0a89a-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="0a89a-153">Задание был прекращен из-за tooa перехода на другой ресурс</span><span class="sxs-lookup"><span data-stu-id="0a89a-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="0a89a-154">Повторите попытку отправки заданий для копирования tootwo минут</span><span class="sxs-lookup"><span data-stu-id="0a89a-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="0a89a-155">Был использован недопустимый идентификатор задания</span><span class="sxs-lookup"><span data-stu-id="0a89a-155">An Invalid job id was used</span></span> |<span data-ttu-id="0a89a-156">Проверьте правильность идентификатора задания hello</span><span class="sxs-lookup"><span data-stu-id="0a89a-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="0a89a-157">Недопустимый шлюз</span><span class="sxs-lookup"><span data-stu-id="0a89a-157">Bad gateway</span></span>

<span data-ttu-id="0a89a-158">**Код состояния HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="0a89a-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="0a89a-159">Причина:</span><span class="sxs-lookup"><span data-stu-id="0a89a-159">Cause</span></span> | <span data-ttu-id="0a89a-160">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="0a89a-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="0a89a-161">Внутренняя сборка мусора выполняется в hello WebHCat процесса</span><span class="sxs-lookup"><span data-stu-id="0a89a-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="0a89a-162">Дождитесь toofinish сбора мусора и перезапуск службы WebHCat hello</span><span class="sxs-lookup"><span data-stu-id="0a89a-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="0a89a-163">Время ожидания истекло, Ожидание ответа от службы ResourceManager hello.</span><span class="sxs-lookup"><span data-stu-id="0a89a-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="0a89a-164">Эта ошибка может возникать, когда hello число активных приложений становится более hello настроен (по умолчанию 10 000)</span><span class="sxs-lookup"><span data-stu-id="0a89a-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="0a89a-165">Подождите выполняющихся заданий toocomplete или увеличить ограничение одновременных заданий hello, изменив `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="0a89a-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="0a89a-166">Дополнительные сведения см. в разделе hello [изменение конфигурации](#modifying-configuration) раздела.</span><span class="sxs-lookup"><span data-stu-id="0a89a-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="0a89a-167">Попытка tooretrieve все задания через hello [GET/Jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) вызова при `Fields` задано слишком`*`</span><span class="sxs-lookup"><span data-stu-id="0a89a-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="0a89a-168">Не пытайтесь получить сведения о *всех* заданиях.</span><span class="sxs-lookup"><span data-stu-id="0a89a-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="0a89a-169">Вместо этого используйте `jobid` tooretrieve сведения о заданиях, только больше определенных идентификатор задания. Или не используйте `Fields`</span><span class="sxs-lookup"><span data-stu-id="0a89a-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="0a89a-170">Hello службы WebHCat не работает во время отработки отказа головному узлу</span><span class="sxs-lookup"><span data-stu-id="0a89a-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="0a89a-171">Подождите 2 минуты и повторите операцию hello</span><span class="sxs-lookup"><span data-stu-id="0a89a-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="0a89a-172">В настоящий момент более 500 заданий, отправленных через WebHCat, находятся в режиме ожидания</span><span class="sxs-lookup"><span data-stu-id="0a89a-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="0a89a-173">Дождитесь завершения текущих заданий, находящихся в режиме ожидания, перед отправкой новых заданий</span><span class="sxs-lookup"><span data-stu-id="0a89a-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
