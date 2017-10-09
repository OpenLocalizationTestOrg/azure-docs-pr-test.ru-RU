---
title: "aaaData передачи в поиске Azure | Документы Microsoft"
description: "Узнайте, как tooan tooupload данных индекса в поиске Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Отправка данных tooAzure поиска
> [!div class="op_single_selector"]
> * [Обзор](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Существует два способа toopopulate индекса со сжатием данных. Первый вариант Hello вручную внедряет данные в индекс hello hello поиска Azure с помощью [API-интерфейса REST](search-import-data-rest-api.md) или [.NET SDK](search-import-data-dotnet.md). второй вариант Hello — слишком[указать источник данных, поддерживаемые](search-indexer-overview.md) tooyour индекса и позволяет автоматически получать данные hello поиска Azure.

## <a name="push-data-tooan-index"></a>Индекс tooan принудительной данных
Этот подход ссылается tooprogrammatically отправки вашего toomake поиска данных tooAzure его доступным для поиска. Для приложений, имеющих требования к очень низкой задержкой (например, если требуется поиска toobe операций синхронизации с базами данных динамических инвентаризации) модель принудительной отправки hello является единственным вариантом.

Можно использовать hello [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) или [.NET SDK](search-import-data-dotnet.md) индекс tooan toopush данных. В настоящее время не поддерживается средство для проталкивания данных через портал hello.

Этот подход является более гибким, чем модель по запросу hello, поскольку можно загружать документы по отдельности или в виде пакетов (копирование too1000 каждого пакета и 16 МБ любого из этих идет первой). Принудительная модель Hello также позволяет tooAzure документы tooupload поиска независимо от того, где данные.

формат данных Hello воспринимает поиска Azure, JSON, а все документы в наборе данных hello должны иметь поля, которые сопоставляют toofields, определенных в схеме индекса. 

## <a name="pull-data-into-an-index"></a>Извлечение данных в индекс
модель извлечения Hello сканирование поддерживаемый источник данных и автоматически отправляет данные hello в индекс. Служба поиска Azure реализует эту возможность с помощью *индексаторов*, которые сейчас доступны для [хранилища BLOB-объектов](search-howto-indexing-azure-blob-storage.md), [хранилища таблиц](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [базы данных SQL Azure и SQL Server на виртуальных машинах Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Индексаторы подключиться к источнику индекс tooa данных (обычно таблицы, представления или эквивалентная структура), а также сопоставить исходные поля tooequivalent поля в индексе hello. Во время выполнения hello набора строк является автоматически преобразованный tooJSON и загружается в hello указанному индексу. Все индексаторы поддерживает планирования, можно указать, как часто данные hello — toobe обновления. Большинство Индексаторы обеспечивают отслеживания изменений, если источник данных hello поддерживает его. Отслеживание изменений и удаления tooexisting документы Кроме toorecognizing новый, индексаторы удалите hello необходимость tooactively управления данными hello в индексе. 

Индексатор функциональность предоставляется в hello [портал Azure](search-import-data-portal.md), hello [API-интерфейса REST](/rest/api/searchservice/Indexer-operations)и hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Преимущества toousing hello портал — что поиска Azure позволяет обычно создать схему индекса по умолчанию к путем чтения метаданных hello hello исходный набор данных. Вы можете изменить hello указателя до обработки индекса hello, после которого hello только изменения схемы допускается являются те, которые не требуют повторного индексирования. Если hello изменения toomake влияние hello схемы напрямую, потребуется toorebuild hello индекса. 

После заполнения индекса hello, можно использовать **обозреватель поиска** панели команд портала hello в качестве проверки.

## <a name="query-an-index-using-search-explorer"></a>Создание запроса к индексу с помощью проводника поиска

Быстро tooperform предварительная проверка на загрузку документа hello — toouse **обозреватель поиска** hello портала. обозреватель Hello позволяет запроса индекса без необходимости toowrite любого кода. Hello поисковый интерфейс основан на параметры по умолчанию, такие как hello [простой синтаксис](/rest/api/searchservice/simple-query-syntax-in-azure-search) и значение по умолчанию [параметр запроса поиска searchMode](/rest/api/searchservice/search-documents). Результаты возвращаются в формате JSON, чтобы можно было просмотреть hello весь документ.

> [!TIP]
> Многочисленные [образцы кода для поиска Azure](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) включить внедренный или доступны наборы данных предлагает простой способ tooget работы. портал Hello также предоставляет образец индексатора и источника данных, состоящий из набора небольших недвижимости (с именем «объем отображаемой us пример»). При запуске индексатора предварительно настроенных hello на hello образец источника данных, индекс создается и загружается с документами, которые затем могут быть запрошены в обозреватель поиска или код, написанный.
