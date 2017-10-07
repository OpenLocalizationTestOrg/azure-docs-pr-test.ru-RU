---
title: "aaaGet работы с аудитом базы данных Azure SQL | Документы Microsoft"
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
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="bed40-103">Приступая к работе с аудитом базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="bed40-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="bed40-104">Аудита базы данных Azure отслеживает события базы данных и записывает их tooan журнал аудита вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bed40-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="bed40-105">Аудит также дает следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="bed40-105">Auditing also:</span></span>

* <span data-ttu-id="bed40-106">Аудит может помочь вам соблюсти требования нормативов, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="bed40-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="bed40-107">Позволяет и обеспечивает соблюдение стандартов toocompliance, несмотря на то, что он не гарантирует соответствие.</span><span class="sxs-lookup"><span data-stu-id="bed40-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="bed40-108">Дополнительные сведения о Azure программы, соответствие стандартам поддержки, см. в разделе hello [Центр управления безопасностью Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="bed40-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="bed40-109"><a id="subheading-1"></a>Обзор аудита баз данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bed40-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="bed40-110">Используйте аудит базы данных SQL, чтобы выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bed40-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="bed40-111">**Сохранить** журнал аудита выбранных событий.</span><span class="sxs-lookup"><span data-stu-id="bed40-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="bed40-112">Можно определить категории аудита toobe действия базы данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="bed40-113">**Создавать отчеты** по действиям, производимым с базой данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-113">**Report** on database activity.</span></span> <span data-ttu-id="bed40-114">Можно использовать готовые отчеты и панели мониторинга tooget, быстро начать работу с действия и уведомления о событиях.</span><span class="sxs-lookup"><span data-stu-id="bed40-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="bed40-115">**Анализировать** отчеты.</span><span class="sxs-lookup"><span data-stu-id="bed40-115">**Analyze** reports.</span></span> <span data-ttu-id="bed40-116">Вы можете искать подозрительные события, необычную деятельность и тенденции.</span><span class="sxs-lookup"><span data-stu-id="bed40-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="bed40-117">Можно настроить аудит для различных категорий событий, как описано в hello [настройки аудита для базы данных](#subheading-2) раздела.</span><span class="sxs-lookup"><span data-stu-id="bed40-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="bed40-118">Журналы аудита записываются tooAzure хранилища больших двоичных объектов в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="bed40-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="bed40-119"><a id="subheading-8"></a>Определение политики аудита уровня сервера и базы данных</span><span class="sxs-lookup"><span data-stu-id="bed40-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="bed40-120">Политику аудита можно определить для конкретной базы данных или как политику сервера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bed40-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="bed40-121">Политика сервера применяется tooall существующих и новых баз данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="bed40-122">Если *включен аудит больших двоичных объектов сервера*, его *всегда применяется базы данных toohello* (то есть hello базы данных будет выполняться аудит), независимо от базы данных hello параметры аудита.</span><span class="sxs-lookup"><span data-stu-id="bed40-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="bed40-123">Включение аудита для базы данных hello в tooenabling сложения его на сервере hello большого двоичного объекта будет *не* переопределить или изменить любые параметры hello hello server большого двоичного объекта аудита.</span><span class="sxs-lookup"><span data-stu-id="bed40-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="bed40-124">Оба аудита будут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="bed40-124">Both audits will exist side by side.</span></span> <span data-ttu-id="bed40-125">Другими словами hello базы данных будет выполняться аудит дважды в параллельном режиме (один раз политикой сервера hello и один раз политикой hello базы данных).</span><span class="sxs-lookup"><span data-stu-id="bed40-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="bed40-126">Не устанавливайте политику аудита больших двоичных объектов одновременно для сервера и базы данных, за исключением следующих случаев.</span><span class="sxs-lookup"><span data-stu-id="bed40-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="bed40-127">Требуется другой toouse *учетной записи хранилища* или *срок хранения* для конкретной базы данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="bed40-128">Типы событий tooaudit или категорий, необходимой для конкретной базы данных, отличные от типов событий или категорий, которые проверяются для hello rest hello баз данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="bed40-129">Например может потребоваться вставки для таблицы, требующих аудита toobe только для конкретной базы данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="bed40-130">В противном случае рекомендуется включить аудит больших двоичных объектов только на уровне сервера, так и оставьте hello уровня базы данных аудита выключены для всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="bed40-131"><a id="subheading-2"></a>Настройка аудита базы данных</span><span class="sxs-lookup"><span data-stu-id="bed40-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="bed40-132">Hello следующем разделе описана конфигурация hello аудита с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="bed40-133">Go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bed40-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bed40-134">Go toohello **параметры** колонке SQL базы данных и SQL server требуется tooaudit hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="bed40-135">В hello **параметры** колонке выберите **обнаружения аудита и угрозы**.</span><span class="sxs-lookup"><span data-stu-id="bed40-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="bed40-136"><a id="auditing-screenshot"></a> ![Область навигации][1]</span><span class="sxs-lookup"><span data-stu-id="bed40-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="bed40-137">Если вы предпочитаете tooset политику аудита сервера (который будет применяться tooall существующих и новых баз данных на этом сервере), можно выбрать hello **проверить параметры сервера** ссылку в колонке аудита hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="bed40-138">Можно просмотреть или изменить параметры аудита сервера hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-138">You can then view or modify hello server auditing settings.</span></span>

    ![Область навигации][2]
4. <span data-ttu-id="bed40-140">Если вы предпочитаете tooenable большого двоичного объекта аудита на уровне hello базы данных (в дополнение tooor вместо аудит на уровне сервера), для **аудита**выберите **ON**и для **аудита тип** , выберите **большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="bed40-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="bed40-141">Если включен аудит сервера больших двоичных объектов, hello база данных настроена аудита будет существовать параллельно с hello server большого двоичного объекта аудита.</span><span class="sxs-lookup"><span data-stu-id="bed40-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Область навигации][3]
5. <span data-ttu-id="bed40-143">tooopen hello **хранения журналов аудита** колонке выберите **сведения о хранилище**.</span><span class="sxs-lookup"><span data-stu-id="bed40-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="bed40-144">Выберите учетную запись хранилища Azure hello где журналы будут сохранены, а затем выберите срок хранения hello, после которого hello старые журналы будут удалены.</span><span class="sxs-lookup"><span data-stu-id="bed40-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="bed40-145">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bed40-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="bed40-146">hello tooget наиболее эффективно использовать hello аудита шаблоны отчетов, используйте hello учетную запись хранения для всех баз данных аудита.</span><span class="sxs-lookup"><span data-stu-id="bed40-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="bed40-147"><a id="storage-screenshot"></a> ![Область навигации][4]</span><span class="sxs-lookup"><span data-stu-id="bed40-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="bed40-148">Следует toocustomize hello аудиту события можно сделать это с помощью PowerShell или hello REST API.</span><span class="sxs-lookup"><span data-stu-id="bed40-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="bed40-149">Дополнительные сведения см. в разделе hello [автоматизации (PowerShell или REST API)](#subheading-7) раздела.</span><span class="sxs-lookup"><span data-stu-id="bed40-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="bed40-150">После настройки параметров аудита, можно включить возможность обнаружения новых угроз hello и настройка оповещений безопасности tooreceive сообщений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="bed40-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="bed40-151">Использование функции обнаружения угроз позволяет настроить упреждающие оповещения об аномальной активности в базах данных, которая может указывать на потенциальные угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="bed40-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="bed40-152">Дополнительные сведения см. в статье [Обнаружение угроз для базы данных SQL](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bed40-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="bed40-153">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bed40-153">Click **Save**.</span></span>





## <span data-ttu-id="bed40-154"><a id="subheading-3"></a>Анализ журналов и отчетов аудита</span><span class="sxs-lookup"><span data-stu-id="bed40-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="bed40-155">Журналы аудита, собираются в учетной записи хранилища Azure, которые были выбраны во время установки hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="bed40-156">Журналы аудита можно просматривать с помощью таких инструментов, как [обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="bed40-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="bed40-157">Журналы аудита больших двоичных объектов сохраняются в виде коллекции файлов больших двоичных объектов в контейнере **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="bed40-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="bed40-158">Дополнительные сведения об иерархии hello папки хранения журналов аудита blob hello, соглашения об именовании для BLOB-объектов и формат журнала см. в разделе hello [большой двоичный объект аудита формат ссылку на журнал (Загрузка файла .docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="bed40-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="bed40-159">Большой двоичный объект tooview журналы аудита можно использовать несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="bed40-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="bed40-160">Используйте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bed40-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="bed40-161">Откройте hello соответствующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-161">Open hello relevant database.</span></span> <span data-ttu-id="bed40-162">AT hello верхней части базы данных hello **аудита и угрозы обнаружения** колонке нажмите кнопку **Просмотр журналов аудита**.</span><span class="sxs-lookup"><span data-stu-id="bed40-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Область навигации][7]

    <span data-ttu-id="bed40-164">**Записи аудита** открывается колонка, из которых вы будете иметь доступ tooview hello журналы.</span><span class="sxs-lookup"><span data-stu-id="bed40-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="bed40-165">Определенные даты можно просмотреть, щелкнув **фильтра** вверху hello hello **записи аудита** колонку.</span><span class="sxs-lookup"><span data-stu-id="bed40-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="bed40-166">Вы можете переключаться между записями аудита, созданными политиками аудита для сервера и для базы данных.</span><span class="sxs-lookup"><span data-stu-id="bed40-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Область навигации][8]

* <span data-ttu-id="bed40-168">Используйте системную функцию hello **sys.fn_get_audit_file** данные журнала аудита hello tooreturn (T-SQL) в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="bed40-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="bed40-169">Дополнительные сведения об использовании этой функции см. в разделе hello [sys.fn_get_audit_file документации](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="bed40-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="bed40-170">Используйте **объединение файлов аудита** в SQL Server Management Studio (начиная с SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="bed40-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="bed40-171">Hello меню среды SSMS выберите **файл** > **откройте** > **слияние файлов аудита**.</span><span class="sxs-lookup"><span data-stu-id="bed40-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Область навигации][9]
    2. <span data-ttu-id="bed40-173">Hello **добавить файлы аудита** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="bed40-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="bed40-174">Выберите один из hello **добавить** вариантов ли toomerge аудита файлов из локального диска или импортировать их из хранилища Azure (вам будет tooprovide необходимые сведения о хранилище Azure и ключа учетной записи).</span><span class="sxs-lookup"><span data-stu-id="bed40-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="bed40-175">После добавления всех файлов toomerge щелкните **ОК** операции слияния toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="bed40-176">Hello объединенный файл откроется в среде SSMS, где можно просмотреть и проанализировать их, а также экспорта его tooan XEL или CSV-файла или tooa таблицы.</span><span class="sxs-lookup"><span data-stu-id="bed40-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="bed40-177">Используйте hello [синхронизации приложения](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , мы создали.</span><span class="sxs-lookup"><span data-stu-id="bed40-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="bed40-178">Он работает в Azure и использует служба аналитики журналов Operations Management Suite (OMS) открытого API-интерфейсы toopush SQL журналы аудита в OMS.</span><span class="sxs-lookup"><span data-stu-id="bed40-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="bed40-179">Синхронизация приложения Hello журналы аудита SQL помещает в аналитику журнала OMS для использования через панель мониторинга службы анализа журналов OMS hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="bed40-180">Используйте Power BI.</span><span class="sxs-lookup"><span data-stu-id="bed40-180">Use Power BI.</span></span> <span data-ttu-id="bed40-181">Вы можете просматривать и анализировать данные журнала аудита в Power BI.</span><span class="sxs-lookup"><span data-stu-id="bed40-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="bed40-182">Вы можете узнать больше о [Power BI, а также скачать шаблон](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="bed40-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="bed40-183">Загрузите файлы журналов из контейнера больших двоичных объектов хранилища Azure через портал hello, или с помощью средства, такие как [обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="bed40-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="bed40-184">После загрузки файла журнала локально, можно дважды щелкнуть tooopen файл hello, просмотр и анализ журналов hello в среде SSMS.</span><span class="sxs-lookup"><span data-stu-id="bed40-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="bed40-185">Вы также можете загрузить одновременно несколько файлов через обозреватель хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bed40-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="bed40-186">Щелкните правой кнопкой мыши конкретную вложенную папку (например, вложенную папку, содержащую все файлы журналов для определенной даты) и выберите **сохранение** toosave в локальной папке.</span><span class="sxs-lookup"><span data-stu-id="bed40-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="bed40-187">Дополнительные методы</span><span class="sxs-lookup"><span data-stu-id="bed40-187">Additional methods:</span></span>
   * <span data-ttu-id="bed40-188">После загрузки нескольких файлов (или вложенную папку, содержащую файлы журнала для целый день, как описано в hello предыдущему элементу этого списка), можно объединить их локально как описано hello файлов аудита слияния SSMS описано выше.</span><span class="sxs-lookup"><span data-stu-id="bed40-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="bed40-189">Чтобы просмотреть журналы аудита больших двоичных объектов программным способом:</span><span class="sxs-lookup"><span data-stu-id="bed40-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="bed40-190">Используйте hello [чтения расширенных событий](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) библиотеки C#.</span><span class="sxs-lookup"><span data-stu-id="bed40-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="bed40-191">Используйте [запросы к файлам расширенных событий](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bed40-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="bed40-192"><a id="subheading-5"></a>Рекомендации для рабочей среды</span><span class="sxs-lookup"><span data-stu-id="bed40-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="bed40-193"><a id="subheading-6">Аудит геореплицированных баз данных</a></span><span class="sxs-lookup"><span data-stu-id="bed40-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="bed40-194">При использовании географически реплицируемых баз данных, это возможно tooset аудита для базы данных-источника hello, базы данных-получателя hello или оба, в зависимости от типа аудита hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="bed40-195">Следуйте данным инструкциям (Помните, что аудит больших двоичных объектов можно включить или отключить только от hello основной базы данных, параметры аудита).</span><span class="sxs-lookup"><span data-stu-id="bed40-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="bed40-196">**База данных-источник**.</span><span class="sxs-lookup"><span data-stu-id="bed40-196">**Primary database**.</span></span> <span data-ttu-id="bed40-197">Включить аудит больших двоичных объектов, либо на сервере hello, либо на саму базу данных hello, следуя инструкциям в hello [настройки аудита для базы данных](#subheading-2) раздела.</span><span class="sxs-lookup"><span data-stu-id="bed40-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="bed40-198">**База данных-получатель**.</span><span class="sxs-lookup"><span data-stu-id="bed40-198">**Secondary database**.</span></span> <span data-ttu-id="bed40-199">Включить аудит больших двоичных объектов на hello базы данных-источника, как описано в hello [настройки аудита для базы данных](#subheading-2) раздела.</span><span class="sxs-lookup"><span data-stu-id="bed40-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="bed40-200">Большой двоичный объект должен быть включен аудит на hello *базы данных-источника самого*, не hello server.</span><span class="sxs-lookup"><span data-stu-id="bed40-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="bed40-201">Включив аудит больших двоичных объектов в базе данных-источнике hello, он также становятся доступными на базу данных-получатель hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="bed40-202">По умолчанию hello параметры хранилища для баз данных-получателей hello будет идентичные toothose hello базы данных-источника, вызывают трафика между язык.</span><span class="sxs-lookup"><span data-stu-id="bed40-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="bed40-203">Этого можно избежать, включив аудит больших двоичных объектов на сервере-получателе hello и настройки локального хранения в параметрах хранилища сервера-получателя hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="bed40-204">Место хранения hello hello базы данных-получателя, для них в каждой базе данных, сохранении свое хранилище toolocal журналы аудита будут переопределены.</span><span class="sxs-lookup"><span data-stu-id="bed40-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="bed40-205"><a id="subheading-6">Повторное создание ключа к хранилищу данных</a></span><span class="sxs-lookup"><span data-stu-id="bed40-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="bed40-206">В рабочей среде, скорее всего, toorefresh хранилища ключей периодически.</span><span class="sxs-lookup"><span data-stu-id="bed40-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="bed40-207">При обновлении ключей, требуется политика аудита tooresave hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="bed40-208">Hello процесс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bed40-208">hello process is as follows:</span></span>

1. <span data-ttu-id="bed40-209">Откройте hello **сведения о хранилище** колонку.</span><span class="sxs-lookup"><span data-stu-id="bed40-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="bed40-210">В hello **ключ доступа к хранилищу** выберите **получателя**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bed40-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="bed40-211">Нажмите кнопку **Сохранить** вверху hello hello аудит колонке конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bed40-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Область навигации][5]
2. <span data-ttu-id="bed40-213">Вернитесь к колонке конфигурации toohello хранилища и повторно создать hello первичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="bed40-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Область навигации][6]
3. <span data-ttu-id="bed40-215">Вернитесь к предыдущему окну toohello аудит колонке конфигурации, переключение hello ключ доступа к хранилищу из вторичного tooprimary и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bed40-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="bed40-216">Нажмите кнопку **Сохранить** вверху hello hello аудит колонке конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bed40-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="bed40-217">Вы можете вернуться в колонке конфигурации хранилища toohello и hello повторно создать вторичный ключ доступа (в процессе подготовки для следующего ключа hello цикл обновления).</span><span class="sxs-lookup"><span data-stu-id="bed40-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="bed40-218"><a id="subheading-7"></a>Автоматизация (PowerShell или REST API)</span><span class="sxs-lookup"><span data-stu-id="bed40-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="bed40-219">Также можно настроить аудит в базе данных SQL Azure с помощью следующих средств автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="bed40-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="bed40-220">**Командлеты PowerShell**</span><span class="sxs-lookup"><span data-stu-id="bed40-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="bed40-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="bed40-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="bed40-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="bed40-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="bed40-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="bed40-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="bed40-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="bed40-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="bed40-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="bed40-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="bed40-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="bed40-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="bed40-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="bed40-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="bed40-228">Пример сценария см. в статье [Настройка аудита и обнаружения угроз для базы данных SQL с помощью PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bed40-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="bed40-229">**REST API — аудит больших двоичных объектов**:</span><span class="sxs-lookup"><span data-stu-id="bed40-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="bed40-230">Создание или обновление политики аудита BLOB-объектов базы данных</span><span class="sxs-lookup"><span data-stu-id="bed40-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="bed40-231">Создание или обновление политики аудита BLOB-объектов сервера</span><span class="sxs-lookup"><span data-stu-id="bed40-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="bed40-232">Получение политики аудита BLOB-объектов базы данных</span><span class="sxs-lookup"><span data-stu-id="bed40-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="bed40-233">Получение политики аудита BLOB-объектов сервера</span><span class="sxs-lookup"><span data-stu-id="bed40-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="bed40-234">Получение результата операции аудита для BLOB-объектов сервера</span><span class="sxs-lookup"><span data-stu-id="bed40-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
