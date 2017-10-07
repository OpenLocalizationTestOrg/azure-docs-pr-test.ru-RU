---
title: "aaaUse фабрики данных Azure с хранилищем данных SQL | Документы Microsoft"
description: "Советы по использованию фабрики данных Azure (ADF) с хранилищем данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Работа с фабрикой данных Azure и хранилищем данных SQL
Фабрика данных Azure предоставляет полностью управляемого метода для обеспечения взаимодействия hello передачу данных и выполнения хранимых процедур в хранилище данных SQL.  Это позволит вам toomore легко настроить расписание сложных извлечения, преобразования и загрузки (ETL) процедуры и с хранилищем данных SQL. Более полный обзор фабрики данных Azure см. в разделе hello [документации фабрики данных Azure][Azure Data Factory documentation].

## <a name="data-movement"></a>Перемещение данных
Фабрика Azure данных обеспечивает перемещение данных между локальными источниками и различными службами Azure.  Интеграция с общей, текущее с фабрикой данных Azure поддерживает tooand перемещения данных из hello следующих элементов:

* Хранилище blob-объектов Azure
* База данных SQL Azure
* Локальный сервер SQL Server
* Сервер SQL Server в IaaS

Сведения о как действие копирования tooset копирование данных в разделе [копирование данных с помощью фабрики данных Azure][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Хранимые процедуры
 В hello таким же, каким образом его можно использовать передачу данных tooschedule, фабрики данных Azure может также быть используется tooorchestrate hello выполнение хранимых процедур.  Это позволяет более сложные toobe конвейеры создан и расширяет фабрики данных Azure возможность tooleverage hello вычислительные возможности хранилища данных SQL.

## <a name="next-steps"></a>Дальнейшие действия
Общие сведения об интеграции см. в статье [Интеграция других служб с хранилищем данных SQL][SQL Data Warehouse integration overview].
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

