---
<span data-ttu-id="01b21-101">Заголовок: aaa» Azure Cosmos DB DocumentDB API: синтаксис SQL | Документы Microsoft» Описание: справочную документацию по классу hello язык запросов SQL Azure Cosmos базы данных DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="01b21-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="01b21-102">службы: cosmos db Автор: диспетчер mimig1: jhubbard редактора: mimig documentationcenter: ''</span><span class="sxs-lookup"><span data-stu-id="01b21-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="01b21-103">MS.AssetId: ms.service: ms.workload cosmos db: ms.tgt_pltfrm службы данных: ms.devlang н/д: н/д ms.topic: ссылки ms.date: ms.author 06/13/2017 г.: mimig</span><span class="sxs-lookup"><span data-stu-id="01b21-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="01b21-104">Справочник по синтаксису SQL-запросов API DocumentDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="01b21-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="01b21-105">Hello Azure Cosmos DB DocumentDB API поддерживает запросов документы с помощью знакомого языка SQL (языка структурированных запросов) как грамматики иерархическим документам JSON, не требуя явной схемы или создания вторичных индексов.</span><span class="sxs-lookup"><span data-stu-id="01b21-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="01b21-106">Этот раздел содержит справочную документацию по hello язык запросов DocumentDB API SQL.</span><span class="sxs-lookup"><span data-stu-id="01b21-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="01b21-107">Пошаговое hello язык запросов DocumentDB API SQL см. в разделе [SQL-запросов для Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="01b21-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="01b21-108">Мы также приглашаем вас toovisit hello [площадку запросов](http://www.documentdb.com/sql/demo) где попробуйте Azure Cosmos DB и выполнение запросов SQL, используя наш набор данных.</span><span class="sxs-lookup"><span data-stu-id="01b21-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="01b21-109">Запрос SELECT</span><span class="sxs-lookup"><span data-stu-id="01b21-109">SELECT query</span></span>  
<span data-ttu-id="01b21-110">Получает документы JSON из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="01b21-111">Он поддерживает вычисление выражений, проектирование, фильтрацию и соединение.</span><span class="sxs-lookup"><span data-stu-id="01b21-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="01b21-112">Hello обозначения, используемые для описания инструкций SELECT hello, приведены в разделе соглашения о синтаксисе hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="01b21-113">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="01b21-114">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-114">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-115">Сведения о каждом из этих предложений см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="01b21-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="01b21-116">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="01b21-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="01b21-117">Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="01b21-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="01b21-118">Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="01b21-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="01b21-119">Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="01b21-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="01b21-120">Hello предложения в инструкции SELECT hello должны быть упорядочены, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="01b21-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="01b21-121">Любое из необязательных предложений hello может быть опущено.</span><span class="sxs-lookup"><span data-stu-id="01b21-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="01b21-122">Но если необязательные предложения используются, они должны следовать в правильном порядке hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="01b21-123">**Логический порядок обработки инструкции SELECT hello**</span><span class="sxs-lookup"><span data-stu-id="01b21-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="01b21-124">— Hello порядок, в котором обрабатываются предложения:</span><span class="sxs-lookup"><span data-stu-id="01b21-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="01b21-125">Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="01b21-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="01b21-126">Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="01b21-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="01b21-127">Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="01b21-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="01b21-128">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="01b21-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="01b21-129">Обратите внимание, что это отличается от порядка hello, в котором они появляются в синтаксис hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="01b21-130">Hello упорядочение выполняется таким образом, что все новые символы, представленные обработанным предложением видны и могут использоваться в предложениях, обрабатываемых позднее.</span><span class="sxs-lookup"><span data-stu-id="01b21-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="01b21-131">Например, псевдонимы, объявленные в предложении FROM, доступны в предложениях WHERE и SELECT.</span><span class="sxs-lookup"><span data-stu-id="01b21-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="01b21-132">**Пробелы и комментарии**</span><span class="sxs-lookup"><span data-stu-id="01b21-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="01b21-133">Все символы пробелов, которые не являются частью строку в кавычках или заключенный в кавычки идентификатор не являются частью грамматики языка hello и учитываются во время синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="01b21-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="01b21-134">Hello язык запросов поддерживает комментарии в стиле T-SQL</span><span class="sxs-lookup"><span data-stu-id="01b21-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="01b21-135">Инструкция SQL `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="01b21-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="01b21-136">Пробелы и комментарии не имеют значения в грамматике hello, они должны быть используется tooseparate маркеры.</span><span class="sxs-lookup"><span data-stu-id="01b21-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="01b21-137">Например, `-1e5` представляет лексему с одним номером, а `: – 1 e5` — лексему "минус" (–), за которой следует номер 1 и идентификатор e5.</span><span class="sxs-lookup"><span data-stu-id="01b21-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="01b21-138"><a name="bk_select_query"></a>Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="01b21-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="01b21-139">Hello предложения в инструкции SELECT hello должны быть упорядочены, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="01b21-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="01b21-140">Любое из необязательных предложений hello может быть опущено.</span><span class="sxs-lookup"><span data-stu-id="01b21-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="01b21-141">Но если необязательные предложения используются, они должны следовать в правильном порядке hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="01b21-142">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="01b21-143">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="01b21-144">Свойства или значение toobe, выбранных для hello результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="01b21-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="01b21-145">Указывает, что значение hello должно быть получено без внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="01b21-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="01b21-146">В частности в том случае, если значение hello обработки является объектом, будет получен все свойства.</span><span class="sxs-lookup"><span data-stu-id="01b21-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="01b21-147">Указывает список свойств toobe получить hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="01b21-148">Каждое возвращаемое значение будет свой объект с указанных свойств hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="01b21-149">Указывает, что вместо hello полного объекта JSON должно быть получено значение JSON hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="01b21-150">Это, в отличие от `<property_list>` не переносится hello предполагаемое значение в объекте.</span><span class="sxs-lookup"><span data-stu-id="01b21-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="01b21-151">Вычислить выражение, представляющее значение toobe hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="01b21-152">Дополнительные сведения см. в разделе [Скалярные выражения](#bk_scalar_expressions).</span><span class="sxs-lookup"><span data-stu-id="01b21-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="01b21-153">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-153">**Remarks**</span></span>  
  
<span data-ttu-id="01b21-154">Hello `SELECT *` синтаксис допустим, только если предложение FROM объявило ровно один псевдоним.</span><span class="sxs-lookup"><span data-stu-id="01b21-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="01b21-155">Синтаксис `SELECT *` обеспечивает проекцию удостоверения, что может пригодиться, если проекция не требуется.</span><span class="sxs-lookup"><span data-stu-id="01b21-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="01b21-156">Кроме того, это единственный действительный синтаксис, если в предложении FROM указан один источник входных данных.</span><span class="sxs-lookup"><span data-stu-id="01b21-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="01b21-157">Обратите внимание, что `SELECT <select_list>` и `SELECT *` — это "синтаксический сахар". При необходимости их можно выразить с помощью простых инструкций SELECT, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="01b21-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="01b21-158">эквивалентно правилу</span><span class="sxs-lookup"><span data-stu-id="01b21-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="01b21-159">эквивалентно правилу</span><span class="sxs-lookup"><span data-stu-id="01b21-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="01b21-160">**См. также**</span><span class="sxs-lookup"><span data-stu-id="01b21-160">**See Also**</span></span>  
  
[<span data-ttu-id="01b21-161">Скалярные выражения</span><span class="sxs-lookup"><span data-stu-id="01b21-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="01b21-162">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="01b21-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="01b21-163"><a name="bk_from_clause"></a>Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="01b21-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="01b21-164">Указывает источник hello или присоединенных источников.</span><span class="sxs-lookup"><span data-stu-id="01b21-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="01b21-165">Hello from является необязательным.</span><span class="sxs-lookup"><span data-stu-id="01b21-165">hello FROM clause is optional.</span></span> <span data-ttu-id="01b21-166">Даже без него другие приложения по-прежнему выполнятся.</span><span class="sxs-lookup"><span data-stu-id="01b21-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="01b21-167">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-167">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="01b21-168">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="01b21-169">Указывает источник данных с псевдонимом или без него.</span><span class="sxs-lookup"><span data-stu-id="01b21-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="01b21-170">Если псевдоним не указан, он будет выведен из hello `<collection_expression>` с помощью следующих правил:</span><span class="sxs-lookup"><span data-stu-id="01b21-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="01b21-171">Если выражение hello представляет собой collection_name, collection_name будет использоваться в качестве псевдонима.</span><span class="sxs-lookup"><span data-stu-id="01b21-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="01b21-172">Если выражение hello `<collection_expression>`, property_name, а затем property_name будет использоваться в качестве псевдонима.</span><span class="sxs-lookup"><span data-stu-id="01b21-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="01b21-173">Если выражение hello представляет собой collection_name, collection_name будет использоваться в качестве псевдонима.</span><span class="sxs-lookup"><span data-stu-id="01b21-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="01b21-174">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="01b21-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="01b21-175">Указывает, что hello `input_alias` — это набор значений, возвращаемых базовым выражением коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="01b21-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="01b21-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="01b21-177">Указывает, что hello `input_alias` должен представлять набор значений, полученных путем итерации всех элементов массива каждого массиве, возвращенном базовым выражением коллекции hello hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="01b21-178">Значения, возвращенные базовым выражением коллекции, которые не являются массивом, игнорируются.</span><span class="sxs-lookup"><span data-stu-id="01b21-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="01b21-179">Указывает выражение toobe hello коллекции документов tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="01b21-180">Указывает, что документ должен быть получен от значения по умолчанию hello, текущей подключенной коллекции.</span><span class="sxs-lookup"><span data-stu-id="01b21-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="01b21-181">Указывает, что документ должен быть получен из коллекции указанный hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="01b21-182">Имя Hello hello коллекции должно соответствовать имя hello коллекции hello, подключенного в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="01b21-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="01b21-183">Указывает, что документ должен быть получен из hello другого источника, определенного по псевдониму предоставленный hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="01b21-184">Указывает, что документ должен быть получен путем обращения к hello `property_name` свойства или элементу массива array_index для всех документов, полученных с указанного выражения коллекции.</span><span class="sxs-lookup"><span data-stu-id="01b21-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="01b21-185">Указывает, что документ должен быть получен путем обращения к hello `property_name` свойства или элементу массива array_index для всех документов, полученных с указанного выражения коллекции.</span><span class="sxs-lookup"><span data-stu-id="01b21-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="01b21-186">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-186">**Remarks**</span></span>  
  
<span data-ttu-id="01b21-187">Все псевдонимы, предоставленные или выведенные в hello `<from_source>(`s) должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="01b21-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="01b21-188">Hello синтаксис `<collection_expression>.`property_name Здравствуйте, таким же, как `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="01b21-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="01b21-189">Однако hello такой синтаксис можно использовать, если имя свойства содержит недопустимые символы.</span><span class="sxs-lookup"><span data-stu-id="01b21-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="01b21-190">**Обработка отсутствующих свойств, элементов массива и неопределенных значений**</span><span class="sxs-lookup"><span data-stu-id="01b21-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="01b21-191">Если выражение коллекции обращается к свойствам или элементам массива и необходимое значение отсутствует, это значение игнорируется и не проходит дальнейшую обработку.</span><span class="sxs-lookup"><span data-stu-id="01b21-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="01b21-192">**Определение области контекста выражения коллекции**</span><span class="sxs-lookup"><span data-stu-id="01b21-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="01b21-193">Выражение коллекции может указываться на уровне коллекции или документа:</span><span class="sxs-lookup"><span data-stu-id="01b21-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="01b21-194">Выражение имеет уровень коллекции, если hello базовым источником выражения коллекции hello является либо ROOT или `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="01b21-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="01b21-195">Такое выражение представляет набор документов, полученных непосредственно из коллекции hello и не зависит от hello обработки других выражений коллекции.</span><span class="sxs-lookup"><span data-stu-id="01b21-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="01b21-196">Выражение имеет уровень документа, если hello является базовым источником выражения коллекции hello `input_alias` представленные ранее в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="01b21-197">Такое выражение представляет набор документов, полученный в результате вычисления выражения коллекции hello в области hello каждого документа, принадлежащего toohello набор, связанный с коллекцией псевдонима hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="01b21-198">Hello результирующий набор будет объединением наборов, полученных при вычислении выражения коллекции hello для каждого из документов hello в базовый набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="01b21-199">**Соединения**</span><span class="sxs-lookup"><span data-stu-id="01b21-199">**Joins**</span></span>  
  
<span data-ttu-id="01b21-200">В текущем выпуске hello Azure Cosmos DB поддерживает внутренние соединения.</span><span class="sxs-lookup"><span data-stu-id="01b21-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="01b21-201">Дополнительные возможности соединения будут добавлены позже.</span><span class="sxs-lookup"><span data-stu-id="01b21-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="01b21-202">Задает результат внутренние соединения в полное перекрестное произведение hello, участвующих в соединении hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="01b21-203">Hello результатом N-стороннего соединения является набор N-элементных кортежей, где каждое значение в кортеж hello связанный с набором, участвующим в соединении hello псевдоним hello и может осуществляться с помощью ссылки на этот псевдоним в других предложениях.</span><span class="sxs-lookup"><span data-stu-id="01b21-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="01b21-204">Вычисление Hello hello соединения зависит от hello области контекста участвующих наборов hello:</span><span class="sxs-lookup"><span data-stu-id="01b21-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="01b21-205">Результатом соединения набора элементов набора A и набора Б уровня коллекции является векторное произведение всех элементов в наборе А и Б.</span><span class="sxs-lookup"><span data-stu-id="01b21-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="01b21-206">Соединение набора A и набора Б уровня документа приводит к объединению всех наборов, полученных при оценке набора Б уровня документа для каждого документа из набора А.</span><span class="sxs-lookup"><span data-stu-id="01b21-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="01b21-207">В текущем выпуске hello обработчиком запросов hello поддерживается более одного выражения уровня коллекции.</span><span class="sxs-lookup"><span data-stu-id="01b21-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="01b21-208">**Примеры соединений**</span><span class="sxs-lookup"><span data-stu-id="01b21-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="01b21-209">Рассмотрим следующую из предложения hello.`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="01b21-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="01b21-210">Разрешите каждому источнику определить `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="01b21-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="01b21-211">Это предложение FROM возвращает набор N-кортежей (кортежей, у которых число значений равно N).</span><span class="sxs-lookup"><span data-stu-id="01b21-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="01b21-212">Каждый кортеж будет иметь значения, полученные путем итерации всех псевдонимов коллекции среди их наборов.</span><span class="sxs-lookup"><span data-stu-id="01b21-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="01b21-213">*Пример соединения 1 с 2 источниками:*</span><span class="sxs-lookup"><span data-stu-id="01b21-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="01b21-214">Определите аргумент `<from_source1>` на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="01b21-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="01b21-215">Определите аргумент `<from_source2>` на уровне документа и добавьте ссылку на input_alias1. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="01b21-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="01b21-216">{1, 2} для `input_alias1 = A,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="01b21-217">{3} для `input_alias1 = B,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="01b21-218">{4, 5} для `input_alias1 = C,`.</span><span class="sxs-lookup"><span data-stu-id="01b21-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="01b21-219">Здравствуйте, предложение FROM `<from_source1> JOIN <from_source2>` приведет к hello следующих кортежей:</span><span class="sxs-lookup"><span data-stu-id="01b21-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="01b21-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="01b21-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="01b21-221">*Пример соединения 2 с 3 источниками:*</span><span class="sxs-lookup"><span data-stu-id="01b21-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="01b21-222">Определите аргумент `<from_source1>` на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="01b21-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="01b21-223">Определите аргумент `<from_source2>` на уровне документа и добавьте ссылку на `input_alias1`. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="01b21-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="01b21-224">{1, 2} для `input_alias1 = A,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="01b21-225">{3} для `input_alias1 = B,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="01b21-226">{4, 5} для `input_alias1 = C,`.</span><span class="sxs-lookup"><span data-stu-id="01b21-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="01b21-227">Определите аргумент `<from_source3>` на уровне документа и добавьте ссылку на `input_alias2`. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="01b21-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="01b21-228">{100, 200} для `input_alias2 = 1,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="01b21-229">{300} для `input_alias2 = 3,`.</span><span class="sxs-lookup"><span data-stu-id="01b21-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="01b21-230">Здравствуйте, предложение FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` приведет к hello следующих кортежей:</span><span class="sxs-lookup"><span data-stu-id="01b21-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="01b21-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="01b21-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="01b21-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="01b21-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="01b21-233">Отсутствие кортежей для других значений `input_alias1`, `input_alias2`, для которых hello `<from_source3>` не вернул все значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="01b21-234">*Пример соединения 3 с 3 источниками:*</span><span class="sxs-lookup"><span data-stu-id="01b21-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="01b21-235">Определите аргумент <from_source1> на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="01b21-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="01b21-236">Определите аргумент `<from_source1>` на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="01b21-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="01b21-237">Определите аргумент <from_source2> на уровне документа и добавьте ссылку на input_alias1. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="01b21-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="01b21-238">{1, 2} для `input_alias1 = A,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="01b21-239">{3} для `input_alias1 = B,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="01b21-240">{4, 5} для `input_alias1 = C,`.</span><span class="sxs-lookup"><span data-stu-id="01b21-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="01b21-241">Разрешить `<from_source3>` объединить слишком`input_alias1` и представлять наборы:</span><span class="sxs-lookup"><span data-stu-id="01b21-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="01b21-242">{100, 200} для `input_alias2 = A,`;</span><span class="sxs-lookup"><span data-stu-id="01b21-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="01b21-243">{300} для `input_alias2 = C,`.</span><span class="sxs-lookup"><span data-stu-id="01b21-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="01b21-244">Здравствуйте, предложение FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` приведет к hello следующих кортежей:</span><span class="sxs-lookup"><span data-stu-id="01b21-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="01b21-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="01b21-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="01b21-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="01b21-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="01b21-247">Это привело к перекрестному произведению между `<from_source2>` и `<from_source3>` , так как оба эти области toohello же `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="01b21-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="01b21-248">Это привело к созданию 4 (2 x 2) кортежей со значением A, 0 кортежей (1 x 0) со значением B и 2 (2x1) кортежей со значением C.</span><span class="sxs-lookup"><span data-stu-id="01b21-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="01b21-249">**См. также**</span><span class="sxs-lookup"><span data-stu-id="01b21-249">**See also**</span></span>  
  
 [<span data-ttu-id="01b21-250">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="01b21-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="01b21-251"><a name="bk_where_clause"></a>Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="01b21-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="01b21-252">Указывает условие поиска hello hello документами, возвращенными запросом hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="01b21-253">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="01b21-254">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="01b21-255">Указывает о toobe документы hello вернул toobe условие hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="01b21-256">Вычислить выражение, представляющее значение toobe hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="01b21-257">В разделе hello [скалярные выражения](#bk_scalar_expressions) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="01b21-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="01b21-258">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-258">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-259">Чтобы hello toobe документа возвращается выражение, указанное как условие фильтра должно возвращать tootrue.</span><span class="sxs-lookup"><span data-stu-id="01b21-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="01b21-260">Только логическое значение true будет удовлетворять условию hello, любое другое значение: undefined, null, значение равно false, число, массив или объект будет удовлетворяет условию hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="01b21-261"><a name="bk_orderby_clause"></a>Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="01b21-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="01b21-262">Указывает порядок для результатов, возвращаемых запросом hello сортировки hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="01b21-263">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="01b21-264">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="01b21-265">Задает свойство или выражение, на котором toosort hello результирующий набор запроса.</span><span class="sxs-lookup"><span data-stu-id="01b21-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="01b21-266">Столбец сортировки можно указать в качестве имени или псевдонима.</span><span class="sxs-lookup"><span data-stu-id="01b21-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="01b21-267">Вы можете указать несколько столбцов сортировки.</span><span class="sxs-lookup"><span data-stu-id="01b21-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="01b21-268">Имена столбцов должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="01b21-268">Column names must be unique.</span></span> <span data-ttu-id="01b21-269">последовательность Hello hello столбцов сортировки в предложении ORDER BY hello определяет организации hello hello сортировки результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="01b21-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="01b21-270">То есть hello результирующий набор сортируется по первым свойством hello и затем упорядоченный список сортируется по второму свойству hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="01b21-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="01b21-271">Hello имена столбцов, на которые ссылается предложение ORDER BY hello должно соответствовать tooeither списка или tooa столбца, определенного в таблице, указанной в предложении FROM hello без неопределенность выберите столбец в hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="01b21-272">Указывает одно свойство или выражение, на какие результирующего набора запроса hello toosort.</span><span class="sxs-lookup"><span data-stu-id="01b21-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="01b21-273">В разделе hello [скалярные выражения](#bk_scalar_expressions) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="01b21-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="01b21-274">Указывает, что значения hello в указанном столбце hello должны сортироваться в порядке возрастания или убывания.</span><span class="sxs-lookup"><span data-stu-id="01b21-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="01b21-275">Значение ASC сортирует от hello наименьшее значение toohighest значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="01b21-276">Значение DESC сортирует от наибольшее значение toolowest значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="01b21-277">Порядок сортировки по умолчанию hello — ASC.</span><span class="sxs-lookup"><span data-stu-id="01b21-277">ASC is hello default sort order.</span></span> <span data-ttu-id="01b21-278">Значения NULL рассматриваются как минимально возможные значения hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="01b21-279">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-279">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-280">Хотя Грамматика hello запросов поддерживает несколько порядок по свойствам, hello Azure Cosmos DB запроса времени выполнения поддерживает сортировки только для одного свойства и только имена свойств, т. е. не для вычисляемых свойств.</span><span class="sxs-lookup"><span data-stu-id="01b21-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="01b21-281">Сортировка также требует hello, что политика индексирования включает индекс диапазона для свойства hello и hello указан тип с наибольшей точностью hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="01b21-282">См. в документации для получения дополнительных сведений по политике индексации toohello.</span><span class="sxs-lookup"><span data-stu-id="01b21-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="01b21-283"><a name="bk_scalar_expressions"></a>Скалярные выражения</span><span class="sxs-lookup"><span data-stu-id="01b21-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="01b21-284">Скалярное выражение представляет собой сочетание символов и операторов, которые могут быть вычисляется tooobtain одно значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="01b21-285">К простым выражениям можно отнести константы, ссылки на свойства, ссылки на элементы массива, ссылки на псевдонимы или вызовы функций.</span><span class="sxs-lookup"><span data-stu-id="01b21-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="01b21-286">C помощью операторов простые выражения можно объединить в сложные.</span><span class="sxs-lookup"><span data-stu-id="01b21-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="01b21-287">Дополнительные сведения о значениях скалярных выражений см. в разделе [Константы](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="01b21-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="01b21-288">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-288">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="01b21-289">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="01b21-290">Представляет значение константы.</span><span class="sxs-lookup"><span data-stu-id="01b21-290">Represents a constant value.</span></span> <span data-ttu-id="01b21-291">Дополнительные сведения см. в разделе [Константы](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="01b21-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="01b21-292">Представляет значение, определяемое hello `input_alias` появился в hello `FROM` предложения.</span><span class="sxs-lookup"><span data-stu-id="01b21-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="01b21-293">Это значение гарантированно toonot быть **не определено** —**не определено** значения во входном файле hello, пропускаются.</span><span class="sxs-lookup"><span data-stu-id="01b21-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="01b21-294">Представляет значение свойства hello объекта.</span><span class="sxs-lookup"><span data-stu-id="01b21-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="01b21-295">Если свойство hello не существует или ссылка на свойство в значение, которое не является объектом, то выражение hello принимает слишком**не определено** значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="01b21-296">Представляет значение hello свойство с именем `property_name` или элементу массива с индексом `array_index` из объекта или массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="01b21-297">Если индекс свойства или массива hello не существует или на значение, которое не является объектом или массивом указана ссылка на индекс свойства или массива hello, hello выражение вычисляет значение tooundefined.</span><span class="sxs-lookup"><span data-stu-id="01b21-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="01b21-298">Представляет оператор, который будет применен tooa одно значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="01b21-299">Дополнительные сведения см. в разделе [Операторы](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="01b21-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="01b21-300">Представляет оператор, который будет применен tootwo значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="01b21-301">Дополнительные сведения см. в разделе [Операторы](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="01b21-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="01b21-302">Представляет значение, определяемое результатом вызова функции.</span><span class="sxs-lookup"><span data-stu-id="01b21-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="01b21-303">Имя пользователя hello определяемой скалярной функции.</span><span class="sxs-lookup"><span data-stu-id="01b21-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="01b21-304">Имя встроенной скалярной функции hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="01b21-305">Представляет значение, полученное в процессе создания объекта с заданными свойствами и их значениями.</span><span class="sxs-lookup"><span data-stu-id="01b21-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="01b21-306">Представляет значение, полученное в процессе создания массива с заданными значениями в качестве элементов.</span><span class="sxs-lookup"><span data-stu-id="01b21-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="01b21-307">Представляет значение hello указанное имя параметра.</span><span class="sxs-lookup"><span data-stu-id="01b21-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="01b21-308">Имена параметров должны быть одиночный символ @ как первый символ hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="01b21-309">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-309">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-310">При вызове встроенной или определяемой пользователем скалярной функции необходимо определить все аргументы.</span><span class="sxs-lookup"><span data-stu-id="01b21-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="01b21-311">Если любой из аргументов hello не определен, не будет вызвана функция hello и hello результат будет неопределенным.</span><span class="sxs-lookup"><span data-stu-id="01b21-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="01b21-312">При создании объекта, любое свойство, которому назначено значение undefined будет пропущена и не включается в созданном объекте hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="01b21-313">При создании массива любое значение элемента, который назначается **не определено** значение будет пропускаться и не включенных в объект создан hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="01b21-314">Это приведет к tootake hello рядом определенный элемент вместо него таким образом, этот массив hello создан не будет пропущенных индексов.</span><span class="sxs-lookup"><span data-stu-id="01b21-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="01b21-315"><a name="bk_operators"></a>Операторы</span><span class="sxs-lookup"><span data-stu-id="01b21-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="01b21-316">В этом разделе описаны операторы hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="01b21-316">This section describes hello supported operators.</span></span> <span data-ttu-id="01b21-317">Каждый оператор может быть назначенных tooexactly одной категории.</span><span class="sxs-lookup"><span data-stu-id="01b21-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="01b21-318">В таблице **Категории операторов** ниже приведены сведения об обработке значений **undefined**, требованиях к типу входных значений и обработке значений несоответствующего типа.</span><span class="sxs-lookup"><span data-stu-id="01b21-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="01b21-319">**Категории операторов**</span><span class="sxs-lookup"><span data-stu-id="01b21-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="01b21-320">**Категория**</span><span class="sxs-lookup"><span data-stu-id="01b21-320">**Category**</span></span>|<span data-ttu-id="01b21-321">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="01b21-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="01b21-322">**Арифметические**</span><span class="sxs-lookup"><span data-stu-id="01b21-322">**arithmetic**</span></span>|<span data-ttu-id="01b21-323">Оператор ожидает, что входными данными toobe номера.</span><span class="sxs-lookup"><span data-stu-id="01b21-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="01b21-324">выходные данные — числа.</span><span class="sxs-lookup"><span data-stu-id="01b21-324">Output is also a Number.</span></span> <span data-ttu-id="01b21-325">Если какие-либо из входных данных hello **не определено** , или тип, отличный от номера, а затем hello результат **не определено**.</span><span class="sxs-lookup"><span data-stu-id="01b21-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="01b21-326">**Битовые**</span><span class="sxs-lookup"><span data-stu-id="01b21-326">**bitwise**</span></span>|<span data-ttu-id="01b21-327">Оператор ожидает, что входными данными toobe 32-разрядное целое число со знаком номера.</span><span class="sxs-lookup"><span data-stu-id="01b21-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="01b21-328">выходные данные — 32-разрядные целые числа со знаками.</span><span class="sxs-lookup"><span data-stu-id="01b21-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="01b21-329">Все нецелочисленные значения округляются.</span><span class="sxs-lookup"><span data-stu-id="01b21-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="01b21-330">Положительные значения округляются в меньшую сторону, а отрицательные — в большую.</span><span class="sxs-lookup"><span data-stu-id="01b21-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="01b21-331">Любое значение, выходящее за пределы диапазона 32-разрядное целое число hello будут преобразованы, выполнив последние 32 бита его дополнительном коде.</span><span class="sxs-lookup"><span data-stu-id="01b21-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="01b21-332">Если какие-либо из входных данных hello **не определено** или тип, отличный от числового, результатом hello является **не определено**.</span><span class="sxs-lookup"><span data-stu-id="01b21-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="01b21-333">**Примечание:** hello выше поведение совместимо с поведением побитового оператора JavaScript.</span><span class="sxs-lookup"><span data-stu-id="01b21-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="01b21-334">**Логические**</span><span class="sxs-lookup"><span data-stu-id="01b21-334">**logical**</span></span>|<span data-ttu-id="01b21-335">Оператор ожидает, что входными данными toobe логические значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="01b21-336">выходные данные — логические значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="01b21-337">Если какие-либо из входных данных hello **не определено** или тип, отличный от логического, результатом hello будет **не определено**.</span><span class="sxs-lookup"><span data-stu-id="01b21-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="01b21-338">**Сравнение**</span><span class="sxs-lookup"><span data-stu-id="01b21-338">**comparison**</span></span>|<span data-ttu-id="01b21-339">Оператор ожидает, что входными данными hello toohave же типа и не быть неопределенным.</span><span class="sxs-lookup"><span data-stu-id="01b21-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="01b21-340">Выходные данные — логические значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="01b21-341">Если какие-либо из входных данных hello **не определено** или hello входные данные имеют разные типы, а затем результат hello **не определено**.</span><span class="sxs-lookup"><span data-stu-id="01b21-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="01b21-342">Сведения об упорядочении значений см. в таблице **Упорядочение сравниваемых значений**.</span><span class="sxs-lookup"><span data-stu-id="01b21-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="01b21-343">**string**</span><span class="sxs-lookup"><span data-stu-id="01b21-343">**string**</span></span>|<span data-ttu-id="01b21-344">Оператор ожидает, что входными данными toobe строки.</span><span class="sxs-lookup"><span data-stu-id="01b21-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="01b21-345">выходные данные — строки.</span><span class="sxs-lookup"><span data-stu-id="01b21-345">Output is also a String.</span></span><br /><span data-ttu-id="01b21-346">Если какие-либо из входных данных hello **не определено** , или тип, отличный от строки, а затем hello результат **не определено**.</span><span class="sxs-lookup"><span data-stu-id="01b21-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="01b21-347">**Унарные операторы**</span><span class="sxs-lookup"><span data-stu-id="01b21-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="01b21-348">**Имя**</span><span class="sxs-lookup"><span data-stu-id="01b21-348">**Name**</span></span>|<span data-ttu-id="01b21-349">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="01b21-349">**Operator**</span></span>|<span data-ttu-id="01b21-350">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="01b21-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="01b21-351">**Арифметические**</span><span class="sxs-lookup"><span data-stu-id="01b21-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="01b21-352">Возвращает значение числа "hello".</span><span class="sxs-lookup"><span data-stu-id="01b21-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="01b21-353">Выполняет побитовую операцию.</span><span class="sxs-lookup"><span data-stu-id="01b21-353">Bitwise negation.</span></span> <span data-ttu-id="01b21-354">Возвращает отрицательное числовое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="01b21-355">**Битовые**</span><span class="sxs-lookup"><span data-stu-id="01b21-355">**bitwise**</span></span>|~|<span data-ttu-id="01b21-356">Дополнение.</span><span class="sxs-lookup"><span data-stu-id="01b21-356">Ones' complement.</span></span> <span data-ttu-id="01b21-357">Возвращает дополнение числового значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="01b21-358">**Логические**</span><span class="sxs-lookup"><span data-stu-id="01b21-358">**Logical**</span></span>|<span data-ttu-id="01b21-359">**NOT**</span><span class="sxs-lookup"><span data-stu-id="01b21-359">**NOT**</span></span>|<span data-ttu-id="01b21-360">Отрицание.</span><span class="sxs-lookup"><span data-stu-id="01b21-360">Negation.</span></span> <span data-ttu-id="01b21-361">Возвращает отрицательное логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="01b21-362">**Бинарные операторы**</span><span class="sxs-lookup"><span data-stu-id="01b21-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="01b21-363">**Имя**</span><span class="sxs-lookup"><span data-stu-id="01b21-363">**Name**</span></span>|<span data-ttu-id="01b21-364">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="01b21-364">**Operator**</span></span>|<span data-ttu-id="01b21-365">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="01b21-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="01b21-366">**Арифметические**</span><span class="sxs-lookup"><span data-stu-id="01b21-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="01b21-367">Сложение.</span><span class="sxs-lookup"><span data-stu-id="01b21-367">Addition.</span></span><br /><br /> <span data-ttu-id="01b21-368">Вычитание.</span><span class="sxs-lookup"><span data-stu-id="01b21-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="01b21-369">Умножение.</span><span class="sxs-lookup"><span data-stu-id="01b21-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="01b21-370">Деление.</span><span class="sxs-lookup"><span data-stu-id="01b21-370">Division.</span></span><br /><br /> <span data-ttu-id="01b21-371">Модуляция.</span><span class="sxs-lookup"><span data-stu-id="01b21-371">Modulation.</span></span>|  
|<span data-ttu-id="01b21-372">**Битовые**</span><span class="sxs-lookup"><span data-stu-id="01b21-372">**bitwise**</span></span>|<span data-ttu-id="01b21-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="01b21-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="01b21-374">Битовый OR.</span><span class="sxs-lookup"><span data-stu-id="01b21-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="01b21-375">Битовый AND.</span><span class="sxs-lookup"><span data-stu-id="01b21-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="01b21-376">Битовый XOR.</span><span class="sxs-lookup"><span data-stu-id="01b21-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="01b21-377">Сдвиг влево.</span><span class="sxs-lookup"><span data-stu-id="01b21-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="01b21-378">Сдвиг вправо.</span><span class="sxs-lookup"><span data-stu-id="01b21-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="01b21-379">Сдвиг вправо с заполнением нулями.</span><span class="sxs-lookup"><span data-stu-id="01b21-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="01b21-380">**Логические**</span><span class="sxs-lookup"><span data-stu-id="01b21-380">**logical**</span></span>|<span data-ttu-id="01b21-381">**AND**</span><span class="sxs-lookup"><span data-stu-id="01b21-381">**AND**</span></span><br /><br /> <span data-ttu-id="01b21-382">**OR**</span><span class="sxs-lookup"><span data-stu-id="01b21-382">**OR**</span></span>|<span data-ttu-id="01b21-383">Логическое умножение.</span><span class="sxs-lookup"><span data-stu-id="01b21-383">Logical conjunction.</span></span> <span data-ttu-id="01b21-384">Возвращает значение **true**, если оба аргумента имеют значение **true**. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="01b21-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-385">Логическое умножение.</span><span class="sxs-lookup"><span data-stu-id="01b21-385">Logical conjunction.</span></span> <span data-ttu-id="01b21-386">Возвращает значение **true**, если оба аргумента имеют значение **true**. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="01b21-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="01b21-387">**Сравнение**</span><span class="sxs-lookup"><span data-stu-id="01b21-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="01b21-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="01b21-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="01b21-389">**??**</span><span class="sxs-lookup"><span data-stu-id="01b21-389">**??**</span></span>|<span data-ttu-id="01b21-390">Равно.</span><span class="sxs-lookup"><span data-stu-id="01b21-390">Equals.</span></span> <span data-ttu-id="01b21-391">Возвращает значение **true**, если оба аргумента равны. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="01b21-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-392">Не равно.</span><span class="sxs-lookup"><span data-stu-id="01b21-392">Not equal to.</span></span> <span data-ttu-id="01b21-393">Возвращает значение **true**, если оба аргумента не равны. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="01b21-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-394">Больше.</span><span class="sxs-lookup"><span data-stu-id="01b21-394">Greater Than.</span></span> <span data-ttu-id="01b21-395">Возвращает **true** Если первый аргумент больше, чем hello второй, возвращают **false** в противном случае.</span><span class="sxs-lookup"><span data-stu-id="01b21-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-396">Больше или равно.</span><span class="sxs-lookup"><span data-stu-id="01b21-396">Greater Than or Equal To.</span></span> <span data-ttu-id="01b21-397">Возвращает **true** Если первого аргумента больше или равно toohello второй, возвращают **false** в противном случае.</span><span class="sxs-lookup"><span data-stu-id="01b21-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-398">Меньше.</span><span class="sxs-lookup"><span data-stu-id="01b21-398">Less Than.</span></span> <span data-ttu-id="01b21-399">Возвращает **true** Если первый аргумент меньше, чем второй hello, возвращают **false** в противном случае.</span><span class="sxs-lookup"><span data-stu-id="01b21-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-400">Меньше или равно.</span><span class="sxs-lookup"><span data-stu-id="01b21-400">Less Than or Equal To.</span></span> <span data-ttu-id="01b21-401">Возвращает **true** Если первого аргумента меньше или равно toohello второй одно возвращаемое **false** в противном случае.</span><span class="sxs-lookup"><span data-stu-id="01b21-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="01b21-402">Слияние.</span><span class="sxs-lookup"><span data-stu-id="01b21-402">Coalesce.</span></span> <span data-ttu-id="01b21-403">Возвращает hello второй аргумент, если первый аргумент hello **не определено** значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="01b21-404">**Строка**</span><span class="sxs-lookup"><span data-stu-id="01b21-404">**String**</span></span>|<span data-ttu-id="01b21-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="01b21-405">**&#124;&#124;**</span></span>|<span data-ttu-id="01b21-406">Объединение.</span><span class="sxs-lookup"><span data-stu-id="01b21-406">Concatenation.</span></span> <span data-ttu-id="01b21-407">Возвращает объединение обоих аргументов.</span><span class="sxs-lookup"><span data-stu-id="01b21-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="01b21-408">**Тернарные операторы**</span><span class="sxs-lookup"><span data-stu-id="01b21-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="01b21-409">Тернарный оператор</span><span class="sxs-lookup"><span data-stu-id="01b21-409">Ternary operator</span></span>|<span data-ttu-id="01b21-410">?</span><span class="sxs-lookup"><span data-stu-id="01b21-410">?</span></span>|<span data-ttu-id="01b21-411">Возвращает hello второй аргумент, если первый аргумент hello принимает слишком**true**; в противном случае возвращает третий аргумент hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="01b21-412">**Упорядочение сравниваемых значений**</span><span class="sxs-lookup"><span data-stu-id="01b21-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="01b21-413">**Тип**</span><span class="sxs-lookup"><span data-stu-id="01b21-413">**Type**</span></span>|<span data-ttu-id="01b21-414">**Порядок значений**</span><span class="sxs-lookup"><span data-stu-id="01b21-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="01b21-415">**Неопределенное**</span><span class="sxs-lookup"><span data-stu-id="01b21-415">**Undefined**</span></span>|<span data-ttu-id="01b21-416">Невозможно сравнить.</span><span class="sxs-lookup"><span data-stu-id="01b21-416">Not comparable.</span></span>|  
|<span data-ttu-id="01b21-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="01b21-417">**Null**</span></span>|<span data-ttu-id="01b21-418">Доступное значение: **Null**</span><span class="sxs-lookup"><span data-stu-id="01b21-418">Single value: **null**</span></span>|  
|<span data-ttu-id="01b21-419">**Число**</span><span class="sxs-lookup"><span data-stu-id="01b21-419">**Number**</span></span>|<span data-ttu-id="01b21-420">Натуральное вещественное число.</span><span class="sxs-lookup"><span data-stu-id="01b21-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="01b21-421">Отрицательное значение бесконечности меньше любого другого числового значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="01b21-422">Положительное значение бесконечности больше любого другого числового значения. Значение **NaN** невозможно сравнить.</span><span class="sxs-lookup"><span data-stu-id="01b21-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="01b21-423">При сравнение с **NaN** возвращается значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="01b21-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="01b21-424">**Строка**</span><span class="sxs-lookup"><span data-stu-id="01b21-424">**String**</span></span>|<span data-ttu-id="01b21-425">Лексикографический порядок.</span><span class="sxs-lookup"><span data-stu-id="01b21-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="01b21-426">**Массив**</span><span class="sxs-lookup"><span data-stu-id="01b21-426">**Array**</span></span>|<span data-ttu-id="01b21-427">Не поддерживает упорядочивание, но равнозначные.</span><span class="sxs-lookup"><span data-stu-id="01b21-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="01b21-428">**Объект**</span><span class="sxs-lookup"><span data-stu-id="01b21-428">**Object**</span></span>|<span data-ttu-id="01b21-429">Не поддерживает упорядочивание, но равнозначные.</span><span class="sxs-lookup"><span data-stu-id="01b21-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="01b21-430">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-430">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-431">В базе данных Azure Cosmos hello типы значений часто неизвестны до их фактического извлечения из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="01b21-432">В порядке toosupport эффективное выполнение запросов большинство hello операторов имеют строгие требования к типам.</span><span class="sxs-lookup"><span data-stu-id="01b21-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="01b21-433">Кроме того, операторы сами по себе не выполняют неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="01b21-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="01b21-434">Это означает, что запрос, такие как: ВЫБЕРИТЕ * FROM ROOT r WHERE r.Age = 21 вернет только документы со свойством Age toohello равно числу 21.</span><span class="sxs-lookup"><span data-stu-id="01b21-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="01b21-435">Документы с строки равно toohello свойства Age «21» или hello строке «0021», не соответствуют, как выражение hello «21» = 21 оценивает tooundefined.</span><span class="sxs-lookup"><span data-stu-id="01b21-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="01b21-436">Это позволяет лучше использовать индексы, так как Уточняющий запрос hello определенного значения (т. е. числа 21) выполняется быстрее, чем поиск неопределенного количества возможных совпадений, (т. е. числа 21 или строк «21», «021», «21,0»...).</span><span class="sxs-lookup"><span data-stu-id="01b21-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="01b21-437">Это отличается от способа вычисления операторов в значениях различных типов на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="01b21-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="01b21-438">**Равенство и сравнение массивов и объектов**</span><span class="sxs-lookup"><span data-stu-id="01b21-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="01b21-439">При сравнении значений массивов или объектов с использованием операторов диапазона (>, >=, <, <=) возвращается значение undefined, так как порядок этих значений не определен.</span><span class="sxs-lookup"><span data-stu-id="01b21-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="01b21-440">Но выполнить структурное сравнение можно с помощью операторов равенства и неравенства (=, !=, <>).</span><span class="sxs-lookup"><span data-stu-id="01b21-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="01b21-441">Два массива считаются равными, если они имеют одинаковое число элементов и сопоставляемые элементы также равны.</span><span class="sxs-lookup"><span data-stu-id="01b21-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="01b21-442">Если сравнение пары элементов приводит к undefined, результатом сравнения массива hello не определен.</span><span class="sxs-lookup"><span data-stu-id="01b21-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="01b21-443">Два объекта считаются равными, если они имеют одинаковые свойства и сопоставляемые свойства также равны.</span><span class="sxs-lookup"><span data-stu-id="01b21-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="01b21-444">Если сравнение пары значений свойств приводит к undefined, результатом сравнения объектов hello не определен.</span><span class="sxs-lookup"><span data-stu-id="01b21-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="01b21-445"><a name="bk_constants"></a>Константы</span><span class="sxs-lookup"><span data-stu-id="01b21-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="01b21-446">Константа (также известная как литерал или скаляр) — это символ, представляющий определенное значение данных.</span><span class="sxs-lookup"><span data-stu-id="01b21-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="01b21-447">Hello формат константы зависит от типа данных hello hello значения, которое он представляет.</span><span class="sxs-lookup"><span data-stu-id="01b21-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="01b21-448">**Поддерживаемые скалярные типы данных**</span><span class="sxs-lookup"><span data-stu-id="01b21-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="01b21-449">**Тип**</span><span class="sxs-lookup"><span data-stu-id="01b21-449">**Type**</span></span>|<span data-ttu-id="01b21-450">**Порядок значений**</span><span class="sxs-lookup"><span data-stu-id="01b21-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="01b21-451">**Неопределенное**</span><span class="sxs-lookup"><span data-stu-id="01b21-451">**Undefined**</span></span>|<span data-ttu-id="01b21-452">Доступное значение: **undefined**</span><span class="sxs-lookup"><span data-stu-id="01b21-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="01b21-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="01b21-453">**Null**</span></span>|<span data-ttu-id="01b21-454">Доступное значение: **Null**</span><span class="sxs-lookup"><span data-stu-id="01b21-454">Single value: **null**</span></span>|  
|<span data-ttu-id="01b21-455">**Логический**</span><span class="sxs-lookup"><span data-stu-id="01b21-455">**Boolean**</span></span>|<span data-ttu-id="01b21-456">Доступные значения: **false**, **true**</span><span class="sxs-lookup"><span data-stu-id="01b21-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="01b21-457">**Число**</span><span class="sxs-lookup"><span data-stu-id="01b21-457">**Number**</span></span>|<span data-ttu-id="01b21-458">Число с плавающей запятой двойной точности, стандарт IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="01b21-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="01b21-459">**Строка**</span><span class="sxs-lookup"><span data-stu-id="01b21-459">**String**</span></span>|<span data-ttu-id="01b21-460">Последовательности из нуля или более знаков Юникода.</span><span class="sxs-lookup"><span data-stu-id="01b21-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="01b21-461">Строки необходимо заключить в одинарные или двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="01b21-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="01b21-462">**Массив**</span><span class="sxs-lookup"><span data-stu-id="01b21-462">**Array**</span></span>|<span data-ttu-id="01b21-463">Последовательность из нуля или более элементов.</span><span class="sxs-lookup"><span data-stu-id="01b21-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="01b21-464">Каждый элемент может иметь значение любого скалярного типа данных (за исключением типа "Неопределенное").</span><span class="sxs-lookup"><span data-stu-id="01b21-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="01b21-465">**Объект**</span><span class="sxs-lookup"><span data-stu-id="01b21-465">**Object**</span></span>|<span data-ttu-id="01b21-466">Неупорядоченный набор из нуля или более пар "имя — значение".</span><span class="sxs-lookup"><span data-stu-id="01b21-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="01b21-467">Имя является строкой Юникода. Значение может иметь любой скалярный тип данных (за исключением типа **Неопределенное**).</span><span class="sxs-lookup"><span data-stu-id="01b21-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="01b21-468">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-468">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="01b21-469">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="01b21-470">Представляет неопределенное значение типа "Неопределенное".</span><span class="sxs-lookup"><span data-stu-id="01b21-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="01b21-471">Представляет значение **Null** типа **Null**.</span><span class="sxs-lookup"><span data-stu-id="01b21-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="01b21-472">Представляет константу типа "Логический".</span><span class="sxs-lookup"><span data-stu-id="01b21-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="01b21-473">Представляет значение **false** типа "Логический".</span><span class="sxs-lookup"><span data-stu-id="01b21-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="01b21-474">Представляет значение **true** типа "Логический".</span><span class="sxs-lookup"><span data-stu-id="01b21-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="01b21-475">Представляет константу.</span><span class="sxs-lookup"><span data-stu-id="01b21-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="01b21-476">Десятичные литералы — это числа, представленные в десятичном или экспоненциальном представлении.</span><span class="sxs-lookup"><span data-stu-id="01b21-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="01b21-477">Шестнадцатеричные литералы — это числа, представленные с помощью префикса 0x, за которым следуют одна или несколько шестнадцатеричных цифр.</span><span class="sxs-lookup"><span data-stu-id="01b21-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="01b21-478">Представляет константу типа "Строка".</span><span class="sxs-lookup"><span data-stu-id="01b21-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="01b21-479">Строковые литералы — это строки Юникода, представленные в виде последовательности из нуля или более знаков Юникода или escape-последовательностей.</span><span class="sxs-lookup"><span data-stu-id="01b21-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="01b21-480">Строковые литералы заключаются в одинарные кавычки (апостроф — ') или двойные кавычки (кавычки — ").</span><span class="sxs-lookup"><span data-stu-id="01b21-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="01b21-481">Допускаются следующие escape-последовательности:</span><span class="sxs-lookup"><span data-stu-id="01b21-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="01b21-482">**escape-последовательность**</span><span class="sxs-lookup"><span data-stu-id="01b21-482">**Escape sequence**</span></span>|<span data-ttu-id="01b21-483">**Описание**</span><span class="sxs-lookup"><span data-stu-id="01b21-483">**Description**</span></span>|<span data-ttu-id="01b21-484">**Символ Юникода**</span><span class="sxs-lookup"><span data-stu-id="01b21-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="01b21-485">\\'</span><span class="sxs-lookup"><span data-stu-id="01b21-485">\\'</span></span>|<span data-ttu-id="01b21-486">Апостроф (')</span><span class="sxs-lookup"><span data-stu-id="01b21-486">apostrophe (')</span></span>|<span data-ttu-id="01b21-487">U+0027</span><span class="sxs-lookup"><span data-stu-id="01b21-487">U+0027</span></span>|  
|<span data-ttu-id="01b21-488">\\"</span><span class="sxs-lookup"><span data-stu-id="01b21-488">\\"</span></span>|<span data-ttu-id="01b21-489">Кавычки (")</span><span class="sxs-lookup"><span data-stu-id="01b21-489">quotation mark (")</span></span>|<span data-ttu-id="01b21-490">U+0022</span><span class="sxs-lookup"><span data-stu-id="01b21-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="01b21-491">Обратная косая черта (\\)</span><span class="sxs-lookup"><span data-stu-id="01b21-491">reverse solidus (\\)</span></span>|<span data-ttu-id="01b21-492">U+005C</span><span class="sxs-lookup"><span data-stu-id="01b21-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="01b21-493">Косая черта (/)</span><span class="sxs-lookup"><span data-stu-id="01b21-493">solidus (/)</span></span>|<span data-ttu-id="01b21-494">U+002F</span><span class="sxs-lookup"><span data-stu-id="01b21-494">U+002F</span></span>|  
|<span data-ttu-id="01b21-495">\b</span><span class="sxs-lookup"><span data-stu-id="01b21-495">\b</span></span>|<span data-ttu-id="01b21-496">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="01b21-496">backspace</span></span>|<span data-ttu-id="01b21-497">U+0008</span><span class="sxs-lookup"><span data-stu-id="01b21-497">U+0008</span></span>|  
|<span data-ttu-id="01b21-498">\f</span><span class="sxs-lookup"><span data-stu-id="01b21-498">\f</span></span>|<span data-ttu-id="01b21-499">Смена страницы</span><span class="sxs-lookup"><span data-stu-id="01b21-499">form feed</span></span>|<span data-ttu-id="01b21-500">U+000C</span><span class="sxs-lookup"><span data-stu-id="01b21-500">U+000C</span></span>|  
|\n|<span data-ttu-id="01b21-501">Перевод строки</span><span class="sxs-lookup"><span data-stu-id="01b21-501">line feed</span></span>|<span data-ttu-id="01b21-502">U+000A</span><span class="sxs-lookup"><span data-stu-id="01b21-502">U+000A</span></span>|  
|<span data-ttu-id="01b21-503">\r</span><span class="sxs-lookup"><span data-stu-id="01b21-503">\r</span></span>|<span data-ttu-id="01b21-504">Возврат каретки</span><span class="sxs-lookup"><span data-stu-id="01b21-504">carriage return</span></span>|<span data-ttu-id="01b21-505">U+000D</span><span class="sxs-lookup"><span data-stu-id="01b21-505">U+000D</span></span>|  
|<span data-ttu-id="01b21-506">\t</span><span class="sxs-lookup"><span data-stu-id="01b21-506">\t</span></span>|<span data-ttu-id="01b21-507">TAB</span><span class="sxs-lookup"><span data-stu-id="01b21-507">tab</span></span>|<span data-ttu-id="01b21-508">U+0009</span><span class="sxs-lookup"><span data-stu-id="01b21-508">U+0009</span></span>|  
|<span data-ttu-id="01b21-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="01b21-509">\uXXXX</span></span>|<span data-ttu-id="01b21-510">Символ Юникода, определяемый 4 шестнадцатеричными цифрами.</span><span class="sxs-lookup"><span data-stu-id="01b21-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="01b21-511">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="01b21-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="01b21-512"><a name="bk_query_perf_guidelines"></a> Рекомендации по повышению производительности запросов</span><span class="sxs-lookup"><span data-stu-id="01b21-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="01b21-513">Чтобы запрос toobe, эффективного выполнения больших коллекции следует использовать фильтры, которые могут обслуживаться одним или несколькими индексами.</span><span class="sxs-lookup"><span data-stu-id="01b21-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="01b21-514">для поиска по индексу будут считаться Hello следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="01b21-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="01b21-515">Используйте оператор равенства (=) с выражением пути к документу и константой.</span><span class="sxs-lookup"><span data-stu-id="01b21-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="01b21-516">Используйте операторы диапазона (<, \<=, >, >=) с выражением пути к документу и числовыми константами.</span><span class="sxs-lookup"><span data-stu-id="01b21-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="01b21-517">Выражение пути к документу означает любое выражение, которое определяет постоянный путь в документах hello из коллекции hello ссылки на базы данных.</span><span class="sxs-lookup"><span data-stu-id="01b21-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="01b21-518">**Выражение пути к документу**</span><span class="sxs-lookup"><span data-stu-id="01b21-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="01b21-519">Выражения пути к документу — это выражения, которые оценивают путь свойства или индексатор массива в документе из коллекции баз данных.</span><span class="sxs-lookup"><span data-stu-id="01b21-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="01b21-520">Этот путь может быть расположение используемых tooidentify hello, упоминаемых в фильтре непосредственно в hello документов в коллекции баз данных hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="01b21-521">Для toobe выражение считается выражением пути к документу следует:</span><span class="sxs-lookup"><span data-stu-id="01b21-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="01b21-522">Справочник по hello коллекции корень напрямую.</span><span class="sxs-lookup"><span data-stu-id="01b21-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="01b21-523">Ссылаться на свойство или индексатор массива констант любого выражения пути к документу.</span><span class="sxs-lookup"><span data-stu-id="01b21-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="01b21-524">Ссылаться на псевдоним, который представляет выражение пути к документу.</span><span class="sxs-lookup"><span data-stu-id="01b21-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="01b21-525">**Соглашения о синтаксисе**</span><span class="sxs-lookup"><span data-stu-id="01b21-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="01b21-526">Hello в следующей таблице описывается синтаксис toodescribe hello соглашения, используемые в справочнике по языку запроса DocumentDB API hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="01b21-527">**Соглашение**</span><span class="sxs-lookup"><span data-stu-id="01b21-527">**Convention**</span></span>|<span data-ttu-id="01b21-528">**Область использования**</span><span class="sxs-lookup"><span data-stu-id="01b21-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="01b21-529">Прописные буквы</span><span class="sxs-lookup"><span data-stu-id="01b21-529">UPPERCASE</span></span>|<span data-ttu-id="01b21-530">Ключевые слова, не учитывающие регистр.</span><span class="sxs-lookup"><span data-stu-id="01b21-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="01b21-531">Нижний регистр</span><span class="sxs-lookup"><span data-stu-id="01b21-531">lowercase</span></span>|<span data-ttu-id="01b21-532">Ключевые слова, учитывающие регистр.</span><span class="sxs-lookup"><span data-stu-id="01b21-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="01b21-533">\<Нетерминальный символ></span><span class="sxs-lookup"><span data-stu-id="01b21-533">\<nonterminal></span></span>|<span data-ttu-id="01b21-534">Нетерминальный символ, определяется отдельно.</span><span class="sxs-lookup"><span data-stu-id="01b21-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="01b21-535">\<Нетерминальный символ> ::=</span><span class="sxs-lookup"><span data-stu-id="01b21-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="01b21-536">Определение синтаксиса нетерминального символа hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="01b21-537">Другие терминальные символы</span><span class="sxs-lookup"><span data-stu-id="01b21-537">other_terminal</span></span>|<span data-ttu-id="01b21-538">Терминальный символ (лексема) подробно описывается в словах.</span><span class="sxs-lookup"><span data-stu-id="01b21-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="01b21-539">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="01b21-539">identifier</span></span>|<span data-ttu-id="01b21-540">Идентификатор.</span><span class="sxs-lookup"><span data-stu-id="01b21-540">Identifier.</span></span> <span data-ttu-id="01b21-541">Поддерживает только следующие знаки: a–z, A–Z, 0–9. Первый знак не может быть цифрой.</span><span class="sxs-lookup"><span data-stu-id="01b21-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="01b21-542">Строка</span><span class="sxs-lookup"><span data-stu-id="01b21-542">"string"</span></span>|<span data-ttu-id="01b21-543">Строка в кавычках.</span><span class="sxs-lookup"><span data-stu-id="01b21-543">Quoted string.</span></span> <span data-ttu-id="01b21-544">Разрешает любые допустимые строки.</span><span class="sxs-lookup"><span data-stu-id="01b21-544">Allows any valid string.</span></span> <span data-ttu-id="01b21-545">См. описание аргумента string_literal.</span><span class="sxs-lookup"><span data-stu-id="01b21-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="01b21-546">Символ</span><span class="sxs-lookup"><span data-stu-id="01b21-546">'symbol'</span></span>|<span data-ttu-id="01b21-547">Литеральный символ, который является частью синтаксиса hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="01b21-548">&#124; (вертикальная линия)</span><span class="sxs-lookup"><span data-stu-id="01b21-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="01b21-549">Варианты элементов синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="01b21-549">Alternatives for syntax items.</span></span> <span data-ttu-id="01b21-550">Можно использовать только один из указанных элементов hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="01b21-551">[ ] /(квадратные скобки)</span><span class="sxs-lookup"><span data-stu-id="01b21-551">[ ] /(brackets)</span></span>|<span data-ttu-id="01b21-552">В квадратных скобках указывается один или несколько дополнительных элементов.</span><span class="sxs-lookup"><span data-stu-id="01b21-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="01b21-553">[ ,…n ]</span><span class="sxs-lookup"><span data-stu-id="01b21-553">[ ,...n ]</span></span>|<span data-ttu-id="01b21-554">Указывает, что предшествующий элемент hello может быть повторяющихся n — количество раз.</span><span class="sxs-lookup"><span data-stu-id="01b21-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="01b21-555">Hello отдельные вхождения элемента разделяются запятыми.</span><span class="sxs-lookup"><span data-stu-id="01b21-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="01b21-556">[ …n ]</span><span class="sxs-lookup"><span data-stu-id="01b21-556">[ ...n ]</span></span>|<span data-ttu-id="01b21-557">Указывает, что предшествующий элемент hello может быть повторяющихся n — количество раз.</span><span class="sxs-lookup"><span data-stu-id="01b21-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="01b21-558">Hello вхождения разделяются пробелами.</span><span class="sxs-lookup"><span data-stu-id="01b21-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="01b21-559"><a name="bk_built_in_functions"></a>Встроенные функции</span><span class="sxs-lookup"><span data-stu-id="01b21-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="01b21-560">Azure Cosmos DB предоставляет множество встроенных функций SQL.</span><span class="sxs-lookup"><span data-stu-id="01b21-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="01b21-561">Ниже перечислены категории встроенных функций Hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="01b21-562">Функция</span><span class="sxs-lookup"><span data-stu-id="01b21-562">Function</span></span>|<span data-ttu-id="01b21-563">Описание</span><span class="sxs-lookup"><span data-stu-id="01b21-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="01b21-564">Математические функции</span><span class="sxs-lookup"><span data-stu-id="01b21-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="01b21-565">Hello математические функции производят вычисления, чаще всего основываясь на входящих значениях, заданных в качестве аргументов и возвращают числовые значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="01b21-566">Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="01b21-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="01b21-567">функции проверки типа Hello разрешить toocheck hello тип выражения в запросах SQL.</span><span class="sxs-lookup"><span data-stu-id="01b21-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="01b21-568">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="01b21-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="01b21-569">Hello строковые функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="01b21-570">Функции массивов</span><span class="sxs-lookup"><span data-stu-id="01b21-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="01b21-571">функции массивов Hello выполняют операции с входным значением массива и возвращают числовое, логическое значение или значение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="01b21-572">Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="01b21-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="01b21-573">Hello Пространственные функции выполняют операцию над пространственного объекта входного значения и возвращают числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="01b21-574"><a name="bk_mathematical_functions"></a>Математические функции</span><span class="sxs-lookup"><span data-stu-id="01b21-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="01b21-575">Hello следующие функции выполняют вычисление, обычно на основании входных значений, заданных в качестве аргументов и возвращают числовое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="01b21-576">ABS</span><span class="sxs-lookup"><span data-stu-id="01b21-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="01b21-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="01b21-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="01b21-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="01b21-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="01b21-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="01b21-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="01b21-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="01b21-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="01b21-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="01b21-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="01b21-582">COS</span><span class="sxs-lookup"><span data-stu-id="01b21-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="01b21-583">COT</span><span class="sxs-lookup"><span data-stu-id="01b21-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="01b21-584">DEGREES</span><span class="sxs-lookup"><span data-stu-id="01b21-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="01b21-585">EXP</span><span class="sxs-lookup"><span data-stu-id="01b21-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="01b21-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="01b21-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="01b21-587">LOG</span><span class="sxs-lookup"><span data-stu-id="01b21-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="01b21-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="01b21-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="01b21-589">PI</span><span class="sxs-lookup"><span data-stu-id="01b21-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="01b21-590">POWER</span><span class="sxs-lookup"><span data-stu-id="01b21-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="01b21-591">RADIANS</span><span class="sxs-lookup"><span data-stu-id="01b21-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="01b21-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="01b21-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="01b21-593">SIN</span><span class="sxs-lookup"><span data-stu-id="01b21-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="01b21-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="01b21-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="01b21-595">SQUARE</span><span class="sxs-lookup"><span data-stu-id="01b21-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="01b21-596">SIGN</span><span class="sxs-lookup"><span data-stu-id="01b21-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="01b21-597">TAN</span><span class="sxs-lookup"><span data-stu-id="01b21-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="01b21-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="01b21-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="01b21-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="01b21-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="01b21-600">Возвращает hello абсолютное (положительное) значение hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-601">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-602">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-603">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-604">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-604">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-605">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-606">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-606">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-607">Hello пример hello результатов с помощью функции hello ABS к трем различным числам.</span><span class="sxs-lookup"><span data-stu-id="01b21-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="01b21-608">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="01b21-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="01b21-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="01b21-610">Возвращает hello угол в радианах, косинус которого является hello указанного числового выражения; также называется арккосинусом.</span><span class="sxs-lookup"><span data-stu-id="01b21-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="01b21-611">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-612">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-613">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-614">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-614">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-615">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-616">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-616">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-617">Hello следующий пример возвращает hello ACOS-1.</span><span class="sxs-lookup"><span data-stu-id="01b21-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="01b21-618">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="01b21-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="01b21-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="01b21-620">Hello Возвращает угол в радианах, синус которого равен hello указано числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="01b21-621">Также называется арксинусом.</span><span class="sxs-lookup"><span data-stu-id="01b21-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="01b21-622">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-623">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-624">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-625">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-625">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-626">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-627">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-627">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-628">Hello следующий пример возвращает hello ASIN-1.</span><span class="sxs-lookup"><span data-stu-id="01b21-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="01b21-629">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="01b21-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="01b21-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="01b21-631">Hello Возвращает угол в радианах, тангенс которого равен hello указано числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="01b21-632">Также называется арктангенсом.</span><span class="sxs-lookup"><span data-stu-id="01b21-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="01b21-633">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-634">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-635">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-636">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-636">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-637">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-638">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-638">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-639">Следующий пример, что возвращает hello ATAN hello Hello заданное значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="01b21-640">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="01b21-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="01b21-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="01b21-642">Возвращает главное значение hello hello арктангенса y / x, выраженное в радианах.</span><span class="sxs-lookup"><span data-stu-id="01b21-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="01b21-643">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-644">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-645">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-646">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-646">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-647">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-648">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-648">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-649">Hello следующий пример вычисляет hello ATN2 для hello указан x и y компонентов.</span><span class="sxs-lookup"><span data-stu-id="01b21-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="01b21-650">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="01b21-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="01b21-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="01b21-652">Возвращает hello наименьшее целочисленное значение больше или равно, hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-653">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-654">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-655">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-656">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-656">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-657">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-658">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-658">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-659">Hello в следующем примере показаны положительные числовые, отрицательные, и функция CEILING hello нулевые значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="01b21-660">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="01b21-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="01b21-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="01b21-662">Возвращает hello hello в тригонометрический косинус указанного угла в радианах, в hello указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="01b21-663">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-664">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-665">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-666">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-666">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-667">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-668">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-668">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-669">Следующий пример Hello вычисляет hello COS hello, который задан угол.</span><span class="sxs-lookup"><span data-stu-id="01b21-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="01b21-670">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="01b21-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="01b21-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="01b21-672">Возвращает hello hello в тригонометрический котангенс указанного угла в радианах, в hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-673">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-674">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-675">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-676">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-676">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-677">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-678">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-678">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-679">Следующий пример Hello вычисляет hello COT заданного угла hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="01b21-680">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="01b21-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="01b21-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="01b21-682">Возвращает hello соответствующее значение угла в градусах для значения угла в радианах.</span><span class="sxs-lookup"><span data-stu-id="01b21-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="01b21-683">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-684">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-685">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-686">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-686">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-687">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-688">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-688">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-689">Hello следующий пример возвращает hello число градусов в угле, равном PI/2 радиан.</span><span class="sxs-lookup"><span data-stu-id="01b21-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="01b21-690">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="01b21-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="01b21-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="01b21-692">Возвращает наибольшее целое число hello меньше или равно toohello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-693">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-694">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-695">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-696">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-696">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-697">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-698">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-698">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-699">Hello в следующем примере показаны положительные числовые, отрицательные, и функция FLOOR hello нулевые значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="01b21-700">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="01b21-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="01b21-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="01b21-702">Возвращает значение экспоненты hello объекта hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-703">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-704">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-705">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-706">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-706">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-707">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-708">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-708">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-709">Константа Hello **e** (2,718281...) является hello базовый натуральных логарифмов.</span><span class="sxs-lookup"><span data-stu-id="01b21-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="01b21-710">Hello экспоненты числа является константой hello **e** возникает toohello степень числа hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="01b21-711">Например, EXP(1.0) = e^1.0 = 2,71828182845905 и EXP(10) = e^10 = 22026,4657948067.</span><span class="sxs-lookup"><span data-stu-id="01b21-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="01b21-712">Экспонента натурального логарифма hello числа Hello — номер hello, сам: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="01b21-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="01b21-713">А hello натуральный логарифм экспоненты числа hello — номер hello, сам: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="01b21-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="01b21-714">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-714">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-715">Hello в примере объявляется переменная и возвращает значение экспоненты hello hello указанной переменной (10).</span><span class="sxs-lookup"><span data-stu-id="01b21-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="01b21-716">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="01b21-717">Hello следующий пример возвращает значение экспоненты hello hello натурального логарифма 20 и натуральный логарифм hello hello экспоненты 20.</span><span class="sxs-lookup"><span data-stu-id="01b21-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="01b21-718">Поскольку эти функции являются обратными друг от друга, возвращаемому значению hello округления чисел с плавающей запятой, что в обоих случаях — 20.</span><span class="sxs-lookup"><span data-stu-id="01b21-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="01b21-719">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="01b21-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="01b21-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="01b21-721">Возвращает hello натуральный логарифм hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-722">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="01b21-723">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-724">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="01b21-725">Дополнительный числовой аргумент, который задает hello базовой логарифм hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="01b21-726">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-726">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-727">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-728">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-728">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-729">По умолчанию LOG() возвращает натуральный логарифм hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="01b21-730">Hello основание системы счисления hello логарифм tooanother значения можно изменить с помощью дополнительного параметра основания hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="01b21-731">Hello натуральный логарифм — базовый toohello логарифм hello **e**, где **e** является иррациональная константа приблизительно равно too2.718281828.</span><span class="sxs-lookup"><span data-stu-id="01b21-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="01b21-732">Номер hello сам является Hello натуральный логарифм экспоненты числа hello: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="01b21-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="01b21-733">А hello экспоненту hello натуральный логарифм числа — номер hello, сам: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="01b21-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="01b21-734">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-734">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-735">Hello в примере объявляется переменная и возвращает значение логарифма hello hello указанной переменной (10).</span><span class="sxs-lookup"><span data-stu-id="01b21-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="01b21-736">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="01b21-737">Hello следующий пример вычисляет hello ЖУРНАЛА для hello экспоненты числа.</span><span class="sxs-lookup"><span data-stu-id="01b21-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="01b21-738">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="01b21-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="01b21-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="01b21-740">Возвращает логарифм по основанию 10 hello hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-741">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-742">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-743">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-744">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-744">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-745">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-746">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="01b21-746">**Remarks**</span></span>  
  
 <span data-ttu-id="01b21-747">Hello LOG10 и POWER функции являются обратно связанные tooone другой.</span><span class="sxs-lookup"><span data-stu-id="01b21-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="01b21-748">Например, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="01b21-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="01b21-749">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-749">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-750">Hello в примере объявляется переменная и возвращает значение LOG10 hello hello указанной переменной (100).</span><span class="sxs-lookup"><span data-stu-id="01b21-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="01b21-751">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="01b21-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="01b21-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="01b21-753">Возвращает hello константное значение PI.</span><span class="sxs-lookup"><span data-stu-id="01b21-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="01b21-754">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="01b21-755">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-756">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-757">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-757">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-758">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-759">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-759">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-760">Hello следующий пример возвращает hello число пи.</span><span class="sxs-lookup"><span data-stu-id="01b21-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="01b21-761">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="01b21-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="01b21-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="01b21-763">Здравствуйте, возвращает значение указанного hello toohello выражения указанная степень.</span><span class="sxs-lookup"><span data-stu-id="01b21-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="01b21-764">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="01b21-765">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-766">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="01b21-767">— Hello power toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="01b21-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="01b21-768">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-768">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-769">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-770">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-770">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-771">Следующий пример Hello показано возведение числа toohello степень 3 (куб hello hello числа).</span><span class="sxs-lookup"><span data-stu-id="01b21-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="01b21-772">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="01b21-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="01b21-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="01b21-774">Возвращает значение угла в радианах для числового значения, указанного в градусах.</span><span class="sxs-lookup"><span data-stu-id="01b21-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="01b21-775">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-776">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-777">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-778">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-778">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-779">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-780">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-780">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-781">Hello в примере берется несколько углов в качестве входных данных и возвращает их соответствующие значения в радианах.</span><span class="sxs-lookup"><span data-stu-id="01b21-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="01b21-782">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="01b21-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="01b21-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="01b21-784">Возвращает числовое значение, округленное toohello ближайшего целого значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="01b21-785">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-786">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-787">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-788">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-788">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-789">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-790">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-790">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-791">Hello примере округляет hello следующие положительные и отрицательные числа toohello ближайшего целого.</span><span class="sxs-lookup"><span data-stu-id="01b21-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="01b21-792">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="01b21-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="01b21-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="01b21-794">Здравствуйте, возвращает положительное (+ 1), ноль (0) или отрицательный знак (-1) hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-795">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-796">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-797">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-798">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-798">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-799">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-800">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-800">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-801">Hello следующий пример возвращает hello значения знака для чисел от-2 too2.</span><span class="sxs-lookup"><span data-stu-id="01b21-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="01b21-802">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="01b21-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="01b21-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="01b21-804">Возвращает hello hello в Тригонометрический синус указанного угла в радианах, в hello указанное выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="01b21-805">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-806">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-807">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-808">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-808">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-809">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-810">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-810">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-811">Следующий пример Hello вычисляет hello SIN указанного угла hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="01b21-812">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="01b21-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="01b21-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="01b21-814">Возвращает hello квадратный корень из hello указано числовое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="01b21-815">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-816">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-817">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-818">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-818">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-819">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-820">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-820">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-821">Hello следующий пример возвращает hello квадратные корни чисел 1 – 3.</span><span class="sxs-lookup"><span data-stu-id="01b21-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="01b21-822">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="01b21-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="01b21-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="01b21-824">Квадратный из hello hello возвращает указанное числовое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="01b21-825">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-826">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-827">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-828">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-828">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-829">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-830">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-830">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-831">Hello следующий пример возвращает hello квадратов чисел 1 – 3.</span><span class="sxs-lookup"><span data-stu-id="01b21-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="01b21-832">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="01b21-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="01b21-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="01b21-834">Возвращает тангенс hello hello указанного угла в радианах, в hello определенных выражением.</span><span class="sxs-lookup"><span data-stu-id="01b21-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="01b21-835">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-836">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-837">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-838">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-838">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-839">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-840">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-840">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-841">Hello следующем примере вычисляется тангенс hello PI () / 2.</span><span class="sxs-lookup"><span data-stu-id="01b21-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="01b21-842">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="01b21-843"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="01b21-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="01b21-844">Возвращает числовое значение, усеченное toohello ближайшего целого значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="01b21-845">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="01b21-846">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="01b21-847">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-848">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-848">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-849">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-850">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-850">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-851">Следующий пример Hello усекает hello следующие положительные и отрицательные числа toohello ближайшее целое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="01b21-852">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="01b21-853"><a name="bk_type_checking_functions"></a> Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="01b21-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="01b21-854">Hello следующие функции поддерживают проверку типа входных значений, и каждая возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="01b21-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="01b21-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="01b21-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="01b21-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="01b21-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="01b21-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="01b21-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="01b21-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="01b21-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="01b21-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="01b21-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="01b21-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="01b21-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="01b21-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="01b21-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="01b21-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="01b21-863"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="01b21-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="01b21-864">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является массивом.</span><span class="sxs-lookup"><span data-stu-id="01b21-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="01b21-865">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="01b21-866">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-867">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-868">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-868">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-869">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-870">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-870">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-871">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_ARRAY hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-872">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="01b21-873"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="01b21-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="01b21-874">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является логическим.</span><span class="sxs-lookup"><span data-stu-id="01b21-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="01b21-875">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="01b21-876">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-877">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-878">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-878">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-879">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-880">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-880">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-881">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_BOOL hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-882">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="01b21-883"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="01b21-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="01b21-884">Возвращает логическое значение, указывающее, если свойство hello назначено значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="01b21-885">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="01b21-886">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-887">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-888">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-888">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-889">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-890">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-890">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-891">Следующий пример проверяет наличие hello свойство в пределах hello Hello указан документ JSON.</span><span class="sxs-lookup"><span data-stu-id="01b21-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="01b21-892">Hello сначала возвращает значение true, так как «» присутствует, но hello второй возвращает значение false, так как отсутствует «b».</span><span class="sxs-lookup"><span data-stu-id="01b21-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="01b21-893">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="01b21-894"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="01b21-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="01b21-895">Возвращает логическое значение, указывающее, если тип hello hello задать выражение имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="01b21-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="01b21-896">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="01b21-897">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-898">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-899">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-899">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-900">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-901">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-901">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-902">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_NULL hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-903">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="01b21-904"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="01b21-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="01b21-905">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является числом.</span><span class="sxs-lookup"><span data-stu-id="01b21-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="01b21-906">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="01b21-907">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-908">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-909">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-909">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-910">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-911">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-911">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-912">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_NULL hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-913">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="01b21-914"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="01b21-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="01b21-915">Возвращает логическое значение, указывающее, если тип hello hello задать выражение, объект JSON.</span><span class="sxs-lookup"><span data-stu-id="01b21-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="01b21-916">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="01b21-917">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-918">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-919">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-919">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-920">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-921">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-921">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-922">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_OBJECT hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-923">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="01b21-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="01b21-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="01b21-925">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является примитивом (строка, логическое значение, числовое значение или null).</span><span class="sxs-lookup"><span data-stu-id="01b21-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="01b21-926">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="01b21-927">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-928">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-929">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-929">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-930">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-931">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-931">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-932">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_PRIMITIVE hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-933">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="01b21-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="01b21-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="01b21-935">Возвращает логическое значение, указывающее, если тип hello hello выражения является строка.</span><span class="sxs-lookup"><span data-stu-id="01b21-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="01b21-936">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="01b21-937">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="01b21-938">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-939">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-939">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-940">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-941">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-941">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-942">Hello следующий пример проверяет объекты JSON Boolean, number, string, значение null, объект, массив и неопределенных типов, с помощью функции IS_STRING hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="01b21-943">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="01b21-944"><a name="bk_string_functions"></a> Строковые функции</span><span class="sxs-lookup"><span data-stu-id="01b21-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="01b21-945">Hello следующие скалярные функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="01b21-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="01b21-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="01b21-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="01b21-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="01b21-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="01b21-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="01b21-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="01b21-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="01b21-950">LEFT</span><span class="sxs-lookup"><span data-stu-id="01b21-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="01b21-951">LENGTH</span><span class="sxs-lookup"><span data-stu-id="01b21-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="01b21-952">LOWER</span><span class="sxs-lookup"><span data-stu-id="01b21-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="01b21-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="01b21-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="01b21-954">REPLACE</span><span class="sxs-lookup"><span data-stu-id="01b21-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="01b21-955">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="01b21-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="01b21-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="01b21-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="01b21-957">RIGHT</span><span class="sxs-lookup"><span data-stu-id="01b21-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="01b21-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="01b21-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="01b21-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="01b21-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="01b21-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="01b21-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="01b21-961">UPPER</span><span class="sxs-lookup"><span data-stu-id="01b21-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="01b21-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="01b21-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="01b21-963">Возвращает строку, являющуюся результатом объединения двух или более строковых значений hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="01b21-964">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="01b21-965">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-966">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-967">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-967">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-968">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-969">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-969">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-970">Следующий пример возвращает строку hello объединенные hello Hello указанные значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="01b21-971">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="01b21-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="01b21-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="01b21-973">Возвращает логическое значение, указывающее, является ли hello первое строковое выражение содержит hello второй.</span><span class="sxs-lookup"><span data-stu-id="01b21-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="01b21-974">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="01b21-975">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-976">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-977">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-977">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-978">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-979">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-979">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-980">Hello следующий пример проверяет «abc» содержит «ab» и содержит «d».</span><span class="sxs-lookup"><span data-stu-id="01b21-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="01b21-981">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="01b21-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="01b21-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="01b21-983">Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй.</span><span class="sxs-lookup"><span data-stu-id="01b21-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="01b21-984">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="01b21-985">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-986">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-987">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-987">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-988">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-989">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-989">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-990">Hello следующий пример возвращает hello, «abc» заканчивается «b» и «bc».</span><span class="sxs-lookup"><span data-stu-id="01b21-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="01b21-991">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="01b21-992"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="01b21-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="01b21-993">Возвращает hello, начальная позиция первого вхождения hello hello второго строкового выражения внутри первого указанного строкового выражения hello, или значение -1, если строка hello не найдена.</span><span class="sxs-lookup"><span data-stu-id="01b21-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="01b21-994">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="01b21-995">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-996">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-997">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-997">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-998">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-999">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-999">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1000">Hello следующем примере возвращается индекс различных подстрок внутри «abc» hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="01b21-1001">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="01b21-1002"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="01b21-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="01b21-1003">Возвращает hello левую часть строки с hello указанное число символов.</span><span class="sxs-lookup"><span data-stu-id="01b21-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="01b21-1004">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="01b21-1005">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1006">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="01b21-1007">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-1008">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1009">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1010">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1010">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1011">Hello следующий пример возвращает hello в левом верхнем углу «abc» для различных значений длины.</span><span class="sxs-lookup"><span data-stu-id="01b21-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="01b21-1012">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="01b21-1013"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="01b21-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="01b21-1014">Количество символов для hello hello возвращает указанного строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="01b21-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="01b21-1015">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="01b21-1016">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1017">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1018">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1019">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1020">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1020">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1021">Hello следующий пример возвращает длину строки hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="01b21-1022">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="01b21-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="01b21-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="01b21-1024">Возвращает строковое выражение после преобразования данных toolowercase символ верхнего регистра.</span><span class="sxs-lookup"><span data-stu-id="01b21-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="01b21-1025">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="01b21-1026">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1027">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1028">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1029">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1030">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1030">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1031">Следующий пример показывает как Hello toouse НИЖНЕГО в запросе.</span><span class="sxs-lookup"><span data-stu-id="01b21-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="01b21-1032">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="01b21-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="01b21-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="01b21-1034">Возвращает строковое выражение после удаления начальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="01b21-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="01b21-1035">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="01b21-1036">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1037">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1038">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1039">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1040">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1040">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1041">Следующий пример показывает как Hello toouse LTRIM внутри запроса.</span><span class="sxs-lookup"><span data-stu-id="01b21-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="01b21-1042">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="01b21-1043"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="01b21-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="01b21-1044">Заменяет все вхождения указанного строкового значения другим строковым значением.</span><span class="sxs-lookup"><span data-stu-id="01b21-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="01b21-1045">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="01b21-1046">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1047">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1048">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1049">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1050">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1050">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1051">Hello в следующем примере показано, как toouse ЗАМЕНИТЕ в запросе.</span><span class="sxs-lookup"><span data-stu-id="01b21-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="01b21-1052">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="01b21-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="01b21-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="01b21-1054">Повторяет строковое значение указанное число раз.</span><span class="sxs-lookup"><span data-stu-id="01b21-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="01b21-1055">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="01b21-1056">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1057">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="01b21-1058">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-1059">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1060">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1061">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1061">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1062">Hello в следующем примере показано, как РЕПЛИЦИРОВАТЬ toouse в запросе.</span><span class="sxs-lookup"><span data-stu-id="01b21-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="01b21-1063">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="01b21-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="01b21-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="01b21-1065">Возвращает hello строковое значение в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="01b21-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="01b21-1066">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="01b21-1067">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1068">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1069">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1070">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1071">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1071">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1072">Hello, следующий пример показывает, как ОТМЕНИТЬ toouse в запросе.</span><span class="sxs-lookup"><span data-stu-id="01b21-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="01b21-1073">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="01b21-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="01b21-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="01b21-1075">Возвращает hello правой части строки с hello указанное число символов.</span><span class="sxs-lookup"><span data-stu-id="01b21-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="01b21-1076">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="01b21-1077">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1078">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="01b21-1079">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-1080">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1081">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1082">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1082">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1083">Hello следующий пример возвращает hello правую часть «abc» для различных значений длины.</span><span class="sxs-lookup"><span data-stu-id="01b21-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="01b21-1084">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="01b21-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="01b21-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="01b21-1086">Возвращает строковое выражение после удаления конечных пробелов.</span><span class="sxs-lookup"><span data-stu-id="01b21-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="01b21-1087">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="01b21-1088">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1089">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1090">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1091">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1092">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1092">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1093">Следующий пример показывает как Hello toouse RTRIM внутри запроса.</span><span class="sxs-lookup"><span data-stu-id="01b21-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="01b21-1094">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="01b21-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="01b21-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="01b21-1096">Возвращает логическое значение, указывающее, является ли первое строковое выражение hello начинается с hello во-вторых.</span><span class="sxs-lookup"><span data-stu-id="01b21-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="01b21-1097">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="01b21-1098">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1099">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1100">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1101">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-1102">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1102">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1103">Hello следующий пример проверяет hello строка «abc» начинается с «b» и «».</span><span class="sxs-lookup"><span data-stu-id="01b21-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="01b21-1104">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="01b21-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="01b21-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="01b21-1106">Возвращает часть строкового выражения, начиная с hello указан символ Отсчитываемая от нуля позиция и продолжает toohello указывается длина или toohello конца строки hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="01b21-1107">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="01b21-1108">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1109">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="01b21-1110">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-1111">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1112">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1113">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1113">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1114">Hello следующий пример возвращает hello подстрока «abc» начиная с 1 и длиной 1 символ.</span><span class="sxs-lookup"><span data-stu-id="01b21-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="01b21-1115">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="01b21-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="01b21-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="01b21-1117">Возвращает строковое выражение после преобразования данных toouppercase строчные буквы.</span><span class="sxs-lookup"><span data-stu-id="01b21-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="01b21-1118">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="01b21-1119">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="01b21-1120">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="01b21-1121">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1122">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="01b21-1123">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1123">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1124">Следующий пример показывает как Hello toouse ВЕРХНЕМ в запросе</span><span class="sxs-lookup"><span data-stu-id="01b21-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="01b21-1125">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="01b21-1126"><a name="bk_array_functions"></a> Функции массивов</span><span class="sxs-lookup"><span data-stu-id="01b21-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="01b21-1127">Hello следующие скалярные функции выполняют операцию над входным значением массива и возвращают числовое, логическое значение или значение массива</span><span class="sxs-lookup"><span data-stu-id="01b21-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="01b21-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="01b21-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="01b21-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="01b21-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="01b21-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="01b21-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="01b21-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="01b21-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="01b21-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="01b21-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="01b21-1133">Возвращает массив, который является результатом объединения двух или более значений массивов hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="01b21-1134">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="01b21-1135">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="01b21-1136">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="01b21-1137">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1138">Возвращает выражение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="01b21-1139">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1139">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1140">Hello в следующем примере как tooconcatenate двух массивов.</span><span class="sxs-lookup"><span data-stu-id="01b21-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="01b21-1141">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="01b21-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="01b21-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="01b21-1143">Возвращает логическое значение, указывающее, содержит ли массив hello hello заданного значения.</span><span class="sxs-lookup"><span data-stu-id="01b21-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="01b21-1144">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="01b21-1145">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="01b21-1146">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="01b21-1147">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="01b21-1148">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1149">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="01b21-1150">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1150">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1151">Следующий пример как Hello toocheck членства в массив с помощью ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="01b21-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="01b21-1152">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="01b21-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="01b21-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="01b21-1154">Возвращает число hello элементов hello указано выражение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="01b21-1155">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="01b21-1156">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="01b21-1157">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="01b21-1158">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1159">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-1160">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1160">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1161">Следующий пример Hello как tooget hello длину массива с помощью ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="01b21-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="01b21-1162">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="01b21-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="01b21-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="01b21-1164">Возвращает часть выражения массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="01b21-1165">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="01b21-1166">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="01b21-1167">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="01b21-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="01b21-1168">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="01b21-1169">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1170">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="01b21-1171">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1171">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1172">Следующий пример как Hello tooget часть массива с помощью ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="01b21-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="01b21-1173">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="01b21-1174"><a name="bk_spatial_functions"></a> Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="01b21-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="01b21-1175">Hello следующие скалярные функции выполняют операции над входным значением пространственного объекта и возвращают числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="01b21-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="01b21-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="01b21-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="01b21-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="01b21-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="01b21-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="01b21-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="01b21-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="01b21-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="01b21-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="01b21-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="01b21-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="01b21-1182">Возвращает hello расстояние между выражениями hello две точки GeoJSON Polygon и LineString.</span><span class="sxs-lookup"><span data-stu-id="01b21-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="01b21-1183">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="01b21-1184">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1185">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="01b21-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="01b21-1186">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1187">Возвращает числовое выражение, содержащее hello расстояние.</span><span class="sxs-lookup"><span data-stu-id="01b21-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="01b21-1188">Это выражается в метрах для эталонной системы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="01b21-1189">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1189">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1190">Следующий пример показывает как Hello tooreturn семейства все документы, которые находятся в пределах 30 км hello определенное место, с помощью встроенной функции ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="01b21-1191">.</span><span class="sxs-lookup"><span data-stu-id="01b21-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="01b21-1192">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="01b21-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="01b21-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="01b21-1194">Возвращает логическое выражение, указывающее, является ли объект GeoJSON на hello (точка Polygon и LineString), указанный в первый аргумент hello в hello GeoJSON (точка Polygon и LineString) в hello второго аргумента.</span><span class="sxs-lookup"><span data-stu-id="01b21-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="01b21-1195">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="01b21-1196">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1197">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="01b21-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1198">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="01b21-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="01b21-1199">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1200">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="01b21-1201">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1201">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1202">Hello в следующем примере показано, как toofind все семейство документы внутри многоугольника с помощью ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="01b21-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="01b21-1203">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="01b21-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="01b21-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="01b21-1205">Возвращает логическое выражение, указывающее, пересекается ли объект GeoJSON на hello (точка Polygon и LineString), указанный в первый аргумент hello hello GeoJSON (точка Polygon и LineString) в hello второго аргумента.</span><span class="sxs-lookup"><span data-stu-id="01b21-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="01b21-1206">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="01b21-1207">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1208">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="01b21-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1209">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="01b21-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="01b21-1210">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1211">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="01b21-1212">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1212">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1213">Следующий пример показывает как Hello toofind hello все области, которые пересекается с заданной многоугольника.</span><span class="sxs-lookup"><span data-stu-id="01b21-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="01b21-1214">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="01b21-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="01b21-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="01b21-1216">Возвращает логическое значение, указывающее, является ли hello точки GeoJSON Polygon и LineString выражение допустимо.</span><span class="sxs-lookup"><span data-stu-id="01b21-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="01b21-1217">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="01b21-1218">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1219">Любое допустимое выражение GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="01b21-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="01b21-1220">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1221">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="01b21-1222">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1222">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1223">Следующий пример показывает как Hello toocheck, если точка может быть использована с помощью ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="01b21-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="01b21-1224">Например, эта точка имеет значение широты, которая не находится в допустимый диапазон значений [-90, 90] hello, поэтому Здравствуйте, запрос возвращает значение false.</span><span class="sxs-lookup"><span data-stu-id="01b21-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="01b21-1225">Для многоугольников hello GeoJSON спецификация требует, должно быть hello последней парой координат предоставленный hello таким же как первого, toocreate hello замкнутую фигуру.</span><span class="sxs-lookup"><span data-stu-id="01b21-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="01b21-1226">Точки внутри многоугольника должны указываться в порядке против часовой стрелки.</span><span class="sxs-lookup"><span data-stu-id="01b21-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="01b21-1227">Многоугольник, указанным в заказе по часовой стрелке представляет обратное hello hello области внутри него.</span><span class="sxs-lookup"><span data-stu-id="01b21-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="01b21-1228">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="01b21-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="01b21-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="01b21-1230">Возвращает значение JSON, содержащий логическое значение, указываемое hello точки GeoJSON Polygon и LineString выражение является допустимым и если недействительной, кроме того hello причина как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="01b21-1231">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="01b21-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="01b21-1232">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="01b21-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="01b21-1233">Любое допустимое выражение точки или многоугольника GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="01b21-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="01b21-1234">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="01b21-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="01b21-1235">Возвращает значение JSON, содержащий логическое значение, если hello указания момента GeoJSON или Многоугольник выражение является допустимым и если недействительной, кроме того hello причина как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="01b21-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="01b21-1236">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="01b21-1236">**Examples**</span></span>  
  
 <span data-ttu-id="01b21-1237">Следующий пример как Hello toocheck срок действия (с сведения о) с помощью ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="01b21-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="01b21-1238">Ниже приведен результирующий набор hello.</span><span class="sxs-lookup"><span data-stu-id="01b21-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="01b21-1239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01b21-1239">Next steps</span></span>  
 <span data-ttu-id="01b21-1240">[SQL-запросы и синтаксис SQL в Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="01b21-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="01b21-1241">Документация по базе данных Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="01b21-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
