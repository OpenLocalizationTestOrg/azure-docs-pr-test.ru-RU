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
# <a name="sqlfilter-syntax"></a>Синтаксис SQLFilter

Объект *SqlFilter* является экземпляром типа hello [класса SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)и представляет выражение фильтра на основе языка SQL, которое оценивается [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). SqlFilter поддерживает подмножество стандарта SQL-92 hello.  
  
 В этом разделе приведены сведения о грамматике SqlFilter.  
  
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
  
## <a name="arguments"></a>Аргументы  
  
-   `<scope>`Необязательная строка, указывающее область hello hello является `<property_name>`. Допустимые значения: `sys` и `user`. Hello `sys` значение указывает область системы где `<property_name>` — имя открытого свойства hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`Указывает область пользователя где `<property_name>` является ключ hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) словаря. `user`область — область по умолчанию hello, если `<scope>` не указан.  
  
## <a name="remarks"></a>Примечания

Попытка tooaccess несуществующий системное свойство, является ошибкой во время попытки tooaccess несуществующей пользователя свойство не является ошибкой. Вместо этого несуществующее свойство пользователя вычисляется внутри системы как неизвестное значение. Неизвестное значение обрабатывается особым образом во время вычисления оператора.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Аргументы  

 `<regular_identifier>`строки, представленной hello следовать регулярного выражения:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Это любая строка, которая начинается с буквы, после которой идет один или несколько символов подчеркивания, букв или цифр.  
  
`[:IsLetter:]` — любой символ Юникода, который относится к категории букв Юникода. `System.Char.IsLetter(c)` возвращает значение `true`, если `c` является буквой Юникода.  
  
`[:IsDigit:]` — любой символ Юникода, который относится к категории десятичных цифр. `System.Char.IsDigit(c)` возвращает значение `true`, если `c` является цифрой Юникода.  
  
`<regular_identifier>` не может быть зарезервированным ключевым словом.  
  
`<delimited_identifier>` — любая строка, заключенная в квадратные скобки ([]). Закрывающая квадратная скобка представляется в виде двух закрывающих квадратных скобок. Hello ниже приведены примеры `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>` — любая строка, заключенная в двойные кавычки. Двойные кавычки в идентификаторе представляются в виде двух пар двойных кавычек. Не рекомендуется toouse заключенные в кавычки идентификаторы, так как его можно легко спутать с строковая константа. По возможности используйте идентификаторы с разделителем. Hello ниже приведен пример `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>pattern  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Примечания
  
Свойство `<pattern>` должно быть выражением, которое будет вычисляться как строка. Он используется в качестве шаблона для hello оператор LIKE.      Имя может содержать следующие символы-шаблоны hello:  
  
-   `%` — любая строка без символов или с несколькими символами.  
  
-   `_` — любой один символ.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Примечания  

Свойство `<escape_char>` должно быть выражением, которое будет вычисляться в качестве строки с 1 символом. Он используется в качестве escape-символа для hello оператор LIKE.  
  
 Например, `property LIKE 'ABC\%' ESCAPE '\'` соответствует `ABC%`, а не строке, начинающейся с `ABC`.  
  
## <a name="constant"></a>константа  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Аргументы  
  
-   `<integer_constant>` — строка чисел без кавычек и десятичного разделителя. Hello значения хранятся в виде `System.Int64` внутренне, и выполните hello же диапазон.  
  
     Ниже приведены примеры длинных констант.  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>` — строка чисел без кавычек с десятичным разделителем. Hello значения хранятся в виде `System.Double` на внутреннем уровне и следовать hello же диапазон и точность.  
  
     В будущей версии это число может храниться в различных данных toosupport точное число семантику типа, поэтому не следует полагаться на hello фактов hello базовый тип данных является `System.Double` для `<decimal_constant>`.  
  
     Hello ниже приведены примеры десятичных констант.  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>` — число, записанное в экспоненциальном представлении чисел. Hello значения хранятся в виде `System.Double` на внутреннем уровне и следовать hello же диапазон и точность. Hello ниже приведены примеры приблизительные числовые константы.  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Примечания  

Ключевые слова hello представлены логических констант **TRUE** или **FALSE**. Hello значения хранятся в виде `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Примечания  

Строковые константы заключаются в одинарные кавычки и включают любые допустимые символы Юникода. Одинарная кавычка, внедренная в строковую константу, представляется в виде двух одинарных кавычек.  
  
## <a name="function"></a>function  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Примечания
  
Hello `newid()` возврата функцией **System.Guid** созданные hello `System.Guid.NewGuid()` метод.  
  
Hello `property(name)` функция возвращает значение свойства hello ссылается hello `name`. Hello `name` значение может быть любое допустимое выражение, возвращающее строковое значение.  
  
## <a name="considerations"></a>Рекомендации
  
Рассмотрим следующие hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) семантику:  
  
-   В именах свойств не учитывается регистр.  
  
-   Во всех сценариях операторы следуют семантике неявного преобразования C#.  
  
-   Системные свойства являются общедоступными свойствами, используемыми в экземплярах [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).  
  
    Рассмотрим следующие hello `IS [NOT] NULL` семантику:  
  
    -   `property IS NULL`вычисляется как `true` Если одно из свойств hello не существует или hello значение свойства `null`.  
  
### <a name="property-evaluation-semantics"></a>Семантика оценки свойств  
  
-   Попытка tooevaluate несуществующий системное свойство вызывает [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) исключение.  
  
-   Несуществующее свойство вычисляется внутри системы как **неизвестное**.  
  
 Вычисление неизвестного свойства в арифметических операторах:  
  
-   Для бинарных операторов, если либо hello левым и правым операндов оценивается как **Неизвестный**, hello результатом является **Неизвестный**.  
  
-   Для унарных операторов, если операнд вычисляется как **Неизвестный**, то результат hello **Неизвестный**.  
  
 Неизвестный результат вычисления в двоичных операторах сравнения:  
  
-   Если либо hello левым и правым операндов оценивается как **Неизвестный**, hello результатом является **Неизвестный**.  
  
 Неизвестный результат вычисления в `[NOT] LIKE`:  
  
-   Если любой операнд вычисляется как **Неизвестный**, hello результатом является **Неизвестный**.  
  
 Неизвестный результат вычисления в `[NOT] IN`:  
  
-   Если левый операнд hello вычисляется как **Неизвестный**, hello результатом является **Неизвестный**.  
  
 Неизвестный результат вычисления в операторе **AND**:  
  
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
  
 Неизвестный результат вычисления в операторе **OR**:  
  
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
  
### <a name="operator-binding-semantics"></a>Семантика привязки операторов
  
-   Операторы сравнения, такие как `>`, `>=`, `<`, `<=`, `!=`, и `=` выполните hello же семантику, что оператор hello C#, привязка данных введите повышений и неявные преобразования.  
  
-   Арифметические операторы, такие как `+`, `-`, `*`, `/`, и `%` выполните hello же семантику, что оператор hello C#, привязка данных введите повышений и неявные преобразования.

## <a name="next-steps"></a>Дальнейшие действия

- [SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) (Класс SQLFilter)
- [SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) (Класс SQLRuleAction)