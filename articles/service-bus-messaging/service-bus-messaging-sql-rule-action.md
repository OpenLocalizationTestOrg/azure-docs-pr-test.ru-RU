---
title: "Справочник по синтаксису SQLRuleAction в Azure | Документация Майкрософт"
description: "Сведения о грамматике SQLRuleAction."
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="7974e-103">Синтаксис SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="7974e-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="7974e-104">*SqlRuleAction* — это экземпляр класса [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction). Он представляет набор действий, написанных по правилам синтаксиса на основе языка SQL, выполняемых с [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="7974e-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="7974e-105">В этой статье приведены сведения о грамматике действия правила SQL.</span><span class="sxs-lookup"><span data-stu-id="7974e-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
## <a name="arguments"></a><span data-ttu-id="7974e-106">Аргументы</span><span class="sxs-lookup"><span data-stu-id="7974e-106">Arguments</span></span>  
  
-   <span data-ttu-id="7974e-107">`<scope>` — необязательная строка, указывающая область `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="7974e-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="7974e-108">Допустимые значения: `sys` и `user`.</span><span class="sxs-lookup"><span data-stu-id="7974e-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="7974e-109">Значение `sys` указывает область системы, где `<property_name>` — имя общедоступного свойства [класса BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="7974e-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="7974e-110">Значение `user` указывает область пользователя, где `<property_name>` — ключ словаря [класса BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="7974e-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="7974e-111">Область `user` используется по умолчанию, если аргумент `<scope>` не указан.</span><span class="sxs-lookup"><span data-stu-id="7974e-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="7974e-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="7974e-112">Remarks</span></span>  

<span data-ttu-id="7974e-113">Попытка доступа к несуществующему системному свойству вызывает ошибку, а попытка доступа к несуществующему свойству пользователя — нет.</span><span class="sxs-lookup"><span data-stu-id="7974e-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="7974e-114">Вместо этого несуществующее свойство пользователя вычисляется внутри системы как неизвестное значение.</span><span class="sxs-lookup"><span data-stu-id="7974e-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="7974e-115">Неизвестное значение обрабатывается особым образом во время вычисления оператора.</span><span class="sxs-lookup"><span data-stu-id="7974e-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="7974e-116">property_name</span><span class="sxs-lookup"><span data-stu-id="7974e-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="7974e-117">Аргументы</span><span class="sxs-lookup"><span data-stu-id="7974e-117">Arguments</span></span>  
 <span data-ttu-id="7974e-118">`<regular_identifier>` — строка, представленная следующим регулярным выражением:</span><span class="sxs-lookup"><span data-stu-id="7974e-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="7974e-119">Это любая строка, которая начинается с буквы, после которой идет один или несколько символов подчеркивания, букв или цифр.</span><span class="sxs-lookup"><span data-stu-id="7974e-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="7974e-120">`[:IsLetter:]` — любой символ Юникода, который относится к категории букв Юникода.</span><span class="sxs-lookup"><span data-stu-id="7974e-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="7974e-121">`System.Char.IsLetter(c)` возвращает значение `true`, если `c` является буквой Юникода.</span><span class="sxs-lookup"><span data-stu-id="7974e-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="7974e-122">`[:IsDigit:]` — любой символ Юникода, который относится к категории десятичных цифр.</span><span class="sxs-lookup"><span data-stu-id="7974e-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="7974e-123">`System.Char.IsDigit(c)` возвращает значение `true`, если `c` является цифрой Юникода.</span><span class="sxs-lookup"><span data-stu-id="7974e-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="7974e-124">`<regular_identifier>` не может быть зарезервированным ключевым словом.</span><span class="sxs-lookup"><span data-stu-id="7974e-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="7974e-125">`<delimited_identifier>` — любая строка, заключенная в квадратные скобки ([]).</span><span class="sxs-lookup"><span data-stu-id="7974e-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="7974e-126">Закрывающая квадратная скобка представляется в виде двух закрывающих квадратных скобок.</span><span class="sxs-lookup"><span data-stu-id="7974e-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="7974e-127">Ниже приведены примеры `<delimited_identifier>`.</span><span class="sxs-lookup"><span data-stu-id="7974e-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="7974e-128">`<quoted_identifier>` — любая строка, заключенная в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="7974e-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="7974e-129">Двойные кавычки в идентификаторе представляются в виде двух пар двойных кавычек.</span><span class="sxs-lookup"><span data-stu-id="7974e-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="7974e-130">Мы не рекомендуем использовать заключенные в кавычки идентификаторы, так как их можно легко спутать со строковой константой.</span><span class="sxs-lookup"><span data-stu-id="7974e-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="7974e-131">По возможности используйте идентификаторы с разделителем.</span><span class="sxs-lookup"><span data-stu-id="7974e-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="7974e-132">Ниже приведен пример `<quoted_identifier>`.</span><span class="sxs-lookup"><span data-stu-id="7974e-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="7974e-133">pattern</span><span class="sxs-lookup"><span data-stu-id="7974e-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="7974e-134">Примечания</span><span class="sxs-lookup"><span data-stu-id="7974e-134">Remarks</span></span>
  
 <span data-ttu-id="7974e-135">Свойство `<pattern>` должно быть выражением, которое будет вычисляться как строка.</span><span class="sxs-lookup"><span data-stu-id="7974e-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="7974e-136">Оно используется в качестве шаблона для оператора LIKE.</span><span class="sxs-lookup"><span data-stu-id="7974e-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="7974e-137">Оно может содержать следующие подстановочные знаки:</span><span class="sxs-lookup"><span data-stu-id="7974e-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="7974e-138">`%` — любая строка без символов или с несколькими символами.</span><span class="sxs-lookup"><span data-stu-id="7974e-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="7974e-139">`_` — любой один символ.</span><span class="sxs-lookup"><span data-stu-id="7974e-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="7974e-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="7974e-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="7974e-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="7974e-141">Remarks</span></span>
  
 <span data-ttu-id="7974e-142">Свойство `<escape_char>` должно быть выражением, которое будет вычисляться в качестве строки с 1 символом.</span><span class="sxs-lookup"><span data-stu-id="7974e-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="7974e-143">Оно используется в качестве escape-символа для оператора LIKE.</span><span class="sxs-lookup"><span data-stu-id="7974e-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="7974e-144">Например, `property LIKE 'ABC\%' ESCAPE '\'` соответствует `ABC%`, а не строке, начинающейся с `ABC`.</span><span class="sxs-lookup"><span data-stu-id="7974e-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="7974e-145">константа</span><span class="sxs-lookup"><span data-stu-id="7974e-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="7974e-146">Аргументы</span><span class="sxs-lookup"><span data-stu-id="7974e-146">Arguments</span></span>  
  
-   <span data-ttu-id="7974e-147">`<integer_constant>` — строка чисел без кавычек и десятичного разделителя.</span><span class="sxs-lookup"><span data-stu-id="7974e-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="7974e-148">Значения хранятся в виде `System.Int64` внутри системы и попадают в тот же диапазон.</span><span class="sxs-lookup"><span data-stu-id="7974e-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="7974e-149">Ниже приведены примеры длинных констант.</span><span class="sxs-lookup"><span data-stu-id="7974e-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="7974e-150">`<decimal_constant>` — строка чисел без кавычек с десятичным разделителем.</span><span class="sxs-lookup"><span data-stu-id="7974e-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="7974e-151">Значения хранятся в виде `System.Double` внутри системы и попадают в тот же диапазон и точность.</span><span class="sxs-lookup"><span data-stu-id="7974e-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="7974e-152">В следующих версиях это число может храниться в другом типе данных для обеспечения поддержки более точной числовой семантики. Поэтому не следует полагаться на тот факт, что базовый тип данных для `<decimal_constant>` — `System.Double`.</span><span class="sxs-lookup"><span data-stu-id="7974e-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="7974e-153">Ниже приведены примеры десятичных констант.</span><span class="sxs-lookup"><span data-stu-id="7974e-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="7974e-154">`<approximate_number_constant>` — число, записанное в экспоненциальном представлении чисел.</span><span class="sxs-lookup"><span data-stu-id="7974e-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="7974e-155">Значения хранятся в виде `System.Double` внутри системы и попадают в тот же диапазон и точность.</span><span class="sxs-lookup"><span data-stu-id="7974e-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="7974e-156">Ниже приведены примеры констант с приближенными числами.</span><span class="sxs-lookup"><span data-stu-id="7974e-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="7974e-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="7974e-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="7974e-158">Примечания</span><span class="sxs-lookup"><span data-stu-id="7974e-158">Remarks</span></span>
  
<span data-ttu-id="7974e-159">Логические константы представлены в виде ключевого слова `TRUE` или `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="7974e-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="7974e-160">Значения хранятся в виде `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="7974e-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="7974e-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="7974e-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="7974e-162">Примечания</span><span class="sxs-lookup"><span data-stu-id="7974e-162">Remarks</span></span>
  
<span data-ttu-id="7974e-163">Строковые константы заключаются в одинарные кавычки и включают любые допустимые символы Юникода.</span><span class="sxs-lookup"><span data-stu-id="7974e-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="7974e-164">Одинарная кавычка, внедренная в строковую константу, представляется в виде двух одинарных кавычек.</span><span class="sxs-lookup"><span data-stu-id="7974e-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="7974e-165">function</span><span class="sxs-lookup"><span data-stu-id="7974e-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="7974e-166">Примечания</span><span class="sxs-lookup"><span data-stu-id="7974e-166">Remarks</span></span>  

<span data-ttu-id="7974e-167">Функция `newid()` возвращает значение **System.Guid**, созданное методом `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="7974e-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="7974e-168">Функция `property(name)` возвращает значение свойства, на которое указывает `name`.</span><span class="sxs-lookup"><span data-stu-id="7974e-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="7974e-169">В качестве значения `name` может использоваться любое допустимое выражение, возвращающее строковое значение.</span><span class="sxs-lookup"><span data-stu-id="7974e-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="7974e-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="7974e-170">Considerations</span></span>

- <span data-ttu-id="7974e-171">Оператор SET используется для создания свойства или обновления значения имеющегося свойства.</span><span class="sxs-lookup"><span data-stu-id="7974e-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="7974e-172">Оператор REMOVE используется для удаления свойства.</span><span class="sxs-lookup"><span data-stu-id="7974e-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="7974e-173">По возможности оператор SET выполняет неявное преобразование, если тип выражения и тип имеющегося свойства отличаются.</span><span class="sxs-lookup"><span data-stu-id="7974e-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="7974e-174">Если ссылка указывает на несуществующие свойства системы, действие завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="7974e-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="7974e-175">Если ссылка указывает на несуществующие свойства пользователя, действие не завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="7974e-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="7974e-176">Несуществующее свойство пользователя вычисляется внутри системы как неизвестное значение с использованием той же семантики, что и [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) при вычислении операторов.</span><span class="sxs-lookup"><span data-stu-id="7974e-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7974e-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7974e-177">Next steps</span></span>

- <span data-ttu-id="7974e-178">[SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) (Класс SQLRuleAction)</span><span class="sxs-lookup"><span data-stu-id="7974e-178">[SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)</span></span>
- <span data-ttu-id="7974e-179">[SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) (Класс SQLFilter)</span><span class="sxs-lookup"><span data-stu-id="7974e-179">[SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)</span></span>
