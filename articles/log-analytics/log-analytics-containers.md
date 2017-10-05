---
title: "Решение для мониторинга контейнеров в Azure Log Analytics | Документация Майкрософт"
description: "Решение для мониторинга контейнеров в Log Analytics позволяет централизованно просматривать узлы контейнеров Docker и Windows, а также управлять ими."
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
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="b14e2-103">Решение для мониторинга контейнеров в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b14e2-103">Container Monitoring solution in Log Analytics</span></span>

![Символ решения "Контейнеры"](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="b14e2-105">В этой статье описано, как настроить и использовать решение для мониторинга контейнеров в Log Analytics, чтобы централизованно просматривать узлы контейнеров Docker и Windows, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="b14e2-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="b14e2-106">Docker — это система виртуализации программного обеспечения, с помощью которой можно создавать контейнеры, автоматизирующие развертывание программного обеспечения в соответствующей ИТ-инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="b14e2-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="b14e2-107">Решение показывает, какие контейнеры запущены, какой образ контейнера запущен и где выполняются контейнеры.</span><span class="sxs-lookup"><span data-stu-id="b14e2-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="b14e2-108">Также можно просматривать подробные сведения аудита, в том числе команды, используемые в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="b14e2-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="b14e2-109">Кроме того, вы можете устранять неполадки контейнеров, просматривая централизованные журналы и выполняя в них поиск, без необходимости удаленного просмотра узлов Docker или Windows.</span><span class="sxs-lookup"><span data-stu-id="b14e2-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="b14e2-110">Решение позволяет находить контейнеры, содержащие ошибки и использующие слишком много ресурсов на узле.</span><span class="sxs-lookup"><span data-stu-id="b14e2-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="b14e2-111">Также у вас есть возможность централизованно просматривать сведения об использовании и производительности ЦП, памяти, хранилища и сети по контейнерам.</span><span class="sxs-lookup"><span data-stu-id="b14e2-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="b14e2-112">На компьютерах под управлением Windows можно централизовать и сравнивать журналы из Windows Server, Hyper-V и контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="b14e2-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="b14e2-113">Решение поддерживает следующие оркестраторы контейнеров:</span><span class="sxs-lookup"><span data-stu-id="b14e2-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="b14e2-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b14e2-114">Docker Swarm</span></span>
- <span data-ttu-id="b14e2-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="b14e2-115">DC/OS</span></span>
- <span data-ttu-id="b14e2-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="b14e2-116">Kubernetes</span></span>
- <span data-ttu-id="b14e2-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b14e2-117">Service Fabric</span></span>
- <span data-ttu-id="b14e2-118">Red Hat OpenShift.</span><span class="sxs-lookup"><span data-stu-id="b14e2-118">Red Hat OpenShift</span></span>


<span data-ttu-id="b14e2-119">На схеме ниже показаны связи между разными узлами контейнера и агентами с OMS.</span><span class="sxs-lookup"><span data-stu-id="b14e2-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Схема контейнеров](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="b14e2-121">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="b14e2-121">System requirements</span></span>

<span data-ttu-id="b14e2-122">Сначала необходимо выполнить следующие требования.</span><span class="sxs-lookup"><span data-stu-id="b14e2-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="b14e2-123">Поддержка решений для мониторинга контейнеров: оркестратор Docker и платформа ОС</span><span class="sxs-lookup"><span data-stu-id="b14e2-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="b14e2-124">Ниже представлена таблица поддержки мониторинга операционных систем и оркестрации Docker с помощью Log Analytics. В частности, в таблице описана поддержка мониторинга списка контейнеров, производительности и журналов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="b14e2-125">ACS</span><span class="sxs-lookup"><span data-stu-id="b14e2-125">ACS</span></span> | <span data-ttu-id="b14e2-126">Linux</span><span class="sxs-lookup"><span data-stu-id="b14e2-126">Linux</span></span> | <span data-ttu-id="b14e2-127">Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-127">Windows</span></span> | <span data-ttu-id="b14e2-128">Контейнер</span><span class="sxs-lookup"><span data-stu-id="b14e2-128">Container</span></span><br><span data-ttu-id="b14e2-129">Список</span><span class="sxs-lookup"><span data-stu-id="b14e2-129">Inventory</span></span> | <span data-ttu-id="b14e2-130">Образ —</span><span class="sxs-lookup"><span data-stu-id="b14e2-130">Image</span></span><br><span data-ttu-id="b14e2-131">Список</span><span class="sxs-lookup"><span data-stu-id="b14e2-131">Inventory</span></span> | <span data-ttu-id="b14e2-132">Узел</span><span class="sxs-lookup"><span data-stu-id="b14e2-132">Node</span></span><br><span data-ttu-id="b14e2-133">Список</span><span class="sxs-lookup"><span data-stu-id="b14e2-133">Inventory</span></span> | <span data-ttu-id="b14e2-134">Контейнер</span><span class="sxs-lookup"><span data-stu-id="b14e2-134">Container</span></span><br><span data-ttu-id="b14e2-135">Производительность</span><span class="sxs-lookup"><span data-stu-id="b14e2-135">Performance</span></span> | <span data-ttu-id="b14e2-136">Контейнер</span><span class="sxs-lookup"><span data-stu-id="b14e2-136">Container</span></span><br><span data-ttu-id="b14e2-137">Событие</span><span class="sxs-lookup"><span data-stu-id="b14e2-137">Event</span></span> | <span data-ttu-id="b14e2-138">Событие</span><span class="sxs-lookup"><span data-stu-id="b14e2-138">Event</span></span><br><span data-ttu-id="b14e2-139">Журнал</span><span class="sxs-lookup"><span data-stu-id="b14e2-139">Log</span></span> | <span data-ttu-id="b14e2-140">Контейнер</span><span class="sxs-lookup"><span data-stu-id="b14e2-140">Container</span></span><br><span data-ttu-id="b14e2-141">Журнал</span><span class="sxs-lookup"><span data-stu-id="b14e2-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="b14e2-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="b14e2-142">Kubernetes</span></span> | <span data-ttu-id="b14e2-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-143">&#8226;</span></span> | <span data-ttu-id="b14e2-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-144">&#8226;</span></span> | | <span data-ttu-id="b14e2-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-145">&#8226;</span></span> | <span data-ttu-id="b14e2-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-146">&#8226;</span></span> | <span data-ttu-id="b14e2-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-147">&#8226;</span></span> | <span data-ttu-id="b14e2-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-148">&#8226;</span></span> | <span data-ttu-id="b14e2-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-149">&#8226;</span></span> | <span data-ttu-id="b14e2-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-150">&#8226;</span></span> | <span data-ttu-id="b14e2-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-151">&#8226;</span></span> |
| <span data-ttu-id="b14e2-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="b14e2-152">Mesosphere</span></span><br><span data-ttu-id="b14e2-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="b14e2-153">DC/OS</span></span> | <span data-ttu-id="b14e2-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-154">&#8226;</span></span> | <span data-ttu-id="b14e2-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-155">&#8226;</span></span> | | <span data-ttu-id="b14e2-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-156">&#8226;</span></span> | <span data-ttu-id="b14e2-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-157">&#8226;</span></span> | <span data-ttu-id="b14e2-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-158">&#8226;</span></span> | <span data-ttu-id="b14e2-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-159">&#8226;</span></span>| <span data-ttu-id="b14e2-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-160">&#8226;</span></span> | <span data-ttu-id="b14e2-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-161">&#8226;</span></span> | <span data-ttu-id="b14e2-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-162">&#8226;</span></span> |
| <span data-ttu-id="b14e2-163">Docker</span><span class="sxs-lookup"><span data-stu-id="b14e2-163">Docker</span></span><br><span data-ttu-id="b14e2-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="b14e2-164">Swarm</span></span> | <span data-ttu-id="b14e2-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-165">&#8226;</span></span> | <span data-ttu-id="b14e2-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-166">&#8226;</span></span> | <span data-ttu-id="b14e2-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-167">&#8226;</span></span> | <span data-ttu-id="b14e2-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-168">&#8226;</span></span> | <span data-ttu-id="b14e2-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-169">&#8226;</span></span> | <span data-ttu-id="b14e2-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-170">&#8226;</span></span> | <span data-ttu-id="b14e2-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-171">&#8226;</span></span> | <span data-ttu-id="b14e2-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-172">&#8226;</span></span> | | <span data-ttu-id="b14e2-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-173">&#8226;</span></span> |
| <span data-ttu-id="b14e2-174">служба</span><span class="sxs-lookup"><span data-stu-id="b14e2-174">Service</span></span><br><span data-ttu-id="b14e2-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="b14e2-175">Fabric</span></span> | | | <span data-ttu-id="b14e2-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-176">&#8226;</span></span> | <span data-ttu-id="b14e2-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-177">&#8226;</span></span> | <span data-ttu-id="b14e2-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-178">&#8226;</span></span> | <span data-ttu-id="b14e2-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-179">&#8226;</span></span> | <span data-ttu-id="b14e2-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-180">&#8226;</span></span> | <span data-ttu-id="b14e2-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-181">&#8226;</span></span> | <span data-ttu-id="b14e2-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-182">&#8226;</span></span> | <span data-ttu-id="b14e2-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-183">&#8226;</span></span> |
| <span data-ttu-id="b14e2-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="b14e2-184">Red Hat Open</span></span><br><span data-ttu-id="b14e2-185">Shift</span><span class="sxs-lookup"><span data-stu-id="b14e2-185">Shift</span></span> | | <span data-ttu-id="b14e2-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-186">&#8226;</span></span> | | <span data-ttu-id="b14e2-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-187">&#8226;</span></span> | <span data-ttu-id="b14e2-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-188">&#8226;</span></span>| <span data-ttu-id="b14e2-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-189">&#8226;</span></span> | <span data-ttu-id="b14e2-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-190">&#8226;</span></span> | <span data-ttu-id="b14e2-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-191">&#8226;</span></span> | | <span data-ttu-id="b14e2-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-192">&#8226;</span></span> |
| <span data-ttu-id="b14e2-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="b14e2-193">Windows Server</span></span><br><span data-ttu-id="b14e2-194">(изолированный)</span><span class="sxs-lookup"><span data-stu-id="b14e2-194">(standalone)</span></span> | | | <span data-ttu-id="b14e2-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-195">&#8226;</span></span> | <span data-ttu-id="b14e2-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-196">&#8226;</span></span> | <span data-ttu-id="b14e2-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-197">&#8226;</span></span> | <span data-ttu-id="b14e2-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-198">&#8226;</span></span> | <span data-ttu-id="b14e2-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-199">&#8226;</span></span> | <span data-ttu-id="b14e2-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-200">&#8226;</span></span> | | <span data-ttu-id="b14e2-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-201">&#8226;</span></span> |
| <span data-ttu-id="b14e2-202">Linux Server</span><span class="sxs-lookup"><span data-stu-id="b14e2-202">Linux Server</span></span><br><span data-ttu-id="b14e2-203">(изолированный)</span><span class="sxs-lookup"><span data-stu-id="b14e2-203">(standalone)</span></span> | | <span data-ttu-id="b14e2-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-204">&#8226;</span></span> | | <span data-ttu-id="b14e2-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-205">&#8226;</span></span> | <span data-ttu-id="b14e2-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-206">&#8226;</span></span> | <span data-ttu-id="b14e2-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-207">&#8226;</span></span> | <span data-ttu-id="b14e2-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-208">&#8226;</span></span> | <span data-ttu-id="b14e2-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-209">&#8226;</span></span> | | <span data-ttu-id="b14e2-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b14e2-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="b14e2-211">Версии Docker, поддерживаемые в Linux</span><span class="sxs-lookup"><span data-stu-id="b14e2-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="b14e2-212">Docker 1.11–1.13</span><span class="sxs-lookup"><span data-stu-id="b14e2-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="b14e2-213">Docker CE и EE v17.06</span><span class="sxs-lookup"><span data-stu-id="b14e2-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="b14e2-214">Дистрибутивы Linux x64, поддерживаемые в качестве узлов контейнера</span><span class="sxs-lookup"><span data-stu-id="b14e2-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="b14e2-215">Ubuntu 14.04 LTS и 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b14e2-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="b14e2-216">CoreOS (стабильный выпуск);</span><span class="sxs-lookup"><span data-stu-id="b14e2-216">CoreOS(stable)</span></span>
- <span data-ttu-id="b14e2-217">Amazon Linux 2016.09.0;</span><span class="sxs-lookup"><span data-stu-id="b14e2-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="b14e2-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="b14e2-218">openSUSE 13.2</span></span>
- <span data-ttu-id="b14e2-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="b14e2-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="b14e2-220">CentOS 7.2 и 7.3</span><span class="sxs-lookup"><span data-stu-id="b14e2-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="b14e2-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="b14e2-221">SLES 12</span></span>
- <span data-ttu-id="b14e2-222">RHEL 7.2 и 7.3</span><span class="sxs-lookup"><span data-stu-id="b14e2-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="b14e2-223">Платформа контейнеров Red Hat OpenShift (OCP) 3.4 и 3.5</span><span class="sxs-lookup"><span data-stu-id="b14e2-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="b14e2-224">ACS Mesosphere DC/OS 1.7.3–1.8.8</span><span class="sxs-lookup"><span data-stu-id="b14e2-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="b14e2-225">ACS Kubernetes 1.4.5–1.6</span><span class="sxs-lookup"><span data-stu-id="b14e2-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="b14e2-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b14e2-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="b14e2-227">Поддерживаемая операционная система Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-227">Supported Windows operating system</span></span>

- <span data-ttu-id="b14e2-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b14e2-228">Windows Server 2016</span></span>
- <span data-ttu-id="b14e2-229">Юбилейный выпуск Windows 10 (профессиональный или корпоративный)</span><span class="sxs-lookup"><span data-stu-id="b14e2-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="b14e2-230">Версии Docker, поддерживаемые в Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="b14e2-231">Docker 1.12 и 1.13</span><span class="sxs-lookup"><span data-stu-id="b14e2-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="b14e2-232">Docker 17.03.0 и более поздних версий</span><span class="sxs-lookup"><span data-stu-id="b14e2-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="b14e2-233">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="b14e2-233">Installing and configuring the solution</span></span>
<span data-ttu-id="b14e2-234">Для установки и настройки решений используйте указанные ниже данные.</span><span class="sxs-lookup"><span data-stu-id="b14e2-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="b14e2-235">Решение для мониторинга контейнеров необходимо добавить в рабочую область OMS из [Azure Мarketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) или в соответствии с инструкциями по [добавлению решений Log Analytics из коллекции решений](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="b14e2-236">Установите и используйте Docker с агентом OMS.</span><span class="sxs-lookup"><span data-stu-id="b14e2-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="b14e2-237">В зависимости от операционной системы можно выбрать один из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="b14e2-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="b14e2-238">В поддерживаемых операционных системах Linux установите и запустите Docker, а затем установите и настройте [агент OMS для Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="b14e2-239">В CoreOS невозможно запустить агент OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="b14e2-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="b14e2-240">Вместо этого можно запустить контейнерную версию агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="b14e2-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="b14e2-241">Если вы работаете с контейнерами в облаке "Azure для государственных организаций", то см. раздел [Для всех узлов контейнера Linux, включая CoreOS](#for-all-linux-container-hosts-including-coreos) или [Для всех узлов контейнера Linux Azure для государственных организаций, включая CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos).</span><span class="sxs-lookup"><span data-stu-id="b14e2-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="b14e2-242">В Windows Server 2016 и Windows 10 установите модуль и клиент Docker, после чего подключите агент, чтобы собрать сведения и отправить их в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b14e2-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="b14e2-243">Служба контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-243">Container services</span></span>

- <span data-ttu-id="b14e2-244">Если вы используете среду Red Hat OpenShift, то см. раздел [Настройка агента OMS для Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="b14e2-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="b14e2-245">При наличии кластера Kubernetes, использующего службу контейнеров Azure, см. статью [Мониторинг кластера Службы контейнеров Azure с помощью Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="b14e2-246">При наличии кластера DC/OS в службе контейнеров Azure дополнительные сведения см. в статье [Мониторинг кластера DC/OS в службе контейнеров Azure с помощью Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="b14e2-247">При наличии среды режима Docker Swarm ознакомьтесь с разделом [Настройка агента OMS для Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="b14e2-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="b14e2-248">При использовании контейнеров с Service Fabric см. статью [Общие сведения о Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="b14e2-249">Дополнительные сведения о том, как установить и настроить модули Docker на компьютерах под управлением Windows, см. в [этой статье](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="b14e2-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b14e2-250">Docker необходимо запустить **перед** установкой [агента OMS для Linux](log-analytics-agent-linux.md) на узлах контейнера.</span><span class="sxs-lookup"><span data-stu-id="b14e2-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="b14e2-251">Если вы уже установили агент перед установкой Docker, то необходимо переустановить агент OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="b14e2-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="b14e2-252">Дополнительные сведения о Docker см. на [веб-сайте Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="b14e2-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="b14e2-253">Узлы контейнера Linux</span><span class="sxs-lookup"><span data-stu-id="b14e2-253">Linux container hosts</span></span>

<span data-ttu-id="b14e2-254">После установки Docker используйте приведенные ниже параметры узла контейнера, чтобы настроить агент для использования с Docker.</span><span class="sxs-lookup"><span data-stu-id="b14e2-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="b14e2-255">Сначала необходимо получить идентификатор и ключ рабочей области OMS, которые можно найти на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b14e2-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="b14e2-256">В рабочей области щелкните **Быстрый запуск** > **Компьютеры**, чтобы просмотреть **идентификатор рабочей области** и **первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="b14e2-257">Скопируйте их и вставьте в любой удобный для вас редактор.</span><span class="sxs-lookup"><span data-stu-id="b14e2-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="b14e2-258">Для всех узлов контейнера Linux, за исключением CoreOS</span><span class="sxs-lookup"><span data-stu-id="b14e2-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="b14e2-259">Дополнительные сведения и инструкции по установке агента OMS для Linux см. в статье [Подключение компьютеров Linux к Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="b14e2-260">Для всех узлов контейнера Linux, включая CoreOS</span><span class="sxs-lookup"><span data-stu-id="b14e2-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="b14e2-261">Запустите контейнер OMS, который вы хотите отслеживать.</span><span class="sxs-lookup"><span data-stu-id="b14e2-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="b14e2-262">Используйте следующий пример, внеся в него необходимые изменения:</span><span class="sxs-lookup"><span data-stu-id="b14e2-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="b14e2-263">Для всех узлов контейнера Linux Azure для государственных организаций, включая CoreOS</span><span class="sxs-lookup"><span data-stu-id="b14e2-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="b14e2-264">Запустите контейнер OMS, который вы хотите отслеживать.</span><span class="sxs-lookup"><span data-stu-id="b14e2-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="b14e2-265">Используйте следующий пример, внеся в него необходимые изменения:</span><span class="sxs-lookup"><span data-stu-id="b14e2-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="b14e2-266">Переход от использования установленного агента Linux к использованию агента в контейнере</span><span class="sxs-lookup"><span data-stu-id="b14e2-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="b14e2-267">Если ранее вы использовали установленный напрямую агент и теперь вместо него хотите использовать агент, работающий в контейнере, сначала необходимо удалить агент OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="b14e2-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="b14e2-268">Сведения об удалении агента см. в разделе [Удаление агента OMS для Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="b14e2-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="b14e2-269">Настройка агента OMS для Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b14e2-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="b14e2-270">Агент OMS можно запускать в качестве глобальной службы в Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="b14e2-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="b14e2-271">Используйте приведенные ниже сведения для создания службы агента OMS.</span><span class="sxs-lookup"><span data-stu-id="b14e2-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="b14e2-272">Необходимо вставить свой идентификатор рабочей области OMS и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="b14e2-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="b14e2-273">Выполните следующую команду на главном узле.</span><span class="sxs-lookup"><span data-stu-id="b14e2-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="b14e2-274">Настройка агента OMS для Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="b14e2-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="b14e2-275">Существует три способа добавления агента OMS в Red Hat OpenShift, чтобы начать сбор данных мониторинга контейнера:</span><span class="sxs-lookup"><span data-stu-id="b14e2-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="b14e2-276">[установить агент OMS для Linux](log-analytics-agent-linux.md) непосредственно на каждом узле OpenShift;</span><span class="sxs-lookup"><span data-stu-id="b14e2-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="b14e2-277">[включить расширение виртуальной машины Log Analytics](log-analytics-azure-vm-extension.md) на каждом узле OpenShift, размещенном в Azure;</span><span class="sxs-lookup"><span data-stu-id="b14e2-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="b14e2-278">установить агент OMS как набор daemon-set для OpenShift.</span><span class="sxs-lookup"><span data-stu-id="b14e2-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="b14e2-279">В этом разделе описаны действия, которые необходимо выполнить для установки агента OMS как набора daemon-set для OpenShift.</span><span class="sxs-lookup"><span data-stu-id="b14e2-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="b14e2-280">Войдите на главный узел OpenShift и скопируйте YAML-файл [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) с портала GitHub на свой главный узел. При этом замените значения идентификатора рабочей области OMS и первичного ключа своими значениями.</span><span class="sxs-lookup"><span data-stu-id="b14e2-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="b14e2-281">Выполните следующие команды, чтобы создать проект для OMS и настроить учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="b14e2-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="b14e2-282">Чтобы развернуть набор daemon-set, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="b14e2-283">Чтобы проверить правильность его настроек и работоспособность, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="b14e2-284">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="b14e2-284">and the output should resemble:</span></span>

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

<span data-ttu-id="b14e2-285">Чтобы применить секреты для защиты идентификатора рабочей области OMS и первичного ключа, когда используется YAML-файл набора daemon-set агента OMS, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b14e2-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="b14e2-286">Войдите на главный узел OpenShift и скопируйте YAML-файл [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) и сценарий создания секретов [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) с портала GitHub.</span><span class="sxs-lookup"><span data-stu-id="b14e2-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="b14e2-287">Этот сценарий создаст YAML-файл секретов для идентификатора рабочей области OMS и первичного ключа, чтобы защитить ваши секретные сведения.</span><span class="sxs-lookup"><span data-stu-id="b14e2-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="b14e2-288">Выполните следующие команды, чтобы создать проект для OMS и настроить учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="b14e2-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="b14e2-289">Сценарий создания секретов запросит ввести идентификатор рабочей области OMS <WSID> и первичный ключ <KEY>, после чего создаст файл ocp-secret.yaml.</span><span class="sxs-lookup"><span data-stu-id="b14e2-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="b14e2-290">Разверните файл секретов, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="b14e2-291">Проверьте развертывание, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="b14e2-292">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="b14e2-292">and the  output should resemble:</span></span>  

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

6. <span data-ttu-id="b14e2-293">Разверните YAML-файл набора daemon-set агента OMS, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="b14e2-294">Проверьте развертывание, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="b14e2-295">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="b14e2-295">and the output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="b14e2-296">Защита секретных сведений для Docker Swarm и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b14e2-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="b14e2-297">Вы можете защитить секретный идентификатор рабочей области OMS и первичные ключи для служб контейнеров Docker Swarm и Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b14e2-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="b14e2-298">Защита секретов для Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b14e2-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="b14e2-299">Для Docker Swarm после создания секрета для идентификатора рабочей области и первичного ключа вы можете выполнять процесс создания службы Docker для агента OMS.</span><span class="sxs-lookup"><span data-stu-id="b14e2-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="b14e2-300">Используйте приведенные ниже сведения для создания секретных данных.</span><span class="sxs-lookup"><span data-stu-id="b14e2-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="b14e2-301">Выполните следующую команду на главном узле.</span><span class="sxs-lookup"><span data-stu-id="b14e2-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="b14e2-302">Убедитесь, что секретные данные созданы надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="b14e2-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="b14e2-303">Запустите следующую команду, чтобы подключить секреты к контейнерному агенту OMS.</span><span class="sxs-lookup"><span data-stu-id="b14e2-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="b14e2-304">Защита секретов для Kubernetes с помощью файлов YAML</span><span class="sxs-lookup"><span data-stu-id="b14e2-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="b14e2-305">Для Kubernetes используйте сценарий, чтобы создать YAML-файл секретов для идентификатора рабочей области и первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="b14e2-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="b14e2-306">На странице [OMS Docker Kubernetes в GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) есть файлы, которые можно использовать с секретными данными или без них:</span><span class="sxs-lookup"><span data-stu-id="b14e2-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="b14e2-307">стандартный файл DaemonSet агента OMS не поддерживает секретные сведения (omsagent.yaml);</span><span class="sxs-lookup"><span data-stu-id="b14e2-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="b14e2-308">YAML-файл DaemonSet агента OMS использует секретные сведения (omsagent-ds-secrets.yaml) со сценариями формирования секретов, чтобы создать YAML-файл секретов (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="b14e2-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="b14e2-309">Вы можете создать DaemonSet агента OMS с секретными данными или без них.</span><span class="sxs-lookup"><span data-stu-id="b14e2-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="b14e2-310">Стандартный файл YAML DaemonSet агента OMS без секретов</span><span class="sxs-lookup"><span data-stu-id="b14e2-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="b14e2-311">Для стандартного файла YAML DaemonSet агента OMS замените `<WSID>` и `<KEY>` на ваши WSID и ключ.</span><span class="sxs-lookup"><span data-stu-id="b14e2-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="b14e2-312">Скопируйте файл на главный узел и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="b14e2-313">Стандартный файл YAML DaemonSet агента OMS с секретами</span><span class="sxs-lookup"><span data-stu-id="b14e2-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="b14e2-314">Чтобы использовать DaemonSet агента OMS с секретными сведениями, сначала создайте секреты.</span><span class="sxs-lookup"><span data-stu-id="b14e2-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="b14e2-315">Скопируйте сценарий и файл шаблона секретов в один и тот же каталог.</span><span class="sxs-lookup"><span data-stu-id="b14e2-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="b14e2-316">Сценарий создания секретов — secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="b14e2-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="b14e2-317">Шаблон секретов — secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="b14e2-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="b14e2-318">Выполните сценарий, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b14e2-318">Run the script, like the following example.</span></span> <span data-ttu-id="b14e2-319">Сценарий запрашивает идентификатор рабочей области OMS и первичный ключ, а после их ввода создает YAML-файл секретов, который можно запустить.</span><span class="sxs-lookup"><span data-stu-id="b14e2-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="b14e2-320">Создайте pod секретов, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="b14e2-321">Чтобы проверить, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b14e2-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="b14e2-322">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="b14e2-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="b14e2-323">Выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="b14e2-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="b14e2-324">Создание свой набор daemon-set omsagent, выполнив команду ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="b14e2-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="b14e2-325">Убедитесь, что DaemonSet агента OMS запущен, что будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="b14e2-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="b14e2-326">Для Kubernetes используйте сценарий для создания файла YAML секретов для идентификатора рабочей области и первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="b14e2-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="b14e2-327">Используйте сведения из следующего примера с [файлом YAML omsagent](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml), чтобы защитить свои секретные сведения.</span><span class="sxs-lookup"><span data-stu-id="b14e2-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="b14e2-328">Узлы контейнеров Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="b14e2-329">Подготовка к установке агентов Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="b14e2-330">Настройте службу Docker, прежде чем устанавливать агенты на компьютерах под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="b14e2-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="b14e2-331">Конфигурация позволяет агенту Windows или расширению виртуальной машины Log Analytics использовать TCP-сокет Docker, чтобы агенты могли получить удаленный доступ к управляющей программе Docker и возможность получать данные мониторинга.</span><span class="sxs-lookup"><span data-stu-id="b14e2-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="b14e2-332">Запуск Docker и проверка его конфигурации</span><span class="sxs-lookup"><span data-stu-id="b14e2-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="b14e2-333">Для настройки именованного канала TCP для Windows Server выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b14e2-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="b14e2-334">Включите канал TCP и именованный канал в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b14e2-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="b14e2-335">Настройте Docker с помощью файла конфигурации для канала TCP и именованного канала.</span><span class="sxs-lookup"><span data-stu-id="b14e2-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="b14e2-336">Файл конфигурации расположен в папке C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="b14e2-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="b14e2-337">В файле daemon.json потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="b14e2-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="b14e2-338">Дополнительные сведения о настройке управляющей программы Docker, используемой в контейнерах Windows, см. в статье [Подсистема Docker в Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="b14e2-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="b14e2-339">Установка агентов Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-339">Install Windows agents</span></span>

<span data-ttu-id="b14e2-340">Чтобы включить мониторинг контейнеров Windows и Hyper-V, установите Microsoft Monitoring Agent (MMA) на компьютерах Windows, которые являются узлами контейнера.</span><span class="sxs-lookup"><span data-stu-id="b14e2-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="b14e2-341">Сведения для компьютеров под управлением Windows в локальной среде см. в статье [Подключение компьютеров Windows к Log Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="b14e2-342">Виртуальные машины, запущенные в Azure, следует подключить к Log Analytics с помощью [расширения виртуальной машины](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="b14e2-343">Вы можете отслеживать контейнеры Windows, запущенные в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b14e2-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="b14e2-344">Однако сейчас для Service Fabric поддерживаются только [виртуальные машины, работающие в Azure](log-analytics-azure-vm-extension.md), и [компьютеры под управлением Windows в локальной среде](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="b14e2-345">Убедитесь, что решение для мониторинга контейнеров правильно установлено в Windows.</span><span class="sxs-lookup"><span data-stu-id="b14e2-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="b14e2-346">Чтобы проверить, был ли пакет управления скачан должным образом, найдите файл *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="b14e2-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="b14e2-347">Файлы должны находиться в папке, расположенной по адресу C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="b14e2-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="b14e2-348">Компоненты решения</span><span class="sxs-lookup"><span data-stu-id="b14e2-348">Solution components</span></span>

<span data-ttu-id="b14e2-349">Если вы используете агенты Windows, то при добавлении этого решения на каждом компьютере с агентом устанавливается следующий пакет управления.</span><span class="sxs-lookup"><span data-stu-id="b14e2-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="b14e2-350">Для этих пакетов управления не требуются настройка или обслуживание.</span><span class="sxs-lookup"><span data-stu-id="b14e2-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="b14e2-351">*ContainerManagement.xxx* устанавливается в папке, расположенной по адресу C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="b14e2-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="b14e2-352">Сведения о сборе данных из контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-352">Container data collection details</span></span>
<span data-ttu-id="b14e2-353">Решение для мониторинга контейнеров собирает различные метрики производительности и данные журналов из узлов контейнеров и контейнеров, в которых включен агент.</span><span class="sxs-lookup"><span data-stu-id="b14e2-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="b14e2-354">Данные собираются каждые три минуты следующими типами агентов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="b14e2-355">Агент OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="b14e2-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="b14e2-356">Агент Windows</span><span class="sxs-lookup"><span data-stu-id="b14e2-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="b14e2-357">Расширение виртуальной машины Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b14e2-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="b14e2-358">Записи контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-358">Container records</span></span>

<span data-ttu-id="b14e2-359">В таблице ниже приведены примеры записей, собранных решением для мониторинга контейнеров, и типов данных, которые отображаются при поиске по журналам и в результатах.</span><span class="sxs-lookup"><span data-stu-id="b14e2-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="b14e2-360">Тип данных</span><span class="sxs-lookup"><span data-stu-id="b14e2-360">Data type</span></span> | <span data-ttu-id="b14e2-361">Тип данных, используемый для поиска в журналах</span><span class="sxs-lookup"><span data-stu-id="b14e2-361">Data type in Log Search</span></span> | <span data-ttu-id="b14e2-362">Поля</span><span class="sxs-lookup"><span data-stu-id="b14e2-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b14e2-363">Производительность узлов и контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="b14e2-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b14e2-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="b14e2-365">Список контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="b14e2-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="b14e2-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="b14e2-367">Список образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="b14e2-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="b14e2-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="b14e2-369">Журнал контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="b14e2-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="b14e2-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="b14e2-371">Журнал службы контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="b14e2-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="b14e2-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="b14e2-373">Список узлов контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="b14e2-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b14e2-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="b14e2-375">Список Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b14e2-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="b14e2-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b14e2-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="b14e2-377">Процесс контейнера</span><span class="sxs-lookup"><span data-stu-id="b14e2-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="b14e2-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b14e2-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="b14e2-379">События Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b14e2-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="b14e2-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="b14e2-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="b14e2-381">Метки, добавленные в типы данных *PodLabel* — это ваши метки.</span><span class="sxs-lookup"><span data-stu-id="b14e2-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="b14e2-382">Например, приведенные в таблице метки PodLabel.</span><span class="sxs-lookup"><span data-stu-id="b14e2-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="b14e2-383">Таким образом, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` будут отличаться в наборе данных вашей среды и должны выглядеть примерно так: `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="b14e2-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="b14e2-384">Мониторинг контейнеров</span><span class="sxs-lookup"><span data-stu-id="b14e2-384">Monitor containers</span></span>
<span data-ttu-id="b14e2-385">Включив решение на портале OMS, вы увидите плитку **Контейнеры**, на которой отображаются сводные сведения об узлах контейнеров и контейнерах, запущенных на узлах.</span><span class="sxs-lookup"><span data-stu-id="b14e2-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![Плитка "Контейнеры"](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="b14e2-387">Плитка показывает число контейнеров в среде, число запущенных и остановленных контейнеров, а также число контейнеров, работа которых завершилась сбоем.</span><span class="sxs-lookup"><span data-stu-id="b14e2-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="b14e2-388">Использование панели мониторинга "Контейнеры"</span><span class="sxs-lookup"><span data-stu-id="b14e2-388">Using the Containers dashboard</span></span>
<span data-ttu-id="b14e2-389">Щелкните плитку **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-389">Click the **Containers** tile.</span></span> <span data-ttu-id="b14e2-390">Отсюда можно открыть представления, упорядоченные по:</span><span class="sxs-lookup"><span data-stu-id="b14e2-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="b14e2-391">**Событиям контейнера.** Здесь отображается состояние контейнера и компьютеры, содержащие контейнеры со сбоями.</span><span class="sxs-lookup"><span data-stu-id="b14e2-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="b14e2-392">**Журналам контейнера.** Здесь отображается диаграмма файлов журналов контейнеров, созданных за определенный период, и список компьютеров с наибольшим количеством файлов журналов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="b14e2-393">**Событиям Kubernetes.** Здесь отображается диаграмма событий Kubernetes, созданных за определенный период, и список причин, по которым модули pod создали события.</span><span class="sxs-lookup"><span data-stu-id="b14e2-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="b14e2-394">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="b14e2-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b14e2-395">**Списку пространств имен Kubernetes.** Здесь отображается количество пространств имен и модулей pod, а также их иерархия.</span><span class="sxs-lookup"><span data-stu-id="b14e2-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="b14e2-396">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="b14e2-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b14e2-397">**Списку узлов контейнеров.** Здесь отображается количество типов оркестрации, которые используются на узлах контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b14e2-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="b14e2-398">Узлы компьютеров также перечислены по количеству контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b14e2-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="b14e2-399">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="b14e2-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b14e2-400">**Списку образов контейнеров.** Здесь отображается общее количество используемых образов контейнеров и количество типов образов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="b14e2-401">Количество образов также указано по тегам образов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="b14e2-402">**Состоянию контейнеров.** Здесь отображается общее количество компьютеров узлов контейнера с запущенными контейнерами.</span><span class="sxs-lookup"><span data-stu-id="b14e2-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="b14e2-403">Компьютеры также перечислены по количеству запущенных узлов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="b14e2-404">**Процессу контейнера.** Здесь отображается график процессов контейнера, выполняемых за период времени.</span><span class="sxs-lookup"><span data-stu-id="b14e2-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="b14e2-405">Контейнеры также перечислены по выполняемым в них командам или процессам.</span><span class="sxs-lookup"><span data-stu-id="b14e2-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="b14e2-406">*Этот набор данных используется только в средах Linux.*</span><span class="sxs-lookup"><span data-stu-id="b14e2-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b14e2-407">**Производительности ЦП контейнера.** Здесь отображается график среднего использования ЦП по времени для узлов компьютеров.</span><span class="sxs-lookup"><span data-stu-id="b14e2-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="b14e2-408">В нем также перечисляются узлы компьютеров по среднему использованию ЦП.</span><span class="sxs-lookup"><span data-stu-id="b14e2-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="b14e2-409">**Производительности памяти контейнера.** Здесь отображается график использования памяти по времени,</span><span class="sxs-lookup"><span data-stu-id="b14e2-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="b14e2-410">а также использование памяти компьютера по имени экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b14e2-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="b14e2-411">**Производительности компьютера.** Здесь отображаются графики с процентами производительности ЦП, использования памяти и свободным дисковым пространством в мегабайтах по времени.</span><span class="sxs-lookup"><span data-stu-id="b14e2-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="b14e2-412">Наведите указатель на любую линию в диаграмме, чтобы просмотреть дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="b14e2-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="b14e2-413">Каждая область на панели мониторинга — это визуальное представление поиска по собранным данным.</span><span class="sxs-lookup"><span data-stu-id="b14e2-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Панель мониторинга "Контейнеры"](./media/log-analytics-containers/containers-dash01.png)

![Панель мониторинга "Контейнеры"](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="b14e2-416">Перейдите в область **Container Status** (Состояния контейнера) и щелкните верхнюю область, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b14e2-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![Состояние контейнера](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="b14e2-418">Откроется колонка Log Search (Поиск по журналам) со сведениями о состоянии контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b14e2-418">Log Search opens, displaying information about the state of your containers.</span></span>

![Колонка "Поиск по журналам" для контейнеров](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="b14e2-420">Здесь можно изменить поисковый запрос таким образом, чтобы найти нужную вам информацию.</span><span class="sxs-lookup"><span data-stu-id="b14e2-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="b14e2-421">Дополнительные сведения об использовании поиска по журналам см. в статье [Поиск по журналам в Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="b14e2-422">Устранение неполадок с помощью поиска контейнера со сбоем</span><span class="sxs-lookup"><span data-stu-id="b14e2-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="b14e2-423">Log Analytics добавляет к контейнеру пометку **Сбой**, если такой контейнер завершил работу с ненулевым кодом выхода.</span><span class="sxs-lookup"><span data-stu-id="b14e2-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="b14e2-424">Обзор ошибок и сбоев в среде можно просмотреть в области **Failed Containers** (Контейнеры со сбоями).</span><span class="sxs-lookup"><span data-stu-id="b14e2-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="b14e2-425">Поиск контейнеров со сбоями</span><span class="sxs-lookup"><span data-stu-id="b14e2-425">To find failed containers</span></span>
1. <span data-ttu-id="b14e2-426">Щелкните область **Container Status** (Состояние контейнера).</span><span class="sxs-lookup"><span data-stu-id="b14e2-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="b14e2-427">![состояние контейнера](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="b14e2-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="b14e2-428">Откроется колонка Log Search (Поиск по журналам), в которой отобразится состояние контейнеров, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b14e2-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![Состояние контейнеров](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="b14e2-430">Выберите агрегированное значение контейнеров со сбоями, чтобы просмотреть дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="b14e2-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="b14e2-431">Разверните пункт **Показать больше**, чтобы просмотреть идентификатор образа.</span><span class="sxs-lookup"><span data-stu-id="b14e2-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="b14e2-432">![Контейнеры со сбоями](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="b14e2-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="b14e2-433">Введите в поисковый запрос следующий код.</span><span class="sxs-lookup"><span data-stu-id="b14e2-433">Next, type the following in the search query.</span></span> <span data-ttu-id="b14e2-434">`Type=ContainerInventory <ImageID>` для просмотра сведений об образе, таких как размер образа, количество остановленных образов, а также образы со сбоями.</span><span class="sxs-lookup"><span data-stu-id="b14e2-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="b14e2-435">![Контейнеры со сбоями](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="b14e2-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="b14e2-436">Поиск данных контейнера по журналам</span><span class="sxs-lookup"><span data-stu-id="b14e2-436">Search logs for container data</span></span>
<span data-ttu-id="b14e2-437">При устранении определенной ошибки эта функция помогает узнать, где именно в среде возникает эта ошибка.</span><span class="sxs-lookup"><span data-stu-id="b14e2-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="b14e2-438">С помощью журналов следующих типов можно создавать запросы для получения нужных вам сведений.</span><span class="sxs-lookup"><span data-stu-id="b14e2-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="b14e2-439">**ContainerImageInventory** — этот тип используется для поиска сведений, упорядоченных по образам, и для просмотра информации об образах, включая идентификаторы или размеры образов.</span><span class="sxs-lookup"><span data-stu-id="b14e2-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="b14e2-440">**ContainerInventory** — этот тип используется для получения сведений о расположении контейнеров, их именах и образах, которые в них выполняются.</span><span class="sxs-lookup"><span data-stu-id="b14e2-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="b14e2-441">**ContainerLog** — этот тип используется, если требуется найти определенные сведения или записи в журнале ошибок.</span><span class="sxs-lookup"><span data-stu-id="b14e2-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="b14e2-442">**ContainerNodeInventory_CL** — этот тип используется для получения сведений об узле, где находятся контейнеры.</span><span class="sxs-lookup"><span data-stu-id="b14e2-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="b14e2-443">С его помощью можно получить сведения о версии Docker, типе оркестрации, хранилище и сведения о сети.</span><span class="sxs-lookup"><span data-stu-id="b14e2-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="b14e2-444">**ContainerProcess_CL** — этот тип используется для быстрого просмотра процессов, запущенных в контейнере.</span><span class="sxs-lookup"><span data-stu-id="b14e2-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="b14e2-445">**ContainerServiceLog** — этот тип используется для поиска в журнале аудита данных об управляющей программе Docker, включая команды для запуска, остановки и извлечения.</span><span class="sxs-lookup"><span data-stu-id="b14e2-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="b14e2-446">**KubeEvents_CL** — этот тип используется для просмотра событий Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b14e2-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="b14e2-447">**KubePodInventory_CL** — этот тип используется, если необходимо получить сведения об иерархии кластера.</span><span class="sxs-lookup"><span data-stu-id="b14e2-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="b14e2-448">Поиск данных контейнера по журналам</span><span class="sxs-lookup"><span data-stu-id="b14e2-448">To search logs for container data</span></span>
* <span data-ttu-id="b14e2-449">Выберите образ, в котором недавно произошел сбой, и найдите журнал ошибок для этого образа.</span><span class="sxs-lookup"><span data-stu-id="b14e2-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="b14e2-450">Сначала найдите имя контейнера, в котором выполняется этот образ, выполнив поиск в журнале **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="b14e2-451">Например, выполните поиск по запросу `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="b14e2-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="b14e2-452">![Поиск контейнеров Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="b14e2-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="b14e2-453">Запишите имя контейнера в строке **Имя** и выполните поиск по журналам.</span><span class="sxs-lookup"><span data-stu-id="b14e2-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="b14e2-454">В нашем примере поисковый запрос будет выглядеть так: `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="b14e2-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="b14e2-455">**Просмотр сведений о производительности**</span><span class="sxs-lookup"><span data-stu-id="b14e2-455">**View performance information**</span></span>

<span data-ttu-id="b14e2-456">Начиная создавать запрос, прежде всего следует узнать, какие данные можно найти с его помощью.</span><span class="sxs-lookup"><span data-stu-id="b14e2-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="b14e2-457">Например, чтобы просмотреть все данные о производительности, попробуйте использовать общий запрос следующего вида:</span><span class="sxs-lookup"><span data-stu-id="b14e2-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![Производительность контейнеров](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="b14e2-459">Чтобы отобразить данные производительности только для конкретного контейнера, введите его имя в правой части запроса.</span><span class="sxs-lookup"><span data-stu-id="b14e2-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="b14e2-460">Вы увидите список метрик производительности, собранных для отдельного контейнера.</span><span class="sxs-lookup"><span data-stu-id="b14e2-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![Производительность контейнеров](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="b14e2-462">Примеры запросов для поиска по журналам</span><span class="sxs-lookup"><span data-stu-id="b14e2-462">Example log search queries</span></span>
<span data-ttu-id="b14e2-463">При создании запросов часто бывает полезно начать с одного-двух примеров, внося затем в них изменения в соответствии с конкретной средой.</span><span class="sxs-lookup"><span data-stu-id="b14e2-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="b14e2-464">Сначала можно поэкспериментировать с областью **Sample Queries** (Примеры запросов), чтобы научиться создавать более сложные запросы.</span><span class="sxs-lookup"><span data-stu-id="b14e2-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Запросы по контейнерам](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="b14e2-466">Сохранение запросов для поиска по журналам</span><span class="sxs-lookup"><span data-stu-id="b14e2-466">Saving log search queries</span></span>
<span data-ttu-id="b14e2-467">Сохранение запросов — это стандартная функция в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b14e2-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="b14e2-468">Она позволяет сохранять полезные запросы для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="b14e2-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="b14e2-469">Создав запрос, который вы считаете полезным, сохраните его, щелкнув **Избранное** в верхней части страницы поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="b14e2-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="b14e2-470">Позднее вы сможете легко открыть его на странице **Моя панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b14e2-471">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b14e2-471">Next steps</span></span>
* <span data-ttu-id="b14e2-472">[Выполните поиск по журналам](log-analytics-log-searches.md), чтобы просмотреть подробные записи с данными контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b14e2-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
