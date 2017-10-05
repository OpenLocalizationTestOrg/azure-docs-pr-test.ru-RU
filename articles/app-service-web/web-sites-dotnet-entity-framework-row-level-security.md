---
title: "Руководство по разработке веб-приложения с мультитенантной базой данных с помощью Entity Framework и политики безопасности на уровне строк"
description: "Узнайте, как разработать веб-приложение ASP.NET MVC 5 с серверной частью в виде мультитенантной базы данных SQL с помощью Entity Framework и политики безопасности на уровне строк."
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="1bd00-103">Руководство по разработке веб-приложения с мультитенантной базой данных с помощью Entity Framework и политики безопасности на уровне строк</span><span class="sxs-lookup"><span data-stu-id="1bd00-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="1bd00-104">В этом руководстве показано, как создать мультитенантное веб-приложение с [общей базой данных и общей схемой](https://msdn.microsoft.com/library/aa479086.aspx) с помощью Entity Framework и политики [безопасности на уровне строк](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bd00-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="1bd00-105">Подобная модель предусматривает, что в отдельной базе данных содержатся данные для многих клиентов, а каждая строка в каждой таблице связана с идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="1bd00-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="1bd00-106">Безопасность на уровне строк (RLS) — это новая функция базы данных SQL Azure, которая не позволяет клиентам обращаться к данным других клиентов.</span><span class="sxs-lookup"><span data-stu-id="1bd00-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="1bd00-107">Для работы этой политики в приложение нужно внести одно небольшое изменение.</span><span class="sxs-lookup"><span data-stu-id="1bd00-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="1bd00-108">Централизуя логику доступа к клиенту в самой базе данных, политика RLS упрощает код приложения и снижает риск случайной утечки данных клиентов.</span><span class="sxs-lookup"><span data-stu-id="1bd00-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="1bd00-109">Начнем с простого приложения диспетчера контактов (прочтите статью [Создание и развертывание в службе приложений Azure приложения ASP.NET MVP с проверкой подлинности и базой данных SQL Server](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)).</span><span class="sxs-lookup"><span data-stu-id="1bd00-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="1bd00-110">В этом приложении все пользователи (клиенты) могут видеть все контакты.</span><span class="sxs-lookup"><span data-stu-id="1bd00-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Приложение диспетчера контактов перед включением RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="1bd00-112">Немного изменив его, мы включим поддержку мультитенантного режима, благодаря чему пользователи будут видеть только свои контакты.</span><span class="sxs-lookup"><span data-stu-id="1bd00-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="1bd00-113">Шаг 1. Добавление в приложение класса-перехватчика для определения SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="1bd00-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="1bd00-114">Сейчас нам нужно внести в приложение одно изменение.</span><span class="sxs-lookup"><span data-stu-id="1bd00-114">There is one application change we need to make.</span></span> <span data-ttu-id="1bd00-115">Так как все пользователи приложения подключаются к базе данных с помощью одной строки подключения (т. е. одних учетных данных SQL), текущая политика RLS не предусматривает фильтрацию пользователей.</span><span class="sxs-lookup"><span data-stu-id="1bd00-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="1bd00-116">Такой подход очень часто используется в веб-приложениях, позволяя эффективно регулировать количество запросов при подключении. Но в данном случае это означает, что нам нужно настроить другой способ идентификации текущего пользователя приложения в базе данных.</span><span class="sxs-lookup"><span data-stu-id="1bd00-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="1bd00-117">Решение: присвоить пару "ключ-значение" текущему идентификатору UserId в [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) сразу после открытия приложения и до того, как приложение выполнит запрос.</span><span class="sxs-lookup"><span data-stu-id="1bd00-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="1bd00-118">SESSION_CONTEXT — это хранилище пар «ключ — значение» для области сеанса. Хранимый в нем идентификатор UserId будет использоваться политикой RLS для определения текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="1bd00-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="1bd00-119">Кроме того, мы добавим [перехватчик](https://msdn.microsoft.com/data/dn469464.aspx) (в частности, [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), новую функцию Entity Framework (EF) 6, используемую для автоматической настройки текущего идентификатора UserId в SESSION_CONTEXT путем добавления инструкции T-SQL независимо от того, когда EF откроет подключение.</span><span class="sxs-lookup"><span data-stu-id="1bd00-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="1bd00-120">Откройте проект ContactManager в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bd00-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="1bd00-121">В обозревателе решений щелкните правой кнопкой мыши папку «Модели», а затем выберите «Добавить» > «Класс».</span><span class="sxs-lookup"><span data-stu-id="1bd00-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="1bd00-122">Присвойте новому классу имя SessionContextInterceptor.cs и нажмите кнопку «Добавить».</span><span class="sxs-lookup"><span data-stu-id="1bd00-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="1bd00-123">Замените содержимое файла SessionContextInterceptor.cs кодом, приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="1bd00-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

<span data-ttu-id="1bd00-124">Это все, что необходимо изменить в приложении.</span><span class="sxs-lookup"><span data-stu-id="1bd00-124">That's the only application change required.</span></span> <span data-ttu-id="1bd00-125">Теперь создайте и опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="1bd00-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="1bd00-126">Шаг 2. Добавление столбца UserId в схему базы данных</span><span class="sxs-lookup"><span data-stu-id="1bd00-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="1bd00-127">Далее нам нужно добавить в таблицу контактов столбец UserId, чтобы связать каждую строку с пользователем (клиентом).</span><span class="sxs-lookup"><span data-stu-id="1bd00-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="1bd00-128">Так как мы изменим схему непосредственно в базе данных, нам не нужно включать это поле в модель данных EF.</span><span class="sxs-lookup"><span data-stu-id="1bd00-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="1bd00-129">Подключитесь к базе данных напрямую, используя SQL Server Management Studio или Visual Studio, и выполните следующую инструкцию T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1bd00-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="1bd00-130">Столбец UserId будет добавлен в таблицу контактов.</span><span class="sxs-lookup"><span data-stu-id="1bd00-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="1bd00-131">Мы выполним сопоставление идентификаторов UserId, хранимых в таблице AspNetUsers, с помощью типа данных nvarchar(128). Затем мы создадим ограничение DEFAULT, которое автоматически присваивает новым вставленным строкам значение UserId, хранимое в SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1bd00-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="1bd00-132">Теперь таблица выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1bd00-132">Now the table looks like this:</span></span>

![Таблицы контактов SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="1bd00-134">Правильное значение UserId присваивается созданным контактам автоматически.</span><span class="sxs-lookup"><span data-stu-id="1bd00-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="1bd00-135">В качестве примера мы назначим существующим пользователям несколько существующих контактов.</span><span class="sxs-lookup"><span data-stu-id="1bd00-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="1bd00-136">Пользователи, созданные в приложении (например, с помощью локальной учетной записи, учетной записи Google или Facebook), отобразятся таблице AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="1bd00-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="1bd00-137">На приведенном ниже снимке экрана отображен только один пользователь.</span><span class="sxs-lookup"><span data-stu-id="1bd00-137">In the screenshot below, there is only one user so far.</span></span>

![Таблица AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="1bd00-139">Скопируйте значение идентификатора для пользователя user1@contoso.com и вставьте его в приведенную ниже инструкцию T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1bd00-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="1bd00-140">Выполните эту инструкцию, чтобы связать три контакта с этим идентификатором UserId.</span><span class="sxs-lookup"><span data-stu-id="1bd00-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="1bd00-141">Шаг 3. Создание в базе данных политики безопасности на уровне строк</span><span class="sxs-lookup"><span data-stu-id="1bd00-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="1bd00-142">Последним шагом является создание политики безопасности, которая использует UserId в SESSION_CONTEXT для автоматической фильтрации результатов, возвращаемых запросами.</span><span class="sxs-lookup"><span data-stu-id="1bd00-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="1bd00-143">Не прерывая подключение к базе данных, выполните следующую инструкцию T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1bd00-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="1bd00-144">Этот код выполняет три действия.</span><span class="sxs-lookup"><span data-stu-id="1bd00-144">This code does three things.</span></span> <span data-ttu-id="1bd00-145">Во-первых, он создает новую схему для централизации и ограничения доступа к объектам RLS.</span><span class="sxs-lookup"><span data-stu-id="1bd00-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="1bd00-146">Во-вторых, он создает предикатную функцию, которая возвращает 1, если значение UserId строки соответствует значению UserId в хранилище SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1bd00-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="1bd00-147">Наконец, он создает политику безопасности, которая добавляет эту функцию в таблицу контактов в качестве предиката фильтрации и блокировки.</span><span class="sxs-lookup"><span data-stu-id="1bd00-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="1bd00-148">Предикат фильтрации вызывает запросы для возврата только тех строк, которые принадлежат текущему пользователю, а предикат блокировки не позволяет приложению случайно вставить строку для неправильного пользователя.</span><span class="sxs-lookup"><span data-stu-id="1bd00-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="1bd00-149">Запустите приложение и войдите как user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1bd00-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="1bd00-150">Этот пользователь теперь видит только те контакты, которые мы перед этим назначили его идентификатору UserId:</span><span class="sxs-lookup"><span data-stu-id="1bd00-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Приложение диспетчера контактов перед включением RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="1bd00-152">Для дальнейшей проверки зарегистрируйте нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="1bd00-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="1bd00-153">Новый пользователь не увидит никаких контактов, так как мы ему ничего не назначили.</span><span class="sxs-lookup"><span data-stu-id="1bd00-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="1bd00-154">Чтобы увидеть контакт, новый пользователь должен создать его, после чего этот контакт будет назначен его идентификатору UserId.</span><span class="sxs-lookup"><span data-stu-id="1bd00-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bd00-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1bd00-155">Next steps</span></span>
<span data-ttu-id="1bd00-156">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="1bd00-156">That's it!</span></span> <span data-ttu-id="1bd00-157">Мы преобразовали простое приложение диспетчера контактов в мультитенантное приложение, где у каждого пользователя есть собственный список контактов.</span><span class="sxs-lookup"><span data-stu-id="1bd00-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="1bd00-158">Применение политики безопасности на уровне строк позволило нам избежать сложностей при реализации логики доступа к клиенту в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="1bd00-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="1bd00-159">Эта прозрачность позволяет использовать приложение для реальных бизнес-задач. Кроме того, это позволяет минимизировать риск случайной утечки данных, связанный с увеличением объема кода приложения.</span><span class="sxs-lookup"><span data-stu-id="1bd00-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="1bd00-160">В этом руководстве приводится только беглый обзор возможностей применения политики RLS.</span><span class="sxs-lookup"><span data-stu-id="1bd00-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="1bd00-161">Например, вы можете использовать более сложную или адресную логику доступа, а в хранилище SESSION_CONTEXT могут храниться не только текущие значения идентификаторов UserId.</span><span class="sxs-lookup"><span data-stu-id="1bd00-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="1bd00-162">Кроме того, в можете [интегрировать RLS в клиентские библиотеки средств работы с эластичными базами данных](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) для поддержки мультитенантных сегментов на уровне данных горизонтального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="1bd00-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="1bd00-163">Мы работаем над тем, чтобы сделать политику RLS еще лучше.</span><span class="sxs-lookup"><span data-stu-id="1bd00-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="1bd00-164">Если у вас возникли вопросы или идеи, которые вы хотели бы реализовать, сообщите нам об этом в комментариях.</span><span class="sxs-lookup"><span data-stu-id="1bd00-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="1bd00-165">Ваши отзывы важны для нас!</span><span class="sxs-lookup"><span data-stu-id="1bd00-165">We appreciate your feedback!</span></span>

