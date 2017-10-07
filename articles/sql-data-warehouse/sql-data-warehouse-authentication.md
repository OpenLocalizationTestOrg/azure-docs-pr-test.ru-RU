---
title: "aaaAuthentication tooAzure хранилище данных SQL | Документы Microsoft"
description: "Azure Active Directory (AAD) и SQL Server authentication tooAzure хранилище данных SQL."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Проверка подлинности tooAzure хранилище данных SQL
> [!div class="op_single_selector"]
> * [Обзор безопасности](sql-data-warehouse-overview-manage-security.md)
> * [Аутентификация](sql-data-warehouse-authentication.md)
> * [Шифрование (портал)](sql-data-warehouse-encryption-tde.md)
> * [Шифрование (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooSQL tooconnect хранилища данных, необходимо передать в учетных данных безопасности для проверки подлинности. После установки подключения некоторые его параметры настраиваются при установке сеанса запроса.  

Дополнительные сведения о безопасности и как хранилище данных tooyour tooenable соединения, в разделе [защиты базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Аутентификация SQL
tooSQL tooconnect хранилища данных, необходимо предоставить hello следующую информацию:

* Полное имя сервера
* Тип проверки подлинности SQL
* Имя пользователя
* Пароль
* База данных по умолчанию (необязательно)

По умолчанию соединения toohello *master* базы данных и не пользовательскую базу данных. tooconnect tooyour пользовательской базы данных, вы можете toodo одно из следующих действий:

* Укажите базу данных по умолчанию hello, при регистрации сервера в обозревателе объектов SQL Server в SSDT и SSMS, или в строке подключения приложения hello. Например включать параметр InitialCatalog hello для подключения ODBC.
* Выделите hello пользовательской базы данных перед созданием сеанса в SSDT.

> [!NOTE]
> Здравствуйте, инструкции Transact-SQL **используйте MyDatabase;** не поддерживается для изменения hello базы данных для подключения. Рекомендации при подключении tooSQL хранилища данных с помощью SSDT, см. в разделе toohello [запроса с помощью Visual Studio] [ Query with Visual Studio] статьи.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Аутентификация Azure Active Directory (AAD)
[Azure Active Directory] [ What is Azure Active Directory] проверка подлинности — это механизм подключения tooMicrosoft хранилище данных SQL Azure с помощью удостоверений в Azure Active Directory (Azure AD). С помощью проверки подлинности Azure Active Directory можно централизованно управлять hello удостоверений пользователей базы данных и другие службы Майкрософт, в одном централизованном месте. Централизованное управление идентификатор представляет собой единое место пользователей toomanage хранилище данных SQL и упрощает управление разрешениями. 

### <a name="benefits"></a>Преимущества
Преимущества Azure Active Directory:

* Предоставляет альтернативные tooSQL проверки подлинности сервера.
* Позволяет остановить hello увеличением числа пользователей на серверах базы данных.
* изменение паролей в одном расположении;
* управление разрешениями базы данных с помощью внешних групп (AAD);
* возможность исключить хранение паролей с помощью встроенной проверки подлинности Windows и других видов аутентификации, поддерживаемых Azure Active Directory;
* Использует содержатся идентификаторы tooauthenticate пользователей базы данных на уровне базы данных hello.
* Поддерживает проверку подлинности на основе токена для приложений, соединяющихся tooSQL хранилища данных.
* поддержка Многофакторной Идентификации с помощью универсальной аутентификации Active Directory для SQL Server Management Studio. Описание Multi-Factor Authentication см. в статье [Поддержка SSMS в Azure AD MFA для базы данных SQL и хранилища данных SQL](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory является сравнительно новым компонентом и имеет некоторые ограничения. tooensure, что Azure Active Directory, подходит для вашей среды. в разделе [функции Azure AD и ограничения][Azure AD features and limitations], в частности hello Дополнительные соображения.
> 
> 

### <a name="configuration-steps"></a>Этапы настройки
Выполните эти шаги tooconfigure Azure Active Directory authentication.

1. Создание и заполнение каталога Azure Active Directory
2. Необязательно: Связать или изменение hello active directory, который сейчас связан с подпиской Azure
3. Создание администратора Azure Active Directory для хранилища данных SQL Azure
4. Настройка клиентских компьютеров
5. Создать пользователей автономной базы данных в вашей базы данных сопоставлен tooAzure удостоверений AD
6. Подключение tooyour хранилища данных с помощью удостоверений Azure AD

Сейчас пользователи Azure Active Directory не отображаются в обозревателе объектов SSDT. Чтобы избежать этого, просмотра сведений о пользователях hello в [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Найти сведения о hello
* Hello действия tooconfigure и использовать Azure Active Directory authentication практически идентичны для базы данных SQL Azure и хранилище данных SQL Azure. Выполните hello подробные инструкции в разделе hello [tooSQL подключение базы данных или SQL данные хранилища с использованием Azure Active Directory проверки подлинности](../sql-database/sql-database-aad-authentication.md).
* Создание пользовательских ролей базы данных и Добавление ролей toohello пользователей. Предоставьте роли toohello Гранулярные разрешения. Дополнительные сведения см. в разделе [Приступая к работе с разрешениями Database Engine](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Дальнейшие действия
toostart запросов хранилищ данных в Visual Studio и других приложений, в разделе [запроса с помощью Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
