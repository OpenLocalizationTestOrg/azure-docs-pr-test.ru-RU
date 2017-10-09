---
title: "Клиент aaaMulti приложений с помощью средства эластичной базы данных и безопасность на уровне строк"
description: "Узнайте, как средства toouse эластичной базы данных вместе с уровня строк toobuild безопасности приложения с уровнем высокомасштабируемых данных в базе данных SQL Azure, поддерживающий сегментов несколькими клиентами."
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
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="78cca-103">Мультитенантные приложения со средствами эластичных баз данных и безопасностью на уровне строк</span><span class="sxs-lookup"><span data-stu-id="78cca-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="78cca-104">[Инструменты для баз данных эластичного](sql-database-elastic-scale-get-started.md) и [безопасности (RLS) на уровне строк](https://msdn.microsoft.com/library/dn765131) предоставляют мощный набор возможностей для гибкого и эффективного масштабирования уровня данных hello многопользовательского приложения с базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="78cca-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="78cca-105">Дополнительные сведения см. в статье [Шаблоны разработки для мультитенантных приложений SaaS и базы данных SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="78cca-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="78cca-106">В этой статье показано, как toouse этих технологий вместе toobuild приложения уровня данных высокомасштабируемых, поддерживающий сегментов несколькими клиентами, с помощью **ADO.NET SqlClient** и/или **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="78cca-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="78cca-107">**Инструменты для баз данных эластичного** позволяет разработчикам tooscale hello данных уровня приложения посредством методов сегментирования отраслевым стандартам, используя набор библиотек .NET и шаблоны служб Azure.</span><span class="sxs-lookup"><span data-stu-id="78cca-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="78cca-108">Управление сегментов с помощью hello клиентской библиотеке эластичной базы данных помогает автоматизировать и упростить многие из задач инфраструктурных hello, обычно связанные с сегментирования.</span><span class="sxs-lookup"><span data-stu-id="78cca-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="78cca-109">**Безопасность на уровне строк** позволяет разработчикам toostore данные для нескольких клиентов в hello же базы данных с помощью toofilter политики безопасности, не принадлежащие toohello клиента, выполнив запрос к строк.</span><span class="sxs-lookup"><span data-stu-id="78cca-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="78cca-110">Централизация логики доступа при использовании RLS hello базы данных, а не в приложении hello упрощает обслуживание и снижает вероятность ошибки hello как codebase приложения увеличивается.</span><span class="sxs-lookup"><span data-stu-id="78cca-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="78cca-111">Используя эти функции вместе, приложения могут использовать преимущества прибыли экономию и эффективности затрат путем хранения данных для нескольких клиентов в hello же сегментов базы данных.</span><span class="sxs-lookup"><span data-stu-id="78cca-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="78cca-112">На hello одновременно, приложение по-прежнему имеет изолированная, toooffer гибкость hello сегментов одного клиента для клиентов «premium», которые требует более строгие гарантии производительности, поскольку сегментов нескольких клиентов не гарантируют распределение ресурсов равно среди клиентов.</span><span class="sxs-lookup"><span data-stu-id="78cca-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="78cca-113">Иными словами, hello эластичной базы данных клиентской библиотеки [управляемой данными маршрутизацией](sql-database-elastic-scale-data-dependent-routing.md) API-интерфейсы автоматически подключаться клиенты toohello нужный сегмент базы данных, содержащей их ключ сегментирования (обычно «TenantId»).</span><span class="sxs-lookup"><span data-stu-id="78cca-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="78cca-114">После подключения политику безопасности RLS в базе данных hello гарантирует, что клиенты доступны только строки, содержащие их идентификатора клиента.</span><span class="sxs-lookup"><span data-stu-id="78cca-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="78cca-115">Предполагается, что все таблицы содержат tooindicate столбец идентификатора клиента, какие строки принадлежат tooeach клиента.</span><span class="sxs-lookup"><span data-stu-id="78cca-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Архитектура приложений для ведения блогов][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="78cca-117">Загрузите образец проекта hello</span><span class="sxs-lookup"><span data-stu-id="78cca-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="78cca-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="78cca-118">Prerequisites</span></span>
* <span data-ttu-id="78cca-119">Используйте Visual Studio 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="78cca-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="78cca-120">Создайте три базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="78cca-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="78cca-121">Скачайте пример проекта: [Elastic DB Tools for Azure SQL — Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="78cca-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="78cca-122">Введите сведения о hello для баз данных в начале hello **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="78cca-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="78cca-123">Этот проект расширяет hello один описано в [эластичной базы данных средства для SQL Azure — Entity Framework интеграции](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) , добавляя поддержку нескольких клиентов сегментов баз данных.</span><span class="sxs-lookup"><span data-stu-id="78cca-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="78cca-124">Он создает простое консольное приложение для создания сообщения в блогах и на четыре клиентов и две базы данных нескольких клиентов сегментов стремительного hello выше схемы.</span><span class="sxs-lookup"><span data-stu-id="78cca-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="78cca-125">Постройте и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="78cca-125">Build and run hello application.</span></span> <span data-ttu-id="78cca-126">Это будет начальной загрузки hello эластичной базы данных средства диспетчера карты сегментов и выполнения hello следующие тесты:</span><span class="sxs-lookup"><span data-stu-id="78cca-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="78cca-127">С помощью Entity Framework и LINQ, создайте новый блог, а затем отобразите все блоги для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="78cca-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="78cca-128">С помощью ADO.NET SqlClient отобразите все блоги для клиента.</span><span class="sxs-lookup"><span data-stu-id="78cca-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="78cca-129">Повторите tooinsert блог tooverify неправильный клиента hello, возникает ошибка</span><span class="sxs-lookup"><span data-stu-id="78cca-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="78cca-130">Обратите внимание, поскольку RLS еще не была включена в базах данных сегментов hello, каждый из этих тестов показывает проблема: это может toosee блоги, которые не принадлежат toothem клиентов и приложения hello не запрещается вставка блог hello неправильный клиента.</span><span class="sxs-lookup"><span data-stu-id="78cca-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="78cca-131">Hello в этой статье описываются как tooresolve эти проблемы путем применения клиента изоляции при использовании RLS.</span><span class="sxs-lookup"><span data-stu-id="78cca-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="78cca-132">Существует два шага:</span><span class="sxs-lookup"><span data-stu-id="78cca-132">There are two steps:</span></span> 

1. <span data-ttu-id="78cca-133">**Уровень приложений**: менять код приложения hello набор tooalways hello текущего идентификатора клиента в hello SESSION_CONTEXT после открытия подключения.</span><span class="sxs-lookup"><span data-stu-id="78cca-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="78cca-134">Образец Hello проекта уже произошло.</span><span class="sxs-lookup"><span data-stu-id="78cca-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="78cca-135">**Уровень данных**: создайте политику безопасности RLS в каждой toofilter сегментов базы данных, хранимых строк на основании hello TenantId в SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="78cca-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="78cca-136">Он потребуется toodo для каждой базы данных сегмента, в противном случае не будут фильтроваться строк в сегментах с несколькими клиентами.</span><span class="sxs-lookup"><span data-stu-id="78cca-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="78cca-137">Шаг 1) уровня приложения: значение TenantId в hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="78cca-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="78cca-138">После подключения базы данных сегментов tooa с использованием данных hello эластичной базы данных клиентской библиотеки, которые по-прежнему зависимой маршрутизации API-интерфейсы, приложение hello требуется база данных hello tootell какие TenantId использует это соединение, чтобы политику безопасности RLS можно отфильтровать строки принадлежащие tooother клиентов.</span><span class="sxs-lookup"><span data-stu-id="78cca-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="78cca-139">Здравствуйте, рекомендуемым способом toopass эти сведения toostore hello текущего идентификатора клиента для этого подключения в hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="78cca-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="78cca-140">(Примечание: в качестве альтернативы можно использовать [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), но SESSION_CONTEXT является лучшим вариантом, так как он проще toouse, по умолчанию возвращает значение NULL и поддерживает пары «ключ значение».)</span><span class="sxs-lookup"><span data-stu-id="78cca-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="78cca-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="78cca-141">Entity Framework</span></span>
<span data-ttu-id="78cca-142">Для приложений с помощью платформы Entity Framework, hello простой подход — tooset hello, SESSION_CONTEXT в ElasticScaleContext переопределить hello описано в [управляемой данными маршрутизацией с помощью EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="78cca-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="78cca-143">Перед возвратом hello подключения через управляемой данными маршрутизацией посредника, создание и выполнение SqlCommand, которое задает «TenantId» в shardingKey toohello SESSION_CONTEXT hello, указанный для этого соединения.</span><span class="sxs-lookup"><span data-stu-id="78cca-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="78cca-144">В этом случае требуется только код toowrite после tooset hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="78cca-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

<span data-ttu-id="78cca-145">Теперь автоматически принимает значение hello SESSION_CONTEXT hello указанного идентификатора клиента при каждом вызове ElasticScaleContext:</span><span class="sxs-lookup"><span data-stu-id="78cca-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="78cca-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="78cca-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="78cca-147">Для приложений с помощью ADO.NET SqlClient hello рекомендуется toocreate функцию-оболочку вокруг ShardMap.OpenConnectionForKey(), который автоматически задает «TenantId» в hello SESSION_CONTEXT toohello исправить TenantId перед возвратом соединение.</span><span class="sxs-lookup"><span data-stu-id="78cca-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="78cca-148">tooensure, всегда имеет значение SESSION_CONTEXT, следует открывать только подключения с помощью этой функции-оболочки.</span><span class="sxs-lookup"><span data-stu-id="78cca-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="78cca-149">Шаг 2. Уровень данных — создание политики безопасности на уровне строк</span><span class="sxs-lookup"><span data-stu-id="78cca-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="78cca-150">Создание типа hello toofilter политики безопасности строк, каждый клиент может получить доступ</span><span class="sxs-lookup"><span data-stu-id="78cca-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="78cca-151">Теперь, когда приложение hello устанавливает SESSION_CONTEXT с hello текущего идентификатора клиента перед запросом, можно фильтровать запросы и исключить строки, имеющие разные TenantId политику безопасности RLS.</span><span class="sxs-lookup"><span data-stu-id="78cca-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="78cca-152">RLS реализуется в T-SQL: hello логики доступа к определяет определяемую пользователем функцию и политику безопасности привязывает этот номер tooany функции таблиц.</span><span class="sxs-lookup"><span data-stu-id="78cca-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="78cca-153">Для этого проекта функции hello будет просто убедитесь, что hello приложения (а не SQL другим пользователем) является toohello подключенной базы данных и что hello, «TenantId», хранящимся в hello SESSION_CONTEXT соответствует hello TenantId данной строки.</span><span class="sxs-lookup"><span data-stu-id="78cca-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="78cca-154">Предикат фильтра позволит строк, удовлетворяющих эти условия toopass через фильтр hello для запросов SELECT, UPDATE и DELETE; и предотвращает предиката блокировки строк, которые нарушают эти условия не INSERTed или обновлено.</span><span class="sxs-lookup"><span data-stu-id="78cca-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="78cca-155">Если SESSION_CONTEXT не было задано, возвращается NULL и строки не будет видимым или может toobe вставлены.</span><span class="sxs-lookup"><span data-stu-id="78cca-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="78cca-156">tooenable RLS, выполните следующий T-SQL для всех сегментов с помощью либо Visual Studio (SSDT), среда SSMS, hello или скрипт PowerShell, входящий в проекте hello hello (или если вы используете [заданий эластичных баз данных](sql-database-elastic-jobs-overview.md), его можно использовать tooautomate выполнения Это T-SQL для всех сегментов):</span><span class="sxs-lookup"><span data-stu-id="78cca-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="78cca-157">Для более сложных проектов, требующих предиката hello tooadd для сотен таблиц можно использовать вспомогательную хранимую процедуру, которая автоматически создает политику безопасности, добавив предикат для всех таблиц в схеме.</span><span class="sxs-lookup"><span data-stu-id="78cca-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="78cca-158">В разделе [таблиц tooall применить безопасность на уровне строк — вспомогательный сценарий (блог)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="78cca-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="78cca-159">Теперь при запуске образца hello приложение снова клиентов будет доступ toosee только строки, которые принадлежат toothem.</span><span class="sxs-lookup"><span data-stu-id="78cca-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="78cca-160">Кроме того приложение hello не могут вставлять строки, принадлежащие tootenants отличается от базы данных сегментов одного подключенного toohello hello и не может обновить видимых строк toohave различные TenantId.</span><span class="sxs-lookup"><span data-stu-id="78cca-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="78cca-161">Приложение hello toodo либо, если возникает DbUpdateException.</span><span class="sxs-lookup"><span data-stu-id="78cca-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="78cca-162">Если впоследствии добавить новую таблицу, просто ALTER hello политики безопасности и добавьте предикаты фильтров и блокировки для новых таблиц hello:</span><span class="sxs-lookup"><span data-stu-id="78cca-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="78cca-163">Добавить значение по умолчанию ограничения tooautomatically заполнения идентификатора клиента для вставок</span><span class="sxs-lookup"><span data-stu-id="78cca-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="78cca-164">Значение по умолчанию можно поместить ограничения для каждой таблицы tooautomatically заполнения hello TenantId с hello в данный момент хранящееся в SESSION_CONTEXT при вставке строк.</span><span class="sxs-lookup"><span data-stu-id="78cca-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="78cca-165">Например:</span><span class="sxs-lookup"><span data-stu-id="78cca-165">For example:</span></span> 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="78cca-166">Теперь приложение hello не требует toospecify TenantId при вставке строк:</span><span class="sxs-lookup"><span data-stu-id="78cca-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="78cca-167">При использовании ограничения по умолчанию для проекта Entity Framework, рекомендуется не включать столбец идентификатора клиента hello EF модели.</span><span class="sxs-lookup"><span data-stu-id="78cca-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="78cca-168">Это так, как запросы Entity Framework автоматически предоставлять значения по умолчанию, которые переопределяют hello ограничения по умолчанию в T-SQL, использующих SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="78cca-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="78cca-169">ограничения по умолчанию toouse в hello пример проекта, для экземпляра следует удалить TenantId из DataClasses.cs (и выполнения Add-Migration hello консоль диспетчера пакетов) и tooensure используйте T-SQL, hello поля существует только в таблицах базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="78cca-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="78cca-170">Таким образом, EF не будет автоматически предоставлять неверные значения по умолчанию при вставке данных.</span><span class="sxs-lookup"><span data-stu-id="78cca-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="78cca-171">(Необязательно) Включить все строки tooaccess «суперпользователь»</span><span class="sxs-lookup"><span data-stu-id="78cca-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="78cca-172">Для некоторых приложений может потребоваться toocreate «суперпользователь», кто имеет доступ к все строки, например, в порядке tooenable отчетов по всей операции разделения или слияния tooperform на сегменты, которые включают перемещение строк клиента между базами данных и всех клиентов на всех сегментах.</span><span class="sxs-lookup"><span data-stu-id="78cca-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="78cca-173">tooenable это, следует создать нового пользователя SQL («суперпользователь» в данном примере) в каждой базе данных сегментов.</span><span class="sxs-lookup"><span data-stu-id="78cca-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="78cca-174">Затем измените политику безопасности hello с новой функцию предиката, которая позволяет этот пользователь tooaccess все строки:</span><span class="sxs-lookup"><span data-stu-id="78cca-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="78cca-175">Обслуживание, </span><span class="sxs-lookup"><span data-stu-id="78cca-175">Maintenance</span></span>
* <span data-ttu-id="78cca-176">**Добавление новых сегментов**: необходимо выполнить скрипт T-SQL hello tooenable RLS на любые новые сегменты, в противном случае не будут фильтроваться запросы на этих сегментов.</span><span class="sxs-lookup"><span data-stu-id="78cca-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="78cca-177">**Добавление новых таблиц**: необходимо добавить фильтр и блокировать предиката toohello политики безопасности на всех сегментов, каждый раз, когда создается новая таблица, в противном случае не будут фильтроваться запросов для новых таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="78cca-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="78cca-178">Это можно автоматизировать с помощью триггера DDL, как описано в [применить безопасность на уровне строк автоматически toonewly созданы таблицы (блог)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="78cca-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="78cca-179">Сводка</span><span class="sxs-lookup"><span data-stu-id="78cca-179">Summary</span></span>
<span data-ttu-id="78cca-180">Средства эластичной базы данных и безопасность на уровне строк может быть используется совместно tooscale приложения уровня данных с поддержкой нескольких клиентов и одного клиента сегментов.</span><span class="sxs-lookup"><span data-stu-id="78cca-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="78cca-181">Сегменты нескольких клиентов может быть используется toostore данных более эффективно (особенно в случаях, когда большое количество клиентов имеют лишь несколько строк данных), во время одного клиента сегментов могут быть используется toosupport premium клиентов с строгой изоляции и производительности требования.</span><span class="sxs-lookup"><span data-stu-id="78cca-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="78cca-182">Дополнительные сведения см. в [справочнике по безопасности на уровне строк](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="78cca-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="78cca-183">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="78cca-183">Additional resources</span></span>
* [<span data-ttu-id="78cca-184">Что такое пул эластичных БД Azure?</span><span class="sxs-lookup"><span data-stu-id="78cca-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="78cca-185">Общие сведения о возможностях эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="78cca-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="78cca-186">Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="78cca-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="78cca-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="78cca-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="78cca-188">Сведения о приложении Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="78cca-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="78cca-189">Вопросы и запросы на функции</span><span class="sxs-lookup"><span data-stu-id="78cca-189">Questions and Feature Requests</span></span>
<span data-ttu-id="78cca-190">Ответить на вопросы, пожалуйста направляться на hello toous [форум базы данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) и для запросов, компонент, добавьте их toohello [форуме обратной связи в базе данных SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="78cca-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


