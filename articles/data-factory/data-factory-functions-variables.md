---
title: "aaaData функции фабрики и системные переменные | Документы Microsoft"
description: "Содержит список функций и системных переменных фабрики данных Azure."
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="8b861-103">Фабрика данных Azure — функции и системные переменные</span><span class="sxs-lookup"><span data-stu-id="8b861-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="8b861-104">В этой статье содержатся сведения о функциях и переменных, поддерживаемых фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="8b861-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="8b861-105">Системные переменные фабрики данных</span><span class="sxs-lookup"><span data-stu-id="8b861-105">Data Factory system variables</span></span>
| <span data-ttu-id="8b861-106">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="8b861-106">Variable Name</span></span> | <span data-ttu-id="8b861-107">Описание</span><span class="sxs-lookup"><span data-stu-id="8b861-107">Description</span></span> | <span data-ttu-id="8b861-108">Область объекта</span><span class="sxs-lookup"><span data-stu-id="8b861-108">Object Scope</span></span> | <span data-ttu-id="8b861-109">Область JSON и примеры использования</span><span class="sxs-lookup"><span data-stu-id="8b861-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b861-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="8b861-110">WindowStart</span></span> |<span data-ttu-id="8b861-111">Начало интервала времени для текущего окна запуска действия.</span><span class="sxs-lookup"><span data-stu-id="8b861-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="8b861-112">действие</span><span class="sxs-lookup"><span data-stu-id="8b861-112">activity</span></span> |<ol><li><span data-ttu-id="8b861-113">Укажите запросы на выбор данных.</span><span class="sxs-lookup"><span data-stu-id="8b861-113">Specify data selection queries.</span></span> <span data-ttu-id="8b861-114">См. в статьях соединитель, на которые ссылается hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="8b861-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="8b861-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="8b861-115">WindowEnd</span></span> |<span data-ttu-id="8b861-116">Конец интервала времени для текущего окна запуска действия.</span><span class="sxs-lookup"><span data-stu-id="8b861-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="8b861-117">действие</span><span class="sxs-lookup"><span data-stu-id="8b861-117">activity</span></span> |<span data-ttu-id="8b861-118">то же, что и WindowStart.</span><span class="sxs-lookup"><span data-stu-id="8b861-118">same as WindowStart.</span></span> |
| <span data-ttu-id="8b861-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="8b861-119">SliceStart</span></span> |<span data-ttu-id="8b861-120">Начало интервала времени для формируемого среза данных.</span><span class="sxs-lookup"><span data-stu-id="8b861-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="8b861-121">действие</span><span class="sxs-lookup"><span data-stu-id="8b861-121">activity</span></span><br/><span data-ttu-id="8b861-122">набор данных</span><span class="sxs-lookup"><span data-stu-id="8b861-122">dataset</span></span> |<ol><li><span data-ttu-id="8b861-123">Укажите динамические пути к папкам и имена файлов при работе с [большими двоичными объектами Azure](data-factory-azure-blob-connector.md) и [наборами данных файловой системы](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8b861-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="8b861-124">Укажите входные зависимости с помощью функций фабрики данных в коллекции входных данных действия.</span><span class="sxs-lookup"><span data-stu-id="8b861-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="8b861-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="8b861-125">SliceEnd</span></span> |<span data-ttu-id="8b861-126">Конец интервала времени для текущего среза данных.</span><span class="sxs-lookup"><span data-stu-id="8b861-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="8b861-127">действие</span><span class="sxs-lookup"><span data-stu-id="8b861-127">activity</span></span><br/><span data-ttu-id="8b861-128">dataset</span><span class="sxs-lookup"><span data-stu-id="8b861-128">dataset</span></span> |<span data-ttu-id="8b861-129">То же, что и для SliceStart.</span><span class="sxs-lookup"><span data-stu-id="8b861-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="8b861-130">В настоящее время фабрики данных требует, что hello запланировать hello указано в действие точно соответствует hello расписанием, заданным в доступности hello выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="8b861-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="8b861-131">Таким образом, WindowStart, WindowEnd, а также SliceStart и SliceEnd всегда сопоставляйте toohello одновременную период и один выходной среза.</span><span class="sxs-lookup"><span data-stu-id="8b861-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="8b861-132">Пример использования системной переменной</span><span class="sxs-lookup"><span data-stu-id="8b861-132">Example for using a system variable</span></span>
<span data-ttu-id="8b861-133">В следующий пример, год, месяц, день и время hello **SliceStart** извлекаются в отдельные переменные, которые используются в **folderPath** и **fileName** свойства.</span><span class="sxs-lookup"><span data-stu-id="8b861-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="8b861-134">Функции фабрики данных</span><span class="sxs-lookup"><span data-stu-id="8b861-134">Data Factory functions</span></span>
<span data-ttu-id="8b861-135">Можно использовать функции в фабрике данных, а также системные переменные для hello следующих целей:</span><span class="sxs-lookup"><span data-stu-id="8b861-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="8b861-136">Указание запросов для выбора данных (см. в статьях соединителя ссылается hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="8b861-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="8b861-137">Здравствуйте, tooinvoke синтаксис функции фабрики данных —:  **$$ <function>**  запросы выбора данных и других свойств в действие hello и наборах данных.</span><span class="sxs-lookup"><span data-stu-id="8b861-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="8b861-138">Указание входных зависимостей с помощью функций фабрики данных в коллекции входных данных действия.</span><span class="sxs-lookup"><span data-stu-id="8b861-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="8b861-139">Префикс $$ не требуется при указании выражений входных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="8b861-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="8b861-140">В следующий пример hello **sqlReaderQuery** в файле JSON присваивается значение tooa, возвращенное hello `Text.Format` функции.</span><span class="sxs-lookup"><span data-stu-id="8b861-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="8b861-141">В этом примере также используется системная переменная с именем **WindowStart**, который представляет hello время начала действия hello, выполните в окне.</span><span class="sxs-lookup"><span data-stu-id="8b861-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="8b861-142">В разделе [Строки настраиваемых форматов даты и времени](https://msdn.microsoft.com/library/8kb3ddd4.aspx) описаны различные варианты форматирования, которые можно использовать (пример: гг и гггг).</span><span class="sxs-lookup"><span data-stu-id="8b861-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="8b861-143">Функции</span><span class="sxs-lookup"><span data-stu-id="8b861-143">Functions</span></span>
<span data-ttu-id="8b861-144">Hello в следующей таблице перечислены все функции hello в фабрике данных Azure:</span><span class="sxs-lookup"><span data-stu-id="8b861-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="8b861-145">Категория</span><span class="sxs-lookup"><span data-stu-id="8b861-145">Category</span></span> | <span data-ttu-id="8b861-146">Функция</span><span class="sxs-lookup"><span data-stu-id="8b861-146">Function</span></span> | <span data-ttu-id="8b861-147">Параметры</span><span class="sxs-lookup"><span data-stu-id="8b861-147">Parameters</span></span> | <span data-ttu-id="8b861-148">Описание</span><span class="sxs-lookup"><span data-stu-id="8b861-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b861-149">Время</span><span class="sxs-lookup"><span data-stu-id="8b861-149">Time</span></span> |<span data-ttu-id="8b861-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-150">AddHours(X,Y)</span></span> |<span data-ttu-id="8b861-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="8b861-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-152">Y: int</span></span> |<span data-ttu-id="8b861-153">Добавляет Y часов toohello заданному времени X.</span><span class="sxs-lookup"><span data-stu-id="8b861-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="8b861-154">Пример: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="8b861-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="8b861-155">Время</span><span class="sxs-lookup"><span data-stu-id="8b861-155">Time</span></span> |<span data-ttu-id="8b861-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="8b861-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="8b861-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-158">Y: int</span></span> |<span data-ttu-id="8b861-159">Добавляет Y минут tooX.</span><span class="sxs-lookup"><span data-stu-id="8b861-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="8b861-160">Пример: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="8b861-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="8b861-161">Время</span><span class="sxs-lookup"><span data-stu-id="8b861-161">Time</span></span> |<span data-ttu-id="8b861-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-162">StartOfHour(X)</span></span> |<span data-ttu-id="8b861-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-163">X: Datetime</span></span> |<span data-ttu-id="8b861-164">Возвращает hello время начала для часа hello, представленного компонентом часа hello X.</span><span class="sxs-lookup"><span data-stu-id="8b861-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="8b861-165">Пример: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="8b861-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="8b861-166">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-166">Date</span></span> |<span data-ttu-id="8b861-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-167">AddDays(X,Y)</span></span> |<span data-ttu-id="8b861-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-168">X: DateTime</span></span><br/><br/><span data-ttu-id="8b861-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-169">Y: int</span></span> |<span data-ttu-id="8b861-170">Добавляет Y дней tooX.</span><span class="sxs-lookup"><span data-stu-id="8b861-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="8b861-171">Пример: 15.09.2013 12:00:00 + 2 дня = 17.09.2013 12:00:00.</span><span class="sxs-lookup"><span data-stu-id="8b861-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="8b861-172">Можно также вычитать дни, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="8b861-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="8b861-173">Пример: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="8b861-174">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-174">Date</span></span> |<span data-ttu-id="8b861-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="8b861-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-176">X: DateTime</span></span><br/><br/><span data-ttu-id="8b861-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-177">Y: int</span></span> |<span data-ttu-id="8b861-178">Добавляет Y месяцев tooX.</span><span class="sxs-lookup"><span data-stu-id="8b861-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="8b861-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="8b861-180">Можно также вычитать месяцы, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="8b861-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="8b861-181">Пример: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="8b861-182">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-182">Date</span></span> |<span data-ttu-id="8b861-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="8b861-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="8b861-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-185">Y: int</span></span> |<span data-ttu-id="8b861-186">Добавляет Y * 3 месяца tooX.</span><span class="sxs-lookup"><span data-stu-id="8b861-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="8b861-187">Пример: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="8b861-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="8b861-188">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-188">Date</span></span> |<span data-ttu-id="8b861-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="8b861-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-190">X: DateTime</span></span><br/><br/><span data-ttu-id="8b861-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-191">Y: int</span></span> |<span data-ttu-id="8b861-192">Добавляет Y * 7 дней tooX</span><span class="sxs-lookup"><span data-stu-id="8b861-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="8b861-193">Пример: 15.09.2013 12:00:00 + 1 неделя = 22.09.2013 12:00:00.</span><span class="sxs-lookup"><span data-stu-id="8b861-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="8b861-194">Можно также вычитать недели, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="8b861-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="8b861-195">Пример: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="8b861-196">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-196">Date</span></span> |<span data-ttu-id="8b861-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="8b861-197">AddYears(X,Y)</span></span> |<span data-ttu-id="8b861-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-198">X: DateTime</span></span><br/><br/><span data-ttu-id="8b861-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="8b861-199">Y: int</span></span> |<span data-ttu-id="8b861-200">Добавляет Y лет tooX.</span><span class="sxs-lookup"><span data-stu-id="8b861-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="8b861-201">Можно также вычитать года, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="8b861-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="8b861-202">Пример: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="8b861-203">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-203">Date</span></span> |<span data-ttu-id="8b861-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-204">Day(X)</span></span> |<span data-ttu-id="8b861-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-205">X: DateTime</span></span> |<span data-ttu-id="8b861-206">Возвращает компонент дня hello X.</span><span class="sxs-lookup"><span data-stu-id="8b861-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="8b861-207">Пример: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="8b861-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="8b861-208">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-208">Date</span></span> |<span data-ttu-id="8b861-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-209">DayOfWeek(X)</span></span> |<span data-ttu-id="8b861-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-210">X: DateTime</span></span> |<span data-ttu-id="8b861-211">Возвращает день недели Координата X hello.</span><span class="sxs-lookup"><span data-stu-id="8b861-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="8b861-212">Пример: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="8b861-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="8b861-213">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-213">Date</span></span> |<span data-ttu-id="8b861-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-214">DayOfYear(X)</span></span> |<span data-ttu-id="8b861-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-215">X: DateTime</span></span> |<span data-ttu-id="8b861-216">Возвращает день hello hello года, представленный компонентом года hello X.</span><span class="sxs-lookup"><span data-stu-id="8b861-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="8b861-217">Примеры:</span><span class="sxs-lookup"><span data-stu-id="8b861-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="8b861-218">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-218">Date</span></span> |<span data-ttu-id="8b861-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-219">DaysInMonth(X)</span></span> |<span data-ttu-id="8b861-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-220">X: DateTime</span></span> |<span data-ttu-id="8b861-221">Возвращает hello дней в месяце hello, представленный hello компонентом месяца параметра X.</span><span class="sxs-lookup"><span data-stu-id="8b861-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="8b861-222">Пример: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="8b861-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="8b861-223">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-223">Date</span></span> |<span data-ttu-id="8b861-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-224">EndOfDay(X)</span></span> |<span data-ttu-id="8b861-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-225">X: DateTime</span></span> |<span data-ttu-id="8b861-226">Возвращает hello даты времени, представляющее конец hello hello дня (компонента дня) X.</span><span class="sxs-lookup"><span data-stu-id="8b861-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="8b861-227">Пример: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="8b861-228">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-228">Date</span></span> |<span data-ttu-id="8b861-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-229">EndOfMonth(X)</span></span> |<span data-ttu-id="8b861-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-230">X: DateTime</span></span> |<span data-ttu-id="8b861-231">Получает конец hello hello месяца, представленный компонентом месяца параметра X.</span><span class="sxs-lookup"><span data-stu-id="8b861-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="8b861-232">Пример: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (Дата и время, представляющий hello конец сентября)</span><span class="sxs-lookup"><span data-stu-id="8b861-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="8b861-233">Дата</span><span class="sxs-lookup"><span data-stu-id="8b861-233">Date</span></span> |<span data-ttu-id="8b861-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-234">StartOfDay(X)</span></span> |<span data-ttu-id="8b861-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-235">X: DateTime</span></span> |<span data-ttu-id="8b861-236">Получает начало hello hello дня, представленного компонентом дня hello параметра X.</span><span class="sxs-lookup"><span data-stu-id="8b861-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="8b861-237">Пример: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="8b861-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="8b861-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="8b861-238">DateTime</span></span> |<span data-ttu-id="8b861-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-239">From(X)</span></span> |<span data-ttu-id="8b861-240">X: String</span><span class="sxs-lookup"><span data-stu-id="8b861-240">X: String</span></span> |<span data-ttu-id="8b861-241">Синтаксический анализ строки X tooa Дата и время.</span><span class="sxs-lookup"><span data-stu-id="8b861-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="8b861-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="8b861-242">DateTime</span></span> |<span data-ttu-id="8b861-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-243">Ticks(X)</span></span> |<span data-ttu-id="8b861-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="8b861-244">X: DateTime</span></span> |<span data-ttu-id="8b861-245">Возвращает свойства параметра hello X hello тактов. Один такт равен 100 наносекунд.</span><span class="sxs-lookup"><span data-stu-id="8b861-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="8b861-246">Hello значение этого свойства представляет hello количество тактов, прошедших с полуночи в 12:00:00, 1 января 0001 г.</span><span class="sxs-lookup"><span data-stu-id="8b861-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="8b861-247">текст</span><span class="sxs-lookup"><span data-stu-id="8b861-247">Text</span></span> |<span data-ttu-id="8b861-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="8b861-248">Format(X)</span></span> |<span data-ttu-id="8b861-249">X: String (переменная)</span><span class="sxs-lookup"><span data-stu-id="8b861-249">X: String variable</span></span> |<span data-ttu-id="8b861-250">Текст hello форматов (использовать `\\'` tooescape комбинации `'` символов).</span><span class="sxs-lookup"><span data-stu-id="8b861-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="8b861-251">При использовании функции в другую функцию, нет необходимости toouse  **$$**  префикс для внутренней функции hello.</span><span class="sxs-lookup"><span data-stu-id="8b861-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="8b861-252">Например, $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="8b861-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="8b861-253">Обратите внимание, что в этом примере  **$$**  префикс не используется для hello **Time.AddHours** функции.</span><span class="sxs-lookup"><span data-stu-id="8b861-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="8b861-254">Пример</span><span class="sxs-lookup"><span data-stu-id="8b861-254">Example</span></span>
<span data-ttu-id="8b861-255">В hello в следующем примере, входные и выходные параметры для действия Hive hello определяются с использованием hello `Text.Format` функции и SliceStart системной переменной.</span><span class="sxs-lookup"><span data-stu-id="8b861-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="8b861-256">Пример 2</span><span class="sxs-lookup"><span data-stu-id="8b861-256">Example 2</span></span>

<span data-ttu-id="8b861-257">В следующем примере hello hello параметра DateTime для hello действия хранимой процедуры, определяется с помощью текста hello.</span><span class="sxs-lookup"><span data-stu-id="8b861-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="8b861-258">Функции форматирования и hello SliceStart переменной.</span><span class="sxs-lookup"><span data-stu-id="8b861-258">Format function and hello SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="8b861-259">Пример 3</span><span class="sxs-lookup"><span data-stu-id="8b861-259">Example 3</span></span>
<span data-ttu-id="8b861-260">tooread данные из предыдущего дня вместо день представлен прошедшими hello SliceStart, используйте функции hello AddDays, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="8b861-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="8b861-261">В разделе [Строки настраиваемых форматов даты и времени](https://msdn.microsoft.com/library/8kb3ddd4.aspx) описаны различные варианты форматирования, которые можно использовать (пример: гг и гггг).</span><span class="sxs-lookup"><span data-stu-id="8b861-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

