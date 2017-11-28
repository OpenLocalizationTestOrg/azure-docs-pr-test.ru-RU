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
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="8e3cd-103">Динамический SQL в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="8e3cd-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="8e3cd-104">При разработке кода приложения для хранилища данных SQL, вы можете требуется toohelp toouse динамического sql предоставляют гибкие, универсальных и модульные решения.</span><span class="sxs-lookup"><span data-stu-id="8e3cd-104">When developing application code for SQL Data Warehouse you may need toouse dynamic sql toohelp deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="8e3cd-105">На данный момент хранилище данных SQL не поддерживает двоичные типы данных.</span><span class="sxs-lookup"><span data-stu-id="8e3cd-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="8e3cd-106">Это может ограничивать hello размер строк как типов больших двоичных объектов включают в себя типы varchar(max) и nvarchar(max).</span><span class="sxs-lookup"><span data-stu-id="8e3cd-106">This may limit hello size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="8e3cd-107">При использовании этих типов в коде приложения при создании очень больших строк, необходимо будет toobreak кода hello в блоки и инструкции EXEC hello используйте вместо этого.</span><span class="sxs-lookup"><span data-stu-id="8e3cd-107">If you have used these types in your application code when building very large strings, you will need toobreak hello code into chunks and use hello EXEC statement instead.</span></span>

<span data-ttu-id="8e3cd-108">Вот простой пример:</span><span class="sxs-lookup"><span data-stu-id="8e3cd-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="8e3cd-109">При коротком строку hello можно использовать [sp_executesql] [ sp_executesql] в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="8e3cd-109">If hello string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="8e3cd-110">Выполнение динамических SQL операторов по-прежнему будут правила проверки TSQL tooall субъекта.</span><span class="sxs-lookup"><span data-stu-id="8e3cd-110">Statements executed as dynamic SQL will still be subject tooall TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8e3cd-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e3cd-111">Next steps</span></span>
<span data-ttu-id="8e3cd-112">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="8e3cd-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
