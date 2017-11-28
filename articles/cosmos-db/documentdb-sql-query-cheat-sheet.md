---
title: "Памятка по SQL-запросам Azure Cosmos DB (PDF-файл) | Документация Майкрософт"
description: "Доступный для печати PDF-файл памятки по SQL-запросам, который поможет использовать синтаксис SQL в Azure Cosmos DB для выполнения запросов к документам JSON в базе данных — краткий справочник по SQL"
keywords: "памятка по SQL, PDF-файл памятки по SQL, памятка по SQL-запросам"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: monicar
ms.assetid: fdbdbc39-5a46-4129-b4ed-b049d1c9ccab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: mimig
ms.openlocfilehash: cd314049a536ad4a95e243eac26aa044c90c8164
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-query-cheat-sheet-pdf"></a><span data-ttu-id="eb5b1-104">Azure Cosmos DB. Памятка по SQL-запросам API DocumentDB в формате PDF</span><span class="sxs-lookup"><span data-stu-id="eb5b1-104">Azure Cosmos DB: DocumentDB API SQL query cheat sheet PDF</span></span>
<span data-ttu-id="eb5b1-105">**Памятка по SQL-запросам API DocumentDB Azure Cosmos DB** помогает быстро создавать запросы для данных API DocumentDB, так как в удобном для печати справочном листе в формате PDF отображаются общие запросы, ключевые слова, встроенные функции и операторы базы данных.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-105">The **Azure Cosmos DB: DocumentDB API SQL Query Cheat Sheet** helps you quickly write queries for DocumentDB API data by displaying common database queries, keywords, built-in functions, and operators in an easy to print PDF reference sheet.</span></span> 

<span data-ttu-id="eb5b1-106">Cosmos DB поддерживает реляционные, иерархические и пространственные запросы документов JSON с использованием [SQL](documentdb-sql-query.md) без указания схемы или вторичных индексов.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-106">Cosmos DB supports relational, hierarchical,  and spatial querying of JSON documents using [SQL](documentdb-sql-query.md) without specifying a schema or secondary indexes.</span></span> <span data-ttu-id="eb5b1-107">Кроме стандартных ключевых слов и операторов ANSI-SQL, Cosmos DB поддерживает определяемые пользователем функции (UDF) JavaScript, операторы JavaScript и множество встроенных функций.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-107">In addition to the standard ANSI-SQL keywords and operators, Cosmos DB supports JavaScript user defined functions (UDFs), JavaScript operators, and a multitude of built-in functions.</span></span>

## <a name="download-the-cosmos-db-sql-query-cheat-sheet-pdf"></a><span data-ttu-id="eb5b1-108">Скачивание PDF-файла памятки по SQL-запросам Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eb5b1-108">Download the Cosmos DB SQL query cheat sheet PDF</span></span>
<span data-ttu-id="eb5b1-109">Скачайте памятку по SQL-запросам и используйте ее в качестве краткого справочника, чтобы быстрее создавать запросы.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-109">Write your queries faster by downloading the SQL query cheat sheet and using it as a quick reference.</span></span> <span data-ttu-id="eb5b1-110">В PDF-файле памятки по SQL-запросам приводятся общие запросы, используемые для получения данных из двух примеров документов JSON.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-110">The SQL cheat sheet PDF shows common queries used to retrieve data from two example JSON documents.</span></span> <span data-ttu-id="eb5b1-111">Чтобы держать памятку по SQL-запросам под рукой, напечатайте ее на одной стороне листа в формате Letter (8,5 x 11 дюймов, или 21,59 x 27,94 см).</span><span class="sxs-lookup"><span data-stu-id="eb5b1-111">To keep it nearby, you can print the single-sided SQL query cheat sheet in page letter size (8.5 x 11 in.).</span></span>

<span data-ttu-id="eb5b1-112">**Памятку можно скачать по следующей ссылке: [Памятка по Microsoft Azure Cosmos DB SQL](http://go.microsoft.com/fwlink/?LinkId=623215)**.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-112">**Download the SQL cheat sheet here: [Microsoft Azure Cosmos DB SQL cheat sheet](http://go.microsoft.com/fwlink/?LinkId=623215)**</span></span>

![Памятка SQL-запросов Cosmos DB: краткий PDF-справочник по синтаксису SQL, поддерживаемому Cosmos DB — памятка по SQL, памятка по SQL в формате PDF, краткий справочник по SQL][cheat-sheet]

[cheat-sheet]: ./media/documentdb-sql-query-cheat-sheet/microsoft-documentdb-sql-query-cheat-sheet-v4.png


## <a name="more-help-with-writing-sql-queries"></a><span data-ttu-id="eb5b1-114">Дополнительная справка по созданию SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="eb5b1-114">More help with writing SQL queries</span></span>
* <span data-ttu-id="eb5b1-115">Подробное описание параметров запросов, доступных в DocumentDB, см. в статье [SQL-запросы и синтаксис SQL в Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="eb5b1-115">For a walk through of the query options available in Cosmos DB, see [Query Cosmos DB](documentdb-sql-query.md).</span></span>
* <span data-ttu-id="eb5b1-116">Связанную справочную документацию см. в разделе [Справочник по синтаксису SQL-запросов API DocumentDB в Azure Cosmos DB](https://msdn.microsoft.com/library/azure/dn782250.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb5b1-116">For the related reference documentation, see [Azure Cosmos DB DocumentDB API: SQL syntax reference](https://msdn.microsoft.com/library/azure/dn782250.aspx).</span></span>

## <a name="release-notes"></a><span data-ttu-id="eb5b1-117">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="eb5b1-117">Release notes</span></span>
<span data-ttu-id="eb5b1-118">Обновлено 29.07.2016 г.</span><span class="sxs-lookup"><span data-stu-id="eb5b1-118">Updated on 7/29/2016 to include TOP.</span></span>

