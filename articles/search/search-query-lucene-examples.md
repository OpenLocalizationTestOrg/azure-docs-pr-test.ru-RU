---
title: "Примеры запросов aaaLucene для службы поиска Azure | Документы Microsoft"
description: "Синтаксис запросов Lucene для поиска нечетких соответствий, поиска с учетом расположения, повышения приоритета слов, поиска по регулярным выражениям и поиска с использованием подстановочных знаков."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Примеры синтаксиса запросов Lucene для создания запросов в службе поиска Azure
При написании запросов для поиска Azure, можно использовать либо по умолчанию hello [синтаксис простого запроса](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) или вариант hello [Lucene синтаксического анализа запросов в поиске Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Hello синтаксического анализа Lucene запросов поддерживает более сложные конструкциях запроса, например запросов в области полей нечеткого поиска, поиск по сходству, повышение термин и поиска регулярного выражения.

В этой статье можно пошагово проходить примеров, демонстрирующих операций запросов, доступных при использовании hello полный синтаксис.

## <a name="viewing-hello-examples-in-jsfiddle"></a>Просмотр примеров hello в JSFiddle

Все примеры hello в этой статье, исполняемые запросы, выполняемые к предварительно загруженных индекса поиска в [JSFiddle](https://jsfiddle.net), редактор кода для тестирования скриптов и HTML. 

toorun их, щелкните правой кнопкой мыши hello запроса пример URL-адреса tooopen JSFiddle в отдельном окне браузера.

> [!NOTE]
> Hello следующие примеры использования поиска индекса, состоящего из доступных заданий на основе набора данных, предоставляемые hello [OpenData Город Нью-Йорк](https://nycopendata.socrata.com/) "инициатива". Эти данные не являются текущими или завершенными. Индекс Hello находится на "песочницы", предоставляемый корпорацией Майкрософт. Необязательно подписки Azure или tootry поиска Azure эти запросы.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Как tooinvoke полного синтаксического анализа Lucene

Все примеры hello в этой статье укажите hello **queryType = полный** поиска параметр, указывающий, hello полный синтаксис может быть обработано hello синтаксического анализа Lucene запросов. 

**Пример 1** — hello щелкните правой кнопкой мыши следующие tooopen фрагмент запроса его в другом браузере страницу, которая загружает JSFiddle и запускает hello запроса:

* [&queryType=full&search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

В новом окне браузера hello hello исходного кода JavaScript и HTML выходные данные представлены рядом друг с другом. Hello скрипт ссылается на полный запрос (не только hello фрагмент кода, как показано в ссылке hello). отображается полный запрос Hello hello URL-адресов для каждого примера. 

Этот запрос возвращает документы из нашего индекса вакансий New York City (nycjobs, загруженного в службу "песочницы"). Для краткости hello запроса указывает, что возвращаются только заголовки бизнеса. Hello полный базовый запрос выглядит следующим образом:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Hello **searchFields** параметр ограничивает hello поиска toojust hello бизнеса поле "Название". Hello **queryType** задано слишком**полного**, отдает hello toouse поиска Azure синтаксического анализа Lucene запросов для этого запроса.

> [!NOTE]
> Общие сведения об обработке запросов см. в статье [Как работает полнотекстовый поиск в службе поиска Azure](search-lucene-query-architecture.md). Дополнительные сведения о параметрах поиска см. в разделе [Поиск документов (REST API поиска Azure)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).
>

### <a name="fielded-query-operation"></a>Операция запроса, относящегося к полю
Примеры hello в этой статье можно изменить, указав **fieldname:searchterm** toodefine конструкции операции были запроса, где поле hello одно слово, и условие поиска hello также задано одно слово или фразу, При необходимости с логическими операторами. Hello ниже приведены некоторые примеры.

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

Быть tooput убедиться, что несколько строк в кавычках, если требуется, чтобы оба toobe строки вычисляется как единая сущность, поскольку в данном случае поиск два уникальных городов, в поле расположение hello. Кроме того, убедитесь, оператор hello написано с прописной буквы как видеть не и AND.

указанное в поле Hello **fieldname:searchterm** должен быть полем для поиска. Дополнительные сведения об использовании атрибутов индекса в определениях полей см. в статье [Create Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) (Создание индексов (REST API службы поиска Azure)).

**Пример 2** — щелкните правой кнопкой мыши hello следующий запрос фрагмента этот запрос выполняет поиск наименований бизнеса с hello терминов старший в них, но не к младшему:

* [&queryType=full&search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Пример поиска нечетких соответствий
Операция поиска нечетких соответствий позволяет найти совпадения в словах с аналогичной конструкцией. В [документации Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html) поиск нечетких соответствий основан на [расстоянии Дамерау — Левенштейна](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo нечеткого поиска, добавления hello тильды «~» символа в конце hello одно слово, с необязательным параметром, значение между 0 и 2, указывающее hello расстояния. Например, "blue~" или "blue~1" вернет результаты с "blue", "blues" и "glue".

**Пример 3** --следующий hello щелкните правой кнопкой мыши запрос, фрагмент кода. Этот запрос выполняет поиск заданий с сопоставление термин hello (где он неправильно указано):

* [&queryType=full&search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Нечеткие запросы не [анализируются](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), что может оказаться непредвиденным, если ожидается морфологический поиск или лемматизация. Лексический анализ выполняется только для полными терминами (запрос термина или запрос фразы). Типы запросов с неполными условия (префикс запрос, шаблон запроса, запрос регулярных выражений, Нечеткий уточняющий запрос) добавляются непосредственно toohello дерево запроса, минуя этап анализа hello. Hello только преобразование, выполненное на условиях неполные запроса строчной версии.
>

## <a name="proximity-search-example"></a>Пример поиска с учетом расположения
Поиск с учетом расположения, используемые toofind термины, которые находятся рядом друг с другом в документе. Вставка тильды «~» символа в конце hello фразы следуют hello число слов, образующих hello выражение с учетом границ. Например, «гостиницы аэропорта» ~ 5 поиск гостиницы условия hello и аэропорта 5 слова в документе.

**Пример 4** --hello запросов щелкните правой кнопкой мыши. Поиск задания с hello термин «ведущего аналитика», где разделены по словам не более одного:

* [&queryType=full&search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Пример 5** --попробуйте снова удалить слова hello между hello термин «ведущего аналитика».

* [&queryType=full&search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Пример повышения приоритета термина
Повышение приоритета термин относится tooranking документе выше, если он содержит hello повышенного термин относительный toodocuments, которые не содержат термин hello. Этот тип запроса отличается от профилей повышения, так как они повышают приоритет определенных полей, а не определенных слов. Hello примере помогает проиллюстрировать hello различия.

Рассмотрим профиль оценки, который повышает соответствует определенные поля, такие как **жанр** в примере musicstoreindex hello. Термин повышение приоритета может быть используется toofurther повышения определенных условий поиска, выше, чем другие. Например «рок ^ 2 электронных» делают документы, содержащие слова hello в hello **жанр** поля выше, чем другие поля для поиска в индексе hello. Кроме того документы, содержащие условия поиска hello «рок» ранжируются выше, чем hello другие условия поиска «электронных», в результате hello термин boost значение (2).

tooboost указать условия, используйте курсор hello, «^», символ с коэффициент повышения приоритета (число) в конце hello hello условия поиска. Здравствуйте, высокий коэффициент повышения приоритета hello, hello большей степени hello термин будет относительный tooother условия поиска. По умолчанию hello коэффициент повышения приоритета — 1. Несмотря на то, что коэффициент повышения приоритета hello должно быть положительным, он может быть меньше 1 (например, 0,2).

**Пример 6** --hello запросов щелкните правой кнопкой мыши. Поиск заданий с hello термин «компьютера аналитик», где указан нет результатов с компьютера слов и аналитик, но вверху hello hello результаты находятся аналитик заданий.

* [&queryType=full&search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Пример 7** --попробуйте еще раз, это повышение времени результатов с компьютером термин hello через аналитик термин hello Если оба слова не существуют.

* [&queryType=full&search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Пример поиска с использованием регулярного выражения
Поиск регулярного выражения совпадения в соответствии с содержимым hello между косые черты «/», как документированные в hello [класса RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Пример 8** --hello запросов щелкните правой кнопкой мыши. Поиск заданий с hello термин старший или молодых.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

Hello URL-адрес для этого примера не будет правильно подготовлен к странице приветствия. Чтобы избежать этого скопируйте URL-адрес hello ниже и вставьте его в URL-адрес браузера hello:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Пример поиска с использованием подстановочных знаков
Вы можете использовать распознаваемый синтаксис для поиска с использованием одного (?) или нескольких (\*) подстановочных знаков. Обратите внимание, запрос Lucene hello, средство синтаксического анализа поддерживает использование этих символов с единый термин и не фразу hello.

**Пример 9** --hello запросов щелкните правой кнопкой мыши. Найти задания, содержащие hello префикс «prog», включающий заголовки бизнеса с hello термины программирования и программиста в нем.

* [&queryType=full&$select=business_title&search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

Символ "*" или "?" символ как первый символ hello поиска.

## <a name="next-steps"></a>Дальнейшие действия
Попробуйте указать hello синтаксического анализа Lucene запросов в коде. Hello ссылкам объясняется, как tooset копирование поиска запрашивает .NET и API-интерфейса REST hello. ссылки Hello использовать простой синтаксис hello по умолчанию, поэтому вам необходимо будет tooapply вы узнали из этой статьи toospecify hello **queryType**.

* [Запросить индекс поиска Azure с помощью hello .NET SDK](search-query-dotnet.md)
* [Запросить индекс поиска Azure с помощью API-интерфейса REST hello](search-query-rest-api.md)

## <a name="see-also"></a>См. также

 [Как работает полнотекстовый поиск в службе поиска Azure](search-lucene-query-architecture.md)