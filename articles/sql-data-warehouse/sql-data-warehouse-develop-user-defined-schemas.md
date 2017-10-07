---
title: "определенные aaaUser схемы в хранилище данных SQL | Документы Microsoft"
description: "Советы по использованию схем Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Определяемые пользователем схемы в хранилище данных SQL
Традиционных хранилищах данных часто используйте отдельные базы данных toocreate границы приложения на основе рабочей нагрузки, домена или безопасности. Например, традиционное хранилище данных SQL Server может включать в себя промежуточную базу данных, базу данных хранилища данных и базы данных киоска данных. В этой топологии каждая база данных работает в качестве рабочей нагрузки и границы безопасности в архитектуре hello.

В отличие от этого хранилище данных SQL выполняется hello нагрузку хранилища данных в одной базе данных. Кроссплатформенные соединения баз данных не допускаются. Поэтому хранилище данных SQL ожидает, что все таблицы, используемые toobe хранилища hello, хранятся в одной базе данных hello.

> [!NOTE]
> Хранилище данных SQL не поддерживает какие-либо перекрестные запросы к базам данных. В результате реализации хранилища данных, использующие этот шаблон потребуется toobe внес изменения.
> 
> 

## <a name="recommendations"></a>Рекомендации
Ниже приведены рекомендации по консолидации границ рабочих нагрузок, безопасности, домена и функциональных границы с помощью определяемых пользователем схем.

1. Использовать один toorun базы данных хранилища данных SQL рабочей нагрузке хранилища данных
2. Консолидация вашей существующей среды toouse одно хранилище данных SQL базы данных хранилища данных
3. Использование **пользовательских схем** границ hello tooprovide ранее реализовано с помощью базы данных.

Если ранее определяемые пользователем схемы не использовалось, следует начать с нуля. Для пользовательских схем в базе данных хранилища данных SQL hello просто используйте hello старое имя базы данных в качестве основы hello.

Если же схемы уже использовались, у вас несколько вариантов:

1. Удалите имена прежних версий схем hello и начать заново
2. Сохранить имена hello прежних версий схем по имени таблицы toohello имя прежних версий схемы предварительно ожидающие hello
3. Сохранить имена прежних версий схем hello путем реализации представления над таблицей hello в дополнительных схем toore-создать hello старую структуру схемы.

> [!NOTE]
> На первой проверки вариант 3 может показаться наиболее привлекательный параметр hello. Однако hello devil будет подробно hello. Представления в хранилище данных SQL доступны только для чтения. Любые изменения данных или таблицы, должны toobe, выполняются для hello базовой таблицы. Кроме того, вариант 3 добавляет в систему уровень представлений. Может потребоваться toogive этого некоторые дополнительные размышления при использовании представления в архитектуре уже.
> 
> 

### <a name="examples"></a>Примеры:
Реализация определяемых пользователем схем на основе имен баз данных

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Сохранить прежних версий схемы назначает путем предварительно ожидающие их toohello имя таблицы. Используйте схемы для границ hello рабочей нагрузки.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Сохранение прежних имен схем с помощью представлений

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Любое изменение в стратегии схемы должен ознакомиться с моделью безопасности hello для hello базы данных. Во многих случаях может быть модель безопасности может toosimplify hello путем назначения разрешений на уровне схемы hello. Если требуются более детализированные разрешения, можно использовать роли базы данных.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
