---
title: "aaaContainer решения мониторинга в службе анализа журналов Azure | Документы Microsoft"
description: "решение для наблюдения за контейнера в службе анализа журналов Hello служит для просмотра и управления Docker и Windows узлы контейнера в одном месте."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="a0b89-103">Решение для мониторинга контейнеров в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a0b89-103">Container Monitoring solution in Log Analytics</span></span>

![Символ решения "Контейнеры"](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="a0b89-105">В этой статье описывается, как решение для наблюдения за контейнера в службы анализа журналов, который служит для просмотра и управления Docker и Windows hello tooset вверх и использовать узлы контейнера в одном месте.</span><span class="sxs-lookup"><span data-stu-id="a0b89-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="a0b89-106">Docker — программной системы виртуализации используются контейнеры toocreate для автоматизации развертывания программного обеспечения tootheir ИТ инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a0b89-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="a0b89-107">Здравствуйте, решение показывает, контейнеры, работающие под управлением, какой образ контейнера, они выполняются, и запущенным контейнеров.</span><span class="sxs-lookup"><span data-stu-id="a0b89-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="a0b89-108">Также можно просматривать подробные сведения аудита, в том числе команды, используемые в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="a0b89-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="a0b89-109">И устранения контейнеры с помощью просмотра и поиска централизованные журналы без необходимости представление tooremotely Docker или узлов Windows.</span><span class="sxs-lookup"><span data-stu-id="a0b89-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="a0b89-110">Решение позволяет находить контейнеры, содержащие ошибки и использующие слишком много ресурсов на узле.</span><span class="sxs-lookup"><span data-stu-id="a0b89-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="a0b89-111">Также у вас есть возможность централизованно просматривать сведения об использовании и производительности ЦП, памяти, хранилища и сети по контейнерам.</span><span class="sxs-lookup"><span data-stu-id="a0b89-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="a0b89-112">На компьютерах под управлением Windows можно централизовать и сравнивать журналы из Windows Server, Hyper-V и контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="a0b89-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="a0b89-113">решение Hello поддерживает следующие orchestrators контейнера hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="a0b89-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a0b89-114">Docker Swarm</span></span>
- <span data-ttu-id="a0b89-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="a0b89-115">DC/OS</span></span>
- <span data-ttu-id="a0b89-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="a0b89-116">Kubernetes</span></span>
- <span data-ttu-id="a0b89-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a0b89-117">Service Fabric</span></span>
- <span data-ttu-id="a0b89-118">Red Hat OpenShift.</span><span class="sxs-lookup"><span data-stu-id="a0b89-118">Red Hat OpenShift</span></span>


<span data-ttu-id="a0b89-119">Hello следующая диаграмма показывает hello связи между различными узлы контейнера и агентов в OMS.</span><span class="sxs-lookup"><span data-stu-id="a0b89-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Схема контейнеров](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="a0b89-121">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="a0b89-121">System requirements</span></span>

<span data-ttu-id="a0b89-122">Прежде чем начать, просмотрите следующие сведения о tooverify требованиям hello hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="a0b89-123">Поддержка решений для мониторинга контейнеров: оркестратор Docker и платформа ОС</span><span class="sxs-lookup"><span data-stu-id="a0b89-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="a0b89-124">Hello следующей таблице показано hello Docker orchestration и операционной системы, наблюдение за поддержку инвентаризации контейнера, производительности и журналов с помощью аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="a0b89-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="a0b89-125">ACS</span><span class="sxs-lookup"><span data-stu-id="a0b89-125">ACS</span></span> | <span data-ttu-id="a0b89-126">Linux</span><span class="sxs-lookup"><span data-stu-id="a0b89-126">Linux</span></span> | <span data-ttu-id="a0b89-127">Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-127">Windows</span></span> | <span data-ttu-id="a0b89-128">Контейнер</span><span class="sxs-lookup"><span data-stu-id="a0b89-128">Container</span></span><br><span data-ttu-id="a0b89-129">Список</span><span class="sxs-lookup"><span data-stu-id="a0b89-129">Inventory</span></span> | <span data-ttu-id="a0b89-130">Образ —</span><span class="sxs-lookup"><span data-stu-id="a0b89-130">Image</span></span><br><span data-ttu-id="a0b89-131">Список</span><span class="sxs-lookup"><span data-stu-id="a0b89-131">Inventory</span></span> | <span data-ttu-id="a0b89-132">Узел</span><span class="sxs-lookup"><span data-stu-id="a0b89-132">Node</span></span><br><span data-ttu-id="a0b89-133">Список</span><span class="sxs-lookup"><span data-stu-id="a0b89-133">Inventory</span></span> | <span data-ttu-id="a0b89-134">Контейнер</span><span class="sxs-lookup"><span data-stu-id="a0b89-134">Container</span></span><br><span data-ttu-id="a0b89-135">Производительность</span><span class="sxs-lookup"><span data-stu-id="a0b89-135">Performance</span></span> | <span data-ttu-id="a0b89-136">Контейнер</span><span class="sxs-lookup"><span data-stu-id="a0b89-136">Container</span></span><br><span data-ttu-id="a0b89-137">Событие</span><span class="sxs-lookup"><span data-stu-id="a0b89-137">Event</span></span> | <span data-ttu-id="a0b89-138">Событие</span><span class="sxs-lookup"><span data-stu-id="a0b89-138">Event</span></span><br><span data-ttu-id="a0b89-139">Журнал</span><span class="sxs-lookup"><span data-stu-id="a0b89-139">Log</span></span> | <span data-ttu-id="a0b89-140">Контейнер</span><span class="sxs-lookup"><span data-stu-id="a0b89-140">Container</span></span><br><span data-ttu-id="a0b89-141">Журнал</span><span class="sxs-lookup"><span data-stu-id="a0b89-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="a0b89-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="a0b89-142">Kubernetes</span></span> | <span data-ttu-id="a0b89-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-143">&#8226;</span></span> | <span data-ttu-id="a0b89-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-144">&#8226;</span></span> | | <span data-ttu-id="a0b89-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-145">&#8226;</span></span> | <span data-ttu-id="a0b89-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-146">&#8226;</span></span> | <span data-ttu-id="a0b89-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-147">&#8226;</span></span> | <span data-ttu-id="a0b89-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-148">&#8226;</span></span> | <span data-ttu-id="a0b89-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-149">&#8226;</span></span> | <span data-ttu-id="a0b89-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-150">&#8226;</span></span> | <span data-ttu-id="a0b89-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-151">&#8226;</span></span> |
| <span data-ttu-id="a0b89-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="a0b89-152">Mesosphere</span></span><br><span data-ttu-id="a0b89-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="a0b89-153">DC/OS</span></span> | <span data-ttu-id="a0b89-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-154">&#8226;</span></span> | <span data-ttu-id="a0b89-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-155">&#8226;</span></span> | | <span data-ttu-id="a0b89-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-156">&#8226;</span></span> | <span data-ttu-id="a0b89-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-157">&#8226;</span></span> | <span data-ttu-id="a0b89-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-158">&#8226;</span></span> | <span data-ttu-id="a0b89-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-159">&#8226;</span></span>| <span data-ttu-id="a0b89-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-160">&#8226;</span></span> | <span data-ttu-id="a0b89-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-161">&#8226;</span></span> | <span data-ttu-id="a0b89-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-162">&#8226;</span></span> |
| <span data-ttu-id="a0b89-163">Docker</span><span class="sxs-lookup"><span data-stu-id="a0b89-163">Docker</span></span><br><span data-ttu-id="a0b89-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="a0b89-164">Swarm</span></span> | <span data-ttu-id="a0b89-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-165">&#8226;</span></span> | <span data-ttu-id="a0b89-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-166">&#8226;</span></span> | <span data-ttu-id="a0b89-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-167">&#8226;</span></span> | <span data-ttu-id="a0b89-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-168">&#8226;</span></span> | <span data-ttu-id="a0b89-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-169">&#8226;</span></span> | <span data-ttu-id="a0b89-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-170">&#8226;</span></span> | <span data-ttu-id="a0b89-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-171">&#8226;</span></span> | <span data-ttu-id="a0b89-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-172">&#8226;</span></span> | | <span data-ttu-id="a0b89-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-173">&#8226;</span></span> |
| <span data-ttu-id="a0b89-174">служба</span><span class="sxs-lookup"><span data-stu-id="a0b89-174">Service</span></span><br><span data-ttu-id="a0b89-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="a0b89-175">Fabric</span></span> | | | <span data-ttu-id="a0b89-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-176">&#8226;</span></span> | <span data-ttu-id="a0b89-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-177">&#8226;</span></span> | <span data-ttu-id="a0b89-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-178">&#8226;</span></span> | <span data-ttu-id="a0b89-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-179">&#8226;</span></span> | <span data-ttu-id="a0b89-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-180">&#8226;</span></span> | <span data-ttu-id="a0b89-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-181">&#8226;</span></span> | <span data-ttu-id="a0b89-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-182">&#8226;</span></span> | <span data-ttu-id="a0b89-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-183">&#8226;</span></span> |
| <span data-ttu-id="a0b89-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="a0b89-184">Red Hat Open</span></span><br><span data-ttu-id="a0b89-185">Shift</span><span class="sxs-lookup"><span data-stu-id="a0b89-185">Shift</span></span> | | <span data-ttu-id="a0b89-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-186">&#8226;</span></span> | | <span data-ttu-id="a0b89-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-187">&#8226;</span></span> | <span data-ttu-id="a0b89-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-188">&#8226;</span></span>| <span data-ttu-id="a0b89-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-189">&#8226;</span></span> | <span data-ttu-id="a0b89-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-190">&#8226;</span></span> | <span data-ttu-id="a0b89-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-191">&#8226;</span></span> | | <span data-ttu-id="a0b89-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-192">&#8226;</span></span> |
| <span data-ttu-id="a0b89-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="a0b89-193">Windows Server</span></span><br><span data-ttu-id="a0b89-194">(изолированный)</span><span class="sxs-lookup"><span data-stu-id="a0b89-194">(standalone)</span></span> | | | <span data-ttu-id="a0b89-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-195">&#8226;</span></span> | <span data-ttu-id="a0b89-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-196">&#8226;</span></span> | <span data-ttu-id="a0b89-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-197">&#8226;</span></span> | <span data-ttu-id="a0b89-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-198">&#8226;</span></span> | <span data-ttu-id="a0b89-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-199">&#8226;</span></span> | <span data-ttu-id="a0b89-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-200">&#8226;</span></span> | | <span data-ttu-id="a0b89-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-201">&#8226;</span></span> |
| <span data-ttu-id="a0b89-202">Linux Server</span><span class="sxs-lookup"><span data-stu-id="a0b89-202">Linux Server</span></span><br><span data-ttu-id="a0b89-203">(изолированный)</span><span class="sxs-lookup"><span data-stu-id="a0b89-203">(standalone)</span></span> | | <span data-ttu-id="a0b89-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-204">&#8226;</span></span> | | <span data-ttu-id="a0b89-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-205">&#8226;</span></span> | <span data-ttu-id="a0b89-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-206">&#8226;</span></span> | <span data-ttu-id="a0b89-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-207">&#8226;</span></span> | <span data-ttu-id="a0b89-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-208">&#8226;</span></span> | <span data-ttu-id="a0b89-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-209">&#8226;</span></span> | | <span data-ttu-id="a0b89-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0b89-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="a0b89-211">Версии Docker, поддерживаемые в Linux</span><span class="sxs-lookup"><span data-stu-id="a0b89-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="a0b89-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="a0b89-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="a0b89-213">Docker CE и EE v17.06</span><span class="sxs-lookup"><span data-stu-id="a0b89-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="a0b89-214">Дистрибутивы Linux x64, поддерживаемые в качестве узлов контейнера</span><span class="sxs-lookup"><span data-stu-id="a0b89-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="a0b89-215">Ubuntu 14.04 LTS и 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a0b89-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="a0b89-216">CoreOS (стабильный выпуск);</span><span class="sxs-lookup"><span data-stu-id="a0b89-216">CoreOS(stable)</span></span>
- <span data-ttu-id="a0b89-217">Amazon Linux 2016.09.0;</span><span class="sxs-lookup"><span data-stu-id="a0b89-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="a0b89-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="a0b89-218">openSUSE 13.2</span></span>
- <span data-ttu-id="a0b89-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="a0b89-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="a0b89-220">CentOS 7.2 и 7.3</span><span class="sxs-lookup"><span data-stu-id="a0b89-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="a0b89-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="a0b89-221">SLES 12</span></span>
- <span data-ttu-id="a0b89-222">RHEL 7.2 и 7.3</span><span class="sxs-lookup"><span data-stu-id="a0b89-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="a0b89-223">Платформа контейнеров Red Hat OpenShift (OCP) 3.4 и 3.5</span><span class="sxs-lookup"><span data-stu-id="a0b89-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="a0b89-224">Too1.8.8 DC/OS 1.7.3 ACS Mesosphere</span><span class="sxs-lookup"><span data-stu-id="a0b89-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="a0b89-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="a0b89-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="a0b89-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a0b89-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="a0b89-227">Поддерживаемая операционная система Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-227">Supported Windows operating system</span></span>

- <span data-ttu-id="a0b89-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a0b89-228">Windows Server 2016</span></span>
- <span data-ttu-id="a0b89-229">Юбилейный выпуск Windows 10 (профессиональный или корпоративный)</span><span class="sxs-lookup"><span data-stu-id="a0b89-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="a0b89-230">Версии Docker, поддерживаемые в Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="a0b89-231">Docker 1.12 и 1.13</span><span class="sxs-lookup"><span data-stu-id="a0b89-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="a0b89-232">Docker 17.03.0 и более поздних версий</span><span class="sxs-lookup"><span data-stu-id="a0b89-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="a0b89-233">Установка и настройка решения hello</span><span class="sxs-lookup"><span data-stu-id="a0b89-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="a0b89-234">Используйте следующие сведения tooinstall hello и настроить решение hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="a0b89-235">Добавление hello мониторинга контейнера решение tooyour OMS рабочей области из [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="a0b89-236">Установите и используйте Docker с агентом OMS.</span><span class="sxs-lookup"><span data-stu-id="a0b89-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="a0b89-237">В зависимости от операционной системы, можно выбрать из hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="a0b89-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="a0b89-238">Установите на поддерживаемых операционных систем Linux, а запуска Docker и затем установите и настройте hello [агента OMS для Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="a0b89-239">На CoreOS невозможно запустить hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="a0b89-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="a0b89-240">Вместо этого выполняется контейнерного версии hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="a0b89-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="a0b89-241">Если вы работаете с контейнерами в облаке "Azure для государственных организаций", то см. раздел [Для всех узлов контейнера Linux, включая CoreOS](#for-all-linux-container-hosts-including-coreos) или [Для всех узлов контейнера Linux Azure для государственных организаций, включая CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos).</span><span class="sxs-lookup"><span data-stu-id="a0b89-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="a0b89-242">В Windows Server 2016 и Windows 10 установить hello подсистемы Docker и клиент затем подключения агента toogather сведения и отправить его tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="a0b89-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="a0b89-243">Служба контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-243">Container services</span></span>

- <span data-ttu-id="a0b89-244">Если вы используете среду Red Hat OpenShift, то см. раздел [Настройка агента OMS для Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="a0b89-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="a0b89-245">При наличии Kubernetes кластер, использующий hello контейнера службы Azure, просмотрите [мониторинга контейнера службы Azure с Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="a0b89-246">При наличии кластера DC/OS в службе контейнеров Azure дополнительные сведения см. в статье [Мониторинг кластера DC/OS в службе контейнеров Azure с помощью Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="a0b89-247">При наличии среды режима Docker Swarm ознакомьтесь с разделом [Настройка агента OMS для Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="a0b89-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="a0b89-248">При использовании контейнеров с Service Fabric см. статью [Общие сведения о Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="a0b89-249">Просмотрите hello [подсистема Docker в Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) статьи для получения дополнительных сведений о tooinstall и настройте ядер Docker на компьютерах под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="a0b89-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0b89-250">Должен быть запущен docker **перед** установить hello [агента OMS для Linux](log-analytics-agent-linux.md) узлов контейнера.</span><span class="sxs-lookup"><span data-stu-id="a0b89-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="a0b89-251">Если уже установлен агент hello перед установкой Docker, необходимо tooreinstall hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="a0b89-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="a0b89-252">Дополнительные сведения о Docker см. в разделе hello [веб-узел Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="a0b89-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="a0b89-253">Узлы контейнера Linux</span><span class="sxs-lookup"><span data-stu-id="a0b89-253">Linux container hosts</span></span>

<span data-ttu-id="a0b89-254">После установки Docker, используйте следующие параметры для агента hello tooconfigure узла контейнера для использования с помощью Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="a0b89-255">Во-первых, требуется свой идентификатор рабочей области OMS и ключ, который можно найти в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a0b89-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="a0b89-256">В рабочей области, нажмите кнопку **быстрый запуск** > **компьютеры** tooview вашей **идентификатор рабочей области** и **первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="a0b89-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="a0b89-257">Скопируйте их и вставьте в любой удобный для вас редактор.</span><span class="sxs-lookup"><span data-stu-id="a0b89-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="a0b89-258">Для всех узлов контейнера Linux, за исключением CoreOS</span><span class="sxs-lookup"><span data-stu-id="a0b89-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="a0b89-259">Дополнительные сведения и инструкции по как tooinstall hello агента OMS для Linux см. в разделе [подключения на компьютерах Linux tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="a0b89-260">Для всех узлов контейнера Linux, включая CoreOS</span><span class="sxs-lookup"><span data-stu-id="a0b89-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="a0b89-261">Запустите контейнер hello OMS, что требуется toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a0b89-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="a0b89-262">Изменить и использовать следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="a0b89-263">Для всех узлов контейнера Linux Azure для государственных организаций, включая CoreOS</span><span class="sxs-lookup"><span data-stu-id="a0b89-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="a0b89-264">Запустите контейнер hello OMS, что требуется toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a0b89-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="a0b89-265">Изменить и использовать следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="a0b89-266">Переключение из установленных tooone агент Linux, в контейнере с помощью</span><span class="sxs-lookup"><span data-stu-id="a0b89-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="a0b89-267">Если ранее используется hello напрямую установлен агент и требуется использование tooinstead агента, работающего в контейнере, необходимо сначала удалить hello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="a0b89-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="a0b89-268">В разделе [hello Удаление агента OMS для Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand, как удалить toosuccessfully hello агента.</span><span class="sxs-lookup"><span data-stu-id="a0b89-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="a0b89-269">Настройка агента OMS для Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a0b89-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="a0b89-270">Hello агента OMS как глобальная служба запускается с помощью Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a0b89-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="a0b89-271">Используйте следующие сведения toocreate службу агента OMS hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="a0b89-272">Необходимо tooinsert идентификатор рабочей области OMS и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="a0b89-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="a0b89-273">Запустите следующие hello hello главного узла.</span><span class="sxs-lookup"><span data-stu-id="a0b89-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="a0b89-274">Настройка агента OMS для Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="a0b89-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="a0b89-275">Нет агента OMS hello tooRed Hat OpenShift toostart сбора данных мониторинга данные контейнера для трех способов tooadd.</span><span class="sxs-lookup"><span data-stu-id="a0b89-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="a0b89-276">[Установка hello агента OMS для Linux](log-analytics-agent-linux.md) непосредственно на каждом узле OpenShift</span><span class="sxs-lookup"><span data-stu-id="a0b89-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="a0b89-277">[включить расширение виртуальной машины Log Analytics](log-analytics-azure-vm-extension.md) на каждом узле OpenShift, размещенном в Azure;</span><span class="sxs-lookup"><span data-stu-id="a0b89-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="a0b89-278">Установка агента OMS hello как набор управляющей программы OpenShift</span><span class="sxs-lookup"><span data-stu-id="a0b89-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="a0b89-279">В этом разделе будет рассматриваться как набор управляющая программа OpenShift hello действия требуется tooinstall hello агента OMS.</span><span class="sxs-lookup"><span data-stu-id="a0b89-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="a0b89-280">Войдите на toohello OpenShift главного узла и скопируйте hello yaml файла [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) из GitHub tooyour главного узла и изменить значение hello с Идентификатором рабочей области OMS и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="a0b89-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="a0b89-281">Запустите следующие команды toocreate hello проекта для OMS и задайте hello учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0b89-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="a0b89-282">hello toodeploy управляющей программы набора, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="a0b89-283">tooverify может быть сконфигурирован и работают правильно, введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="a0b89-284">и hello выходные данные должны иметь:</span><span class="sxs-lookup"><span data-stu-id="a0b89-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="a0b89-285">Секреты toosecure toouse идентификатор рабочей области OMS и первичный ключ при использовании файла yaml набор управляющей программы агента OMS hello, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="a0b89-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="a0b89-286">Войдите на toohello OpenShift главного узла и скопируйте hello yaml файла [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) и секрет Создание сценария [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) из GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0b89-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="a0b89-287">Данный сценарий создаст файл yaml секреты hello для toosecure идентификатор рабочей области OMS и первичный ключ к secrete сведения.</span><span class="sxs-lookup"><span data-stu-id="a0b89-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="a0b89-288">Запустите следующие команды toocreate hello проекта для OMS и задайте hello учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0b89-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="a0b89-289">Создание скрипта секрет Hello запрашивает свой идентификатор рабочей области OMS <WSID> и первичный ключ <KEY> и после завершения, он создает файл ocp secret.yaml hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="a0b89-290">Развертывание файла секретный hello, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="a0b89-291">Проверка развертывания, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="a0b89-292">и hello выходные данные должны иметь:</span><span class="sxs-lookup"><span data-stu-id="a0b89-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="a0b89-293">Развертывание файла yaml набор управляющей программы агента OMS hello, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="a0b89-294">Проверка развертывания, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="a0b89-295">и hello выходные данные должны иметь:</span><span class="sxs-lookup"><span data-stu-id="a0b89-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="a0b89-296">Защита секретных сведений для Docker Swarm и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a0b89-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="a0b89-297">Вы можете защитить секретный идентификатор рабочей области OMS и первичные ключи для служб контейнеров Docker Swarm и Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a0b89-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="a0b89-298">Защита секретов для Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a0b89-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="a0b89-299">Для помощью Docker Swarm, создав hello секрет для идентификатора рабочей области и первичный ключ, вы можете запустить hello создайте службу hello Docker для OMSagent.</span><span class="sxs-lookup"><span data-stu-id="a0b89-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="a0b89-300">Используйте следующие сведения toocreate hello секретные данные.</span><span class="sxs-lookup"><span data-stu-id="a0b89-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="a0b89-301">Запустите следующие hello hello главного узла.</span><span class="sxs-lookup"><span data-stu-id="a0b89-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="a0b89-302">Убедитесь, что секретные данные созданы надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="a0b89-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="a0b89-303">Выполнения hello, следующая команда toomount hello секреты toohello контейнерных агента OMS.</span><span class="sxs-lookup"><span data-stu-id="a0b89-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="a0b89-304">Защита секретов для Kubernetes с помощью файлов YAML</span><span class="sxs-lookup"><span data-stu-id="a0b89-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="a0b89-305">Для Kubernetes используйте файл сценария секреты hello toogenerate yaml для идентификатора рабочей области и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="a0b89-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="a0b89-306">В hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) есть файлы, которые можно использовать с или без вашего конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="a0b89-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="a0b89-307">Hello DaemonSet по умолчанию для агента OMS имеет секретные сведения (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="a0b89-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="a0b89-308">файл yaml Hello DaemonSet агента OMS использует секретные сведения (secrets.yaml omsagent доменных служб Active Directory) с файл yaml (omsagentsecret.yaml) секреты hello toogenerate секретный формирования сценариев.</span><span class="sxs-lookup"><span data-stu-id="a0b89-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="a0b89-309">Вы можете toocreate omsagent DaemonSets с или без секретные данные.</span><span class="sxs-lookup"><span data-stu-id="a0b89-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="a0b89-310">Стандартный файл YAML DaemonSet агента OMS без секретов</span><span class="sxs-lookup"><span data-stu-id="a0b89-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="a0b89-311">Для файла yaml DaemonSet агента OMS по умолчанию hello, замените hello `<WSID>` и `<KEY>` tooyour WSID и ключ.</span><span class="sxs-lookup"><span data-stu-id="a0b89-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="a0b89-312">Скопируйте hello файл tooyour главного узла и выполнения hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a0b89-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="a0b89-313">Стандартный файл YAML DaemonSet агента OMS с секретами</span><span class="sxs-lookup"><span data-stu-id="a0b89-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="a0b89-314">toouse DaemonSet агента OMS с помощью секретная информация, создайте hello секретные данные.</span><span class="sxs-lookup"><span data-stu-id="a0b89-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="a0b89-315">Скопируйте сценарий hello и файл секретный шаблона и убедитесь, что они находятся на hello один каталог.</span><span class="sxs-lookup"><span data-stu-id="a0b89-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="a0b89-316">Сценарий создания секретов — secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="a0b89-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="a0b89-317">Шаблон секретов — secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="a0b89-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="a0b89-318">Выполните сценарий hello, как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="a0b89-319">Hello скрипт запрашивает hello идентификатор рабочей области OMS и первичный ключ и после их ввода hello скрипт создает секретный yaml файл, чтобы можно было запустить.</span><span class="sxs-lookup"><span data-stu-id="a0b89-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="a0b89-320">Создайте pod hello секретные данные, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a0b89-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="a0b89-321">tooverify hello следующей:</span><span class="sxs-lookup"><span data-stu-id="a0b89-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="a0b89-322">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="a0b89-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="a0b89-323">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="a0b89-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="a0b89-324">Создание свой набор daemon-set omsagent, выполнив команду ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="a0b89-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="a0b89-325">Проверьте, hello запущенного DaemonSet агента OMS аналогичные toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="a0b89-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="a0b89-326">Для Kubernetes используйте файл сценария секреты hello toogenerate yaml идентификатор рабочей области и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="a0b89-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="a0b89-327">Hello используйте следующую информацию пример с hello [omsagent yaml файл](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure вашей конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="a0b89-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="a0b89-328">Узлы контейнеров Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="a0b89-329">Подготовка к установке агентов Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="a0b89-330">Прежде чем устанавливать агенты на компьютерах под управлением Windows, необходима служба Docker tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="a0b89-331">Настройка Hello позволяет hello Windows агента или hello анализа журналов виртуальную машину расширения toouse hello сокета Docker TCP, чтобы агенты hello можно удаленный доступ к управляющей программе Docker hello и toocapture данных мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a0b89-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="a0b89-332">toostart Docker и проверьте его конфигурацию</span><span class="sxs-lookup"><span data-stu-id="a0b89-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="a0b89-333">Существует tooset шаги, которые необходимы копирование TCP, именованный канал для Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a0b89-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="a0b89-334">Включите канал TCP и именованный канал в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0b89-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="a0b89-335">Настройка Docker с hello файла конфигурации для канала TCP и именованного канала.</span><span class="sxs-lookup"><span data-stu-id="a0b89-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="a0b89-336">Hello файл конфигурации расположен в C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="a0b89-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="a0b89-337">В файле daemon.json hello вам потребуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a0b89-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="a0b89-338">Дополнительные сведения о настройке управляющей программы Docker hello, используемые с контейнерами Windows см. в разделе [подсистема Docker в Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="a0b89-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="a0b89-339">Установка агентов Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-339">Install Windows agents</span></span>

<span data-ttu-id="a0b89-340">tooenable Windows и контейнер Hyper-V наблюдения, установите hello агента наблюдения Майкрософт (MMA) на компьютерах Windows, которые являются узлами контейнера.</span><span class="sxs-lookup"><span data-stu-id="a0b89-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="a0b89-341">Для компьютеров под управлением Windows в локальной среде, в разделе [tooLog компьютеров Windows для подключения аналитики](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="a0b89-342">Для виртуальных машин, запущенных в Azure, подключите их tooLog аналитика с помощью hello [расширение виртуальной машины](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="a0b89-343">Вы можете отслеживать контейнеры Windows, запущенные в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a0b89-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="a0b89-344">Однако сейчас для Service Fabric поддерживаются только [виртуальные машины, работающие в Azure](log-analytics-azure-vm-extension.md), и [компьютеры под управлением Windows в локальной среде](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="a0b89-345">Можно проверить, что правильно установлены, hello решения отслеживания контейнера Windows.</span><span class="sxs-lookup"><span data-stu-id="a0b89-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="a0b89-346">toocheck ли пакет управления hello был загрузки надлежащим образом, поиск *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="a0b89-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="a0b89-347">Hello файлы должны находиться в папке C:\Program Files\Microsoft мониторинг Agent\Agent\Health Service State\Management Packs hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="a0b89-348">Компоненты решения</span><span class="sxs-lookup"><span data-stu-id="a0b89-348">Solution components</span></span>

<span data-ttu-id="a0b89-349">При использовании агентов Windows, затем hello следующий пакет управления устанавливается на каждом компьютере с агентом при добавлении этого решения.</span><span class="sxs-lookup"><span data-stu-id="a0b89-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="a0b89-350">Настройки или обслуживания является обязательным для пакета управления hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="a0b89-351">*ContainerManagement.xxx* устанавливается в папке, расположенной по адресу C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="a0b89-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="a0b89-352">Сведения о сборе данных из контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-352">Container data collection details</span></span>
<span data-ttu-id="a0b89-353">Hello решения отслеживания контейнера сбор узлы контейнера и контейнеры, агенты, которые можно включить с помощью различных данных метрики и журнала производительности.</span><span class="sxs-lookup"><span data-stu-id="a0b89-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="a0b89-354">Собирает данные каждые три минуты hello следующие типы агентов.</span><span class="sxs-lookup"><span data-stu-id="a0b89-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="a0b89-355">Агент OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="a0b89-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="a0b89-356">Агент Windows</span><span class="sxs-lookup"><span data-stu-id="a0b89-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="a0b89-357">Расширение виртуальной машины Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a0b89-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="a0b89-358">Записи контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-358">Container records</span></span>

<span data-ttu-id="a0b89-359">Hello следующей таблице приведены примеры записей, собранные решением отслеживания контейнера hello и hello типы данных, которые отображаются в результатах поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="a0b89-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="a0b89-360">Тип данных</span><span class="sxs-lookup"><span data-stu-id="a0b89-360">Data type</span></span> | <span data-ttu-id="a0b89-361">Тип данных, используемый для поиска в журналах</span><span class="sxs-lookup"><span data-stu-id="a0b89-361">Data type in Log Search</span></span> | <span data-ttu-id="a0b89-362">Поля</span><span class="sxs-lookup"><span data-stu-id="a0b89-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0b89-363">Производительность узлов и контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="a0b89-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a0b89-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="a0b89-365">Список контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="a0b89-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="a0b89-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="a0b89-367">Список образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="a0b89-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="a0b89-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="a0b89-369">Журнал контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="a0b89-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="a0b89-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="a0b89-371">Журнал службы контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="a0b89-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="a0b89-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="a0b89-373">Список узлов контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="a0b89-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a0b89-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="a0b89-375">Список Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a0b89-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="a0b89-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a0b89-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="a0b89-377">Процесс контейнера</span><span class="sxs-lookup"><span data-stu-id="a0b89-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="a0b89-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a0b89-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="a0b89-379">События Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a0b89-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="a0b89-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="a0b89-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="a0b89-381">Метки добавлено слишком*PodLabel* типами данных являются собственные пользовательские метки.</span><span class="sxs-lookup"><span data-stu-id="a0b89-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="a0b89-382">Hello присоединенных PodLabel метки, приведенных в таблице hello приведены примеры.</span><span class="sxs-lookup"><span data-stu-id="a0b89-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="a0b89-383">Таким образом, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` будут отличаться в наборе данных вашей среды и должны выглядеть примерно так: `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="a0b89-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="a0b89-384">Мониторинг контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-384">Monitor containers</span></span>
<span data-ttu-id="a0b89-385">После включения на портале OMS hello решения hello, hello **контейнеры** плитки отображаются сводные данные о узлах контейнера и контейнерами hello в узлах.</span><span class="sxs-lookup"><span data-stu-id="a0b89-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Плитка "Контейнеры"](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="a0b89-387">Плитка приветствия приведен обзор количество контейнеров в среде hello и ли они все не удалось, запущенной или остановленной.</span><span class="sxs-lookup"><span data-stu-id="a0b89-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="a0b89-388">С помощью панели мониторинга контейнеры hello</span><span class="sxs-lookup"><span data-stu-id="a0b89-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="a0b89-389">Нажмите кнопку hello **контейнеры** плитки.</span><span class="sxs-lookup"><span data-stu-id="a0b89-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="a0b89-390">Отсюда можно открыть представления, упорядоченные по:</span><span class="sxs-lookup"><span data-stu-id="a0b89-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="a0b89-391">**Событиям контейнера.** Здесь отображается состояние контейнера и компьютеры, содержащие контейнеры со сбоями.</span><span class="sxs-lookup"><span data-stu-id="a0b89-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="a0b89-392">**Журналы контейнера** -показана диаграмма контейнера файлов журнала, созданные со временем и список компьютеров с hello наибольшее количество файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="a0b89-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="a0b89-393">**События Kubernetes** -показана диаграмма Kubernetes события, создаваемые со временем и список hello причин, почему модулей созданных событий hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="a0b89-394">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="a0b89-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="a0b89-395">**Инвентаризацию пространств имен Kubernetes** — показывает количество hello пространств имен и модулей и показывает их иерархии.</span><span class="sxs-lookup"><span data-stu-id="a0b89-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="a0b89-396">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="a0b89-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="a0b89-397">**Инвентаризация узел контейнера** -показывает количество hello orchestration типы, используемые на узлы контейнера.</span><span class="sxs-lookup"><span data-stu-id="a0b89-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="a0b89-398">узлы и узлы, Hello компьютера также перечислены hello число контейнеров.</span><span class="sxs-lookup"><span data-stu-id="a0b89-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="a0b89-399">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="a0b89-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="a0b89-400">**Контейнер образов инвентаризации** -показывает общее количество контейнера изображений, используемых для hello и количество типов изображений.</span><span class="sxs-lookup"><span data-stu-id="a0b89-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="a0b89-401">Hello несколько образов, также перечислены hello тег изображения.</span><span class="sxs-lookup"><span data-stu-id="a0b89-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="a0b89-402">**Состояние контейнеры** -показывает общее количество hello контейнера узлов или узел компьютеров с запущенными контейнерами.</span><span class="sxs-lookup"><span data-stu-id="a0b89-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="a0b89-403">Hello число запущенных узлов также перечислены компьютеры.</span><span class="sxs-lookup"><span data-stu-id="a0b89-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="a0b89-404">**Процессу контейнера.** Здесь отображается график процессов контейнера, выполняемых за период времени.</span><span class="sxs-lookup"><span data-stu-id="a0b89-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="a0b89-405">Контейнеры также перечислены по выполняемым в них командам или процессам.</span><span class="sxs-lookup"><span data-stu-id="a0b89-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="a0b89-406">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="a0b89-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="a0b89-407">**Производительность ЦП контейнера** -показывает график hello средняя загрузка ЦП со временем для компьютера узлы.</span><span class="sxs-lookup"><span data-stu-id="a0b89-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="a0b89-408">Также перечислены hello компьютера узлы и узлы, основанные на средней загрузки ЦП.</span><span class="sxs-lookup"><span data-stu-id="a0b89-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="a0b89-409">**Производительности памяти контейнера.** Здесь отображается график использования памяти по времени,</span><span class="sxs-lookup"><span data-stu-id="a0b89-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="a0b89-410">а также использование памяти компьютера по имени экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a0b89-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="a0b89-411">**Производительность компьютера** -показывает процент использования памяти со временем и объем свободного места на диске графиках hello процентов производительности ЦП с течением времени, с течением времени.</span><span class="sxs-lookup"><span data-stu-id="a0b89-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="a0b89-412">Наводите указатель мыши на любую строку в tooview диаграммы Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="a0b89-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="a0b89-413">Каждая область hello мониторинга — это визуальное представление поиска, которое запускается на собранных данных.</span><span class="sxs-lookup"><span data-stu-id="a0b89-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Панель мониторинга "Контейнеры"](./media/log-analytics-containers/containers-dash01.png)

![Панель мониторинга "Контейнеры"](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="a0b89-416">В hello **состояние контейнера** области, щелкните hello верхней области, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a0b89-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Состояние контейнера](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="a0b89-418">Откроется поиска журналов сведения о состоянии hello вашей контейнеров.</span><span class="sxs-lookup"><span data-stu-id="a0b89-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Колонка "Поиск по журналам" для контейнеров](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="a0b89-420">Здесь можно изменить toomodify запрос поиска hello его конкретные сведения toofind hello вас интересует.</span><span class="sxs-lookup"><span data-stu-id="a0b89-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="a0b89-421">Дополнительные сведения об использовании поиска по журналам см. в статье [Поиск по журналам в Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="a0b89-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="a0b89-422">Устранение неполадок с помощью поиска контейнера со сбоем</span><span class="sxs-lookup"><span data-stu-id="a0b89-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="a0b89-423">Log Analytics добавляет к контейнеру пометку **Сбой**, если такой контейнер завершил работу с ненулевым кодом выхода.</span><span class="sxs-lookup"><span data-stu-id="a0b89-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="a0b89-424">Можно просмотреть обзор hello ошибок и сбоев в среде hello в hello **сбой контейнеры** области.</span><span class="sxs-lookup"><span data-stu-id="a0b89-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="a0b89-425">не удалось выполнить toofind контейнеров</span><span class="sxs-lookup"><span data-stu-id="a0b89-425">toofind failed containers</span></span>
1. <span data-ttu-id="a0b89-426">Нажмите кнопку hello **состояние контейнера** области.</span><span class="sxs-lookup"><span data-stu-id="a0b89-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="a0b89-427">![состояние контейнера](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="a0b89-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="a0b89-428">Поиск журналов открывает и отображает состояние hello вашей контейнеров, аналогичные toohello следующие.</span><span class="sxs-lookup"><span data-stu-id="a0b89-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![Состояние контейнеров](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="a0b89-430">После этого щелкните значение hello суммарный неудачных контейнеры tooview дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="a0b89-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="a0b89-431">Разверните **Показать больше** ИД tooview hello образа.</span><span class="sxs-lookup"><span data-stu-id="a0b89-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="a0b89-432">![Контейнеры со сбоями](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="a0b89-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="a0b89-433">Далее введите ниже hello в hello поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="a0b89-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="a0b89-434">`Type=ContainerInventory <ImageID>`toosee подробные сведения о hello изображения, например размер образа и число образов остановлена, которая завершилась неудачно.</span><span class="sxs-lookup"><span data-stu-id="a0b89-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="a0b89-435">![Контейнеры со сбоями](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="a0b89-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="a0b89-436">Поиск данных контейнера по журналам</span><span class="sxs-lookup"><span data-stu-id="a0b89-436">Search logs for container data</span></span>
<span data-ttu-id="a0b89-437">При устранении неполадок конкретную ошибку, он может помочь toosee, где происходит в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="a0b89-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="a0b89-438">следующие типы журналов Hello поможет вам создать запросы нужные сведения tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="a0b89-439">**ContainerImageInventory** — этот тип используется, если вы пытаетесь toofind данные, организованные изображения и tooview изображения такие сведения, идентификаторы изображения или размеров.</span><span class="sxs-lookup"><span data-stu-id="a0b89-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="a0b89-440">**ContainerInventory** — этот тип используется для получения сведений о расположении контейнеров, их именах и образах, которые в них выполняются.</span><span class="sxs-lookup"><span data-stu-id="a0b89-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="a0b89-441">**ContainerLog** — используйте этот тип, если нужно toofind конкретных сведений об ошибке журнала и записи.</span><span class="sxs-lookup"><span data-stu-id="a0b89-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="a0b89-442">**ContainerNodeInventory_CL** этот тип используется hello сведения о узла и где находятся контейнеры.</span><span class="sxs-lookup"><span data-stu-id="a0b89-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="a0b89-443">С его помощью можно получить сведения о версии Docker, типе оркестрации, хранилище и сведения о сети.</span><span class="sxs-lookup"><span data-stu-id="a0b89-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="a0b89-444">**ContainerProcess_CL** используйте этот тип tooquickly разделе hello процесс, запущенный в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="a0b89-445">**ContainerServiceLog** — этот тип используется, если вы пытаетесь toofind аудита сведения об аудите для hello управляющей программы Docker, такие как запуск, остановка, удалить или по запросу команды.</span><span class="sxs-lookup"><span data-stu-id="a0b89-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="a0b89-446">**KubeEvents_CL** использовать этот тип toosee hello Kubernetes события.</span><span class="sxs-lookup"><span data-stu-id="a0b89-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="a0b89-447">**KubePodInventory_CL** этот тип используется при необходимости сведения об иерархии toounderstand hello кластера.</span><span class="sxs-lookup"><span data-stu-id="a0b89-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="a0b89-448">toosearch журналы для контейнера данных</span><span class="sxs-lookup"><span data-stu-id="a0b89-448">toosearch logs for container data</span></span>
* <span data-ttu-id="a0b89-449">Выберите изображение, которое известно недавно произошел сбой и поиск журналов ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="a0b89-450">Сначала найдите имя контейнера, в котором выполняется этот образ, выполнив поиск в журнале **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="a0b89-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="a0b89-451">Например, выполните поиск по запросу `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="a0b89-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="a0b89-452">![Поиск контейнеров Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="a0b89-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="a0b89-453">Здравствуйте имя контейнера hello рядом слишком**имя**и выполните поиск эти журналы.</span><span class="sxs-lookup"><span data-stu-id="a0b89-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="a0b89-454">В нашем примере поисковый запрос будет выглядеть так: `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="a0b89-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="a0b89-455">**Просмотр сведений о производительности**</span><span class="sxs-lookup"><span data-stu-id="a0b89-455">**View performance information**</span></span>

<span data-ttu-id="a0b89-456">При начиная tooconstruct запросы, может помочь toosee возможности возможных сначала.</span><span class="sxs-lookup"><span data-stu-id="a0b89-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="a0b89-457">Например toosee поиск все данные производительности, попробуйте hello общих запросов, введя следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="a0b89-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![Производительность контейнеров](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="a0b89-459">Вы можете задать область hello данные о производительности, что вы видите tooa конкретному контейнеру, введя имя hello его toohello справа от запроса.</span><span class="sxs-lookup"><span data-stu-id="a0b89-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="a0b89-460">Отображается список hello метрики производительности, собранных для отдельных контейнера.</span><span class="sxs-lookup"><span data-stu-id="a0b89-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![Производительность контейнеров](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="a0b89-462">Примеры запросов для поиска по журналам</span><span class="sxs-lookup"><span data-stu-id="a0b89-462">Example log search queries</span></span>
<span data-ttu-id="a0b89-463">Часто полезно toobuild запрашивает начиная с примером или два, а затем изменить их toofit вашей среде.</span><span class="sxs-lookup"><span data-stu-id="a0b89-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="a0b89-464">В качестве отправной точки, можно поэкспериментировать с hello **примеры запросов** toohelp область построения более сложные запросы.</span><span class="sxs-lookup"><span data-stu-id="a0b89-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Запросы по контейнерам](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="a0b89-466">Сохранение запросов для поиска по журналам</span><span class="sxs-lookup"><span data-stu-id="a0b89-466">Saving log search queries</span></span>
<span data-ttu-id="a0b89-467">Сохранение запросов — это стандартная функция в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a0b89-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="a0b89-468">Она позволяет сохранять полезные запросы для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="a0b89-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="a0b89-469">После создания запроса, который вам пригодиться, сохраните его, выбрав **Избранное** hello верхней части страницы поиска журналов hello.</span><span class="sxs-lookup"><span data-stu-id="a0b89-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="a0b89-470">Затем можно легко получить его позже из hello **Моя панель мониторинга** страницы.</span><span class="sxs-lookup"><span data-stu-id="a0b89-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0b89-471">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0b89-471">Next steps</span></span>
* <span data-ttu-id="a0b89-472">[Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробные записи данных контейнера.</span><span class="sxs-lookup"><span data-stu-id="a0b89-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
