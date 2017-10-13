---
title: "Защита базы данных в хранилище данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: 6ea45c40bc428282faf24b4a08f8b0d345adb3fd
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Защита базы данных в хранилище данных SQL
> [!div class="op_single_selector"]
> * [Обзор безопасности](sql-data-warehouse-overview-manage-security.md)
> * [Аутентификация](sql-data-warehouse-authentication.md)
> * [Шифрование (портал)](sql-data-warehouse-encryption-tde.md)
> * [Шифрование (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

В этой статье рассматриваются основы защиты базы данных в хранилище данных SQL. В частности, эта статья содержит инструкции по началу работы с ресурсами для ограничения доступа, защиты данных и мониторинга действий с базой данных.

## <a name="connection-security"></a>Безопасность подключения
Под безопасностью подключения подразумеваются способы ограничения и защиты подключений к базе данных с помощью правил брандмауэра и шифрования подключения.

Правила брандмауэра используются как сервером, так и базой данных для отклонения попыток подключиться с IP-адресов, которые не были явно включены в белый список. Чтобы разрешить подключение из своего приложения или с клиентского компьютера с общедоступным IP-адресом, сначала необходимо создать правило брандмауэра уровня сервера. Для этого воспользуйтесь порталом Azure, REST API или PowerShell. В брандмауэре сервера рекомендуется максимально ограничить диапазоны разрешенных IP-адресов.  Для доступа к хранилищу данных SQL Azure с локального компьютера убедитесь, что брандмауэр сети и локального компьютера разрешает исходящие подключения по TCP-порту 1433.  Дополнительные сведения см. в разделах [Брандмауэр базы данных SQL Azure][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] и [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Подключения к хранилищу данных SQL шифруются по умолчанию.  Изменение параметров подключения для отключения шифрования игнорируется.

## <a name="authentication"></a>Аутентификация
В процессе аутентификации предлагается подтвердить личность пользователя при подключении к базе данных. Сейчас хранилище данных SQL поддерживает аутентификацию SQL с использованием имени пользователя и пароля, а также Azure Active Directory. 

При создании логического сервера для базы данных вы указали имя для входа "Администратор сервера" и пароль. Используя эти учетные данные, можно выполнить проверку подлинности SQL Server для любой базы данных на этом сервере в качестве владельца базы данных (или dbo).

Но рекомендуется, чтобы пользователи вашей организации использовали для проверки подлинности другую учетную запись. Это позволит ограничить разрешения, предоставляемые приложению, и снизить риски вредоносных действий в случае, если приложение уязвимо для атак путем внедрения кода SQL. 

Чтобы создать пользователя, прошедшего аутентификацию SQL Server, подключитесь к базе данных **master** на сервере с именем для входа администратора сервера и создайте новое имя для входа на сервер.  Кроме того, рекомендуется создать в базе данных master учетную запись для пользователей хранилища данных SQL Azure. Это позволит пользователям входить в систему с помощью таких инструментов, как среда SSMS, без указания имени базы данных.  Кроме того, это позволяет использовать обозреватель объектов для просмотра всех баз данных в SQL Server.

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Затем подключитесь к **базе данных хранилища данных SQL** с именем для входа администратора сервера и создайте пользователя базы данных на для только что созданного имени для входа на сервер.

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Если пользователь будет выполнять дополнительные операции, такие как создание имен для входа или баз данных, ему также потребуется назначить роли `Loginmanager` и `dbmanager` в базе данных master. Дополнительные сведения об этих дополнительных ролях и аутентификации в Базе данных SQL см. в статье [Проверка подлинности и авторизация в базе данных SQL: предоставление доступа][Managing databases and logins in Azure SQL Database].  Дополнительные сведения об использовании Azure AD для хранилища данных SQL см. в статье [Аутентификация в хранилище данных SQL Azure][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Авторизация
Авторизация подразумевает набор действий, которые можно выполнять в базе данных хранилища SQL Azure. Этот набор действий определяют разрешения учетной записи пользователя и присвоенные ей роли. Обычно пользователям рекомендуется предоставлять наименьшие необходимые привилегии. Хранилищем данных SQL Azure можно легко управлять с использованием ролей в T-SQL.

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

Учетной записи администратора сервера, которая используется для подключения, присвоена роль db_owner, обладатель которой может выполнять любые действия в базе данных. Сохраните эту учетную запись для развертывания обновлений схемы и выполнения других действий по управлению. Для подключения к базе данных из приложения с использованием наименьших привилегий, необходимых приложению, используйте учетную запись "ApplicationUser" с более ограниченными разрешениями.

Существуют способы еще больше ограничить действия пользователя с Базой данных SQL Azure.

* Детальная настройка [разрешений][Permissions] позволяет указать операции, которые можно выполнять с отдельными столбцами, таблицами, представлениями, процедурами и другими объектами в базе данных. Используйте детализированные разрешения для обеспечения наивысшего уровня контроля и предоставления минимальных необходимых разрешений. Система детализированных разрешений является довольно сложной, поэтому для ее эффективного использования потребуется пройти дополнительное обучение.
* Чтобы создать учетные записи пользователей приложения с более широкими правами или учетные записи управления с меньшим набором разрешений, можно использовать [роли базы данных][Database roles], отличные от db_datareader и db_datawriter. С помощью встроенных фиксированных ролей базы данных можно легко присваивать разрешения, однако это может привести к предоставлению лишних разрешений.
* Чтобы ограничить действия, выполняемые в базе данных, можно использовать [хранимые процедуры][Stored procedures].

Управление базами данных и логическими серверами на классическом портале Azure или с помощью API-интерфейса диспетчера ресурсов Azure контролируется путем назначения ролей для учетной записи пользователя портала. Дополнительные сведения об этом см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Шифрование
Прозрачное шифрование данных хранилища данных SQL Azure помогает защититься от вредоносных атак благодаря шифрованию и расшифровке неактивных данных в реальном времени.  При шифровании базы связанные резервные копии и файлы журналов транзакций шифруются без необходимости вносить изменения в приложения. При использовании TDE хранилище всей базы данных шифруется с помощью симметричного ключа, который называется ключом шифрования базы данных. В Базе данных SQL ключ шифрования базы данных защищается встроенным сертификатом сервера. Каждый сервер Базы данных SQL обладает уникальным встроенным сертификатом. Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней. Алгоритм шифрования, используемый в хранилище данных SQL, это AES-256. Общее описание функции TDE см. в статье [Прозрачное шифрование данных (TDE)][Transparent Data Encryption].

Базу данных можно зашифровать с помощью [портала Azure][Encryption with Portal] или [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения и примеры подключения к хранилищу данных SQL с различными протоколами см. в статье [Подключение к хранилищу данных SQL Azure][Connect to SQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect to SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

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
