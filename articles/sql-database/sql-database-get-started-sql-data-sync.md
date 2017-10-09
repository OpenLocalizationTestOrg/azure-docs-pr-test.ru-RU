---
title: "aaaGetting к работе с SQL Azure Data Sync (Предварительная версия) | Документы Microsoft"
description: "Это руководство поможет вам приступить к работе с синхронизацией данных SQL Azure (предварительная версия)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Приступая к работе с синхронизацией данных SQL Azure (предварительная версия)
В этом учебнике вы узнаете, как tooset копирование синхронизации данных SQL Azure путем создания гибридных группы синхронизации, содержит экземпляры базы данных SQL Azure и SQL Server. Hello новых групп синхронизации полностью настроена и синхронизирует на hello запланированное время.

В этом руководстве предполагается, что у вас имеется некоторый опыт работы с базой данных SQL и SQL Server. 

Общие сведения о синхронизации данных SQL см. в разделе [Синхронизация данных](sql-database-sync-data.md).

Полные примеры PowerShell, которые показывают, как tooconfigure SQL Data Sync см. статью hello в следующих статьях:
-   [Используйте PowerShell toosync между несколькими базами данных Azure SQL](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Используйте PowerShell toosync между базы данных SQL Azure и локальной базы данных SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Hello полный набор технических документов о синхронизации данных SQL Azure, ранее доступные в библиотеке MSDN, доступен в виде. PDF-документ. Его можно скачать [здесь](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Шаг 1. Создание группы синхронизации

### <a name="locate-hello-data-sync-settings"></a>Поиск параметров синхронизации данных hello

1.  В браузере перейдите toohello портал Azure.

2.  Hello портала найдите базами данных SQL из панели мониторинга или значок hello баз данных SQL на панели инструментов hello.

    ![Список баз данных SQL Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  На hello **баз данных SQL** колонки, hello выберите существующую базу данных SQL требуется toouse как открывает hello базы данных основного сервера для синхронизации данных. hello SQL колонке базы данных.

4.  В колонке базы данных SQL hello для hello выбранной базы данных, выберите **синхронизировать базы данных tooother**. Открывает колонку Hello синхронизации данных.

    ![Параметр базы данных tooother синхронизации](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Создание группы синхронизации

1.  В колонке hello синхронизации данных, выберите **новых групп синхронизации**. Hello **новых групп синхронизации** открывает колонку с шага 1, **создать группу синхронизации**, выделенный. Hello **создать группу синхронизации данных** также открывает колонку.

2.  На hello **создать группу синхронизации данных** колонке hello следующие действия:

    1.  В hello **имя группы синхронизации** введите имя для новой группы синхронизации hello.

    2.  В hello **базы данных метаданных синхронизации** выберите ли toocreate новой базы данных (рекомендуется) или toouse существующей базы данных.

        > [!NOTE]
        > Корпорация Майкрософт рекомендует создать toouse новую пустую базу данных, как hello синхронизации базы данных метаданных. Служба синхронизации данных создает таблицы в этой базе данных и часто выполняет рабочую нагрузку. Эта база данных автоматически становятся как hello синхронизации базы данных метаданных для всех групп синхронизации в выбранной области hello. Нельзя изменить hello синхронизации базы данных метаданных, имени или ее обновления без его удаления.

        Если вы выбрали параметр **Новая база данных**, щелкните **Создать новую базу данных**. Hello **базы данных SQL** открывает колонку. На hello **базы данных SQL** колонки, задайте имя и настройте новую базу данных hello. Нажмите кнопку **ОК**.

        Если вы выбрали **использовать существующую базу данных**выберите hello базы данных из списка hello.

    3.  В hello **автоматическая синхронизация** сначала выберите **на** или **Off**.

        Если вы выбрали **на**, в hello **частота синхронизации** , введите число и выберите в секундах, минутах, часах или днях.

        ![Указание частоты синхронизации](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  В hello **разрешения конфликтов** выберите «Приоритет концентратора» или «Значению члена».

        ![Настройка устранения конфликтов](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Выберите **ОК** и дождитесь hello новый синхронизации группы toobe создан и развернут.

## <a name="step-2---add-sync-members"></a>Шаг 2. Добавление членов синхронизации

После создания и развертывания, шаг 2 новых групп синхронизации hello **добавить участников синхронизации**, выделяется в hello **новых групп синхронизации** колонку.

В hello **базы данных-концентратора** введите учетные данные существующего hello для hello базы данных SQL сервера, на какие hello базы данных-концентратора. Не вводите *новые* учетные данные в этом разделе.

![Добавлена база данных концентратора, группу toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Добавление базы данных SQL Azure

В hello **база данных-участник** статьи, при необходимости добавьте к группе синхронизации toohello базы данных SQL Azure, выбрав **добавления базы данных Azure**. Hello **Настройка базы данных Azure** открывает колонку.

На hello **Настройка базы данных Azure** колонке hello следующие действия:

1.  В hello **имя члена синхронизации** укажите имя для нового участника синхронизации hello. Данное имя отличается от имени hello самой базы данных hello.

2.  В hello **подписки** hello выберите связанные подписки Azure для выставления.

3.  В hello **Azure SQL Server** hello выберите существующий сервер базы данных SQL.

4.  В hello **базы данных SQL Azure** hello выберите существующую базу данных SQL.

5.  В hello **направления синхронизации** выберите двусторонней синхронизации, toohello концентратора, или из hello концентратора.

    ![Добавление нового члена синхронизации для базы данных SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  В hello **Username** и **пароль** введите hello существующие учетные данные для hello базы данных SQL server, на какие hello расположена база данных-участник. Не вводите *новые* учетные данные в этом разделе.

7.  Выберите **ОК** и дождитесь hello новый синхронизации член toobe создан и развернут.

    ![Добавлен новый член синхронизации для базы данных SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Добавление локальной базы данных SQL Server

В hello **база данных-участник** статьи, при необходимости добавьте к группе синхронизации локальной toohello SQL Server, выбрав **добавления базы данных локального**. Hello **Настройка локальной** открывает колонку.

На hello **Настройка локальной** колонке hello следующие действия:

1.  Выберите **hello Выбор шлюза агента синхронизации**. Hello **выберите агент синхронизации** открывает колонку.

    ![Выберите шлюз агента синхронизации hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  На hello **hello Выбор шлюза агента синхронизации** колонке выберите ли toouse существующего агента или создать новый агент.

    Если вы выбрали **существующие агенты**, выберите hello существующий агент из списка hello.

    Если вы выбрали **создайте новый агент**, hello следующие действия:

    1.  Загрузите программное обеспечение агента синхронизации клиента hello по ссылке hello и установить его на компьютере hello, где находится hello SQL Server.
 
        > [!IMPORTANT]
        > У вас есть tooopen исходящих TCP-порт 1433 hello брандмауэра toolet hello клиентского агента в связи с сервером hello.


    2.  Введите имя для hello агента.

    3.  Выберите **Создание и генерация ключа**.

    4.  Копировать буфер toohello ключа агента hello.
        
        ![Создание агента синхронизации](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Выберите **ОК** tooclose hello **выберите агент синхронизации** колонку.

    6.  На компьютере SQL Server hello найдите и запустите приложение hello агент синхронизации клиента.

        ![клиентское приложение агента синхронизации данных Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  В приложении агента синхронизации hello выберите **отправить ключ агента**. Hello **синхронизации метаданных базы данных конфигурации** откроется диалоговое окно.

    8.  В hello **синхронизации метаданных базы данных конфигурации** диалоговое окно, вставить в ключ агента hello, скопированные из hello портал Azure. Также предоставляют hello существующие учетные данные для сервера базы данных SQL Azure hello, на какие hello находится база данных метаданных. (Если вы создали новую базу данных метаданных, это база данных находится на hello сервере базы данных-концентратора hello.) Выберите **ОК** и дождитесь toofinish конфигурации hello.

        ![Введите учетные данные ключа и сервера агента hello](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Если возникли ошибка брандмауэра на этом этапе у вас есть toocreate правило брандмауэра Azure tooallow входящего трафика с компьютера SQL Server hello. Можно создать правило hello вручную на портале hello, но может оказаться проще toocreate его в SQL Server Management Studio (SSMS). В среде SSMS попробуйте tooconnect toohello концентратора и база данных в Azure. Введите ее имя как \<имя_центральной_базы_данных\>.database.windows.net. Следуйте указаниям hello hello hello диалогового окна поле tooconfigure правило брандмауэра Azure. После этого вернитесь toohello клиентский агент синхронизации приложения.

    9.  В приложение hello агент синхронизации клиента, щелкните **зарегистрировать** tooregister базы данных SQL Server с агентом hello. Hello **конфигурация SQL Server** откроется диалоговое окно.

        ![Добавление и настройка базы данных SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. В hello **конфигурация SQL Server** диалогового окна выберите ли tooconnect с помощью проверки подлинности SQL Server или проверка подлинности Windows. Если выбрана проверка подлинности SQL Server, введите учетные данные существующего hello. Укажите имена SQL Server hello и hello hello базы данных, в которое следует toosync. Выберите **Проверка соединения** tootest параметры. Затем нажмите кнопку **Save** (Сохранить). Hello зарегистрированной базы данных отображается в списке hello.

        ![База данных SQL Server зарегистрирована](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. Теперь можно закрыть приложение hello агент синхронизации клиента.

    12. На hello hello портала **Настройка локальной** колонке выберите **выберите hello базы данных.** Hello **Выбор базы данных** открывает колонку.

    13. На hello **Выбор базы данных** колонки в hello **имя члена синхронизации** укажите имя для нового участника синхронизации hello. Данное имя отличается от имени hello самой базы данных hello. Выберите базу данных hello из списка hello. В hello **направления синхронизации** выберите двусторонней синхронизации, toohello концентратора, или из hello концентратора.

        ![Выберите hello в локальную базу данных](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Выберите **ОК** tooclose hello **Выбор базы данных** колонку. Выберите **ОК** tooclose hello **Настройка локальной** колонки и ожидания hello новые синхронизации toobe член создан и развернут. Наконец, нажмите кнопку **ОК** tooclose hello **выбрать элементы синхронизации** колонку.

        ![На локальную базу данных, добавленные toosync группы](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL Data Sync и hello локальный агент, добавьте вашей роли пользователя имя toohello `DataSync_Executor`. Синхронизация данных создает эту роль на экземпляре SQL Server hello.

## <a name="step-3---configure-sync-group"></a>Шаг 3. Настройка группы синхронизации

После создания и развертывания, шаг 3 hello новым участникам группы синхронизации **Настройка группы синхронизации**, выделяется в hello **новых групп синхронизации** колонку.

1.  На hello **таблиц** колонке выберите базу данных из списка hello синхронизации членов группы, а затем выберите **обновление схемы**.

2.  Из списка доступных таблиц hello выберите hello таблиц, которые должны toosync.

    ![Выберите таблицы toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  По умолчанию выбраны все столбцы в таблице hello. Если вы не хотите toosync все столбцы hello, отключите hello флажки для столбцов hello, что вы не хотите toosync. Убедитесь, что выбран tooleave hello первичного ключевого столбца.

    ![Выбор полей toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Наконец, щелкните **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
Поздравляем! Вы создали группу синхронизации, которая включает и экземпляр базы данных SQL, и базу данных SQL Server.

Дополнительные сведения о базе данных SQL и синхронизации данных SQL:

-   [Загрузите hello технической документации завершения синхронизации данных SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Загрузить документацию по API REST для синхронизации данных SQL hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Обзор Базы данных SQL](sql-database-technical-overview.md)
-   [Управление жизненным циклом базы данных](https://msdn.microsoft.com/library/jj907294.aspx)
