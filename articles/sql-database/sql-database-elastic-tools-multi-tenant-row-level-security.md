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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Мультитенантные приложения со средствами эластичных баз данных и безопасностью на уровне строк
[Инструменты для баз данных эластичного](sql-database-elastic-scale-get-started.md) и [безопасности (RLS) на уровне строк](https://msdn.microsoft.com/library/dn765131) предоставляют мощный набор возможностей для гибкого и эффективного масштабирования уровня данных hello многопользовательского приложения с базой данных SQL Azure. Дополнительные сведения см. в статье [Шаблоны разработки для мультитенантных приложений SaaS и базы данных SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md). 

В этой статье показано, как toouse этих технологий вместе toobuild приложения уровня данных высокомасштабируемых, поддерживающий сегментов несколькими клиентами, с помощью **ADO.NET SqlClient** и/или **Entity Framework**.  

* **Инструменты для баз данных эластичного** позволяет разработчикам tooscale hello данных уровня приложения посредством методов сегментирования отраслевым стандартам, используя набор библиотек .NET и шаблоны служб Azure. Управление сегментов с помощью hello клиентской библиотеке эластичной базы данных помогает автоматизировать и упростить многие из задач инфраструктурных hello, обычно связанные с сегментирования. 
* **Безопасность на уровне строк** позволяет разработчикам toostore данные для нескольких клиентов в hello же базы данных с помощью toofilter политики безопасности, не принадлежащие toohello клиента, выполнив запрос к строк. Централизация логики доступа при использовании RLS hello базы данных, а не в приложении hello упрощает обслуживание и снижает вероятность ошибки hello как codebase приложения увеличивается. 

Используя эти функции вместе, приложения могут использовать преимущества прибыли экономию и эффективности затрат путем хранения данных для нескольких клиентов в hello же сегментов базы данных. На hello одновременно, приложение по-прежнему имеет изолированная, toooffer гибкость hello сегментов одного клиента для клиентов «premium», которые требует более строгие гарантии производительности, поскольку сегментов нескольких клиентов не гарантируют распределение ресурсов равно среди клиентов.  

Иными словами, hello эластичной базы данных клиентской библиотеки [управляемой данными маршрутизацией](sql-database-elastic-scale-data-dependent-routing.md) API-интерфейсы автоматически подключаться клиенты toohello нужный сегмент базы данных, содержащей их ключ сегментирования (обычно «TenantId»). После подключения политику безопасности RLS в базе данных hello гарантирует, что клиенты доступны только строки, содержащие их идентификатора клиента. Предполагается, что все таблицы содержат tooindicate столбец идентификатора клиента, какие строки принадлежат tooeach клиента. 

![Архитектура приложений для ведения блогов][1]

## <a name="download-hello-sample-project"></a>Загрузите образец проекта hello
### <a name="prerequisites"></a>Предварительные требования
* Используйте Visual Studio 2012 или более поздней версии. 
* Создайте три базы данных SQL Azure. 
* Скачайте пример проекта: [Elastic DB Tools for Azure SQL — Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)
  * Введите сведения о hello для баз данных в начале hello **Program.cs** 

Этот проект расширяет hello один описано в [эластичной базы данных средства для SQL Azure — Entity Framework интеграции](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) , добавляя поддержку нескольких клиентов сегментов баз данных. Он создает простое консольное приложение для создания сообщения в блогах и на четыре клиентов и две базы данных нескольких клиентов сегментов стремительного hello выше схемы. 

Постройте и запустите приложение hello. Это будет начальной загрузки hello эластичной базы данных средства диспетчера карты сегментов и выполнения hello следующие тесты: 

1. С помощью Entity Framework и LINQ, создайте новый блог, а затем отобразите все блоги для каждого клиента.
2. С помощью ADO.NET SqlClient отобразите все блоги для клиента.
3. Повторите tooinsert блог tooverify неправильный клиента hello, возникает ошибка  

Обратите внимание, поскольку RLS еще не была включена в базах данных сегментов hello, каждый из этих тестов показывает проблема: это может toosee блоги, которые не принадлежат toothem клиентов и приложения hello не запрещается вставка блог hello неправильный клиента. Hello в этой статье описываются как tooresolve эти проблемы путем применения клиента изоляции при использовании RLS. Существует два шага: 

1. **Уровень приложений**: менять код приложения hello набор tooalways hello текущего идентификатора клиента в hello SESSION_CONTEXT после открытия подключения. Образец Hello проекта уже произошло. 
2. **Уровень данных**: создайте политику безопасности RLS в каждой toofilter сегментов базы данных, хранимых строк на основании hello TenantId в SESSION_CONTEXT. Он потребуется toodo для каждой базы данных сегмента, в противном случае не будут фильтроваться строк в сегментах с несколькими клиентами. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Шаг 1) уровня приложения: значение TenantId в hello SESSION_CONTEXT
После подключения базы данных сегментов tooa с использованием данных hello эластичной базы данных клиентской библиотеки, которые по-прежнему зависимой маршрутизации API-интерфейсы, приложение hello требуется база данных hello tootell какие TenantId использует это соединение, чтобы политику безопасности RLS можно отфильтровать строки принадлежащие tooother клиентов. Здравствуйте, рекомендуемым способом toopass эти сведения toostore hello текущего идентификатора клиента для этого подключения в hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Примечание: в качестве альтернативы можно использовать [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), но SESSION_CONTEXT является лучшим вариантом, так как он проще toouse, по умолчанию возвращает значение NULL и поддерживает пары «ключ значение».)

### <a name="entity-framework"></a>Entity Framework
Для приложений с помощью платформы Entity Framework, hello простой подход — tooset hello, SESSION_CONTEXT в ElasticScaleContext переопределить hello описано в [управляемой данными маршрутизацией с помощью EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Перед возвратом hello подключения через управляемой данными маршрутизацией посредника, создание и выполнение SqlCommand, которое задает «TenantId» в shardingKey toohello SESSION_CONTEXT hello, указанный для этого соединения. В этом случае требуется только код toowrite после tooset hello SESSION_CONTEXT. 

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

Теперь автоматически принимает значение hello SESSION_CONTEXT hello указанного идентификатора клиента при каждом вызове ElasticScaleContext: 

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

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
Для приложений с помощью ADO.NET SqlClient hello рекомендуется toocreate функцию-оболочку вокруг ShardMap.OpenConnectionForKey(), который автоматически задает «TenantId» в hello SESSION_CONTEXT toohello исправить TenantId перед возвратом соединение. tooensure, всегда имеет значение SESSION_CONTEXT, следует открывать только подключения с помощью этой функции-оболочки.

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Шаг 2. Уровень данных — создание политики безопасности на уровне строк
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Создание типа hello toofilter политики безопасности строк, каждый клиент может получить доступ
Теперь, когда приложение hello устанавливает SESSION_CONTEXT с hello текущего идентификатора клиента перед запросом, можно фильтровать запросы и исключить строки, имеющие разные TenantId политику безопасности RLS.  

RLS реализуется в T-SQL: hello логики доступа к определяет определяемую пользователем функцию и политику безопасности привязывает этот номер tooany функции таблиц. Для этого проекта функции hello будет просто убедитесь, что hello приложения (а не SQL другим пользователем) является toohello подключенной базы данных и что hello, «TenantId», хранящимся в hello SESSION_CONTEXT соответствует hello TenantId данной строки. Предикат фильтра позволит строк, удовлетворяющих эти условия toopass через фильтр hello для запросов SELECT, UPDATE и DELETE; и предотвращает предиката блокировки строк, которые нарушают эти условия не INSERTed или обновлено. Если SESSION_CONTEXT не было задано, возвращается NULL и строки не будет видимым или может toobe вставлены. 

tooenable RLS, выполните следующий T-SQL для всех сегментов с помощью либо Visual Studio (SSDT), среда SSMS, hello или скрипт PowerShell, входящий в проекте hello hello (или если вы используете [заданий эластичных баз данных](sql-database-elastic-jobs-overview.md), его можно использовать tooautomate выполнения Это T-SQL для всех сегментов): 

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
> Для более сложных проектов, требующих предиката hello tooadd для сотен таблиц можно использовать вспомогательную хранимую процедуру, которая автоматически создает политику безопасности, добавив предикат для всех таблиц в схеме. В разделе [таблиц tooall применить безопасность на уровне строк — вспомогательный сценарий (блог)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Теперь при запуске образца hello приложение снова клиентов будет доступ toosee только строки, которые принадлежат toothem. Кроме того приложение hello не могут вставлять строки, принадлежащие tootenants отличается от базы данных сегментов одного подключенного toohello hello и не может обновить видимых строк toohave различные TenantId. Приложение hello toodo либо, если возникает DbUpdateException.

Если впоследствии добавить новую таблицу, просто ALTER hello политики безопасности и добавьте предикаты фильтров и блокировки для новых таблиц hello: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Добавить значение по умолчанию ограничения tooautomatically заполнения идентификатора клиента для вставок
Значение по умолчанию можно поместить ограничения для каждой таблицы tooautomatically заполнения hello TenantId с hello в данный момент хранящееся в SESSION_CONTEXT при вставке строк. Например: 

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

Теперь приложение hello не требует toospecify TenantId при вставке строк: 

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
> При использовании ограничения по умолчанию для проекта Entity Framework, рекомендуется не включать столбец идентификатора клиента hello EF модели. Это так, как запросы Entity Framework автоматически предоставлять значения по умолчанию, которые переопределяют hello ограничения по умолчанию в T-SQL, использующих SESSION_CONTEXT. ограничения по умолчанию toouse в hello пример проекта, для экземпляра следует удалить TenantId из DataClasses.cs (и выполнения Add-Migration hello консоль диспетчера пакетов) и tooensure используйте T-SQL, hello поля существует только в таблицах базы данных hello. Таким образом, EF не будет автоматически предоставлять неверные значения по умолчанию при вставке данных. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Необязательно) Включить все строки tooaccess «суперпользователь»
Для некоторых приложений может потребоваться toocreate «суперпользователь», кто имеет доступ к все строки, например, в порядке tooenable отчетов по всей операции разделения или слияния tooperform на сегменты, которые включают перемещение строк клиента между базами данных и всех клиентов на всех сегментах. tooenable это, следует создать нового пользователя SQL («суперпользователь» в данном примере) в каждой базе данных сегментов. Затем измените политику безопасности hello с новой функцию предиката, которая позволяет этот пользователь tooaccess все строки:

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


### <a name="maintenance"></a>Обслуживание, 
* **Добавление новых сегментов**: необходимо выполнить скрипт T-SQL hello tooenable RLS на любые новые сегменты, в противном случае не будут фильтроваться запросы на этих сегментов.
* **Добавление новых таблиц**: необходимо добавить фильтр и блокировать предиката toohello политики безопасности на всех сегментов, каждый раз, когда создается новая таблица, в противном случае не будут фильтроваться запросов для новых таблиц hello. Это можно автоматизировать с помощью триггера DDL, как описано в [применить безопасность на уровне строк автоматически toonewly созданы таблицы (блог)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Сводка
Средства эластичной базы данных и безопасность на уровне строк может быть используется совместно tooscale приложения уровня данных с поддержкой нескольких клиентов и одного клиента сегментов. Сегменты нескольких клиентов может быть используется toostore данных более эффективно (особенно в случаях, когда большое количество клиентов имеют лишь несколько строк данных), во время одного клиента сегментов могут быть используется toosupport premium клиентов с строгой изоляции и производительности требования.  Дополнительные сведения см. в [справочнике по безопасности на уровне строк](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Что такое пул эластичных БД Azure?](sql-database-elastic-pool.md)
* [Общие сведения о возможностях эластичных баз данных](sql-database-elastic-scale-introduction.md)
* [Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Authentication in multitenant apps, using Azure AD and OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Сведения о приложении Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Вопросы и запросы на функции
Ответить на вопросы, пожалуйста направляться на hello toous [форум базы данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) и для запросов, компонент, добавьте их toohello [форуме обратной связи в базе данных SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


