---
title: "Справочник по синтаксису aaaSQLRuleAction в Azure | Документы Microsoft"
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
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="9c957-103">Синтаксис SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="9c957-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="9c957-104">Объект *SqlRuleAction* является экземпляром типа hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) класс и представляет набор действий, написанные на языке SQL на основе синтаксиса, который выполняется относительно [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="9c957-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="9c957-105">В этом разделе перечислены сведения о hello SQL-грамматику действия правила.</span><span class="sxs-lookup"><span data-stu-id="9c957-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="9c957-106">Аргументы</span><span class="sxs-lookup"><span data-stu-id="9c957-106">Arguments</span></span>  
  
-   <span data-ttu-id="9c957-107">`<scope>`Необязательная строка, указывающее область hello hello является `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="9c957-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="9c957-108">Допустимые значения: `sys` и `user`.</span><span class="sxs-lookup"><span data-stu-id="9c957-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="9c957-109">Hello `sys` значение указывает область системы где `<property_name>` — имя открытого свойства hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="9c957-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="9c957-110">`user`Указывает область пользователя где `<property_name>` является ключ hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) словаря.</span><span class="sxs-lookup"><span data-stu-id="9c957-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="9c957-111">`user`область — область по умолчанию hello, если `<scope>` не указан.</span><span class="sxs-lookup"><span data-stu-id="9c957-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="9c957-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="9c957-112">Remarks</span></span>  

<span data-ttu-id="9c957-113">Попытка tooaccess несуществующий системное свойство, является ошибкой во время попытки tooaccess несуществующей пользователя свойство не является ошибкой.</span><span class="sxs-lookup"><span data-stu-id="9c957-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="9c957-114">Вместо этого несуществующее свойство пользователя вычисляется внутри системы как неизвестное значение.</span><span class="sxs-lookup"><span data-stu-id="9c957-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="9c957-115">Неизвестное значение обрабатывается особым образом во время вычисления оператора.</span><span class="sxs-lookup"><span data-stu-id="9c957-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="9c957-116">property_name</span><span class="sxs-lookup"><span data-stu-id="9c957-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="9c957-117">Аргументы</span><span class="sxs-lookup"><span data-stu-id="9c957-117">Arguments</span></span>  
 <span data-ttu-id="9c957-118">`<regular_identifier>`строки, представленной hello следовать регулярного выражения:</span><span class="sxs-lookup"><span data-stu-id="9c957-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="9c957-119">Это любая строка, которая начинается с буквы, после которой идет один или несколько символов подчеркивания, букв или цифр.</span><span class="sxs-lookup"><span data-stu-id="9c957-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="9c957-120">`[:IsLetter:]` — любой символ Юникода, который относится к категории букв Юникода.</span><span class="sxs-lookup"><span data-stu-id="9c957-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="9c957-121">`System.Char.IsLetter(c)` возвращает значение `true`, если `c` является буквой Юникода.</span><span class="sxs-lookup"><span data-stu-id="9c957-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="9c957-122">`[:IsDigit:]` — любой символ Юникода, который относится к категории десятичных цифр.</span><span class="sxs-lookup"><span data-stu-id="9c957-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="9c957-123">`System.Char.IsDigit(c)` возвращает значение `true`, если `c` является цифрой Юникода.</span><span class="sxs-lookup"><span data-stu-id="9c957-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="9c957-124">`<regular_identifier>` не может быть зарезервированным ключевым словом.</span><span class="sxs-lookup"><span data-stu-id="9c957-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="9c957-125">`<delimited_identifier>` — любая строка, заключенная в квадратные скобки ([]).</span><span class="sxs-lookup"><span data-stu-id="9c957-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="9c957-126">Закрывающая квадратная скобка представляется в виде двух закрывающих квадратных скобок.</span><span class="sxs-lookup"><span data-stu-id="9c957-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="9c957-127">Hello ниже приведены примеры `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="9c957-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="9c957-128">`<quoted_identifier>` — любая строка, заключенная в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="9c957-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="9c957-129">Двойные кавычки в идентификаторе представляются в виде двух пар двойных кавычек.</span><span class="sxs-lookup"><span data-stu-id="9c957-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="9c957-130">Не рекомендуется toouse заключенные в кавычки идентификаторы, так как его можно легко спутать с строковая константа.</span><span class="sxs-lookup"><span data-stu-id="9c957-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="9c957-131">По возможности используйте идентификаторы с разделителем.</span><span class="sxs-lookup"><span data-stu-id="9c957-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="9c957-132">Hello ниже приведен пример `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="9c957-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="9c957-133">pattern</span><span class="sxs-lookup"><span data-stu-id="9c957-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9c957-134">Примечания</span><span class="sxs-lookup"><span data-stu-id="9c957-134">Remarks</span></span>
  
 <span data-ttu-id="9c957-135">Свойство `<pattern>` должно быть выражением, которое будет вычисляться как строка.</span><span class="sxs-lookup"><span data-stu-id="9c957-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="9c957-136">Он используется в качестве шаблона для hello оператор LIKE.</span><span class="sxs-lookup"><span data-stu-id="9c957-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="9c957-137">Имя может содержать следующие символы-шаблоны hello:</span><span class="sxs-lookup"><span data-stu-id="9c957-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="9c957-138">`%` — любая строка без символов или с несколькими символами.</span><span class="sxs-lookup"><span data-stu-id="9c957-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="9c957-139">`_` — любой один символ.</span><span class="sxs-lookup"><span data-stu-id="9c957-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="9c957-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="9c957-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9c957-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="9c957-141">Remarks</span></span>
  
 <span data-ttu-id="9c957-142">Свойство `<escape_char>` должно быть выражением, которое будет вычисляться в качестве строки с 1 символом.</span><span class="sxs-lookup"><span data-stu-id="9c957-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="9c957-143">Он используется в качестве escape-символа для hello оператор LIKE.</span><span class="sxs-lookup"><span data-stu-id="9c957-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="9c957-144">Например, `property LIKE 'ABC\%' ESCAPE '\'` соответствует `ABC%`, а не строке, начинающейся с `ABC`.</span><span class="sxs-lookup"><span data-stu-id="9c957-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="9c957-145">константа</span><span class="sxs-lookup"><span data-stu-id="9c957-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="9c957-146">Аргументы</span><span class="sxs-lookup"><span data-stu-id="9c957-146">Arguments</span></span>  
  
-   <span data-ttu-id="9c957-147">`<integer_constant>` — строка чисел без кавычек и десятичного разделителя.</span><span class="sxs-lookup"><span data-stu-id="9c957-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="9c957-148">Hello значения хранятся в виде `System.Int64` внутренне, и выполните hello же диапазон.</span><span class="sxs-lookup"><span data-stu-id="9c957-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="9c957-149">Hello ниже приведены примеры констант long.</span><span class="sxs-lookup"><span data-stu-id="9c957-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="9c957-150">`<decimal_constant>` — строка чисел без кавычек с десятичным разделителем.</span><span class="sxs-lookup"><span data-stu-id="9c957-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="9c957-151">Hello значения хранятся в виде `System.Double` на внутреннем уровне и следовать hello же диапазон и точность.</span><span class="sxs-lookup"><span data-stu-id="9c957-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="9c957-152">В будущей версии это число может храниться в различных данных toosupport точное число семантику типа, поэтому не следует полагаться на hello фактов hello базовый тип данных является `System.Double` для `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="9c957-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="9c957-153">Hello ниже приведены примеры десятичных констант.</span><span class="sxs-lookup"><span data-stu-id="9c957-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="9c957-154">`<approximate_number_constant>` — число, записанное в экспоненциальном представлении чисел.</span><span class="sxs-lookup"><span data-stu-id="9c957-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="9c957-155">Hello значения хранятся в виде `System.Double` на внутреннем уровне и следовать hello же диапазон и точность.</span><span class="sxs-lookup"><span data-stu-id="9c957-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="9c957-156">Hello ниже приведены примеры приблизительные числовые константы.</span><span class="sxs-lookup"><span data-stu-id="9c957-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="9c957-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="9c957-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="9c957-158">Примечания</span><span class="sxs-lookup"><span data-stu-id="9c957-158">Remarks</span></span>
  
<span data-ttu-id="9c957-159">Ключевые слова hello представлены логических констант `TRUE` или `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="9c957-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="9c957-160">Hello значения хранятся в виде `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="9c957-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="9c957-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="9c957-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9c957-162">Примечания</span><span class="sxs-lookup"><span data-stu-id="9c957-162">Remarks</span></span>
  
<span data-ttu-id="9c957-163">Строковые константы заключаются в одинарные кавычки и включают любые допустимые символы Юникода.</span><span class="sxs-lookup"><span data-stu-id="9c957-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="9c957-164">Одинарная кавычка, внедренная в строковую константу, представляется в виде двух одинарных кавычек.</span><span class="sxs-lookup"><span data-stu-id="9c957-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="9c957-165">function</span><span class="sxs-lookup"><span data-stu-id="9c957-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="9c957-166">Примечания</span><span class="sxs-lookup"><span data-stu-id="9c957-166">Remarks</span></span>  

<span data-ttu-id="9c957-167">Hello `newid()` возврата функцией **System.Guid** созданные hello `System.Guid.NewGuid()` метод.</span><span class="sxs-lookup"><span data-stu-id="9c957-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="9c957-168">Hello `property(name)` функция возвращает значение свойства hello ссылается hello `name`.</span><span class="sxs-lookup"><span data-stu-id="9c957-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="9c957-169">Hello `name` значение может быть любое допустимое выражение, возвращающее строковое значение.</span><span class="sxs-lookup"><span data-stu-id="9c957-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="9c957-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="9c957-170">Considerations</span></span>

- <span data-ttu-id="9c957-171">НАБОР — используется toocreate новое значение свойства или обновление hello существующего свойства.</span><span class="sxs-lookup"><span data-stu-id="9c957-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="9c957-172">Удаление — tooremove используется свойство.</span><span class="sxs-lookup"><span data-stu-id="9c957-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="9c957-173">НАБОР по возможности выполняет неявное преобразование, когда тип выражения hello и hello существующий тип свойства отличаются.</span><span class="sxs-lookup"><span data-stu-id="9c957-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="9c957-174">Если ссылка указывает на несуществующие свойства системы, действие завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="9c957-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="9c957-175">Если ссылка указывает на несуществующие свойства пользователя, действие не завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="9c957-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="9c957-176">Свойство пользователя несуществующий вычисляется как «Неизвестно» внутренне, следующие hello же семантику, что [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) при вычислении операторов.</span><span class="sxs-lookup"><span data-stu-id="9c957-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c957-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c957-177">Next steps</span></span>

- <span data-ttu-id="9c957-178">[SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) (Класс SQLRuleAction)</span><span class="sxs-lookup"><span data-stu-id="9c957-178">[SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)</span></span>
- <span data-ttu-id="9c957-179">[SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) (Класс SQLFilter)</span><span class="sxs-lookup"><span data-stu-id="9c957-179">[SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)</span></span>
