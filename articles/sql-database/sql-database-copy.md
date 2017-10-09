---
title: "aaaCopy базы данных Azure SQL | Документы Microsoft"
description: "Создание копии Базы данных SQL Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Копирование Базы данных SQL Azure

База данных SQL Azure предоставляет несколько методов для создания транзакционно согласованной копии существующий SQL Azure базы данных на любом hello же сервере или другом сервере. Можно скопировать базу данных SQL с помощью hello портал Azure, PowerShell или T-SQL. 

## <a name="overview"></a>Обзор

Копия базы данных является моментальным снимком hello базы данных-источника на момент времени hello hello копирования запроса. Можно выбрать hello того же сервера или другой сервер, уровень производительности и уровня службы или на разных уровнях производительности в рамках hello же уровень обслуживания (выпуск). После завершения копирования hello, оно становится полностью работоспособной независимой базой данных. На этом этапе можно обновить или понизить его tooany выпуска. Hello имена входа, пользователей и разрешения можно управлять независимо друг от друга.  

## <a name="logins-in-hello-database-copy"></a>Имена для входа в hello копии базы данных.

При копировании toohello базы данных на одном логическом сервере, можно использовать одинаковые имена входа в обеих базах данных hello. Hello субъект безопасности, используемый базы данных hello toocopy становится владельцем базы данных hello hello новой базе данных. Все пользователи базы данных, их разрешения и их представляют идентификаторы безопасности копируются toohello копию базы данных.  

При копировании базы данных tooa другой логический сервер участника на новом сервере hello hello безопасности становится владельцем базы данных hello hello новой базе данных. Если вы используете [пользователей автономной базы данных](sql-database-manage-logins.md) для доступа к данным, убедитесь, что оба hello источника и базы данных-получатели всегда имеют одинаковые учетные данные пользователя, завершить, так что после копирования hello вы сразу же доступны hello его с таким же hello учетные данные. 

Если вы используете [Azure Active Directory](../active-directory/active-directory-whatis.md), можно полностью исключить hello потребность в управлении учетными данными в копии hello. Тем не менее при копировании hello базы данных tooa новый сервер доступа на основе имени входа hello могут не работать, поскольку приветствия имен входа на новом сервере hello не существуют. toolearn об управлении именами входа, при копировании базы данных tooa другого логического сервера, в разделе [как toomanage Azure SQL базы данных безопасности после аварийного восстановления](sql-database-geo-replication-security-config.md). 

После успешного завершения копирования hello, перед другими пользователями, сопоставляются только hello входа, инициировавший копирование, hello hello владелец базы данных, можно выполнить toohello новой базы данных. имена входа tooresolve после завершения операции копирования hello. в разделе [разрешение имен входа](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Копирование базы данных с помощью портала Azure hello

toocopy базы данных с помощью hello портал Azure, Привет открыть страницу для базы данных и нажмите кнопку **копирования**. 

   ![Копирование базы данных](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Копирование базы данных с помощью PowerShell

базы данных с помощью PowerShell, используйте hello toocopy [New AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) командлета. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Полный пример скрипта см. в разделе [скопировать новый сервер базы данных tooa](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Копирование базы данных с помощью Transact-SQL

Войдите в базе данных master toohello базы данных с именем входа субъекта серверного уровня hello или hello имя входа, создавшее hello базы данных, которая toocopy. Для копирования toosucceed базы данных имена входа, которые не являются hello участник уровня сервера должны быть членами роли dbmanager hello. Дополнительные сведения об именах входа и подключения toohello сервера см. в разделе [Управление именами входа](sql-database-manage-logins.md).

Запустите копирование базы данных-источника hello с hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) инструкции. Выполнение этой инструкции запускает процесс копирования базы данных hello. Поскольку копирование базы данных является асинхронным процессом, hello инструкции CREATE DATABASE возвращает до завершения копирования базы данных hello.

### <a name="copy-a-sql-database-toohello-same-server"></a>Копирование базы данных SQL toohello того же сервера.
Войдите в базе данных master toohello базы данных с именем входа субъекта серверного уровня hello или hello имя входа, создавшее hello базы данных, которая toocopy. Для копирования toosucceed базы данных имена входа, которые не являются hello участник уровня сервера должны быть членами роли dbmanager hello.

Эта команда копирует Database1 tooa новая база данных Database 2 на hello того же сервера. В зависимости от размера базы данных hello hello, операция копирования может занять некоторое время toocomplete.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Скопируйте другой сервер tooa базы данных SQL

Войдите в базе данных master toohello базы данных на сервере назначения hello, где создан toobe hello новую базу данных сервера базы данных SQL hello. Используйте имя входа, которое имеет hello же имя и пароль как владелец базы данных hello hello базы данных-источника на сервере базы данных SQL источника hello. Hello входа на сервер назначения hello также необходимо быть членом роли dbmanager hello или именем входа субъекта серверного уровня hello.

Эта команда копирует Database1 на сервере server1 tooa новая база данных Database 2 на сервере server2. В зависимости от размера базы данных hello hello, операция копирования может занять некоторое время toocomplete.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Следить за ходом hello hello операции копирования

Наблюдать за процессом копирования hello с помощью представления sys.databases и sys.dm_database_copies hello. Здравствуйте, копирование hello во время выполнения, **state_desc** столбца представления sys.databases hello для новой базы данных hello установлено слишком**копирование**.

* Здравствуйте, если hello копирование завершилось с ошибкой, **state_desc** столбца представления sys.databases hello для новой базы данных hello установлено слишком**ПОДОЗРЕНИЕ**. Выполнение инструкции DROP hello hello новой базе данных и повторите попытку позже.
* Если hello копирование завершилось успешно, hello **state_desc** столбца представления sys.databases hello для новой базы данных hello установлено слишком**ONLINE**. копирование Hello завершена, и новая база данных hello является обычной базой данных, которые могут быть изменены независимо от базы данных-источника hello.

> [!NOTE]
> Если вы решите toocancel hello копирование его во время выполнения, выполните hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) инструкции hello новой базе данных. Кроме того при выполнении инструкции DROP DATABASE hello hello базы данных-источника также отменяет hello, процесс копирования.
> 

## <a name="resolve-logins"></a>Разрешение имен для входа

После hello новая база данных находится в оперативном режиме на конечном сервере hello, используйте hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) инструкции tooremap hello пользователям hello создания базы данных toologins на конечном сервере hello. tooresolve связь с учетной записью, пользователям [Диагностика потерянных пользователей](https://msdn.microsoft.com/library/ms175475.aspx). См. также [как toomanage Azure SQL базы данных безопасности после аварийного восстановления](sql-database-geo-replication-security-config.md).

Все пользователи в новую базу данных hello сохранять hello разрешения, которыми они обладали hello базы данных-источника. Hello пользователя, запустившего hello копию базы данных, становится владельцем базы данных hello hello новой базы данных и назначается новый идентификатор безопасности (SID). После успешного завершения копирования hello, перед другими пользователями, сопоставляются только hello входа, инициировавший копирование, hello hello владелец базы данных, можно выполнить toohello новой базы данных.

toolearn об управлении пользователями и именами входа, при копировании базы данных tooa другого логического сервера, в разделе [как toomanage Azure SQL базы данных безопасности после аварийного восстановления](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Дальнейшие действия

* Сведения об именах входа см. в разделе [Управление именами входа](sql-database-manage-logins.md) и [как toomanage Azure SQL базы данных безопасности после аварийного восстановления](sql-database-geo-replication-security-config.md).
* tooexport базы данных, в разделе [экспорта базы данных hello tooa BACPAC](sql-database-export.md).
