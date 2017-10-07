---
title: "Учебник глобального распространения Cosmos DB aaaAzure для таблицы API | Документы Microsoft"
description: "Узнайте, как toosetup Azure Cosmos DB глобального распространителя с помощью hello API таблиц."
services: cosmos-db
keywords: "глобальное распределение, таблица"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>Как toosetup Azure Cosmos DB глобального распространителя с помощью hello API таблиц

В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью hello API таблиц (Предварительная версия).

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello [API таблиц](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Подключение tooa предпочтительную область с помощью hello API таблиц

В порядке tootake преимуществами [глобального распространения](distribute-data-globally.md), клиентских приложений можно указать hello упорядоченный список предпочтения toobe области используется tooperform операции с документом. Это можно сделать путем установки hello `TablePreferredLocations` значение конфигурации в файле конфигурации приложения hello для предварительного просмотра hello пакет SDK хранилища Azure. В зависимости от конфигурации учетной записи Azure Cosmos DB hello текущий язык доступности указан, список предпочтения hello приветствия большинство оптимальной конечной точки будет выбрана по tooperform пакет SDK хранилища Azure hello записи и операций чтения.

Hello `TablePreferredLocations` должен содержать список разделенных запятыми предпочтительный расположения (множественной адресацией) для операций чтения. Каждый экземпляр клиента можно указать подмножество этих областей в порядке hello предпочтительный для операций чтения с небольшой задержкой. Hello областей должны иметь имена с помощью их [отображаемые имена](https://msdn.microsoft.com/library/azure/gg441293.aspx), например `West US`.

Все операции чтения будут передаваться первой доступной области toohello hello `TablePreferredLocations` списка. Если hello запрос завершается неудачно, клиент hello ошибкой вниз область Далее toohello списка hello и так далее.

Hello SDK предпринимает попытку tooread из регионов hello, указанный в `TablePreferredLocations`. Таким образом, например, hello учетной записи базы данных доступен в трех регионах, когда клиент hello только задает два hello записи областей для `TablePreferredLocations`, то никаких операций чтения будет обслуживается hello записи области, даже в случае hello перехода на другой ресурс.

пакет SDK для Hello будет автоматически отправлять все записи toohello текущей записи области.

Если hello `TablePreferredLocations` свойство не задано, все запросы будут поступать из hello текущей записи области.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

На этом руководство завершено. Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md). Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB

Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.

> [!div class="nextstepaction"]
> [Разрабатывать локально в эмуляторе hello](local-emulator.md)
