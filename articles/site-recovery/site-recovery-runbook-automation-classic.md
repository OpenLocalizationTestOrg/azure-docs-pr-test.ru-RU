---
title: "Добавление модулей Runbook службы автоматизации Azure в планы восстановления на классическом портале | Документация Майкрософт"
description: "В этой статье описывается, как Azure Site Recovery позволяет расширить планы восстановления с помощью службы автоматизации Azure для выполнения сложных задач во время восстановления в Azure."
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
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="fcef8-103">Добавление модулей Runbook службы автоматизации Azure в планы восстановления на классическом портале</span><span class="sxs-lookup"><span data-stu-id="fcef8-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="fcef8-104">В этом руководстве описывается, как Azure Site Recovery интегрируется со службой автоматизации Azure для обеспечения расширяемости для планов восстановления.</span><span class="sxs-lookup"><span data-stu-id="fcef8-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="fcef8-105">Планы восстановления позволяют управлять восстановлением виртуальных машин, защищенных с помощью Azure Site Recovery, как для репликации в дополнительное облако, так и для репликации в сценарии Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="fcef8-106">Они также помогают реализовать **точное**, **воспроизводимое** и **автоматическое** восстановление.</span><span class="sxs-lookup"><span data-stu-id="fcef8-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="fcef8-107">Если выполняется отработка отказа с переносом виртуальных машин в Azure, интеграция со службой автоматизации Azure позволяет расширить планы восстановления и предоставляет возможность выполнять Runbook, а это, в свою очередь, позволяет значительно облегчить выполнение задач автоматизации.</span><span class="sxs-lookup"><span data-stu-id="fcef8-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="fcef8-108">Если вы еще не знакомы со службой автоматизации Azure, зарегистрируйтесь [здесь](https://azure.microsoft.com/services/automation/) и скачайте примеры сценариев [здесь](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="fcef8-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="fcef8-109">Дополнительные сведения об [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) и о том, как управлять восстановлением в Azure с помощью планов восстановления, см. [здесь](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="fcef8-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="fcef8-110">В этом кратком руководстве мы рассмотрим то, как можно интегрировать модули Runbook службы автоматизации Azure в планы восстановления.</span><span class="sxs-lookup"><span data-stu-id="fcef8-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="fcef8-111">Мы автоматизируем выполнение простых задач, которые ранее требовалось выполнять вручную, и узнаем, как преобразовать процесс восстановления, включающий несколько этапов, в действие восстановления одним щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="fcef8-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="fcef8-112">Также мы рассмотрим порядок устранения ошибок, возникающих при выполнении простого сценария.</span><span class="sxs-lookup"><span data-stu-id="fcef8-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="fcef8-113">Защита приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="fcef8-113">Protect the application to Azure</span></span>
<span data-ttu-id="fcef8-114">Начнем с простого приложения HRweb компании Fabrikam,</span><span class="sxs-lookup"><span data-stu-id="fcef8-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="fcef8-115">состоящего из двух виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="fcef8-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="fcef8-116">Fabrikam-HRweb-frontend и Fabrikam-Hrweb-backend. Эти виртуальные машины защищены в Azure с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fcef8-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="fcef8-117">Чтобы защитить виртуальные машины с помощью Azure Site Recovery, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fcef8-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="fcef8-118">Включите защиту для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fcef8-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="fcef8-119">Убедитесь, что виртуальные машины завершили начальную репликацию и выполняют репликацию.</span><span class="sxs-lookup"><span data-stu-id="fcef8-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="fcef8-120">Дождитесь завершения начальной репликации (в столбце "Состояние репликации" должно быть указано "Защищено").</span><span class="sxs-lookup"><span data-stu-id="fcef8-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="fcef8-121">В этом руководстве мы создадим план восстановления для приложения HRweb компании Fabrikam для отработки отказа приложения с переносом его в Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="fcef8-122">Затем мы интегрируем приложение с модулем Runbook, который создаст конечную точку на резервной виртуальной машине Azure для обслуживания веб-страниц через порт 80.</span><span class="sxs-lookup"><span data-stu-id="fcef8-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="fcef8-123">Сначала создадим план восстановления для приложения.</span><span class="sxs-lookup"><span data-stu-id="fcef8-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="fcef8-124">Создание плана восстановления</span><span class="sxs-lookup"><span data-stu-id="fcef8-124">Create the recovery plan</span></span>
<span data-ttu-id="fcef8-125">Чтобы восстановить приложение в Azure, необходимо создать план восстановления.</span><span class="sxs-lookup"><span data-stu-id="fcef8-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="fcef8-126">С помощью плана восстановления можно задать порядок восстановления виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fcef8-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="fcef8-127">Виртуальная машина, помещенная в группу 1, будет восстановлена и запущена первой, после чего аналогичные действия выполняются для виртуальной машины в группе 2.</span><span class="sxs-lookup"><span data-stu-id="fcef8-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="fcef8-128">Создайте план восстановления, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fcef8-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="fcef8-129">Дополнительные сведения о планах восстановления см. в документации, представленной[здесь](https://msdn.microsoft.com/library/azure/dn788799.aspx "здесь").</span><span class="sxs-lookup"><span data-stu-id="fcef8-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="fcef8-130">Теперь создадим необходимые артефакты в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="fcef8-131">Создание учетной записи службы автоматизации и соответствующих ресурсов</span><span class="sxs-lookup"><span data-stu-id="fcef8-131">Create the automation account and its assets</span></span>
<span data-ttu-id="fcef8-132">Для создания модулей Runbook требуется учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="fcef8-133">Если у вас еще нет такой учетной записи, перейдите на вкладку службы автоматизации Azure, обозначенную как ![](media/site-recovery-runbook-automation/02.png), и создайте учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fcef8-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="fcef8-134">Присвойте имя учетной записи для ее идентификации.</span><span class="sxs-lookup"><span data-stu-id="fcef8-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="fcef8-135">Укажите географический регион, где требуется разместить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fcef8-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="fcef8-136">Учетную запись рекомендуется размещать в том же регионе, в котором находится хранилище ASR.</span><span class="sxs-lookup"><span data-stu-id="fcef8-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="fcef8-137">Затем создадим в учетной записи указанные ниже ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fcef8-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="fcef8-138">Добавление названия подписки в качестве ресурса</span><span class="sxs-lookup"><span data-stu-id="fcef8-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="fcef8-139">Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в разделе ресурсов службы автоматизации Azure и нажмите ![](media/site-recovery-runbook-automation/05.png).</span><span class="sxs-lookup"><span data-stu-id="fcef8-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="fcef8-140">В качестве типа переменной выберите **Строка**</span><span class="sxs-lookup"><span data-stu-id="fcef8-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="fcef8-141">В качестве имени переменной укажите **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="fcef8-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="fcef8-142">В качестве значения переменной укажите фактическое имя подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="fcef8-143">Имя подписки указано на странице параметров учетной записи на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="fcef8-144">Добавление учетных данных для входа в Azure в качестве ресурса</span><span class="sxs-lookup"><span data-stu-id="fcef8-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="fcef8-145">Служба автоматизации Azure использует Azure PowerShell для подключения к подписке и оперирования артефактами.</span><span class="sxs-lookup"><span data-stu-id="fcef8-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="fcef8-146">Для этого необходимо пройти проверку подлинности с использованием учетной записи Майкрософт или рабочей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fcef8-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="fcef8-147">Учетные данные можно хранить в ресурсе для их безопасного использования модулем Runbook.</span><span class="sxs-lookup"><span data-stu-id="fcef8-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="fcef8-148">Добавьте новый параметр ![](media/site-recovery-runbook-automation/04.png) в разделе ресурсов службы автоматизации Azure и нажмите ![](media/site-recovery-runbook-automation/09.png).</span><span class="sxs-lookup"><span data-stu-id="fcef8-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="fcef8-149">Для параметра "Тип учетных данных" выберите **Учетные данные Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fcef8-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="fcef8-150">Укажите имя **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="fcef8-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="fcef8-151">Укажите имя пользователя и пароль для входа.</span><span class="sxs-lookup"><span data-stu-id="fcef8-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="fcef8-152">Теперь оба этих параметра доступны в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="fcef8-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="fcef8-153">Дополнительные сведения о подключении к подписке через PowerShell см. [здесь](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fcef8-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="fcef8-154">Затем создадим в службе автоматизации Azure модуль Runbook, который может добавить конечную точку для интерфейсной виртуальной машины после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="fcef8-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="fcef8-155">Контекст службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcef8-155">Azure automation context</span></span>
<span data-ttu-id="fcef8-156">ASR передает в модуль Runbook переменную контекста, которая помогает создавать детерминированные сценарии.</span><span class="sxs-lookup"><span data-stu-id="fcef8-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="fcef8-157">Кто-то может утверждать, что имена облачной службы и виртуальной машины предсказуемые, однако это не всегда так, поскольку существуют сценарии, в которых, например, имя виртуальной машины могло быть изменено из-за неподдерживаемых Azure символов.</span><span class="sxs-lookup"><span data-stu-id="fcef8-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="fcef8-158">Поэтому такая информация передается в план восстановления ASR как часть *контекста*.</span><span class="sxs-lookup"><span data-stu-id="fcef8-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="fcef8-159">Ниже приведен пример того, как выглядит переменная контекста.</span><span class="sxs-lookup"><span data-stu-id="fcef8-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="fcef8-160">В таблице ниже указаны имя и описание для каждой переменной в контексте.</span><span class="sxs-lookup"><span data-stu-id="fcef8-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="fcef8-161">**Имя переменной**</span><span class="sxs-lookup"><span data-stu-id="fcef8-161">**Variable name**</span></span> | <span data-ttu-id="fcef8-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="fcef8-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fcef8-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="fcef8-163">RecoveryPlanName</span></span> |<span data-ttu-id="fcef8-164">Имя выполняемого плана.</span><span class="sxs-lookup"><span data-stu-id="fcef8-164">Name of plan being run.</span></span> <span data-ttu-id="fcef8-165">Позволяет предпринять действия на основе имени, используя тот же скрипт</span><span class="sxs-lookup"><span data-stu-id="fcef8-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="fcef8-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="fcef8-166">FailoverType</span></span> |<span data-ttu-id="fcef8-167">Указывает, является ли выполнение тестовым, запланированным или незапланированным.</span><span class="sxs-lookup"><span data-stu-id="fcef8-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="fcef8-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="fcef8-168">FailoverDirection</span></span> |<span data-ttu-id="fcef8-169">Указывает, производится ли восстановление в первичное или вторичное расположение</span><span class="sxs-lookup"><span data-stu-id="fcef8-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="fcef8-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="fcef8-170">GroupID</span></span> |<span data-ttu-id="fcef8-171">Определяет номер группы в плане восстановления при выполнении плана</span><span class="sxs-lookup"><span data-stu-id="fcef8-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="fcef8-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="fcef8-172">VmMap</span></span> |<span data-ttu-id="fcef8-173">Это массив всех виртуальных машин в группе.</span><span class="sxs-lookup"><span data-stu-id="fcef8-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="fcef8-174">Ключ VMMap</span><span class="sxs-lookup"><span data-stu-id="fcef8-174">VMMap key</span></span> |<span data-ttu-id="fcef8-175">Уникальный ключ (GUID) для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fcef8-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="fcef8-176">Это то же самое, что и VMM ID виртуальной машины, там, где это применимо.</span><span class="sxs-lookup"><span data-stu-id="fcef8-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="fcef8-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="fcef8-177">RoleName</span></span> |<span data-ttu-id="fcef8-178">Имя виртуальной машины Azure, для которой выполняется восстановление</span><span class="sxs-lookup"><span data-stu-id="fcef8-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="fcef8-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="fcef8-179">CloudServiceName</span></span> |<span data-ttu-id="fcef8-180">Имя облачной службы Azure, под которой создана виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="fcef8-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="fcef8-181">Чтобы определить переменную VmMap Key в контексте, также можно перейти на страницу свойств виртуальной машины в ASR и обратиться к свойству VMGUID.</span><span class="sxs-lookup"><span data-stu-id="fcef8-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="fcef8-182">Создание модуля Runbook службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="fcef8-182">Author an Automation runbook</span></span>
<span data-ttu-id="fcef8-183">Теперь создадим модуль Runbook для открытия порта 80 на интерфейсной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="fcef8-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="fcef8-184">Создайте новый модуль Runbook в учетной записи службы автоматизации Azure и присвойте ему имя **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="fcef8-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="fcef8-185">Перейдите в представление создания модуля Runbook и войдите в режиме черновика.</span><span class="sxs-lookup"><span data-stu-id="fcef8-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="fcef8-186">Сначала укажите переменную, которая будет использоваться в качестве контекста плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="fcef8-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="fcef8-187">Затем подключитесь к подписке, указав учетные данные и имя подписки.</span><span class="sxs-lookup"><span data-stu-id="fcef8-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="fcef8-188">Обратите внимание, что здесь используются ресурсы **AzureCredential** и **AzureSubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="fcef8-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="fcef8-189">Теперь укажите сведения о конечной точке и идентификатор GUID виртуальной машины, для которой требуется предоставить конечную точку.</span><span class="sxs-lookup"><span data-stu-id="fcef8-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="fcef8-190">В данном случае это интерфейсная виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="fcef8-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="fcef8-191">Эти сведения включают протокол конечной точки Azure, локальный порт на виртуальной машине и сопоставленный ему открытый порт.</span><span class="sxs-lookup"><span data-stu-id="fcef8-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="fcef8-192">Эти переменные выступают в качестве параметров, необходимых для выполнения команд Azure по добавлению конечных точек для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fcef8-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="fcef8-193">VMGUID содержит идентификатор GUID виртуальной машины, с которой необходимо выполнить требуемые операции.</span><span class="sxs-lookup"><span data-stu-id="fcef8-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="fcef8-194">Теперь этот сценарий позволит извлечь контекст для заданного идентификатора VMGUID и создать конечную точку на виртуальной машине, на которую указывает этот идентификатор.</span><span class="sxs-lookup"><span data-stu-id="fcef8-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="fcef8-195">После этого нажмите "Опубликовать" ![](media/site-recovery-runbook-automation/20.png) , чтобы сценарий стал доступен для выполнения.</span><span class="sxs-lookup"><span data-stu-id="fcef8-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="fcef8-196">Ниже приведен полный код сценария для справки.</span><span class="sxs-lookup"><span data-stu-id="fcef8-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="fcef8-197">Добавление сценария в план восстановления</span><span class="sxs-lookup"><span data-stu-id="fcef8-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="fcef8-198">После того как сценарий готов, его можно добавить в план восстановления, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="fcef8-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="fcef8-199">В созданном ранее плане восстановления выберите команду добавления сценария после группы 2.</span><span class="sxs-lookup"><span data-stu-id="fcef8-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="fcef8-200">Укажите название сценария.</span><span class="sxs-lookup"><span data-stu-id="fcef8-200">Specify a script name.</span></span> <span data-ttu-id="fcef8-201">Достаточно указать понятное имя для этого сценария для отображения в плане восстановления.</span><span class="sxs-lookup"><span data-stu-id="fcef8-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="fcef8-202">В поле выбора сценария отработки отказа в Azure выберите в раскрывающемся списке имя учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="fcef8-203">В поле выбора сценария модуля Runbook Azure выберите в раскрывающемся списке созданный вами модуль.</span><span class="sxs-lookup"><span data-stu-id="fcef8-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="fcef8-204">Первичные сценарии</span><span class="sxs-lookup"><span data-stu-id="fcef8-204">Primary side scripts</span></span>
<span data-ttu-id="fcef8-205">При отработке отказа в Azure также можно выбрать первичные сценарии для выполнения.</span><span class="sxs-lookup"><span data-stu-id="fcef8-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="fcef8-206">Эти сценарии будут запущены на сервере VMM при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="fcef8-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="fcef8-207">Первичные сценарии доступны только для этапов «до выключения» и «после выключения».</span><span class="sxs-lookup"><span data-stu-id="fcef8-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="fcef8-208">Это объясняется тем, что первичный сценарий обычно считается недоступным при возникновении сбоя.</span><span class="sxs-lookup"><span data-stu-id="fcef8-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="fcef8-209">Во время внеплановой отработки отказа первичные сценарии будут запущены только в том случае, если вы выбрали их запуск.</span><span class="sxs-lookup"><span data-stu-id="fcef8-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="fcef8-210">Если они недоступны или тайм-аут их ожидания истек, отработка отказа будет продолжена для восстановления виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fcef8-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="fcef8-211">При отработке отказа в Azure первичные сценарии недоступны для сайтов VMware/Hyper-v и физических узлов, на которых не настроена защита VMM на Azure.</span><span class="sxs-lookup"><span data-stu-id="fcef8-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="fcef8-212">Однако при отработке отказа из Azure в локальную среду сценарии для первичных реплик могут использоваться для всех целевых объектов, за исключением VMware.</span><span class="sxs-lookup"><span data-stu-id="fcef8-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="fcef8-213">Тестирование плана восстановления</span><span class="sxs-lookup"><span data-stu-id="fcef8-213">Test the recovery plan</span></span>
<span data-ttu-id="fcef8-214">После добавления модуля Runbook в план можно запустить тестовую отработку отказа и посмотреть модуль в действии.</span><span class="sxs-lookup"><span data-stu-id="fcef8-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="fcef8-215">Рекомендуется всегда выполнить тестовую отработку отказа для тестирования приложения и плана восстановления, чтобы убедиться в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="fcef8-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="fcef8-216">Выберите план восстановления и запустите тестовую отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="fcef8-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="fcef8-217">Во время выполнения плана можно просмотреть, был ли выполнен модуль или нет, обратившись к сведениям о его состоянии.</span><span class="sxs-lookup"><span data-stu-id="fcef8-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="fcef8-218">Кроме того, можно перейти на страницу заданий службы автоматизации Azure для модуля, чтобы ознакомиться с подробными сведениями о состоянии выполнении модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="fcef8-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="fcef8-219">После завершения отработки отказа, помимо результатов выполнения модуля Runbook, можно просмотреть сведения о том, было ли выполнение успешным. Для этого посетите страницу виртуальной машины Azure и обратитесь к сведениям о конечных точках.</span><span class="sxs-lookup"><span data-stu-id="fcef8-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="fcef8-220">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="fcef8-220">Sample scripts</span></span>
<span data-ttu-id="fcef8-221">В данном руководстве мы рассмотрели автоматизацию одной часто используемой задачи по добавлению конечной точки к виртуальной машине Azure, однако с помощью службы автоматизации Azure можно выполнять множество других задач по эффективной автоматизации.</span><span class="sxs-lookup"><span data-stu-id="fcef8-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="fcef8-222">Мы совместно с сообществом, которое создалось вокруг службы автоматизации Azure, предоставляем примеры модулей Runbook, которые помогут вам научиться создавать собственные решения, а также вспомогательные модули, которые можно использовать для создания более крупных задач автоматизации.</span><span class="sxs-lookup"><span data-stu-id="fcef8-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="fcef8-223">Приступите к работе с ними и воспользуйтесь коллекцией примеров для создания эффективных планов восстановления своих приложений одним щелчком мыши с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fcef8-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcef8-224">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fcef8-224">Additional Resources</span></span>
[<span data-ttu-id="fcef8-225">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcef8-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")

[<span data-ttu-id="fcef8-226">Примеры сценариев службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="fcef8-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
