---
title: "aaaMulti двойной проверки подлинности — Azure SQL | Документы Microsoft"
description: "Использование Многофакторной идентификации с SSMS для базы данных SQL и хранилища данных SQL."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Универсальная проверка подлинности для Базы данных SQL и хранилища данных SQL (поддержка SSMS для MFA)
База данных SQL Azure и хранилище данных SQL Azure поддерживают подключения из SQL Server Management Studio (SSMS) с использованием *универсальной проверки подлинности Active Directory*. 
**Загрузите hello последняя версия SSMS** — на клиентском компьютере hello, загрузить последнюю версию SSMS, hello [загрузить SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Для всех функций hello в этом разделе используйте по крайней мере июля 2017 г., версия 17,2.  Hello последних диалогового соединения, выглядит следующим образом: ![1mfa универсального подключения](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "поле имени пользователя выполняемой hello.")  

## <a name="hello-five-authentication-options"></a>Параметры проверки подлинности Hello пяти  
- Универсальной проверки подлинности Active Directory поддерживает два метода проверки подлинности неинтерактивной hello (`Active Directory - Password` проверки подлинности и `Active Directory - Integrated` проверки подлинности). Неинтерактивные методы аутентификации (`Active Directory - Password` и `Active Directory - Integrated`) можно использовать во множестве различных приложений (ADO.NET, JDBC, ODBC и т. д.). При использовании этих двух методов никогда не отображаются всплывающие диалоговые окна.

- Аутентификация `Active Directory - Universal with MFA` — это интерактивный метод, который также поддерживает *Многофакторную идентификацию Azure* (MFA). Azure MFA помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему. Оно обеспечивает надежную проверку подлинности с диапазоном параметры простой проверки (телефонный звонок, текстовое сообщение, смарт-карты с ПИН-кода или уведомление мобильного приложения), позволяя пользователям toochoose hello метод обеспечивается. Интерактивная MFA с использованием Azure AD может привести к появлению всплывающего диалогового окна для реализации проверки.

Общие сведения о многофакторной идентификации см. в [этой статье](../multi-factor-authentication/multi-factor-authentication.md).
Инструкции по настройке см. в разделе [Настройка Многофакторной идентификации Базы данных SQL Azure для SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Параметр доменного имени или идентификатора клиента Azure AD   

Начиная с версии [SSMS версия 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), пользователи, которые импортируются в hello текущего Active Directory из других активных каталогов Azure как гостевых пользователей можно указать имя домена hello Azure AD, или идентификатор клиента при подключении. К гостевым пользователям относятся пользователи, приглашенные из других каталогов Azure AD, учетные записи Майкрософт, такие как outlook.com, hotmail.com и live.com, или другие учетные записи, например, gmail.com. Эти сведения позволяют **Active Directory универсальной с проверкой подлинности многофакторной проверки Подлинности** tooidentify hello правильный центр проверки подлинности. Этот параметр также является обязательным toosupport учетные записи Майкрософт (MSA), такие как outlook.com, hotmail.com, live.com или учетные записи не являются MSA. Эти пользователи, которые хотят toobe проверку подлинности с помощью универсальной проверки подлинности необходимо ввести их имена домена Azure AD или клиент по идентификатору. Этот параметр представляет hello текущего Azure AD домена имя или клиента идентификатор приветствия сервера Azure, связанная с. Например, если сервер Azure связан с доменом Azure AD `contosotest.onmicrosoft.com` где пользователя `joe@contosodev.onmicrosoft.com` размещается в виде импортированных пользователей из домена Azure AD `contosodev.onmicrosoft.com`, hello tooauthenticate необходимо указать имя домена, этот пользователь является `contosotest.onmicrosoft.com`. Когда пользователь hello собственного пользователь tooAzure hello Azure AD связанный сервер и не является Управляемой учетной записи, не ИД домена имя или клиента не требуется. параметр tooenter hello (начиная с версии 17,2 SSMS) в hello **подключения tooDatabase** диалоговое окно, в диалоговом окне завершения hello при выборе **Active Directory — универсальная с многофакторной проверки Подлинности** проверки подлинности Нажмите кнопку **параметры**, полный hello **имя пользователя** , а затем щелкните hello **свойства соединения** вкладки. Проверьте hello **код домена имя или клиента AD** и укажите центра проверки подлинности, такие как имя домена hello (**contosotest.onmicrosoft.com**) или hello GUID идентификатора клиента hello.  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Поддерживает toobusiness бизнес Azure AD   
Поддержка сценариев Azure AD B2B как гости пользователей Azure AD (см. [возможности совместной работы Azure B2B](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) можно подключиться только как часть членов группы в текущей Azure AD и сопоставляется вручную tooSQL базы данных и хранилище данных SQL с помощью Transact-SQL "hello" `CREATE USER` инструкции в данной базе данных. Например если `steve@gmail.com` — приглашенных tooAzure AD `contosotest` (с доменом Azure Active Directory hello `contosotest.onmicrosoft.com`), группу Azure AD, например `usergroup` должны быть созданы в Azure AD, который содержит hello hello `steve@gmail.com` член. Затем эту группу для конкретной базы данных (т. е. MyDatabase) должен создать администратор SQL Azure AD или владелец базы данных Azure AD, выполнив инструкцию `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` Transact-SQL. После создания пользователя базы данных hello hello пользователя `steve@gmail.com` входа слишком`MyDatabase` с помощью параметра authentication SSMS hello `Active Directory – Universal with MFA support`. Hello группа пользователей, по умолчанию имеет только hello подключения разрешения и любого дальнейший доступ данные которого будут предоставлены hello toobe обычным способом. Обратите внимание, что пользователь `steve@gmail.com` как Гость должен установите флажок "hello" и добавьте имя домена hello AD `contosotest.onmicrosoft.com` в hello SSMS **свойство соединения** диалоговое окно. Hello **код домена имя или клиента AD** параметр поддерживается только для hello Universal с параметрами подключения многофакторной проверки Подлинности, в противном случае он неактивен.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Ограничения универсальной аутентификации для базы данных SQL и хранилища данных SQL
* Среда SSMS и SqlPackage.exe являются только средства hello в настоящее время включена для многофакторной проверки Подлинности через универсальной проверки подлинности Active Directory.
* SSMS версии 17.2 поддерживает одновременный доступ нескольких пользователей с помощью универсальной аутентификации с MFA. Версия 17.0 и 17,1, ограниченное журнала в экземпляре SSMS, с помощью учетной записи универсальной проверкой подлинности tooa один Azure Active Directory. toolog в другой учетной записи Azure AD, необходимо использовать другой экземпляр среды SSMS. (Это ограничение является ограниченной tooActive универсальной проверкой подлинности каталога; вы можете войти toodifferent серверов, с помощью проверки подлинности паролей Active Directory, встроенная проверка подлинности Active Directory или проверки подлинности SQL Server).
* SSMS поддерживает универсальную аутентификацию Active Directory для отображения обозревателя объектов, редактора запросов и хранилища запросов.
* SSMS версии 17.2 поддерживает мастер DacFx для экспорта, извлечения и развертывания данных базы данных. После проверки подлинности определенным пользователем через диалоговое окно приветствия начальной проверки подлинности, с помощью универсальной проверки подлинности hello мастер DacFx функции hello таким же образом, как и для всех других методов проверки подлинности.
* Hello конструкторе таблиц SSMS не поддерживает универсальные проверки подлинности.
* Для универсальной аутентификации Active Directory не требуется дополнительное программное обеспечение, за исключением того, что необходимо использовать поддерживаемую версию SSMS.  
* последнюю версию ADAL.dll 3.13.9 доступных выпущен обновленный tooits была версия библиотеки проверки подлинности Active Directory (ADAL) Hello для универсальной проверкой подлинности. Ознакомьтесь с [библиотекой аутентификации Active Directory версии 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Дальнейшие действия

- Инструкции по настройке см. в разделе [Настройка Многофакторной идентификации Базы данных SQL Azure для SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Предоставление другим пользователям доступ к базе данных tooyour: [проверки подлинности базы данных SQL и авторизации: предоставление доступа](sql-database-manage-logins.md)  
- Убедитесь, что другие пользователи могут подключаться через брандмауэр hello: [Настройка базы данных SQL Azure уровня сервера правило брандмауэра с помощью hello портал Azure](sql-database-configure-firewall-settings.md)  
- [Настройка аутентификации Azure Active Directory и управление ею с использованием базы данных SQL или хранилища данных SQL](sql-database-aad-authentication-configure.md)  
- [Платформа приложения уровня данных Microsoft® SQL Server® (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Импорт файла BACPAC tooa новой базы данных SQL Azure](../sql-database/sql-database-import.md)  
- [Экспорт файла BACPAC tooa базы данных Azure SQL](../sql-database/sql-database-export.md)  
- Интерфейс C# [IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
