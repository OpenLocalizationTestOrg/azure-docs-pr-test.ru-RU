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
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="b880a-103">Работа с фабрикой данных Azure и хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="b880a-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="b880a-104">Фабрика данных Azure предоставляет полностью управляемого метода для обеспечения взаимодействия hello передачу данных и выполнения хранимых процедур в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b880a-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="b880a-105">Это позволит вам toomore легко настроить расписание сложных извлечения, преобразования и загрузки (ETL) процедуры и с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b880a-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="b880a-106">Более полный обзор фабрики данных Azure см. в разделе hello [документации фабрики данных Azure][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="b880a-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="b880a-107">Перемещение данных</span><span class="sxs-lookup"><span data-stu-id="b880a-107">Data Movement</span></span>
<span data-ttu-id="b880a-108">Фабрика Azure данных обеспечивает перемещение данных между локальными источниками и различными службами Azure.</span><span class="sxs-lookup"><span data-stu-id="b880a-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="b880a-109">Интеграция с общей, текущее с фабрикой данных Azure поддерживает tooand перемещения данных из hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b880a-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="b880a-110">Хранилище blob-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="b880a-110">Azure blob storage</span></span>
* <span data-ttu-id="b880a-111">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b880a-111">Azure SQL Database</span></span>
* <span data-ttu-id="b880a-112">Локальный сервер SQL Server</span><span class="sxs-lookup"><span data-stu-id="b880a-112">On-premises SQL Server</span></span>
* <span data-ttu-id="b880a-113">Сервер SQL Server в IaaS</span><span class="sxs-lookup"><span data-stu-id="b880a-113">SQL Server on IaaS</span></span>

<span data-ttu-id="b880a-114">Сведения о как действие копирования tooset копирование данных в разделе [копирование данных с помощью фабрики данных Azure][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="b880a-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="b880a-115">Хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="b880a-115">Stored Procedures</span></span>
 <span data-ttu-id="b880a-116">В hello таким же, каким образом его можно использовать передачу данных tooschedule, фабрики данных Azure может также быть используется tooorchestrate hello выполнение хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="b880a-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="b880a-117">Это позволяет более сложные toobe конвейеры создан и расширяет фабрики данных Azure возможность tooleverage hello вычислительные возможности хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b880a-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b880a-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b880a-118">Next steps</span></span>
<span data-ttu-id="b880a-119">Общие сведения об интеграции см. в статье [Интеграция других служб с хранилищем данных SQL][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="b880a-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="b880a-120">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="b880a-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

