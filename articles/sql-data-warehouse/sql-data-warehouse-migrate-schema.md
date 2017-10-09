---
title: "aaaMigrate tooSQL к схеме хранилища данных | Документы Microsoft"
description: "Советы по переносу tooAzure вашей схемы хранилища данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Перенос вашей tooSQL схемы хранилища данных
Рекомендации по переносу вашей tooSQL схем SQL хранилища данных. 

## <a name="plan-your-schema-migration"></a>Планирование переноса схемы

При планировании миграции в разделе hello [Общие сведения о таблицах] [ table overview] toobecome знакомы таблицы вопросы проектирования, таких как статистика распределения, секционирования и индексирование.  В нем также рассматриваются некоторые [неподдерживаемые функции таблиц][unsupported table features] и способы их обойти.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Использовать базы данных tooconsolidate пользовательских схем

Ваша текущая рабочая нагрузка, вероятно, использует более одной базы данных. Например, хранилище данных SQL Server может включать в себя промежуточную базу данных, базу данных хранилища данных и базы данных киоска данных. В этой топологии на каждой базе данных выполняется отдельная рабочая нагрузка с собственными политиками безопасности.

В отличие от этого хранилище данных SQL выполняется hello нагрузку хранилища данных в одной базе данных. Кроссплатформенные соединения баз данных не допускаются. Таким образом хранилище данных SQL ожидает, что все таблицы, используемые toobe хранилища данных hello, хранятся в одной базе данных hello.

Мы рекомендуем использовать пользовательских схем tooconsolidate вашей текущей рабочей нагрузки в одну базу данных. Примеры см. в разделе [Пользовательские схемы](sql-data-warehouse-develop-user-defined-schemas.md).

## <a name="use-compatible-data-types"></a>Использование совместимых типов данных
Измените ваш toobe типы данных, совместимый с хранилищем данных SQL. Список поддерживаемых и неподдерживаемых типов данных см. в разделе [о типах данных][data types]. Этот раздел предоставляет обходные пути для типов hello не поддерживается. Он также предоставляет запрос tooidentify существующие типы, которые не поддерживаются в хранилище данных SQL.

## <a name="minimize-row-size"></a>Сведение к минимуму длины строки
Для повышения производительности рекомендуется свести к минимуму hello длина строки таблицы. Так как более короткие длины строк привести toobetter производительности, используете типы данных наименьшее hello, которые работают для данных. 

Для ширины строки таблицы в PolyBase действует ограничение в 1 МБ.  Если планируется tooload данных в хранилище данных SQL с помощью PolyBase, обновите ширина максимальной строка таблицы toohave меньше 1 МБ. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Укажите параметр распространения hello
Хранилище данных SQL — это система управления распределенными базами данных. Каждая таблица распределения или реплицировать по hello вычислительных узлов. Отсутствует параметр, позволяющий указать, каким образом toodistribute hello данных. варианты Hello реплицируются циклический перебор, или распределенные хэш. У каждого варианта есть преимущества и недостатки. Если не указать параметр распространения hello, хранилище данных SQL будет использовать циклический перебор по умолчанию hello.

- Циклический перебор — по умолчанию hello. Это простейший toouse hello и загружает данные hello максимально возможной скоростью, но соединения потребуется перемещение данных, что снижает производительность запросов.
- Хранит реплицированные копии таблицы hello на каждом вычислительном узле. Реплицированные таблицы являются высокопроизводительных, так как они не требуют перемещения данных для операций соединения и агрегирования. Для них требуется дополнительное место в хранилище, поэтому этот тип распределения лучше всего подходит для небольших таблиц.
- Хэш распределенных распределяет hello строк по всем узлам hello через хэш-функции. Распределенных хэш-таблицы являются основой hello хранилище данных SQL, поскольку они являются спроектированный tooprovide высокую производительность запросов в больших таблицах. Этот параметр требует некоторых планирования tooselect hello столбец лучше всего на какие данные toodistribute hello. Тем не менее если не выбрать лучший столбца hello hello первый раз, можно легко повторно распространять hello данные на другой столбец. 

toochoose hello распространения оптимальным для каждой таблицы в статье [распределенных таблиц](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Дальнейшие действия
Вы успешно перенесли вашей tooSQL схемы базы данных хранилища данных, откройте tooone из hello в следующих статьях:

* [Перенос данных][Migrate your data]
* [Перенос кода][Migrate your code]

Дополнительные сведения о хранилище данных SQL советы и рекомендации см. в разделе hello [рекомендации] [ best practices] статьи.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
