---
title: "Функции и системные переменные фабрики данных | Документация Майкрософт"
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
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="30e00-103">Фабрика данных Azure — функции и системные переменные</span><span class="sxs-lookup"><span data-stu-id="30e00-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="30e00-104">В этой статье содержатся сведения о функциях и переменных, поддерживаемых фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="30e00-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="30e00-105">Системные переменные фабрики данных</span><span class="sxs-lookup"><span data-stu-id="30e00-105">Data Factory system variables</span></span>
| <span data-ttu-id="30e00-106">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="30e00-106">Variable Name</span></span> | <span data-ttu-id="30e00-107">Описание</span><span class="sxs-lookup"><span data-stu-id="30e00-107">Description</span></span> | <span data-ttu-id="30e00-108">Область объекта</span><span class="sxs-lookup"><span data-stu-id="30e00-108">Object Scope</span></span> | <span data-ttu-id="30e00-109">Область JSON и примеры использования</span><span class="sxs-lookup"><span data-stu-id="30e00-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="30e00-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="30e00-110">WindowStart</span></span> |<span data-ttu-id="30e00-111">Начало интервала времени для текущего окна запуска действия.</span><span class="sxs-lookup"><span data-stu-id="30e00-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="30e00-112">действие</span><span class="sxs-lookup"><span data-stu-id="30e00-112">activity</span></span> |<ol><li><span data-ttu-id="30e00-113">Укажите запросы на выбор данных.</span><span class="sxs-lookup"><span data-stu-id="30e00-113">Specify data selection queries.</span></span> <span data-ttu-id="30e00-114">Ознакомьтесь со статьями о соединителях, упомянутых в статье [Действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="30e00-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="30e00-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="30e00-115">WindowEnd</span></span> |<span data-ttu-id="30e00-116">Конец интервала времени для текущего окна запуска действия.</span><span class="sxs-lookup"><span data-stu-id="30e00-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="30e00-117">действие</span><span class="sxs-lookup"><span data-stu-id="30e00-117">activity</span></span> |<span data-ttu-id="30e00-118">то же, что и WindowStart.</span><span class="sxs-lookup"><span data-stu-id="30e00-118">same as WindowStart.</span></span> |
| <span data-ttu-id="30e00-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="30e00-119">SliceStart</span></span> |<span data-ttu-id="30e00-120">Начало интервала времени для формируемого среза данных.</span><span class="sxs-lookup"><span data-stu-id="30e00-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="30e00-121">действие</span><span class="sxs-lookup"><span data-stu-id="30e00-121">activity</span></span><br/><span data-ttu-id="30e00-122">набор данных</span><span class="sxs-lookup"><span data-stu-id="30e00-122">dataset</span></span> |<ol><li><span data-ttu-id="30e00-123">Укажите динамические пути к папкам и имена файлов при работе с [большими двоичными объектами Azure](data-factory-azure-blob-connector.md) и [наборами данных файловой системы](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="30e00-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="30e00-124">Укажите входные зависимости с помощью функций фабрики данных в коллекции входных данных действия.</span><span class="sxs-lookup"><span data-stu-id="30e00-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="30e00-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="30e00-125">SliceEnd</span></span> |<span data-ttu-id="30e00-126">Конец интервала времени для текущего среза данных.</span><span class="sxs-lookup"><span data-stu-id="30e00-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="30e00-127">действие</span><span class="sxs-lookup"><span data-stu-id="30e00-127">activity</span></span><br/><span data-ttu-id="30e00-128">dataset</span><span class="sxs-lookup"><span data-stu-id="30e00-128">dataset</span></span> |<span data-ttu-id="30e00-129">То же, что и для SliceStart.</span><span class="sxs-lookup"><span data-stu-id="30e00-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="30e00-130">В настоящее время для фабрики данных требуется, чтобы расписание, указанное в действии, в точности соответствовало расписанию, указанному в разделе availability выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="30e00-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="30e00-131">Следовательно, WindowStart, WindowEnd, SliceStart и SliceEnd всегда сопоставляются с одним и тем же периодом времени и отдельным выходным срезом.</span><span class="sxs-lookup"><span data-stu-id="30e00-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="30e00-132">Пример использования системной переменной</span><span class="sxs-lookup"><span data-stu-id="30e00-132">Example for using a system variable</span></span>
<span data-ttu-id="30e00-133">В этом примере год, месяц, день и время **SliceStart** извлекаются в отдельные переменные, используемые в свойствах **folderPath** и **fileName**.</span><span class="sxs-lookup"><span data-stu-id="30e00-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="30e00-134">Функции фабрики данных</span><span class="sxs-lookup"><span data-stu-id="30e00-134">Data Factory functions</span></span>
<span data-ttu-id="30e00-135">Функции фабрики данных можно использовать с системными переменными для следующих целей:</span><span class="sxs-lookup"><span data-stu-id="30e00-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="30e00-136">Указание запросов выбора данных (см. статьи о соединителях, на которые ссылается статья [Действия перемещения данных](data-factory-data-movement-activities.md)).</span><span class="sxs-lookup"><span data-stu-id="30e00-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="30e00-137">Синтаксис, необходимый для вызова функции фабрики данных, — это **$$<function>** (используется для запросов выбора данных и других свойств действий и наборов данных).</span><span class="sxs-lookup"><span data-stu-id="30e00-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="30e00-138">Указание входных зависимостей с помощью функций фабрики данных в коллекции входных данных действия.</span><span class="sxs-lookup"><span data-stu-id="30e00-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="30e00-139">Префикс $$ не требуется при указании выражений входных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="30e00-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="30e00-140">В следующем примере свойству **sqlReaderQuery** в JSON-файле присваивается значение, возвращаемое функцией `Text.Format`.</span><span class="sxs-lookup"><span data-stu-id="30e00-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="30e00-141">Кроме того, в этом примере используется системная переменная с именем **WindowStart**, которая отображает время начала для окна запуска действия.</span><span class="sxs-lookup"><span data-stu-id="30e00-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="30e00-142">В разделе [Строки настраиваемых форматов даты и времени](https://msdn.microsoft.com/library/8kb3ddd4.aspx) описаны различные варианты форматирования, которые можно использовать (пример: гг и гггг).</span><span class="sxs-lookup"><span data-stu-id="30e00-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="30e00-143">Функции</span><span class="sxs-lookup"><span data-stu-id="30e00-143">Functions</span></span>
<span data-ttu-id="30e00-144">В приведенных ниже таблицах перечислены все функции фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="30e00-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="30e00-145">Категория</span><span class="sxs-lookup"><span data-stu-id="30e00-145">Category</span></span> | <span data-ttu-id="30e00-146">Функция</span><span class="sxs-lookup"><span data-stu-id="30e00-146">Function</span></span> | <span data-ttu-id="30e00-147">Параметры</span><span class="sxs-lookup"><span data-stu-id="30e00-147">Parameters</span></span> | <span data-ttu-id="30e00-148">Описание</span><span class="sxs-lookup"><span data-stu-id="30e00-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="30e00-149">Время</span><span class="sxs-lookup"><span data-stu-id="30e00-149">Time</span></span> |<span data-ttu-id="30e00-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-150">AddHours(X,Y)</span></span> |<span data-ttu-id="30e00-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="30e00-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-152">Y: int</span></span> |<span data-ttu-id="30e00-153">Добавляет Y часов к заданному времени X.</span><span class="sxs-lookup"><span data-stu-id="30e00-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="30e00-154">Пример: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="30e00-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="30e00-155">Время</span><span class="sxs-lookup"><span data-stu-id="30e00-155">Time</span></span> |<span data-ttu-id="30e00-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="30e00-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="30e00-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-158">Y: int</span></span> |<span data-ttu-id="30e00-159">Добавляет Y минут к Х.</span><span class="sxs-lookup"><span data-stu-id="30e00-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="30e00-160">Пример: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="30e00-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="30e00-161">Время</span><span class="sxs-lookup"><span data-stu-id="30e00-161">Time</span></span> |<span data-ttu-id="30e00-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-162">StartOfHour(X)</span></span> |<span data-ttu-id="30e00-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-163">X: Datetime</span></span> |<span data-ttu-id="30e00-164">Получает то время, когда начинался час, отображаемый компонентом часа в параметре X.</span><span class="sxs-lookup"><span data-stu-id="30e00-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="30e00-165">Пример: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="30e00-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="30e00-166">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-166">Date</span></span> |<span data-ttu-id="30e00-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-167">AddDays(X,Y)</span></span> |<span data-ttu-id="30e00-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-168">X: DateTime</span></span><br/><br/><span data-ttu-id="30e00-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-169">Y: int</span></span> |<span data-ttu-id="30e00-170">Добавляет Y дней к Х.</span><span class="sxs-lookup"><span data-stu-id="30e00-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="30e00-171">Пример: 15.09.2013 12:00:00 + 2 дня = 17.09.2013 12:00:00.</span><span class="sxs-lookup"><span data-stu-id="30e00-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="30e00-172">Можно также вычитать дни, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="30e00-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="30e00-173">Пример: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="30e00-174">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-174">Date</span></span> |<span data-ttu-id="30e00-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="30e00-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-176">X: DateTime</span></span><br/><br/><span data-ttu-id="30e00-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-177">Y: int</span></span> |<span data-ttu-id="30e00-178">Добавляет Y месяцев к Х.</span><span class="sxs-lookup"><span data-stu-id="30e00-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="30e00-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="30e00-180">Можно также вычитать месяцы, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="30e00-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="30e00-181">Пример: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="30e00-182">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-182">Date</span></span> |<span data-ttu-id="30e00-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="30e00-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="30e00-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-185">Y: int</span></span> |<span data-ttu-id="30e00-186">Добавляет Y * 3 месяцев к Х.</span><span class="sxs-lookup"><span data-stu-id="30e00-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="30e00-187">Пример: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="30e00-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="30e00-188">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-188">Date</span></span> |<span data-ttu-id="30e00-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="30e00-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-190">X: DateTime</span></span><br/><br/><span data-ttu-id="30e00-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-191">Y: int</span></span> |<span data-ttu-id="30e00-192">Добавляет Y (одна единица которого равна 7 дням) к X</span><span class="sxs-lookup"><span data-stu-id="30e00-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="30e00-193">Пример: 15.09.2013 12:00:00 + 1 неделя = 22.09.2013 12:00:00.</span><span class="sxs-lookup"><span data-stu-id="30e00-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="30e00-194">Можно также вычитать недели, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="30e00-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="30e00-195">Пример: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="30e00-196">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-196">Date</span></span> |<span data-ttu-id="30e00-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="30e00-197">AddYears(X,Y)</span></span> |<span data-ttu-id="30e00-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-198">X: DateTime</span></span><br/><br/><span data-ttu-id="30e00-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="30e00-199">Y: int</span></span> |<span data-ttu-id="30e00-200">Добавляет Y лет к Х.</span><span class="sxs-lookup"><span data-stu-id="30e00-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="30e00-201">Можно также вычитать года, указав в качестве Y отрицательное число.</span><span class="sxs-lookup"><span data-stu-id="30e00-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="30e00-202">Пример: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="30e00-203">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-203">Date</span></span> |<span data-ttu-id="30e00-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-204">Day(X)</span></span> |<span data-ttu-id="30e00-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-205">X: DateTime</span></span> |<span data-ttu-id="30e00-206">Возвращает значение дня для X.</span><span class="sxs-lookup"><span data-stu-id="30e00-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="30e00-207">Пример: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="30e00-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="30e00-208">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-208">Date</span></span> |<span data-ttu-id="30e00-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-209">DayOfWeek(X)</span></span> |<span data-ttu-id="30e00-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-210">X: DateTime</span></span> |<span data-ttu-id="30e00-211">Возвращает значение дня недели для X.</span><span class="sxs-lookup"><span data-stu-id="30e00-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="30e00-212">Пример: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="30e00-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="30e00-213">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-213">Date</span></span> |<span data-ttu-id="30e00-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-214">DayOfYear(X)</span></span> |<span data-ttu-id="30e00-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-215">X: DateTime</span></span> |<span data-ttu-id="30e00-216">Получает день года, представленный значением года параметра X.</span><span class="sxs-lookup"><span data-stu-id="30e00-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="30e00-217">Примеры:</span><span class="sxs-lookup"><span data-stu-id="30e00-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="30e00-218">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-218">Date</span></span> |<span data-ttu-id="30e00-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-219">DaysInMonth(X)</span></span> |<span data-ttu-id="30e00-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-220">X: DateTime</span></span> |<span data-ttu-id="30e00-221">Получает количество дней в месяце, представленном значением месяца параметра X.</span><span class="sxs-lookup"><span data-stu-id="30e00-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="30e00-222">Пример: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="30e00-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="30e00-223">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-223">Date</span></span> |<span data-ttu-id="30e00-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-224">EndOfDay(X)</span></span> |<span data-ttu-id="30e00-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-225">X: DateTime</span></span> |<span data-ttu-id="30e00-226">Получает значение даты и времени, которое соответствует окончанию суток (значения дня) в параметре X.</span><span class="sxs-lookup"><span data-stu-id="30e00-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="30e00-227">Пример: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="30e00-228">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-228">Date</span></span> |<span data-ttu-id="30e00-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-229">EndOfMonth(X)</span></span> |<span data-ttu-id="30e00-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-230">X: DateTime</span></span> |<span data-ttu-id="30e00-231">Получает значение конца месяца, представленного значением месяца параметра X.</span><span class="sxs-lookup"><span data-stu-id="30e00-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="30e00-232">Пример: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (дата и время конца сентября).</span><span class="sxs-lookup"><span data-stu-id="30e00-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="30e00-233">Дата</span><span class="sxs-lookup"><span data-stu-id="30e00-233">Date</span></span> |<span data-ttu-id="30e00-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-234">StartOfDay(X)</span></span> |<span data-ttu-id="30e00-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-235">X: DateTime</span></span> |<span data-ttu-id="30e00-236">Получает начало суток, представленных значением дня в параметре X.</span><span class="sxs-lookup"><span data-stu-id="30e00-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="30e00-237">Пример: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="30e00-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="30e00-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="30e00-238">DateTime</span></span> |<span data-ttu-id="30e00-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-239">From(X)</span></span> |<span data-ttu-id="30e00-240">X: String</span><span class="sxs-lookup"><span data-stu-id="30e00-240">X: String</span></span> |<span data-ttu-id="30e00-241">Разбор строки X в значение даты и времени.</span><span class="sxs-lookup"><span data-stu-id="30e00-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="30e00-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="30e00-242">DateTime</span></span> |<span data-ttu-id="30e00-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-243">Ticks(X)</span></span> |<span data-ttu-id="30e00-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="30e00-244">X: DateTime</span></span> |<span data-ttu-id="30e00-245">Получает свойство тактов времени параметра X. Один такт равен 100 наносекундам.</span><span class="sxs-lookup"><span data-stu-id="30e00-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="30e00-246">Значение этого свойства соответствует количеству тактов, прошедших с полуночи (24:00:00) 1 января 0001 года.</span><span class="sxs-lookup"><span data-stu-id="30e00-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="30e00-247">текст</span><span class="sxs-lookup"><span data-stu-id="30e00-247">Text</span></span> |<span data-ttu-id="30e00-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="30e00-248">Format(X)</span></span> |<span data-ttu-id="30e00-249">X: String (переменная)</span><span class="sxs-lookup"><span data-stu-id="30e00-249">X: String variable</span></span> |<span data-ttu-id="30e00-250">Форматирует текст (используйте комбинацию `\\'` для экранирования символа `'`).</span><span class="sxs-lookup"><span data-stu-id="30e00-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="30e00-251">При использовании функции внутри другой функции нет необходимости использовать для внутренней функции префикс **$$** .</span><span class="sxs-lookup"><span data-stu-id="30e00-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="30e00-252">Например, $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="30e00-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="30e00-253">В этом примере обратите внимание, что префикс **$$** не используется для функции **Time.AddHours**.</span><span class="sxs-lookup"><span data-stu-id="30e00-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="30e00-254">Пример</span><span class="sxs-lookup"><span data-stu-id="30e00-254">Example</span></span>
<span data-ttu-id="30e00-255">В следующем примере входные и выходные параметры для действия Hive определяются с помощью функции `Text.Format` и системной переменной SliceStart.</span><span class="sxs-lookup"><span data-stu-id="30e00-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="30e00-256">Пример 2</span><span class="sxs-lookup"><span data-stu-id="30e00-256">Example 2</span></span>

<span data-ttu-id="30e00-257">В следующем примере параметр DateTime для действия хранимой процедуры определяется с помощью функции Text.</span><span class="sxs-lookup"><span data-stu-id="30e00-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="30e00-258">Format и системной переменной SliceStart.</span><span class="sxs-lookup"><span data-stu-id="30e00-258">Format function and the SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="30e00-259">Пример 3</span><span class="sxs-lookup"><span data-stu-id="30e00-259">Example 3</span></span>
<span data-ttu-id="30e00-260">Для чтения данных за предыдущий день, а не день, указанный в SliceStart, используйте функцию AddDays, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="30e00-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

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

<span data-ttu-id="30e00-261">В разделе [Строки настраиваемых форматов даты и времени](https://msdn.microsoft.com/library/8kb3ddd4.aspx) описаны различные варианты форматирования, которые можно использовать (пример: гг и гггг).</span><span class="sxs-lookup"><span data-stu-id="30e00-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

