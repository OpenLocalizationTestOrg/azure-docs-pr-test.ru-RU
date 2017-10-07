---
title: "планы toorecovery модулей Runbook службы автоматизации Azure aaaAdd классическом портале hello | Документы Microsoft"
description: "В этой статье описывается, как Azure Site Recovery теперь позволяет с помощью службы автоматизации Azure toocomplete сложных задач во время восстановления tooAzure планы восстановления tooextend"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="f26ec-103">Добавить схемы toorecovery модулей Runbook службы автоматизации Azure hello классическом портале</span><span class="sxs-lookup"><span data-stu-id="f26ec-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="f26ec-104">Этот учебник описывает, как интегрируется Azure Site Recovery с планами toorecovery расширяемости tooprovide автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="f26ec-105">Планы восстановления может управлять восстановления виртуальных машин, защищенных с помощью Azure Site Recovery для облака toosecondary репликации и tooAzure сценарии репликации.</span><span class="sxs-lookup"><span data-stu-id="f26ec-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="f26ec-106">Они также помогут при выполнении восстановления hello **точных**, **repeatable**, и **автоматических**.</span><span class="sxs-lookup"><span data-stu-id="f26ec-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="f26ec-107">Если выполняется переход к tooAzure виртуальных машин, интеграция в службе автоматизации Azure расширяет планов восстановления и дает возможность tooexecute Runbook, позволяя тем самым мощным автоматизации задач.</span><span class="sxs-lookup"><span data-stu-id="f26ec-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="f26ec-108">Если вы еще не знакомы со службой автоматизации Azure, зарегистрируйтесь [здесь](https://azure.microsoft.com/services/automation/) и скачайте примеры сценариев [здесь](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="f26ec-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="f26ec-109">Дополнительные сведения о [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) и как планы восстановления tooAzure tooorchestrate, с помощью восстановления [здесь](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="f26ec-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="f26ec-110">В этом кратком руководстве мы рассмотрим то, как можно интегрировать модули Runbook службы автоматизации Azure в планы восстановления.</span><span class="sxs-lookup"><span data-stu-id="f26ec-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="f26ec-111">Мы автоматизации простых задач, которые более ранних версий требуется ручное вмешательство и разделе как tooconvert нескольких шаг восстановления в действие восстановления одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="f26ec-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="f26ec-112">Также мы рассмотрим порядок устранения ошибок, возникающих при выполнении простого сценария.</span><span class="sxs-lookup"><span data-stu-id="f26ec-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="f26ec-113">Защита tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="f26ec-114">Начнем с простого приложения HRweb компании Fabrikam,</span><span class="sxs-lookup"><span data-stu-id="f26ec-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="f26ec-115">состоящего из двух виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="f26ec-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="f26ec-116">Fabrikam HRweb переднего плана и Fabrikam Hrweb серверной части являются hello две виртуальные машины, защищенные с помощью Azure Site Recovery tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="f26ec-117">tooprotect hello виртуальных машин с помощью Azure Site Recovery, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="f26ec-118">Включите защиту для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f26ec-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="f26ec-119">Убедитесь, что виртуальные машины hello завершена начальная репликация и выполняется репликация.</span><span class="sxs-lookup"><span data-stu-id="f26ec-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="f26ec-120">Дождитесь завершения начальной репликации hello и Protected говорит hello состояние репликации.</span><span class="sxs-lookup"><span data-stu-id="f26ec-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="f26ec-121">В этом учебнике мы создадим для hello Fabrikam HRweb приложения toofailover hello приложения tooAzure плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="f26ec-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="f26ec-122">Затем мы будет интегрировать с runbook, который создаст конечную точку на hello отработку отказа виртуальной машины Azure tooserve веб-страниц на порт 80.</span><span class="sxs-lookup"><span data-stu-id="f26ec-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="f26ec-123">Сначала создадим план восстановления для приложения.</span><span class="sxs-lookup"><span data-stu-id="f26ec-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="f26ec-124">Создание плана восстановления hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-124">Create hello recovery plan</span></span>
<span data-ttu-id="f26ec-125">tooAzure приложения hello toorecover, необходимо toocreate план восстановления.</span><span class="sxs-lookup"><span data-stu-id="f26ec-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="f26ec-126">С помощью плана восстановления, которые можно задать порядок hello восстановления виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f26ec-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="f26ec-127">Hello виртуальной машине размещена в группе 1 будет восстановить и запустите первый, и следуйте hello виртуальной машины в группе 2.</span><span class="sxs-lookup"><span data-stu-id="f26ec-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="f26ec-128">Создайте план восстановления, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f26ec-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="f26ec-129">Дополнительные сведения о планах восстановления, ознакомьтесь с документацией tooread [здесь](https://msdn.microsoft.com/library/azure/dn788799.aspx "здесь").</span><span class="sxs-lookup"><span data-stu-id="f26ec-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="f26ec-130">Теперь давайте создадим hello необходимые артефакты в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="f26ec-131">Создать учетную запись автоматизации hello и ресурсы</span><span class="sxs-lookup"><span data-stu-id="f26ec-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="f26ec-132">Необходимо Runbook toocreate учетной записи автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="f26ec-133">Если у вас еще нет учетной записи, перейдите обозначается вкладка автоматизации tooAzure ![](media/site-recovery-runbook-automation/02.png)и создать новую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f26ec-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="f26ec-134">Предоставьте учетной записи hello tooidentify имя с.</span><span class="sxs-lookup"><span data-stu-id="f26ec-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="f26ec-135">Укажите географический регион, где требуется учетная запись tooplace hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="f26ec-136">Рекомендуется использовать учетную запись hello tooplace в hello же регионе, что хранилище hello ASR.</span><span class="sxs-lookup"><span data-stu-id="f26ec-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="f26ec-137">Создайте следующие ресурсы в учетной записи hello hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="f26ec-138">Добавление названия подписки в качестве ресурса</span><span class="sxs-lookup"><span data-stu-id="f26ec-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="f26ec-139">Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в hello ресурсы автоматизации Azure и выберите слишком![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="f26ec-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="f26ec-140">Выберите тип переменной hello как **строка**</span><span class="sxs-lookup"><span data-stu-id="f26ec-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="f26ec-141">В качестве имени переменной укажите **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="f26ec-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="f26ec-142">Задайте в качестве значения переменной hello фактическое имя подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="f26ec-143">Можно определить имя hello подписки со страницы приветствия параметры учетной записи пользователя на портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="f26ec-144">Добавление учетных данных для входа в Azure в качестве ресурса</span><span class="sxs-lookup"><span data-stu-id="f26ec-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="f26ec-145">Служба автоматизации Azure использует Azure PowerShell tooconnect toothe подписки и работает с существует артефакты hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="f26ec-146">Для этого необходимо пройти проверку подлинности с использованием учетной записи Майкрософт или рабочей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f26ec-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="f26ec-147">Hello учетные данные можно хранить в toobe активов использовать безопасным образом модулем hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f26ec-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="f26ec-148">Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в hello ресурсы автоматизации Azure и выберите пункт![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="f26ec-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="f26ec-149">Выберите тип учетных данных hello как **учетные данные Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f26ec-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="f26ec-150">Укажите имя hello как **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="f26ec-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="f26ec-151">Укажите hello имя пользователя и пароль в toosign с.</span><span class="sxs-lookup"><span data-stu-id="f26ec-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="f26ec-152">Теперь оба этих параметра доступны в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="f26ec-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="f26ec-153">Дополнительные сведения о предоставляется как tooconnect tooyour подписки через PowerShell [здесь](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f26ec-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="f26ec-154">Далее будет создан модуль runbook в службе автоматизации Azure, можно добавить конечную точку для hello интерфейса виртуальной машины после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="f26ec-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="f26ec-155">Контекст службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="f26ec-155">Azure automation context</span></span>
<span data-ttu-id="f26ec-156">ASR передает контекст переменной toohello runbook toohelp детерминированным сценариев.</span><span class="sxs-lookup"><span data-stu-id="f26ec-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="f26ec-157">Можно утверждать, что предсказуемы имена hello hello облачной службы и hello виртуальной машины, но происходит в том, что он не всегда hello место по причине toocertain сценариев, таких как hello один которых могли измениться имя hello hello виртуальной машины, из-за toounsupported символы в Azure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="f26ec-158">Поэтому эти сведения передаются toohello ASR плана восстановления в рамках hello *контекста*.</span><span class="sxs-lookup"><span data-stu-id="f26ec-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="f26ec-159">Ниже приведен пример того, как выглядит hello контекстной переменной.</span><span class="sxs-lookup"><span data-stu-id="f26ec-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="f26ec-160">в следующей таблице Hello содержит имя и описание для каждой переменной в контексте hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="f26ec-161">**Имя переменной**</span><span class="sxs-lookup"><span data-stu-id="f26ec-161">**Variable name**</span></span> | <span data-ttu-id="f26ec-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="f26ec-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f26ec-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="f26ec-163">RecoveryPlanName</span></span> |<span data-ttu-id="f26ec-164">Имя выполняемого плана.</span><span class="sxs-lookup"><span data-stu-id="f26ec-164">Name of plan being run.</span></span> <span data-ttu-id="f26ec-165">Помогает выполнить действия в имени с помощью hello же сценарий</span><span class="sxs-lookup"><span data-stu-id="f26ec-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="f26ec-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="f26ec-166">FailoverType</span></span> |<span data-ttu-id="f26ec-167">Указывает, является ли hello отработки отказа тестировать, плановой или незапланированной.</span><span class="sxs-lookup"><span data-stu-id="f26ec-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="f26ec-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="f26ec-168">FailoverDirection</span></span> |<span data-ttu-id="f26ec-169">Укажите, является ли восстановления tooprimary или получателя</span><span class="sxs-lookup"><span data-stu-id="f26ec-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="f26ec-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="f26ec-170">GroupID</span></span> |<span data-ttu-id="f26ec-171">Определите hello номер группы в соответствии с планом восстановления hello при выполнении плана hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="f26ec-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="f26ec-172">VmMap</span></span> |<span data-ttu-id="f26ec-173">Массив всех hello виртуальных машин в группе hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="f26ec-174">Ключ VMMap</span><span class="sxs-lookup"><span data-stu-id="f26ec-174">VMMap key</span></span> |<span data-ttu-id="f26ec-175">Уникальный ключ (GUID) для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f26ec-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="f26ec-176">Имеет hello равна hello VMM с Идентификатором hello виртуальной машины, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="f26ec-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="f26ec-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="f26ec-177">RoleName</span></span> |<span data-ttu-id="f26ec-178">Имя виртуальной Машины Azure, в которой выполняется восстановление hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="f26ec-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="f26ec-179">CloudServiceName</span></span> |<span data-ttu-id="f26ec-180">В разделе какие hello создается виртуальная машина Azure имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f26ec-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="f26ec-181">Здравствуйте, tooidentify VmMap ключ в контексте hello можно также перейти на странице свойств виртуальной Машины toohello в ASR и посмотрите на hello свойство GUID виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f26ec-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="f26ec-182">Создание модуля Runbook службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="f26ec-182">Author an Automation runbook</span></span>
<span data-ttu-id="f26ec-183">Теперь создайте hello runbook tooopen порт 80 на виртуальной машине hello для переднего плана.</span><span class="sxs-lookup"><span data-stu-id="f26ec-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="f26ec-184">Создание модуля runbook в учетной записи службы автоматизации Azure с именем hello hello **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="f26ec-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="f26ec-185">Перейдите toohello представление Автор hello runbook и введите hello черновом режиме.</span><span class="sxs-lookup"><span data-stu-id="f26ec-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="f26ec-186">Сначала укажите hello переменной toouse как hello контекст плана восстановления</span><span class="sxs-lookup"><span data-stu-id="f26ec-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="f26ec-187">Затем подключения toohello подписку, используя имя учетных данных и подписки hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="f26ec-188">Обратите внимание, что используется hello Azure активы — **AzureCredential** и **AzureSubscriptionName** здесь.</span><span class="sxs-lookup"><span data-stu-id="f26ec-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="f26ec-189">Теперь укажите сведения о конечной точке hello и hello GUID hello виртуальной машины, для которого требуется конечная точка tooexpose hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="f26ec-190">Виртуальная машина переднего плана вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="f26ec-191">Указывает hello протокола конечной точки Azure, локальный на hello виртуальной Машины и ее сопоставленных открытый порт.</span><span class="sxs-lookup"><span data-stu-id="f26ec-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="f26ec-192">Эти переменные, параметры, необходимые по hello Azure команды, добавить tooVMs конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f26ec-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="f26ec-193">Hello VMGUID содержит hello hello виртуальная машина, которую требуется toooperate на идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="f26ec-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="f26ec-194">Hello скрипт будет извлечь hello контекст для hello, заданный идентификатором GUID виртуальной Машины и создайте конечную точку на виртуальной машине hello, он ссылается.</span><span class="sxs-lookup"><span data-stu-id="f26ec-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="f26ec-195">После завершения этого процесса попаданий публикации ![](media/site-recovery-runbook-automation/20.png) tooallow toobe вашего сценария, для выполнения.</span><span class="sxs-lookup"><span data-stu-id="f26ec-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="f26ec-196">для справки ниже приведен полный сценарий Hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="f26ec-197">Добавление плана восстановления toohello сценария hello</span><span class="sxs-lookup"><span data-stu-id="f26ec-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="f26ec-198">После подготовки скрипта hello, его можно добавить toohello план восстановления, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="f26ec-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="f26ec-199">В план восстановления hello, который вы создали выберите tooadd сценарий после группы 2.</span><span class="sxs-lookup"><span data-stu-id="f26ec-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="f26ec-200">Укажите название сценария.</span><span class="sxs-lookup"><span data-stu-id="f26ec-200">Specify a script name.</span></span> <span data-ttu-id="f26ec-201">Это просто понятное имя для этого сценария для отображение в плане восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="f26ec-202">В скрипте tooAzure hello перехода на другой ресурс — выберите имя учетной записи службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f26ec-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="f26ec-203">Выберите runbook hello, созданные в hello Azure модули Runbook.</span><span class="sxs-lookup"><span data-stu-id="f26ec-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="f26ec-204">Первичные сценарии</span><span class="sxs-lookup"><span data-stu-id="f26ec-204">Primary side scripts</span></span>
<span data-ttu-id="f26ec-205">При выполнении tooAzure перехода на другой ресурс, также можно tooexecute первичный скриптов.</span><span class="sxs-lookup"><span data-stu-id="f26ec-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="f26ec-206">Эти скрипты будут выполняться на сервере VMM hello во время перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="f26ec-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="f26ec-207">Первичные сценарии доступны только для этапов «до выключения» и «после выключения».</span><span class="sxs-lookup"><span data-stu-id="f26ec-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="f26ec-208">Это так, как ожидается, что основной сайт toobe hello обычно недоступна при аварии на сервере.</span><span class="sxs-lookup"><span data-stu-id="f26ec-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="f26ec-209">Во время внеплановой отработки отказа только в том случае, если вы выбрали в операциях первичного сайта, он предпримет toorun hello первичный скриптов.</span><span class="sxs-lookup"><span data-stu-id="f26ec-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="f26ec-210">Если они не доступны или тайм-аута hello отработки отказа продолжит toorecover hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f26ec-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="f26ec-211">Первичный сценариев без доступны для узлов VMware или физических/Hyper-v без VMM защищенных tooAzure - во время перехода на другой ресурс tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="f26ec-212">Тем не менее, когда восстановление из Azure tooon организациями, первичный скриптов (Runbooks) может использоваться для всех целевых объектов, за исключением VMware.</span><span class="sxs-lookup"><span data-stu-id="f26ec-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="f26ec-213">План восстановления hello тестирования</span><span class="sxs-lookup"><span data-stu-id="f26ec-213">Test hello recovery plan</span></span>
<span data-ttu-id="f26ec-214">После добавления hello runbook toohello плана можно инициировать тестовую отработку отказа и посмотрите в действии.</span><span class="sxs-lookup"><span data-stu-id="f26ec-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="f26ec-215">Всегда рекомендуется toorun tootest теста отработки отказа вашего приложения и hello восстановления плана tooensure, нет ли ошибок.</span><span class="sxs-lookup"><span data-stu-id="f26ec-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="f26ec-216">Выберите план восстановления hello и инициировать тестовую отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="f26ec-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="f26ec-217">Во время выполнения плана hello вы увидите hello runbook выполнен или не с помощью его состояние.</span><span class="sxs-lookup"><span data-stu-id="f26ec-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="f26ec-218">Можно также просмотреть hello сведения о состоянии выполнения runbook на странице заданий службы автоматизации Azure hello hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f26ec-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="f26ec-219">После завершения отработки отказа hello, отдельно от результата выполнения модуля runbook hello, видно ли hello выполнение было успешным или нет, посетив страницу приветствия виртуальной машины Azure и оценив hello конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f26ec-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="f26ec-220">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="f26ec-220">Sample scripts</span></span>
<span data-ttu-id="f26ec-221">Хотя мы рассмотрения автоматизация один часто используемые задачи по добавлению конечной точки tooan виртуальной машины Azure в этом учебнике, можно выполнить ряд других мощных автоматизации задач, с помощью автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f26ec-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="f26ec-222">Корпорация Майкрософт и сообщества Azure Automation hello предоставляют образцы модулей Runbook, которые помогут вам приступить к созданию собственного решения и программа Runbook, которые можно использовать в качестве стандартных блоков для более крупных задач автоматизации.</span><span class="sxs-lookup"><span data-stu-id="f26ec-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="f26ec-223">Начать использовать их из галереи hello и мощные восстановления одним щелчком на планы построения для приложений с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f26ec-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f26ec-224">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f26ec-224">Additional Resources</span></span>
[<span data-ttu-id="f26ec-225">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="f26ec-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")

[<span data-ttu-id="f26ec-226">Примеры сценариев службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="f26ec-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
