---
title: "aaaMigrate tooSQL вашего решения хранилища данных | Документы Microsoft"
description: "Руководство по миграции для переноса вашей платформы решения tooAzure хранилище данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Перенос вашего решения tooAzure хранилище данных SQL
См. что происходит при переносе существующего tooAzure решения базы данных хранилища данных SQL. 

## <a name="profile-your-workload"></a>Профилирование рабочей нагрузки
Перед миграцией необходимо toobe уверенности, что хранилище данных SQL — hello подходящее решение для рабочей нагрузки. Хранилище данных SQL — это распределенная система, предназначенная tooperform анализ больших объемов данных.  Миграция tooSQL хранилища данных требуется некоторые изменения структуры, не слишком жесткие toounderstand, но может занять некоторое время tooimplement. Если компании требуется хранилище данных корпоративного уровня, преимущества hello заслуживают hello усилий. Однако если не требуется power hello хранилища данных SQL, это более экономичное toouse SQL Server или база данных SQL Azure.

Рассмотрите возможность использования хранилища данных SQL, если вы:
- обслуживаете один или нескольких терабайтов данных;
- Анализ плана toorun больших объемов данных
- Требуется hello возможность tooscale вычислений и хранения 
- Необходимо toosave расходы из-за приостановки вычислительные ресурсы, если они не нужны.

Не используйте хранилище данных SQL для операционных рабочих нагрузок (OLTP) со следующими характеристиками:
- высокая частота операций чтения и записи;
- большое число операций одноэлементной выборки;
- большие объемы операций вставки одной строки;
- необходимость построчной обработки;
- несовместимые форматы (JSON, XML).


## <a name="plan-hello-migration"></a>Планирование миграции hello

После выбора toomigrate tooSQL существующие решения хранилища данных, это миграции hello важные tooplan перед началом работы. 

Одна из целей планирования является tooensure данные схемы таблицы, и ваш код совместимы с хранилищем данных SQL. Существуют некоторые различия совместимости toowork вокруг между текущей системы и хранилище данных SQL. Кроме того переноса больших объемов данных tooAzure занимает время. Тщательное планирование упростит начало вашей tooAzure данных. 

Планирование другой целью является toomake конструирования tooensure корректировки, которые решение использует преимущества hello высокую производительность запросов, хранилище данных SQL — предназначены tooprovide. Проектирование хранилищ данных для масштабирования представлены шаблоны другую структуру и поэтому традиционных подходов не всегда hello наилучшим образом. Несмотря на то, что после миграции можно внести некоторые изменения проектирования, изменения раньше в процессе hello будет сэкономить время в дальнейшем.

tooperform успешной миграции, необходимо toomigrate таблицы схемы, кода и данных. Рекомендации по этим аспектам переноса можно изучить, воспользовавшись ссылками ниже:

-  [Перенос схем](sql-data-warehouse-migrate-schema.md)
-  [Перенос кода](sql-data-warehouse-migrate-code.md)
-  [Перенос данных](sql-data-warehouse-migrate-data.md) 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Дальнейшие действия
также Hello CAT (группа консультантов по) имеет некоторые значительные руководство хранилище данных SQL, в котором они будут публиковать через блоги.  Рассмотрим их статьи [tooAzure перенос данных хранилища данных SQL на практике] [ Migrating data tooAzure SQL Data Warehouse in practice] Дополнительные рекомендации по миграции.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
