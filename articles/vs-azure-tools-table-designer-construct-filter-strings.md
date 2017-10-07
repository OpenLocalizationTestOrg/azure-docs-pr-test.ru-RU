---
title: "aaaConstructing фильтр строк для конструктора таблиц hello | Документы Microsoft"
description: "Построение строк фильтра для конструктора таблиц hello"
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
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="211ba-103">Построение строк фильтра для hello конструктора таблиц</span><span class="sxs-lookup"><span data-stu-id="211ba-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="211ba-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="211ba-104">Overview</span></span>
<span data-ttu-id="211ba-105">Здравствуйте, toofilter данные в таблице Azure, которая отображается в Visual Studio **конструктор таблиц**, создать строку фильтра и ввести в поле фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="211ba-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="211ba-106">синтаксис строки фильтра Hello определяется hello службы данных WCF — примерно tooa SQL предложение WHERE, но отправляется toohello службе таблиц через HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="211ba-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="211ba-107">Hello **конструктор таблиц** hello обрабатывает соответствующую кодировку, поэтому toofilter по значению свойства, потребуется только ввести имя свойства hello, оператор сравнения, значение условия, и при необходимости отфильтровать логический оператор в hello поле.</span><span class="sxs-lookup"><span data-stu-id="211ba-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="211ba-108">Как при построении URL-адрес таблицы hello tooquery через hello не требуется параметр запроса hello $filter tooinclude [Справочник API REST служб хранилища](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="211ba-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="211ba-109">Службы данных WCF Hello основаны на hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="211ba-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="211ba-110">Дополнительные сведения о параметр системного запроса фильтрации hello (**$filter**), hello в разделе [соглашения об URI OData спецификации](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="211ba-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="211ba-111">Операторы сравнения</span><span class="sxs-lookup"><span data-stu-id="211ba-111">Comparison Operators</span></span>
<span data-ttu-id="211ba-112">Hello следующие логические операторы поддерживаются для всех типов свойств:</span><span class="sxs-lookup"><span data-stu-id="211ba-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="211ba-113">Логический оператор</span><span class="sxs-lookup"><span data-stu-id="211ba-113">Logical operator</span></span> | <span data-ttu-id="211ba-114">Описание</span><span class="sxs-lookup"><span data-stu-id="211ba-114">Description</span></span> | <span data-ttu-id="211ba-115">Пример строки фильтра</span><span class="sxs-lookup"><span data-stu-id="211ba-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="211ba-116">eq</span><span class="sxs-lookup"><span data-stu-id="211ba-116">eq</span></span> |<span data-ttu-id="211ba-117">Равно</span><span class="sxs-lookup"><span data-stu-id="211ba-117">Equal</span></span> |<span data-ttu-id="211ba-118">City eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="211ba-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="211ba-119">gt</span><span class="sxs-lookup"><span data-stu-id="211ba-119">gt</span></span> |<span data-ttu-id="211ba-120">Больше</span><span class="sxs-lookup"><span data-stu-id="211ba-120">Greater than</span></span> |<span data-ttu-id="211ba-121">Price gt 20</span><span class="sxs-lookup"><span data-stu-id="211ba-121">Price gt 20</span></span> |
| <span data-ttu-id="211ba-122">ge</span><span class="sxs-lookup"><span data-stu-id="211ba-122">ge</span></span> |<span data-ttu-id="211ba-123">Больше или равно слишком</span><span class="sxs-lookup"><span data-stu-id="211ba-123">Greater than or equal too</span></span>|<span data-ttu-id="211ba-124">Price ge 10</span><span class="sxs-lookup"><span data-stu-id="211ba-124">Price ge 10</span></span> |
| <span data-ttu-id="211ba-125">lt</span><span class="sxs-lookup"><span data-stu-id="211ba-125">lt</span></span> |<span data-ttu-id="211ba-126">Меньше</span><span class="sxs-lookup"><span data-stu-id="211ba-126">Less than</span></span> |<span data-ttu-id="211ba-127">Price lt 20</span><span class="sxs-lookup"><span data-stu-id="211ba-127">Price lt 20</span></span> |
| <span data-ttu-id="211ba-128">le</span><span class="sxs-lookup"><span data-stu-id="211ba-128">le</span></span> |<span data-ttu-id="211ba-129">Меньше или равно</span><span class="sxs-lookup"><span data-stu-id="211ba-129">Less than or equal</span></span> |<span data-ttu-id="211ba-130">Price le 100</span><span class="sxs-lookup"><span data-stu-id="211ba-130">Price le 100</span></span> |
| <span data-ttu-id="211ba-131">ne</span><span class="sxs-lookup"><span data-stu-id="211ba-131">ne</span></span> |<span data-ttu-id="211ba-132">Не равно</span><span class="sxs-lookup"><span data-stu-id="211ba-132">Not equal</span></span> |<span data-ttu-id="211ba-133">City ne 'London'</span><span class="sxs-lookup"><span data-stu-id="211ba-133">City ne 'London'</span></span> |
| <span data-ttu-id="211ba-134">и</span><span class="sxs-lookup"><span data-stu-id="211ba-134">and</span></span> |<span data-ttu-id="211ba-135">и</span><span class="sxs-lookup"><span data-stu-id="211ba-135">And</span></span> |<span data-ttu-id="211ba-136">Price le 200 and Price gt 3.5</span><span class="sxs-lookup"><span data-stu-id="211ba-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="211ba-137">или</span><span class="sxs-lookup"><span data-stu-id="211ba-137">or</span></span> |<span data-ttu-id="211ba-138">или</span><span class="sxs-lookup"><span data-stu-id="211ba-138">Or</span></span> |<span data-ttu-id="211ba-139">Price le 3.5 or Price gt 200</span><span class="sxs-lookup"><span data-stu-id="211ba-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="211ba-140">not</span><span class="sxs-lookup"><span data-stu-id="211ba-140">not</span></span> |<span data-ttu-id="211ba-141">not</span><span class="sxs-lookup"><span data-stu-id="211ba-141">Not</span></span> |<span data-ttu-id="211ba-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="211ba-142">not isAvailable</span></span> |

<span data-ttu-id="211ba-143">При создании строки фильтра hello следующие правила, важные.</span><span class="sxs-lookup"><span data-stu-id="211ba-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="211ba-144">Используйте логические операторы hello toocompare tooa значения свойства.</span><span class="sxs-lookup"><span data-stu-id="211ba-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="211ba-145">Обратите внимание, что возможные toocompare tooa динамическое значение свойства; одна часть hello выражение должно быть константой.</span><span class="sxs-lookup"><span data-stu-id="211ba-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="211ba-146">Все части hello строки фильтра учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="211ba-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="211ba-147">должен иметь постоянное значение Hello hello и тех же данных введите в качестве свойства hello в порядке для hello фильтра tooreturn правильные результаты.</span><span class="sxs-lookup"><span data-stu-id="211ba-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="211ba-148">Дополнительные сведения о поддерживаемых типах свойств см. в разделе [hello основные сведения о модели данных службы таблиц](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="211ba-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="211ba-149">Фильтрация по строковым свойствам</span><span class="sxs-lookup"><span data-stu-id="211ba-149">Filtering on String Properties</span></span>
<span data-ttu-id="211ba-150">При фильтрации по строковым свойствам заключайте hello строковую константу в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="211ba-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="211ba-151">далее примере фильтры hello Hello **PartitionKey** и **RowKey** свойства; дополнительные не ключевые свойства также могут быть добавлены toohello строку фильтра:</span><span class="sxs-lookup"><span data-stu-id="211ba-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="211ba-152">Каждое выражение фильтра можно заключить в круглые скобки, хотя это не обязательно:</span><span class="sxs-lookup"><span data-stu-id="211ba-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="211ba-153">Обратите внимание, что hello служба таблиц не поддерживает запросы подстановочный знак, они не поддерживаются в конструкторе таблиц hello либо.</span><span class="sxs-lookup"><span data-stu-id="211ba-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="211ba-154">Тем не менее можно выполнить с помощью операторов сравнения на hello желаемый префикс сопоставления префиксов.</span><span class="sxs-lookup"><span data-stu-id="211ba-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="211ba-155">Hello следующий пример возвращает сущности с свойство LastName начинается с hello буквы «A».</span><span class="sxs-lookup"><span data-stu-id="211ba-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="211ba-156">Фильтрация по числовым свойствам</span><span class="sxs-lookup"><span data-stu-id="211ba-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="211ba-157">toofilter на целое число или число с плавающей запятой, укажите номер hello без кавычек.</span><span class="sxs-lookup"><span data-stu-id="211ba-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="211ba-158">Следующий пример возвращает все сущности свойства Age, значения которых больше 30.</span><span class="sxs-lookup"><span data-stu-id="211ba-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="211ba-159">Этот пример возвращает все сущности со значением свойства AmountDue меньше или равен too100.25:</span><span class="sxs-lookup"><span data-stu-id="211ba-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="211ba-160">Фильтрация по логическим свойствам</span><span class="sxs-lookup"><span data-stu-id="211ba-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="211ba-161">Укажите toofilter к логическому значению **true** или **false** без кавычек.</span><span class="sxs-lookup"><span data-stu-id="211ba-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="211ba-162">Hello следующий пример возвращает все сущности которых hello свойство IsActive имеет значение слишком**true**:</span><span class="sxs-lookup"><span data-stu-id="211ba-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="211ba-163">Можно также написать этот критерий фильтра без hello логический оператор.</span><span class="sxs-lookup"><span data-stu-id="211ba-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="211ba-164">В следующем примере hello, hello служба таблиц также вернет все сущности которых свойство IsActive имеет **true**:</span><span class="sxs-lookup"><span data-stu-id="211ba-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="211ba-165">все сущности, в которых свойство IsActive имеет значение false, можно использовать hello не tooreturn оператор:</span><span class="sxs-lookup"><span data-stu-id="211ba-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="211ba-166">Фильтрация по свойствам DateTime</span><span class="sxs-lookup"><span data-stu-id="211ba-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="211ba-167">toofilter в значении даты и времени, укажите hello **datetime** ключевое слово, за которым введите константу даты и времени hello в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="211ba-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="211ba-168">Константа даты времени Hello должна быть в комбинированном формате UTC, как описано в [форматирование значений свойств DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="211ba-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="211ba-169">Следующий пример Hello возвращает сущности, где свойство CustomerSince hello — tooJuly равно 10, 2008.</span><span class="sxs-lookup"><span data-stu-id="211ba-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
