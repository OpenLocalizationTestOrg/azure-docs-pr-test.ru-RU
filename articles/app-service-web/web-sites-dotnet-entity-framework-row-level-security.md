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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="2696e-103">Руководство по разработке веб-приложения с мультитенантной базой данных с помощью Entity Framework и политики безопасности на уровне строк</span><span class="sxs-lookup"><span data-stu-id="2696e-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="2696e-104">В этом учебнике показано, как toobuild многопользовательское веб-приложение с «[общей базы данных, общей схемы](https://msdn.microsoft.com/library/aa479086.aspx)» модели аренды, использующий Entity Framework и [безопасность на уровне строк](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="2696e-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="2696e-105">Подобная модель предусматривает, что в отдельной базе данных содержатся данные для многих клиентов, а каждая строка в каждой таблице связана с идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="2696e-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="2696e-106">На уровне строк безопасности (RLS), нового компонента для базы данных SQL Azure — используется tooprevent клиентам доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="2696e-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="2696e-107">Это требуется только один, toohello приложение небольшое изменение.</span><span class="sxs-lookup"><span data-stu-id="2696e-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="2696e-108">Путем централизации hello клиента доступа логику в самой базе данных hello RLS упрощает код приложения hello и снижает риск hello утечки случайных данных между клиентами.</span><span class="sxs-lookup"><span data-stu-id="2696e-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="2696e-109">Давайте начнем с hello простое приложение диспетчера контактов из [Создание приложения ASP.NET MVP с проверки подлинности и баз данных SQL Server и развернуть tooAzure службы приложений](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2696e-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="2696e-110">Право теперь приложения hello позволяет все пользователи (клиенты) toosee все контакты:</span><span class="sxs-lookup"><span data-stu-id="2696e-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Приложение диспетчера контактов перед включением RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="2696e-112">С только что небольшие изменения мы добавим поддержку многопользовательский режим, чтобы пользователи могли toosee только hello контактов, принадлежащих toothem.</span><span class="sxs-lookup"><span data-stu-id="2696e-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="2696e-113">Шаг 1: Добавьте класс перехватчик в hello tooset приложения hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="2696e-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="2696e-114">Имеется одно изменение приложений, мы должны toomake.</span><span class="sxs-lookup"><span data-stu-id="2696e-114">There is one application change we need toomake.</span></span> <span data-ttu-id="2696e-115">Так как все пользователи приложения подключаются toohello базы данных с помощью Здравствуйте одинаковые строки подключения (т. е. же имя входа SQL), в настоящее время нет возможности для tooknow политики RLS, какой именно пользователь, его следует фильтровать по.</span><span class="sxs-lookup"><span data-stu-id="2696e-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="2696e-116">Этот подход является очень распространены в веб-приложений, так как она позволяет эффективно пула подключений, однако это означает, что нам нужно другим способом tooidentify hello текущего пользователя приложения в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="2696e-117">Hello решения является набор приложения hello toohave пару "ключ значение" для hello идентификатор текущего пользователя в hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) сразу после открытия соединения, перед выполняет все запросы.</span><span class="sxs-lookup"><span data-stu-id="2696e-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="2696e-118">SESSION_CONTEXT хранилище значений ключей, областью действия сеанса, и политике RLS будут использовать hello UserId сохраненные в ней tooidentify hello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="2696e-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="2696e-119">Мы будем добавлять [перехватчик](https://msdn.microsoft.com/data/dn469464.aspx) (в частности, [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), новая возможность в Entity Framework (EF) 6, набор tooautomatically hello текущего UserId в hello SESSION_CONTEXT путем выполнения Инструкции T-SQL, каждый раз, когда EF открывает соединение.</span><span class="sxs-lookup"><span data-stu-id="2696e-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="2696e-120">Откройте проект ContactManager hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2696e-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="2696e-121">Правой кнопкой мыши папку Models hello в hello в обозревателе решений и выберите команду Добавить > класса.</span><span class="sxs-lookup"><span data-stu-id="2696e-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="2696e-122">Имя нового класса hello «SessionContextInterceptor.cs» и нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="2696e-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="2696e-123">Замените содержимое hello SessionContextInterceptor.cs hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="2696e-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

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

<span data-ttu-id="2696e-124">Это необходимо изменить только приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-124">That's hello only application change required.</span></span> <span data-ttu-id="2696e-125">Продолжим построение и опубликовать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="2696e-126">Шаг 2: Добавление схемы UserId toohello столбца базы данных</span><span class="sxs-lookup"><span data-stu-id="2696e-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="2696e-127">Теперь нам нужны tooadd UserId контактов toohello столбца таблицы tooassociate каждой строки с пользователем (клиента).</span><span class="sxs-lookup"><span data-stu-id="2696e-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="2696e-128">Мы приведут к изменению схемы hello непосредственно в базе данных hello, чего мы в нашей модели данных EF tooinclude нет в этом поле.</span><span class="sxs-lookup"><span data-stu-id="2696e-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="2696e-129">Подключение базы данных toohello напрямую, с помощью SQL Server Management Studio или Visual Studio, а затем выполните hello следующий T-SQL:</span><span class="sxs-lookup"><span data-stu-id="2696e-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="2696e-130">Это добавляет toohello контакты UserId столбца таблицы.</span><span class="sxs-lookup"><span data-stu-id="2696e-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="2696e-131">Мы используем hello nvarchar(128) данных типа toomatch hello недопустимость, хранящимся в таблице AspNetUsers hello, а также создавать ограничение по умолчанию, автоматически установит hello UserId для вставленных строк toobe hello UserId, хранящихся в SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="2696e-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="2696e-132">Теперь таблица hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2696e-132">Now hello table looks like this:</span></span>

![Таблицы контактов SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="2696e-134">При создании новых контактов, они будут автоматически назначены hello исправьте идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="2696e-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="2696e-135">В целях демонстрации тем не менее, давайте назначить некоторые из этих существующих контактов tooan существующего пользователя.</span><span class="sxs-lookup"><span data-stu-id="2696e-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="2696e-136">Если вы создали несколько пользователей в приложение hello уже (например, с использованием локальных, Google или Facebook учетных записей), чтобы увидеть их в таблице AspNetUsers hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="2696e-137">В следующем снимке экрана приветствия имеется только один пользователь до сих.</span><span class="sxs-lookup"><span data-stu-id="2696e-137">In hello screenshot below, there is only one user so far.</span></span>

![Таблица AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="2696e-139">Копировать hello идентификатор для user1@contoso.comи вставьте его в Приведенная ниже инструкция hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="2696e-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="2696e-140">Выполнение этой инструкции tooassociate трех, контактов, hello с этот код пользователя.</span><span class="sxs-lookup"><span data-stu-id="2696e-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="2696e-141">Шаг 3: Создание политики безопасности на уровне строк в базе данных hello</span><span class="sxs-lookup"><span data-stu-id="2696e-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="2696e-142">последним шагом Hello является toocreate политику безопасности, использующий hello UserId в SESSION_CONTEXT tooautomatically фильтра hello результатов, возвращенных запросами.</span><span class="sxs-lookup"><span data-stu-id="2696e-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="2696e-143">При toohello по-прежнему подключенной базы данных выполните следующий T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="2696e-143">While still connected toohello database, execute hello following T-SQL:</span></span>

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

<span data-ttu-id="2696e-144">Этот код выполняет три действия.</span><span class="sxs-lookup"><span data-stu-id="2696e-144">This code does three things.</span></span> <span data-ttu-id="2696e-145">Во-первых он создает новую схему рекомендуется для централизации и ограничение доступа к объектам RLS toohello.</span><span class="sxs-lookup"><span data-stu-id="2696e-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="2696e-146">Затем он создает функцию предиката, которая возвращает "1", если hello UserId строки соответствует hello UserId в SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="2696e-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="2696e-147">Наконец он создает политику безопасности, которая добавляет эту функцию в качестве предиката фильтров и блокировки для таблицы Contacts hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="2696e-148">предикат фильтра Hello вызывает tooreturn запросы только строки, которые принадлежат toohello текущего пользователя, и предиката блокировки hello действует как приложение hello защиты tooprevent когда-либо случайно вставить строку для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="2696e-149">Теперь запустите приложение hello и войдите как user1@contoso.com. Теперь этот пользователь видит только контакты hello, назначенные ранее toothis UserId:</span><span class="sxs-lookup"><span data-stu-id="2696e-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Приложение диспетчера контактов перед включением RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="2696e-151">toovalidate это в дальнейшем попытку регистрации нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="2696e-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="2696e-152">Так как ни один не назначены toothem контакты не будут отображены.</span><span class="sxs-lookup"><span data-stu-id="2696e-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="2696e-153">Если они создают новый контакт, ему назначается toothem и только они будут может toosee его.</span><span class="sxs-lookup"><span data-stu-id="2696e-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2696e-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2696e-154">Next steps</span></span>
<span data-ttu-id="2696e-155">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="2696e-155">That's it!</span></span> <span data-ttu-id="2696e-156">Многопользовательское один где каждый пользователь имеет свой собственный список контактов будет преобразовано Hello простой веб-приложение диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="2696e-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="2696e-157">С помощью безопасности на уровне строк, мы избежать hello сложности реализации логики доступа клиента в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="2696e-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="2696e-158">Прозрачности позволяет toofocus приложения hello на hello под рукой реальные бизнес-задачи, и это также уменьшает риск случайной утечки данных как кода приложения hello hello роста.</span><span class="sxs-lookup"><span data-stu-id="2696e-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="2696e-159">Этот учебник содержит только поцарапан hello поверхности возможности RLS.</span><span class="sxs-lookup"><span data-stu-id="2696e-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="2696e-160">Для экземпляра это более сложное возможные toohave или логику детального доступа и возможные toostore больше, чем просто hello текущего UserId в hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="2696e-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="2696e-161">Можно также слишком[интегрировать RLS hello эластичной базы данных средства клиентские библиотеки](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport сегментов несколькими клиентами на уровне данных горизонтального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="2696e-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="2696e-162">Помимо этих возможностей мы работаем toomake RLS еще лучше.</span><span class="sxs-lookup"><span data-stu-id="2696e-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="2696e-163">Если у вас возникли вопросы, идеи или вещей, которые вы хотите toosee, сообщите нам в комментариях hello.</span><span class="sxs-lookup"><span data-stu-id="2696e-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="2696e-164">Ваши отзывы важны для нас!</span><span class="sxs-lookup"><span data-stu-id="2696e-164">We appreciate your feedback!</span></span>

