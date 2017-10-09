---
title: "определяемые пользователем функции aaaAzure Stream Analytics JavaScript | Документы Microsoft"
description: "Выполнение расширенных запросов с помощью определяемых пользователем функций JavaScript"
keywords: "javascript, определяемые пользователем функции, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Определяемые пользователем функции JavaScript в Azure Stream Analytics
Azure Stream Analytics поддерживает определяемые пользователем функции, написанные на языке JavaScript. С hello богатый набор **строка**, **RegExp**, **математические**, **массива**, и **даты** методы, Преобразования сложных данных с помощью задания Stream Analytics предоставляет JavaScript, и становятся проще toocreate.

## <a name="javascript-user-defined-functions"></a>Определяемые пользователем функции JavaScript
Определяемые пользователем функции JavaScript поддерживают скалярные вычислительные функции без отслеживания состояния, не требующие внешнего подключения. Hello возвращаемое значение функции может быть только скалярное значение (одно). После добавления задания tooa определяемой пользователем функции JavaScript, можно использовать функции hello в любом месте в hello запрос, подобный встроенной скалярной функции.

Ниже приведены некоторые сценарии, в которых могут пригодиться определяемые пользователем функции JavaScript.
* Анализ и обработка строки с использованием функций регулярных выражений, например **Regexp_Replace()** или **Regexp_Extract()**.
* Декодирование и кодирование данных, например преобразование двоичных данных в шестнадцатеричные.
* Математические вычисления с помощью объекта JavaScript **Math**.
* Операции с массивами, такие как сортировка, присоединение, поиск и заполнение.

Вот некоторые действия, которые невозможно выполнить в Stream Analytics с помощью определяемой пользователем функции JavaScript.
* Вызов внешних конечных точек REST, например выполнение обратного разрешения IP-адресов или извлечение ссылочных данных из внешнего источника.
* Сериализация или десериализация входных и выходных данных в пользовательский формат сообщения.
* Создание пользовательских статистических функций.

Несмотря на то, что функции, например **Date.GetDate()** или **Math.random()** не блокируются в определении функции hello, следует избегать их использования. Эти функции **не** возвращаемого hello же привести при каждом их вызове и hello службой Azure Stream Analytics не вести журнал вызовов функций и возвращены результаты. Если функция возвращает другой результат на hello того же события, повторяемость не гарантируется при перезапуске задания пользователем или службой hello Stream Analytics.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Добавьте определяемую пользователем функцию JavaScript в hello портал Azure
toocreate простой JavaScript определяемой пользователем функции в существующее задание Stream Analytics, выполните следующие действия:

1.  Найдите задание Stream Analytics в hello портал Azure.
2.  В разделе **топология задания** выберите нужную функцию. Откроется пустой список функций.
3.  Выберите toocreate новой определяемой пользователем функции, **добавить**.
4.  На hello **новая функция** колонке для **тип функции**выберите **JavaScript**. Функция шаблона по умолчанию отображается в редакторе hello.
5.  Для hello **псевдоним определяемая пользователем Функция**, введите **hex2Int**и измените реализацию функции hello следующим образом:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Щелкните **Сохранить**. Функции отображается в списке hello функции.
7.  Выберите hello новый **hex2Int** функцией и проверьте определение функции hello. Все функции имеют **определяемой пользователем функции** префикс toohello добавлена функция псевдоним. Требуется слишком*включать префикс hello* при вызове функции hello в запросе Stream Analytics. В нашем примере нужно вызывать функцию **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Вызов определяемой пользователем функции из запроса

1. В hello редактор запросов, в разделе **ТОПОЛОГИИ задания**выберите **запроса**.
2.  Изменение запроса, а затем вызвать hello определяемой пользователем функции, следующим образом:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  hello tooupload образец файла данных, щелкните правой кнопкой мыши hello задания ввода.
4.  tootest ваш запрос, выберите **теста**.


## <a name="supported-javascript-objects"></a>Поддерживаемые объекты JavaScript
Определяемые пользователем функции JavaScript в Azure Stream Analytics могут использовать все стандартные встроенные объекты JavaScript. Список этих объектов вы найдете [здесь](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Преобразование типов Stream Analytics и JavaScript

Существуют различия в hello типы, поддерживающие язык запросов Stream Analytics hello и JavaScript. В этой таблице перечислены hello преобразование сопоставления между двумя hello.

Stream Analytics | JavaScript
--- | ---
bigint | Номер (JavaScript может представлять только целые числа вверх tooprecisely 2 ^ 53)
DateTime | Дата (JavaScript поддерживает только миллисекунды)
double | Number
nvarchar(MAX) | Строка
Record | Объект
Массив, | Массив,
NULL | Null


Ниже описаны преобразования из типов JavaScript в типы Stream Analytics.


JavaScript | Анализ потока
--- | ---
Number | Bigint (если число hello round и между долго. MinValue и долго. MaxValue; в противном случае — double)
Дата | DateTime
Строка | nvarchar(MAX)
Объект | Record
Массив, | Массив,
NULL, не определено | NULL
Любой другой тип (например, функция или ошибка) | Не поддерживается (возникает ошибка времени выполнения)

## <a name="troubleshooting"></a>Устранение неполадок
Ошибки среды выполнения JavaScript считаются неустранимыми и подключаемых через журнал действий hello. Журнал hello tooretrieve, hello портал Azure, откройте tooyour задание и выберите **журнал действий**.


## <a name="other-javascript-user-defined-function-patterns"></a>Другие методы использования определяемой пользователем функции

### <a name="write-nested-json-toooutput"></a>Записи вложенных toooutput JSON
Если имеются дополнительные инструкции обработки шаг, который используется в качестве входных данных выходные данные задания Stream Analytics, и его требуется формат JSON, можно написать toooutput строка JSON. Следующий пример Hello вызывает hello **JSON.stringify()** функции toopack все пары "имя значение" hello входные данные и записывают их в виде одно строковое значение в выходных данных.

**Определение определяемой пользователем функции JavaScript:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Пример запроса**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).
* [Azure Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics).
