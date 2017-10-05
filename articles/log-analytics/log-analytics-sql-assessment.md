---
title: "Оптимизация среды SQL Server с помощью Azure Log Analytics | Документация Майкрософт"
description: "Решение оценки SQL в Azure Log Analytics можно использовать для оценки риска и работоспособности среды SQL Server с постоянной периодичностью."
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
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="d9f7e-103">Оптимизация среды SQL Server с помощью решения оценки SQL в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d9f7e-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![Символ оценки SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="d9f7e-105">Решения оценки SQL можно использовать для оценки риска и работоспособности серверной среды с постоянной периодичностью.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="d9f7e-106">Эта статья поможет вам установить решение таким образом, чтобы в случае проблем вы могли предпринять корректирующие меры.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="d9f7e-107">Это решение предоставляет приоритетный список рекомендаций, относящихся к развернутой серверной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="d9f7e-108">Рекомендации сгруппированы в шесть приоритетных областей, помогающих быстро оценить риски и принять корректирующие меры.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="d9f7e-109">В основу предлагаемых рекомендаций положены знания и опыт, приобретенные специалистами Майкрософт в результате многочисленных посещений клиентов.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="d9f7e-110">Каждая рекомендация является определенным руководством, поясняющим важность проблемы и приводящим действия по реализации предложенных изменений.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="d9f7e-111">Можно выбрать приоритетные области, наиболее важные для организации, и отслеживать выполнение задач по формированию работоспособной и свободной от рисков среды.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="d9f7e-112">После добавления решения и завершения оценки сводная информация по приоритетным областям отображается на панели мониторинга **Оценка SQL** для инфраструктуры среды.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="d9f7e-113">В следующих разделах описано, как использовать информацию на панели мониторинга **Оценка SQL** , где можно увидеть и выполнить действия, рекомендованные для вашей инфраструктуры сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![image of SQL Assessment tile](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![image of SQL Assessment dashboard](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="d9f7e-116">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="d9f7e-116">Installing and configuring the solution</span></span>
<span data-ttu-id="d9f7e-117">Оценка SQL поддерживает выпуски Standard, Developer и Enterprise SQL Server — все текущие поддерживаемые версии.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="d9f7e-118">Для установки и настройки решений используйте указанные ниже данные.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="d9f7e-119">Агенты должны устанавливаться на серверах, на которых установлен SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="d9f7e-120">Для решения оценки SQL на каждом компьютере с агентом OMS должна быть установлена поддерживаемая версия платформы .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="d9f7e-121">Чтобы установить решение, при использовании портала Azure пользователь должен быть администратором или участником подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="d9f7e-122">Кроме того, пользователю должна быть назначена роль участника или администратора рабочей области OMS на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="d9f7e-123">При использовании агента Operations Manager с решением оценки SQL необходимо использовать учетную запись запуска от имени Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="d9f7e-124">Дополнительные сведения см. в разделе ниже [Учетные записи запуска от имени в Operations Manager для службы OMS](#operations-manager-run-as-accounts-for-oms).</span><span class="sxs-lookup"><span data-stu-id="d9f7e-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d9f7e-125">Агент MMA не поддерживает учетные записи запуска от имени Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="d9f7e-126">Решение оценки SQL необходимо добавить в рабочую область OMS, как описано в разделе [Добавление решений Log Analytics из коллекции решений](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d9f7e-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="d9f7e-127">Дополнительная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="d9f7e-128">После добавления решения на серверы с агентами добавляется файл AdvisorAssessment.exe.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="d9f7e-129">Данные конфигурации считываются и отправляются на обработку в службу OMS в облаке.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="d9f7e-130">К полученным данным применяется логика и облачная служба записывает данные.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="d9f7e-131">Сведения о сборе данных по оценке SQL</span><span class="sxs-lookup"><span data-stu-id="d9f7e-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="d9f7e-132">Оценка SQL собирает данные WMI, данные реестра, данные производительности и результаты динамического административного представления SQL Server с помощью включенных агентов.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="d9f7e-133">В следующей таблице показаны методы сбора данных для агентов, необходимость Operations Manager (SCOM) и периодичность сбора данных агентом.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="d9f7e-134">платформа</span><span class="sxs-lookup"><span data-stu-id="d9f7e-134">platform</span></span> | <span data-ttu-id="d9f7e-135">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="d9f7e-135">Direct Agent</span></span> | <span data-ttu-id="d9f7e-136">Агент SCOM</span><span class="sxs-lookup"><span data-stu-id="d9f7e-136">SCOM agent</span></span> | <span data-ttu-id="d9f7e-137">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="d9f7e-137">Azure Storage</span></span> | <span data-ttu-id="d9f7e-138">Нужен ли SCOM?</span><span class="sxs-lookup"><span data-stu-id="d9f7e-138">SCOM required?</span></span> | <span data-ttu-id="d9f7e-139">Отправка данных агента SCOM через группу управления</span><span class="sxs-lookup"><span data-stu-id="d9f7e-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="d9f7e-140">частота сбора</span><span class="sxs-lookup"><span data-stu-id="d9f7e-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d9f7e-141">Windows</span><span class="sxs-lookup"><span data-stu-id="d9f7e-141">Windows</span></span> | <span data-ttu-id="d9f7e-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="d9f7e-142">&#8226;</span></span> | <span data-ttu-id="d9f7e-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="d9f7e-143">&#8226;</span></span> |  |  | <span data-ttu-id="d9f7e-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="d9f7e-144">&#8226;</span></span> |<span data-ttu-id="d9f7e-145">7 дней</span><span class="sxs-lookup"><span data-stu-id="d9f7e-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="d9f7e-146">Учетные записи запуска от имени в Operations Manager для службы OMS</span><span class="sxs-lookup"><span data-stu-id="d9f7e-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="d9f7e-147">Log Analytics в OMS использует агент Operations Manager и группу управления для сбора и отправки данных в службу OMS.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="d9f7e-148">С целью предоставления ценных услуг служба OMS строится на пакетах управления для рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="d9f7e-149">Каждой рабочей нагрузке требуются права, относящиеся к конкретным рабочим нагрузкам, для запуска пакетов управления в другом контексте безопасности, например в учетной записи домена.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="d9f7e-150">Необходимо предоставить учетные данные, настроив учетную запись запуска от имени для Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="d9f7e-151">Для настройки учетной записи запуска от имени Operations Manager для оценки SQL используйте указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="d9f7e-152">Настройка учетной записи запуска от имени для оценки SQL</span><span class="sxs-lookup"><span data-stu-id="d9f7e-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="d9f7e-153">Если пакет управления SQL Server уже используется, следует использовать эту учетную запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="d9f7e-154">Настройка учетной записи SQL запуска от имени в консоли управления</span><span class="sxs-lookup"><span data-stu-id="d9f7e-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="d9f7e-155">Если используется прямой агент OMS, а не агент SCOM, то пакет управления всегда выполняется в контексте безопасности учетной записи Local System.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="d9f7e-156">Пропустите шаги 1-5, описанные ниже, и выполните пример T-SQL или Powershell, указав в качестве имени пользователя NT AUTHORITY\SYSTEM.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="d9f7e-157">В Operations Manager откройте консоль управления и щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="d9f7e-158">В разделе **Настройка запуска от имени** щелкните **Профили** и откройте **Профиль запуска от имени для оценки SQL в OMS**.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="d9f7e-159">На странице **Учетные записи запуска от имени** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="d9f7e-160">Выберите учетную запись Windows запуска от имени, которая содержит учетные данные, необходимые для SQL Server, или нажмите кнопку **Создать** для ее создания.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d9f7e-161">Тип учетной записи «Запуск от имени» должен быть указан как Windows.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="d9f7e-162">Учетная запись запуска от имени также должна входить в группу локальных администраторов на всех серверах Windows Server, на которых размещены экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="d9f7e-163">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-163">Click **Save**.</span></span>
6. <span data-ttu-id="d9f7e-164">Измените, а затем выполните следующий пример T-SQL на каждом экземпляре SQL Server, чтобы предоставить минимальные разрешения, необходимые учетной записи запуска от имени для выполнения оценки SQL.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="d9f7e-165">Но это не требуется делать в том случае, если учетная запись запуска от имени уже является частью серверной роли sysadmin в экземплярах SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="d9f7e-166">Настройка учетной записи SQL запуска от имени с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9f7e-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="d9f7e-167">Откройте окно PowerShell и выполните следующий скрипт после его обновления с собственными данными.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="d9f7e-168">Основные сведения о приоритизации рекомендаций</span><span class="sxs-lookup"><span data-stu-id="d9f7e-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="d9f7e-169">Каждая рекомендация получает взвешенное значение, определяющее относительную важность рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="d9f7e-170">Отображаются только десять наиболее важных рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="d9f7e-171">Процесс вычисления взвешенного значения</span><span class="sxs-lookup"><span data-stu-id="d9f7e-171">How weights are calculated</span></span>
<span data-ttu-id="d9f7e-172">Взвешенные значения являются статистическими значениями, основанными на трех ключевых факторах.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="d9f7e-173">*Вероятность* возникновения проблемы.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="d9f7e-174">Более высокие значения вероятности приравниваются к более высокой общей оценке для рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="d9f7e-175">*Влияние* на работу организации, если она является причиной проблемы.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="d9f7e-176">Более высокая степень влияния приравнивается к более высокой общей оценке для рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="d9f7e-177">*Усилия* , необходимые для реализации рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="d9f7e-178">Более высокое значение усилий приравнивается к меньшей общей оценке рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="d9f7e-179">Взвешенное значение для каждой рекомендации выражается в процентах от общей оценки, доступной для каждой приоритетной области.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="d9f7e-180">Например, если рекомендация в области обеспечения безопасности и соответствия требованиям имеет показатель 5 %, реализация этой рекомендации увеличит общую оценку в этой области на 5 %.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="d9f7e-181">Приоритетные области</span><span class="sxs-lookup"><span data-stu-id="d9f7e-181">Focus areas</span></span>
<span data-ttu-id="d9f7e-182">**Безопасность и соответствие требованиям**. В этой области содержатся рекомендации в отношении возможных угроз, нарушений безопасности и корпоративных политик, а также технические, юридические и нормативные требования.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="d9f7e-183">**Доступность и непрерывность бизнес-процессов**. Эта область содержит рекомендации в отношении доступности служб, устойчивости инфраструктуры и защиты бизнеса.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="d9f7e-184">**Производительность и масштабируемость**. В этой области содержатся рекомендации, которые помогут ИТ-инфраструктуре вашей организации расти, обеспечат соответствие ИТ-среды текущим требованиям к производительности и позволят ей адаптироваться под новые требования к инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="d9f7e-185">**Обновление, перенос и развертывание**. Эта область содержит рекомендации, которые помогут вам обновить, перенести и развернуть SQL Server в существующую инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="d9f7e-186">**Операции и мониторинг**. В этой области содержатся рекомендации, которые позволят оптимизировать ИТ-операции, реализовать программу профилактического обслуживания и повысить эффективность бизнеса.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="d9f7e-187">**Управление изменениями и конфигурациями**. Эта область содержит рекомендации, которые помогут защитить повседневные операции, предотвратить негативное воздействие изменений на инфраструктуру, создать процедуры управления изменениями, а также отслеживать конфигурации системы и проводить их аудит.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="d9f7e-188">Следует ли стремиться к показателю 100 % в каждой приоритетной области?</span><span class="sxs-lookup"><span data-stu-id="d9f7e-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="d9f7e-189">Не обязательно.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-189">Not necessarily.</span></span> <span data-ttu-id="d9f7e-190">В основу предлагаемых рекомендаций положены знания и опыт, приобретенные специалистами Майкрософт в результате многочисленных посещений клиентов.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="d9f7e-191">Однако не существует двух одинаковых серверных инфраструктур, и конкретные рекомендации могут быть применимы к вам в большей или меньшей степени.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="d9f7e-192">Например, некоторые рекомендации по обеспечению безопасности могут быть менее значимыми, если виртуальные машины в организации не подключены к Интернету.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="d9f7e-193">Некоторые рекомендации о доступности могут иметь менее важное значение для служб, которые обеспечивают сбор низкоприоритетных данных.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="d9f7e-194">Проблемы, которые важны для зрелой организации, могут быть не так важны для начинающей компании.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="d9f7e-195">Можно определить приоритетные области и затем отследить изменение оценок с течением времени.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="d9f7e-196">В каждой рекомендации указано, почему она важна.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="d9f7e-197">Их следует использовать, чтобы определить целесообразность реализации рекомендации с учетом характера ИТ-служб и бизнес-потребностей организации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="d9f7e-198">Использование рекомендаций по оцениваемой приоритетной области</span><span class="sxs-lookup"><span data-stu-id="d9f7e-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="d9f7e-199">Чтобы использовать решение оценки в OMS, его необходимо установить.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="d9f7e-200">Дополнительные сведения об установке решений см. в статье [Добавление решений Log Analytics из коллекции решений](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d9f7e-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="d9f7e-201">Когда решение будет установлено, вы сможете просматривать сводные рекомендации с помощью плитки "Оценка SQL" на странице обзора в OMS.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="d9f7e-202">Вы можете посматривать сводку оценок соответствия для инфраструктуры, а затем глубже изучить рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="d9f7e-203">Просмотр рекомендаций для приоритетной области и выполнение действий по исправлению</span><span class="sxs-lookup"><span data-stu-id="d9f7e-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="d9f7e-204">На странице **Обзор** щелкните элемент **Оценка SQL**.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="d9f7e-205">На странице **Оценка SQL** просмотрите сводные данные в одной из колонок приоритетной области, а затем щелкните одну колонку, чтобы просмотреть рекомендации для соответствующей области.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="d9f7e-206">На всех страницах интересующей области можно просматривать приоритетные рекомендации для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="d9f7e-207">Щелкните рекомендацию в разделе **Затронутые объекты** , чтобы просмотреть сведения о причинах возникновения этой рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="d9f7e-208">![Изображение с рекомендациями оценки SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="d9f7e-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="d9f7e-209">В разделе **Предложенные действия**представлены действия по исправлению, которые вы можете предпринять.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="d9f7e-210">Когда проблема с этим элементом будет устранена, последующие оценки будут указывать, что рекомендованные действия были выполнены, и тогда оценка соответствия возрастет.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="d9f7e-211">Исправленные элементы отображаются как **Прошедшие проверку объекты**.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="d9f7e-212">Игнорирование рекомендаций</span><span class="sxs-lookup"><span data-stu-id="d9f7e-212">Ignore recommendations</span></span>
<span data-ttu-id="d9f7e-213">Если вы хотите проигнорировать какие-то рекомендации, создайте текстовый файл, который OMS будет использовать для того, чтобы убрать рекомендации из результатов оценки.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="d9f7e-214">Указание рекомендаций, которые нужно проигнорировать</span><span class="sxs-lookup"><span data-stu-id="d9f7e-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="d9f7e-215">Войдите в рабочую область и откройте поиск по журналам.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="d9f7e-216">Выполните следующий запрос, чтобы получить список рекомендаций, не выполненных на компьютерах в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="d9f7e-217">Вот снимок экрана с запросом на поиск по журналам: ![невыполненные рекомендации](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png).</span><span class="sxs-lookup"><span data-stu-id="d9f7e-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="d9f7e-218">Выберите рекомендации, которые нужно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="d9f7e-219">Эти значения будут использоваться для параметра RecommendationId в следующей процедуре.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="d9f7e-220">Создание и использование текстового файла IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="d9f7e-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="d9f7e-221">Создайте файл с именем IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="d9f7e-222">Вставьте или введите значение RecommendationId для каждой рекомендации, которую служба OMS должна игнорировать, в отдельной строке, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="d9f7e-223">Поместите файл в следующую папку на каждом компьютере, где OMS должен проигнорировать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="d9f7e-224">На компьютерах с Microsoft Monitoring Agent (подключенных напрямую или через Operations Manager): *системный диск*:\Program Files\Microsoft Monitoring Agent\Agent.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="d9f7e-225">На сервере управления Operations Manager: *системный диск*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="d9f7e-226">Контроль игнорирования рекомендаций</span><span class="sxs-lookup"><span data-stu-id="d9f7e-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="d9f7e-227">После выполнения следующей плановой оценки (по умолчанию выполняется раз в семь дней) указанные рекомендации помечаются как игнорируемые и больше не отображаются на панели мониторинга оценки.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="d9f7e-228">Для получения списка всех игнорируемых рекомендаций можно использовать следующие запросы поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="d9f7e-229">Если вы решите позже просмотреть игнорируемые рекомендации, удалите все файлы IgnoreRecommendations.txt или RecommendationIDs можно удалить из них.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="d9f7e-230">Часто задаваемые вопросы по решениям оценки SQL</span><span class="sxs-lookup"><span data-stu-id="d9f7e-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="d9f7e-231">*Как часто выполняется оценка?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="d9f7e-232">Оценка выполняется каждые 7 дней.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="d9f7e-233">*Есть ли способ настроить частоту оценки?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="d9f7e-234">На данный момент нет.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-234">Not at this time.</span></span>

<span data-ttu-id="d9f7e-235">*Если после добавления решения оценки SQL будет обнаружен другой сервер, оценивается ли он?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="d9f7e-236">Да, после обнаружения он оценивается каждые 7 дней.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="d9f7e-237">*Если сервер выведен из эксплуатации, он будет удален из оценки?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="d9f7e-238">Если сервер не отправляет данные в течение 3 недель, то он удаляется.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="d9f7e-239">*Как называется процесс, который собирает данные?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="d9f7e-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="d9f7e-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="d9f7e-241">*Сколько времени требуется для сбора данных?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="d9f7e-242">Время сбора данных на сервере занимает примерно 1 час.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="d9f7e-243">На серверах, которые имеют большое количество экземпляров или баз данных SQL, процесс сбора может занять больше времени.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="d9f7e-244">*Какие типы данных собираются?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="d9f7e-245">Собираются следующие типы данных:</span><span class="sxs-lookup"><span data-stu-id="d9f7e-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="d9f7e-246">WMI</span><span class="sxs-lookup"><span data-stu-id="d9f7e-246">WMI</span></span>
  * <span data-ttu-id="d9f7e-247">Реестр</span><span class="sxs-lookup"><span data-stu-id="d9f7e-247">Registry</span></span>
  * <span data-ttu-id="d9f7e-248">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="d9f7e-248">Performance counters</span></span>
  * <span data-ttu-id="d9f7e-249">Динамические административные представления (DMV) SQL</span><span class="sxs-lookup"><span data-stu-id="d9f7e-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="d9f7e-250">*Можно ли настроить время сбора данных?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="d9f7e-251">На данный момент нет.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-251">Not at this time.</span></span>

<span data-ttu-id="d9f7e-252">*Почему необходимо настроить учетную запись «Запуск от имени»?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="d9f7e-253">Для SQL Server выполняется небольшое количество SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="d9f7e-254">Для того чтобы их можно было выполнить, необходимо использовать учетную запись выполнения от имени с разрешениями VIEW SERVER STATE для SQL.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="d9f7e-255">Кроме того, чтобы выполнять запросы к WMI, потребуются учетные данные локального администратора.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="d9f7e-256">*Почему отображаются только первые 10 рекомендаций?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="d9f7e-257">Вместо отображения полного списка задач мы рекомендуем сконцентрироваться на приоритетных рекомендациях.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="d9f7e-258">После этого станут доступны дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="d9f7e-259">Если вы хотите просмотреть весь список, используйте функцию поиска по журналам OMS.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="d9f7e-260">*Можно ли игнорировать рекомендации?*</span><span class="sxs-lookup"><span data-stu-id="d9f7e-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="d9f7e-261">Да. См. раздел [Игнорирование рекомендаций](#ignore-recommendations) выше в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9f7e-262">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9f7e-262">Next steps</span></span>
* <span data-ttu-id="d9f7e-263">[поиск в журналах](log-analytics-log-searches.md) , чтобы просмотреть подробные данные оценки SQL и соответствующие рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9f7e-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
