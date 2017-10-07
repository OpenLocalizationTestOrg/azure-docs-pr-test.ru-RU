---
title: "aaaSecure базы данных в хранилище данных SQL | Документы Microsoft"
description: "Советы по защите базы данных в хранилище данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Защита базы данных в хранилище данных SQL
> [!div class="op_single_selector"]
> * [Обзор безопасности](sql-data-warehouse-overview-manage-security.md)
> * [Аутентификация](sql-data-warehouse-authentication.md)
> * [Шифрование (портал)](sql-data-warehouse-encryption-tde.md)
> * [Шифрование (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

В этой статье рассматриваются hello основные сведения о защите базы данных хранилища данных SQL Azure. В частности, эта статья содержит инструкции по началу работы с ресурсами для ограничения доступа, защиты данных и мониторинга действий с базой данных.

## <a name="connection-security"></a>Безопасность подключения
Безопасность подключения ссылается toohow ограничить и защиту tooyour подключения базы данных, с помощью правил брандмауэра и шифрование соединения.

Используются оба hello server и hello базы данных tooreject попытки подключения с IP-адресов, которые не были явно входят правила брандмауэра. tooallow подключения из приложения или общедоступный IP-адрес клиентского компьютера, необходимо сначала создать правило брандмауэра уровня сервера с помощью портала Azure hello, API-интерфейса REST или PowerShell. Рекомендуется ограничить hello разрешен в брандмауэре сервера максимально диапазоны IP-адресов.  tooaccess хранилище данных SQL Azure с локального компьютера, убедитесь, что hello брандмауэр сети и локального компьютера разрешает исходящие соединения через TCP-порт 1433.  Дополнительные сведения см. в разделах [Брандмауэр базы данных SQL Azure][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] и [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Шифрование соединения tooyour хранилище данных SQL по умолчанию.  Изменение соединения toodisable параметры шифрования учитываются.

## <a name="authentication"></a>Аутентификация
Проверка подлинности ссылается toohow проверки подлинности при подключении toohello базы данных. Сейчас хранилище данных SQL поддерживает аутентификацию SQL с использованием имени пользователя и пароля, а также Azure Active Directory. 

При создании hello логического сервера для базы данных, имя входа «администратор сервера» указано имя пользователя и пароль. Используя эти учетные данные, вы можете проверять подлинность tooany базы данных на этом сервере как владелец базы данных hello, или «dbo» через проверку подлинности SQL Server.

Однако рекомендуется, пользователи в вашей организации следует использовать tooauthenticate отдельную учетную запись. Таким образом, можно ограничить hello разрешения, предоставленные toohello приложения и уменьшить риски hello вредоносных действий в случае, если код приложения является уязвимым tooa атак путем внедрения кода SQL. 

пользователь, прошедший проверку подлинности SQL Server, toocreate подключения toohello **master** базы данных на сервере при обработке входа администратора сервера и создать новое имя входа сервера.  Кроме того это разумно toocreate пользователя в базе данных master hello для пользователей в хранилище данных SQL Azure. Создание пользователя в базе данных master позволяет toologin пользователя, с помощью таких средств, как среда SSMS без указания имени базы данных.  Он также позволяет им toouse hello объекта обозревателя tooview все базы данных на SQL server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Подключите tooyour **базы данных хранилища данных SQL** при обработке входа администратора сервера и создать пользователя базы данных на основе только что созданный входа сервера hello.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Если пользователь будет выполнять дополнительные операции, такие как создание имен входа или создания новых баз данных, им также необходимо назначить toobe toohello `Loginmanager` и `dbmanager` роли в базе данных master hello. Дополнительные сведения о эти дополнительные роли и проверкой подлинности tooa базы данных SQL см. в разделе [Управление базами данных и именами входа в базе данных SQL Azure][Managing databases and logins in Azure SQL Database].  Дополнительные сведения о хранилище данных SQL Azure AD см. в разделе [tooSQL данные хранилища с использованием Azure Active Directory проверки подлинности подключения][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Авторизация
Авторизация ссылается toowhat можно выполнить в базе данных хранилища данных SQL Azure и осуществляется с помощью членства в роли и разрешения учетной записи пользователя. Рекомендуется необходимо предоставить пользователям hello наименьшими необходимыми правами. Хранилище данных SQL Azure делает это легко toomanage с ролями в T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

Учетная запись администратора Hello сервера с которым соединение является членом роли db_owner, имеющая центра toodo все условия в базе данных hello. Сохраните эту учетную запись для развертывания обновлений схемы и выполнения других действий по управлению. Использовать учетную запись «ApplicationUser» hello с более ограниченные разрешения tooconnect из базы данных приложения toohello с hello наименьшие права доступа, необходимые для приложения.

Существует предел toofurther способов действиями пользователя с базой данных SQL Azure.

* Детальные [разрешений] [ Permissions] позволяют управления операции, которые можно выполнить для отдельных столбцов таблицы, представления, процедуры и другие объекты в базе данных hello. Используйте Гранулярные разрешения toohave hello большинство элементов управления и предоставьте hello минимальные разрешения, необходимые. Hello детализированные системы слишком сложное и эффективное требует некоторых toouse исследования.
* [Роли базы данных] [ Database roles] отличного от db_datareader и db_datawriter может быть используется toocreate более мощных учетные записи пользователей приложения или менее мощных управления. Hello встроенных предопределенных ролей базы данных предоставляют простой способ toogrant разрешения, но может привести к предоставлять больше прав доступа, чем это необходимо.
* [Хранимые процедуры] [ Stored procedures] может быть используется toolimit hello действия, которые могут быть выполнены в базе данных hello.

Управление базами данных и логических серверов из hello классический портал Azure или с помощью hello API диспетчера ресурсов Azure контролируется с помощью назначений ролей для учетной записи пользователя портала. Дополнительные сведения об этом см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Шифрование
Azure SQL данные хранилища прозрачное шифрование данных (TDE) помогает защититься от угроз вредоносных действий hello, выполняя в реальном времени шифрование и расшифровку статических данных.  При шифровании базы данных, связанных резервных копий и файлов журнала транзакций, шифруются без необходимости tooyour любые изменения приложения. TDE шифрует hello хранения всей базы данных с помощью ключа шифрования симметричного ключа вызываемой hello базы данных. В базе данных SQL hello ключ шифрования базы данных защищен используется встроенный сертификат сервера. Hello встроенный сертификат сервера уникален для каждой базы данных SQL server. Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней. алгоритм шифрования Hello, используемый в хранилище данных SQL — AES-256. Общее описание функции TDE см. в статье [Прозрачное шифрование данных (TDE)][Transparent Data Encryption].

Можно зашифровать базу данных с помощью hello [портала Azure] [ Encryption with Portal] или [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения и примеры о подключении tooyour хранилище данных SQL с помощью различных протоколов см. в разделе [подключения хранилища данных tooSQL][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
