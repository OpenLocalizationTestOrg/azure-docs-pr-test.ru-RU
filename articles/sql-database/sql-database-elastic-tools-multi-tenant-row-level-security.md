---
title: "Мультитенантные приложения со средствами эластичных баз данных и безопасностью на уровне строк"
description: "Узнайте, как использовать средства эластичных баз данных совместно с безопасностью на уровне строк для создания приложения с высокомасштабируемым уровнем данных в базе данных SQL Azure, поддерживающей мультитенантные сегменты."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="c8b37-103">Мультитенантные приложения со средствами эластичных баз данных и безопасностью на уровне строк</span><span class="sxs-lookup"><span data-stu-id="c8b37-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="c8b37-104">[Средства эластичных баз данных](sql-database-elastic-scale-get-started.md) и [безопасность на уровне строк (RLS)](https://msdn.microsoft.com/library/dn765131) предоставляют мощный набор возможностей для гибкого и эффективного масштабирования уровня данных мультитенантного приложения с базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b37-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="c8b37-105">Дополнительные сведения см. в статье [Шаблоны разработки для мультитенантных приложений SaaS и базы данных SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c8b37-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="c8b37-106">В этой статье показано, как использовать эти технологии совместно, чтобы создать приложение с высокомасштабируемым уровнем данных, который поддерживает мультиканальные сегменты, используя **ADO.NET SqlClient** и (или) **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="c8b37-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="c8b37-107">**Средства эластичных баз данных** позволяют разработчикам развернуть уровень данных приложения через стандартные методы сегментирования с помощью набора библиотек .NET и шаблонов служб Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b37-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="c8b37-108">Управление сегментами с использованием клиентской библиотеки эластичных баз данных помогает автоматизировать и упростить многие инфраструктурные задачи, которые обычно связаны с сегментированием.</span><span class="sxs-lookup"><span data-stu-id="c8b37-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="c8b37-109">**Безопасность на уровне строк** позволяет разработчикам хранить данные для нескольких клиентов в одной базе данных, а также отфильтровывать строки, не принадлежащие клиенту, выполняющему запрос, с помощью политик безопасности.</span><span class="sxs-lookup"><span data-stu-id="c8b37-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="c8b37-110">Централизующая логика доступа с RLS внутри базы данных, а не внутри приложения, упрощает обслуживание и снижает вероятность возникновения ошибок по мере роста базы кода приложения.</span><span class="sxs-lookup"><span data-stu-id="c8b37-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="c8b37-111">При совместном использовании этих функций приложение может выиграть на снижении издержек и повышении эффективности за счет хранения данных для нескольких клиентов в одной базе данных сегментов.</span><span class="sxs-lookup"><span data-stu-id="c8b37-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="c8b37-112">В то же время приложение по-прежнему обладает достаточной гибкостью, чтобы предоставлять изолированные, принадлежащие однотенантные сегменты для premium-клиентов, которым требуются более строгие гарантии производительности, поскольку мультитенантные сегменты не гарантируют равномерного распространения ресурсов среди клиентов.</span><span class="sxs-lookup"><span data-stu-id="c8b37-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="c8b37-113">Другими словами, API-интерфейсы [маршрутизации, управляемой данными](sql-database-elastic-scale-data-dependent-routing.md) , для клиентской библиотеки эластичных баз данных автоматически подключают клиентов к нужной базе данных сегментов, которая содержит их ключ сегментирования (обычно "TenantId").</span><span class="sxs-lookup"><span data-stu-id="c8b37-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="c8b37-114">После подключения политика безопасности RLS внутри базы данных гарантирует, что клиентам доступны только те строки, которые содержат их TenantId.</span><span class="sxs-lookup"><span data-stu-id="c8b37-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="c8b37-115">Предполагается, что все таблицы содержат столбец TenantId для обозначения того, какие строки принадлежат каждому из клиентов.</span><span class="sxs-lookup"><span data-stu-id="c8b37-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![Архитектура приложений для ведения блогов][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="c8b37-117">Загрузка примера проекта</span><span class="sxs-lookup"><span data-stu-id="c8b37-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="c8b37-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c8b37-118">Prerequisites</span></span>
* <span data-ttu-id="c8b37-119">Используйте Visual Studio 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c8b37-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="c8b37-120">Создайте три базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b37-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="c8b37-121">Скачайте пример проекта: [Elastic DB Tools for Azure SQL — Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="c8b37-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="c8b37-122">Заполните информацию по своим базам данных в начале файла **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="c8b37-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="c8b37-123">Этот проект расширяет проект, описанный в [Elastic DB Tools for Azure SQL — Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) , за счет добавления поддержки для баз данных с мультитенантными сегментами.</span><span class="sxs-lookup"><span data-stu-id="c8b37-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="c8b37-124">Он создает простое консольное приложение для построения блогов и записей с помощью четырех клиентов и двух баз данных с мультитенантными сегментами, как это показано на схеме выше.</span><span class="sxs-lookup"><span data-stu-id="c8b37-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="c8b37-125">Создайте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="c8b37-125">Build and run the application.</span></span> <span data-ttu-id="c8b37-126">Запустится диспетчер карт сегментов для средств эластичных баз данных, выполните следующие проверки:</span><span class="sxs-lookup"><span data-stu-id="c8b37-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="c8b37-127">С помощью Entity Framework и LINQ, создайте новый блог, а затем отобразите все блоги для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="c8b37-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="c8b37-128">С помощью ADO.NET SqlClient отобразите все блоги для клиента.</span><span class="sxs-lookup"><span data-stu-id="c8b37-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="c8b37-129">Попробуйте вставить блог неправильного клиента, чтобы проверить, возникнет ли ошибка.</span><span class="sxs-lookup"><span data-stu-id="c8b37-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="c8b37-130">Обратите внимание, что поскольку RLS пока не включена в базах данных сегментов, каждая из этих проверок выдает ошибки: клиенты видят блоги, которые им не принадлежат, а приложение не запрещается вставить блог неправильному клиенту.</span><span class="sxs-lookup"><span data-stu-id="c8b37-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="c8b37-131">В оставшейся части этой статьи описано, как решить эти проблемы, применив изоляцию клиентов с помощью RLS.</span><span class="sxs-lookup"><span data-stu-id="c8b37-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="c8b37-132">Существует два шага:</span><span class="sxs-lookup"><span data-stu-id="c8b37-132">There are two steps:</span></span> 

1. <span data-ttu-id="c8b37-133">**Уровень приложений.** Измените код приложения, чтобы после открытия подключения в хранилище SESSION_CONTEXT всегда использовалось текущее значение TenantId.</span><span class="sxs-lookup"><span data-stu-id="c8b37-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="c8b37-134">В примере проекта данный шаг уже выполнен.</span><span class="sxs-lookup"><span data-stu-id="c8b37-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="c8b37-135">**Уровень данных.** Создайте в каждой базе данных сегментов политику безопасности RLS, чтобы фильтровать строки на основе значения TenantId, хранимого в SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="c8b37-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="c8b37-136">Этот шаг необходимо выполнить для каждой базы данных сегментов; в противном случае строки мультитенантных сегментов фильтроваться не будут.</span><span class="sxs-lookup"><span data-stu-id="c8b37-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="c8b37-137">Шаг 1. Уровень приложений — выбор значения TenantId в SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="c8b37-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="c8b37-138">После установки соединения с базой данных сегментов с помощью API-интерфейса маршрутизации, управляемой данными, для клиентской библиотеки эластичных баз данных этому приложению по-прежнему необходимо указать базу данных, TenantId которой использует это подключение, чтобы отфильтровать строки, принадлежащих другим клиентам, с помощью политики безопасности RLS.</span><span class="sxs-lookup"><span data-stu-id="c8b37-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="c8b37-139">Чтобы передать эту информацию, рекомендуется сохранить текущее значение TenantId для этого подключения в [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8b37-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="c8b37-140">(Примечание. Также можно использовать [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), но SESSION_CONTEXT — лучший вариант, так как это хранилище проще в использовании. Кроме того, оно возвращает значение NULL по умолчанию и поддерживает пары "ключ — значение".)</span><span class="sxs-lookup"><span data-stu-id="c8b37-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="c8b37-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="c8b37-141">Entity Framework</span></span>
<span data-ttu-id="c8b37-142">Для приложений, использующих Entity Framework, задать нужное значение в SESSION_CONTEXT проще всего в рамках переопределения ElasticScaleContext, как описано в разделе [Маршрутизация на основе данных с помощью EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="c8b37-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="c8b37-143">Перед возвратом подключения, установленного с помощью зависящей от данных маршрутизации, просто создайте и выполните команду SqlCommand, которая устанавливает в SESSION_CONTEXT для TenantId значение shardingKey, указанное для этого подключения.</span><span class="sxs-lookup"><span data-stu-id="c8b37-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="c8b37-144">Таким образом, чтобы задать нужное значение в SESSION_CONTEXT, необходимо написать код один раз.</span><span class="sxs-lookup"><span data-stu-id="c8b37-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

<span data-ttu-id="c8b37-145">Теперь при каждом вызове ElasticScaleContext хранилище SESSION_CONTEXT будет автоматически использоваться с указанным значением TenantId:</span><span class="sxs-lookup"><span data-stu-id="c8b37-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a><span data-ttu-id="c8b37-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="c8b37-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="c8b37-147">Для приложений, которые используют ADO.NET SqlClient, рекомендованный подход заключается в следующем. Вам нужно создать функцию-оболочку для ShardMap.OpenConnectionForKey(), которая перед возвратом подключения автоматически будет задавать в хранилище SESSION_CONTEXT нужное значение ключа TenantId.</span><span class="sxs-lookup"><span data-stu-id="c8b37-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="c8b37-148">Чтобы в хранилище SESSION_CONTEXT всегда использовалось нужное значение, открывайте подключение только с помощью этой функции-оболочки.</span><span class="sxs-lookup"><span data-stu-id="c8b37-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="c8b37-149">Шаг 2. Уровень данных — создание политики безопасности на уровне строк</span><span class="sxs-lookup"><span data-stu-id="c8b37-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="c8b37-150">Создание политики безопасности для фильтрации строк, доступных для всех клиентов</span><span class="sxs-lookup"><span data-stu-id="c8b37-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="c8b37-151">Теперь, когда перед выполнением запроса приложение задает в хранилище SESSION_CONTEXT нужное текущее значение TenantId, политика безопасности RLS может фильтровать запросы и исключать строки с разным значением TenantId.</span><span class="sxs-lookup"><span data-stu-id="c8b37-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="c8b37-152">Политика RLS реализована в инструкциях T-SQL: определяемая пользователем функция определяет логику доступа, а политика безопасности связывает эту функцию с любым количеством таблиц.</span><span class="sxs-lookup"><span data-stu-id="c8b37-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="c8b37-153">В рамках этого проекта функция просто проверяет, что к базе данных подключено приложение (а не какой-либо другой пользователь SQL), а значение TenantId в SESSION_CONTEXT соответствует значению TenantId определенной строки.</span><span class="sxs-lookup"><span data-stu-id="c8b37-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="c8b37-154">Предикат фильтрации отфильтрует для запросов SELECT, UPDATE и DELETE строки, соответствующие этим условиям. А предикат блокировки предотвратит использование в запросах INSERT и UPDATE строк, не соответствующих этим условиям.</span><span class="sxs-lookup"><span data-stu-id="c8b37-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="c8b37-155">Если нужное значение в SESSION_CONTEXT не задано, будет возвращено значение NULL, а видимые строки или строки, доступные для вставки, будут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="c8b37-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="c8b37-156">Чтобы включить RLS, выполните следующий запрос T-SQL на всех сегментах, использующих Visual Studio (SSDT), среду SSMS или сценарий PowerShell, которые включены в проект (либо, если вы используете [службу заданий эластичной базы данных](sql-database-elastic-jobs-overview.md), вы можете использовать ее для автоматизации выполнения этого запроса T-SQL на всех сегментах):</span><span class="sxs-lookup"><span data-stu-id="c8b37-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> <span data-ttu-id="c8b37-157">В более сложных проектах, требующих добавления предиката в сотни таблиц, можно использовать вспомогательную хранимую процедуру, которая автоматически создает политику безопасности, добавляя предикат во все таблицы схемы.</span><span class="sxs-lookup"><span data-stu-id="c8b37-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="c8b37-158">Ознакомьтесь с записью блога [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script) (Применение безопасности на уровне строк ко всем таблицам — вспомогательный сценарий (блог)).</span><span class="sxs-lookup"><span data-stu-id="c8b37-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="c8b37-159">Теперь, если вы снова запустите пример приложения, клиенты смогут просматривать только те строки, которые им принадлежат.</span><span class="sxs-lookup"><span data-stu-id="c8b37-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="c8b37-160">Кроме того, приложение не сможет ни вставлять строки, принадлежащие клиентам, которые в настоящее время не подключены к базе данных сегментов, ни изменять значение TenantId в видимых строках.</span><span class="sxs-lookup"><span data-stu-id="c8b37-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="c8b37-161">Если приложение пытается выполнить одно из этих действий, будет инициировано исключение DbUpdateException.</span><span class="sxs-lookup"><span data-stu-id="c8b37-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="c8b37-162">Если впоследствии вы добавите новую таблицу, просто измените политику безопасности с помощью запроса ALTER и добавьте в новую таблицу предикаты фильтрации и блокировки:</span><span class="sxs-lookup"><span data-stu-id="c8b37-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="c8b37-163">Добавление ограничений по умолчанию на автоматическое заполнение TenantId для команд INSERT</span><span class="sxs-lookup"><span data-stu-id="c8b37-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="c8b37-164">Для каждой таблицы при вставке строк можно установить стандартное ограничение на автоматическое заполнение ключа TenantId значением, в настоящее время хранимым в SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="c8b37-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="c8b37-165">Например:</span><span class="sxs-lookup"><span data-stu-id="c8b37-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="c8b37-166">Теперь приложению не требуется указывать TenantId при вставке строк:</span><span class="sxs-lookup"><span data-stu-id="c8b37-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> <span data-ttu-id="c8b37-167">Если вы используете ограничения по умолчанию для проекта Entity Framework, рекомендуется НЕ включать столбец TenantId в свою модель данных EF.</span><span class="sxs-lookup"><span data-stu-id="c8b37-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="c8b37-168">Это объясняется тем, что запросы Entity Framework автоматически предоставляют значения по умолчанию. Эти значения переопределят применяемые к хранилищу SESSION_CONTEXT ограничения по умолчанию, созданные в инструкциях T-SQL.</span><span class="sxs-lookup"><span data-stu-id="c8b37-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="c8b37-169">Чтобы использовать ограничения по умолчанию, например в примере проекта, следует удалить TenantId из файла DataClasses.cs (и запустить Add-Migration в консоли диспетчера пакетов) и воспользоваться T-SQL, чтобы убедиться, что это поле существует только в таблицах базы данных.</span><span class="sxs-lookup"><span data-stu-id="c8b37-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="c8b37-170">Таким образом, EF не будет автоматически предоставлять неверные значения по умолчанию при вставке данных.</span><span class="sxs-lookup"><span data-stu-id="c8b37-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="c8b37-171">(Необязательно) Включение суперпользователя для получения доступа ко всем строкам</span><span class="sxs-lookup"><span data-stu-id="c8b37-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="c8b37-172">Некоторым приложениям требуется суперпользователь, который имеет доступ ко всем строкам. Например, чтобы включить создание отчетов по всем клиентам всех сегментов или чтобы выполнять операции разделения и объединения сегментов, для которых потребуется перемещение строк между базами данных.</span><span class="sxs-lookup"><span data-stu-id="c8b37-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="c8b37-173">Для этого потребуется создать нового пользователя SQL (в данном случае суперпользователя) в каждой базе данных сегмента.</span><span class="sxs-lookup"><span data-stu-id="c8b37-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="c8b37-174">Затем измените политику безопасности, внеся в нее новую функцию предиката, которая разрешит пользователю доступ ко всем строкам:</span><span class="sxs-lookup"><span data-stu-id="c8b37-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="c8b37-175">Обслуживание</span><span class="sxs-lookup"><span data-stu-id="c8b37-175">Maintenance</span></span>
* <span data-ttu-id="c8b37-176">**Добавление новых сегментов.** Необходимо выполнить скрипт T-SQL, чтобы включить политику RLS для новых сегментов, иначе запросы в таких сегментах фильтроваться не будут.</span><span class="sxs-lookup"><span data-stu-id="c8b37-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="c8b37-177">**Добавление новых таблиц.** Необходимо добавлять предикат фильтрации и блокировки в политику безопасности для всех сегментов каждый раз, когда создается таблица, иначе запросы в такой таблице фильтроваться не будут.</span><span class="sxs-lookup"><span data-stu-id="c8b37-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="c8b37-178">Это действие можно автоматизировать с помощью триггера DDL, как это описано в записи блога [Apply Row-Level Security automatically to newly created tables](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx) (Автоматическое применение безопасности на уровне строк для вновь созданных таблиц).</span><span class="sxs-lookup"><span data-stu-id="c8b37-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="c8b37-179">Сводка</span><span class="sxs-lookup"><span data-stu-id="c8b37-179">Summary</span></span>
<span data-ttu-id="c8b37-180">Средства эластичных баз данных и безопасность на уровне строк могут использоваться совместно для масштабирования уровня данных приложения благодаря поддержке мультитенантных и однотенантных сегментов.</span><span class="sxs-lookup"><span data-stu-id="c8b37-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="c8b37-181">Мультитенантные сегменты могут использоваться для более эффективного хранения данных (особенно в случаях, где большое количество клиентов имеет лишь несколько строк данных), в то время как однотенантные сегменты — для поддержки premium-клиентов с более строгими требованиями к производительности и изоляции.</span><span class="sxs-lookup"><span data-stu-id="c8b37-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="c8b37-182">Дополнительные сведения см. в [справочнике по безопасности на уровне строк](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="c8b37-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c8b37-183">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c8b37-183">Additional resources</span></span>
* [<span data-ttu-id="c8b37-184">Что такое пул эластичных БД Azure?</span><span class="sxs-lookup"><span data-stu-id="c8b37-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="c8b37-185">Общие сведения о возможностях эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="c8b37-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="c8b37-186">Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="c8b37-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="c8b37-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="c8b37-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="c8b37-188">Сведения о приложении Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="c8b37-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="c8b37-189">Вопросы и запросы на функции</span><span class="sxs-lookup"><span data-stu-id="c8b37-189">Questions and Feature Requests</span></span>
<span data-ttu-id="c8b37-190">Все возникшие вопросы задавайте на [форуме по базам данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted), а запросы новых функций оставляйте на [форуме отзывов и предложений по базам данных SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="c8b37-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


