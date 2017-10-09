---
title: "Проверка подлинности Azure Active Directory aaaConfigure - SQL | Документы Microsoft"
description: "Узнайте, как tooconnect tooSQL базы данных и хранилище данных SQL с помощью проверки подлинности Azure Active Directory."
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
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Настройка аутентификации Azure Active Directory и управление ею с использованием базы данных SQL или хранилища данных SQL

В этой статье показано, как toocreate и заполнить Azure AD, а затем использовать Azure AD с базой данных SQL Azure и хранилище данных SQL. Обзор см. в статье [Подключение к базе данных SQL или хранилищу данных SQL c использованием проверки подлинности Azure Active Directory](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Подключение tooSQL сервера, работающего на Виртуальной машине Azure не поддерживается с использованием учетной записи Azure Active Directory. Вместо этого используйте учетную запись домена Active Directory.

## <a name="create-and-populate-an-azure-ad"></a>Создание и заполнение каталога Azure AD
Создайте каталог Azure AD и заполните его пользователями и группами. Azure AD может быть управляемого домена hello первоначальный домен Azure AD. Azure AD также может быть локальной службы Active Directory домена, включена в федерацию с Azure AD hello.

Дополнительные сведения см. в разделе [интеграция локальных удостоверений с Azure Active Directory](../active-directory/active-directory-aadconnect.md), [добавить собственные tooAzure имя домена AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure теперь поддерживает федерацию с Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [администрирование каталога Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [управление Azure AD с помощью Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), и [гибридное удостоверение Необходимые порты и протоколы](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Необязательно: Связать или изменение hello active directory, который сейчас связан с подпиской Azure
tooassociate базы данных с каталогом hello Azure AD для вашей организации, сделать каталог hello доверенных каталог для базы данных размещения hello hello подписки Azure. Дополнительные сведения см. в статье [Связь между подписками Azure и службой Azure Active Directory](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Дополнительные сведения.** Каждая подписка Azure связана отношением доверия с экземпляром Azure AD. Это означает, что она доверяет, tooauthenticate directory пользователей, служб и устройств. Несколько подписок могут доверять hello же каталоге, но подписка доверяет только одному каталогу. Вы увидите каталога, который является доверенным для вашей подписки, под hello **параметры** tab в [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Это отношение доверия с подпиской и каталогом не похожи hello отношения подписки с другими ресурсами в Azure (веб-сайтов, баз данных и т. д), которые наиболее точно дочерними ресурсами подписки. Если подписки истекает, а затем получить доступ к toothose другие ресурсы, связанные с подпиской hello также останавливается. Но hello каталог останется в Azure, и можно связать с этим каталогом другую подписку и продолжить toomanage hello каталог пользователей. Дополнительные сведения о ресурсах см. в статье, посвященной [доступу к ресурсам в Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Hello следующих процедурах показано, как toochange hello связан каталог для данной подписки.
1. Подключение tooyour [классический портал Azure](https://manage.windowsazure.com/) с помощью администратора подписки Azure.
2. В hello слева выберите **параметры**.
3. Ваши подписки отобразятся в параметры экрана приветствия. По желанию hello подписки не отображается, нажмите кнопку **подписки** вверху hello раскрывающийся список hello **фильтр по DIRECTORY** поле hello каталог, содержащий подписки и нажмите кнопку **Применить**.
   
    ![выбрать подписку][4]
4. В hello **параметры** , щелкните свою подписку, а затем выберите **изменить КАТАЛОГ** hello нижней части страницы приветствия.
   
    ![ad-settings-portal][5]
5. В hello **изменить КАТАЛОГ** поле hello Azure Active Directory, связанный с SQL Server или хранилища данных SQL и нажмите кнопку со стрелкой hello для следующего.
   
    ![edit-directory-select][6]
6. В hello **Подтверждение** directory диалоговое окно сопоставления, убедитесь, что «**все соадминистраторы будут удалены.**»
   
    ![edit-directory-confirm][7]
7. Щелкните флажок tooreload hello hello-портал.

   > [!NOTE]
   > При изменить каталог hello, администраторов tooall доступ, пользователи Azure AD и группам и пользователи каталога резервных ресурсов будут удалены и больше не имеют подписки toothis доступа или его ресурсам. Только, администратор служб, можно настроить доступ для участников, в зависимости от нового каталога hello. Это изменение может занять значительное время toopropagate tooall ресурсов. Изменение каталога hello, также изменения Здравствуйте, администратор Azure AD для базы данных SQL и хранилища данных SQL и запретить доступ к базе данных для всех существующих пользователей Azure AD. Azure AD Здравствуйте, администратор должен быть сброса (как описано ниже) и новый Azure необходимо создать пользователей AD.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Создание администратора Azure AD для сервера Azure SQL Server
Каждый сервер Azure SQL (в котором размещена база данных SQL или хранилище данных SQL) начинается с одного сервера учетной записи администратора, администратор hello hello всего сервера Azure SQL. Необходимо создать второго администратора SQL Server, то есть учетную запись Azure AD. Этот участник создается как пользователя автономной базы данных в базе данных master hello. Администраторы учетных записей администратора сервера hello являются членами hello **db_owner** роли в каждый пользователь базы данных и введите каждой пользовательской базы данных в качестве hello **dbo** пользователя. Дополнительные сведения об учетных записях администратора сервера hello см. в разделе [Управление базами данных и именами входа в базе данных SQL Azure](sql-database-manage-logins.md).

При использовании Azure Active Directory с георепликации, Здравствуйте, администратор Azure Active Directory необходимо включить поддержку основного hello и серверы-получатели hello. Если сервер не имеет администратора Azure Active Directory, то Azure Active Directory имена входа и пользователи принимать tooserver ошибку «Не удается подключиться».

> [!NOTE]
> Пользователи, которые не основаны на учетную запись Azure AD (включая учетной записи администратора hello Azure SQL server), невозможно создать Azure AD — пользователи, так как они не имеют разрешений toovalidate предложенные пользователей базы данных с hello Azure AD.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Подготовка администратора Azure Active Directory для сервера Azure SQL Server

следующие две процедуры Hello показывается, как tooprovision администратора Azure Active Directory для сервера Azure SQL в hello портал Azure и с помощью PowerShell.

### <a name="azure-portal"></a>Портал Azure
1. В hello [портал Azure](https://portal.azure.com/)в hello в правом верхнем углу, щелкнув вашей toodrop подключения список возможных каталогов Active Directory. Выберите hello исправить Active Directory по умолчанию hello Azure AD. Этот шаг ссылки hello связь подписки с помощью Active Directory с сервером Azure SQL, убедившись, что hello одной подписке используется для Azure AD и SQL Server. (можно размещение hello Azure SQL server, базы данных SQL Azure или хранилище данных SQL Azure.)   
    ![choose-ad][8]   
    
2. В hello слева выберите баннер **серверов SQL Server**, выберите ваш **SQL server**и затем в hello **SQL Server** колонке нажмите кнопку **администратора Active Directory**.   
3. В hello **администратора Active Directory** колонка, щелкните **задать администратора**.   
    ![выбор Active Directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. В hello **добавить администратора** колонке поиск пользователя, выберите hello пользователя или группы toobe администратора и нажмите кнопку **выберите**. (колонки администрирования Active Directory hello показывает все элементы и группы в Active Directory. Пользователей или группы, которые выделены серым цветом, нельзя выбрать; они не поддерживаются ролью администратора Azure AD. (См. список поддерживаемых Администраторы в hello hello **функции Azure AD и ограничения** раздел [использование Azure проверки подлинности Active Directory для проверки подлинности в базе данных SQL или хранилище данных SQL](sql-database-aad-authentication.md).) Управление доступом на основе ролей (RBAC) применяется только toohello портала и не распространенный tooSQL сервера.   
    ![выбор администратора](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Вверху hello hello **администратора Active Directory** колонка, щелкните **Сохранить**.   
    ![сохранение администратора](./media/sql-database-aad-authentication/save-admin.png)   

Hello изменения Здравствуйте, администратор может занять несколько минут. После чего появится новый администратор hello в hello **администратора Active Directory** поле.

   > [!NOTE]
   > При настройке Azure AD Здравствуйте, администратор, hello новое имя администратора (пользователя или группы) не может быть уже присутствует в базе данных master виртуального hello имени пользователя проверки подлинности SQL Server. Если он имеется, hello Azure AD администратор установка завершится ошибкой; откат его создания и указав, что такие права администратора (имя) уже существует. Так как такой пользователь проверку подлинности SQL Server не является частью hello Azure AD, любой сервер toohello tooconnect усилия с использованием проверки подлинности Azure AD завершается ошибкой.
   > 


toolater удалить администратора, вверху hello hello **администратора Active Directory** колонка, щелкните **удалить администратора**и нажмите кнопку **Сохранить**.

### <a name="powershell"></a>PowerShell
toorun командлеты PowerShell, необходимо toohave Azure PowerShell установлена и запущена. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

tooprovision администратор Azure AD, выполните следующие команды Azure PowerShell hello:

* Add-AzureRmAccount
* Select-AzureRmSubscription

Командлеты используются tooprovision и управление администрирования Azure AD.

| Имя командлета | Описание |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Выполняет подготовку учетной записи администратора Azure Active Directory для сервера Azure SQL Server или хранилища данных SQL Azure. (Должен быть из текущей подписки hello). |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Удаляет учетную запись администратора Azure Active Directory для сервера Azure SQL Server или хранилища данных SQL Azure. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Возвращает сведения о администратора Azure Active Directory, настроенных для hello Azure SQL server или хранилище данных SQL Azure. |

Используйте команду get-help toosee более подробные сведения для каждого из этих команд, например PowerShell ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Здравствуйте, выполнив скрипт подготавливает группы администратора Azure AD с именем **DBA_Group** (идентификатор объекта `40b79501-b343-44ed-9ce7-da4c8cc7353f`) для hello **demo_server** сервера в группу ресурсов с именем **23 группы** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Hello **DisplayName** входного параметра принимает hello Azure AD отображаемое имя или имя участника-пользователя hello. Например, ``DisplayName="John Smith"`` и ``DisplayName="johns@contoso.com"``. Для Azure AD группы только hello Azure AD поддерживается отображаемое имя.

> [!NOTE]
> Hello команду Azure PowerShell ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` не остановит процесс подготовки Администраторы Azure AD для пользователей, не поддерживается. Неподдерживаемые пользователя могут быть подготовлены, но не удается подключиться tooa базы данных. 
> 

Hello следующем примере используется необязательный hello **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Hello Azure AD **ObjectID** является обязательным, если hello **DisplayName** не является уникальным. tooretrieve hello **ObjectID** и **DisplayName** значения, воспользуйтесь разделом Active Directory hello классический портал Azure и просмотрите свойства hello пользователя или группы.
> 

Следующий пример Hello возвращает сведения о текущей Azure AD Здравствуйте, администратор для сервера Azure SQL:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Следующий пример Hello удаляет администратор Azure AD:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Можно также подготовить администратора Azure Active Directory с помощью API-интерфейсов REST hello. Дополнительные сведения см. в справочнике по REST API управления службами и статье [Operations for Azure SQL Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx) (Операции для баз данных SQL Azure).

### <a name="cli"></a>Интерфейс командной строки  
Можно также предоставить вызывающему Привет, следующие команды CLI администратор Azure AD:
| Команда | Описание |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Выполняет подготовку учетной записи администратора Azure Active Directory для сервера Azure SQL Server или хранилища данных SQL Azure. (Должен быть из текущей подписки hello). |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Удаляет учетную запись администратора Azure Active Directory для сервера Azure SQL Server или хранилища данных SQL Azure. |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Возвращает сведения о администратора Azure Active Directory, настроенных для hello Azure SQL server или хранилище данных SQL Azure. |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Обновляет Здравствуйте, администратор Active Directory для сервера Azure SQL или хранилище данных SQL Azure. |

Дополнительные сведения о командах CLI см. в статье [SQL Server - az sql server](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Настройка клиентских компьютеров
На всех клиентских компьютерах, из которых приложениям или пользователям подключаться tooAzure базы данных SQL или хранилище данных SQL Azure, с помощью удостоверений Azure AD, необходимо установить hello после программного обеспечения:

* .NET Framework 4.6 или более поздней версии можно скачать на веб-странице [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Библиотека проверки подлинности Azure Active Directory для SQL Server (**ADALSQL. Библиотеки DLL**) доступна на нескольких языках (x86 и amd64) из центра загрузки hello [Microsoft библиотеку аутентификации Active Directory для Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Вы можете выполнить эти требования, сделав следующее:

* Установка любого [среды Management Studio SQL Server 2016](https://msdn.microsoft.com/library/mt238290.aspx) или [SQL Server Data Tools для Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) соответствует hello требования .NET Framework 4.6.
* SSMS устанавливается версия hello x86 **ADALSQL. Библиотеки DLL**.
* SSDT устанавливает версию amd64 hello **ADALSQL. Библиотеки DLL**.
* Hello последний выпуск Visual Studio из [загрузки Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) требованиям hello .NET Framework 4.6, но не устанавливает версию необходимые amd64 hello **ADALSQL. Библиотеки DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Создать пользователей автономной базы данных в вашей базы данных сопоставлен tooAzure удостоверений AD

Проверка подлинности Azure Active Directory требует toobe пользователей базы данных создана в виде пользователей автономной базы данных. Пользователя автономной базы данных в зависимости от Azure AD identity является пользователем базы данных, не имеет имени входа в базе данных master hello и каталог Azure AD, который связан с базой данных hello hello удостоверению tooan карты в. Hello удостоверений Azure AD может быть отдельного пользователя или группы. Дополнительные сведения о пользователях автономной базы данных см. в статье [Пользователи автономной базы данных — создание переносимой базы данных](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Пользователи базы данных (за исключением hello администраторов) не может создаваться с помощью портала. RBAC роли не являются распространенный tooSQL сервера, базы данных SQL или хранилище данных SQL. Роли RBAC Azure используются для управления ресурсами Azure и не применять разрешения toodatabase. Например, hello **участника SQL Server** роль не предоставляет toohello tooconnect доступа к базе данных SQL или хранилище данных SQL. необходимо предоставить разрешение доступа Hello непосредственно в базе данных hello, с помощью инструкций Transact-SQL.
>

по крайней мере hello Azure AD содержится база данных пользователя на основе (кроме hello администратора сервера, которому принадлежит hello базы данных), подключение toohello базы данных с использованием идентификатора Azure AD в качестве пользователя с toocreate **ALTER ANY USER** разрешение. Затем используйте hello, используя синтаксис языка Transact-SQL:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* может быть hello имя участника-пользователя Azure AD пользователя или hello отображаемое имя для группы Azure AD.

**Примеры:** toocreate пользователя автономной базы данных, представляющий Azure AD федеративные или управляемые пользователя домена:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate пользователя автономной базы данных, представляющий Azure AD или федеративного группу домена обеспечивают hello отображаемое имя группы безопасности:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate пользователя автономной базы данных, представляющий приложение, которое соединяется с использованием маркера Azure AD:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Невозможно напрямую создать пользователя из Azure Active Directory Кроме hello Azure Active Directory, которая связана с подпиской Azure. Однако члены других каталогов Active Directory, импортированных пользователей в hello связанные Active Directory (это называется внешних пользователей) можно добавить группы Active Directory tooan hello клиента Active Directory. Создание пользователя автономной базы данных для этой группы AD, hello пользователям hello внешних Active Directory можно получить доступ tooSQL базы данных.   

Подробные сведения о создании пользователей автономной базы данных на основе удостоверений Azure Active Directory см. в статье [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Удаление администратора hello Azure Active Directory для Azure SQL server невозможным подключение сервера toohello любого пользователя проверка подлинности Azure AD. При необходимости администратор Базы данных SQL может вручную удалить неиспользуемых пользователей Azure AD.   

>  [!NOTE]
>  При получении **превышено время ожидания подключения**, может потребоваться tooset hello `TransparentNetworkIPResolution` параметр toofalse строку hello соединения. Дополнительные сведения см. в статье [Connection timeout issue with .NET Framework 4.6.1 — TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/) (Проблема с временем ожидания подключения в .NET Framework 4.6.1 — TransparentNetworkIPResolution).   

   
При создании пользователя базы данных, пользователь получает hello **CONNECT** разрешения и могут подключиться toothat базы данных как член hello **ОТКРЫТЫЙ** роли. Изначально hello только те разрешения, которые являются доступными toohello пользователя toohello предоставлены все разрешения **ОТКРЫТЫЙ** роли или какие-либо разрешения предоставлены tooany группы Windows, являясь членом. После подготовки Azure содержащихся на основе AD пользователя базы данных, можно предоставить дополнительные разрешения пользователя hello hello таким же, как предоставить разрешения tooany другого типа пользователя. Обычно разрешения роли toodatabase и добавьте пользователей tooroles. Подробные сведения см. в статье [Database Engine Permission Basics](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx) (Основные сведения о разрешениях ядра СУБД). Дополнительные сведения о специальных ролях базы данных SQL см. в статье [Проверка подлинности и авторизация в базе данных SQL: предоставление доступа](sql-database-manage-logins.md).
Федеративный домен пользователя, импортированы в домен управление, необходимо использовать идентификатор hello управляемого домена.

> [!NOTE]
> Azure AD пользователи будут отмечены в метаданных базы данных hello с типом E (EXTERNAL_USER) и для групп типа X (EXTERNAL_GROUPS). Дополнительные сведения см. в статье [sys.database_principals (Transact-SQL)](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Подключиться с помощью SSMS или SSDT toohello пользователя базы данных или хранилища данных  
Администратор tooconfirm hello Azure AD установлена должным образом, подключите toohello **master** базы данных с помощью учетной записи администратора hello Azure AD.
tooprovision Azure AD содержится база данных пользователя на основе (кроме hello администратором сервера, которому принадлежит hello базы данных) и подключитесь toohello базу данных с использованием идентификатора Azure AD, который имеет доступ к базе данных toohello.

> [!IMPORTANT]
> Проверку подлинности Azure Active Directory поддерживают [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) и [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) для Visual Studio 2015. Hello августа 2016 г. выпуск SSMS также включает поддержку универсальной проверки подлинности Active Directory, который позволяет администраторам toorequire многофакторной проверки подлинности с помощью телефонный звонок, текстовое сообщение, смарт-карты с помощью ПИН-кода или уведомление мобильного приложения.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>С помощью tooconnect удостоверений Azure AD с помощью SSMS или SSDT  

Hello перечисленные ниже действия показывают, как tooconnect tooa SQL базы данных с использованием идентификатора Azure AD с помощью SQL Server Management Studio или инструменты для баз данных SQL Server.

### <a name="active-directory-integrated-authentication"></a>Встроенная аутентификация Active Directory

Используйте этот метод, если вы вошли в tooWindows, используя учетные данные Azure Active Directory из федеративный домен.

1. Запустите среду Management Studio или Data Tools и в hello **подключения tooServer** (или **подключения tooDatabase ядра**) диалогового окна hello **проверки подлинности** выберите **Интегрированных в active Directory -**. Пароль не требуется, или можно ввести, поскольку существующие учетные данные будут представлены для подключения hello.   

    ![Выбор встроенной аутентификации Active Directory][11]
2. Щелкните hello **параметры** кнопки и на hello **свойства соединения** страницы в hello **подключения toodatabase** введите имя hello hello пользовательской базы данных требуется tooconnect Кому. (hello **код домена имя или клиента AD**» параметр поддерживается только для **универсальной с многофакторной проверки Подлинности подключения** "Параметры", в противном случае он неактивен.)  

    ![Выберите имя базы данных hello][13]

## <a name="active-directory-password-authentication"></a>Проверка пароля Active Directory

Этот метод следует используйте при подключении с именем участника Azure AD с помощью Azure AD hello управляемого домена. Ее также можно использовать для федеративной учетной записи без домена toohello доступа, например при удаленной работе.

Используйте этот метод, если вы вошли с использованием учетных данных из домена, который не входит в федерацию с Azure tooWindows или при использовании проверки подлинности Azure AD с помощью Azure AD на основании начального приветствия или hello домена клиента.

1. Запустите среду Management Studio или Data Tools и в hello **подключения tooServer** (или **подключения tooDatabase ядра**) диалогового окна hello **проверки подлинности** выберите **Active Directory — пароль**.
2. В hello **имя пользователя** введите свое имя пользователя Azure Active Directory в формате hello  **username@domain.com** . Это должна быть учетной записью из hello Azure Active Directory или учетную запись из домена федерацию с Azure Active Directory hello.
3. В hello **пароль** введите пароль пользователя для учетной записи Azure Active Directory hello или федеративной учетной записи домена.

    ![Выбор проверки пароля Active Directory][12]
4. Щелкните hello **параметры** кнопки и на hello **свойства соединения** страницы в hello **подключения toodatabase** введите имя hello hello пользовательской базы данных требуется tooconnect Кому. (См. рисунок hello в предыдущем варианте hello).

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>С помощью tooconnect удостоверений Azure AD из клиентского приложения

Hello перечисленные ниже действия показывают, как tooconnect tooa SQL базы данных с использованием идентификатора Azure AD из клиентского приложения.

###  <a name="active-directory-integrated-authentication"></a>Встроенная аутентификация Active Directory

toouse встроенная проверка подлинности Windows, Active Directory вашего домена необходимо федерацию с Azure Active Directory. Клиентское приложение (или служба) соединения toohello базы данных должна быть запущена на компьютере, присоединенном к домену, учетными данными пользователя домена.

tooconnect tooa базы данных с помощью интегрированной проверки подлинности и удостоверение Azure AD, ключевое слово hello проверки подлинности, в строку подключения базы данных hello необходимо задать tooActive интеграции каталогов. Hello следующий код C# использует ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Здравствуйте, ключевое слово строки подключения ``Integrated Security=True`` не поддерживается для подключения tooAzure базы данных SQL. При создании соединения ODBC, будет требуется tooremove пробелы и задать too'ActiveDirectoryIntegrated проверки подлинности ".

### <a name="active-directory-password-authentication"></a>Проверка пароля Active Directory

tooconnect tooa базы данных с помощью интегрированной проверки подлинности и удостоверение Azure AD, ключевое слово hello проверки подлинности необходимо задать tooActive пароль. Строка подключения Hello должен содержать идентификатор пользователя или UID и пароль/PWD ключевых слов и значений. Hello следующий код C# использует ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Дополнительные сведения о методах проверки подлинности Azure AD с помощью hello демонстрационный код примеров по адресу [Демонстрация GitHub проверки подлинности Azure AD](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Токен Azure AD
Этот метод проверки подлинности позволяет tooAzure tooconnect службы среднего уровня базы данных SQL или хранилище данных SQL Azure с помощью получения токена из Azure Active Directory (AAD). Он используется для реализации сложных сценариев, включая проверку подлинности на основе сертификатов. Необходимо выполнить четыре основные шаги toouse токена проверки подлинности Azure AD.

1. Зарегистрировать приложение в Azure Active Directory и получить идентификатор клиента hello в коде. 
2. Создание пользователя базы данных представления приложения hello. (Выполнено ранее на шаге 6.)
3. Создайте сертификат при запуске компьютера клиента hello приложения hello.
4. Добавление сертификата hello в качестве ключа для вашего приложения.

Пример строки подключения.

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Дополнительные сведения см. в [блоге о безопасности SQL Server](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Здравствуйте, при использовании после инструкций, подключитесь с помощью версии 13.1 sqlcmd, которое доступно из hello [центра загрузки](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Дальнейшие действия
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
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

