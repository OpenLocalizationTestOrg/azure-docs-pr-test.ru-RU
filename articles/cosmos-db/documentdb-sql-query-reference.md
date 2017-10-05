---
title: "API DocumentDB в Azure Cosmos DB. Синтаксис SQL | Документация Майкрософт"
description: "Справочная документация по языку SQL-запросов API DocumentDB в Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="6969c-103">Справочник по синтаксису SQL-запросов API DocumentDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6969c-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="6969c-104">API DocumentDB в Azure Cosmos DB позволяет выполнять запросы к документам с помощью знакомой грамматики SQL, например к иерархическим файлам JSON, без использования явных схем или создания вторичных индексов.</span><span class="sxs-lookup"><span data-stu-id="6969c-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="6969c-105">В этой статье содержится справочная документация по языку SQL-запросов API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6969c-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="6969c-106">Пошаговое руководство по языку SQL-запросов API DocumentDB см. в статье [SQL-запросы для API DocumentDB в Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="6969c-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="6969c-107">Мы также предлагаем вам посетить сайт [Query Playground](http://www.documentdb.com/sql/demo), где вы можете испытать базу данных Azure Cosmos DB в действии и выполнить запросы SQL к нашему набору данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="6969c-108">Запрос SELECT</span><span class="sxs-lookup"><span data-stu-id="6969c-108">SELECT query</span></span>  
<span data-ttu-id="6969c-109">Этот запрос извлекает документы JSON из базы данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="6969c-110">Он поддерживает вычисление выражений, проектирование, фильтрацию и соединение.</span><span class="sxs-lookup"><span data-stu-id="6969c-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="6969c-111">Соглашения, используемые для описания инструкций SELECT, приведены в разделе "Соглашения о синтаксисе".</span><span class="sxs-lookup"><span data-stu-id="6969c-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="6969c-112">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="6969c-113">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-113">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-114">Сведения о каждом из этих предложений см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="6969c-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="6969c-115">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="6969c-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="6969c-116">Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="6969c-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="6969c-117">Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="6969c-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="6969c-118">Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="6969c-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="6969c-119">Предложения в инструкции SELECT необходимо упорядочить, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="6969c-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="6969c-120">Необязательные предложения можно опустить,</span><span class="sxs-lookup"><span data-stu-id="6969c-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="6969c-121">но если вы используете их, их необходимо упорядочить в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="6969c-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="6969c-122">**Логические этапы обработки инструкции SELECT**</span><span class="sxs-lookup"><span data-stu-id="6969c-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="6969c-123">Порядок обработки предложений:</span><span class="sxs-lookup"><span data-stu-id="6969c-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="6969c-124">Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="6969c-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="6969c-125">Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="6969c-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="6969c-126">Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="6969c-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="6969c-127">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="6969c-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="6969c-128">Обратите внимание, что этот порядок отличается от порядка в синтаксисе.</span><span class="sxs-lookup"><span data-stu-id="6969c-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="6969c-129">Такое упорядочение связано с тем, что все новые символы, представленные в обработанном предложении, отображаются. Их можно использовать на следующих этапах.</span><span class="sxs-lookup"><span data-stu-id="6969c-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="6969c-130">Например, псевдонимы, объявленные в предложении FROM, доступны в предложениях WHERE и SELECT.</span><span class="sxs-lookup"><span data-stu-id="6969c-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="6969c-131">**Пробелы и комментарии**</span><span class="sxs-lookup"><span data-stu-id="6969c-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="6969c-132">Все пробели за пределами строки в кавычках или нестандартного идентификатора не входят в грамматику языка. Во время синтаксического анализа они игнорируются.</span><span class="sxs-lookup"><span data-stu-id="6969c-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="6969c-133">Язык запросов поддерживает комментарии T-SQL. Например:</span><span class="sxs-lookup"><span data-stu-id="6969c-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="6969c-134">Инструкция SQL `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="6969c-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="6969c-135">Пробелы и комментарии не имеют значения в грамматике. Их следует использовать для разделения лексем.</span><span class="sxs-lookup"><span data-stu-id="6969c-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="6969c-136">Например, `-1e5` представляет лексему с одним номером, а `: – 1 e5` — лексему "минус" (–), за которой следует номер 1 и идентификатор e5.</span><span class="sxs-lookup"><span data-stu-id="6969c-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="6969c-137"><a name="bk_select_query"></a>Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="6969c-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="6969c-138">Предложения в инструкции SELECT необходимо упорядочить, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="6969c-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="6969c-139">Необязательные предложения можно опустить,</span><span class="sxs-lookup"><span data-stu-id="6969c-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="6969c-140">но если вы используете их, их необходимо упорядочить в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="6969c-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="6969c-141">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="6969c-142">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="6969c-143">Свойства или значения, выбираемые для результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="6969c-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="6969c-144">Указывает, что значение необходимо извлечь без внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="6969c-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="6969c-145">В частности, если обработанное значение — это объект, извлекаются все свойства.</span><span class="sxs-lookup"><span data-stu-id="6969c-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="6969c-146">Указывает список свойств, которые требуется извлечь.</span><span class="sxs-lookup"><span data-stu-id="6969c-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="6969c-147">Каждое возвращаемое значение представляет собой объект с указанными свойствами.</span><span class="sxs-lookup"><span data-stu-id="6969c-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="6969c-148">Указывает, что следует извлечь только значение JSON, а не весь объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6969c-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="6969c-149">Этот аргумент, в отличие от аргумента `<property_list>`, не выделяет прогнозируемое значение в объекте.</span><span class="sxs-lookup"><span data-stu-id="6969c-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="6969c-150">Выражение, представляющее вычисляемое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="6969c-151">Дополнительные сведения см. в разделе [Скалярные выражения](#bk_scalar_expressions).</span><span class="sxs-lookup"><span data-stu-id="6969c-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="6969c-152">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-152">**Remarks**</span></span>  
  
<span data-ttu-id="6969c-153">Если предложение FROM объявило один псевдоним, действителен только синтаксис `SELECT *`.</span><span class="sxs-lookup"><span data-stu-id="6969c-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="6969c-154">Синтаксис `SELECT *` обеспечивает проекцию удостоверения, что может пригодиться, если проекция не требуется.</span><span class="sxs-lookup"><span data-stu-id="6969c-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="6969c-155">Кроме того, это единственный действительный синтаксис, если в предложении FROM указан один источник входных данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="6969c-156">Обратите внимание, что `SELECT <select_list>` и `SELECT *` — это "синтаксический сахар". При необходимости их можно выразить с помощью простых инструкций SELECT, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6969c-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="6969c-157">эквивалентно правилу</span><span class="sxs-lookup"><span data-stu-id="6969c-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="6969c-158">эквивалентно правилу</span><span class="sxs-lookup"><span data-stu-id="6969c-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="6969c-159">**См. также**</span><span class="sxs-lookup"><span data-stu-id="6969c-159">**See Also**</span></span>  
  
[<span data-ttu-id="6969c-160">Скалярные выражения</span><span class="sxs-lookup"><span data-stu-id="6969c-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="6969c-161">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="6969c-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="6969c-162"><a name="bk_from_clause"></a>Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="6969c-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="6969c-163">Это предложение указывает источник или несколько соединенных источников.</span><span class="sxs-lookup"><span data-stu-id="6969c-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="6969c-164">Предложение FROM можно не указывать.</span><span class="sxs-lookup"><span data-stu-id="6969c-164">The FROM clause is optional.</span></span> <span data-ttu-id="6969c-165">Даже без него другие приложения по-прежнему выполнятся.</span><span class="sxs-lookup"><span data-stu-id="6969c-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="6969c-166">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-166">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="6969c-167">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="6969c-168">Указывает источник данных с псевдонимом или без него.</span><span class="sxs-lookup"><span data-stu-id="6969c-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="6969c-169">Если псевдоним не указан, он выводится из аргумента `<collection_expression>` на основе следующих правил:</span><span class="sxs-lookup"><span data-stu-id="6969c-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="6969c-170">При использовании выражения collection_name оно указывается в качестве псевдонима.</span><span class="sxs-lookup"><span data-stu-id="6969c-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="6969c-171">При использовании выражения `<collection_expression>` в качестве псевдонима указывается свойство property_name.</span><span class="sxs-lookup"><span data-stu-id="6969c-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="6969c-172">При использовании выражения collection_name оно указывается в качестве псевдонима.</span><span class="sxs-lookup"><span data-stu-id="6969c-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="6969c-173">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="6969c-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="6969c-174">Указывает, что аргумент `input_alias` — это набор значений, возвращенный базовым выражением коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="6969c-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="6969c-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="6969c-176">Указывает, что аргумент `input_alias` должен представлять набор значений, полученных путем итерации всех элементов в каждом массиве, возвращенном базовым выражением коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="6969c-177">Значения, возвращенные базовым выражением коллекции, которые не являются массивом, игнорируются.</span><span class="sxs-lookup"><span data-stu-id="6969c-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="6969c-178">Указывает выражение коллекции, используемое для получения документов.</span><span class="sxs-lookup"><span data-stu-id="6969c-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="6969c-179">Указывает, что документ необходимо извлечь из подключенной в настоящий момент коллекции по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6969c-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="6969c-180">Указывает, что документ необходимо извлечь из предоставленной коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="6969c-181">Имя этой коллекции должно совпадать с именем подключенной в настоящий момент коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="6969c-182">Указывает, что документ необходимо извлечь из источника, определенного предоставленным псевдонимом.</span><span class="sxs-lookup"><span data-stu-id="6969c-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="6969c-183">Указывает, что документ необходимо извлечь из свойства `property_name` или элемента массива array_index всех документов, полученных указанным выражением коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="6969c-184">Указывает, что документ необходимо извлечь из свойства `property_name` или элемента массива array_index всех документов, полученных указанным выражением коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="6969c-185">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-185">**Remarks**</span></span>  
  
<span data-ttu-id="6969c-186">Все псевдонимы, предоставленные или выведенные в аргументе `<from_source>(`, должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="6969c-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="6969c-187">Синтаксис `<collection_expression>.`property_name совпадает с синтаксисом `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="6969c-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="6969c-188">Второй синтаксис можно использовать, если имя свойства содержит знаки, не являющиеся идентификатором.</span><span class="sxs-lookup"><span data-stu-id="6969c-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="6969c-189">**Обработка отсутствующих свойств, элементов массива и неопределенных значений**</span><span class="sxs-lookup"><span data-stu-id="6969c-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="6969c-190">Если выражение коллекции обращается к свойствам или элементам массива и необходимое значение отсутствует, это значение игнорируется и не проходит дальнейшую обработку.</span><span class="sxs-lookup"><span data-stu-id="6969c-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="6969c-191">**Определение области контекста выражения коллекции**</span><span class="sxs-lookup"><span data-stu-id="6969c-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="6969c-192">Выражение коллекции может указываться на уровне коллекции или документа:</span><span class="sxs-lookup"><span data-stu-id="6969c-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="6969c-193">Если в качестве базового источника выражения коллекции используется ROOT или `collection_name`, выражение определено на уровне коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="6969c-194">Такое выражение представляет набор документов, полученный напрямую из коллекции. Оно не зависит от обработки других выражений коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="6969c-195">Если в качестве базового источника выражения коллекции используется аргумент `input_alias`, сформированный ранее в запросе, выражение определено на уровне документа.</span><span class="sxs-lookup"><span data-stu-id="6969c-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="6969c-196">Такое выражение представляет набор документов, полученный при оценке выражения коллекции в области каждого документа, который входит в набор, связанный с коллекцией, содержащей псевдоним.</span><span class="sxs-lookup"><span data-stu-id="6969c-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="6969c-197">Результирующий набор в этом случае представляет собой ряд наборов, полученных в результате вычисления выражения коллекции для всех документов в базовом наборе.</span><span class="sxs-lookup"><span data-stu-id="6969c-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="6969c-198">**Соединения**</span><span class="sxs-lookup"><span data-stu-id="6969c-198">**Joins**</span></span>  
  
<span data-ttu-id="6969c-199">В текущем выпуске Azure Cosmos DB поддерживает внутренние соединения.</span><span class="sxs-lookup"><span data-stu-id="6969c-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="6969c-200">Дополнительные возможности соединения будут добавлены позже.</span><span class="sxs-lookup"><span data-stu-id="6969c-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="6969c-201">Результат внутренних соединений —это полное векторное произведение множеств, участвующих в соединении.</span><span class="sxs-lookup"><span data-stu-id="6969c-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="6969c-202">Результатом других типов соединений является набор кортежей элементов того же типа, где каждое значение в кортеже связано с набором с псевдонимом, участвующим в соединении. Доступ к этому набору можно получить, создав ссылку на этот псевдоним в остальных предложениях.</span><span class="sxs-lookup"><span data-stu-id="6969c-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="6969c-203">Вычисление соединения зависит от области контекста участвующих наборов:</span><span class="sxs-lookup"><span data-stu-id="6969c-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="6969c-204">Результатом соединения набора элементов набора A и набора Б уровня коллекции является векторное произведение всех элементов в наборе А и Б.</span><span class="sxs-lookup"><span data-stu-id="6969c-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="6969c-205">Соединение набора A и набора Б уровня документа приводит к объединению всех наборов, полученных при оценке набора Б уровня документа для каждого документа из набора А.</span><span class="sxs-lookup"><span data-stu-id="6969c-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="6969c-206">В текущем выпуске обработчик запросов поддерживает максимум одно выражение уровня коллекции.</span><span class="sxs-lookup"><span data-stu-id="6969c-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="6969c-207">**Примеры соединений**</span><span class="sxs-lookup"><span data-stu-id="6969c-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="6969c-208">Рассмотрим следующее выражение FROM: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`.</span><span class="sxs-lookup"><span data-stu-id="6969c-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="6969c-209">Разрешите каждому источнику определить `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="6969c-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="6969c-210">Это предложение FROM возвращает набор N-кортежей (кортежей, у которых число значений равно N).</span><span class="sxs-lookup"><span data-stu-id="6969c-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="6969c-211">Каждый кортеж будет иметь значения, полученные путем итерации всех псевдонимов коллекции среди их наборов.</span><span class="sxs-lookup"><span data-stu-id="6969c-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="6969c-212">*Пример соединения 1 с 2 источниками:*</span><span class="sxs-lookup"><span data-stu-id="6969c-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="6969c-213">Определите аргумент `<from_source1>` на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="6969c-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="6969c-214">Определите аргумент `<from_source2>` на уровне документа и добавьте ссылку на input_alias1. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="6969c-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="6969c-215">{1, 2} для `input_alias1 = A,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="6969c-216">{3} для `input_alias1 = B,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="6969c-217">{4, 5} для `input_alias1 = C,`.</span><span class="sxs-lookup"><span data-stu-id="6969c-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="6969c-218">В результате выполнения предложения FROM `<from_source1> JOIN <from_source2>` вернутся следующие кортежи:</span><span class="sxs-lookup"><span data-stu-id="6969c-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="6969c-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="6969c-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="6969c-220">*Пример соединения 2 с 3 источниками:*</span><span class="sxs-lookup"><span data-stu-id="6969c-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="6969c-221">Определите аргумент `<from_source1>` на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="6969c-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="6969c-222">Определите аргумент `<from_source2>` на уровне документа и добавьте ссылку на `input_alias1`. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="6969c-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="6969c-223">{1, 2} для `input_alias1 = A,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="6969c-224">{3} для `input_alias1 = B,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="6969c-225">{4, 5} для `input_alias1 = C,`.</span><span class="sxs-lookup"><span data-stu-id="6969c-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="6969c-226">Определите аргумент `<from_source3>` на уровне документа и добавьте ссылку на `input_alias2`. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="6969c-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="6969c-227">{100, 200} для `input_alias2 = 1,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="6969c-228">{300} для `input_alias2 = 3,`.</span><span class="sxs-lookup"><span data-stu-id="6969c-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="6969c-229">В результате выполнения предложения FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` вернутся следующие кортежи:</span><span class="sxs-lookup"><span data-stu-id="6969c-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="6969c-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="6969c-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="6969c-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="6969c-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6969c-232">Другие значения `input_alias1`, например `input_alias2`, для которых `<from_source3>` не вернул значения, не имеют кортежей.</span><span class="sxs-lookup"><span data-stu-id="6969c-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="6969c-233">*Пример соединения 3 с 3 источниками:*</span><span class="sxs-lookup"><span data-stu-id="6969c-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="6969c-234">Определите аргумент <from_source1> на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="6969c-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="6969c-235">Определите аргумент `<from_source1>` на уровне коллекции. Он должен представлять набор {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="6969c-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="6969c-236">Определите аргумент <from_source2> на уровне документа и добавьте ссылку на input_alias1. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="6969c-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="6969c-237">{1, 2} для `input_alias1 = A,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="6969c-238">{3} для `input_alias1 = B,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="6969c-239">{4, 5} для `input_alias1 = C,`.</span><span class="sxs-lookup"><span data-stu-id="6969c-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="6969c-240">Определите аргумент `<from_source3>` в области `input_alias1`. Он должен представлять следующие наборы:</span><span class="sxs-lookup"><span data-stu-id="6969c-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="6969c-241">{100, 200} для `input_alias2 = A,`;</span><span class="sxs-lookup"><span data-stu-id="6969c-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="6969c-242">{300} для `input_alias2 = C,`.</span><span class="sxs-lookup"><span data-stu-id="6969c-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="6969c-243">В результате выполнения предложения FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` вернутся следующие кортежи:</span><span class="sxs-lookup"><span data-stu-id="6969c-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="6969c-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="6969c-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="6969c-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="6969c-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6969c-246">В результате этого соединения образовалось векторное произведение между `<from_source2>` и `<from_source3>`. Это связано с тем, что оба этих аргумента относятся к аргументу `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="6969c-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="6969c-247">Это привело к созданию 4 (2 x 2) кортежей со значением A, 0 кортежей (1 x 0) со значением B и 2 (2x1) кортежей со значением C.</span><span class="sxs-lookup"><span data-stu-id="6969c-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="6969c-248">**См. также**</span><span class="sxs-lookup"><span data-stu-id="6969c-248">**See also**</span></span>  
  
 [<span data-ttu-id="6969c-249">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="6969c-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="6969c-250"><a name="bk_where_clause"></a>Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="6969c-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="6969c-251">Это предложение указывает условие поиска для документов, возвращенных запросом.</span><span class="sxs-lookup"><span data-stu-id="6969c-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="6969c-252">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="6969c-253">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="6969c-254">Указывает рекомендованное условие для возвращаемых документов.</span><span class="sxs-lookup"><span data-stu-id="6969c-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="6969c-255">Выражение, представляющее вычисляемое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="6969c-256">Дополнительные сведения см. в разделе [Скалярные выражения](#bk_scalar_expressions).</span><span class="sxs-lookup"><span data-stu-id="6969c-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="6969c-257">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-257">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-258">Чтобы вернуть документ, выражение, указанное в качестве условия фильтра, должно иметь значение true.</span><span class="sxs-lookup"><span data-stu-id="6969c-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="6969c-259">Только логическое значение true соответствует условию. Все остальные значения, например undefined, Null, false, число, массив, объект, не подходят.</span><span class="sxs-lookup"><span data-stu-id="6969c-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="6969c-260"><a name="bk_orderby_clause"></a>Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="6969c-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="6969c-261">Это предложение указывает порядок сортировки результатов, возвращаемых запросом.</span><span class="sxs-lookup"><span data-stu-id="6969c-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="6969c-262">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="6969c-263">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="6969c-264">Указывает свойство или выражение, по которому производится сортировка результирующего набора запроса.</span><span class="sxs-lookup"><span data-stu-id="6969c-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="6969c-265">Столбец сортировки можно указать в качестве имени или псевдонима.</span><span class="sxs-lookup"><span data-stu-id="6969c-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="6969c-266">Вы можете указать несколько столбцов сортировки.</span><span class="sxs-lookup"><span data-stu-id="6969c-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="6969c-267">Имена столбцов должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="6969c-267">Column names must be unique.</span></span> <span data-ttu-id="6969c-268">Последовательность столбцов сортировки в предложении ORDER BY определяет организацию упорядоченного результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="6969c-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="6969c-269">То есть результирующий набор сортируется по первому свойству, а затем упорядоченный список сортируется по второму свойству и т. д.</span><span class="sxs-lookup"><span data-stu-id="6969c-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="6969c-270">Имена столбцов, на которые указываются ссылки в предложении ORDER BY, должны соответствовать столбцу в списке выбора или столбцу в таблице, указанной в предложении FROM.</span><span class="sxs-lookup"><span data-stu-id="6969c-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="6969c-271">Указывает одно свойство или выражение, по которому производится сортировка результирующего набора запроса.</span><span class="sxs-lookup"><span data-stu-id="6969c-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="6969c-272">Дополнительные сведения см. в разделе [Скалярные выражения](#bk_scalar_expressions).</span><span class="sxs-lookup"><span data-stu-id="6969c-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="6969c-273">Указывает порядок сортировки значений в указанном столбце (по возрастанию или по убыванию).</span><span class="sxs-lookup"><span data-stu-id="6969c-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="6969c-274">Если указать ASC, значения сортируются по возрастанию,</span><span class="sxs-lookup"><span data-stu-id="6969c-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="6969c-275">а если DESC — по убыванию.</span><span class="sxs-lookup"><span data-stu-id="6969c-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="6969c-276">По умолчанию значения сортируются по возрастанию.</span><span class="sxs-lookup"><span data-stu-id="6969c-276">ASC is the default sort order.</span></span> <span data-ttu-id="6969c-277">Значения Null рассматриваются как минимальные возможные значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="6969c-278">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-278">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-279">Хотя грамматика запроса поддерживает несколько параметров сортировки по свойствам, среда выполнения запросов Azure Cosmos DB поддерживает только сортировку по одному свойству и по именам свойств (т. е. не по вычисляемым свойствам).</span><span class="sxs-lookup"><span data-stu-id="6969c-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="6969c-280">Кроме того, требуется, чтобы политика индексации содержала максимально точный индекс диапазона свойства и указанного типа.</span><span class="sxs-lookup"><span data-stu-id="6969c-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="6969c-281">Дополнительные сведения см. в документации по политике индексации.</span><span class="sxs-lookup"><span data-stu-id="6969c-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="6969c-282"><a name="bk_scalar_expressions"></a>Скалярные выражения</span><span class="sxs-lookup"><span data-stu-id="6969c-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="6969c-283">Скалярное выражение — это сочетание символов и операторов, в результате вычисления которых возвращается одно значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="6969c-284">К простым выражениям можно отнести константы, ссылки на свойства, ссылки на элементы массива, ссылки на псевдонимы или вызовы функций.</span><span class="sxs-lookup"><span data-stu-id="6969c-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="6969c-285">C помощью операторов простые выражения можно объединить в сложные.</span><span class="sxs-lookup"><span data-stu-id="6969c-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="6969c-286">Дополнительные сведения о значениях скалярных выражений см. в разделе [Константы](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="6969c-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="6969c-287">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-287">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="6969c-288">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="6969c-289">Представляет значение константы.</span><span class="sxs-lookup"><span data-stu-id="6969c-289">Represents a constant value.</span></span> <span data-ttu-id="6969c-290">Дополнительные сведения см. в разделе [Константы](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="6969c-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="6969c-291">Представляет значение, определяемое аргументом `input_alias` в предложении `FROM`.</span><span class="sxs-lookup"><span data-stu-id="6969c-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="6969c-292">Выражение гарантировано не может принять значение **undefined**. Значения **undefined** пропускаются.</span><span class="sxs-lookup"><span data-stu-id="6969c-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="6969c-293">Представляет значение свойства объекта.</span><span class="sxs-lookup"><span data-stu-id="6969c-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="6969c-294">Если свойство не существует или ссылается на значение, которое не является объектом, выражение принимает значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="6969c-295">Представляет значение свойства с именем `property_name` или элемент массива с индексом `array_index` из объекта или массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="6969c-296">Если объект или массив не существует или ссылается на значение, которое не является объектом или массивом, выражение принимает значение undefined.</span><span class="sxs-lookup"><span data-stu-id="6969c-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="6969c-297">Представляет оператор, применяемый к одному значению.</span><span class="sxs-lookup"><span data-stu-id="6969c-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="6969c-298">Дополнительные сведения см. в разделе [Операторы](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="6969c-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="6969c-299">Представляет оператор, применяемый к двум значениям.</span><span class="sxs-lookup"><span data-stu-id="6969c-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="6969c-300">Дополнительные сведения см. в разделе [Операторы](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="6969c-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="6969c-301">Представляет значение, определяемое результатом вызова функции.</span><span class="sxs-lookup"><span data-stu-id="6969c-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="6969c-302">Имя определяемой пользователем скалярной функции.</span><span class="sxs-lookup"><span data-stu-id="6969c-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="6969c-303">Имя встроенной скалярной функции.</span><span class="sxs-lookup"><span data-stu-id="6969c-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="6969c-304">Представляет значение, полученное в процессе создания объекта с заданными свойствами и их значениями.</span><span class="sxs-lookup"><span data-stu-id="6969c-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="6969c-305">Представляет значение, полученное в процессе создания массива с заданными значениями в качестве элементов.</span><span class="sxs-lookup"><span data-stu-id="6969c-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="6969c-306">Представляет значение указанного имени параметра.</span><span class="sxs-lookup"><span data-stu-id="6969c-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="6969c-307">Имена параметров должны начинаться со знака "@".</span><span class="sxs-lookup"><span data-stu-id="6969c-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="6969c-308">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-308">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-309">При вызове встроенной или определяемой пользователем скалярной функции необходимо определить все аргументы.</span><span class="sxs-lookup"><span data-stu-id="6969c-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="6969c-310">Если любой из аргументов не определен, функция не будет вызвана, и значение не будет определено.</span><span class="sxs-lookup"><span data-stu-id="6969c-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="6969c-311">При создании объекта все свойства со значением undefined пропускаются и не включаются в созданный объект.</span><span class="sxs-lookup"><span data-stu-id="6969c-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="6969c-312">При создании массива все элементы со значением **undefined** пропускаются и не включаются в созданный объект.</span><span class="sxs-lookup"><span data-stu-id="6969c-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="6969c-313">В этом случае место неопределенного элемента занимает следующий определенный элемент, таким образом в созданном массиве не будет пропущенных индексов.</span><span class="sxs-lookup"><span data-stu-id="6969c-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="6969c-314"><a name="bk_operators"></a>Операторы</span><span class="sxs-lookup"><span data-stu-id="6969c-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="6969c-315">В этом разделе описываются поддерживаемые операторы.</span><span class="sxs-lookup"><span data-stu-id="6969c-315">This section describes the supported operators.</span></span> <span data-ttu-id="6969c-316">Каждый оператор может назначаться только одной категории.</span><span class="sxs-lookup"><span data-stu-id="6969c-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="6969c-317">В таблице **Категории операторов** ниже приведены сведения об обработке значений **undefined**, требованиях к типу входных значений и обработке значений несоответствующего типа.</span><span class="sxs-lookup"><span data-stu-id="6969c-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="6969c-318">**Категории операторов**</span><span class="sxs-lookup"><span data-stu-id="6969c-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="6969c-319">**Категория**</span><span class="sxs-lookup"><span data-stu-id="6969c-319">**Category**</span></span>|<span data-ttu-id="6969c-320">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="6969c-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="6969c-321">**Арифметические**</span><span class="sxs-lookup"><span data-stu-id="6969c-321">**arithmetic**</span></span>|<span data-ttu-id="6969c-322">Ожидаемые входные и</span><span class="sxs-lookup"><span data-stu-id="6969c-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="6969c-323">выходные данные — числа.</span><span class="sxs-lookup"><span data-stu-id="6969c-323">Output is also a Number.</span></span> <span data-ttu-id="6969c-324">Если любое входное значение **не определено** или имеет другой тип (не число), выражение принимает значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="6969c-325">**Битовые**</span><span class="sxs-lookup"><span data-stu-id="6969c-325">**bitwise**</span></span>|<span data-ttu-id="6969c-326">Ожидаемые входные и</span><span class="sxs-lookup"><span data-stu-id="6969c-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="6969c-327">выходные данные — 32-разрядные целые числа со знаками.</span><span class="sxs-lookup"><span data-stu-id="6969c-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="6969c-328">Все нецелочисленные значения округляются.</span><span class="sxs-lookup"><span data-stu-id="6969c-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="6969c-329">Положительные значения округляются в меньшую сторону, а отрицательные — в большую.</span><span class="sxs-lookup"><span data-stu-id="6969c-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="6969c-330">Все не 32-разрядные целые числа со знаками преобразовываются (берутся последние 32 бита их нотации дополнительного кода).</span><span class="sxs-lookup"><span data-stu-id="6969c-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="6969c-331">Если любое входное значение **не определено** или имеет другой тип (не число), выражение принимает значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="6969c-332">**Примечание.** Описанное выше поведение совместимо с поведением побитового оператора JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6969c-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="6969c-333">**Логические**</span><span class="sxs-lookup"><span data-stu-id="6969c-333">**logical**</span></span>|<span data-ttu-id="6969c-334">Ожидаемые входные и</span><span class="sxs-lookup"><span data-stu-id="6969c-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="6969c-335">выходные данные — логические значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="6969c-336">Если любое входное значение **не определено** или имеет другой тип (не логический), выражение принимает значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="6969c-337">**Сравнение**</span><span class="sxs-lookup"><span data-stu-id="6969c-337">**comparison**</span></span>|<span data-ttu-id="6969c-338">Ожидаемые входные данные — определенные значения одного типа.</span><span class="sxs-lookup"><span data-stu-id="6969c-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="6969c-339">Выходные данные — логические значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="6969c-340">Если любое входное значение **не определено** или тип входных данных не совпадает, выражение принимает значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="6969c-341">Сведения об упорядочении значений см. в таблице **Упорядочение сравниваемых значений**.</span><span class="sxs-lookup"><span data-stu-id="6969c-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="6969c-342">**string**</span><span class="sxs-lookup"><span data-stu-id="6969c-342">**string**</span></span>|<span data-ttu-id="6969c-343">Ожидаемые входные и</span><span class="sxs-lookup"><span data-stu-id="6969c-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="6969c-344">выходные данные — строки.</span><span class="sxs-lookup"><span data-stu-id="6969c-344">Output is also a String.</span></span><br /><span data-ttu-id="6969c-345">Если любое входное значение **не определено** или имеет другой тип (не строка), выражение принимает значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="6969c-346">**Унарные операторы**</span><span class="sxs-lookup"><span data-stu-id="6969c-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="6969c-347">**Имя**</span><span class="sxs-lookup"><span data-stu-id="6969c-347">**Name**</span></span>|<span data-ttu-id="6969c-348">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="6969c-348">**Operator**</span></span>|<span data-ttu-id="6969c-349">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="6969c-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="6969c-350">**Арифметические**</span><span class="sxs-lookup"><span data-stu-id="6969c-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="6969c-351">Возвращает числовое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="6969c-352">Выполняет побитовую операцию.</span><span class="sxs-lookup"><span data-stu-id="6969c-352">Bitwise negation.</span></span> <span data-ttu-id="6969c-353">Возвращает отрицательное числовое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="6969c-354">**Битовые**</span><span class="sxs-lookup"><span data-stu-id="6969c-354">**bitwise**</span></span>|~|<span data-ttu-id="6969c-355">Дополнение.</span><span class="sxs-lookup"><span data-stu-id="6969c-355">Ones' complement.</span></span> <span data-ttu-id="6969c-356">Возвращает дополнение числового значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="6969c-357">**Логические**</span><span class="sxs-lookup"><span data-stu-id="6969c-357">**Logical**</span></span>|<span data-ttu-id="6969c-358">**NOT**</span><span class="sxs-lookup"><span data-stu-id="6969c-358">**NOT**</span></span>|<span data-ttu-id="6969c-359">Отрицание.</span><span class="sxs-lookup"><span data-stu-id="6969c-359">Negation.</span></span> <span data-ttu-id="6969c-360">Возвращает отрицательное логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="6969c-361">**Бинарные операторы**</span><span class="sxs-lookup"><span data-stu-id="6969c-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="6969c-362">**Имя**</span><span class="sxs-lookup"><span data-stu-id="6969c-362">**Name**</span></span>|<span data-ttu-id="6969c-363">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="6969c-363">**Operator**</span></span>|<span data-ttu-id="6969c-364">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="6969c-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="6969c-365">**Арифметические**</span><span class="sxs-lookup"><span data-stu-id="6969c-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="6969c-366">Сложение.</span><span class="sxs-lookup"><span data-stu-id="6969c-366">Addition.</span></span><br /><br /> <span data-ttu-id="6969c-367">Вычитание.</span><span class="sxs-lookup"><span data-stu-id="6969c-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="6969c-368">Умножение.</span><span class="sxs-lookup"><span data-stu-id="6969c-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="6969c-369">Деление.</span><span class="sxs-lookup"><span data-stu-id="6969c-369">Division.</span></span><br /><br /> <span data-ttu-id="6969c-370">Модуляция.</span><span class="sxs-lookup"><span data-stu-id="6969c-370">Modulation.</span></span>|  
|<span data-ttu-id="6969c-371">**Битовые**</span><span class="sxs-lookup"><span data-stu-id="6969c-371">**bitwise**</span></span>|<span data-ttu-id="6969c-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="6969c-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="6969c-373">Битовый OR.</span><span class="sxs-lookup"><span data-stu-id="6969c-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="6969c-374">Битовый AND.</span><span class="sxs-lookup"><span data-stu-id="6969c-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="6969c-375">Битовый XOR.</span><span class="sxs-lookup"><span data-stu-id="6969c-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="6969c-376">Сдвиг влево.</span><span class="sxs-lookup"><span data-stu-id="6969c-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="6969c-377">Сдвиг вправо.</span><span class="sxs-lookup"><span data-stu-id="6969c-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="6969c-378">Сдвиг вправо с заполнением нулями.</span><span class="sxs-lookup"><span data-stu-id="6969c-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="6969c-379">**Логические**</span><span class="sxs-lookup"><span data-stu-id="6969c-379">**logical**</span></span>|<span data-ttu-id="6969c-380">**AND**</span><span class="sxs-lookup"><span data-stu-id="6969c-380">**AND**</span></span><br /><br /> <span data-ttu-id="6969c-381">**OR**</span><span class="sxs-lookup"><span data-stu-id="6969c-381">**OR**</span></span>|<span data-ttu-id="6969c-382">Логическое умножение.</span><span class="sxs-lookup"><span data-stu-id="6969c-382">Logical conjunction.</span></span> <span data-ttu-id="6969c-383">Возвращает значение **true**, если оба аргумента имеют значение **true**. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-384">Логическое умножение.</span><span class="sxs-lookup"><span data-stu-id="6969c-384">Logical conjunction.</span></span> <span data-ttu-id="6969c-385">Возвращает значение **true**, если оба аргумента имеют значение **true**. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="6969c-386">**Сравнение**</span><span class="sxs-lookup"><span data-stu-id="6969c-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="6969c-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="6969c-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="6969c-388">**??**</span><span class="sxs-lookup"><span data-stu-id="6969c-388">**??**</span></span>|<span data-ttu-id="6969c-389">Равно.</span><span class="sxs-lookup"><span data-stu-id="6969c-389">Equals.</span></span> <span data-ttu-id="6969c-390">Возвращает значение **true**, если оба аргумента равны. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-391">Не равно.</span><span class="sxs-lookup"><span data-stu-id="6969c-391">Not equal to.</span></span> <span data-ttu-id="6969c-392">Возвращает значение **true**, если оба аргумента не равны. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-393">Больше.</span><span class="sxs-lookup"><span data-stu-id="6969c-393">Greater Than.</span></span> <span data-ttu-id="6969c-394">Возвращает значение **true**, если первый аргумент больше второго. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-395">Больше или равно.</span><span class="sxs-lookup"><span data-stu-id="6969c-395">Greater Than or Equal To.</span></span> <span data-ttu-id="6969c-396">Возвращает значение **true**, если первый аргумент больше второго или равен ему. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-397">Меньше.</span><span class="sxs-lookup"><span data-stu-id="6969c-397">Less Than.</span></span> <span data-ttu-id="6969c-398">Возвращает значение **true**, если первый аргумент меньше второго. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-399">Меньше или равно.</span><span class="sxs-lookup"><span data-stu-id="6969c-399">Less Than or Equal To.</span></span> <span data-ttu-id="6969c-400">Возвращает значение **true**, если первый аргумент меньше второго или равен ему. В противном случае возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6969c-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="6969c-401">Слияние.</span><span class="sxs-lookup"><span data-stu-id="6969c-401">Coalesce.</span></span> <span data-ttu-id="6969c-402">Возвращает второй аргумент, если первый аргумент имеет значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="6969c-403">**Строка**</span><span class="sxs-lookup"><span data-stu-id="6969c-403">**String**</span></span>|<span data-ttu-id="6969c-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="6969c-404">**&#124;&#124;**</span></span>|<span data-ttu-id="6969c-405">Объединение.</span><span class="sxs-lookup"><span data-stu-id="6969c-405">Concatenation.</span></span> <span data-ttu-id="6969c-406">Возвращает объединение обоих аргументов.</span><span class="sxs-lookup"><span data-stu-id="6969c-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="6969c-407">**Тернарные операторы**</span><span class="sxs-lookup"><span data-stu-id="6969c-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="6969c-408">Тернарный оператор</span><span class="sxs-lookup"><span data-stu-id="6969c-408">Ternary operator</span></span>|<span data-ttu-id="6969c-409">?</span><span class="sxs-lookup"><span data-stu-id="6969c-409">?</span></span>|<span data-ttu-id="6969c-410">Возвращает второй аргумент, если первый аргумент принимает значение **true**. В противном случае возвращает третий аргумент.</span><span class="sxs-lookup"><span data-stu-id="6969c-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="6969c-411">**Упорядочение сравниваемых значений**</span><span class="sxs-lookup"><span data-stu-id="6969c-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="6969c-412">**Тип**</span><span class="sxs-lookup"><span data-stu-id="6969c-412">**Type**</span></span>|<span data-ttu-id="6969c-413">**Порядок значений**</span><span class="sxs-lookup"><span data-stu-id="6969c-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="6969c-414">**Неопределенное**</span><span class="sxs-lookup"><span data-stu-id="6969c-414">**Undefined**</span></span>|<span data-ttu-id="6969c-415">Невозможно сравнить.</span><span class="sxs-lookup"><span data-stu-id="6969c-415">Not comparable.</span></span>|  
|<span data-ttu-id="6969c-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="6969c-416">**Null**</span></span>|<span data-ttu-id="6969c-417">Доступное значение: **Null**</span><span class="sxs-lookup"><span data-stu-id="6969c-417">Single value: **null**</span></span>|  
|<span data-ttu-id="6969c-418">**Число**</span><span class="sxs-lookup"><span data-stu-id="6969c-418">**Number**</span></span>|<span data-ttu-id="6969c-419">Натуральное вещественное число.</span><span class="sxs-lookup"><span data-stu-id="6969c-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="6969c-420">Отрицательное значение бесконечности меньше любого другого числового значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="6969c-421">Положительное значение бесконечности больше любого другого числового значения. Значение **NaN** невозможно сравнить.</span><span class="sxs-lookup"><span data-stu-id="6969c-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="6969c-422">При сравнение с **NaN** возвращается значение **undefined**.</span><span class="sxs-lookup"><span data-stu-id="6969c-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="6969c-423">**Строка**</span><span class="sxs-lookup"><span data-stu-id="6969c-423">**String**</span></span>|<span data-ttu-id="6969c-424">Лексикографический порядок.</span><span class="sxs-lookup"><span data-stu-id="6969c-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="6969c-425">**Массив**</span><span class="sxs-lookup"><span data-stu-id="6969c-425">**Array**</span></span>|<span data-ttu-id="6969c-426">Не поддерживает упорядочивание, но равнозначные.</span><span class="sxs-lookup"><span data-stu-id="6969c-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="6969c-427">**Объект**</span><span class="sxs-lookup"><span data-stu-id="6969c-427">**Object**</span></span>|<span data-ttu-id="6969c-428">Не поддерживает упорядочивание, но равнозначные.</span><span class="sxs-lookup"><span data-stu-id="6969c-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="6969c-429">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-429">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-430">В базе данных Azure Cosmos DB типы значений часто невозможно определить до их фактического извлечения.</span><span class="sxs-lookup"><span data-stu-id="6969c-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="6969c-431">Чтобы обеспечить эффективное выполнение запросов, большинство операторов имеют строгие требования к типам.</span><span class="sxs-lookup"><span data-stu-id="6969c-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="6969c-432">Кроме того, операторы сами по себе не выполняют неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="6969c-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="6969c-433">Это означает, что запрос, такой как SELECT * FROM ROOT r WHERE r.Age = 21, вернет только документы со свойством Age равным числу 21.</span><span class="sxs-lookup"><span data-stu-id="6969c-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="6969c-434">Документы со свойством Age равным строке "21" или "0021" не соответствуют, так как выражение "21" = 21 принимает значение undefined.</span><span class="sxs-lookup"><span data-stu-id="6969c-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="6969c-435">Это позволяет лучше использовать индексы, так как поиск конкретного значения (например, числа 21) выполняется быстрее, чем поиск неопределенного количества возможных совпадений (например, числа 21 или строк "21", "021", "21.0" и т. д.).</span><span class="sxs-lookup"><span data-stu-id="6969c-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="6969c-436">Это отличается от способа вычисления операторов в значениях различных типов на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6969c-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="6969c-437">**Равенство и сравнение массивов и объектов**</span><span class="sxs-lookup"><span data-stu-id="6969c-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="6969c-438">При сравнении значений массивов или объектов с использованием операторов диапазона (>, >=, <, <=) возвращается значение undefined, так как порядок этих значений не определен.</span><span class="sxs-lookup"><span data-stu-id="6969c-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="6969c-439">Но выполнить структурное сравнение можно с помощью операторов равенства и неравенства (=, !=, <>).</span><span class="sxs-lookup"><span data-stu-id="6969c-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="6969c-440">Два массива считаются равными, если они имеют одинаковое число элементов и сопоставляемые элементы также равны.</span><span class="sxs-lookup"><span data-stu-id="6969c-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="6969c-441">Если при сравнении пары элементов возвращается значение undefined, сравнение массива также вернет значение undefined.</span><span class="sxs-lookup"><span data-stu-id="6969c-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="6969c-442">Два объекта считаются равными, если они имеют одинаковые свойства и сопоставляемые свойства также равны.</span><span class="sxs-lookup"><span data-stu-id="6969c-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="6969c-443">Если при сравнении пары значений свойств возвращается значение undefined, сравнение объекта также вернет значение undefined.</span><span class="sxs-lookup"><span data-stu-id="6969c-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="6969c-444"><a name="bk_constants"></a>Константы</span><span class="sxs-lookup"><span data-stu-id="6969c-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="6969c-445">Константа (также известная как литерал или скаляр) — это символ, представляющий определенное значение данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="6969c-446">Формат константы зависит от типа данных значения, которое она представляет.</span><span class="sxs-lookup"><span data-stu-id="6969c-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="6969c-447">**Поддерживаемые скалярные типы данных**</span><span class="sxs-lookup"><span data-stu-id="6969c-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="6969c-448">**Тип**</span><span class="sxs-lookup"><span data-stu-id="6969c-448">**Type**</span></span>|<span data-ttu-id="6969c-449">**Порядок значений**</span><span class="sxs-lookup"><span data-stu-id="6969c-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="6969c-450">**Неопределенное**</span><span class="sxs-lookup"><span data-stu-id="6969c-450">**Undefined**</span></span>|<span data-ttu-id="6969c-451">Доступное значение: **undefined**</span><span class="sxs-lookup"><span data-stu-id="6969c-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="6969c-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="6969c-452">**Null**</span></span>|<span data-ttu-id="6969c-453">Доступное значение: **Null**</span><span class="sxs-lookup"><span data-stu-id="6969c-453">Single value: **null**</span></span>|  
|<span data-ttu-id="6969c-454">**Логический**</span><span class="sxs-lookup"><span data-stu-id="6969c-454">**Boolean**</span></span>|<span data-ttu-id="6969c-455">Доступные значения: **false**, **true**</span><span class="sxs-lookup"><span data-stu-id="6969c-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="6969c-456">**Число**</span><span class="sxs-lookup"><span data-stu-id="6969c-456">**Number**</span></span>|<span data-ttu-id="6969c-457">Число с плавающей запятой двойной точности, стандарт IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="6969c-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="6969c-458">**Строка**</span><span class="sxs-lookup"><span data-stu-id="6969c-458">**String**</span></span>|<span data-ttu-id="6969c-459">Последовательности из нуля или более знаков Юникода.</span><span class="sxs-lookup"><span data-stu-id="6969c-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="6969c-460">Строки необходимо заключить в одинарные или двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="6969c-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="6969c-461">**Массив**</span><span class="sxs-lookup"><span data-stu-id="6969c-461">**Array**</span></span>|<span data-ttu-id="6969c-462">Последовательность из нуля или более элементов.</span><span class="sxs-lookup"><span data-stu-id="6969c-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="6969c-463">Каждый элемент может иметь значение любого скалярного типа данных (за исключением типа "Неопределенное").</span><span class="sxs-lookup"><span data-stu-id="6969c-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="6969c-464">**Объект**</span><span class="sxs-lookup"><span data-stu-id="6969c-464">**Object**</span></span>|<span data-ttu-id="6969c-465">Неупорядоченный набор из нуля или более пар "имя — значение".</span><span class="sxs-lookup"><span data-stu-id="6969c-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="6969c-466">Имя является строкой Юникода. Значение может иметь любой скалярный тип данных (за исключением типа **Неопределенное**).</span><span class="sxs-lookup"><span data-stu-id="6969c-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="6969c-467">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-467">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="6969c-468">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="6969c-469">Представляет неопределенное значение типа "Неопределенное".</span><span class="sxs-lookup"><span data-stu-id="6969c-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="6969c-470">Представляет значение **Null** типа **Null**.</span><span class="sxs-lookup"><span data-stu-id="6969c-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="6969c-471">Представляет константу типа "Логический".</span><span class="sxs-lookup"><span data-stu-id="6969c-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="6969c-472">Представляет значение **false** типа "Логический".</span><span class="sxs-lookup"><span data-stu-id="6969c-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="6969c-473">Представляет значение **true** типа "Логический".</span><span class="sxs-lookup"><span data-stu-id="6969c-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="6969c-474">Представляет константу.</span><span class="sxs-lookup"><span data-stu-id="6969c-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="6969c-475">Десятичные литералы — это числа, представленные в десятичном или экспоненциальном представлении.</span><span class="sxs-lookup"><span data-stu-id="6969c-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="6969c-476">Шестнадцатеричные литералы — это числа, представленные с помощью префикса 0x, за которым следуют одна или несколько шестнадцатеричных цифр.</span><span class="sxs-lookup"><span data-stu-id="6969c-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="6969c-477">Представляет константу типа "Строка".</span><span class="sxs-lookup"><span data-stu-id="6969c-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="6969c-478">Строковые литералы — это строки Юникода, представленные в виде последовательности из нуля или более знаков Юникода или escape-последовательностей.</span><span class="sxs-lookup"><span data-stu-id="6969c-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="6969c-479">Строковые литералы заключаются в одинарные кавычки (апостроф — ') или двойные кавычки (кавычки — ").</span><span class="sxs-lookup"><span data-stu-id="6969c-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="6969c-480">Допускаются следующие escape-последовательности:</span><span class="sxs-lookup"><span data-stu-id="6969c-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="6969c-481">**escape-последовательность**</span><span class="sxs-lookup"><span data-stu-id="6969c-481">**Escape sequence**</span></span>|<span data-ttu-id="6969c-482">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6969c-482">**Description**</span></span>|<span data-ttu-id="6969c-483">**Символ Юникода**</span><span class="sxs-lookup"><span data-stu-id="6969c-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="6969c-484">\\'</span><span class="sxs-lookup"><span data-stu-id="6969c-484">\\'</span></span>|<span data-ttu-id="6969c-485">Апостроф (')</span><span class="sxs-lookup"><span data-stu-id="6969c-485">apostrophe (')</span></span>|<span data-ttu-id="6969c-486">U+0027</span><span class="sxs-lookup"><span data-stu-id="6969c-486">U+0027</span></span>|  
|<span data-ttu-id="6969c-487">\\"</span><span class="sxs-lookup"><span data-stu-id="6969c-487">\\"</span></span>|<span data-ttu-id="6969c-488">Кавычки (")</span><span class="sxs-lookup"><span data-stu-id="6969c-488">quotation mark (")</span></span>|<span data-ttu-id="6969c-489">U+0022</span><span class="sxs-lookup"><span data-stu-id="6969c-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="6969c-490">Обратная косая черта (\\)</span><span class="sxs-lookup"><span data-stu-id="6969c-490">reverse solidus (\\)</span></span>|<span data-ttu-id="6969c-491">U+005C</span><span class="sxs-lookup"><span data-stu-id="6969c-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="6969c-492">Косая черта (/)</span><span class="sxs-lookup"><span data-stu-id="6969c-492">solidus (/)</span></span>|<span data-ttu-id="6969c-493">U+002F</span><span class="sxs-lookup"><span data-stu-id="6969c-493">U+002F</span></span>|  
|<span data-ttu-id="6969c-494">\b</span><span class="sxs-lookup"><span data-stu-id="6969c-494">\b</span></span>|<span data-ttu-id="6969c-495">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="6969c-495">backspace</span></span>|<span data-ttu-id="6969c-496">U+0008</span><span class="sxs-lookup"><span data-stu-id="6969c-496">U+0008</span></span>|  
|<span data-ttu-id="6969c-497">\f</span><span class="sxs-lookup"><span data-stu-id="6969c-497">\f</span></span>|<span data-ttu-id="6969c-498">Смена страницы</span><span class="sxs-lookup"><span data-stu-id="6969c-498">form feed</span></span>|<span data-ttu-id="6969c-499">U+000C</span><span class="sxs-lookup"><span data-stu-id="6969c-499">U+000C</span></span>|  
|\n|<span data-ttu-id="6969c-500">Перевод строки</span><span class="sxs-lookup"><span data-stu-id="6969c-500">line feed</span></span>|<span data-ttu-id="6969c-501">U+000A</span><span class="sxs-lookup"><span data-stu-id="6969c-501">U+000A</span></span>|  
|<span data-ttu-id="6969c-502">\r</span><span class="sxs-lookup"><span data-stu-id="6969c-502">\r</span></span>|<span data-ttu-id="6969c-503">Возврат каретки</span><span class="sxs-lookup"><span data-stu-id="6969c-503">carriage return</span></span>|<span data-ttu-id="6969c-504">U+000D</span><span class="sxs-lookup"><span data-stu-id="6969c-504">U+000D</span></span>|  
|<span data-ttu-id="6969c-505">\t</span><span class="sxs-lookup"><span data-stu-id="6969c-505">\t</span></span>|<span data-ttu-id="6969c-506">TAB</span><span class="sxs-lookup"><span data-stu-id="6969c-506">tab</span></span>|<span data-ttu-id="6969c-507">U+0009</span><span class="sxs-lookup"><span data-stu-id="6969c-507">U+0009</span></span>|  
|<span data-ttu-id="6969c-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="6969c-508">\uXXXX</span></span>|<span data-ttu-id="6969c-509">Символ Юникода, определяемый 4 шестнадцатеричными цифрами.</span><span class="sxs-lookup"><span data-stu-id="6969c-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="6969c-510">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="6969c-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="6969c-511"><a name="bk_query_perf_guidelines"></a> Рекомендации по повышению производительности запросов</span><span class="sxs-lookup"><span data-stu-id="6969c-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="6969c-512">Чтобы повысить эффективность запросов для больших коллекций, следует применить фильтры, которые могут обрабатываться одним или несколькими индексами.</span><span class="sxs-lookup"><span data-stu-id="6969c-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="6969c-513">При поиске по индексу можно применять следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="6969c-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="6969c-514">Используйте оператор равенства (=) с выражением пути к документу и константой.</span><span class="sxs-lookup"><span data-stu-id="6969c-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="6969c-515">Используйте операторы диапазона (<, \<=, >, >=) с выражением пути к документу и числовыми константами.</span><span class="sxs-lookup"><span data-stu-id="6969c-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="6969c-516">Выражение пути к документу — это любое выражение, которое определяет постоянный путь в документах из указанной коллекции баз данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="6969c-517">**Выражение пути к документу**</span><span class="sxs-lookup"><span data-stu-id="6969c-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="6969c-518">Выражения пути к документу — это выражения, которые оценивают путь свойства или индексатор массива в документе из коллекции баз данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="6969c-519">Этот путь позволяет определить расположение значений, указанных в фильтре непосредственно в документах из коллекции баз данных.</span><span class="sxs-lookup"><span data-stu-id="6969c-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="6969c-520">Чтобы выражение рассматривалось как выражение пути к документу, оно должно:</span><span class="sxs-lookup"><span data-stu-id="6969c-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="6969c-521">Ссылаться непосредственно на корневую коллекцию.</span><span class="sxs-lookup"><span data-stu-id="6969c-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="6969c-522">Ссылаться на свойство или индексатор массива констант любого выражения пути к документу.</span><span class="sxs-lookup"><span data-stu-id="6969c-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="6969c-523">Ссылаться на псевдоним, который представляет выражение пути к документу.</span><span class="sxs-lookup"><span data-stu-id="6969c-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="6969c-524">**Соглашения о синтаксисе**</span><span class="sxs-lookup"><span data-stu-id="6969c-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="6969c-525">В таблице ниже описываются соглашения, используемые для описания синтаксиса в справочнике по языку запросов API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6969c-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="6969c-526">**Соглашение**</span><span class="sxs-lookup"><span data-stu-id="6969c-526">**Convention**</span></span>|<span data-ttu-id="6969c-527">**Область использования**</span><span class="sxs-lookup"><span data-stu-id="6969c-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="6969c-528">Прописные буквы</span><span class="sxs-lookup"><span data-stu-id="6969c-528">UPPERCASE</span></span>|<span data-ttu-id="6969c-529">Ключевые слова, не учитывающие регистр.</span><span class="sxs-lookup"><span data-stu-id="6969c-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="6969c-530">Нижний регистр</span><span class="sxs-lookup"><span data-stu-id="6969c-530">lowercase</span></span>|<span data-ttu-id="6969c-531">Ключевые слова, учитывающие регистр.</span><span class="sxs-lookup"><span data-stu-id="6969c-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="6969c-532">\<Нетерминальный символ></span><span class="sxs-lookup"><span data-stu-id="6969c-532">\<nonterminal></span></span>|<span data-ttu-id="6969c-533">Нетерминальный символ, определяется отдельно.</span><span class="sxs-lookup"><span data-stu-id="6969c-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="6969c-534">\<Нетерминальный символ> ::=</span><span class="sxs-lookup"><span data-stu-id="6969c-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="6969c-535">Определение синтаксиса нетерминального символа.</span><span class="sxs-lookup"><span data-stu-id="6969c-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="6969c-536">Другие терминальные символы</span><span class="sxs-lookup"><span data-stu-id="6969c-536">other_terminal</span></span>|<span data-ttu-id="6969c-537">Терминальный символ (лексема) подробно описывается в словах.</span><span class="sxs-lookup"><span data-stu-id="6969c-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="6969c-538">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="6969c-538">identifier</span></span>|<span data-ttu-id="6969c-539">Идентификатор.</span><span class="sxs-lookup"><span data-stu-id="6969c-539">Identifier.</span></span> <span data-ttu-id="6969c-540">Поддерживает только следующие знаки: a–z, A–Z, 0–9. Первый знак не может быть цифрой.</span><span class="sxs-lookup"><span data-stu-id="6969c-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="6969c-541">Строка</span><span class="sxs-lookup"><span data-stu-id="6969c-541">"string"</span></span>|<span data-ttu-id="6969c-542">Строка в кавычках.</span><span class="sxs-lookup"><span data-stu-id="6969c-542">Quoted string.</span></span> <span data-ttu-id="6969c-543">Разрешает любые допустимые строки.</span><span class="sxs-lookup"><span data-stu-id="6969c-543">Allows any valid string.</span></span> <span data-ttu-id="6969c-544">См. описание аргумента string_literal.</span><span class="sxs-lookup"><span data-stu-id="6969c-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="6969c-545">Символ</span><span class="sxs-lookup"><span data-stu-id="6969c-545">'symbol'</span></span>|<span data-ttu-id="6969c-546">Литеральный символ, который является частью синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="6969c-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="6969c-547">&#124; (вертикальная линия)</span><span class="sxs-lookup"><span data-stu-id="6969c-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="6969c-548">Варианты элементов синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="6969c-548">Alternatives for syntax items.</span></span> <span data-ttu-id="6969c-549">Можно использовать только один из указанных элементов.</span><span class="sxs-lookup"><span data-stu-id="6969c-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="6969c-550">[ ] /(квадратные скобки)</span><span class="sxs-lookup"><span data-stu-id="6969c-550">[ ] /(brackets)</span></span>|<span data-ttu-id="6969c-551">В квадратных скобках указывается один или несколько дополнительных элементов.</span><span class="sxs-lookup"><span data-stu-id="6969c-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="6969c-552">[ ,…n ]</span><span class="sxs-lookup"><span data-stu-id="6969c-552">[ ,...n ]</span></span>|<span data-ttu-id="6969c-553">Указывает, что предшествующий элемент может повторяться несколько раз.</span><span class="sxs-lookup"><span data-stu-id="6969c-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="6969c-554">Отдельные вхождения элемента разделяются запятыми.</span><span class="sxs-lookup"><span data-stu-id="6969c-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="6969c-555">[ …n ]</span><span class="sxs-lookup"><span data-stu-id="6969c-555">[ ...n ]</span></span>|<span data-ttu-id="6969c-556">Указывает, что предшествующий элемент может повторяться несколько раз.</span><span class="sxs-lookup"><span data-stu-id="6969c-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="6969c-557">Отдельные вхождения элемента разделяются пробелами.</span><span class="sxs-lookup"><span data-stu-id="6969c-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="6969c-558"><a name="bk_built_in_functions"></a>Встроенные функции</span><span class="sxs-lookup"><span data-stu-id="6969c-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="6969c-559">Azure Cosmos DB предоставляет множество встроенных функций SQL.</span><span class="sxs-lookup"><span data-stu-id="6969c-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="6969c-560">Ниже перечислены их категории.</span><span class="sxs-lookup"><span data-stu-id="6969c-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="6969c-561">Функция</span><span class="sxs-lookup"><span data-stu-id="6969c-561">Function</span></span>|<span data-ttu-id="6969c-562">Описание</span><span class="sxs-lookup"><span data-stu-id="6969c-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="6969c-563">Математические функции</span><span class="sxs-lookup"><span data-stu-id="6969c-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="6969c-564">Математические функции выполняют вычисление, которое обычно основано на входных значениях, предоставляемых в форме аргументов, и возвращают числовое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="6969c-565">Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="6969c-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="6969c-566">Функции проверки типа позволяют проверять тип выражения в запросах SQL.</span><span class="sxs-lookup"><span data-stu-id="6969c-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="6969c-567">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="6969c-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="6969c-568">Cтроковые функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="6969c-569">Функции массивов</span><span class="sxs-lookup"><span data-stu-id="6969c-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="6969c-570">Функции массивов выполняют операцию над входным массивом и возвращают числовое, логическое значение либо массив.</span><span class="sxs-lookup"><span data-stu-id="6969c-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="6969c-571">Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="6969c-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="6969c-572">Пространственные функции выполняют операцию над входным пространственным объектом и возвращают числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="6969c-573"><a name="bk_mathematical_functions"></a>Математические функции</span><span class="sxs-lookup"><span data-stu-id="6969c-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="6969c-574">Следующие функции выполняют вычисление, которое обычно основано на входных значениях, предоставляемых в форме аргументов, и возвращают числовое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="6969c-575">ABS</span><span class="sxs-lookup"><span data-stu-id="6969c-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="6969c-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="6969c-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="6969c-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="6969c-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="6969c-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="6969c-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="6969c-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="6969c-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="6969c-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="6969c-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="6969c-581">COS</span><span class="sxs-lookup"><span data-stu-id="6969c-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="6969c-582">COT</span><span class="sxs-lookup"><span data-stu-id="6969c-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="6969c-583">DEGREES</span><span class="sxs-lookup"><span data-stu-id="6969c-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="6969c-584">EXP</span><span class="sxs-lookup"><span data-stu-id="6969c-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="6969c-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="6969c-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="6969c-586">LOG</span><span class="sxs-lookup"><span data-stu-id="6969c-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="6969c-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="6969c-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="6969c-588">PI</span><span class="sxs-lookup"><span data-stu-id="6969c-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="6969c-589">POWER</span><span class="sxs-lookup"><span data-stu-id="6969c-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="6969c-590">RADIANS</span><span class="sxs-lookup"><span data-stu-id="6969c-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="6969c-591">ROUND</span><span class="sxs-lookup"><span data-stu-id="6969c-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="6969c-592">SIN</span><span class="sxs-lookup"><span data-stu-id="6969c-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="6969c-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="6969c-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="6969c-594">SQUARE</span><span class="sxs-lookup"><span data-stu-id="6969c-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="6969c-595">SIGN</span><span class="sxs-lookup"><span data-stu-id="6969c-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="6969c-596">TAN</span><span class="sxs-lookup"><span data-stu-id="6969c-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="6969c-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="6969c-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="6969c-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="6969c-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="6969c-599">Возвращает модуль (положительное значение) указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-600">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-601">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-602">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-603">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-603">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-604">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-605">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-605">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-606">В приведенном ниже примере показаны результаты применения функции ABS к трем различным числам.</span><span class="sxs-lookup"><span data-stu-id="6969c-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="6969c-607">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="6969c-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="6969c-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="6969c-609">Возвращает угол в радианах, косинус которого равен указанному числовому выражению; также называется арккосинусом.</span><span class="sxs-lookup"><span data-stu-id="6969c-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="6969c-610">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-611">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-612">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-613">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-613">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-614">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-615">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-615">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-616">Пример ниже возвращает значение функции ACOS от –1.</span><span class="sxs-lookup"><span data-stu-id="6969c-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="6969c-617">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="6969c-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="6969c-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="6969c-619">Возвращает угол в радианах, синус которого равен указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="6969c-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="6969c-620">Также называется арксинусом.</span><span class="sxs-lookup"><span data-stu-id="6969c-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="6969c-621">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-622">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-623">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-624">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-624">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-625">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-626">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-626">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-627">Пример ниже возвращает значение функции ASIN от –1.</span><span class="sxs-lookup"><span data-stu-id="6969c-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="6969c-628">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="6969c-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="6969c-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="6969c-630">Возвращает угол в радианах, тангенс которого равен указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="6969c-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="6969c-631">Также называется арктангенсом.</span><span class="sxs-lookup"><span data-stu-id="6969c-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="6969c-632">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-633">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-634">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-635">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-635">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-636">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-637">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-637">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-638">Пример ниже возвращает значение функции ASIN от указанного значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="6969c-639">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="6969c-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="6969c-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="6969c-641">Возвращает основное значение арктангенса y/x, выраженное в радианах.</span><span class="sxs-lookup"><span data-stu-id="6969c-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="6969c-642">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-643">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-644">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-645">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-645">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-646">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-647">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-647">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-648">В примере ниже вычисляется ATN2 для указанных компонентов x и y.</span><span class="sxs-lookup"><span data-stu-id="6969c-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="6969c-649">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="6969c-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="6969c-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="6969c-651">Возвращает наименьшее целочисленное значение, которое больше или равно указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="6969c-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-652">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-653">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-654">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-655">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-655">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-656">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-657">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-657">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-658">В примере ниже показаны положительные числовые, отрицательные и нулевые значения функции CEILING.</span><span class="sxs-lookup"><span data-stu-id="6969c-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="6969c-659">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="6969c-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="6969c-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="6969c-661">Возвращает тригонометрический косинус указанного угла в радианах в указанном выражении.</span><span class="sxs-lookup"><span data-stu-id="6969c-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="6969c-662">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-663">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-664">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-665">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-665">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-666">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-667">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-667">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-668">В примере ниже вычисляется COS указанного угла.</span><span class="sxs-lookup"><span data-stu-id="6969c-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="6969c-669">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="6969c-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="6969c-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="6969c-671">Возвращает тригонометрический котангенс указанного угла в радианах в указанном числовом выражении.</span><span class="sxs-lookup"><span data-stu-id="6969c-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-672">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-673">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-674">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-675">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-675">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-676">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-677">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-677">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-678">В примере ниже вычисляется COT указанного угла.</span><span class="sxs-lookup"><span data-stu-id="6969c-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="6969c-679">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="6969c-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="6969c-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="6969c-681">Возвращает соответствующее значение угла в градусах для угла, указанного в радианах.</span><span class="sxs-lookup"><span data-stu-id="6969c-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="6969c-682">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-683">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-684">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-685">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-685">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-686">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-687">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-687">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-688">Следующий пример возвращает число градусов в угле, равном PI/2 радиан.</span><span class="sxs-lookup"><span data-stu-id="6969c-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="6969c-689">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="6969c-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="6969c-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="6969c-691">Возвращает наибольшее целочисленное значение, которое меньше или равно указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="6969c-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-692">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-693">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-694">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-695">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-695">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-696">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-697">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-697">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-698">В примере ниже показаны положительные числовые, отрицательные и нулевые значения функции FLOOR.</span><span class="sxs-lookup"><span data-stu-id="6969c-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="6969c-699">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="6969c-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="6969c-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="6969c-701">Возвращает значение экспоненты для указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-702">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-703">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-704">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-705">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-705">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-706">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-707">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-707">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-708">Константа **e** (2,718281…) является основанием натуральных логарифмов.</span><span class="sxs-lookup"><span data-stu-id="6969c-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="6969c-709">Экспонента числа — это константа **e** степени числа.</span><span class="sxs-lookup"><span data-stu-id="6969c-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="6969c-710">Например, EXP(1.0) = e^1.0 = 2,71828182845905 и EXP(10) = e^10 = 22026,4657948067.</span><span class="sxs-lookup"><span data-stu-id="6969c-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="6969c-711">Экспонента натурального логарифма числа — это само число. Например, EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="6969c-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="6969c-712">Натуральный логарифм экспоненты числа также является числом. Например, LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="6969c-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="6969c-713">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-713">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-714">В примере ниже объявляется переменная и возвращается значение экспоненты указанной переменной (10).</span><span class="sxs-lookup"><span data-stu-id="6969c-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="6969c-715">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="6969c-716">Пример ниже возвращает значение экспоненты от натурального логарифма 20 и натуральный логарифм экспоненты 20.</span><span class="sxs-lookup"><span data-stu-id="6969c-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="6969c-717">Так как эти функции обратные, в обоих случаях возвращается значение 20 (после округления до плавающей запятой).</span><span class="sxs-lookup"><span data-stu-id="6969c-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="6969c-718">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="6969c-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="6969c-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="6969c-720">Возвращает натуральный логарифм от указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-721">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="6969c-722">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-723">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="6969c-724">Дополнительный числовой аргумент, который задает основание логарифма.</span><span class="sxs-lookup"><span data-stu-id="6969c-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="6969c-725">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-725">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-726">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-727">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-727">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-728">По умолчанию функция LOG() возвращает натуральный логарифм.</span><span class="sxs-lookup"><span data-stu-id="6969c-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="6969c-729">Основание логарифма можно изменить с помощью дополнительного параметра основания.</span><span class="sxs-lookup"><span data-stu-id="6969c-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="6969c-730">Натуральный логарифм — это логарифм с основанием **e**, где **e** — это иррациональная константа приблизительно равная 2,718281828.</span><span class="sxs-lookup"><span data-stu-id="6969c-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="6969c-731">Натуральный логарифм экспоненты числа — это само число. Например, LOG( EXP( n ) ) = n.</span><span class="sxs-lookup"><span data-stu-id="6969c-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="6969c-732">И экспонента натурального логарифма числа также является самым числом. Например, EXP( LOG( n ) ) = n.</span><span class="sxs-lookup"><span data-stu-id="6969c-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="6969c-733">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-733">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-734">В примере ниже объявляется переменная и возвращается значение логарифма указанной переменной (10).</span><span class="sxs-lookup"><span data-stu-id="6969c-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="6969c-735">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="6969c-736">В примере ниже вычисляется логарифм экспоненты числа.</span><span class="sxs-lookup"><span data-stu-id="6969c-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="6969c-737">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="6969c-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="6969c-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="6969c-739">Возвращает десятичный логарифм от указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-740">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-741">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-742">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-743">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-743">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-744">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-745">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="6969c-745">**Remarks**</span></span>  
  
 <span data-ttu-id="6969c-746">Функции LOG10 и POWER обратно связаны друг с другом.</span><span class="sxs-lookup"><span data-stu-id="6969c-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="6969c-747">Например, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="6969c-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="6969c-748">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-748">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-749">В примере ниже объявляется переменная и возвращается значение LOG10 указанной переменной (100).</span><span class="sxs-lookup"><span data-stu-id="6969c-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="6969c-750">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="6969c-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="6969c-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="6969c-752">Возвращает значение константы "пи".</span><span class="sxs-lookup"><span data-stu-id="6969c-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="6969c-753">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="6969c-754">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-755">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-756">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-756">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-757">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-758">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-758">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-759">Пример ниже возвращает значение PI.</span><span class="sxs-lookup"><span data-stu-id="6969c-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="6969c-760">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="6969c-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="6969c-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="6969c-762">Возвращает результат возведения указанного числового выражения в заданную степень.</span><span class="sxs-lookup"><span data-stu-id="6969c-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="6969c-763">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="6969c-764">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-765">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="6969c-766">Степень для возведения аргумента `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="6969c-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="6969c-767">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-767">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-768">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-769">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-769">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-770">В следующем примере показано возведение числа в третью степень (куб числа).</span><span class="sxs-lookup"><span data-stu-id="6969c-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="6969c-771">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="6969c-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="6969c-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="6969c-773">Возвращает значение угла в радианах для числового значения, указанного в градусах.</span><span class="sxs-lookup"><span data-stu-id="6969c-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="6969c-774">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-775">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-776">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-777">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-777">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-778">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-779">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-779">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-780">В примере ниже берется несколько углов в качестве входных данных и возвращаются их соответствующие значения в радианах.</span><span class="sxs-lookup"><span data-stu-id="6969c-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="6969c-781">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="6969c-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="6969c-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="6969c-783">Возвращает числовое значение, округленное до ближайшего целого значения в большую сторону.</span><span class="sxs-lookup"><span data-stu-id="6969c-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="6969c-784">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-785">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-786">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-787">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-787">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-788">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-789">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-789">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-790">В примере ниже положительные и отрицательные числа округляются до ближайшего целого.</span><span class="sxs-lookup"><span data-stu-id="6969c-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="6969c-791">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="6969c-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="6969c-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="6969c-793">Возвращает знак указанного числового выражения (+1 для положительных чисел, 0 для нуля или -1 для отрицательных).</span><span class="sxs-lookup"><span data-stu-id="6969c-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-794">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-795">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-796">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-797">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-797">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-798">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-799">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-799">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-800">Пример ниже возвращает значения SIGN для чисел от –2 до 2.</span><span class="sxs-lookup"><span data-stu-id="6969c-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="6969c-801">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="6969c-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="6969c-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="6969c-803">Возвращает тригонометрический синус заданного угла в радианах для указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="6969c-804">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-805">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-806">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-807">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-807">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-808">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-809">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-809">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-810">В примере ниже вычисляется синус указанного угла.</span><span class="sxs-lookup"><span data-stu-id="6969c-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="6969c-811">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="6969c-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="6969c-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="6969c-813">Возвращает квадратный корень из указанного числового значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="6969c-814">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-815">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-816">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-817">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-817">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-818">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-819">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-819">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-820">Пример ниже возвращает квадратный корень для чисел 1–3.</span><span class="sxs-lookup"><span data-stu-id="6969c-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="6969c-821">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="6969c-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="6969c-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="6969c-823">Возвращает квадратный корень из указанного числового значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="6969c-824">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-825">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-826">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-827">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-827">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-828">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-829">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-829">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-830">Пример ниже возвращает квадраты для чисел 1–3.</span><span class="sxs-lookup"><span data-stu-id="6969c-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="6969c-831">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="6969c-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="6969c-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="6969c-833">Возвращает тангенс заданного угла в радианах для указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="6969c-834">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-835">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-836">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-837">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-837">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-838">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-839">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-839">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-840">Пример ниже вычисляет тангенс от PI()/2.</span><span class="sxs-lookup"><span data-stu-id="6969c-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="6969c-841">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="6969c-842"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="6969c-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="6969c-843">Возвращает числовое значение, округленное до ближайшего целого значения в меньшую сторону.</span><span class="sxs-lookup"><span data-stu-id="6969c-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="6969c-844">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="6969c-845">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="6969c-846">Числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-847">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-847">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-848">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-849">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-849">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-850">В примере ниже положительные и отрицательные числа усекаются до ближайшего целого значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="6969c-851">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="6969c-852"><a name="bk_type_checking_functions"></a> Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="6969c-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="6969c-853">Следующие функции поддерживают проверку типа входных значений и возвращают логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="6969c-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="6969c-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="6969c-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="6969c-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="6969c-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="6969c-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="6969c-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="6969c-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="6969c-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="6969c-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="6969c-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="6969c-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="6969c-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="6969c-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="6969c-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="6969c-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="6969c-862"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="6969c-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="6969c-863">Возвращает логическое значение, указывающее, является ли указанное выражение массивом.</span><span class="sxs-lookup"><span data-stu-id="6969c-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="6969c-864">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="6969c-865">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-866">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-867">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-867">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-868">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-869">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-869">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-870">В примере ниже с помощью функции IS_ARRAY проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-871">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="6969c-872"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="6969c-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="6969c-873">Возвращает логическое значение, указывающее, является ли указанное выражение логическим значением.</span><span class="sxs-lookup"><span data-stu-id="6969c-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="6969c-874">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="6969c-875">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-876">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-877">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-877">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-878">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-879">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-879">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-880">В примере ниже с помощью функции IS_BOOL проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-881">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="6969c-882"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="6969c-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="6969c-883">Возвращает логическое значение, указывающее, назначено ли свойству значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="6969c-884">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="6969c-885">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-886">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-887">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-887">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-888">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-889">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-889">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-890">В примере ниже проверяется наличие свойства в указанном документе JSON.</span><span class="sxs-lookup"><span data-stu-id="6969c-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="6969c-891">Первый пример возвращает значение true, так как присутствует значение "a", но второй возвращает значение false, так как значение "b" отсутствует.</span><span class="sxs-lookup"><span data-stu-id="6969c-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="6969c-892">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="6969c-893"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="6969c-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="6969c-894">Возвращает логическое значение, указывающее, является ли указанное выражение значением Null.</span><span class="sxs-lookup"><span data-stu-id="6969c-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="6969c-895">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="6969c-896">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-897">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-898">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-898">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-899">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-900">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-900">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-901">В примере ниже с помощью функции IS_NULL проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-902">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="6969c-903"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="6969c-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="6969c-904">Возвращает логическое значение, указывающее, является ли указанное выражение числовым значением.</span><span class="sxs-lookup"><span data-stu-id="6969c-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="6969c-905">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="6969c-906">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-907">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-908">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-908">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-909">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-910">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-910">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-911">В примере ниже с помощью функции IS_NULL проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-912">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="6969c-913"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="6969c-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="6969c-914">Возвращает логическое значение, указывающее, является ли указанное выражение объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="6969c-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="6969c-915">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="6969c-916">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-917">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-918">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-918">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-919">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-920">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-920">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-921">В примере ниже с помощью функции IS_OBJECT проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-922">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="6969c-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="6969c-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="6969c-924">Возвращает логическое значение, указывающее, является ли указанное выражение примитивом (строкой, логическим значением, числовым значением или значением Null).</span><span class="sxs-lookup"><span data-stu-id="6969c-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="6969c-925">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="6969c-926">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-927">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-928">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-928">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-929">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-930">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-930">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-931">В примере ниже с помощью функции IS_PRIMITIVE проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-932">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="6969c-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="6969c-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="6969c-934">Возвращает логическое значение, указывающее, является ли указанное выражение строковым значением.</span><span class="sxs-lookup"><span data-stu-id="6969c-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="6969c-935">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="6969c-936">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="6969c-937">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-938">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-938">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-939">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-940">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-940">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-941">В примере ниже с помощью функции IS_STRING проверяются логические значения JSON, числа, строки, значения Null, объекты, массивы и неопределенные типы.</span><span class="sxs-lookup"><span data-stu-id="6969c-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="6969c-942">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="6969c-943"><a name="bk_string_functions"></a> Строковые функции</span><span class="sxs-lookup"><span data-stu-id="6969c-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="6969c-944">Следующие скалярные функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="6969c-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="6969c-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="6969c-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="6969c-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="6969c-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="6969c-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="6969c-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="6969c-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="6969c-949">LEFT</span><span class="sxs-lookup"><span data-stu-id="6969c-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="6969c-950">LENGTH</span><span class="sxs-lookup"><span data-stu-id="6969c-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="6969c-951">LOWER</span><span class="sxs-lookup"><span data-stu-id="6969c-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="6969c-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="6969c-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="6969c-953">REPLACE</span><span class="sxs-lookup"><span data-stu-id="6969c-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="6969c-954">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="6969c-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="6969c-955">REVERSE</span><span class="sxs-lookup"><span data-stu-id="6969c-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="6969c-956">RIGHT</span><span class="sxs-lookup"><span data-stu-id="6969c-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="6969c-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="6969c-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="6969c-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="6969c-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="6969c-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="6969c-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="6969c-960">UPPER</span><span class="sxs-lookup"><span data-stu-id="6969c-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="6969c-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="6969c-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="6969c-962">Возвращает строку, являющуюся результатом объединения двух или более строковых значений.</span><span class="sxs-lookup"><span data-stu-id="6969c-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="6969c-963">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="6969c-964">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-965">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-966">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-966">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-967">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-968">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-968">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-969">Пример ниже возвращает объединенную строку указанных значений.</span><span class="sxs-lookup"><span data-stu-id="6969c-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="6969c-970">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="6969c-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="6969c-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="6969c-972">Возвращает значение логического типа, указывающее, содержит ли первое строковое выражение второе.</span><span class="sxs-lookup"><span data-stu-id="6969c-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="6969c-973">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="6969c-974">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-975">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-976">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-976">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-977">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-978">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-978">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-979">Пример ниже проверяет, содержит ли строка "abc"вхождения "ab" и "d".</span><span class="sxs-lookup"><span data-stu-id="6969c-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="6969c-980">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="6969c-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="6969c-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="6969c-982">Возвращает значение логического типа, указывающее, заканчивается ли первое строковое выражение вторым.</span><span class="sxs-lookup"><span data-stu-id="6969c-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="6969c-983">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="6969c-984">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-985">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-986">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-986">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-987">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-988">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-988">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-989">Пример ниже возвращает строки "abc", в конце которых есть "b" и "bc".</span><span class="sxs-lookup"><span data-stu-id="6969c-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="6969c-990">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="6969c-991"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="6969c-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="6969c-992">Возвращает начальную позицию первого вхождения второго строкового выражения в первое указанное строковое выражение или –1, если строка не найдена.</span><span class="sxs-lookup"><span data-stu-id="6969c-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="6969c-993">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="6969c-994">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-995">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-996">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-996">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-997">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-998">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-998">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-999">Пример ниже возвращает индекс различных подстрок в строке "abc".</span><span class="sxs-lookup"><span data-stu-id="6969c-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="6969c-1000">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="6969c-1001"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="6969c-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="6969c-1002">Возвращает левую часть строки с указанным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="6969c-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="6969c-1003">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="6969c-1004">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1005">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="6969c-1006">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-1007">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1008">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1009">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1009">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1010">Пример ниже возвращает левую часть строки "abc" для значений различной длины.</span><span class="sxs-lookup"><span data-stu-id="6969c-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="6969c-1011">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="6969c-1012"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="6969c-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="6969c-1013">Возвращает число символов указанного строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="6969c-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="6969c-1014">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="6969c-1015">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1016">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1017">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1018">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1019">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1019">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1020">Пример ниже возвращает длину строки.</span><span class="sxs-lookup"><span data-stu-id="6969c-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="6969c-1021">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="6969c-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="6969c-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="6969c-1023">Возвращает строковое выражение после преобразования символов верхнего регистра в нижний.</span><span class="sxs-lookup"><span data-stu-id="6969c-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="6969c-1024">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="6969c-1025">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1026">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1027">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1028">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1029">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1029">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1030">Ниже представлен пример использования функции LOWER в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="6969c-1031">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="6969c-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="6969c-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="6969c-1033">Возвращает строковое выражение после удаления начальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="6969c-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="6969c-1034">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="6969c-1035">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1036">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1037">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1038">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1039">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1039">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1040">Ниже представлен пример использования функции LTRIM в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="6969c-1041">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="6969c-1042"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="6969c-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="6969c-1043">Заменяет все вхождения указанного строкового значения другим строковым значением.</span><span class="sxs-lookup"><span data-stu-id="6969c-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="6969c-1044">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="6969c-1045">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1046">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1047">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1048">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1049">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1049">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1050">Ниже представлен пример использования функции REPLACE в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="6969c-1051">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="6969c-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="6969c-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="6969c-1053">Повторяет строковое значение указанное число раз.</span><span class="sxs-lookup"><span data-stu-id="6969c-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="6969c-1054">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="6969c-1055">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1056">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="6969c-1057">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-1058">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1059">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1060">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1060">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1061">Ниже представлен пример использования функции REPLICATE в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="6969c-1062">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="6969c-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="6969c-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="6969c-1064">Возвращает обратный порядок строкового значения.</span><span class="sxs-lookup"><span data-stu-id="6969c-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="6969c-1065">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="6969c-1066">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1067">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1068">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1069">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1070">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1070">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1071">Ниже представлен пример использования функции REVERSE в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="6969c-1072">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="6969c-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="6969c-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="6969c-1074">Возвращает правую часть строки с указанным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="6969c-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="6969c-1075">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="6969c-1076">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1077">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="6969c-1078">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-1079">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1080">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1081">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1081">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1082">Пример ниже возвращает правую часть строки "abc" для значений различной длины.</span><span class="sxs-lookup"><span data-stu-id="6969c-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="6969c-1083">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="6969c-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="6969c-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="6969c-1085">Возвращает строковое выражение после удаления конечных пробелов.</span><span class="sxs-lookup"><span data-stu-id="6969c-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="6969c-1086">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="6969c-1087">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1088">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1089">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1090">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1091">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1091">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1092">Ниже представлен пример использования функции RTRIM в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="6969c-1093">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="6969c-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="6969c-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="6969c-1095">Возвращает значение логического типа, указывающее, начинается ли первое строковое выражение вторым.</span><span class="sxs-lookup"><span data-stu-id="6969c-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="6969c-1096">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="6969c-1097">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1098">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1099">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1100">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-1101">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1101">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1102">Пример ниже проверяет, начинается ли строка "abc" с "b" и "a".</span><span class="sxs-lookup"><span data-stu-id="6969c-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="6969c-1103">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="6969c-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="6969c-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="6969c-1105">Возвращает часть строкового выражения, начиная с указанной позиции (отсчет начинается с нуля) и до достижения указанной длины (или до конца строки).</span><span class="sxs-lookup"><span data-stu-id="6969c-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="6969c-1106">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="6969c-1107">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1108">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="6969c-1109">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-1110">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1111">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1112">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1112">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1113">Пример ниже возвращает подстроку "abc", которая начинается с 1 и имеет длину в 1 знак.</span><span class="sxs-lookup"><span data-stu-id="6969c-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="6969c-1114">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="6969c-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="6969c-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="6969c-1116">Возвращает строковое выражение после преобразования символов нижнего регистра в верхний.</span><span class="sxs-lookup"><span data-stu-id="6969c-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="6969c-1117">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="6969c-1118">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="6969c-1119">Любое допустимое строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="6969c-1120">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1121">Возвращает строковое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="6969c-1122">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1122">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1123">Ниже представлен пример использования функции UPPER в запросе.</span><span class="sxs-lookup"><span data-stu-id="6969c-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="6969c-1124">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="6969c-1125"><a name="bk_array_functions"></a> Функции массивов</span><span class="sxs-lookup"><span data-stu-id="6969c-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="6969c-1126">Следующие скалярные функции выполняют операцию над входным массивом и возвращают числовое или логическое значение, либо массив.</span><span class="sxs-lookup"><span data-stu-id="6969c-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="6969c-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="6969c-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="6969c-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="6969c-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="6969c-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="6969c-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="6969c-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="6969c-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="6969c-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="6969c-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="6969c-1132">Возвращает массив, который является результатом объединения значений двух или более массивов.</span><span class="sxs-lookup"><span data-stu-id="6969c-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="6969c-1133">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="6969c-1134">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="6969c-1135">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="6969c-1136">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1137">Возвращает выражение массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="6969c-1138">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1138">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1139">В примере ниже показано, как объединить два массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="6969c-1140">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="6969c-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="6969c-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="6969c-1142">Возвращает логическое значение, указывающее, содержит ли массив указанное значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="6969c-1143">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="6969c-1144">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="6969c-1145">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="6969c-1146">Любое допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="6969c-1147">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1148">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="6969c-1149">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1149">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1150">В примере ниже показано, как проверить членство в массиве с помощью функции ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="6969c-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="6969c-1151">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="6969c-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="6969c-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="6969c-1153">Возвращает число элементов массива, указанного в выражении.</span><span class="sxs-lookup"><span data-stu-id="6969c-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="6969c-1154">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="6969c-1155">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="6969c-1156">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="6969c-1157">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1158">Возвращает числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-1159">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1159">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1160">В примере ниже показано, как получить длину массива с помощью функции ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="6969c-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="6969c-1161">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="6969c-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="6969c-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="6969c-1163">Возвращает часть выражения массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="6969c-1164">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="6969c-1165">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="6969c-1166">Любое допустимое выражение массива.</span><span class="sxs-lookup"><span data-stu-id="6969c-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="6969c-1167">Любое допустимое числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="6969c-1168">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1169">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="6969c-1170">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1170">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1171">В примере ниже показано, как получить часть массива с помощью функции ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="6969c-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="6969c-1172">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="6969c-1173"><a name="bk_spatial_functions"></a> Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="6969c-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="6969c-1174">Скалярные функции выполняют операцию над входным пространственным объектом и возвращают числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="6969c-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="6969c-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="6969c-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="6969c-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="6969c-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="6969c-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="6969c-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="6969c-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="6969c-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="6969c-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="6969c-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="6969c-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="6969c-1181">Возвращает расстояние между двумя выражениями точек GeoJSON, многоугольников или объектов LineString.</span><span class="sxs-lookup"><span data-stu-id="6969c-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="6969c-1182">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="6969c-1183">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1184">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="6969c-1185">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1186">Возвращает числовое выражение, указывающее расстояние.</span><span class="sxs-lookup"><span data-stu-id="6969c-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="6969c-1187">При использовании эталонной системы по умолчанию это значение указывается в метрах.</span><span class="sxs-lookup"><span data-stu-id="6969c-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="6969c-1188">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1188">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1189">В примере ниже показано, как вернуть все документы семейств, которые находятся в пределах 30 км от заданного расположения, с помощью встроенной функции ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="6969c-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="6969c-1190">.</span><span class="sxs-lookup"><span data-stu-id="6969c-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="6969c-1191">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="6969c-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="6969c-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="6969c-1193">Возвращает логическое выражение, указывающее, располагается ли объект GeoJSON (точка, многоугольник или LineString), указанный в первом аргументе, внутри второго объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="6969c-1194">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="6969c-1195">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1196">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1197">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="6969c-1198">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1199">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="6969c-1200">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1200">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1201">В следующем примере показано, как найти все документы семейства внутри многоугольника с помощью функции ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="6969c-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="6969c-1202">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="6969c-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="6969c-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="6969c-1204">Возвращает логическое выражение, указывающее, пересекается ли объект GeoJSON (точка, многоугольник или LineString), указанный в первом аргументе, со вторым объектом GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="6969c-1205">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="6969c-1206">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1207">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1208">Любое допустимое выражение объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="6969c-1209">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1210">Возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="6969c-1211">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1211">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1212">В примере ниже показано, как найти все области, пересекающиеся с заданным многоугольником.</span><span class="sxs-lookup"><span data-stu-id="6969c-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="6969c-1213">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="6969c-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="6969c-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="6969c-1215">Возвращает логическое значение, указывающее, является ли действительным выражение GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="6969c-1216">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="6969c-1217">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1218">Любое допустимое выражение GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="6969c-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="6969c-1219">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1220">Возвращает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="6969c-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="6969c-1221">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1221">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1222">В примере ниже показано, как проверить допустимость точки с помощью функции ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="6969c-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="6969c-1223">Например, эта точка может иметь значение широты, которое не входит в допустимый диапазон значений (от –90 до 90), из-за чего запрос возвращает значение false.</span><span class="sxs-lookup"><span data-stu-id="6969c-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="6969c-1224">По спецификации GeoJSON для многоугольника последняя пара координат должна совпадать с первой, чтобы фигура стала замкнутой.</span><span class="sxs-lookup"><span data-stu-id="6969c-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="6969c-1225">Точки внутри многоугольника должны указываться в порядке против часовой стрелки.</span><span class="sxs-lookup"><span data-stu-id="6969c-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="6969c-1226">Если точки указаны в порядке по часовой стрелке, то многоугольник представляет регион, расположенный снаружи от него.</span><span class="sxs-lookup"><span data-stu-id="6969c-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="6969c-1227">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="6969c-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="6969c-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="6969c-1229">Возвращает значение JSON, содержащее логическое значение, указывающее, является ли выражение GeoJSON (точка, многоугольник или LineString) действительным. Если оно является недействительным, то возвращаемое значение также содержит строку с описанием причины.</span><span class="sxs-lookup"><span data-stu-id="6969c-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="6969c-1230">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="6969c-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="6969c-1231">**Аргументы**</span><span class="sxs-lookup"><span data-stu-id="6969c-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="6969c-1232">Любое допустимое выражение точки или многоугольника GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="6969c-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="6969c-1233">**Типы возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="6969c-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="6969c-1234">Возвращает значение JSON, содержащее логическое значение, указывающее, является ли выражение точки или многоугольника GeoJSON действительным. Если оно является недействительным, возвращаемое значение также содержит строку с описанием причины.</span><span class="sxs-lookup"><span data-stu-id="6969c-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="6969c-1235">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="6969c-1235">**Examples**</span></span>  
  
 <span data-ttu-id="6969c-1236">В примере ниже показано, как проверить допустимость (с подробными сведениями) с помощью функции ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="6969c-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="6969c-1237">Результирующий набор:</span><span class="sxs-lookup"><span data-stu-id="6969c-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="6969c-1238">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6969c-1238">Next steps</span></span>  
 <span data-ttu-id="6969c-1239">[SQL-запросы и синтаксис SQL в Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="6969c-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="6969c-1240">Документация по базе данных Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="6969c-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
