---
title: "большие двоичные объекты aaaIndexing CSV с индексатор поиска Azure BLOB-объект | Документы Microsoft"
description: "Узнайте, как tooindex CSV большие двоичные объекты с поиском Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Индексирование BLOB-объектов в формате CSV с помощью индексатора BLOB-объектов службы поиска Azure
По умолчанию [индексатор BLOB-объектов службы поиска Azure](search-howto-indexing-azure-blob-storage.md) анализирует текстовые BLOB-объекты (с разделителями) как один блок текста. Однако с большими двоичными объектами, содержащий данные CSV-файла, часто требуется tootreat каждой строки в большом двоичном объекте hello в отдельном документе. Например данный hello следующие запятыми текст: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

может потребоваться tooparse его в двух документов каждого содержащий «id», «datePublished» и поля «теги».

В этой статье вы узнаете, как tooparse CSV большие двоичные объекты с индексатор поиска Azure BLOB-объектов. 

> [!IMPORTANT]
> Сейчас эта функциональность доступна в режиме предварительной версии. Он доступен только в версии API REST hello **2015-02-28-Preview**. Помните, что предварительные версии API предназначены для тестирования и ознакомления. Они не должны использоваться в рабочей среде. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Настройка индексирования CSV
tooindex CSV BLOB, создать или обновить определение индексатора с hello `delimitedText` синтаксический анализ режим:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Дополнительные сведения о hello создания API индексатора, ознакомьтесь с [Создание индексатора](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`Указывает, что первая строка (непустых) hello каждого BLOB-объекта содержит заголовки.
Если BLOB-объектов не содержат строку заголовка начальной, заголовки hello должно быть указано в конфигурации индексатора hello: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

В настоящее время поддерживается только кодировка UTF-8 hello. Кроме того, hello разделителями `','` знака поддерживается как разделитель hello. Если вам нужна поддержка других форматов кодирования или разделителей, сообщите нам об этом на [нашем сайте UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> При использовании разбора режим поиска Azure текста с разделителями hello предполагается, все большие двоичные объекты в источнике данных будет CSV. Если требуется toosupport сочетание CSV и других ТИПОВ больших двоичных объектов в hello же источника данных, дайте нам знать на [нашем сайте UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Примеры запросов
Говоря все вместе, ниже приведены примеры полных полезных данных hello. 

Источник данных: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Индексатор:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Помогите нам усовершенствовать службу поиска Azure
При наличии запросов компонентов или идеи об улучшениях, пожалуйста направляться toous на нашем [сайт UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

