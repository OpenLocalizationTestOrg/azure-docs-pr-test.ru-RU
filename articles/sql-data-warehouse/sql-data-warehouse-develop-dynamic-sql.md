---
title: "aaaDynamic SQL в хранилище данных SQL | Документы Microsoft"
description: "Рекомендации по использованию динамического SQL в хранилище данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>Динамический SQL в хранилище данных SQL
При разработке кода приложения для хранилища данных SQL, вы можете требуется toohelp toouse динамического sql предоставляют гибкие, универсальных и модульные решения. На данный момент хранилище данных SQL не поддерживает двоичные типы данных. Это может ограничивать hello размер строк как типов больших двоичных объектов включают в себя типы varchar(max) и nvarchar(max). При использовании этих типов в коде приложения при создании очень больших строк, необходимо будет toobreak кода hello в блоки и инструкции EXEC hello используйте вместо этого.

Вот простой пример:

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

При коротком строку hello можно использовать [sp_executesql] [ sp_executesql] в обычном режиме.

> [!NOTE]
> Выполнение динамических SQL операторов по-прежнему будут правила проверки TSQL tooall субъекта.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
