---
title: "Создание интегрированных решений с помощью хранилища данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Интеграция других служб с хранилищем данных SQL
Помимо базовых возможностей, хранилище данных SQL позволяет пользователям дополнительно использовать многие другие службы в Azure.  В частности, мы приняли меры по глубокой интеграции со следующими службами:

* Power BI
* Фабрика данных Azure
* Машинное обучение Azure
* Azure Stream Analytics

Мы работаем над возможностями подключения к большему количеству служб в экосистеме Azure.

## <a name="power-bi"></a>Power BI
Интеграция с Power BI позволяет использовать вычислительные ресурсы хранилища данных SQL с возможностью создания динамических отчетов и визуализацией Power BI. На данный момент интеграция с Power BI включает:

* **Прямое соединение**: расширенное соединение с логической опорой на хранилище данных SQL.  Это обеспечивает более быстрый анализ в большем масштабе.
* **Открыть в Power BI**: кнопка "Открыть в Power BI" передает сведения об экземпляре в Power BI, повышая надежность соединения.

Дополнительные сведения см. в статье [Использование Power BI с хранилищем данных SQL](sql-data-warehouse-integrate-power-bi.md) или в [документации по Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx).

## <a name="azure-data-factory"></a>Фабрика данных Azure
Фабрика данных Azure предоставляет пользователям управляемую платформу для создания сложных конвейеров извлечения и загрузки.  Интеграция хранилища данных SQL с фабрикой данных Azure включает следующее.

* **Хранимые процедуры**: управление выполнением хранимых процедур в хранилище данных SQL.
* **Действие копирования.** Используйте ADF для перемещения данных в хранилище данных SQL.  В основе этой операции может использоваться стандартный механизм перемещения данных ADF или PolyBase. 

Дополнительные сведения см. в статье [Работа с фабрикой данных Azure и хранилищем данных SQL](sql-data-warehouse-integrate-azure-data-factory.md) или в [документации по фабрике данных Azure](https://azure.microsoft.com/documentation/services/data-factory/).

## <a name="azure-machine-learning"></a>Машинное обучение Azure
Машинное обучение Azure — это полностью управляемая аналитическая служба, позволяющая пользователям создавать сложные модели с использованием крупного набора прогнозируемых инструментов.  Хранилище данных SQL поддерживается в качестве источника и цели для этих моделей со следующими возможностями.

* **Чтение данных:** масштабное использование моделей с помощью T-SQL в хранилище данных SQL.
* **Запись данных:** применение изменений любой модели в хранилище данных SQL.

Дополнительные сведения см. в статье [Использование машинного обучения Azure с хранилищем данных SQL](sql-data-warehouse-integrate-azure-machine-learning.md) или в [документации по машинному обучению Azure](https://azure.microsoft.com/services/machine-learning/).

## <a name="azure-stream-analytics"></a>Azure Stream Analytics
Azure Stream Analytics — это сложная полностью управляемая инфраструктура для обработки и потребления данных о событиях, создаваемых концентратором событий Azure.  Интеграция с хранилищем данных SQL обеспечивает эффективную обработку и хранение потоковых данных наряду с реляционными данными, предоставляя более глубокий и расширенный анализ.  

* **Выходные данные заданий:** отправка выходных данных заданий Stream Analytics напрямую в хранилище данных SQL.

Дополнительные сведения см. в статье [Работа со службой Azure Stream Analytics и хранилищем данных SQL](sql-data-warehouse-integrate-azure-stream-analytics.md) или в [документации по Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/).

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
