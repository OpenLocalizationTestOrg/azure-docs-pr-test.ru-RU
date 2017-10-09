---
title: "aaaAuditing в хранилище данных SQL Azure | Документы Microsoft"
description: "Приступая к работе с аудитом в хранилище данных SQL Azure"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="9c2d0-103">Аудит в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9c2d0-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c2d0-104">Аудит</span><span class="sxs-lookup"><span data-stu-id="9c2d0-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="9c2d0-105">Обнаружение угроз</span><span class="sxs-lookup"><span data-stu-id="9c2d0-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="9c2d0-106">Аудит хранилища данных SQL позволяет toorecord события в журнал аудита tooan базы данных в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="9c2d0-107">Аудит может помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="9c2d0-108">Аудит хранилища данных SQL объединен с Microsoft Power BI для создания подробных отчетов и детального анализа.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="9c2d0-109">Средства аудита включить и упростить соблюдение стандартов toocompliance, но не гарантируют соответствия.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="9c2d0-110">Дополнительные сведения о Azure программы, соответствие стандартам поддержки, см. в разделе hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Центр управления безопасностью Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="9c2d0-111">[Основы аудита баз данных]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="9c2d0-112">[Настройка аудита базы данных]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="9c2d0-113">[Анализ журналов и отчетов аудита]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="9c2d0-114"><a id="subheading-1"></a>Основы аудита баз данных хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9c2d0-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="9c2d0-115">Аудит базы данных хранилища данных SQL позволяет:</span><span class="sxs-lookup"><span data-stu-id="9c2d0-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="9c2d0-116">**Сохранить** журнал аудита выбранных событий.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="9c2d0-117">Можно определить категории аудита toobe действия базы данных.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="9c2d0-118">**Создавать отчеты** по действиям, производимым с базой данных.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-118">**Report** on database activity.</span></span> <span data-ttu-id="9c2d0-119">Можно использовать готовые отчеты и панели мониторинга tooget, быстро начать работу с действия и уведомления о событиях.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="9c2d0-120">**Анализировать** отчеты.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-120">**Analyze** reports.</span></span> <span data-ttu-id="9c2d0-121">Вы можете искать подозрительные события, необычную деятельность и тенденции.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="9c2d0-122">Вы можете настроить аудит для hello, следующие категории событий:</span><span class="sxs-lookup"><span data-stu-id="9c2d0-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="9c2d0-123">**Обычный SQL** и **параметризованные SQL** для какой hello журналы аудита, собранные классифицируются как</span><span class="sxs-lookup"><span data-stu-id="9c2d0-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="9c2d0-124">**Toodata доступа**</span><span class="sxs-lookup"><span data-stu-id="9c2d0-124">**Access toodata**</span></span>
* <span data-ttu-id="9c2d0-125">**Изменения в схеме данных (DDL)**</span><span class="sxs-lookup"><span data-stu-id="9c2d0-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="9c2d0-126">**Изменения данных (DML)**</span><span class="sxs-lookup"><span data-stu-id="9c2d0-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="9c2d0-127">**Учетные записи, роли и разрешения (DCL)**</span><span class="sxs-lookup"><span data-stu-id="9c2d0-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="9c2d0-128">**Хранимая процедура**, **Вход в систему** и **Управления транзакциями**.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="9c2d0-129">Для каждой категории событий **успешные** и **неуспешные** операции аудита настраиваются отдельно.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="9c2d0-130">Дополнительные сведения о мероприятиях hello и аудит событий см. в разделе hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">ссылка на формат журнала аудита (Загрузка файла doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="9c2d0-131">Журналы аудита хранятся в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="9c2d0-132">Срок хранения журнала аудита можно установить.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="9c2d0-133">Политику аудита можно определить для конкретной базы данных или как политику сервера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="9c2d0-134">Политика аудита сервера по умолчанию применяется tooall баз данных на сервере, не имеющих переопределение базы данных аудита определена конкретная политика.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="9c2d0-135">Прежде чем настраивать проверку аудита, убедитесь, что вы используете [клиент прежних версий](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="9c2d0-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="9c2d0-136"><a id="subheading-2"></a>Настройка аудита базы данных</span><span class="sxs-lookup"><span data-stu-id="9c2d0-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="9c2d0-137">Запустите hello <a href="https://portal.azure.com" target="_blank">портал Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="9c2d0-138">Go toohello **параметры** колонке hello требуется tooaudit хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="9c2d0-139">В hello **параметры** колонке выберите **обнаружения аудита и угрозы**.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="9c2d0-140">Затем включите аудит, щелкнув hello **ON** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="9c2d0-141">В hello аудит колонке конфигурации, выберите **сведения о ХРАНИЛИЩЕ** tooopen hello хранения журналов аудита колонку.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="9c2d0-142">Выберите учетную запись хранилища Azure, где будут сохраняться журналы hello и hello срока хранения.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="9c2d0-143">Hello используйте учетную запись хранения для всех hello tooget аудита баз данных, наиболее эффективно использовать hello готовые отчеты шаблонов.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="9c2d0-144">Нажмите кнопку hello **ОК** кнопку toosave hello хранения сведений конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="9c2d0-145">В разделе **Ведение ЖУРНАЛА СОБЫТИЙ,**, нажмите кнопку **успех** и **СБОЯ** toolog все события или выберите отдельных категорий событий.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="9c2d0-146">При настройке аудита для базы данных может потребоваться строка подключения hello tooalter вашей tooensure клиента, которые правильно захвачены данные аудита.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="9c2d0-147">Проверьте hello [изменить FDQN сервера в строке подключения hello](sql-data-warehouse-auditing-downlevel-clients.md) разделе для подключения клиентов нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="9c2d0-148">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-148">Click **OK**.</span></span>

## <span data-ttu-id="9c2d0-149"><a id="subheading-3"></a>Анализ журналов и отчетов аудита</span><span class="sxs-lookup"><span data-stu-id="9c2d0-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="9c2d0-150">Журналы аудита объединяются в коллекции таблиц хранилища с **SQLDBAuditLogs** префикс в hello учетной записи хранилища Azure, которые были выбраны во время установки.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="9c2d0-151">Просматривать файлы журнала можно с помощью таких инструментов, как <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">обозреватель хранилищ Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="9c2d0-152">Шаблон отчета предварительно настроенных панель мониторинга доступна как <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">электронная таблица Excel</a> toohelp быстрого анализа данных журнала.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="9c2d0-153">шаблон hello toouse на журналов аудита, требуются Excel 2013 или более поздней версии и Power Query, который можно загрузить <a href="http://www.microsoft.com/download/details.aspx?id=39379">здесь</a>.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="9c2d0-154">шаблон Hello имеет вымышленной образец данных в нем, и можно настроить tooimport Power Query журнал аудита непосредственно из вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="9c2d0-155"><a id="subheading-4"></a>Повторное создание ключа к хранилищу данных</span><span class="sxs-lookup"><span data-stu-id="9c2d0-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="9c2d0-156">В рабочей среде, скорее всего, toorefresh хранилища ключей периодически.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="9c2d0-157">При обновлении ключей, вы должны toosave hello политики.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="9c2d0-158">Hello процесс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c2d0-158">hello process is as follows:</span></span>

1. <span data-ttu-id="9c2d0-159">В hello аудит колонке конфигурации (описано выше в программе установки hello аудита раздела) переключение hello **ключ доступа к хранилищу** из *основной* слишком*получателя* и  **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="9c2d0-160">Колонку настройки хранилища перейдите toohello и **повторно создать** hello *первичный ключ доступа*.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="9c2d0-161">Вернитесь к предыдущему окну toohello аудит колонке конфигурации коммутатора hello **ключ доступа к хранилищу** из *получателя* слишком*основной* и нажмите клавишу **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="9c2d0-162">Вернитесь к предыдущему окну хранилища toohello пользовательского интерфейса и **повторно создать** hello *вторичный ключ доступа* (при подготовке к hello Далее ключи цикл обновления.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="9c2d0-163"><a id="subheading-5"></a>Автоматизация (PowerShell или REST API)</span><span class="sxs-lookup"><span data-stu-id="9c2d0-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="9c2d0-164">Также можно настроить аудит в хранилище данных SQL Azure с помощью следующих средств автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="9c2d0-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="9c2d0-165">**Командлеты PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9c2d0-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="9c2d0-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="9c2d0-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="9c2d0-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="9c2d0-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="9c2d0-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="9c2d0-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="9c2d0-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="9c2d0-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Основы аудита баз данных]: #subheading-1
[Настройка аудита базы данных]: #subheading-2
[Анализ журналов и отчетов аудита]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy