---
title: "aaaSimulate сбоев в Azure микрослужбами | Документы Microsoft"
description: "В этой статье рассказывается о hello действий тестирования в Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="e2596-103">Действия, доступные благодаря Testability</span><span class="sxs-lookup"><span data-stu-id="e2596-103">Testability actions</span></span>
<span data-ttu-id="e2596-104">В порядке toosimulate ненадежной инфраструктуру Azure Service Fabric предоставляет, способов toosimulate разработчику hello различных сбоев реальных и переходов между состояниями.</span><span class="sxs-lookup"><span data-stu-id="e2596-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="e2596-105">Такие действия доступны благодаря компоненту Testability.</span><span class="sxs-lookup"><span data-stu-id="e2596-105">These are exposed as testability actions.</span></span> <span data-ttu-id="e2596-106">Hello действия являются hello низкоуровневые интерфейсы API, которые привести внесения конкретных ошибок, переход состояния или проверки.</span><span class="sxs-lookup"><span data-stu-id="e2596-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="e2596-107">Сочетая эти действия, вы можете создать комплексные сценарии тестирования своих служб.</span><span class="sxs-lookup"><span data-stu-id="e2596-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="e2596-108">В платформе Service Fabric доступны несколько распространенных сценариев тестирования, которые состоят из этих действий.</span><span class="sxs-lookup"><span data-stu-id="e2596-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="e2596-109">Настоятельно рекомендуется использовать эти встроенные сценариев, которые выбираются тщательно tootest общие переходы между состояниями и случаи сбоев.</span><span class="sxs-lookup"><span data-stu-id="e2596-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="e2596-110">Тем не менее действия могут быть сценарии тестирования используется toocreate при необходимости tooadd покрытия для сценариев, не охваченных встроенной сценарии hello еще или, являются пользовательскими, адаптированные для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e2596-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="e2596-111">C# реализации hello действия находятся в hello System.Fabric.dll сборки.</span><span class="sxs-lookup"><span data-stu-id="e2596-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="e2596-112">модуль PowerShell System структуры Hello в hello Microsoft.ServiceFabric.Powershell.dll сборки найден.</span><span class="sxs-lookup"><span data-stu-id="e2596-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="e2596-113">В процессе установки среды выполнения hello модуля ServiceFabric PowerShell — установленных tooallow для удобства использования.</span><span class="sxs-lookup"><span data-stu-id="e2596-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="e2596-114">Нормальные и ненормальные ошибки</span><span class="sxs-lookup"><span data-stu-id="e2596-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="e2596-115">Действия, доступные благодаря Testability, делятся на две основных части.</span><span class="sxs-lookup"><span data-stu-id="e2596-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="e2596-116">Ненормальные ошибки. Эти сбои имитируют ошибки, такие как перезагрузки компьютеров и аварийное завершение процессов.</span><span class="sxs-lookup"><span data-stu-id="e2596-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="e2596-117">В таких случаях сбои hello контекста выполнения процесса неожиданно останавливается.</span><span class="sxs-lookup"><span data-stu-id="e2596-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="e2596-118">Это означает, что очистка hello состояния может выполняться перед запуском приложения hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="e2596-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="e2596-119">Нормальные ошибки. Эти сбои имитируют нормальные действия, такие как перемещение реплик и операции удаления, инициированные балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e2596-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="e2596-120">В таких случаях служба hello получает уведомление о hello закрыть и можно очистить состояние hello перед выходом.</span><span class="sxs-lookup"><span data-stu-id="e2596-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="e2596-121">Для повышения качества проверки, запустить службу hello и business рабочей нагрузки при инициирует различные корректное и нестандартного сбоев.</span><span class="sxs-lookup"><span data-stu-id="e2596-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="e2596-122">Нестандартного ошибки выполнение сценариев, где процесс службы hello неожиданно завершает работу в середине hello некоторых рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="e2596-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="e2596-123">Это тесты hello путь восстановления после восстановления hello реплики службы с помощью Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e2596-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="e2596-124">Это поможет проверить согласованность данных и ли правильной поддержки hello состояния службы после сбоев.</span><span class="sxs-lookup"><span data-stu-id="e2596-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="e2596-125">Hello сбоев (hello корректное сбоев) другой набор тестирования, hello службы правильно реагирует tooreplicas перемещаются Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e2596-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="e2596-126">Это проверяет обработка отмены в метод RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="e2596-127">Служба Hello должна toocheck hello отмены маркера, значение и правильно сохранять свое состояние выхода из метода RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="e2596-128">Список действий, доступных благодаря Testability</span><span class="sxs-lookup"><span data-stu-id="e2596-128">Testability actions list</span></span>
| <span data-ttu-id="e2596-129">Действие</span><span class="sxs-lookup"><span data-stu-id="e2596-129">Action</span></span> | <span data-ttu-id="e2596-130">Описание</span><span class="sxs-lookup"><span data-stu-id="e2596-130">Description</span></span> | <span data-ttu-id="e2596-131">Управляемый интерфейс API</span><span class="sxs-lookup"><span data-stu-id="e2596-131">Managed API</span></span> | <span data-ttu-id="e2596-132">Командлет PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2596-132">PowerShell cmdlet</span></span> | <span data-ttu-id="e2596-133">Нормальная или ненормальная ошибка</span><span class="sxs-lookup"><span data-stu-id="e2596-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e2596-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="e2596-134">CleanTestState</span></span> |<span data-ttu-id="e2596-135">Удаляет все состояния теста hello из кластера hello в случае неудачного завершения теста драйвера hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="e2596-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-136">CleanTestStateAsync</span></span> |<span data-ttu-id="e2596-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="e2596-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="e2596-138">Не применяется</span><span class="sxs-lookup"><span data-stu-id="e2596-138">Not applicable</span></span> |
| <span data-ttu-id="e2596-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="e2596-139">InvokeDataLoss</span></span> |<span data-ttu-id="e2596-140">Приводит к потере данных в разделе службы.</span><span class="sxs-lookup"><span data-stu-id="e2596-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="e2596-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="e2596-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="e2596-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="e2596-143">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-143">Graceful</span></span> |
| <span data-ttu-id="e2596-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="e2596-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="e2596-145">Приводит к потере кворума в указанном разделе службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="e2596-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="e2596-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="e2596-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="e2596-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="e2596-148">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-148">Graceful</span></span> |
| <span data-ttu-id="e2596-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="e2596-149">Move Primary</span></span> |<span data-ttu-id="e2596-150">Перемещает hello указан основной реплики службы с отслеживанием состояния toohello указанный узел кластера.</span><span class="sxs-lookup"><span data-stu-id="e2596-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="e2596-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-151">MovePrimaryAsync</span></span> |<span data-ttu-id="e2596-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="e2596-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="e2596-153">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-153">Graceful</span></span> |
| <span data-ttu-id="e2596-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="e2596-154">Move Secondary</span></span> |<span data-ttu-id="e2596-155">Перемещает hello текущей вторичной реплики службы с отслеживанием состояния tooa другом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="e2596-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="e2596-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="e2596-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="e2596-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="e2596-158">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-158">Graceful</span></span> |
| <span data-ttu-id="e2596-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="e2596-159">RemoveReplica</span></span> |<span data-ttu-id="e2596-160">Имитирует ошибку реплики путем удаления реплики из кластера.</span><span class="sxs-lookup"><span data-stu-id="e2596-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="e2596-161">Это будет закрыт реплики hello и будет выполнить переход toorole «None», удаление свое состояние из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="e2596-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="e2596-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="e2596-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="e2596-164">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-164">Graceful</span></span> |
| <span data-ttu-id="e2596-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="e2596-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="e2596-166">Имитирует ошибку процесса пакета кода путем перезапуска пакета кода, развернутого на узле в кластере.</span><span class="sxs-lookup"><span data-stu-id="e2596-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="e2596-167">Это отменяет пакет кода hello процесс, который будет перезапустить все реплики службы пользователя hello, размещенные в этом процессе.</span><span class="sxs-lookup"><span data-stu-id="e2596-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="e2596-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="e2596-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="e2596-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="e2596-170">Ненормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-170">Ungraceful</span></span> |
| <span data-ttu-id="e2596-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="e2596-171">RestartNode</span></span> |<span data-ttu-id="e2596-172">Имитирует ошибку узла кластера Service Fabric путем перезапуска узла.</span><span class="sxs-lookup"><span data-stu-id="e2596-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="e2596-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-173">RestartNodeAsync</span></span> |<span data-ttu-id="e2596-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e2596-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="e2596-175">Ненормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-175">Ungraceful</span></span> |
| <span data-ttu-id="e2596-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="e2596-176">RestartPartition</span></span> |<span data-ttu-id="e2596-177">Имитирует сценарий отключения центра обработки данных или кластера путем перезапуска некоторых или всех реплик раздела.</span><span class="sxs-lookup"><span data-stu-id="e2596-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="e2596-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-178">RestartPartitionAsync</span></span> |<span data-ttu-id="e2596-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="e2596-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="e2596-180">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-180">Graceful</span></span> |
| <span data-ttu-id="e2596-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="e2596-181">RestartReplica</span></span> |<span data-ttu-id="e2596-182">Имитирует сбой реплики путем перезапуска материализованный реплики в кластере, закрытие реплики hello и открыв его снова.</span><span class="sxs-lookup"><span data-stu-id="e2596-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="e2596-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-183">RestartReplicaAsync</span></span> |<span data-ttu-id="e2596-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="e2596-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="e2596-185">Нормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-185">Graceful</span></span> |
| <span data-ttu-id="e2596-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="e2596-186">StartNode</span></span> |<span data-ttu-id="e2596-187">Запускает узел в кластере, который уже остановлен.</span><span class="sxs-lookup"><span data-stu-id="e2596-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="e2596-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-188">StartNodeAsync</span></span> |<span data-ttu-id="e2596-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e2596-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="e2596-190">Не применяется</span><span class="sxs-lookup"><span data-stu-id="e2596-190">Not applicable</span></span> |
| <span data-ttu-id="e2596-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="e2596-191">StopNode</span></span> |<span data-ttu-id="e2596-192">Имитирует ошибку узла, останавливая его работу в кластере.</span><span class="sxs-lookup"><span data-stu-id="e2596-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="e2596-193">узел Hello остается вниз, пока не будет вызван StartNode.</span><span class="sxs-lookup"><span data-stu-id="e2596-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="e2596-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-194">StopNodeAsync</span></span> |<span data-ttu-id="e2596-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e2596-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="e2596-196">Ненормальная</span><span class="sxs-lookup"><span data-stu-id="e2596-196">Ungraceful</span></span> |
| <span data-ttu-id="e2596-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="e2596-197">ValidateApplication</span></span> |<span data-ttu-id="e2596-198">Проверяет доступность hello и работоспособность всех служб Service Fabric внутри приложения, обычно после включения некоторых ошибок сборки в систему hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="e2596-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="e2596-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="e2596-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="e2596-201">Не применяется</span><span class="sxs-lookup"><span data-stu-id="e2596-201">Not applicable</span></span> |
| <span data-ttu-id="e2596-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="e2596-202">ValidateService</span></span> |<span data-ttu-id="e2596-203">Проверяет доступность hello и работоспособность службы Service Fabric, обычно после включения некоторых ошибок сборки в систему hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="e2596-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="e2596-204">ValidateServiceAsync</span></span> |<span data-ttu-id="e2596-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="e2596-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="e2596-206">Не применяется</span><span class="sxs-lookup"><span data-stu-id="e2596-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="e2596-207">Выполнение действия тестирования с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2596-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="e2596-208">В этом учебнике показано как toorun действие тестирования с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2596-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="e2596-209">Вы узнаете, как toorun тестирования действие по отношению к локальному кластеру (одно поле) или кластере Azure.</span><span class="sxs-lookup"><span data-stu-id="e2596-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="e2596-210">Microsoft.Fabric.Powershell.dll--hello модуля Service Fabric PowerShell — устанавливается автоматически при установке MSI-файла структуры службы Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="e2596-211">модуль Hello загружается автоматически при открытии командной строке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2596-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="e2596-212">Разделы учебника</span><span class="sxs-lookup"><span data-stu-id="e2596-212">Tutorial segments:</span></span>

* [<span data-ttu-id="e2596-213">Выполнение действия для кластера с одним полем</span><span class="sxs-lookup"><span data-stu-id="e2596-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="e2596-214">Выполнение действия для кластера Azure</span><span class="sxs-lookup"><span data-stu-id="e2596-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="e2596-215">Выполнение действия для кластера с одним полем</span><span class="sxs-lookup"><span data-stu-id="e2596-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="e2596-216">toorun тестирования действие по отношению к локальному кластеру, сначала соединения toohello кластера Привет открыть командную строку PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="e2596-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="e2596-217">Рассмотрим hello **ServiceFabricNode перезапуска** действие.</span><span class="sxs-lookup"><span data-stu-id="e2596-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="e2596-218">Здесь hello действие **ServiceFabricNode перезапуска** выполняется на узел с именем «Node1».</span><span class="sxs-lookup"><span data-stu-id="e2596-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="e2596-219">режим завершения Hello указывает, что он не должен проверять, действительно ли успешным действие перезапуска узла hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="e2596-220">Указание режим завершения hello как «Проверить» приведет к его tooverify ли действие перезапуска hello фактически выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="e2596-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="e2596-221">Вместо прямого указания hello узла по его имени, можно указать его через тип ключа и hello секции реплики, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e2596-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="e2596-222">**Перезапуск ServiceFabricNode** должно быть используется toorestart Service Fabric узла в кластере.</span><span class="sxs-lookup"><span data-stu-id="e2596-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="e2596-223">Это остановит процесс Fabric.exe hello, который будет перезапустите все hello системы служб и пользователей службы реплики, размещенные на этом узле.</span><span class="sxs-lookup"><span data-stu-id="e2596-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="e2596-224">С помощью этого API tootest службы помогает обнаружить ошибки по путям восстановления hello отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e2596-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="e2596-225">Он позволяет имитировать сбоев узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="e2596-226">Hello следующем снимке экрана показано hello **ServiceFabricNode перезапуска** команда тестирования в действии.</span><span class="sxs-lookup"><span data-stu-id="e2596-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="e2596-227">Hello вывод hello сначала **Get ServiceFabricNode** (командлета из модуля Service Fabric PowerShell hello) показывает, что hello локальный кластер имеет пять узлов: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="e2596-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="e2596-228">После выполнения действия тестирования hello (командлет) **ServiceFabricNode перезапуска** выполняется на узле hello с именем Node.4, мы видим, время работы этого узла hello был сброшен.</span><span class="sxs-lookup"><span data-stu-id="e2596-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="e2596-229">Выполнение действия для кластера Azure</span><span class="sxs-lookup"><span data-stu-id="e2596-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="e2596-230">При выполнении действия тестирования (с помощью PowerShell) для кластера служб Azure — аналогичные действие hello toorunning по отношению к локальному кластеру.</span><span class="sxs-lookup"><span data-stu-id="e2596-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="e2596-231">Hello только различие состоит в том перед выполнением действия hello, вместо соединения локального кластера toohello необходимо tooconnect toohello Azure сначала кластера.</span><span class="sxs-lookup"><span data-stu-id="e2596-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="e2596-232">Выполнение действия, доступного благодаря Testability, с помощью C&#35;</span><span class="sxs-lookup"><span data-stu-id="e2596-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="e2596-233">toorun действие тестирования с помощью C#, сначала необходимо tooconnect toohello кластера с помощью FabricClient.</span><span class="sxs-lookup"><span data-stu-id="e2596-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="e2596-234">Затем получите toorun hello hello параметры, необходимые действия.</span><span class="sxs-lookup"><span data-stu-id="e2596-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="e2596-235">Можно использовать различные параметры toorun hello одним действием.</span><span class="sxs-lookup"><span data-stu-id="e2596-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="e2596-236">Просмотрев hello RestartServiceFabricNode действие, одним из способов toorun, возможно, это с помощью сведений об узле hello (имя узла и идентификатор экземпляра узла) в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="e2596-237">Описание параметров</span><span class="sxs-lookup"><span data-stu-id="e2596-237">Parameter explanation:</span></span>

* <span data-ttu-id="e2596-238">**CompleteMode** указывает, режим hello не должен проверять ли действие перезапуска hello фактически выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="e2596-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="e2596-239">Указание режим завершения hello как «Проверить» приведет к его tooverify ли действие перезапуска hello фактически выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="e2596-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="e2596-240">**OperationTimeout** наборов hello количество времени для операции toofinish hello, прежде чем создается исключение TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="e2596-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="e2596-241">**CancellationToken** позволяет toobe ожидающие вызов отменен.</span><span class="sxs-lookup"><span data-stu-id="e2596-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="e2596-242">Вместо прямого указания hello узла по его имени, можно указать его через тип ключа и hello секции реплики.</span><span class="sxs-lookup"><span data-stu-id="e2596-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="e2596-243">Дополнительные сведения: [PartitionSelector и ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="e2596-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="e2596-244">PartitionSelector и ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="e2596-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="e2596-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="e2596-245">PartitionSelector</span></span>
<span data-ttu-id="e2596-246">PartitionSelector — это помощник, представлены в возможности тестирования и является используется tooselect конкретной секции на какие tooperform действий тестирования hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="e2596-247">Если заранее известно, идентификатор секции hello может быть используется tooselect определенной секции.</span><span class="sxs-lookup"><span data-stu-id="e2596-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="e2596-248">Также можно ввести ключ секции hello и операции hello внутренне разрешит секции с Идентификатором hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="e2596-249">Также имеется возможность выбора случайного разбиения hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="e2596-250">toouse этого вспомогательного объекта создайте объект PartitionSelector hello и выберите раздел hello с помощью одного из методов hello Select *.</span><span class="sxs-lookup"><span data-stu-id="e2596-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="e2596-251">Затем передайте hello PartitionSelector объекта toohello API, которая в нем нуждается.</span><span class="sxs-lookup"><span data-stu-id="e2596-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="e2596-252">Если параметр не выбран, то по умолчанию tooa случайного разбиения.</span><span class="sxs-lookup"><span data-stu-id="e2596-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="e2596-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="e2596-253">ReplicaSelector</span></span>
<span data-ttu-id="e2596-254">ReplicaSelector — это помощник, представлены в возможности тестирования и является используется toohelp выберите реплику, на какие tooperform действий тестирования hello.</span><span class="sxs-lookup"><span data-stu-id="e2596-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="e2596-255">Если заранее известно, идентификатор hello реплики может быть используется tooselect конкретной реплики.</span><span class="sxs-lookup"><span data-stu-id="e2596-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="e2596-256">Кроме того предусмотрена возможность hello выбрать первичной реплики или случайное получателя.</span><span class="sxs-lookup"><span data-stu-id="e2596-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="e2596-257">ReplicaSelector является производным от PartitionSelector, поэтому требуется tooselect оба hello реплики и hello раздел, на котором вы хотите tooperform hello тестирования операции.</span><span class="sxs-lookup"><span data-stu-id="e2596-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="e2596-258">toouse этого вспомогательного объекта создайте объект ReplicaSelector и задайте нужным образом hello tooselect hello реплики и hello секции.</span><span class="sxs-lookup"><span data-stu-id="e2596-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="e2596-259">Можно затем передайте его в hello API, которая в нем нуждается.</span><span class="sxs-lookup"><span data-stu-id="e2596-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="e2596-260">Если параметр не выбран, то по умолчанию реплика случайных tooa и случайного разбиения.</span><span class="sxs-lookup"><span data-stu-id="e2596-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="e2596-261">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2596-261">Next steps</span></span>
* [<span data-ttu-id="e2596-262">Сценарии Testability</span><span class="sxs-lookup"><span data-stu-id="e2596-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="e2596-263">Как tootest службы</span><span class="sxs-lookup"><span data-stu-id="e2596-263">How tootest your service</span></span>
  * [<span data-ttu-id="e2596-264">Моделирование ошибок во время рабочих нагрузок службы</span><span class="sxs-lookup"><span data-stu-id="e2596-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="e2596-265">Ошибки обмена данными между службами</span><span class="sxs-lookup"><span data-stu-id="e2596-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

