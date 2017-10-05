---
title: "Формирование строк фильтра для конструктора таблиц | Документация Майкрософт"
description: "Построение строк фильтра для конструктора таблиц"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 069224d84462b4955912ce1462a65298a5acc04a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="constructing-filter-strings-for-the-table-designer"></a><span data-ttu-id="6c42e-103">Построение строк фильтра для конструктора таблиц</span><span class="sxs-lookup"><span data-stu-id="6c42e-103">Constructing Filter Strings for the Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="6c42e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6c42e-104">Overview</span></span>
<span data-ttu-id="6c42e-105">Для фильтрации данных в таблице Azure, отображаемой в **конструкторе таблиц**Visual Studio, нужно создать строку фильтра и ввести ее в поле фильтра.</span><span class="sxs-lookup"><span data-stu-id="6c42e-105">To filter data in an Azure table that is displayed in the Visual Studio **Table Designer**, you construct a filter string and enter it into the filter field.</span></span> <span data-ttu-id="6c42e-106">Синтаксис строки фильтра определяется службами данных WCF и напоминает предложение SQL WHERE, но отправляется в службу таблиц через HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="6c42e-106">The filter string syntax is defined by the WCF Data Services and is similar to a SQL WHERE clause, but is sent to the Table service via an HTTP request.</span></span> <span data-ttu-id="6c42e-107">**Конструктор таблиц** обрабатывает соответствующую кодировку, поэтому для фильтрации по определенному значению свойства в поле фильтра необходимо ввести только имя свойства, оператор сравнения, значение критерия и, при необходимости, логический оператор.</span><span class="sxs-lookup"><span data-stu-id="6c42e-107">The **Table Designer** handles the proper encoding for you, so to filter on a desired property value, you need only enter the property name, comparison operator, criteria value, and optionally, Boolean operator in the filter field.</span></span> <span data-ttu-id="6c42e-108">Не нужно включать параметр запроса $filter, как при построении URL-адреса для запроса к таблице через [Справочник по API REST служб хранилища](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="6c42e-108">You do not need to include the $filter query option as you would if you were constructing a URL to query the table via the [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="6c42e-109">Службы данных WCF основаны на протоколе [OData](http://go.microsoft.com/fwlink/p/?LinkId=214805).</span><span class="sxs-lookup"><span data-stu-id="6c42e-109">The WCF Data Services are based on the [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="6c42e-110">Дополнительные сведения о параметре системного запроса фильтрации (**$filter**) см. в [спецификации соглашений об универсальных кодах ресурсов (URI) для OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="6c42e-110">For details on the filter system query option (**$filter**), see the [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="6c42e-111">Операторы сравнения</span><span class="sxs-lookup"><span data-stu-id="6c42e-111">Comparison Operators</span></span>
<span data-ttu-id="6c42e-112">Для всех типов свойств поддерживаются следующие логические операторы:</span><span class="sxs-lookup"><span data-stu-id="6c42e-112">The following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="6c42e-113">Логический оператор</span><span class="sxs-lookup"><span data-stu-id="6c42e-113">Logical operator</span></span> | <span data-ttu-id="6c42e-114">Описание</span><span class="sxs-lookup"><span data-stu-id="6c42e-114">Description</span></span> | <span data-ttu-id="6c42e-115">Пример строки фильтра</span><span class="sxs-lookup"><span data-stu-id="6c42e-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c42e-116">eq</span><span class="sxs-lookup"><span data-stu-id="6c42e-116">eq</span></span> |<span data-ttu-id="6c42e-117">Равно</span><span class="sxs-lookup"><span data-stu-id="6c42e-117">Equal</span></span> |<span data-ttu-id="6c42e-118">City eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="6c42e-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="6c42e-119">gt</span><span class="sxs-lookup"><span data-stu-id="6c42e-119">gt</span></span> |<span data-ttu-id="6c42e-120">Больше</span><span class="sxs-lookup"><span data-stu-id="6c42e-120">Greater than</span></span> |<span data-ttu-id="6c42e-121">Price gt 20</span><span class="sxs-lookup"><span data-stu-id="6c42e-121">Price gt 20</span></span> |
| <span data-ttu-id="6c42e-122">ge</span><span class="sxs-lookup"><span data-stu-id="6c42e-122">ge</span></span> |<span data-ttu-id="6c42e-123">Больше или равно</span><span class="sxs-lookup"><span data-stu-id="6c42e-123">Greater than or equal to</span></span> |<span data-ttu-id="6c42e-124">Price ge 10</span><span class="sxs-lookup"><span data-stu-id="6c42e-124">Price ge 10</span></span> |
| <span data-ttu-id="6c42e-125">lt</span><span class="sxs-lookup"><span data-stu-id="6c42e-125">lt</span></span> |<span data-ttu-id="6c42e-126">Меньше</span><span class="sxs-lookup"><span data-stu-id="6c42e-126">Less than</span></span> |<span data-ttu-id="6c42e-127">Price lt 20</span><span class="sxs-lookup"><span data-stu-id="6c42e-127">Price lt 20</span></span> |
| <span data-ttu-id="6c42e-128">le</span><span class="sxs-lookup"><span data-stu-id="6c42e-128">le</span></span> |<span data-ttu-id="6c42e-129">Меньше или равно</span><span class="sxs-lookup"><span data-stu-id="6c42e-129">Less than or equal</span></span> |<span data-ttu-id="6c42e-130">Price le 100</span><span class="sxs-lookup"><span data-stu-id="6c42e-130">Price le 100</span></span> |
| <span data-ttu-id="6c42e-131">ne</span><span class="sxs-lookup"><span data-stu-id="6c42e-131">ne</span></span> |<span data-ttu-id="6c42e-132">Не равно</span><span class="sxs-lookup"><span data-stu-id="6c42e-132">Not equal</span></span> |<span data-ttu-id="6c42e-133">City ne 'London'</span><span class="sxs-lookup"><span data-stu-id="6c42e-133">City ne 'London'</span></span> |
| <span data-ttu-id="6c42e-134">и</span><span class="sxs-lookup"><span data-stu-id="6c42e-134">and</span></span> |<span data-ttu-id="6c42e-135">и</span><span class="sxs-lookup"><span data-stu-id="6c42e-135">And</span></span> |<span data-ttu-id="6c42e-136">Price le 200 and Price gt 3.5</span><span class="sxs-lookup"><span data-stu-id="6c42e-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="6c42e-137">или</span><span class="sxs-lookup"><span data-stu-id="6c42e-137">or</span></span> |<span data-ttu-id="6c42e-138">или</span><span class="sxs-lookup"><span data-stu-id="6c42e-138">Or</span></span> |<span data-ttu-id="6c42e-139">Price le 3.5 or Price gt 200</span><span class="sxs-lookup"><span data-stu-id="6c42e-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="6c42e-140">not</span><span class="sxs-lookup"><span data-stu-id="6c42e-140">not</span></span> |<span data-ttu-id="6c42e-141">not</span><span class="sxs-lookup"><span data-stu-id="6c42e-141">Not</span></span> |<span data-ttu-id="6c42e-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="6c42e-142">not isAvailable</span></span> |

<span data-ttu-id="6c42e-143">При создании строки фильтра соблюдайте следующие правила.</span><span class="sxs-lookup"><span data-stu-id="6c42e-143">When constructing a filter string, the following rules are important:</span></span>

* <span data-ttu-id="6c42e-144">Для сравнения свойства со значением используйте логические операторы.</span><span class="sxs-lookup"><span data-stu-id="6c42e-144">Use the logical operators to compare a property to a value.</span></span> <span data-ttu-id="6c42e-145">Обратите внимание, что нельзя сравнивать свойство и динамическое значение. Одна из частей выражения должна быть константой.</span><span class="sxs-lookup"><span data-stu-id="6c42e-145">Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.</span></span>
* <span data-ttu-id="6c42e-146">Во всех частях строки фильтра учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="6c42e-146">All parts of the filter string are case-sensitive.</span></span>
* <span data-ttu-id="6c42e-147">Для получения допустимых результатов фильтра значения константы и свойства должны иметь одинаковый тип данных.</span><span class="sxs-lookup"><span data-stu-id="6c42e-147">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="6c42e-148">Дополнительные сведения о поддерживаемых типах свойств см. в статье [Общие сведения о модели данных службы таблиц](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="6c42e-148">For more information about supported property types, see [Understanding the Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="6c42e-149">Фильтрация по строковым свойствам</span><span class="sxs-lookup"><span data-stu-id="6c42e-149">Filtering on String Properties</span></span>
<span data-ttu-id="6c42e-150">Во время фильтрации по строковым свойствам заключайте строковую константу в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="6c42e-150">When you filter on string properties, enclose the string constant in single quotation marks.</span></span>

<span data-ttu-id="6c42e-151">В следующем примере выполняется фильтрация по свойствам **PartitionKey** и **RowKey**. Дополнительные неключевые свойства также можно добавить в строку фильтра.</span><span class="sxs-lookup"><span data-stu-id="6c42e-151">The following example filters on the **PartitionKey** and **RowKey** properties; additional non-key properties could also be added to the filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="6c42e-152">Каждое выражение фильтра можно заключить в круглые скобки, хотя это не обязательно:</span><span class="sxs-lookup"><span data-stu-id="6c42e-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="6c42e-153">Обратите внимание, что служба таблиц не поддерживает запросы с подстановочными знаками, они также не поддерживаются в конструкторе таблиц.</span><span class="sxs-lookup"><span data-stu-id="6c42e-153">Note that the Table service does not support wildcard queries, and they are not supported in the Table Designer either.</span></span> <span data-ttu-id="6c42e-154">Тем не менее можно выполнять фильтрацию по префиксу, используя операторы сравнения и нужный префикс.</span><span class="sxs-lookup"><span data-stu-id="6c42e-154">However, you can perform prefix matching by using comparison operators on the desired prefix.</span></span> <span data-ttu-id="6c42e-155">Следующий пример возвращает сущности, в которых свойство LastName начинается с буквы "A":</span><span class="sxs-lookup"><span data-stu-id="6c42e-155">The following example returns entities with a LastName property beginning with the letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="6c42e-156">Фильтрация по числовым свойствам</span><span class="sxs-lookup"><span data-stu-id="6c42e-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="6c42e-157">Чтобы отфильтровать целое число или число с плавающей запятой, указывайте число без кавычек.</span><span class="sxs-lookup"><span data-stu-id="6c42e-157">To filter on an integer or floating-point number, specify the number without quotation marks.</span></span>

<span data-ttu-id="6c42e-158">Следующий пример возвращает все сущности свойства Age, значения которых больше 30.</span><span class="sxs-lookup"><span data-stu-id="6c42e-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="6c42e-159">Следующий пример возвращает все сущности свойства AmountDue, значения которых меньше или равны 100,25.</span><span class="sxs-lookup"><span data-stu-id="6c42e-159">This example returns all entities with an AmountDue property whose value is less than or equal to 100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="6c42e-160">Фильтрация по логическим свойствам</span><span class="sxs-lookup"><span data-stu-id="6c42e-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="6c42e-161">Для фильтрации по логическим значениям указывайте **true** или **false** без кавычек.</span><span class="sxs-lookup"><span data-stu-id="6c42e-161">To filter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="6c42e-162">В следующем примере возвращаются все сущности, в которых свойство IsActive имеет значение **true**:</span><span class="sxs-lookup"><span data-stu-id="6c42e-162">The following example returns all entities where the IsActive property is set to **true**:</span></span>

    IsActive eq true

<span data-ttu-id="6c42e-163">Это выражение фильтрации также можно записать без логического оператора.</span><span class="sxs-lookup"><span data-stu-id="6c42e-163">You can also write this filter expression without the logical operator.</span></span> <span data-ttu-id="6c42e-164">В следующем примере служба таблиц также вернет все сущности, в которых свойство IsActive имеет значение **true**.</span><span class="sxs-lookup"><span data-stu-id="6c42e-164">In the following example, the Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="6c42e-165">Вернуть все сущности, в которых свойство IsActive имеет значение false, можно с помощью оператора not.</span><span class="sxs-lookup"><span data-stu-id="6c42e-165">To return all entities where IsActive is false, you can use the not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="6c42e-166">Фильтрация по свойствам DateTime</span><span class="sxs-lookup"><span data-stu-id="6c42e-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="6c42e-167">Для фильтрации по значению DateTime укажите ключевое слово **datetime** , за которым введите константу даты и времени в одинарных кавычках.</span><span class="sxs-lookup"><span data-stu-id="6c42e-167">To filter on a DateTime value, specify the **datetime** keyword, followed by the date/time constant in single quotation marks.</span></span> <span data-ttu-id="6c42e-168">Константа даты и времени должна быть указана в комбинированном формате UTC, как описано в статье [Форматирование значений свойства DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="6c42e-168">The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="6c42e-169">Следующий пример возвращает сущности, в которых свойство CustomerSince имеет значение 10 июля 2008 г.</span><span class="sxs-lookup"><span data-stu-id="6c42e-169">The following example returns entities where the CustomerSince property is equal to July 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
