---
title: "База данных SQL Server aaaMigrate tooAzure базы данных SQL | Документы Microsoft"
description: "Узнайте, toomigrate вашей tooAzure базы данных SQL Server базы данных SQL."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Перенос вашей tooAzure базы данных SQL Server база данных SQL

Перемещение сервера SQL tooAzure базы данных база данных SQL состоит из трех этапов - подготовить, а затем экспортировать и затем импортировать hello базы данных. Из этого руководства вы узнаете, как выполнять такие задачи.

> [!div class="checklist"]
> * Подготовка базы данных в SQL Server для миграции tooAzure базы данных SQL с помощью hello [помощник по миграции данных](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
> * Экспорт файла BACPAC tooa hello базы данных
> * Импорт файла BACPAC hello в базе данных SQL Azure

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.

## <a name="prerequisites"></a>Предварительные требования

toocomplete завершения этого учебника, убедитесь, что hello следующие предварительные требования:

- Установленные hello новейшую версию [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). Также при установке SSMS устанавливается hello новейшую версию SQLPackage, программы командной строки, которое может быть используется tooautomate задачи разработки базы данных. 
- Установленные hello [помощник по миграции данных](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Должна быть определена и иметь доступ tooa базы данных toomigrate. В этом учебнике используется hello [SQL Server 2008 R2 базы данных AdventureWorks OLTP](https://msftdbprodsamples.codeplex.com/releases/view/59211) в экземпляре SQL Server 2008 R2 и более поздних версий, но можно использовать любую базу данных, по своему усмотрению. вопросы совместимости toofix, используйте [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Подготовка к переносу

Все готово tooprepare для миграции. Выполните эти шаги toouse hello  **[помощник по миграции данных](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello готовности базы данных для миграции tooAzure базы данных SQL.

1. Откройте hello **помощник по миграции данных**. Можно запустить DMA на любом компьютере с подключением toohello экземпляр содержащего hello базы данных SQL Server, что планирование toomigrate, tooinstall его на компьютере с размещенным hello hello экземпляр SQL Server не требуется.

     ![Открытие Data Migration Assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. В левом меню hello выберите **+ создать** toocreate **оценки** проекта. Заполните форму hello с **имя проекта** (все остальные значения следует оставить значения по умолчанию) и нажмите кнопку **создать**. Hello **параметры** откроется страница.

     ![Создание проекта в Data Migration Assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. На hello **параметры** щелкните **Далее**. Hello **выберите источники** откроется страница.

     ![Создание параметров переноса данных](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. На hello **выберите источники** введите имя экземпляра SQL Server, содержащего сервер hello, планирование toomigrate hello. Изменение hello другие значения на этой странице, при необходимости. Щелкните **Подключить**.

     ![Выбор новых источников при подготовке к переносу данных](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. В hello **добавить источники** часть hello **выберите источники** выберите флажки hello toobe hello баз данных, протестированы на совместимость. Щелкните **Добавить**.

     ![Выбор новых источников при подготовке к переносу данных](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Нажмите кнопку **Start Assessment** (Запустить оценку).

     ![Запуск оценки при подготовке к переносу данных](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. После завершения оценки hello, сначала найдите toosee, если база данных hello toomigrate достаточно совместимы. Найдите флажок hello на фоне зеленого круга.

     ![Результаты оценки совместимости при подготовке к переносу данных](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Просмотрите результаты hello. Hello **паритет функций SQL Server** показаны не все результаты tooreview результатов по умолчанию hello. В частности, просмотрите hello сведения о функциях, не поддерживаемые и частично поддерживаемые и hello предоставленные сведения о рекомендуемых действий. 

     ![Результаты сравнения при подготовке к переносу данных](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Просмотрите hello **проблемы совместимости** , щелкнув соответствующий параметр в верхнем левом углу hello. В частности анализ hello сведения о миграции препятствия для изменения поведения и устаревшие компоненты для каждого уровня совместимости. Для базы данных hello AdventureWorks2008R2, проверьте изменения hello tooFull-Text Search, так как SQL Server 2008 и hello с отличиями tooSERVERPROPERTY('LCID') SQL Server 2000. Дополнительные сведения об этих изменениях предоставлены по ссылкам. Многие параметры и настройки полнотекстового поиска изменились. 

   > [!IMPORTANT] 
   > После переноса tooAzure вашей базы данных база данных SQL, вы можете toooperate hello базы данных на текущем уровне совместимости (уровень 100 для базы данных AdventureWorks2008R2 hello) или на более высоком уровне. Дополнительные сведения о последствиях hello и параметры для работы на уровне совместимости базы данных см. в разделе [уровень совместимости инструкции ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). См. также [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) сведения о дополнительных параметрах уровня базы данных, связанных с toocompatibility уровней.
   >

10. При необходимости щелкните **Экспорт отчета** toosave hello отчет в формате JSON.
11. Закрыть hello помощник по миграции данных.

## <a name="export-toobacpac-file"></a>Файл экспорта tooBACPAC 

BACPAC-файл является ZIP-файл с расширением BACPAC, содержащий hello метаданных и данных из базы данных SQL Server. BACPAC-файл могут храниться в хранилище BLOB-объектов Azure или в локальное хранилище для архивирования или для миграции - например, из SQL Server tooAzure базы данных SQL. Для согласованного toobe экспорта необходимо убедиться, что нет записи во время экспорта приветствия интенсивна деятельность.

Выполните эти шаги toouse hello SQLPackage программы командной строки tooexport hello AdventureWorks2008R2 toolocal режим хранения базы данных.

1. Откройте командную строку Windows и измените папку tooa каталог, в котором имеется hello **130** версии SQLPackage – например, **\Microsoft SQL Server\130\DAC\bin C:\Program Files (x86)**.

2. Выполните следующую команду SQLPackage на hello tooexport командную строку hello hello **AdventureWorks2008R2** из базы данных **localhost** слишком**AdventureWorks2008R2.bacpac**. Измените эти значения как соответствующие tooyour среды.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![Экспорт SqlPackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

После завершения выполнения hello BACPAC-файл, созданный hello хранится в каталоге hello, где находится исполняемый файл sqlpackage hello. В этом примере это C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Войдите в toohello портал Azure

Войдите в toohello [портал Azure](https://portal.azure.com/). Вход в систему с компьютера hello, с которого выполняется запуск программы командной строки SQLPackage hello облегчает создание hello hello правила брандмауэра на шаге 5.

## <a name="create-a-sql-server-logical-server"></a>Создание логического сервера SQL Server

[Логический сервер SQL Server](sql-database-features.md) выступает в качестве центральной точки администрирования нескольких баз данных. Выполните следующие действия toocreate SQL server логический сервер toocontain hello миграции базы данных Adventure Works OLTP SQL Server. 

1. Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.

2. Тип **sql server** в окне поиска hello на hello **New** и выберите **базы данных SQL (логический сервер)** из hello отфильтрованном списке.

    ![выбор логического сервера](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. На hello **все** щелкните **SQL server (логический сервер)** и нажмите кнопку **создать** на hello **SQL Server (логический сервер)** страницы .

    ![Создание логического сервера](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Заполнение hello SQL server (логический сервер) формы с hello следующую информацию, как показано на hello предшествующий образа:     

   | Настройка       | Рекомендуемое значение | Описание | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Server name** (Имя сервера) | Введите любое глобально уникальное имя | Допустимые имена серверов см. в статье о [правилах и ограничениях именования](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Имя для входа администратора сервера** | Введите любое допустимое имя | Допустимые имена входа см. в статье об [идентификаторах базы данных](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). |
   | **Пароль** | Введите любой допустимый пароль | Пароль должен иметь по крайней мере 8 символов и должен содержать символы трех из следующих категорий hello: буквы в верхнем регистре, буквы в нижнем регистре, цифры и не буквенно-цифровых символов. |
   | **Подписка** | Выбор подписки | Дополнительные сведения о подписках см. [здесь](https://account.windowsazure.com/Subscriptions). |
   | **Группа ресурсов** | Выберите имеющуюся группу ресурсов или создайте ее, например **myResourceGroup** |  Допустимые имена групп ресурсов см. в статье о [правилах и ограничениях именования](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Расположение** | Введите любое действительное расположение для нового сервера hello | Дополнительные сведения о регионах Azure см. [здесь](https://azure.microsoft.com/regions/). |

   ![Заполненная форма создания логического сервера](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Нажмите кнопку **создать** tooprovision hello логического сервера. Подготовка занимает несколько минут. 

> [!IMPORTANT]
> Запомните имя сервера, имя для входа администратора сервера и пароль. Эти значения вам понадобятся позже (в рамках этого руководства).
>

## <a name="create-a-server-level-firewall-rule"></a>создадим правило брандмауэра на уровне сервера;

Создает Hello служба базы данных SQL [брандмауэра на уровне сервера hello](sql-database-firewall-configure.md) , предотвращает внешних приложений и средств подключения toohello сервера или любой базы данных на сервере hello правила брандмауэра не введен tooopen hello брандмауэр для конкретных IP-адресов. Выполните эти шаги toocreate правило брандмауэра уровня сервера базы данных SQL для hello IP-адрес компьютера hello, с которого выполняется запуск программы командной строки SQLPackage hello. Это позволяет SQLPackage tooconnect toohello SQL serverDatabase логический сервер через брандмауэр базы данных SQL Azure hello. 

1. Нажмите кнопку **все ресурсы** hello левом меню и выберите новый сервер на hello **все ресурсы** страницы. страница обзора Hello сервера открывает и предоставляет параметры для дальнейшей настройки.

     ![Общие сведения о логическом сервере](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Нажмите кнопку **брандмауэра** в левом меню hello в **параметры** на страницу обзора hello. Hello **параметры брандмауэра** откроется страница приветствия базы данных SQL server. 

3. Нажмите кнопку **добавить IP-адрес клиента** на hello инструментов tooadd hello IP-адрес компьютера hello используют в настоящее время и нажмите кнопку **Сохранить**. Для текущего IP-адреса будет создано правило брандмауэра уровня сервера.

     ![Настройка правила брандмауэра для сервера](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Нажмите кнопку **ОК**.

Теперь можно подключиться tooall баз данных на этом сервере, с помощью SQL Server Management Studio или другого средства по своему усмотрению с этого IP-адреса, с помощью учетной записи администратора сервера hello создали ранее.

> [!NOTE]
> База данных SQL обменивается данными через порт 1433. Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 1433 может оказаться невозможным брандмауэром вашей сети. В этом случае tooyour сервера базы данных SQL Azure не удается подключиться, если ИТ-отдел открывает порт 1433.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Импорт BACPAC файла tooAzure базы данных SQL 

последние версии Hello hello SQLPackage программа командной строки обеспечивает поддержку создания базы данных Azure SQL по указанному индексу [службы уровня и уровня производительности](sql-database-service-tiers.md). Для наилучшей производительности во время импорта выберите уровень производительности и уровня высокого уровня обслуживания и затем масштабирование после импорта, если уровень производительности и уровня обслуживания hello больше, чем требуется немедленно.

Выполните эти шаги использования hello SQLPackage программы командной строки tooimport hello AdventureWorks2008R2 базы данных tooAzure базы данных SQL. При использовании SQL Server Management Studio для выполнения этой задачи SQLPackage — hello предпочтительный метод для большинства рабочих сред для максимальной гибкостью и оптимальной производительности. В разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Выполните следующую команду SQLPackage на hello tooimport командную строку hello hello **AdventureWorks2008R2** базу данных из локального хранилища toohello SQL server логического сервера, вы ранее созданный tooa новую базу данных, службы уровень **Premium**и цель обслуживания **P6**. Замените значения hello в угловые скобки с соответствующими значениями для логического сервера SQL server и укажите имя для новой базы данных hello (также заменить hello угловые скобки). Можно также toochange значения hello выпуск базы данных и службы objectgive как соответствующие tooyour среды. Для целей этого учебника hello hello перенесенной базы данных называется **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![Импорт с помощью SqlPackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Логический сервер SQL Server прослушивает порт 1433. При попытке tooconnect tooa SQL server логического сервера внутри корпоративного брандмауэра, этот порт должен быть открыт в hello корпоративного брандмауэра для подключения к toosuccessfully вы.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Подключение с помощью SQL Server Management Studio

Используйте SQL Server Management Studio tooestablish сервером базы данных SQL Azure tooyour соединения и только что перенесенной базы данных, называемой **myMigratedDatabase** в этом учебнике. При запуске SQL Server Management Studio на другом компьютере, из которой запущен SQLPackage создайте правило брандмауэра для данного компьютера, используя действия hello в предыдущей процедуре hello.

1. Откройте среду SQL Server Management Studio.

2. В hello **подключения tooServer** диалогового окна введите hello следующую информацию:
   - **Тип сервера** — укажите ядро СУБД.
   - **Имя сервера.** Введите полное имя сервера, например **mynewserver20170403.database.windows.net**.
   - **Проверка подлинности** — укажите проверку подлинности SQL Server.
   - **Имя входа** — введите учетную запись администратора сервера.
   - **Пароль**: hello пароль для учетной записи администратора сервера
 
    ![Подключение с помощью SSMS](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Щелкните **Подключить**. Откроется окно обозревателя объектов Hello. 

4. В обозревателе объектов разверните **баз данных** и разверните **myMigratedDatabase** tooview объектов hello в образце hello базы данных.

## <a name="change-database-properties"></a>Изменение свойств базы данных

Можно изменить уровень службы hello, уровень производительности и уровень совместимости в среде SQL Server Management Studio. Во время фазы импорта hello рекомендуется импортировать tooa выше производительности уровня базы данных для повышения производительности, но масштабировать после завершения импорта hello toosave money, пока не используйте готов tooactively hello импортируемой базы данных. Изменение уровня совместимости hello может привести к повышению производительности и возможности доступа к toohello новейшие hello службы базы данных SQL Azure. При переносе старую базу данных, ее уровень совместимости базы данных поддерживается на уровне наименьшее hello поддерживается, совместимый с базой данных hello импорта. Дополнительные сведения см. в статье [Повышение производительности запросов с использованием уровня совместимости 130 в базе данных SQL Azure](sql-database-compatibility-level-query-performance-130.md).

1. В обозревателе объектов щелкните **myMigratedDatabase** правой кнопкой мыши и выберите **Создать запрос**. Откроется окно запроса tooyour подключенной базы данных.

2. Выполните следующий уровень обслуживания hello tooset команда слишком hello**Стандартная** и hello уровень производительности, слишком**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![Изменение уровня служб](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Выполните следующий уровень совместимости базы данных hello toochange команда слишком hello**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![Изменение уровня совместимости](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Дальнейшие действия 
В этом руководстве вы подготовили, экспортировали и импортировали базу данных. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Подготовка базы данных в SQL Server для миграции tooAzure базы данных SQL
> * Экспорт файла BACPAC tooa hello базы данных
> * Импорт файла BACPAC hello в базе данных SQL Azure

Как переместить следующий учебник toolearn toohello toosecure базы данных.

> [!div class="nextstepaction"]
> [Защита базы данных SQL Azure](sql-database-security-tutorial.md)


