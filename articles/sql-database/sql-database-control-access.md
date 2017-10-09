---
title: "tooAzure aaaGranting доступа к базе данных SQL | Документы Microsoft"
description: "Дополнительные сведения о предоставлении доступа tooMicrosoft базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Контроль доступа к базе данных SQL Azure
безопасность tooprovide, база данных SQL управляет доступом с правилами брандмауэра ограничение подключение по IP-адресу механизмов проверки подлинности, требующие tooprove пользователей их идентификаторов и механизмы авторизации ограничений toospecific действий пользователей и данных. 

> [!IMPORTANT]
> Обзор функций безопасности hello базы данных SQL см. в разделе [Обзор безопасности SQL](sql-database-security-overview.md). Ознакомьтесь с руководством [Защита базы данных SQL Azure](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Брандмауэр и правила брандмауэра
База данных SQL Microsoft Azure предоставляет службу реляционных баз данных для Azure и других интернет-приложений. toohelp защитить свои данные, брандмауэр не все сервера базы данных access tooyour, пока вы не укажете компьютеры, на которых есть разрешение. Hello брандмауэр предоставляет доступ toodatabases основании hello, рассчитанные на IP-адреса каждого запроса. Дополнительные сведения см. в статье [Обзор правил брандмауэра базы данных SQL Azure](sql-database-firewall-configure.md).

Hello службы базы данных SQL Azure доступна только через TCP-порт 1433. tooaccess базы данных SQL с компьютера, убедитесь, что брандмауэр клиентского компьютера разрешает исходящие соединения через TCP-порт 1433. Заблокируйте входящие подключения по протоколу TCP через порт 1433, если они не требуются для других приложений. 

В рамках процесса подключения hello подключений от виртуальных машин Azure, перенаправленный tooa другой IP-адрес и порт, уникальный для каждой рабочей роли. Hello используется порт в диапазоне hello от 11000 too11999. Дополнительные сведения о TCP-портах см. в статье [Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Аутентификация

База данных SQL поддерживает два типа аутентификации:

* **Проверка подлинности SQL** с использованием имени пользователя и пароля. При создании hello логического сервера для базы данных, имя входа «администратор сервера» указано имя пользователя и пароль. Используя эти учетные данные, вы можете проверять подлинность tooany базы данных на этом сервере как владелец базы данных hello, или «dbo». 
* **Проверка подлинности Azure Active Directory** с использованием удостоверений, контролируемых Azure Active Directory, которая поддерживается управляемыми и интегрированными доменами. [По возможности](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) используйте проверку подлинности Active Directory (встроенная безопасность). Если вы хотите toouse проверки подлинности Azure Active Directory, необходимо создать другой администратор сервера называется hello «Admin Azure AD», что допускается tooadminister Azure AD — пользователи и группы. Этот администратор также может выполнять все операции, доступные обычному администратору. В разделе [подключении базы данных с использованием Azure Active Directory проверки подлинности tooSQL](sql-database-aad-authentication.md) для Пошаговое руководство по toocreate tooenable администрирования Azure AD проверки подлинности Azure Active Directory.

Hello компонент Database Engine закрывает подключения, которые простаивать в течение более чем за 30 минут. Здравствуйте, соединения необходимо входа еще раз, прежде чем можно будет использовать. Постоянно tooSQL активных подключений базы данных требуется повторная авторизация (выполняется ядром СУБД hello) каждые 10 часов. компонент database engine Hello предпринимается повторная авторизация с использованием пароля изначально отправлено hello и вмешательство пользователя не требуется. Для повышения производительности при сбросе пароля в базе данных SQL, hello соединение не будет выполнена повторная проверка подлинности, даже если сбрасывать hello соединение из-за tooconnection пулов. Это отличается от поведения hello в локальной среде SQL Server. Если hello пароль был изменен с момента подключения hello изначально был авторизован, необходимо завершить подключение hello и установить новое соединение с помощью hello новый пароль. Пользователь с hello `KILL DATABASE CONNECTION` разрешение может явным образом завершить tooSQL подключение базы данных с помощью hello [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) команды.

Учетные записи пользователей могут быть созданы в базе данных master hello и могут быть предоставлены разрешения во всех базах данных на сервере hello, или они могут быть созданы в базе данных hello сам (называемые автономных пользователей). Сведения о создании имен для входа и управлении ими см. в [этой статье](sql-database-manage-logins.md). переносимость tooenhance и scalabilty, используют масштабируемость tooenhance пользователей автономной базы данных. Дополнительные сведения об автономных пользователях см. в статьях [Пользователи автономной базы данных — создание переносимой базы данных](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) и [Автономные базы данных](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

Рекомендуется в приложении следует использовать выделенную учетную запись tooauthenticate--таким образом, можно ограничить hello разрешения, предоставленные toohello приложения и уменьшить риски hello вредоносных действий в случае атаки SQL injection уязвимых tooa код приложения атаки. Hello рекомендуется toocreate [пользователя автономной базы данных](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), что позволяет tooauthenticate вашего приложения непосредственно toohello базы данных. 

## <a name="authorization"></a>Авторизация

Авторизация ссылается toowhat может делать пользователь в базе данных SQL Azure и осуществляется с помощью учетной записи пользователя базы данных [членство в ролях](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) и [разрешения на уровне объекта](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Рекомендуется необходимо предоставить пользователям hello наименьшими необходимыми правами. Учетная запись администратора Hello сервера с которым соединение является членом роли db_owner, имеющая центра toodo все условия в базе данных hello. Сохраните эту учетную запись для развертывания обновлений схемы и выполнения других действий по управлению. Использовать учетную запись «ApplicationUser» hello с более ограниченные разрешения tooconnect из базы данных приложения toohello с hello наименьшие права доступа, необходимые для приложения. Дополнительные сведения см. в статье [Проверка подлинности и авторизация в базе данных SQL: предоставление доступа](sql-database-manage-logins.md).

Как правило, только администраторы должны получить доступ к toohello `master` базы данных. Постоянный доступ tooeach пользовательской базы данных должен быть создан в каждой базе данных, то пользователи автономной базы данных без прав администратора. При использовании пользователей автономной базы данных, не обязательно toocreate учетных записей в hello `master` базы данных. Дополнительные сведения см. в статье [Пользователи автономной базы данных — создание переносимой базы данных](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

Вам следует ознакомиться с hello следующие атрибуты, которые можно использовать toolimit или повысить права:   
* [Олицетворение](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) и [Подписание модулей](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) может быть используется toosecurely повысить права временно.
* [Безопасности на уровне строк](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) может использоваться, чтобы ограничить доступ пользователя к строкам.
* [Маскирование данных](sql-database-dynamic-data-masking-get-started.md) может быть используется toolimit раскрытия конфиденциальных данных.
* [Хранимые процедуры](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) может быть используется toolimit hello действия, которые могут быть выполнены в базе данных hello.

## <a name="next-steps"></a>Дальнейшие действия

- Обзор функций безопасности hello базы данных SQL см. в разделе [Обзор безопасности SQL](sql-database-security-overview.md).
- toolearn Дополнительные сведения о правилах брандмауэра. в разделе [правила брандмауэра](sql-database-firewall-configure.md).
- toolearn о пользователях и имена входа, в разделе [Управление именами входа](sql-database-manage-logins.md). 
- Описание упреждающего мониторинга см. во вводных статьях об [аудите базы данных](sql-database-auditing.md) и [системе обнаружения угроз базы данных SQL](sql-database-threat-detection.md).
- Ознакомьтесь с руководством [Защита базы данных SQL Azure](sql-database-security-tutorial.md).
