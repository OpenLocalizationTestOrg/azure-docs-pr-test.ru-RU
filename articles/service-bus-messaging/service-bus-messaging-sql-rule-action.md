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
# <a name="sqlruleaction-syntax"></a>Синтаксис SQLRuleAction

Объект *SqlRuleAction* является экземпляром типа hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) класс и представляет набор действий, написанные на языке SQL на основе синтаксиса, который выполняется относительно [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
В этом разделе перечислены сведения о hello SQL-грамматику действия правила.  
  
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
  
## <a name="arguments"></a>Аргументы  
  
-   `<scope>`Необязательная строка, указывающее область hello hello является `<property_name>`. Допустимые значения: `sys` и `user`. Hello `sys` значение указывает область системы где `<property_name>` — имя открытого свойства hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`Указывает область пользователя где `<property_name>` является ключ hello [класс BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) словаря. `user`область — область по умолчанию hello, если `<scope>` не указан.  
  
### <a name="remarks"></a>Примечания  

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
  
     Hello ниже приведены примеры констант long.  
  
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
  
Ключевые слова hello представлены логических констант `TRUE` или `FALSE`. Hello значения хранятся в виде `System.Boolean`.  
  
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

- НАБОР — используется toocreate новое значение свойства или обновление hello существующего свойства.
- Удаление — tooremove используется свойство.
- НАБОР по возможности выполняет неявное преобразование, когда тип выражения hello и hello существующий тип свойства отличаются.
- Если ссылка указывает на несуществующие свойства системы, действие завершается сбоем.
- Если ссылка указывает на несуществующие свойства пользователя, действие не завершается сбоем.
- Свойство пользователя несуществующий вычисляется как «Неизвестно» внутренне, следующие hello же семантику, что [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) при вычислении операторов.

## <a name="next-steps"></a>Дальнейшие действия

- [SQLRuleAction class](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) (Класс SQLRuleAction)
- [SQLFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) (Класс SQLFilter)
