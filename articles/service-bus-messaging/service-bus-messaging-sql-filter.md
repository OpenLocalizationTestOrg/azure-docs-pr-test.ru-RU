---
title: "Справочник по синтаксису Service Bus SQLFilter aaaAzure | Документы Microsoft"
description: "Сведения о грамматике SQLFilter."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="62a6b-103">Синтаксис SQLFilter</span><span class="sxs-lookup"><span data-stu-id="62a6b-103">SQLFilter syntax</span></span>

<span data-ttu-id="62a6b-104">Объект *SqlFilter* является экземпляром типа hello [класса SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)и представляет выражение фильтра на основе языка SQL, которое оценивается [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="62a6b-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="62a6b-105">SqlFilter поддерживает подмножество стандарта SQL-92 hello.</span><span class="sxs-lookup"><span data-stu-id="62a6b-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="62a6b-106">В этом разделе приведены сведения о грамматике SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="62a6b-106">This topic lists details about SqlFilter grammar.</span></span>  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a><span data-ttu-id="62a6b-107">Аргументы</span><span class="sxs-lookup"><span data-stu-id="62a6b-107">Arguments</span></span>  
  
-   <span data-ttu-id="62a6b-108">`<scope>`Необязательная строка, указывающее область hello hello является `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="62a6b-109">Допустимые значения: `sys` и `user`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="62a6b-110">Hello `sys` значение указывает область системы где `<property_name>` — имя открытого свойства hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="62a6b-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="62a6b-111">`user`Указывает область пользователя где `<property_name>` является ключ hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) словаря.</span><span class="sxs-lookup"><span data-stu-id="62a6b-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="62a6b-112">`user`область — область по умолчанию hello, если `<scope>` не указан.</span><span class="sxs-lookup"><span data-stu-id="62a6b-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="62a6b-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="62a6b-113">Remarks</span></span>

<span data-ttu-id="62a6b-114">Попытка tooaccess несуществующий системное свойство, является ошибкой во время попытки tooaccess несуществующей пользователя свойство не является ошибкой.</span><span class="sxs-lookup"><span data-stu-id="62a6b-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="62a6b-115">Вместо этого несуществующее свойство пользователя вычисляется внутри системы как неизвестное значение.</span><span class="sxs-lookup"><span data-stu-id="62a6b-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="62a6b-116">Неизвестное значение обрабатывается особым образом во время вычисления оператора.</span><span class="sxs-lookup"><span data-stu-id="62a6b-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="62a6b-117">property_name</span><span class="sxs-lookup"><span data-stu-id="62a6b-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="62a6b-118">Аргументы</span><span class="sxs-lookup"><span data-stu-id="62a6b-118">Arguments</span></span>  

 <span data-ttu-id="62a6b-119">`<regular_identifier>`строки, представленной hello следовать регулярного выражения:</span><span class="sxs-lookup"><span data-stu-id="62a6b-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="62a6b-120">Это любая строка, которая начинается с буквы, после которой идет один или несколько символов подчеркивания, букв или цифр.</span><span class="sxs-lookup"><span data-stu-id="62a6b-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="62a6b-121">`[:IsLetter:]` — любой символ Юникода, который относится к категории букв Юникода.</span><span class="sxs-lookup"><span data-stu-id="62a6b-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="62a6b-122">`System.Char.IsLetter(c)` возвращает значение `true`, если `c` является буквой Юникода.</span><span class="sxs-lookup"><span data-stu-id="62a6b-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="62a6b-123">`[:IsDigit:]` — любой символ Юникода, который относится к категории десятичных цифр.</span><span class="sxs-lookup"><span data-stu-id="62a6b-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="62a6b-124">`System.Char.IsDigit(c)` возвращает значение `true`, если `c` является цифрой Юникода.</span><span class="sxs-lookup"><span data-stu-id="62a6b-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="62a6b-125">`<regular_identifier>` не может быть зарезервированным ключевым словом.</span><span class="sxs-lookup"><span data-stu-id="62a6b-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="62a6b-126">`<delimited_identifier>` — любая строка, заключенная в квадратные скобки ([]).</span><span class="sxs-lookup"><span data-stu-id="62a6b-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="62a6b-127">Закрывающая квадратная скобка представляется в виде двух закрывающих квадратных скобок.</span><span class="sxs-lookup"><span data-stu-id="62a6b-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="62a6b-128">Hello ниже приведены примеры `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="62a6b-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="62a6b-129">`<quoted_identifier>` — любая строка, заключенная в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="62a6b-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="62a6b-130">Двойные кавычки в идентификаторе представляются в виде двух пар двойных кавычек.</span><span class="sxs-lookup"><span data-stu-id="62a6b-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="62a6b-131">Не рекомендуется toouse заключенные в кавычки идентификаторы, так как его можно легко спутать с строковая константа.</span><span class="sxs-lookup"><span data-stu-id="62a6b-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="62a6b-132">По возможности используйте идентификаторы с разделителем.</span><span class="sxs-lookup"><span data-stu-id="62a6b-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="62a6b-133">Hello ниже приведен пример `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="62a6b-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="62a6b-134">pattern</span><span class="sxs-lookup"><span data-stu-id="62a6b-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="62a6b-135">Примечания</span><span class="sxs-lookup"><span data-stu-id="62a6b-135">Remarks</span></span>
  
<span data-ttu-id="62a6b-136">Свойство `<pattern>` должно быть выражением, которое будет вычисляться как строка.</span><span class="sxs-lookup"><span data-stu-id="62a6b-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="62a6b-137">Он используется в качестве шаблона для hello оператор LIKE.</span><span class="sxs-lookup"><span data-stu-id="62a6b-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="62a6b-138">Имя может содержать следующие символы-шаблоны hello:</span><span class="sxs-lookup"><span data-stu-id="62a6b-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="62a6b-139">`%` — любая строка без символов или с несколькими символами.</span><span class="sxs-lookup"><span data-stu-id="62a6b-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="62a6b-140">`_` — любой один символ.</span><span class="sxs-lookup"><span data-stu-id="62a6b-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="62a6b-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="62a6b-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="62a6b-142">Примечания</span><span class="sxs-lookup"><span data-stu-id="62a6b-142">Remarks</span></span>  

<span data-ttu-id="62a6b-143">Свойство `<escape_char>` должно быть выражением, которое будет вычисляться в качестве строки с 1 символом.</span><span class="sxs-lookup"><span data-stu-id="62a6b-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="62a6b-144">Он используется в качестве escape-символа для hello оператор LIKE.</span><span class="sxs-lookup"><span data-stu-id="62a6b-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="62a6b-145">Например, `property LIKE 'ABC\%' ESCAPE '\'` соответствует `ABC%`, а не строке, начинающейся с `ABC`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="62a6b-146">константа</span><span class="sxs-lookup"><span data-stu-id="62a6b-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="62a6b-147">Аргументы</span><span class="sxs-lookup"><span data-stu-id="62a6b-147">Arguments</span></span>  
  
-   <span data-ttu-id="62a6b-148">`<integer_constant>` — строка чисел без кавычек и десятичного разделителя.</span><span class="sxs-lookup"><span data-stu-id="62a6b-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="62a6b-149">Hello значения хранятся в виде `System.Int64` внутренне, и выполните hello же диапазон.</span><span class="sxs-lookup"><span data-stu-id="62a6b-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="62a6b-150">Ниже приведены примеры длинных констант.</span><span class="sxs-lookup"><span data-stu-id="62a6b-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="62a6b-151">`<decimal_constant>` — строка чисел без кавычек с десятичным разделителем.</span><span class="sxs-lookup"><span data-stu-id="62a6b-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="62a6b-152">Hello значения хранятся в виде `System.Double` на внутреннем уровне и следовать hello же диапазон и точность.</span><span class="sxs-lookup"><span data-stu-id="62a6b-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="62a6b-153">В будущей версии это число может храниться в различных данных toosupport точное число семантику типа, поэтому не следует полагаться на hello фактов hello базовый тип данных является `System.Double` для `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="62a6b-154">Hello ниже приведены примеры десятичных констант.</span><span class="sxs-lookup"><span data-stu-id="62a6b-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="62a6b-155">`<approximate_number_constant>` — число, записанное в экспоненциальном представлении чисел.</span><span class="sxs-lookup"><span data-stu-id="62a6b-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="62a6b-156">Hello значения хранятся в виде `System.Double` на внутреннем уровне и следовать hello же диапазон и точность.</span><span class="sxs-lookup"><span data-stu-id="62a6b-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="62a6b-157">Hello ниже приведены примеры приблизительные числовые константы.</span><span class="sxs-lookup"><span data-stu-id="62a6b-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="62a6b-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="62a6b-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="62a6b-159">Примечания</span><span class="sxs-lookup"><span data-stu-id="62a6b-159">Remarks</span></span>  

<span data-ttu-id="62a6b-160">Ключевые слова hello представлены логических констант **TRUE** или **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="62a6b-161">Hello значения хранятся в виде `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="62a6b-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="62a6b-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="62a6b-163">Примечания</span><span class="sxs-lookup"><span data-stu-id="62a6b-163">Remarks</span></span>  

<span data-ttu-id="62a6b-164">Строковые константы заключаются в одинарные кавычки и включают любые допустимые символы Юникода.</span><span class="sxs-lookup"><span data-stu-id="62a6b-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="62a6b-165">Одинарная кавычка, внедренная в строковую константу, представляется в виде двух одинарных кавычек.</span><span class="sxs-lookup"><span data-stu-id="62a6b-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="62a6b-166">function</span><span class="sxs-lookup"><span data-stu-id="62a6b-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="62a6b-167">Примечания</span><span class="sxs-lookup"><span data-stu-id="62a6b-167">Remarks</span></span>
  
<span data-ttu-id="62a6b-168">Hello `newid()` возврата функцией **System.Guid** созданные hello `System.Guid.NewGuid()` метод.</span><span class="sxs-lookup"><span data-stu-id="62a6b-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="62a6b-169">Hello `property(name)` функция возвращает значение свойства hello ссылается hello `name`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="62a6b-170">Hello `name` значение может быть любое допустимое выражение, возвращающее строковое значение.</span><span class="sxs-lookup"><span data-stu-id="62a6b-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="62a6b-171">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="62a6b-171">Considerations</span></span>
  
<span data-ttu-id="62a6b-172">Рассмотрим следующие hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) семантику:</span><span class="sxs-lookup"><span data-stu-id="62a6b-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="62a6b-173">В именах свойств не учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="62a6b-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="62a6b-174">Во всех сценариях операторы следуют семантике неявного преобразования C#.</span><span class="sxs-lookup"><span data-stu-id="62a6b-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="62a6b-175">Системные свойства являются общедоступными свойствами, используемыми в экземплярах [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="62a6b-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="62a6b-176">Рассмотрим следующие hello `IS [NOT] NULL` семантику:</span><span class="sxs-lookup"><span data-stu-id="62a6b-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="62a6b-177">`property IS NULL`вычисляется как `true` Если одно из свойств hello не существует или hello значение свойства `null`.</span><span class="sxs-lookup"><span data-stu-id="62a6b-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="62a6b-178">Семантика оценки свойств</span><span class="sxs-lookup"><span data-stu-id="62a6b-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="62a6b-179">Попытка tooevaluate несуществующий системное свойство вызывает [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) исключение.</span><span class="sxs-lookup"><span data-stu-id="62a6b-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="62a6b-180">Несуществующее свойство вычисляется внутри системы как **неизвестное**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="62a6b-181">Вычисление неизвестного свойства в арифметических операторах:</span><span class="sxs-lookup"><span data-stu-id="62a6b-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="62a6b-182">Для бинарных операторов, если либо hello левым и правым операндов оценивается как **Неизвестный**, hello результатом является **Неизвестный**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="62a6b-183">Для унарных операторов, если операнд вычисляется как **Неизвестный**, то результат hello **Неизвестный**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="62a6b-184">Неизвестный результат вычисления в двоичных операторах сравнения:</span><span class="sxs-lookup"><span data-stu-id="62a6b-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="62a6b-185">Если либо hello левым и правым операндов оценивается как **Неизвестный**, hello результатом является **Неизвестный**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="62a6b-186">Неизвестный результат вычисления в `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="62a6b-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="62a6b-187">Если любой операнд вычисляется как **Неизвестный**, hello результатом является **Неизвестный**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="62a6b-188">Неизвестный результат вычисления в `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="62a6b-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="62a6b-189">Если левый операнд hello вычисляется как **Неизвестный**, hello результатом является **Неизвестный**.</span><span class="sxs-lookup"><span data-stu-id="62a6b-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="62a6b-190">Неизвестный результат вычисления в операторе **AND**:</span><span class="sxs-lookup"><span data-stu-id="62a6b-190">Unknown evaluation in **AND** operator:</span></span>  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 <span data-ttu-id="62a6b-191">Неизвестный результат вычисления в операторе **OR**:</span><span class="sxs-lookup"><span data-stu-id="62a6b-191">Unknown evaluation in **OR** operator:</span></span>  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="62a6b-192">Семантика привязки операторов</span><span class="sxs-lookup"><span data-stu-id="62a6b-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="62a6b-193">Операторы сравнения, такие как `>`, `>=`, `<`, `<=`, `!=`, и `=` выполните hello же семантику, что оператор hello C#, привязка данных введите повышений и неявные преобразования.</span><span class="sxs-lookup"><span data-stu-id="62a6b-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="62a6b-194">Арифметические операторы, такие как `+`, `-`, `*`, `/`, и `%` выполните hello же семантику, что оператор hello C#, привязка данных введите повышений и неявные преобразования.</span><span class="sxs-lookup"><span data-stu-id="62a6b-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62a6b-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62a6b-195">Next steps</span></span>

- <span data-ttu-id="62a6b-196">[SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) (Класс SQLFilter)</span><span class="sxs-lookup"><span data-stu-id="62a6b-196">[SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)</span></span>
- <span data-ttu-id="62a6b-197">[SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) (Класс SQLRuleAction)</span><span class="sxs-lookup"><span data-stu-id="62a6b-197">[SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)</span></span>