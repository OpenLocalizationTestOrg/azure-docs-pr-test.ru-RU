---
title: "Определяемые пользователем функции JavaScript в Azure Stream Analytics | Документация Майкрософт"
description: "Выполнение расширенных запросов с помощью определяемых пользователем функций JavaScript"
keywords: "javascript, определяемые пользователем функции, udf"
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e8c1c784a598416b478d1430258201053185fdee
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Определяемые пользователем функции JavaScript в Azure Stream Analytics
Azure Stream Analytics поддерживает определяемые пользователем функции, написанные на языке JavaScript. Благодаря обширному набору методов, которые предоставляют объекты JavaScript **String**, **RegExp**, **Math**, **Array** и **Date**, в заданиях Stream Analytics стало проще создавать сложные преобразования данных.

## <a name="javascript-user-defined-functions"></a>Определяемые пользователем функции JavaScript
Определяемые пользователем функции JavaScript поддерживают скалярные вычислительные функции без отслеживания состояния, не требующие внешнего подключения. Возвращаемое значение функции может быть только скалярным (одиночным). Добавив в задание определяемую пользователем функцию JavaScript, вы сможете использовать ее в любом месте запроса, например во встроенной скалярной функции.

Ниже приведены некоторые сценарии, в которых могут пригодиться определяемые пользователем функции JavaScript.
* Анализ и обработка строки с использованием функций регулярных выражений, например **Regexp_Replace()** или **Regexp_Extract()**.
* Декодирование и кодирование данных, например преобразование двоичных данных в шестнадцатеричные.
* Математические вычисления с помощью объекта JavaScript **Math**.
* Операции с массивами, такие как сортировка, присоединение, поиск и заполнение.

Вот некоторые действия, которые невозможно выполнить в Stream Analytics с помощью определяемой пользователем функции JavaScript.
* Вызов внешних конечных точек REST, например выполнение обратного разрешения IP-адресов или извлечение ссылочных данных из внешнего источника.
* Сериализация или десериализация входных и выходных данных в пользовательский формат сообщения.
* Создание пользовательских статистических функций.

Следует избегать использования таких функций, как **Date.GetDate()** или **Math.random()**, хотя они не запрещены в определении функции. Эти функции возвращают **разные** результаты при каждом вызове, а служба Azure Stream Analytics не ведет журнал вызовов и возвращаемых результатов для функций. Если функция возвращает разные результаты для одних и тех же событий, невозможно гарантировать повторяемость при перезапуске задания пользователем или службой Stream Analytics.

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a>Добавление определяемой пользователем функции JavaScript на портале Azure
Чтобы создать простую определяемую пользователем функцию JavaScript в существующем задании Stream Analytics, выполните следующие действия.

1.  Найдите нужное задание Stream Analytics на портале Azure.
2.  В разделе **топология задания** выберите нужную функцию. Откроется пустой список функций.
3.  Чтобы создать определяемую пользователем функцию, выберите **Добавить**.
4.  В колонке **Новая функция** для параметра **Тип функции** выберите значение **JavaScript**. В редакторе отобразится стандартный шаблон функции.
5.  В качестве значения для параметра **UDF alias**, введите **hex2Int**, затем измените реализацию функции, как показано ниже.

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Щелкните **Сохранить**. Функция отобразится в списке функций.
7.  Выберите новую функцию **hex2Int** и проверьте определение функции. Для всех пользовательских функций к псевдониму добавляется префикс **UDF**. Этот *префикс нужно использовать* при вызове функции из запроса Stream Analytics. В нашем примере нужно вызывать функцию **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Вызов определяемой пользователем функции из запроса

1. В редакторе запросов для параметра **Топология задания** выберите значение **Запрос**.
2.  Откройте режим редактирования запроса и добавьте вызов определяемой пользователем функции, как показано здесь:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  Чтобы передать пример файла данных, щелкните правой кнопкой мыши входные данные задания.
4.  Чтобы проверить запрос, выберите **Тестирование**.


## <a name="supported-javascript-objects"></a>Поддерживаемые объекты JavaScript
Определяемые пользователем функции JavaScript в Azure Stream Analytics могут использовать все стандартные встроенные объекты JavaScript. Список этих объектов вы найдете [здесь](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Преобразование типов Stream Analytics и JavaScript

Существуют различия между типами, которые поддерживаются в языке запросов Stream Analytics и в JavaScript. В следующей таблице перечислены сопоставления преобразования между этими типами.

Анализ потока | JavaScript
--- | ---
bigint | Число (JavaScript может представлять целые числа только до значения 2^53).
DateTime | Дата (JavaScript поддерживает только миллисекунды)
double | Number
nvarchar(MAX) | Строка
Record | Объект
Массив, | Массив,
NULL | Null


Ниже описаны преобразования из типов JavaScript в типы Stream Analytics.


JavaScript | Анализ потока
--- | ---
Number | Значение типа bigint, если это целое число в диапазоне от long.MinValue до long.MaxValue. Иначе используется тип double.
Дата | DateTime
Строка | nvarchar(MAX)
Объект | Record
Массив, | Массив,
NULL, не определено | NULL
Любой другой тип (например, функция или ошибка) | Не поддерживается (возникает ошибка времени выполнения)

## <a name="troubleshooting"></a>Устранение неполадок
Ошибки времени выполнения JavaScript считаются неустранимыми и регистрируются в журнале действий. Чтобы получить этот журнал, перейдите на портале Azure к нужному заданию и щелкните **Журнал действий**.


## <a name="other-javascript-user-defined-function-patterns"></a>Другие методы использования определяемой пользователем функции

### <a name="write-nested-json-to-output"></a>Вывод вложенных значений JSON
Если вы используете этап обработки результатов, на котором входными данными являются выходные данные в формате JSON задания Stream Analytics, вам нужно записать строку JSON в выходные данные. Приведенный ниже пример вызывает функцию **JSON.stringify()**, которая упаковывает все полученные пары "имя — значение" и передает их единой строкой в качестве выходных данных.

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
* [Введение в Azure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).
* [Azure Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics).
