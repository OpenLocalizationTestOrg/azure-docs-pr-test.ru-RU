---
title: "Руководство по разработке веб-приложения с мультитенантной базой данных с помощью Entity Framework и политики безопасности на уровне строк"
description: "Узнайте, как toodevelop ASP.NET MVC 5 веб-приложения с несколькими клиентами базы данных SQL backent, с помощью платформы Entity Framework и безопасность на уровне строк."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Руководство по разработке веб-приложения с мультитенантной базой данных с помощью Entity Framework и политики безопасности на уровне строк
В этом учебнике показано, как toobuild многопользовательское веб-приложение с «[общей базы данных, общей схемы](https://msdn.microsoft.com/library/aa479086.aspx)» модели аренды, использующий Entity Framework и [безопасность на уровне строк](https://msdn.microsoft.com/library/dn765131.aspx). Подобная модель предусматривает, что в отдельной базе данных содержатся данные для многих клиентов, а каждая строка в каждой таблице связана с идентификатором клиента. На уровне строк безопасности (RLS), нового компонента для базы данных SQL Azure — используется tooprevent клиентам доступ к данным. Это требуется только один, toohello приложение небольшое изменение. Путем централизации hello клиента доступа логику в самой базе данных hello RLS упрощает код приложения hello и снижает риск hello утечки случайных данных между клиентами.

Давайте начнем с hello простое приложение диспетчера контактов из [Создание приложения ASP.NET MVP с проверки подлинности и баз данных SQL Server и развернуть tooAzure службы приложений](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Право теперь приложения hello позволяет все пользователи (клиенты) toosee все контакты:

![Приложение диспетчера контактов перед включением RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

С только что небольшие изменения мы добавим поддержку многопользовательский режим, чтобы пользователи могли toosee только hello контактов, принадлежащих toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Шаг 1: Добавьте класс перехватчик в hello tooset приложения hello SESSION_CONTEXT
Имеется одно изменение приложений, мы должны toomake. Так как все пользователи приложения подключаются toohello базы данных с помощью Здравствуйте одинаковые строки подключения (т. е. же имя входа SQL), в настоящее время нет возможности для tooknow политики RLS, какой именно пользователь, его следует фильтровать по. Этот подход является очень распространены в веб-приложений, так как она позволяет эффективно пула подключений, однако это означает, что нам нужно другим способом tooidentify hello текущего пользователя приложения в базе данных hello. Hello решения является набор приложения hello toohave пару "ключ значение" для hello идентификатор текущего пользователя в hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) сразу после открытия соединения, перед выполняет все запросы. SESSION_CONTEXT хранилище значений ключей, областью действия сеанса, и политике RLS будут использовать hello UserId сохраненные в ней tooidentify hello текущего пользователя.

Мы будем добавлять [перехватчик](https://msdn.microsoft.com/data/dn469464.aspx) (в частности, [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), новая возможность в Entity Framework (EF) 6, набор tooautomatically hello текущего UserId в hello SESSION_CONTEXT путем выполнения Инструкции T-SQL, каждый раз, когда EF открывает соединение.

1. Откройте проект ContactManager hello в Visual Studio.
2. Правой кнопкой мыши папку Models hello в hello в обозревателе решений и выберите команду Добавить > класса.
3. Имя нового класса hello «SessionContextInterceptor.cs» и нажмите кнопку Добавить.
4. Замените содержимое hello SessionContextInterceptor.cs hello, следующий код.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

Это необходимо изменить только приложения hello. Продолжим построение и опубликовать приложение hello.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Шаг 2: Добавление схемы UserId toohello столбца базы данных
Теперь нам нужны tooadd UserId контактов toohello столбца таблицы tooassociate каждой строки с пользователем (клиента). Мы приведут к изменению схемы hello непосредственно в базе данных hello, чего мы в нашей модели данных EF tooinclude нет в этом поле.

Подключение базы данных toohello напрямую, с помощью SQL Server Management Studio или Visual Studio, а затем выполните hello следующий T-SQL:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Это добавляет toohello контакты UserId столбца таблицы. Мы используем hello nvarchar(128) данных типа toomatch hello недопустимость, хранящимся в таблице AspNetUsers hello, а также создавать ограничение по умолчанию, автоматически установит hello UserId для вставленных строк toobe hello UserId, хранящихся в SESSION_CONTEXT.

Теперь таблица hello выглядит следующим образом:

![Таблицы контактов SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

При создании новых контактов, они будут автоматически назначены hello исправьте идентификатор пользователя. В целях демонстрации тем не менее, давайте назначить некоторые из этих существующих контактов tooan существующего пользователя.

Если вы создали несколько пользователей в приложение hello уже (например, с использованием локальных, Google или Facebook учетных записей), чтобы увидеть их в таблице AspNetUsers hello. В следующем снимке экрана приветствия имеется только один пользователь до сих.

![Таблица AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Копировать hello идентификатор для user1@contoso.comи вставьте его в Приведенная ниже инструкция hello T-SQL. Выполнение этой инструкции tooassociate трех, контактов, hello с этот код пользователя.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Шаг 3: Создание политики безопасности на уровне строк в базе данных hello
последним шагом Hello является toocreate политику безопасности, использующий hello UserId в SESSION_CONTEXT tooautomatically фильтра hello результатов, возвращенных запросами.

При toohello по-прежнему подключенной базы данных выполните следующий T-SQL hello:

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

Этот код выполняет три действия. Во-первых он создает новую схему рекомендуется для централизации и ограничение доступа к объектам RLS toohello. Затем он создает функцию предиката, которая возвращает "1", если hello UserId строки соответствует hello UserId в SESSION_CONTEXT. Наконец он создает политику безопасности, которая добавляет эту функцию в качестве предиката фильтров и блокировки для таблицы Contacts hello. предикат фильтра Hello вызывает tooreturn запросы только строки, которые принадлежат toohello текущего пользователя, и предиката блокировки hello действует как приложение hello защиты tooprevent когда-либо случайно вставить строку для пользователя hello.

Теперь запустите приложение hello и войдите как user1@contoso.com. Теперь этот пользователь видит только контакты hello, назначенные ранее toothis UserId:

![Приложение диспетчера контактов перед включением RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate это в дальнейшем попытку регистрации нового пользователя. Так как ни один не назначены toothem контакты не будут отображены. Если они создают новый контакт, ему назначается toothem и только они будут может toosee его.

## <a name="next-steps"></a>Дальнейшие действия
Вот и все! Многопользовательское один где каждый пользователь имеет свой собственный список контактов будет преобразовано Hello простой веб-приложение диспетчера контактов. С помощью безопасности на уровне строк, мы избежать hello сложности реализации логики доступа клиента в коде приложения. Прозрачности позволяет toofocus приложения hello на hello под рукой реальные бизнес-задачи, и это также уменьшает риск случайной утечки данных как кода приложения hello hello роста.

Этот учебник содержит только поцарапан hello поверхности возможности RLS. Для экземпляра это более сложное возможные toohave или логику детального доступа и возможные toostore больше, чем просто hello текущего UserId в hello SESSION_CONTEXT. Можно также слишком[интегрировать RLS hello эластичной базы данных средства клиентские библиотеки](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport сегментов несколькими клиентами на уровне данных горизонтального масштабирования.

Помимо этих возможностей мы работаем toomake RLS еще лучше. Если у вас возникли вопросы, идеи или вещей, которые вы хотите toosee, сообщите нам в комментариях hello. Ваши отзывы важны для нас!

