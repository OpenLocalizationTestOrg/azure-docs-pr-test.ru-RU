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
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Построение строк фильтра для hello конструктора таблиц
## <a name="overview"></a>Обзор
Здравствуйте, toofilter данные в таблице Azure, которая отображается в Visual Studio **конструктор таблиц**, создать строку фильтра и ввести в поле фильтра hello. синтаксис строки фильтра Hello определяется hello службы данных WCF — примерно tooa SQL предложение WHERE, но отправляется toohello службе таблиц через HTTP-запроса. Hello **конструктор таблиц** hello обрабатывает соответствующую кодировку, поэтому toofilter по значению свойства, потребуется только ввести имя свойства hello, оператор сравнения, значение условия, и при необходимости отфильтровать логический оператор в hello поле. Как при построении URL-адрес таблицы hello tooquery через hello не требуется параметр запроса hello $filter tooinclude [Справочник API REST служб хранилища](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Службы данных WCF Hello основаны на hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Дополнительные сведения о параметр системного запроса фильтрации hello (**$filter**), hello в разделе [соглашения об URI OData спецификации](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Операторы сравнения
Hello следующие логические операторы поддерживаются для всех типов свойств:

| Логический оператор | Описание | Пример строки фильтра |
| --- | --- | --- |
| eq |Равно |City eq 'Redmond' |
| gt |Больше |Price gt 20 |
| ge |Больше или равно слишком|Price ge 10 |
| lt |Меньше |Price lt 20 |
| le |Меньше или равно |Price le 100 |
| ne |Не равно |City ne 'London' |
| и |и |Price le 200 and Price gt 3.5 |
| или |или |Price le 3.5 or Price gt 200 |
| not |not |not isAvailable |

При создании строки фильтра hello следующие правила, важные.

* Используйте логические операторы hello toocompare tooa значения свойства. Обратите внимание, что возможные toocompare tooa динамическое значение свойства; одна часть hello выражение должно быть константой.
* Все части hello строки фильтра учитывается регистр.
* должен иметь постоянное значение Hello hello и тех же данных введите в качестве свойства hello в порядке для hello фильтра tooreturn правильные результаты. Дополнительные сведения о поддерживаемых типах свойств см. в разделе [hello основные сведения о модели данных службы таблиц](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Фильтрация по строковым свойствам
При фильтрации по строковым свойствам заключайте hello строковую константу в одинарные кавычки.

далее примере фильтры hello Hello **PartitionKey** и **RowKey** свойства; дополнительные не ключевые свойства также могут быть добавлены toohello строку фильтра:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Каждое выражение фильтра можно заключить в круглые скобки, хотя это не обязательно:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Обратите внимание, что hello служба таблиц не поддерживает запросы подстановочный знак, они не поддерживаются в конструкторе таблиц hello либо. Тем не менее можно выполнить с помощью операторов сравнения на hello желаемый префикс сопоставления префиксов. Hello следующий пример возвращает сущности с свойство LastName начинается с hello буквы «A».

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Фильтрация по числовым свойствам
toofilter на целое число или число с плавающей запятой, укажите номер hello без кавычек.

Следующий пример возвращает все сущности свойства Age, значения которых больше 30.

    Age gt 30

Этот пример возвращает все сущности со значением свойства AmountDue меньше или равен too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Фильтрация по логическим свойствам
Укажите toofilter к логическому значению **true** или **false** без кавычек.

Hello следующий пример возвращает все сущности которых hello свойство IsActive имеет значение слишком**true**:

    IsActive eq true

Можно также написать этот критерий фильтра без hello логический оператор. В следующем примере hello, hello служба таблиц также вернет все сущности которых свойство IsActive имеет **true**:

    IsActive

все сущности, в которых свойство IsActive имеет значение false, можно использовать hello не tooreturn оператор:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Фильтрация по свойствам DateTime
toofilter в значении даты и времени, укажите hello **datetime** ключевое слово, за которым введите константу даты и времени hello в одинарные кавычки. Константа даты времени Hello должна быть в комбинированном формате UTC, как описано в [форматирование значений свойств DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Следующий пример Hello возвращает сущности, где свойство CustomerSince hello — tooJuly равно 10, 2008.

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
