---
title: "aaaBuild интегрированных решений с хранилищем данных SQL | Документы Microsoft"
description: "Инструменты и партнерские решения, которые интегрируются с хранилищем данных SQL "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Интеграция других служб с хранилищем данных SQL
В дополнение к этому tooits основные функциональные возможности, хранилище данных SQL позволяет пользователям tooleverage многие hello другие службы в Azure, наряду с его.  В частности в настоящее время перешли toodeeply интегрировать hello следующие действия:

* Power BI
* Фабрика данных Azure
* Машинное обучение Azure
* Azure Stream Analytics

Мы активно работаем над tooconnect с дополнительные службы по hello Azure экосистемы.

## <a name="power-bi"></a>Power BI
Интеграция с Power BI позволяет tooleverage hello вычислительной мощности хранилища данных SQL с hello динамические отчеты и визуализации Power BI. На данный момент интеграция с Power BI включает:

* **Прямое соединение**: расширенное соединение с логической опорой на хранилище данных SQL.  Это обеспечивает более быстрый анализ в большем масштабе.
* **Открыть в Power BI**: кнопка «Открыть в Power BI» hello передает экземпляр сведения tooPower бизнес-Аналитики, что обеспечивает более эффективное подключение.

В разделе [интеграция с Power BI](sql-data-warehouse-integrate-power-bi.md) или hello [документации по Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) для получения дополнительной информации.

## <a name="azure-data-factory"></a>Фабрика данных Azure
Фабрика данных Azure предоставляет пользователям toocreate управляемой платформы, которые конвейеров сложных извлечения и загрузки.  Интеграция хранилища данных SQL с фабрикой данных Azure включает hello следующее:

* **Хранимые процедуры**: координировать hello выполнение хранимых процедур в хранилище данных SQL.
* **Копировать**: используйте ADF toomove данных в хранилище данных SQL.  Эта операция может использовать механизм перемещения ADF стандартные данные или охватывает PolyBase под hello. 

В разделе [интеграция с фабрикой данных Azure](sql-data-warehouse-integrate-azure-data-factory.md) или hello [фабрики данных Azure документации](https://azure.microsoft.com/documentation/services/data-factory/) для получения дополнительной информации.

## <a name="azure-machine-learning"></a>Машинное обучение Azure
Машинное обучение Azure — это служба полностью управляемая аналитика, что дает возможность пользователям toocreate сложные модели, используя большого набора средств для прогнозирующего.  Хранилище данных SQL поддерживается в качестве источника и назначения для этих моделей с hello следующие функциональные возможности:

* **Чтение данных:** масштабное использование моделей с помощью T-SQL в хранилище данных SQL.
* **Записи данных:** фиксации изменений из любой модели обратно tooSQL хранилища данных.

В разделе [интеграция с машинного обучения Azure](sql-data-warehouse-integrate-azure-machine-learning.md) или hello [документации машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) для получения дополнительной информации.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics
Azure Stream Analytics — это сложная полностью управляемая инфраструктура для обработки и потребления данных о событиях, создаваемых концентратором событий Azure.  Интеграция с хранилищем данных SQL поддерживает потоковую передачу данных toobe эффективно обрабатываются и хранятся вместе с реляционных данных. Это позволяет более глубокого более расширенного анализа.  

* **Выходные данные задания:** отправки выходных данных Stream Analytics непосредственно заданий tooSQL хранилища данных.

В разделе [интеграция с Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) или hello [документации Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) для получения дополнительной информации.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
