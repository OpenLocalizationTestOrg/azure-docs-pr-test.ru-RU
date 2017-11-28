---
title: "aaaIndexers в поиске Azure | Документы Microsoft"
description: "Обход контента базы данных Azure SQL, Azure Cosmos DB или для поиска данных tooextract хранилища Azure и заполнение индекса поиска Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Индексаторы в службе поиска Azure
> [!div class="op_single_selector"]
>
> * [Обзор](search-indexer-overview.md)
> * [Портал](search-import-data-portal.md)
> * [Azure SQL;](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Хранилище BLOB-объектов Azure](search-howto-indexing-azure-blob-storage.md)
> * [Хранилище таблиц Azure](search-howto-indexing-azure-tables.md)
>
>

**Индексатора** в поиске Azure робот, который извлекает данные с возможностью поиска и метаданные из внешнего источника данных и заполняет индекс основан на сопоставление поля к hello индекса и источника данных. Такой подход иногда бывает ссылка tooas «модель передачи по запросу», так как службы hello запрашивает данные в без необходимости toowrite любой код, который помещает индекс tooan данных.

Можно использовать индексатор как означает hello исключительно для приема данных или используйте сочетание методов, которые включают использование hello индексатора для загрузки только некоторые поля hello в индексе.

Вы можете запускать индексаторы по требованию или при регулярном обновлении данных, выполняемом каждые пятнадцать минут. Более частые обновления требуют использования модели отправки, выполняющей одновременное обновление данных в службе поиска Azure и источнике внешних данных.

## <a name="approaches-for-creating-and-managing-indexers"></a>Способы создания индексаторов и управления ими
Вы можете создавать общедоступные индексаторы (например, Azure SQL или Azure Cosmos DB), а также управлять ими, используя следующие средства:

* [Портал > мастер импорта данных;](search-get-started-portal.md)
* [API REST службы](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [Пакет SDK для .NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Основные этапы настройки
Индексаторы могут предложить функции, которые являются уникальными toohello источника данных. Поэтому тип индексатора будет определять особенности настройки источника данных или индексатора. Однако все индексаторы используют hello же основные композиции и требований. Шаги, общие tooall, индексаторы рассматриваются ниже.

### <a name="step-1-create-an-index"></a>Шаг 1. Создание индекса
Индексатор, который позволит автоматизировать некоторые задачи связанные toodata приема, но создание индекса не является одним из них. Перед началом работы у вас должен быть стандартный индекс с полями, которые соответствуют полям во внешнем источнике данных. Дополнительные сведения о структурировании индексатора см. в статье, посвященной [созданию индекса (с использованием REST API службы поиска Azure)](https://msdn.microsoft.com/library/azure/dn798941.aspx).

### <a name="step-2-create-a-data-source"></a>Шаг 2. Создание источника данных
Индексатор извлекает данные из **источника данных** , который содержит такие сведения, как строка подключения. В настоящее время поддерживаются следующие источники данных hello:

* [база данных Azure SQL (или SQL Server на виртуальных машинах Azure);](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [База данных Azure Cosmos](search-howto-index-documentdb.md)
* [Хранилище больших двоичных объектов Azure](search-howto-indexing-azure-blob-storage.md), используемого tooextract текста из документов PDF, Microsoft Office, HTML или XML
* [Хранилище таблиц Azure](search-howto-indexing-azure-tables.md)

Источники данных настраиваются и управляются независимо от индексаторы hello, использующие их, означающее, что источник данных может использоваться несколько индексаторов tooload более одного индекса одновременно.

### <a name="step-3create-and-schedule-hello-indexer"></a>Шаг 3: Создание и планирование индексатора hello
Определение индексатора Hello — это конструкция, указания индекса hello, источник данных и расписания. Индексатор, который может ссылаться источник данных от другой службы, при условии, что этот источник данных находится на hello одной подписке. Дополнительные сведения о структурировании индексатора см. в статье, посвященной [созданию индекса (с использованием REST API службы поиска Azure)](https://msdn.microsoft.com/library/azure/dn946899.aspx).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда основная идея hello hello следующий шаг — tooreview требования и тип источника данных конкретного tooeach задачи.

* [база данных Azure SQL (или SQL Server на виртуальных машинах Azure);](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [База данных Azure Cosmos](search-howto-index-documentdb.md)
* [Хранилище больших двоичных объектов Azure](search-howto-indexing-azure-blob-storage.md), используемого tooextract текста из документов PDF, Microsoft Office, HTML или XML
* [Хранилище таблиц Azure](search-howto-indexing-azure-tables.md)
* [Индексирование CSV BLOB-объектов с помощью индексатора hello больших двоичных объектов для поиска Azure](search-howto-index-csv-blobs.md)
* [Индексирование BLOB-объектов JSON с помощью индексатора BLOB-объектов службы поиска Azure](search-howto-index-json-blobs.md)
