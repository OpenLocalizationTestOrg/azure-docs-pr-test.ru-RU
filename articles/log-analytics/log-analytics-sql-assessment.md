---
title: "aaaOptimize среды SQL Server с помощью анализа журналов Azure | Документы Microsoft"
description: "С помощью аналитики журналов Azure можно использовать hello оценки SQL tooassess решения hello риска и работоспособности среды SQL server через равные промежутки времени."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="4359f-103">Оптимизация среды SQL Server с hello решение для оценки SQL в службе анализа журналов</span><span class="sxs-lookup"><span data-stu-id="4359f-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![Символ оценки SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="4359f-105">Можно использовать hello оценки SQL tooassess решения hello риска и работоспособности серверной среды с регулярным интервалом.</span><span class="sxs-lookup"><span data-stu-id="4359f-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="4359f-106">Эта статья поможет вам установить решение hello, позволяют предпринимать корректирующие действия для потенциальных проблем.</span><span class="sxs-lookup"><span data-stu-id="4359f-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="4359f-107">Это решение предоставляет упорядоченный список рекомендаций конкретных tooyour развернутой серверной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="4359f-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="4359f-108">Hello рекомендации разделены на шесть фокуса, областей, которые помогают быстро понять hello риска и примите необходимые меры.</span><span class="sxs-lookup"><span data-stu-id="4359f-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="4359f-109">Hello рекомендации основаны на hello знания и опыт, приобретенные специалистами Майкрософт в результате многочисленных посещений клиентов.</span><span class="sxs-lookup"><span data-stu-id="4359f-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="4359f-110">Каждая рекомендация содержит обоснования, почему проблема может играть важную роль tooyou и как tooimplement hello предложенные изменения.</span><span class="sxs-lookup"><span data-stu-id="4359f-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="4359f-111">Можно выбрать приоритетные области, наиболее важные tooyour организации и отслеживать выполнение задач по рисков формированию работоспособной и свободной среды.</span><span class="sxs-lookup"><span data-stu-id="4359f-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="4359f-112">После добавления решения hello и оценка завершенной, сводные данные по приоритетным областям отображается на hello **оценки SQL** панель мониторинга для hello инфраструктуры в среде.</span><span class="sxs-lookup"><span data-stu-id="4359f-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="4359f-113">Hello ниже описано, как toouse hello сведения о hello **оценки SQL** мониторинга, где можно просматривать и предпринимать рекомендуемые действия для серверной инфраструктуры SQL.</span><span class="sxs-lookup"><span data-stu-id="4359f-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![image of SQL Assessment tile](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![image of SQL Assessment dashboard](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="4359f-116">Установка и настройка решения hello</span><span class="sxs-lookup"><span data-stu-id="4359f-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="4359f-117">Оценка SQL работает со всеми версиями SQL Server для выпусков Standard, Developer и Enterprise hello, поддерживаемых в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="4359f-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="4359f-118">Используйте следующие сведения tooinstall hello и настроить решение hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="4359f-119">Агенты должны устанавливаться на серверах, на которых установлен SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4359f-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="4359f-120">Hello решение для оценки SQL требуется поддерживаемая версия платформы .NET Framework 4 установлена на каждом компьютере, где установлен агент OMS.</span><span class="sxs-lookup"><span data-stu-id="4359f-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="4359f-121">В решении hello tooinstall порядок hello пользователь должен быть toohello администратора или участника подписки Azure при с помощью портала Azure "hello".</span><span class="sxs-lookup"><span data-stu-id="4359f-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="4359f-122">Кроме того hello пользователь должен быть членом hello OMS рабочей участника или администратора роли на портале OMS hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="4359f-123">При использовании hello агент Operations Manager с помощью оценки SQL, вам потребуется toouse Operations Manager Run-As учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4359f-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="4359f-124">Дополнительные сведения см. в разделе ниже [Учетные записи запуска от имени в Operations Manager для службы OMS](#operations-manager-run-as-accounts-for-oms).</span><span class="sxs-lookup"><span data-stu-id="4359f-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4359f-125">агент MMA Hello не поддерживает учетные записи Operations Manager Run-As.</span><span class="sxs-lookup"><span data-stu-id="4359f-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="4359f-126">Добавить tooyour решения оценки SQL hello, рабочую область OMS hello процесс описывается в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4359f-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="4359f-127">Дополнительная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="4359f-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="4359f-128">После добавления решения hello tooservers с агентами добавляется файл AdvisorAssessment.exe hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="4359f-129">Данные конфигурации считываются и затем отправляется toohello службой OMS в облаке hello для обработки.</span><span class="sxs-lookup"><span data-stu-id="4359f-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="4359f-130">Логика является примененных toohello полученных данных и hello облачная служба записывает данные hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="4359f-131">Сведения о сборе данных по оценке SQL</span><span class="sxs-lookup"><span data-stu-id="4359f-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="4359f-132">Оценка SQL собирает данные WMI, данные реестра, данные о производительности и результатов представления динамического управления SQL Server, с помощью hello агенты, которые вы включили.</span><span class="sxs-lookup"><span data-stu-id="4359f-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="4359f-133">Hello следующей таблице приведены методы сбора данных для агентов, ли Operations Manager (SCOM) является обязательным и как часто данные собираются агентом.</span><span class="sxs-lookup"><span data-stu-id="4359f-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="4359f-134">платформа</span><span class="sxs-lookup"><span data-stu-id="4359f-134">platform</span></span> | <span data-ttu-id="4359f-135">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="4359f-135">Direct Agent</span></span> | <span data-ttu-id="4359f-136">Агент SCOM</span><span class="sxs-lookup"><span data-stu-id="4359f-136">SCOM agent</span></span> | <span data-ttu-id="4359f-137">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="4359f-137">Azure Storage</span></span> | <span data-ttu-id="4359f-138">Нужен ли SCOM?</span><span class="sxs-lookup"><span data-stu-id="4359f-138">SCOM required?</span></span> | <span data-ttu-id="4359f-139">Отправка данных агента SCOM через группу управления</span><span class="sxs-lookup"><span data-stu-id="4359f-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="4359f-140">частота сбора</span><span class="sxs-lookup"><span data-stu-id="4359f-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4359f-141">Windows</span><span class="sxs-lookup"><span data-stu-id="4359f-141">Windows</span></span> | <span data-ttu-id="4359f-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4359f-142">&#8226;</span></span> | <span data-ttu-id="4359f-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4359f-143">&#8226;</span></span> |  |  | <span data-ttu-id="4359f-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4359f-144">&#8226;</span></span> |<span data-ttu-id="4359f-145">7 дней</span><span class="sxs-lookup"><span data-stu-id="4359f-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="4359f-146">Учетные записи запуска от имени в Operations Manager для службы OMS</span><span class="sxs-lookup"><span data-stu-id="4359f-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="4359f-147">Аналитика журналов в OMS использует агент Operations Manager hello и toocollect группы управления и отправки службой OMS toohello данных.</span><span class="sxs-lookup"><span data-stu-id="4359f-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="4359f-148">OMS строится на пакетах управления для рабочих нагрузок tooprovide ценных служб.</span><span class="sxs-lookup"><span data-stu-id="4359f-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="4359f-149">Каждая рабочая нагрузка требует наличия пакетов управления toorun привилегии, относящиеся в другом контексте безопасности, например учетной записи домена.</span><span class="sxs-lookup"><span data-stu-id="4359f-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="4359f-150">Необходимо tooprovide учетные данные, настроив Operations Manager запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4359f-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="4359f-151">Используйте следующие сведения tooset hello Operations Manager запуска от имени учетной записи для оценки SQL hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="4359f-152">Задать hello запись запуска от имени для оценки SQL</span><span class="sxs-lookup"><span data-stu-id="4359f-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="4359f-153">Если вы уже используете hello пакет управления SQL Server, следует использовать эту учетную запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="4359f-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="4359f-154">hello tooconfigure SQL запуска от учетной записи в консоли управления hello</span><span class="sxs-lookup"><span data-stu-id="4359f-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="4359f-155">При использовании hello OMS прямой агент, а не агент SCOM hello, пакет управления hello всегда запускается в контексте безопасности hello hello локальной системной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4359f-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="4359f-156">Пропустить шаги 1 – 5 ниже и выполнения либо hello образец T-SQL или Powershell, указав в качестве hello имя пользователя NT AUTHORITY\SYSTEM.</span><span class="sxs-lookup"><span data-stu-id="4359f-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="4359f-157">В Operations Manager откройте консоль управления hello и нажмите кнопку **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="4359f-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="4359f-158">В разделе **Настройка запуска от имени** щелкните **Профили** и откройте **Профиль запуска от имени для оценки SQL в OMS**.</span><span class="sxs-lookup"><span data-stu-id="4359f-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="4359f-159">На hello **учетные записи запуска от** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="4359f-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="4359f-160">Выберите учетную запись запуска от имени Windows, содержащий hello учетные данные, необходимые для SQL Server, или нажмите кнопку **New** toocreate один.</span><span class="sxs-lookup"><span data-stu-id="4359f-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4359f-161">Hello типа учетной записи запуска от имени должен быть Windows.</span><span class="sxs-lookup"><span data-stu-id="4359f-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="4359f-162">Hello учетная запись запуска от имени также должна входить группы локальных администраторов на всех серверах Windows, размещения экземпляров SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4359f-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="4359f-163">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4359f-163">Click **Save**.</span></span>
6. <span data-ttu-id="4359f-164">Изменения, а затем выполните следующий пример T-SQL на tooRun минимальные разрешения необходимые tooperform учетную запись от имени для оценки SQL toogrant каждого экземпляра SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="4359f-165">Тем не менее вам это не требуется toodo Если учетная запись запуска от имени уже является частью серверной роли sysadmin hello в экземплярах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4359f-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="4359f-166">hello tooconfigure SQL запуска от учетной записи с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4359f-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="4359f-167">Откройте окно PowerShell и выполните следующий скрипт после обновления его своими данными hello:</span><span class="sxs-lookup"><span data-stu-id="4359f-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="4359f-168">Основные сведения о приоритизации рекомендаций</span><span class="sxs-lookup"><span data-stu-id="4359f-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="4359f-169">Каждая рекомендация получает взвешенное значение, определяющее относительную важность рекомендаций hello hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="4359f-170">Отображаются только hello десять наиболее важных рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="4359f-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="4359f-171">Процесс вычисления взвешенного значения</span><span class="sxs-lookup"><span data-stu-id="4359f-171">How weights are calculated</span></span>
<span data-ttu-id="4359f-172">Взвешенные значения являются статистическими значениями, основанными на трех ключевых факторах.</span><span class="sxs-lookup"><span data-stu-id="4359f-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="4359f-173">Hello *вероятность* вызовет что проблемы, обнаруженной проблемы.</span><span class="sxs-lookup"><span data-stu-id="4359f-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="4359f-174">Более высокие значения вероятности приравниваются tooa высокой общей оценке для рекомендации hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="4359f-175">Hello *влияние* проблемы hello в вашей организации, если она является причиной проблемы.</span><span class="sxs-lookup"><span data-stu-id="4359f-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="4359f-176">Более высокая степень влияния приравнивается tooa высокой общей оценке для рекомендации hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="4359f-177">Hello *усилия* необходимые рекомендации tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="4359f-178">Более высокое значение усилий приравнивается tooa меньшей общей оценке для рекомендации hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="4359f-179">Hello весовой коэффициент для каждой рекомендации выражается в процентах от hello общей оценки, доступной для каждой приоритетной области.</span><span class="sxs-lookup"><span data-stu-id="4359f-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="4359f-180">Например если рекомендация в hello безопасности и соответствия приоритетной области имеет показатель 5%, реализация этой рекомендации увеличит общую оценку на 5% безопасности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="4359f-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="4359f-181">Приоритетные области</span><span class="sxs-lookup"><span data-stu-id="4359f-181">Focus areas</span></span>
<span data-ttu-id="4359f-182">**Безопасность и соответствие требованиям**. В этой области содержатся рекомендации в отношении возможных угроз, нарушений безопасности и корпоративных политик, а также технические, юридические и нормативные требования.</span><span class="sxs-lookup"><span data-stu-id="4359f-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="4359f-183">**Доступность и непрерывность бизнес-процессов**. Эта область содержит рекомендации в отношении доступности служб, устойчивости инфраструктуры и защиты бизнеса.</span><span class="sxs-lookup"><span data-stu-id="4359f-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="4359f-184">**Производительность и масштабируемость** -фокус в этой области отображается toohelp рекомендации вашей организации ИТ-инфраструктуры увеличиваться, убедитесь, что ИТ-среды требованиям текущей производительности и возможности toorespond toochanging требуется инфраструктура.</span><span class="sxs-lookup"><span data-stu-id="4359f-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="4359f-185">**Обновление, миграция и развертывание** — в этой области фокуса отображается toohelp рекомендации при обновлении, перенос и развертывание SQL Server tooyour существующей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="4359f-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="4359f-186">**Операции и мониторинг** : фокус в этой области отображается оптимизировать toohelp рекомендации ИТ-операций, реализовать профилактического обслуживания и повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="4359f-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="4359f-187">**Управление изменениями и настройкой** -рекомендаций в этой области фокуса отображается toohelp защита повседневной деятельности, убедитесь, что изменения не отрицательно повлиять на инфраструктуру, Разработка процедур управления изменениями и tootrack и аудита конфигурации системы.</span><span class="sxs-lookup"><span data-stu-id="4359f-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="4359f-188">Следует ли стремиться tooscore 100% в каждой приоритетной области?</span><span class="sxs-lookup"><span data-stu-id="4359f-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="4359f-189">Не обязательно.</span><span class="sxs-lookup"><span data-stu-id="4359f-189">Not necessarily.</span></span> <span data-ttu-id="4359f-190">Hello рекомендации основываются на hello знания и опыт, приобретенные специалистами Майкрософт в результате многочисленных посещений клиентов.</span><span class="sxs-lookup"><span data-stu-id="4359f-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="4359f-191">Однако не двух серверных инфраструктур, же hello и конкретные рекомендации могут быть более или менее соответствующие tooyou.</span><span class="sxs-lookup"><span data-stu-id="4359f-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="4359f-192">Например некоторые рекомендации по безопасности может быть менее значимыми, если виртуальные машины не предоставляется toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="4359f-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="4359f-193">Некоторые рекомендации о доступности могут иметь менее важное значение для служб, которые обеспечивают сбор низкоприоритетных данных.</span><span class="sxs-lookup"><span data-stu-id="4359f-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="4359f-194">Проблемы, которые являются важной tooa зрелой организации может быть менее важные tooa при запуске.</span><span class="sxs-lookup"><span data-stu-id="4359f-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="4359f-195">Можно tooidentify, какие области фокуса и затем отследить изменение оценок с течением времени.</span><span class="sxs-lookup"><span data-stu-id="4359f-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="4359f-196">В каждой рекомендации указано, почему она важна.</span><span class="sxs-lookup"><span data-stu-id="4359f-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="4359f-197">Следует использовать это руководство tooevaluate целесообразность реализации рекомендации hello, условии hello характера ИТ служб и hello потребностям вашей организации.</span><span class="sxs-lookup"><span data-stu-id="4359f-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="4359f-198">Использование рекомендаций по оцениваемой приоритетной области</span><span class="sxs-lookup"><span data-stu-id="4359f-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="4359f-199">Перед использованием решения оценки в OMS, необходимо установить решение hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="4359f-200">tooread Дополнительные сведения об установке решений, в разделе [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4359f-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="4359f-201">После установки, можно просмотреть сводку hello рекомендаций с помощью плитки оценки SQL hello на страницу обзора hello в OMS.</span><span class="sxs-lookup"><span data-stu-id="4359f-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="4359f-202">Представление hello суммирование оценок соответствия для инфраструктуры, а затем глубже изучить рекомендации.</span><span class="sxs-lookup"><span data-stu-id="4359f-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="4359f-203">рекомендации tooview фокус области и предпринять корректирующее действие</span><span class="sxs-lookup"><span data-stu-id="4359f-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="4359f-204">На hello **Обзор** щелкните hello **оценки SQL** плитки.</span><span class="sxs-lookup"><span data-stu-id="4359f-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="4359f-205">На hello **оценки SQL** , просмотрите сводные сведения о hello в одной из колонок приоритетной области hello и выберите один tooview рекомендации для этой приоритетной области.</span><span class="sxs-lookup"><span data-stu-id="4359f-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="4359f-206">На всех страницах интересующей области hello можно просмотреть hello приоритеты рекомендации для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="4359f-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="4359f-207">Щелкните рекомендацию, в разделе **затронутые объекты** tooview сведений о причинах hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="4359f-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="4359f-208">![Изображение с рекомендациями оценки SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="4359f-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="4359f-209">В разделе **Предложенные действия**представлены действия по исправлению, которые вы можете предпринять.</span><span class="sxs-lookup"><span data-stu-id="4359f-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="4359f-210">Когда hello элементом будет устранена, последующие оценки будут указывать, что рекомендованные действия были выполнены, и тогда оценка соответствия возрастет.</span><span class="sxs-lookup"><span data-stu-id="4359f-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="4359f-211">Исправленные элементы отображаются как **Прошедшие проверку объекты**.</span><span class="sxs-lookup"><span data-stu-id="4359f-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="4359f-212">Игнорирование рекомендаций</span><span class="sxs-lookup"><span data-stu-id="4359f-212">Ignore recommendations</span></span>
<span data-ttu-id="4359f-213">Если у вас есть рекомендации, что требуется tooignore, можно создать текстовый файл, который OMS будет использовать tooprevent отображения рекомендаций в результатах оценки.</span><span class="sxs-lookup"><span data-stu-id="4359f-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="4359f-214">tooidentify рекомендации, которые будет игнорировать</span><span class="sxs-lookup"><span data-stu-id="4359f-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="4359f-215">Войдите в рабочую область tooyour и откройте раздел поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="4359f-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="4359f-216">Используйте hello рекомендации запроса toolist сбоев для компьютеров в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="4359f-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="4359f-217">Вот запрос поиска журналов hello снимке экрана показан: ![сбой рекомендации](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="4359f-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="4359f-218">Выберите рекомендации, которые должны tooignore.</span><span class="sxs-lookup"><span data-stu-id="4359f-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="4359f-219">В следующей процедуре hello будут использоваться hello значения для recommendationid будут.</span><span class="sxs-lookup"><span data-stu-id="4359f-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="4359f-220">toocreate и использование текстового файла IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="4359f-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="4359f-221">Создайте файл с именем IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="4359f-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="4359f-222">Вставьте или введите каждое значение RecommendationId для каждой рекомендации требуется tooignore OMS в отдельной строке, а затем сохраните и закройте файл hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="4359f-223">Поместите файл hello в следующие папки на каждом компьютере место рекомендации tooignore OMS hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="4359f-224">На компьютерах с Microsoft Monitoring Agent (с подключением напрямую или с помощью Operations Manager) - hello *SystemDrive*: \Program Files\Microsoft Monitoring agent\agent.</span><span class="sxs-lookup"><span data-stu-id="4359f-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="4359f-225">На сервере управления Operations Manager hello - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="4359f-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="4359f-226">tooverify игнорирования рекомендаций</span><span class="sxs-lookup"><span data-stu-id="4359f-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="4359f-227">После запуска hello следующего запланированного оценки по умолчанию каждые 7 дней hello указан рекомендации помечаются как игнорируемые и не отображаются на панели мониторинга оценки hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="4359f-228">Можно использовать hello следующих toolist запросы поиска журналов всех рекомендаций hello игнорируются.</span><span class="sxs-lookup"><span data-stu-id="4359f-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="4359f-229">Если вы решите позже, toosee учитываются рекомендации, удалите все файлы IgnoreRecommendations.txt или удалите из них Recommendationid.</span><span class="sxs-lookup"><span data-stu-id="4359f-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="4359f-230">Часто задаваемые вопросы по решениям оценки SQL</span><span class="sxs-lookup"><span data-stu-id="4359f-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="4359f-231">*Как часто выполняется оценка?*</span><span class="sxs-lookup"><span data-stu-id="4359f-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="4359f-232">Hello оценка выполняется каждые 7 дней.</span><span class="sxs-lookup"><span data-stu-id="4359f-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="4359f-233">*Есть ли способ tooconfigure как часто выполняется оценка hello?*</span><span class="sxs-lookup"><span data-stu-id="4359f-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="4359f-234">На данный момент нет.</span><span class="sxs-lookup"><span data-stu-id="4359f-234">Not at this time.</span></span>

<span data-ttu-id="4359f-235">*Если после добавления решения оценки SQL hello обнаружен другой сервер, будет оценивается ли он?*</span><span class="sxs-lookup"><span data-stu-id="4359f-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="4359f-236">Да, после обнаружения он оценивается каждые 7 дней.</span><span class="sxs-lookup"><span data-stu-id="4359f-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="4359f-237">*Если сервер выведен из эксплуатации, когда он будет удален из оценки hello?*</span><span class="sxs-lookup"><span data-stu-id="4359f-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="4359f-238">Если сервер не отправляет данные в течение 3 недель, то он удаляется.</span><span class="sxs-lookup"><span data-stu-id="4359f-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="4359f-239">*Что такое имя hello hello процесса, который hello сбора данных?*</span><span class="sxs-lookup"><span data-stu-id="4359f-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="4359f-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="4359f-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="4359f-241">*Сколько времени требуется для toobe данных собираются?*</span><span class="sxs-lookup"><span data-stu-id="4359f-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="4359f-242">время сбора данных на сервере hello Hello занимает примерно 1 час.</span><span class="sxs-lookup"><span data-stu-id="4359f-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="4359f-243">На серверах, которые имеют большое количество экземпляров или баз данных SQL, процесс сбора может занять больше времени.</span><span class="sxs-lookup"><span data-stu-id="4359f-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="4359f-244">*Какие типы данных собираются?*</span><span class="sxs-lookup"><span data-stu-id="4359f-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="4359f-245">собираются следующие типы данных Hello:</span><span class="sxs-lookup"><span data-stu-id="4359f-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="4359f-246">WMI</span><span class="sxs-lookup"><span data-stu-id="4359f-246">WMI</span></span>
  * <span data-ttu-id="4359f-247">Реестр</span><span class="sxs-lookup"><span data-stu-id="4359f-247">Registry</span></span>
  * <span data-ttu-id="4359f-248">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="4359f-248">Performance counters</span></span>
  * <span data-ttu-id="4359f-249">Динамические административные представления (DMV) SQL</span><span class="sxs-lookup"><span data-stu-id="4359f-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="4359f-250">*Есть ли способ tooconfigure время сбора данных?*</span><span class="sxs-lookup"><span data-stu-id="4359f-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="4359f-251">На данный момент нет.</span><span class="sxs-lookup"><span data-stu-id="4359f-251">Not at this time.</span></span>

<span data-ttu-id="4359f-252">*Почему у tooconfigure учетная запись запуска от имени*</span><span class="sxs-lookup"><span data-stu-id="4359f-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="4359f-253">Для SQL Server выполняется небольшое количество SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="4359f-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="4359f-254">Для них необходимо использовать toorun, учетная запись запуска от имени с tooSQL разрешения VIEW SERVER STATE.</span><span class="sxs-lookup"><span data-stu-id="4359f-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="4359f-255">Кроме того в порядке tooquery WMI, требуются учетные данные локального администратора.</span><span class="sxs-lookup"><span data-stu-id="4359f-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="4359f-256">*Почему отображаются только первые 10 рекомендаций hello?*</span><span class="sxs-lookup"><span data-stu-id="4359f-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="4359f-257">Вместо отображения полного списка задач, мы рекомендуем сконцентрироваться на рекомендациях hello приоритеты.</span><span class="sxs-lookup"><span data-stu-id="4359f-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="4359f-258">После этого станут доступны дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="4359f-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="4359f-259">Если вы предпочитаете toosee hello подробный список, можно просмотреть всех рекомендаций, с помощью поиска журналов OMS hello.</span><span class="sxs-lookup"><span data-stu-id="4359f-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="4359f-260">*Есть ли способ tooignore рекомендации?*</span><span class="sxs-lookup"><span data-stu-id="4359f-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="4359f-261">Да. См. раздел [Игнорирование рекомендаций](#ignore-recommendations) выше в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4359f-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4359f-262">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4359f-262">Next steps</span></span>
* <span data-ttu-id="4359f-263">[Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробные данные оценки SQL и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="4359f-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
