---
title: "Проверка подлинности Active Directory aaaAzure — SQL Azure (Обзор) | Документы Microsoft"
description: "Дополнительные сведения о том, как toouse Azure Active Directory для проверки подлинности в базе данных SQL и хранилищем данных SQL"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Использование аутентификации Azure Active Directory для аутентификации с помощью базы данных SQL или хранилища данных SQL
Проверка подлинности Azure Active Directory — это механизм подключения tooMicrosoft базы данных SQL Azure и [хранилище данных SQL](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) с помощью удостоверений в Azure Active Directory (Azure AD). С помощью проверки подлинности Azure AD можно централизованно управлять hello удостоверений пользователей базы данных и другие службы Майкрософт, в одном централизованном месте. Централизованное управление идентификатор представляет собой единое место toomanage пользователей базы данных и упрощает управление разрешениями. Hello следующие преимущества:

* Он предоставляет альтернативные tooSQL проверки подлинности сервера.
* Позволяет остановить hello увеличением числа пользователей на серверах базы данных.
* изменение паролей в одном расположении;
* клиенты могут управлять разрешениями базы данных с помощью внешних групп (AAD);
* возможность исключить хранение паролей с помощью встроенной проверки подлинности Windows и других видов проверки подлинности, поддерживаемых Azure Active Directory;
* Проверки подлинности Azure AD использует удостоверения tooauthenticate пользователей автономной базы данных на уровне базы данных hello.
* Azure AD поддерживает проверку подлинности на основе токена для приложений, соединяющихся tooSQL базы данных.
* Azure AD поддерживает проверку подлинности с использованием AD FS (федерация доменов) или собственную проверку подлинности с помощью имени пользователя и пароля для локального каталога Azure Active Directory без синхронизации домена.  
* Azure AD поддерживает подключения из SQL Server Management Studio, использующие универсальную проверку подлинности Active Directory, в том числе многофакторную идентификацию (MFA).  MFA обеспечивает надежную аутентификацию с использованием ряда простых вариантов проверки посредством телефонного звонка, текстового сообщения, смарт-карты с ПИН-кодом или уведомления в мобильном приложении. Дополнительные сведения см. в разделе [Поддержка SSMS в Azure AD MFA для базы данных SQL и хранилища данных SQL](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Подключение tooSQL сервера, работающего на Виртуальной машине Azure не поддерживается с использованием учетной записи Azure Active Directory. Вместо этого используйте учетную запись домена Active Directory.  

действия по настройке Hello включают следующие процедуры tooconfigure hello и использование проверки подлинности Azure Active Directory.

1. Создайте и заполните каталог Azure AD.
2. Необязательно: Связать или изменение hello active directory, который сейчас связан с подпиской Azure.
3. Создайте учетную запись администратора Azure Active Directory для сервера Azure SQL Server или [хранилища данных SQL Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Настройте клиентские компьютеры.
5. Создайте пользователей автономной базы данных в вашей базы данных сопоставлен tooAzure удостоверений AD.
6. Подключение tooyour базы данных с помощью удостоверений Azure AD.

> [!NOTE]
> toolearn как toocreate и заполнить Azure AD и настройте с базой данных SQL Azure и хранилище данных SQL Azure AD см. в разделе [Настройка Azure AD с базой данных SQL Azure](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Архитектура доверия
Следующая общая диаграмма Hello показана архитектура решения hello использования проверки подлинности в Azure AD с базой данных SQL Azure. Hello же принципы применяются tooSQL хранилища данных. считается toosupport собственного пользовательского пароля Azure AD только часть облака hello и базы данных SQL Azure AD и Azure. toosupport федеративной проверки подлинности (или пароль для учетных данных Windows), при обмене данными hello с блоком служб федерации Active Directory. Hello стрелки обозначают пути обмена данными.

![схема проверки подлинности aad][1]

Hello следующая схема указывает федерации hello, доверия и отношения, обеспечивающие клиенту базы данных tooa tooconnect, отправляя маркер размещения. токен Hello проходит проверку подлинности Azure AD и является доверенным для hello базы данных. Клиент 1 может представлять каталог Azure AD с собственными пользователями или федеративными пользователями. Клиент 2 представляет возможное решение, включая импортированных пользователей. В этом примере пользователи импортированы из федеративной службы Azure Active Directory, при этом службы ADFS синхронизированы с Azure Active Directory. Очень важно, что требуется toounderstand, доступ к базе данных tooa с использованием проверки подлинности Azure AD, hello размещение подписки — связанные toohello Azure AD. Hello же подписка должна быть используется toocreate hello SQL Server размещения hello базы данных SQL Azure или хранилище данных SQL.

![отношение подписки][2]

## <a name="administrator-structure"></a>Структура администраторов
При использовании проверки подлинности Azure AD, существует две учетные записи администратора для сервера базы данных SQL hello. Здравствуйте исходного SQL Server администратор и администратор hello Azure AD. Hello же принципы применяются tooSQL хранилища данных. Только администратор hello, на основе учетной записи Azure AD можно создать hello первый пользователь базы данных Azure AD, которые содержатся в базе данных пользователя. Имя входа администратора Hello Azure AD может быть пользователя Azure AD или группе Azure AD. Здравствуйте, администратор имеет учетную запись группы, может использоваться каким-либо участником группы, включение нескольких администраторов Azure AD для экземпляра SQL Server hello. С помощью учетной записи группы, как администратор улучшает управляемость, позволяя toocentrally добавлять и удалять членов группы в Azure AD, не изменяя hello пользователей или разрешений в базе данных SQL. За один раз можно настроить только одного администратора Azure AD (пользователя или группу).

![структура администраторов][3]

## <a name="permissions"></a>Разрешения
toocreate новых пользователей, необходимо иметь hello `ALTER ANY USER` разрешения в базе данных hello. Hello `ALTER ANY USER` tooany пользователя базы данных могут быть предоставлены разрешения. Hello `ALTER ANY USER` разрешение также удерживаемые hello учетные записи администратора сервера и пользователи базы данных с hello `CONTROL ON DATABASE` или `ALTER ON DATABASE` разрешения для этой базы данных и члены hello `db_owner` роли базы данных.

toocreate пользователя автономной базы данных в базе данных SQL Azure или хранилище данных SQL, необходимо подключиться toohello базу данных, используя удостоверение Azure AD. База данных toohello toocreate hello первого автономной базы данных пользователя, необходимо подключиться с помощью администратор Azure AD (который является владельцем базы данных hello hello). См. шаги 4 и 5 ниже. Проверка подлинности Azure AD можно только в том случае, если было создано Здравствуйте, администратор Azure AD для базы данных SQL Azure или хранилище данных SQL server. Если Здравствуйте, администратор Azure Active Directory был удален с сервера hello, существующих пользователей Azure Active Directory, ранее созданных в SQL Server больше не может подключиться toohello базы данных, используя свои учетные данные Azure Active Directory.

## <a name="azure-ad-features-and-limitations"></a>Функции и ограничения Azure AD
можно подготовить Hello следующие члены Azure AD в Azure SQL server или хранилища данных SQL:

* Собственные элементы: элемент, созданные в Azure AD в управляемый домен hello, или в домене клиента. Дополнительные сведения см. в разделе [добавить собственные tooAzure имя домена AD](../active-directory/active-directory-add-domain.md).
* Федеративные члены домена — члены, созданные в Azure AD с федеративным доменом. Дополнительные сведения см. в статье [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/) (Microsoft Azure теперь поддерживает федерацию с Windows Server Active Directory).
* Импортированные члены из других каталогов Azure AD, являющиеся собственными или федеративными членами домена.
* Группы Active Directory, созданные как группы безопасности.

Учетные записи Майкрософт (например, outlook.com, hotmail.com, live.com) и гостевые учетные записи (например, gmail.com, yahoo.com) не поддерживаются. Если вы можете войти слишком[https://login.live.com](https://login.live.com) с помощью hello учетную запись и пароль, а затем вы используете учетную запись Майкрософт, который не поддерживается для проверки подлинности Azure AD для базы данных SQL Azure или хранилище данных SQL Azure.

## <a name="connecting-using-azure-ad-identities"></a>Подключение с использованием удостоверений Azure AD

Проверка подлинности Azure Active Directory поддерживает следующие методы соединения tooa базы данных с помощью удостоверений Azure AD hello:

* с использованием встроенной проверки подлинности Windows;
* Использование имени субъекта-пользователя и пароля Azure AD
* Использование маркера проверки подлинности приложения

### <a name="additional-considerations"></a>Дополнительные замечания

* управляемость tooenhance, рекомендуется подготовить выделенный Azure AD группы с правами администратора.   
* За один раз можно настроить только одну учетную запись администратора Azure AD (пользователя или группу) для сервера Azure SQL Server или хранилища данных SQL Azure.   
* Только администратор Azure AD для SQL Server можно сначала подключиться toohello Azure SQL server или хранилище данных SQL Azure, используя учетную запись Azure Active Directory. Здравствуйте, администратор Active Directory можно настроить последующих Azure AD пользователи базы данных.   
* Рекомендуется установить время ожидания too30 hello соединения с.   
* Проверку подлинности Azure Active Directory поддерживают SQL Server 2016 Management Studio и SQL Server Data Tools для Visual Studio 2015 (версии 14.0.60311.1, выпущенной в апреле 2016 г., или более поздней). (Проверка подлинности azure AD поддерживается hello **поставщик данных .NET Framework для SQL Server**; по крайней мере версии .NET Framework 4.6). Поэтому hello последние версии этих средств и приложений уровня данных (DAC и bacpac) можно использовать проверку подлинности Azure AD.   
* [ODBC версии 13.1](https://www.microsoft.com/download/details.aspx?id=53339) поддерживает проверку подлинности Azure Active Directory, однако `bcp.exe` не может подключаться с использованием проверки подлинности Azure Active Directory, так как использует устаревший поставщик ODBC.   
* `sqlcmd`поддерживает проверки подлинности Azure Active Directory, начиная с версии 13.1 предоставляемые hello [центра загрузки](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools для Visual Studio 2015 требуется по крайней мере hello апреля 2016 г. версия hello Data Tools (версия 14.0.60311.1). Сейчас пользователи Azure AD не отображаются в обозревателе объектов SSDT. Чтобы избежать этого, просмотра сведений о пользователях hello в [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [Драйвер Microsoft JDBC 6.0 для SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) поддерживает проверку подлинности Azure AD. Кроме того, в разделе [Настройка параметров соединения hello](https://msdn.microsoft.com/library/ms378988.aspx).   
* PolyBase не поддерживает проверку подлинности Azure AD.   
* Проверки подлинности Azure AD поддерживается для базы данных SQL Azure portal hello **Импорт базы данных** и **Экспорт базы данных** колонок. Импорт и экспорт с помощью проверки подлинности Azure AD из hello команду PowerShell также поддерживается.   
* Проверка подлинности Azure AD для базы данных SQL и хранилища данных SQL поддерживается с помощью CLI. Сведения о настройке и управлении Azure AD см. в статьях [Настройка аутентификации Azure Active Directory и управление ею с использованием базы данных SQL или хранилища данных SQL](sql-database-aad-authentication-configure.md) и [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Дальнейшие действия
- toolearn как toocreate и заполнить Azure AD и затем настроить Azure AD с базой данных SQL Azure или хранилище данных SQL Azure см. в разделе [Настройка и управление проверкой подлинности Azure Active Directory с базой данных SQL или хранилище данных SQL](sql-database-aad-authentication-configure.md).
- Общие сведения о доступе к базе данных SQL и управлении ею см. в статье [Контроль доступа к базе данных SQL Azure](sql-database-control-access.md).
- Общие сведения об именах для входа, пользователях и ролях базы данных в базе данных SQL см. в статье [Предоставление доступа к базе данных и управление им](sql-database-manage-logins.md).
- Дополнительные сведения о субъектах базы данных см. в [этой статье](https://msdn.microsoft.com/library/ms181127.aspx).
- Дополнительные сведения о ролях баз данных см. в статье [Роли уровня базы данных](https://msdn.microsoft.com/library/ms189121.aspx).
- Дополнительные сведения о правилах брандмауэра см. в статье [Обзор правил брандмауэра базы данных SQL Azure](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

