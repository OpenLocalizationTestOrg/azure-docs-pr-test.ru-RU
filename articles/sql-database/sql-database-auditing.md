---
title: "Приступая к работе с аудитом баз данных SQL Azure | Документация Майкрософт"
description: "Приступая к работе с аудитом баз данных SQL Azure"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="e56b2-103">Приступая к работе с аудитом базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="e56b2-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="e56b2-104">Аудит базы данных SQL Azure позволяет отслеживать события базы данных и записывать их в журнал аудита в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="e56b2-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="e56b2-105">Аудит также дает следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="e56b2-105">Auditing also:</span></span>

* <span data-ttu-id="e56b2-106">Аудит может помочь вам соблюсти требования нормативов, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="e56b2-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="e56b2-107">Средства аудита способствуют соблюдению стандартов соответствия, но не гарантируют их выполнение.</span><span class="sxs-lookup"><span data-stu-id="e56b2-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="e56b2-108">Дополнительную информацию о программах Azure, поддерживающих проверку соблюдения стандартов, см. в [Центре управления безопасностью Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="e56b2-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="e56b2-109"><a id="subheading-1"></a>Обзор аудита баз данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e56b2-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="e56b2-110">Используйте аудит базы данных SQL, чтобы выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e56b2-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="e56b2-111">**Сохранить** журнал аудита выбранных событий.</span><span class="sxs-lookup"><span data-stu-id="e56b2-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="e56b2-112">Вы можете указать, какие категории действий базы данных должны проходить аудит.</span><span class="sxs-lookup"><span data-stu-id="e56b2-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="e56b2-113">**Создавать отчеты** по действиям, производимым с базой данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-113">**Report** on database activity.</span></span> <span data-ttu-id="e56b2-114">Вы можете использовать предварительно настроенные отчеты и панель мониторинга для быстрого начала работы с отчетностью по действиям и событиям.</span><span class="sxs-lookup"><span data-stu-id="e56b2-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="e56b2-115">**Анализировать** отчеты.</span><span class="sxs-lookup"><span data-stu-id="e56b2-115">**Analyze** reports.</span></span> <span data-ttu-id="e56b2-116">Вы можете искать подозрительные события, необычную деятельность и тенденции.</span><span class="sxs-lookup"><span data-stu-id="e56b2-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="e56b2-117">Аудит можно настроить для различных типов категорий событий (см. раздел [Настройка аудита базы данных](#subheading-2)).</span><span class="sxs-lookup"><span data-stu-id="e56b2-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="e56b2-118">Журналы аудита записываются в хранилище BLOB-объектов Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e56b2-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="e56b2-119"><a id="subheading-8"></a>Определение политики аудита уровня сервера и базы данных</span><span class="sxs-lookup"><span data-stu-id="e56b2-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="e56b2-120">Политику аудита можно определить для конкретной базы данных или как политику сервера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e56b2-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="e56b2-121">Политика сервера применяется ко всем существующим и новым базам данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="e56b2-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="e56b2-122">Если включен *аудит больших двоичных объектов для сервера*, он *всегда применяется к базе данных* (т. е. выполняется аудит базы данных). Это поведение не зависит от параметров аудита базы данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="e56b2-123">Включение аудита больших двоичных объектов для базы данных (кроме его включения для сервера), *не* приведет к переопределению или изменению настроек аудита больших двоичных объектов для сервера.</span><span class="sxs-lookup"><span data-stu-id="e56b2-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="e56b2-124">Оба аудита будут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="e56b2-124">Both audits will exist side by side.</span></span> <span data-ttu-id="e56b2-125">Таким образом, аудит базы данных будет выполняться дважды: один раз в соответствии с политикой сервера и еще раз в соответствии с политикой базы данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="e56b2-126">Не устанавливайте политику аудита больших двоичных объектов одновременно для сервера и базы данных, за исключением следующих случаев.</span><span class="sxs-lookup"><span data-stu-id="e56b2-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="e56b2-127">Если для определенной базы данных нужно использовать другую *учетную запись хранения* или другой *срок хранения*.</span><span class="sxs-lookup"><span data-stu-id="e56b2-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="e56b2-128">Нужно провести аудит типов событий или категорий для конкретной базы данных, которые отличаются от типов событий и категорий, проверенных для остальной части базы данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="e56b2-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="e56b2-129">Например, может потребоваться выполнить аудит вставки данных в таблицу только для конкретной базы данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="e56b2-130">Во всех остальных случаях мы рекомендуем включать аудит больших двоичных объектов только на уровне сервера, а на уровне баз данных отключить все параметры аудита для всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="e56b2-131"><a id="subheading-2"></a>Настройка аудита базы данных</span><span class="sxs-lookup"><span data-stu-id="e56b2-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="e56b2-132">В следующем разделе описывается настройка аудита на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e56b2-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="e56b2-133">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e56b2-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e56b2-134">Перейдите в колонку **параметров** базы данных SQL или SQL Server, где нужно выполнить аудит.</span><span class="sxs-lookup"><span data-stu-id="e56b2-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="e56b2-135">В колонке **Параметры** выберите **Аудит и обнаружение угроз**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="e56b2-136"><a id="auditing-screenshot"></a> ![Область навигации][1]</span><span class="sxs-lookup"><span data-stu-id="e56b2-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="e56b2-137">Если вы предпочитаете настроить политику аудита сервера (которая будет применяться ко всем имеющимся и новым базам данных на этом сервере), можно выбрать ссылку **просмотра параметров сервера** в колонке аудита базы данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="e56b2-138">Вы можете затем просмотреть или изменить параметры аудита сервера.</span><span class="sxs-lookup"><span data-stu-id="e56b2-138">You can then view or modify the server auditing settings.</span></span>

    ![Область навигации][2]
4. <span data-ttu-id="e56b2-140">Если вы предпочитаете включить аудит больших двоичных объектов на уровне базы данных (кроме или вместо аудита на уровне сервера), тогда для параметра **Аудит** выберите значение **Вкл.**, а для параметра **Тип аудита** — **Большой двоичный объект**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="e56b2-141">Если включен аудит больших двоичных объектов сервера, настроенный аудит для базы данных будет существовать параллельно с ним.</span><span class="sxs-lookup"><span data-stu-id="e56b2-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Область навигации][3]
5. <span data-ttu-id="e56b2-143">Выберите **Сведения о хранилище**, чтобы открыть колонку **Хранилище журналов аудита**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="e56b2-144">Выберите учетную запись хранения Azure, в которой будут сохраняться журналы, и срок хранения, по истечении которого старые журналы будут удалены.</span><span class="sxs-lookup"><span data-stu-id="e56b2-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="e56b2-145">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="e56b2-146">Чтобы в полной мере воспользоваться возможностями шаблонов отчетов об аудите, используйте одну и ту же учетную запись хранения для всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="e56b2-147"><a id="storage-screenshot"></a> ![Область навигации][4]</span><span class="sxs-lookup"><span data-stu-id="e56b2-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="e56b2-148">Настроить события аудита можно с помощью PowerShell или REST API.</span><span class="sxs-lookup"><span data-stu-id="e56b2-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="e56b2-149">Дополнительные сведения см. в разделе [Автоматизация (PowerShell или REST API)](#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="e56b2-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="e56b2-150">После настройки параметров аудита можно включить новую функцию обнаружения угроз и настроить адреса электронной почты для получения предупреждений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="e56b2-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="e56b2-151">Использование функции обнаружения угроз позволяет настроить упреждающие оповещения об аномальной активности в базах данных, которая может указывать на потенциальные угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="e56b2-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="e56b2-152">Дополнительные сведения см. в статье [Обнаружение угроз для базы данных SQL](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e56b2-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="e56b2-153">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-153">Click **Save**.</span></span>





## <span data-ttu-id="e56b2-154"><a id="subheading-3"></a>Анализ журналов и отчетов аудита</span><span class="sxs-lookup"><span data-stu-id="e56b2-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="e56b2-155">Журналы аудита объединяются в учетной записи хранения Azure, выбранной на этапе настройки.</span><span class="sxs-lookup"><span data-stu-id="e56b2-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="e56b2-156">Журналы аудита можно просматривать с помощью таких инструментов, как [обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e56b2-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="e56b2-157">Журналы аудита больших двоичных объектов сохраняются в виде коллекции файлов больших двоичных объектов в контейнере **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="e56b2-158">Дополнительные сведения об иерархии папки для хранения журналов аудита больших двоичных объектов, соглашении об именовании больших двоичных объектов и формате журнала см. в [документации по формату журнала аудита (скачать DOC-файл)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="e56b2-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="e56b2-159">Просмотреть журналы аудита больших двоичных объектов можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="e56b2-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="e56b2-160">Используйте [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e56b2-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="e56b2-161">Откройте соответствующую базу данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-161">Open the relevant database.</span></span> <span data-ttu-id="e56b2-162">В верхней области колонки **Auditing & Threat detection** (Аудит и обнаружение угроз) щелкните **Ознакомиться с журналами аудита**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Область навигации][7]

    <span data-ttu-id="e56b2-164">Откроется колонка **Записи аудита**, в которой вы сможете просматривать журналы.</span><span class="sxs-lookup"><span data-stu-id="e56b2-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="e56b2-165">Для просмотра записей за определенную дату щелкните **Фильтр** в верхней области колонки **записей аудита**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="e56b2-166">Вы можете переключаться между записями аудита, созданными политиками аудита для сервера и для базы данных.</span><span class="sxs-lookup"><span data-stu-id="e56b2-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Область навигации][8]

* <span data-ttu-id="e56b2-168">Используйте системную функцию **sys.fn_get_audit_file** (T-SQL), чтобы вернуть данные журнала аудита в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="e56b2-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="e56b2-169">Дополнительные сведения об использовании этой функции см. в статье [sys.fn_get_audit_file (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="e56b2-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="e56b2-170">Используйте **объединение файлов аудита** в SQL Server Management Studio (начиная с SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="e56b2-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="e56b2-171">В меню SSMS выберите **Файл** > **Открыть** > **Объединение файлов аудита**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Область навигации][9]
    2. <span data-ttu-id="e56b2-173">Откроется диалоговое окно **Добавление файлов аудита**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="e56b2-174">Выберите один из способов **добавления**. Вы можете использовать объединение файлов аудита из локального диска или импортировать их из хранилища Azure (вам потребуется предоставить сведения о хранилище Azure и ключ учетной записи).</span><span class="sxs-lookup"><span data-stu-id="e56b2-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="e56b2-175">После добавления всех файлов для слияния нажмите кнопку **OK** для завершения операции слияния.</span><span class="sxs-lookup"><span data-stu-id="e56b2-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="e56b2-176">Объединенный файл откроется в SSMS, где вы сможете его просмотреть и проанализировать, а также экспортировать в XEL- или CSV-файл или в таблицу.</span><span class="sxs-lookup"><span data-stu-id="e56b2-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="e56b2-177">Используйте созданное [приложение синхронизации](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration).</span><span class="sxs-lookup"><span data-stu-id="e56b2-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="e56b2-178">Оно работает в Azure и использует общие API-интерфейсы службы Log Analytics для Operations Management Suite (OMS) для передачи журналов аудита SQL в OMS.</span><span class="sxs-lookup"><span data-stu-id="e56b2-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="e56b2-179">Приложение синхронизации отправляет журналы аудита SQL в OMS Log Analytics для использования через панель мониторинга OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e56b2-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="e56b2-180">Используйте Power BI.</span><span class="sxs-lookup"><span data-stu-id="e56b2-180">Use Power BI.</span></span> <span data-ttu-id="e56b2-181">Вы можете просматривать и анализировать данные журнала аудита в Power BI.</span><span class="sxs-lookup"><span data-stu-id="e56b2-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="e56b2-182">Вы можете узнать больше о [Power BI, а также скачать шаблон](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="e56b2-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="e56b2-183">Скачайте файлы журналов из контейнера больших двоичных объектов хранилища Azure из портала или с помощью [обозревателя хранилища Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e56b2-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="e56b2-184">После загрузки файла дважды щелкните по нему, чтобы открыть, просмотреть и проанализировать файл в среде SSMS.</span><span class="sxs-lookup"><span data-stu-id="e56b2-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="e56b2-185">Вы также можете загрузить одновременно несколько файлов через обозреватель хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e56b2-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="e56b2-186">Щелкните правой кнопкой мыши конкретную вложенную папку (например, вложенную папку, содержащую все файлы журналов для определенной даты), а затем выберите **Сохранить как**, чтобы сохранить ее в локальной папке.</span><span class="sxs-lookup"><span data-stu-id="e56b2-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="e56b2-187">Дополнительные методы</span><span class="sxs-lookup"><span data-stu-id="e56b2-187">Additional methods:</span></span>
   * <span data-ttu-id="e56b2-188">После загрузки нескольких файлов (или вложенной папки, содержащей файлы журнала за целый день, как описано в предыдущем пункте в этом списке), можно объединить их локально, как описано в приведенных выше инструкциях по объединению файлов аудита в SSMS.</span><span class="sxs-lookup"><span data-stu-id="e56b2-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="e56b2-189">Чтобы просмотреть журналы аудита больших двоичных объектов программным способом:</span><span class="sxs-lookup"><span data-stu-id="e56b2-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="e56b2-190">Используйте библиотеку C# [для считывания расширенных событий](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/).</span><span class="sxs-lookup"><span data-stu-id="e56b2-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="e56b2-191">Используйте [запросы к файлам расширенных событий](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e56b2-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="e56b2-192"><a id="subheading-5"></a>Рекомендации для рабочей среды</span><span class="sxs-lookup"><span data-stu-id="e56b2-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="e56b2-193"><a id="subheading-6">Аудит геореплицированных баз данных</a></span><span class="sxs-lookup"><span data-stu-id="e56b2-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="e56b2-194">При использовании географически реплицированных баз данных можно настроить аудит для базы данных-источника, базы данных-получателя или для обеих баз данных в зависимости от типа аудита.</span><span class="sxs-lookup"><span data-stu-id="e56b2-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="e56b2-195">Следуйте инструкциям ниже (помните, что аудит больших двоичных объектов можно включить или отключить только в параметрах аудита базы данных-источника):</span><span class="sxs-lookup"><span data-stu-id="e56b2-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="e56b2-196">**База данных-источник**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-196">**Primary database**.</span></span> <span data-ttu-id="e56b2-197">Включите аудит больших двоичных объектов на сервере или в базе данных, как описано в разделе [настройки аудита базы данных](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="e56b2-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="e56b2-198">**База данных-получатель**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-198">**Secondary database**.</span></span> <span data-ttu-id="e56b2-199">Включите аудит больших двоичных объектов в базе данных-источнике, как описано в разделе [настройки аудита базы данных](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="e56b2-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="e56b2-200">Его необходимо включить для самой *базы данных-источника*, а не для сервера.</span><span class="sxs-lookup"><span data-stu-id="e56b2-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="e56b2-201">После включения аудита больших двоичных объектов в базе данных-источнике он станет доступным в базе данных-получателе.</span><span class="sxs-lookup"><span data-stu-id="e56b2-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="e56b2-202">По умолчанию настройки хранилища для базы данных-получателя будут совпадать с настройками для базы данных-источника, что приведет к появлению трафика между регионами.</span><span class="sxs-lookup"><span data-stu-id="e56b2-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="e56b2-203">Этого можно избежать, включив аудит больших двоичных объектов на сервере-получателе, а также настроив локальное хранилище в параметрах хранилища сервера-получателя.</span><span class="sxs-lookup"><span data-stu-id="e56b2-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="e56b2-204">Это приведет к переопределению расположения хранилища для базы данных-получателя, и каждая база данных сохранит свои журналы аудита в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="e56b2-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="e56b2-205"><a id="subheading-6">Повторное создание ключа к хранилищу данных</a></span><span class="sxs-lookup"><span data-stu-id="e56b2-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="e56b2-206">Обычно в рабочей среде приходится периодически обновлять ключи хранилища.</span><span class="sxs-lookup"><span data-stu-id="e56b2-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="e56b2-207">При обновлении ключей необходимо повторно сохранить политику аудита.</span><span class="sxs-lookup"><span data-stu-id="e56b2-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="e56b2-208">Процесс таков:</span><span class="sxs-lookup"><span data-stu-id="e56b2-208">The process is as follows:</span></span>

1. <span data-ttu-id="e56b2-209">Откройте колонку **Сведения о хранилище**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="e56b2-210">В поле **Ключ доступа к хранилищу** выберите **Вторичный**, а затем нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="e56b2-211">Затем щелкните **Сохранить** в верхней области колонки настройки аудита.</span><span class="sxs-lookup"><span data-stu-id="e56b2-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Область навигации][5]
2. <span data-ttu-id="e56b2-213">Перейдите в колонку конфигурации хранилища и повторно создайте первичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="e56b2-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Область навигации][6]
3. <span data-ttu-id="e56b2-215">Вернитесь в колонку настройки аудита, измените значение ключа доступа к хранилищу с вторичного на первичный, затем нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="e56b2-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="e56b2-216">Затем щелкните **Сохранить** в верхней области колонки настройки аудита.</span><span class="sxs-lookup"><span data-stu-id="e56b2-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="e56b2-217">Вернитесь в колонку настройки хранилища и повторно создайте ключ доступа получателя (для подготовки к следующему циклу обновления ключей).</span><span class="sxs-lookup"><span data-stu-id="e56b2-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="e56b2-218"><a id="subheading-7"></a>Автоматизация (PowerShell или REST API)</span><span class="sxs-lookup"><span data-stu-id="e56b2-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="e56b2-219">Аудит в базе данных SQL Azure также можно настроить с помощью следующих средств автоматизации:</span><span class="sxs-lookup"><span data-stu-id="e56b2-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="e56b2-220">**Командлеты PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e56b2-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="e56b2-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="e56b2-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="e56b2-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="e56b2-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="e56b2-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="e56b2-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="e56b2-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="e56b2-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="e56b2-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="e56b2-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="e56b2-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="e56b2-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="e56b2-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="e56b2-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="e56b2-228">Пример сценария см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e56b2-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="e56b2-229">**REST API — аудит больших двоичных объектов**:</span><span class="sxs-lookup"><span data-stu-id="e56b2-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="e56b2-230">Создание или обновление политики аудита BLOB-объектов базы данных</span><span class="sxs-lookup"><span data-stu-id="e56b2-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="e56b2-231">Создание или обновление политики аудита BLOB-объектов сервера</span><span class="sxs-lookup"><span data-stu-id="e56b2-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="e56b2-232">Получение политики аудита BLOB-объектов базы данных</span><span class="sxs-lookup"><span data-stu-id="e56b2-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="e56b2-233">Получение политики аудита BLOB-объектов сервера</span><span class="sxs-lookup"><span data-stu-id="e56b2-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="e56b2-234">Получение результата операции аудита для BLOB-объектов сервера</span><span class="sxs-lookup"><span data-stu-id="e56b2-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
